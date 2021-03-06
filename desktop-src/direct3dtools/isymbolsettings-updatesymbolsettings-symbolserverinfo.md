---
Description: A request to send debug symbol paths to the local (non-remote) engine.
MS-HAID: vspixengine.ISymbolSettings\_UpdateSymbolSettings\_SymbolServerInfo
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/desktop
title: ISymbolSettings::UpdateSymbolSettings method
ms.topic: article
ms.date: 05/31/2018
ms.assetid: E48E509F-8C33-49D6-B799-B16F70C1AA64
api_name: 
 - ISymbolSettings.UpdateSymbolSettings
api_type: 
 - COM
api_location: 
 - vspixengine.h
topic_type: 
 - APIRef
 - kbSyntax

---

# <span id="vspixengine.isymbolsettings_updatesymbolsettings_symbolserverinfo"></span>ISymbolSettings::UpdateSymbolSettings method

A request to send debug symbol paths to the local (non-remote) engine.

## Syntax


```C++
HRESULT UpdateSymbolSettings(
   SymbolServerInfo symbolServerInfo
);
```

## Parameters

*symbolServerInfo*   
Debug symbol server path information.

## Return value

If this method succeeds, it returns **S\_OK**. Otherwise, it returns an **HRESULT** error code.

## Requirements

<table><colgroup><col style="width: 50%" /><col style="width: 50%" /></colgroup><tbody><tr class="odd"><td><p>Header</p></td><td>Vspixengine.h</td></tr></tbody></table>

## <span id="see_also"></span>See also

[**ISymbolSettings**](https://docs.microsoft.com/windows/desktop/direct3dtools/isymbolsettings)

 

 



