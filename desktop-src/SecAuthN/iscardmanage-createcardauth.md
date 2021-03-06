---
Description: Creates an ISCardAuth interface.
ms.assetid: a091e361-416e-45c9-8077-617b16db654c
title: ISCardManage::CreateCardAuth method
ms.topic: article
ms.date: 05/31/2018
topic_type: 
- APIRef
- kbSyntax
api_name: 
- ISCardManage.CreateCardAuth
api_type: 
- COM
api_location: 
---

# ISCardManage::CreateCardAuth method

\[The **CreateCardAuth** method is available for use in the operating systems specified in the Requirements section. It is not available for use in Windows Server 2003 with Service Pack 1 (SP1) and later, Windows Vista, Windows Server 2008, and subsequent versions of the operating system. The [Smart Card Modules](https://msdn.microsoft.com/en-us/library/Dd627652(v=VS.85).aspx) provide similar functionality.\]

The **CreateCardAuth** method creates an [**ISCardAuth**](iscardauth.md) interface.

## Syntax


```C++
HRESULT CreateCardAuth(
  [out] ISCardAuth **ppISCardAuth
);
```



## Parameters

<dl> <dt>

*ppISCardAuth* \[out\]
</dt> <dd>

Returned pointer to the created interface.

</dd> </dl>

## Return value

The method returns one of the following possible values:



| Return code                                                                                   | Description                                            |
|-----------------------------------------------------------------------------------------------|--------------------------------------------------------|
| <dl> <dt>**S\_OK**</dt> </dl>          | Operation completed successfully.<br/>           |
| <dl> <dt>**E\_INVALIDARG**</dt> </dl>  | The *ppISCardAuth* parameter is not valid.<br/>  |
| <dl> <dt>**E\_POINTER**</dt> </dl>     | A bad pointer was passed in *ppISCardAuth*.<br/> |
| <dl> <dt>**E\_OUTOFMEMORY**</dt> </dl> | Out of memory.<br/>                              |



 

## Remarks

For a list of all the methods defined by this interface, see [**ISCardManage**](iscardmanage.md).

In addition to the COM error codes listed above, this interface may return a [*smart card*](https://msdn.microsoft.com/en-us/library/ms721625(v=VS.85).aspx) error code if a smart card function was called to complete the request. For more information, see [Smart Card Return Values](authentication-return-values.md).

## Requirements



|                                     |                                                      |
|-------------------------------------|------------------------------------------------------|
| Minimum supported client<br/> | Windows XP \[desktop apps only\]<br/>          |
| Minimum supported server<br/> | Windows Server 2003 \[desktop apps only\]<br/> |
| End of client support<br/>    | Windows XP<br/>                                |
| End of server support<br/>    | Windows Server 2003<br/>                       |



## See also

<dl> <dt>

[**ISCardManage**](iscardmanage.md)
</dt> </dl>

 

 




