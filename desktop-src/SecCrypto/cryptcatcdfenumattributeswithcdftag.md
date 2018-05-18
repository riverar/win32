﻿---
Description: 'Enumerates the attributes of member files in the CatalogFiles section of a catalog definition file (CDF).'
ms.assetid: '056a5186-a37c-4255-aaa5-4c6e60f5392e'
title: CryptCATCDFEnumAttributesWithCDFTag function
---

# CryptCATCDFEnumAttributesWithCDFTag function

\[The **CryptCATCDFEnumAttributesWithCDFTag** function is available for use in the operating systems specified in the Requirements section. It may be altered or unavailable in subsequent versions.\]

The **CryptCATCDFEnumAttributesWithCDFTag** function enumerates the attributes of member files in the **CatalogFiles** section of a catalog definition file (CDF). **CryptCATCDFEnumAttributesWithCDFTag** is called by [MakeCat](makecat.md).

> [!Note]  
> This function has no associated header file or import library. To call this function, you must create a user-defined header file and use the [**LoadLibrary**](base.loadlibrary) and [**GetProcAddress**](base.getprocaddress) functions to dynamically link to Mssign32.dll.

 

## Syntax


```C++
CRYPTCATATTRIBUTE* WINAPI CryptCATCDFEnumAttributesWithCDFTag(
  _In_ CRYPTCATCDF                  *pCDF,
  _In_ LPWSTR                       pwszMemberTag,
  _In_ CRYPTCATMEMBER               *pMember,
  _In_ CRYPTCATATTRIBUTE            *pPrevAttr,
  _In_ PFN_CDF_PARSE_ERROR_CALLBACK pfnParseError
);
```



## Parameters

<dl> <dt>

*pCDF* \[in\]
</dt> <dd>

A pointer to a [**CRYPTCATCDF**](cryptcatcdf.md) structure.

</dd> <dt>

*pwszMemberTag* \[in\]
</dt> <dd>

A pointer to a **null**-terminated string that identifies the catalog file member.

</dd> <dt>

*pMember* \[in\]
</dt> <dd>

A pointer to a [**CRYPTCATMEMBER**](cryptcatmember.md) structure that contains the member information.

</dd> <dt>

*pPrevAttr* \[in\]
</dt> <dd>

A pointer to a [**CRYPTCATATTRIBUTE**](cryptcatattribute.md) structure for a file member attribute in the CDF pointed to by *pCDF*.

</dd> <dt>

*pfnParseError* \[in\]
</dt> <dd>

A pointer to a user-defined function to handle file parse errors.

</dd> </dl>

## Return value

Upon success, this function returns a pointer to a [**CRYPTCATATTRIBUTE**](cryptcatattribute.md) structure. The **CryptCATCDFEnumAttributesWithCDFTag** function returns a **NULL** pointer if it fails.

## Remarks

You typically call this function in a loop to enumerate all of the catalog file member attributes in a CDF. Before entering the loop, set *pPrevAttr* to **NULL**. The function returns a pointer to the first attribute. Set *pPrevAttr* to the return value of the function for subsequent iterations of the loop.

## Examples

The following example shows the correct sequence of assignments for the *pPrevAttr* parameter (`pAttr`).


```C++
    CRYPTCATATTRIBUTE   *pAttr;
    CRYPTCATMEMBER      *pMember;
    LPWSTR              pwszMemberTag;
    CRYPTCATCDF         *pCDF;

    pCDF = CryptCATCDFOpen(L"myCDF", NULL);
    

    pMember = NULL;
    pwszMemberTag = NULL;

    while (pwszMemberTag = CryptCATCDFEnumMembersByCDFTagEx(pCDF,
                                                            pwszMemberTag,
                                                            NULL,
                                                            &amp;pMember,
                                                            FALSE,
                                                            NULL))
    {
        pAttr = NULL;

        while (pAttr = CryptCATCDFEnumAttributesWithCDFTag(pCDF,
                                                           pwszMemberTag,
                                                           pMember,
                                                           pAttr,
                                                           DisplayParseError))
        {
            //do something with pAttr
        }

    }

    CryptCATCDFClose(pCDF);
```



## Requirements



|                                     |                                                                                         |
|-------------------------------------|-----------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows XP \[desktop apps only\]<br/>                                             |
| Minimum supported server<br/> | Windows Server 2003 \[desktop apps only\]<br/>                                    |
| DLL<br/>                      | <dl> <dt>Wintrust.dll</dt> </dl> |



## See also

<dl> <dt>

[MakeCat](makecat.md)
</dt> <dt>

[**CRYPTCATATTRIBUTE**](cryptcatattribute.md)
</dt> <dt>

[**CRYPTCATCDF**](cryptcatcdf.md)
</dt> <dt>

[**CRYPTCATMEMBER**](cryptcatmember.md)
</dt> <dt>

[**GetProcAddress**](base.getprocaddress)
</dt> <dt>

[**LoadLibrary**](base.loadlibrary)
</dt> </dl>

 

 



