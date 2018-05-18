---
title: ID3DX11EffectBlendVariable GetBlendState method
description: Get a pointer to a blend-state interface.
ms.assetid: 'ab4ee765-b5ad-4dc3-9b00-48052528d3bd'
keywords: ["GetBlendState method Direct3D 11", "GetBlendState method Direct3D 11 , ID3DX11EffectBlendVariable interface", "ID3DX11EffectBlendVariable interface Direct3D 11 , GetBlendState method"]
topic_type:
- apiref
api_name:
- ID3DX11EffectBlendVariable.GetBlendState
api_location:
- N/A
- N/A.dll
api_type:
- COM
---

# ID3DX11EffectBlendVariable::GetBlendState method

Get a pointer to a blend-state interface.

## Syntax


```C++
HRESULT GetBlendState(
  �UINT ������������Index,
  �ID3D11BlendState **ppBlendState
);
```



## Parameters

<dl> <dt>

*Index* 
</dt> <dd>

Type: **[**UINT**](https://msdn.microsoft.com/library/windows/desktop/aa383751)**

Index into an array of blend-state interfaces. If there is only one blend-state interface, use 0.

</dd> <dt>

*ppBlendState* 
</dt> <dd>

Type: **[**ID3D11BlendState**](id3d11blendstate.md)\*\***

The address of a pointer to a blend-state interface (see [**ID3D11BlendState**](id3d11blendstate.md)).

</dd> </dl>

## Return value

Type: **[**HRESULT**](455d07e9-52c3-4efb-a9dc-2955cbfd38cc)**

Returns one of the following [Direct3D 11 Return Codes](d3d11-graphics-reference-returnvalues.md).

## Remarks

> [!Note]  
> The DirectX SDK does not supply any compiled binaries for effects. You must use Effects 11 source to build your effects-type application. For more information about using Effects 11 source, see [Differences Between Effects 10 and Effects 11](d3d11-graphics-programming-guide-effects-differences.md).

�

## Requirements



|                    |                                                                                                                                              |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>D3dx11effect.h</dt> </dl>                                                    |
| Library<br/> | <dl> <dt>N/A (An Effects 11 library is available online as shared source.)</dt> </dl> |



## See also

<dl> <dt>

[ID3DX11EffectBlendVariable](id3dx11effectblendvariable.md)
</dt> </dl>

�

�




