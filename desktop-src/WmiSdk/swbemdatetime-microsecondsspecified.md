---
Description: 'Boolean value that indicates whether the microseconds component in the CIM datetime value contains an interval or a wildcard value.'
audience: developer
author: 'REDMOND\\markl'
manager: 'REDMOND\\markl'
ms.assetid: '65244ece-2326-4edc-b982-57e2046ec33e'
ms.prod: 'windows-server-dev'
ms.technology: 'windows-management-instrumentation'
ms.tgt_platform: multiple
title: 'SWbemDateTime.MicrosecondsSpecified property'
---

# SWbemDateTime.MicrosecondsSpecified property

The **MicrosecondsSpecified** property of the [**SWbemDateTime**](swbemdatetime.md) object is a Boolean value that indicates whether the microseconds component in the CIM datetime value contains an interval or a wildcard value. If **MicrosecondsSpecified** is **TRUE** and [**IsInterval**](swbemdatetime-isinterval.md) is **FALSE**, then [**SWbemDateTime.Microseconds**](swbemdatetime-microseconds.md) contains a datetime value. A datetime value that contains an interval cannot be converted into either the **VT\_DATE** format or the **FILETIME** format. If [**HoursSpecified**](swbemdatetime-hoursspecified.md) is **FALSE** and **IsInterval** is **TRUE**, then **SWbemDateTime.Microseconds** contains an interval.

For an explanation of this syntax, see [Document Conventions for the Scripting API](document-conventions-for-the-scripting-api.md).

This property is read/write.

## Syntax


```VB
SWbemDateTime.MicrosecondsSpecified As Boolean
```



## Property value

## Examples

For examples of using the [**SWbemDateTime**](swbemdatetime.md) object to convert CIM [**DATETIME**](datetime.md) values to and from either the **FILETIME** format or the **VT\_DATE** format, see [WMI Tasks: Dates and Times](wmi-tasks--dates-and-times.md). For a description of the CIM **DATETIME** format, see [Date and Time Format](date-and-time-format.md).

## Requirements



|                                     |                                                                                         |
|-------------------------------------|-----------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows�Vista<br/>                                                                |
| Minimum supported server<br/> | Windows Server�2008<br/>                                                          |
| Header<br/>                   | <dl> <dt>Wbemdisp.h</dt> </dl>   |
| Type library<br/>             | <dl> <dt>Wbemdisp.tlb</dt> </dl> |
| DLL<br/>                      | <dl> <dt>Wbemdisp.dll</dt> </dl> |
| CLSID<br/>                    | CLSID\_SWbemDateTime<br/>                                                         |
| IID<br/>                      | IID\_ISWbemDateTime<br/>                                                          |



## See also

<dl> <dt>

[**SWbemDateTime.Microseconds**](swbemdatetime-microseconds.md)
</dt> <dt>

[**SWbemDateTime**](swbemdatetime.md)
</dt> <dt>

[DATETIME](datetime.md)
</dt> </dl>

�

�



