---
Description: 'The GetMediaType method retrieves a preferred media type for the output pin.'
ms.assetid: '9a1b123b-aa8a-4bf0-a926-466ded24e506'
title: 'CTransformFilter.GetMediaType method'
---

# CTransformFilter.GetMediaType method

The `GetMediaType` method retrieves a preferred media type for the output pin.

## Syntax


```C++
virtual HRESULT GetMediaType(
  �int �������iPosition,
  �CMediaType *pMediaType
) = 0;
```



## Parameters

<dl> <dt>

*iPosition* 
</dt> <dd>

Zero-based index value.

</dd> <dt>

*pMediaType* 
</dt> <dd>

Pointer to a [**CMediaType**](cmediatype.md) object that receives the media type.

</dd> </dl>

## Return value

Returns an **HRESULT** value. Possible values include those shown in the following table.



| Return code                                                                                            | Description                      |
|--------------------------------------------------------------------------------------------------------|----------------------------------|
| <dl> <dt>**S\_OK**</dt> </dl>                   | Success.<br/>              |
| <dl> <dt>**VFW\_S\_NO\_MORE\_ITEMS**</dt> </dl> | Index out of range.<br/>   |
| <dl> <dt>**E\_INVALIDARG**</dt> </dl>           | Index less than zero.<br/> |



�

## Remarks

The output pin's [**CTransformOutputPin::GetMediaType**](ctransformoutputpin-getmediatype.md) method calls this method. The derived class must implement this method. For more information, see [**CBasePin::GetMediaType**](cbasepin-getmediatype.md).

## Requirements



|                    |                                                                                                                                                                                            |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>Transfrm.h (include Streams.h)</dt> </dl>                                                                                  |
| Library<br/> | <dl> <dt>Strmbase.lib (retail builds); </dt> <dt>Strmbasd.lib (debug builds)</dt> </dl> |



## See also

<dl> <dt>

[**CTransformFilter Class**](ctransformfilter.md)
</dt> </dl>

�

�



