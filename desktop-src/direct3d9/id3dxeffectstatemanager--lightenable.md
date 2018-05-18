﻿---
Description: 'A callback function that must be implemented by a user to enable/disable a light.'
ms.assetid: '11522ca3-8a2f-4767-a6e6-4186cb4f3115'
title: 'ID3DXEffectStateManager::LightEnable method'
---

# ID3DXEffectStateManager::LightEnable method

A callback function that must be implemented by a user to enable/disable a light.

## Syntax


```C++
HRESULT LightEnable(
  [in] DWORD Index,
  [in] BOOL  Enable
);
```



## Parameters

<dl> <dt>

*Index* \[in\]
</dt> <dd>

Type: **[**DWORD**](winprog.windows_data_types)**

The zero-based index of the light. This is the same index in [**IDirect3DDevice9::SetLight**](idirect3ddevice9--setlight.md).

</dd> <dt>

*Enable* \[in\]
</dt> <dd>

Type: **[**BOOL**](winprog.windows_data_types)**

True to enable the light, false otherwise.

</dd> </dl>

## Return value

Type: **[**HRESULT**](455d07e9-52c3-4efb-a9dc-2955cbfd38cc)**

The user-implemented method should return S\_OK. If the callback fails when setting the device state, either of the following will occur:

-   The effect will fail during [**ID3DXEffect::BeginPass**](id3dxeffect--beginpass.md).
-   The dynamic effect state call (such as [**IDirect3DDevice9::LightEnable**](idirect3ddevice9--lightenable.md)) will fail.

## Requirements



|                    |                                                                                          |
|--------------------|------------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>D3DX9Effect.h</dt> </dl> |
| Library<br/> | <dl> <dt>D3dx9.lib</dt> </dl>     |



## See also

<dl> <dt>

[ID3DXEffectStateManager](id3dxeffectstatemanager.md)
</dt> </dl>

 

 



