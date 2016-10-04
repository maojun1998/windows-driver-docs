---
title: Determining BDA Device Topology
author: windows-driver-content
description: Determining BDA Device Topology
MS-HAID:
- 'bdadg\_62a2e931-f78d-4401-b6c8-1a1748e0710f.xml'
- 'stream.determining\_bda\_device\_topology'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: fdac317e-d4fc-47c9-87d3-bec597f758f5
keywords: ["method sets WDK BDA , BDA device topology", "property sets WDK BDA , BDA device topology", "KSPROPERTY_BDA_NODE_TYPES", "KSPROPERTY_BDA_PIN_TYPES", "KSPROPERTY_BDA_TEMPLATE_CONNECTIONS", "template filter topology WDK BDA"]
---

# Determining BDA Device Topology


## <a href="" id="ddk-determining-bda-device-topology-ksg"></a>


A BDA device topology is composed of a connected network of nodes, each of which represent some transformation on a signal. Nodes can be grouped arbitrarily among different filters. This arbitrary grouping provides hardware vendors with a certain freedom in how they implement their hardware and drivers so that such hardware and drivers work in a generic way with the network providers for the different types of networks they wish to support.

For this arbitrary grouping architecture to work, the network provider must be able to query filters as to what kind of transformations those filters perform on a signal (that is, what types of node networks the filter can support). The underlying Ring 0 minidriver for a filter conveys a picture of its supported node networks to the network provider through the [KSPROPSETID\_BdaTopology](https://msdn.microsoft.com/library/windows/hardware/ff566561) property set.

When determining the template topology for a filter, the network provider iterates lists of node types and pin types and queries each node and pin for its capabilities. The network provider uses the following properties of KSPROPSETID\_BdaTopology to determine the template topology for the filter:

-   KSPROPERTY\_BDA\_NODE\_TYPES

    Node types represent possible functional nodes within the filter. The KSPROPERTY\_BDA\_NODE\_TYPES property returns a list of all node types that are provided by a filter instance of the BDA minidriver. The minidriver assigns arbitrary values to identify node types. Typically, the minidriver uses the index of each element in the list of the minidriver's node types as the value for each node type. The BDA minidriver assigns each node type a node description GUID. Description GUIDs for node types that the network provider currently supports are defined in *bdamedia.h*. This node description indicates to the network provider what the node does. In a template topology, a node type can occur only once. However, more than one node of a specific type may have the same node description GUID. This allows a specific signal transformation to occur in more than one place in the filter's topology while allowing the network provider to identify a single topology node unambiguously.

-   KSPROPERTY\_BDA\_PIN\_TYPES

    Pin types represent possible connections to other filters in the graph. The KSPROPERTY\_BDA\_PIN\_TYPES property returns a list of all pin types that can be created on the filter. In a template topology, a pin type can occur only once.

-   KSPROPERTY\_BDA\_TEMPLATE\_CONNECTIONS

    The KSPROPERTY\_BDA\_TEMPLATE\_CONNECTIONS property returns an array that represents all the possible connections between node types and pin types that can be configured on the filter. See [Mapping Connection Topology](mapping-connection-topology.md) for more information.

When a filter instance is first created and added to the graph, it typically has input pins but no output pins. To create output pins, the network provider first uses the KSPROPSETID\_BdaTopology properties to determine what operations the filter can perform. From these properties, the network provider determines which operations it requires the filter to perform for a particular filter graph. The network provider then uses the [KSMETHODSETID\_BdaDeviceConfiguration](https://msdn.microsoft.com/library/windows/hardware/ff563404) method set to create output pins matching a particular pin type and create the internal topology, which is the actual hardware path, between those pins and the input pins. See [Configuring a BDA Filter](configuring-a-bda-filter.md) for more information.

The following code snippet shows how to define functions that are exported by the BDA support library as dispatch routines for the KSPROPSETID\_BdaTopology property set:

```
//
//  KSPROPSETID_BdaTopology property set
//
//  Defines the dispatch routines for the filter level
//  topology properties
//
DEFINE_KSPROPERTY_TABLE(FilterTopologyProperties)
{
    DEFINE_KSPROPERTY_ITEM_BDA_NODE_TYPES(
        BdaPropertyNodeTypes,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_PIN_TYPES(
        BdaPropertyPinTypes,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_TEMPLATE_CONNECTIONS(
        BdaPropertyTemplateConnections,
        NULL
        ),
    DEFINE_KSPROPERTY_ITEM_BDA_CONTROLLING_PIN_ID(
        BdaPropertyGetControllingPinId,
        NULL
        )
};
```

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bstream\stream%5D:%20Determining%20BDA%20Device%20Topology%20%20RELEASE:%20%288/23/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

