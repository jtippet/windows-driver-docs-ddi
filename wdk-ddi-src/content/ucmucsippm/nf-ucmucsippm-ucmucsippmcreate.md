---
UID: NF:ucmucsippm.UcmUcsiPpmCreate
title: UcmUcsiPpmCreate function
author: windows-driver-content
description: Creates a Platform Policy Manager (PPM) object.
ms.assetid: 2b0d12ae-dc1d-45ff-bde5-a589f0272e3e
ms.author: windowsdriverdev
ms.date: 09/30/2018 
ms.topic: function
ms.keywords: UcmUcsiPpmCreate
req.header: Ucmucsippm.h
req.include-header: UcmUcsiCx.h
req.target-type:
req.target-min-winverclnt:
req.target-min-winversvr:
req.kmdf-ver: 1.27
req.umdf-ver: N/A
req.lib: UcmUcsiCxStub.lib
req.dll:
req.irql: PASSIVE_LEVEL
req.ddi-compliance:
req.unicode-ansi:
req.idl:
req.max-support:
req.namespace:
req.assembly:
req.type-library: 
topic_type: 
-	apiref
api_type: 
-	LibDef
api_location: 
-	UcmUcsiCxStub.lib
api_name: 
-	UcmUcsiPpmCreate
product: Windows
targetos: Windows


---

# UcmUcsiPpmCreate function


## -description

Creates a Platform Policy Manager (PPM) object.

## -parameters

### -param WdfDevice [in]
A handle to a framework device object that the client driver received in the previous call to [**WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926).

### -param Config [in]
A pointer to a caller-supplied [**UCMUCSI_PPM_CONFIG**](ns-ucmucsippm-_ucmucsi_ppm_config.md) structure that is initialized by calling [**UCMUCSI_PPM_CONFIG_INIT**](nf-ucmucsippm-ucmucsi_ppm_config_init.md). The **ConnectorCollectionHandle** member must be set to the handle retrieved in a previous call to [**UcmUcsiConnectorCollectionCreate**](nf-ucmucsippm-ucmucsiconnectorcollectioncreate.md).

### -param Attributes [in]
A pointer to a caller-supplied [WDF_OBJECT_ATTRIBUTES](https://msdn.microsoft.com/library/windows/hardware/ff552400) structure that contains attributes for the new connector collection object. This parameter is optional and can be WDF_NO_OBJECT_ATTRIBUTES.

### -param PPMObject [out]
A pointer to a location that receives a handle to the new PPM object.

## -returns
Returns STATUS_SUCCESS if the operation succeeds. Otherwise, this method can return an appropriate [NTSTATUS](https://msdn.microsoft.com/7792201b-63bb-4db5-803d-2af02893d505) value.

## -remarks
The client driver is expected to call **UcmUcsiPpmCreate** from the [EVT_WDF_DEVICE_PREPARE_HARDWARE](../wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) callback function. 

The structure passed in _Config_ contains Type-C connector information that is necessary for creating connectors with USB Type-C connector class extension (UcmCx) by using [**UcmConnectorCreate**](https://msdn.microsoft.com/library/windows/hardware/mt187909) and are not obtainable from PPM through UCSI commands such as GetCapability or GetConnectorCapability.

The _Config_ structure also contains connector IDs, which are required for one-to-one mapping between USB Type-C connectors and USB ports.  

The PPM object is also a WDFOBJECT and creates a one-to-one association with the WDFDEVICE handle provided by the client driver.  

The PPM object is parented to the WDFOBJECT even when UcmUcsiPpmCreate is called by passing WDF_NO_ATTRIBUTES. The lifetime of the object is manager by the framework.

## -see-also