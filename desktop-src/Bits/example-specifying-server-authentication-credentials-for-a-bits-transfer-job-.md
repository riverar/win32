---
title: Example Specifying Server Authentication Credentials for a BITS Transfer Job
description: You can specify different authentication schemes for a Background Intelligent Transfer Service (BITS) transfer job.
ms.assetid: '31db38f6-3639-4042-97f2-4f9d78942e15'
---

# Example: Specifying Server Authentication Credentials for a BITS Transfer Job

You can specify different authentication schemes for a Background Intelligent Transfer Service (BITS) transfer job.

The following procedure gets an authentication scheme and creates an authentication identity structure. Then the application creates a BITS download job and sets the credentials for the job. After the job is created, the application gets a pointer to a callback interface and polls for the status of the BITS transfer job. After the job is complete, it is removed from the queue.

This example uses the header and implementation defined in [Example: Common Classes](common-classes.md).

**To specify server authentication credentials for a BITS transfer job**

1.  Create a container structure that maps [**BG\_AUTH\_SCHEME**](bg-auth-scheme.md) values to scheme names.

    ```C++
    struct
    {
        LPCWSTR        Name;
        BG_AUTH_SCHEME Scheme;
    }
    SchemeNames[] =
    {
        { L"basic",      BG_AUTH_SCHEME_BASIC },
        { L"digest",     BG_AUTH_SCHEME_DIGEST },
        { L"ntlm",       BG_AUTH_SCHEME_NTLM },
        { L"negotiate",  BG_AUTH_SCHEME_NEGOTIATE },
        { L"passport",   BG_AUTH_SCHEME_PASSPORT },

        { NULL,         BG_AUTH_SCHEME_BASIC }
    };
    ```

    

2.  Initialize COM parameters by calling the CCoInitializer function. For more information about the CCoInitializer function, see [Example: Common Classes](common-classes.md).
3.  Prepare a [**BG\_AUTH\_CREDENTIALS**](bg-auth-credentials.md) structure. The example uses the [SecureZeroMemory]( http://go.microsoft.com/fwlink/p/?linkid=162389) function to clear the memory locations associated with the sensitive information. The [SecureZeroMemory]( http://go.microsoft.com/fwlink/p/?linkid=162389) function is defined in WinBase.h.
4.  Use the GetScheme function to get the authentication scheme to use to connect to the server.

    ```C++
    bool GetScheme( LPCWSTR s, BG_AUTH_SCHEME *scheme )
    {
        int i;

        i = 0;
        while (SchemeNames[i].Name != NULL)
        {
            if (0 == _wcsicmp( s, SchemeNames[i].Name ))
            {

                *scheme = SchemeNames[i].Scheme;
                return true;
            }

            ++i;
        }

        return false;
    }
    ```

    

5.  Populate the [**BG\_AUTH\_CREDENTIALS**](bg-auth-credentials.md) structure with the authentication scheme returned by the GetScheme function and the user name and password that were passed into the ServerAuthentication function.
6.  Get a pointer to the [**IBackgroundCopyJob**](ibackgroundcopyjob.md) interface (pJob).
7.  Initialize COM process security by calling [CoInitializeSecurity](http://go.microsoft.com/fwlink/p/?linkid=162390). BITS requires at least the IMPERSONATE level of impersonation. BITS fails with E\_ACCESSDENIED if the correct impersonation level is not set.
8.  Get a pointer to the [**IBackgroundCopyManager**](ibackgroundcopymanager.md) interface, and obtain the initial locator to BITS by calling the [CoCreateInstance]( http://go.microsoft.com/fwlink/p/?linkid=162386) function.
9.  Create a BITS transfer job by calling the [**IBackgroundCopyManager::CreateJob**](ibackgroundcopymanager-createjob.md) method.
10. Get a pointer to the CNotifyInterface callback interface and call the [**IBackgroundCopyJob::SetNotifyInterface**](ibackgroundcopyjob-setnotifyinterface.md) method to receive notification of job-related events. For more information about CNotifyInterface, see [Example: Common Classes](common-classes.md).
11. Call the [**IBackgroundCopyJob::SetNotifyFlags**](ibackgroundcopyjob-setnotifyflags.md) method to set the types of notifications to receive. In this example, the **BG\_NOTIFY\_JOB\_TRANSFERRED** and **BG\_NOTIFY\_JOB\_ERROR** flags are set.
12. Get a pointer to the [**IBackgroundCopyJob2**](ibackgroundcopyjob2.md) interface. Use the **IBackgroundCopyJob2** pointer to set additional properties on the job. This program uses the [**IBackgroundCopyJob2::SetCredentials**](ibackgroundcopyjob2-setcredentials.md) method to set the credentials for the BITS transfer job.
13. Add files to the BITS transfer job by calling [**IBackgroundCopyJob::AddFile**](ibackgroundcopyjob-addfile.md). In this example, the **IBackgroundCopyJob::AddFile** method uses the remoteFile and localFile variables that were passed into the ServerAuthentication function.
14. After the file is added, call [**IBackgroundCopyJob::Resume**](ibackgroundcopyjob-resume.md) to resume the job.
15. Set up a while loop to wait for Quit Message from the callback interface while the job is transferring.

    > [!Note]  
    > This step is necessary only if the COM apartment is a single-threaded apartment. For more information, see [Single-Threaded Apartments](http://go.microsoft.com/fwlink/p/?linkid=163801).

     

    ```C++
    // Wait for QuitMessage from CallBack
        DWORD dwLimit = GetTickCount() + (15 * 60 * 1000);  // set 15 minute limit
        while (dwLimit > GetTickCount())
        {
            MSG msg;

            while (PeekMessage(&amp;msg, NULL, 0, 0, PM_REMOVE)) 
            { 
                // If it is a quit message, exit.
                if (msg.message == WM_QUIT) 
                {
                    return;
                }

                // Otherwise, dispatch the message.
                DispatchMessage(&amp;msg); 
            } // End of PeekMessage while loop
        }
    ```

    

    The preceding loop uses the [GetTickCount](http://go.microsoft.com/fwlink/p/?linkid=162392) function to retrieve the number of milliseconds that have elapsed since the job started transferring.

16. After the BITS transfer job is complete, remove the job from the queue by calling [**IBackgroundCopyJob::Complete**](ibackgroundcopyjob-complete.md).

The following code example specifies server authentication credentials for a BITS transfer job.


```C++
#include <bits.h>
#include <bits4_0.h>
#include <stdio.h>
#include <tchar.h>
#include <lm.h>
#include <iostream>
#include <exception>
#include <string>
#include <atlbase.h>
#include <memory>
#include <new>
#include "CommonCode.h"

//
// Retrieve BG_AUTH_SCHEME from scheme name.
//
//
struct
{
    LPCWSTR        Name;
    BG_AUTH_SCHEME Scheme;
}
SchemeNames[] =
{
    { L"basic",      BG_AUTH_SCHEME_BASIC },
    { L"digest",     BG_AUTH_SCHEME_DIGEST },
    { L"ntlm",       BG_AUTH_SCHEME_NTLM },
    { L"negotiate",  BG_AUTH_SCHEME_NEGOTIATE },
    { L"passport",   BG_AUTH_SCHEME_PASSPORT },

    { NULL,         BG_AUTH_SCHEME_BASIC }
};

bool GetScheme( LPCWSTR s, BG_AUTH_SCHEME *scheme )
{
    int i;

    i = 0;
    while (SchemeNames[i].Name != NULL)
    {
        if (0 == _wcsicmp( s, SchemeNames[i].Name ))
        {

            *scheme = SchemeNames[i].Scheme;
            return true;
        }

        ++i;
    }

    return false;
}

void ServerAuthentication(const LPWSTR &amp;remoteFile, const LPWSTR &amp;localFile, const LPWSTR &amp;scheme, const LPWSTR &amp;username, const LPWSTR &amp;password)
{

 // If CoInitializeEx fails, the exception is unhandled and the program terminates  
 CCoInitializer coInitializer(COINIT_APARTMENTTHREADED);
    
    // Prepare the credentials structure.
    BG_AUTH_CREDENTIALS cred;
    ZeroMemory(&amp;cred, sizeof(cred));
    if (!GetScheme(scheme,&amp;cred.Scheme))
    {
        wprintf(L"Invalid authentication scheme specified\n");
        return;
    }

    cred.Target = BG_AUTH_TARGET_SERVER;
    cred.Credentials.Basic.UserName = username;
    if (0 == _wcsicmp(cred.Credentials.Basic.UserName, L"NULL"))
    {
        cred.Credentials.Basic.UserName = NULL;
    }

    cred.Credentials.Basic.Password = password;
    if (0 == _wcsicmp(cred.Credentials.Basic.Password, L"NULL"))
    {
        cred.Credentials.Basic.Password = NULL;
    }

    CComPtr<IBackgroundCopyJob> pJob;
    try
    {
        //The impersonation level must be at least RPC_C_IMP_LEVEL_IMPERSONATE.
        HRESULT hr = CoInitializeSecurity(NULL, 
            -1, 
            NULL, 
            NULL,
            RPC_C_AUTHN_LEVEL_CONNECT,
            RPC_C_IMP_LEVEL_IMPERSONATE,
            NULL, 
            EOAC_DYNAMIC_CLOAKING, 
            0);
        if (FAILED(hr))
        {
            throw MyException(hr, L"CoInitializeSecurity");
        }

        // Connect to BITS.
        CComPtr<IBackgroundCopyManager> pQueueMgr;
        hr = CoCreateInstance(__uuidof(BackgroundCopyManager), NULL,
            CLSCTX_LOCAL_SERVER,
            __uuidof(IBackgroundCopyManager),
            (void**)&amp;pQueueMgr);

        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"CoCreateInstance");
        }

        // Create a job.
        wprintf(L"Creating Job...\n");

        GUID guidJob;
        hr = pQueueMgr->CreateJob(L"BitsAuthSample",
            BG_JOB_TYPE_DOWNLOAD,
            &amp;guidJob,
            &amp;pJob);

        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"CreateJob");
        }

        // Set the File Completed call.
        CComPtr<CNotifyInterface> pNotify;
        pNotify = new CNotifyInterface();
        hr = pJob->SetNotifyInterface(pNotify);
        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"SetNotifyInterface");
        }
        hr = pJob->SetNotifyFlags(BG_NOTIFY_JOB_TRANSFERRED | 
            BG_NOTIFY_JOB_ERROR);

        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"SetNotifyFlags");
        }

        // Set credentials.
        CComPtr<IBackgroundCopyJob2> job2;
        hr = pJob.QueryInterface(&amp;job2);
        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"QueryInterface");
        }

        hr = job2->SetCredentials(&amp;cred);
        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"SetCredentials");
        }

        // Add a file.
        wprintf(L"Adding File to Job\n");
        hr = pJob->AddFile(remoteFile, localFile);
        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"AddFile");
        }

        //Resume the job.
        wprintf(L"Resuming Job...\n");
        hr = pJob->Resume();
        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"Resume");
        }
    }
    catch(const std::bad_alloc &amp;)
    {
        wprintf(L"Memory allocation failed");
        if (pJob)
        {
            pJob->Cancel();
        }

        return;
    }
    catch(const MyException &amp;ex)
    {
        wprintf(L"Error %x occurred during operation", ex.Error);
        if (pJob)
        {
            pJob->Cancel();
        }

        return;
    }

    wprintf(L"Transferring file and waiting for callback.\n");

    // Wait for QuitMessage from CallBack.
    DWORD dwLimit = GetTickCount() + (15 * 60 * 1000);  // set 15 minute limit
    while (dwLimit > GetTickCount())
    {
        MSG msg;

        while (PeekMessage(&amp;msg, NULL, 0, 0, PM_REMOVE)) 
        { 
            // If it is a quit message, exit.
            if (msg.message == WM_QUIT) 
            {
                return;
            }

            // Otherwise, dispatch the message.
            DispatchMessage(&amp;msg); 
        } // End of PeekMessage while loop
    }

    pJob->Cancel();
    return;
}

void _cdecl _tmain(int argc, LPWSTR* argv)
{   
    if (argc != 6)
    {
        wprintf(L"Usage:");
        wprintf(L"%s", argv[0]);
        wprintf(L" [remote name] [local name] [server authentication scheme =\"NTLM\"|\"NEGOTIATE\"|\"BASIC\"|\"DIGEST\"] [username] [password]\n");
        return;
    }

    ServerAuthentication(argv[1], argv[2], argv[3], argv[4], argv[5]); 

}
```



## Related topics

<dl> <dt>

[**IBackgroundCopyManager**](ibackgroundcopymanager.md)
</dt> <dt>

[**IBackgroundCopyJob**](ibackgroundcopyjob.md)
</dt> <dt>

[**IBackgroundCopyJob2**](ibackgroundcopyjob2.md)
</dt> <dt>

[Example: Common Classes](common-classes.md)
</dt> </dl>

 

 



