---
title: IVMVirtualMachine DetachUSBDevice method
description: Releases a USB device from a virtual machine.
ms.assetid: ae2b70b1-7bf3-4a84-9f05-4e91de93fa73
keywords:
- DetachUSBDevice method Virtual PC
- DetachUSBDevice method Virtual PC , IVMVirtualMachine interface
- IVMVirtualMachine interface Virtual PC , DetachUSBDevice method
topic_type:
- apiref
api_name:
- IVMVirtualMachine.DetachUSBDevice
api_location:
- VPCCOMInterfaces.h
api_type:
- COM
ms.topic: article
ms.date: 05/31/2018
---

# IVMVirtualMachine::DetachUSBDevice method

\[Windows Virtual PC is no longer available for use as of Windows 8. Instead, use the [Hyper-V WMI provider (V2)](https://docs.microsoft.com/windows/desktop/HyperV_v2/windows-virtualization-portal).\]

Releases a USB device from a virtual machine.

## Syntax


```C++
HRESULT DetachUSBDevice(
  [in] IVMUSBDevice *inUSBDevice
);
```



## Parameters

<dl> <dt>

*inUSBDevice* \[in\]
</dt> <dd>

A [**IVMUSBDevice**](ivmusbdevice.md) pointer that represents the USB device to be detached from the virtual machine.

</dd> </dl>

## Return value

This method can return one of these values.



| Return code/value                                                                                                                                                          | Description                                    |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| <dl> <dt>**S\_OK**</dt> <dt>0</dt> </dl>                                | The operation was successful.<br/>       |
| <dl> <dt>**E\_POINTER**</dt> <dt>0x80004003</dt> </dl>                  | The parameter is **NULL**.<br/>          |
| <dl> <dt>**VM\_E\_VM\_NOT\_RUNNING**</dt> <dt>0xA0040206</dt> </dl>     | The virtual machine is not running.<br/> |
| <dl> <dt>**VM\_E\_USB\_DETACH\_FAILED**</dt> <dt>0xA00400927</dt> </dl> | The detach operation failed.<br/>        |
| <dl> <dt>**DISP\_E\_EXCEPTION**</dt> <dt>0x80020009</dt> </dl>          | An unexpected error has occurred.<br/>   |



 

## Requirements



|                                     |                                                                                               |
|-------------------------------------|-----------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows 7 \[desktop apps only\]<br/>                                                    |
| Minimum supported server<br/> | None supported<br/>                                                                     |
| End of client support<br/>    | Windows 7<br/>                                                                          |
| Product<br/>                  | Windows Virtual PC<br/>                                                                 |
| Header<br/>                   | <dl> <dt>VPCCOMInterfaces.h</dt> </dl> |
| IID<br/>                      | IID\_IVMVirtualMachine is defined as f7092aa1-33ed-4f78-a59f-c00adfc2edd7<br/>          |



## See also

<dl> <dt>

[**IVMVirtualMachine**](ivmvirtualmachine.md)
</dt> </dl>

 

 





