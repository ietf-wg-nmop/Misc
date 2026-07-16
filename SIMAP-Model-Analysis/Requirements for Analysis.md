# Requirements for SIMAP Modelling Approach Analysis

The requirement list will be used to compare the approach of modeling 
SIMAP and decide which approach to follow in modeling SIMAP. 

A YANG Data Model for Network Topologies: 
  https://datatracker.ietf.org/doc/html/rfc8345
SIMAP draft: https://datatracker.ietf.org/doc/draft-havel-nmop-simap-yang/
TE RFC: https://datatracker.ietf.org/doc/html/rfc8795

1. Option 1: Have both SIMAP draft and TE teams work on a common proposal
2. Option 2: Use SIMAP draft as base but
o	Indicate in the text that it is out of scope to explore how TE 
model meets/can be augmented or profiled for SIMAP.
o	Add a pointer to the individual assessment made so far by Italo/Aihua
o	Re-use as much as possible structures that would ease mapping 
   with the TE topology
3. Option 3: Use TE work as base
4. Option 4: Use RFC8345 for subset of use cases and TE and other existing models for the uses cases that they are currently sued for. For example:
    - SIMAP can provide a simplified navigation capabilities for multi-layer navigation (including tunnels and paths), it can be alternative view from other IETF RFCs/drafts that only uses network/node/link/tp (as intended by RFC8345) for all domains, layers and technologies. In this case, SIMAP can become a complimentary navigation mechanism for IP, Data Center, etc - unified view of the multi technology, multi-layered topology for multi-domain.
    - SIMAP can be used for declarative what-if and intents for topologies (not what connectivity you want, this would be realized via the existing YANG modules), other existing modules will continue to be used for provisioning and for realization of declarative what-if and intent requests
    - Some solutions/technologies will need TE and other YANG modules and will continue using it for write/control plane
    - Some solutions will use SIMAP topology (e.g. ISIS, OSPF Topology YANG modules) for both read and write

Other suggestions can be identified during the analysis.

## Selected Requirements

All SIMAP requirements are defined in 
https://datatracker.ietf.org/doc/draft-ietf-nmop-simap-concept/

The following requirements are the core set that enables the topology 
navigation without ambiguity and were identified as the most 
important to analyze and agree the modeling approach.

1. REQ-BASIC-MODEL-SUPPORT (supported by RFC8345)
2. REQ-LAYERED-MODEL (supported by RFC8345)
3. REQ-LAYER-NAVIGATE (supported by RFC8345)

4. REQ-SEMANTIC (RFC8345 gap, requires extension)
5. REQ-SUPPORTING (RFC8345 gap, requires extension)
6. REQ-MULTI-DOMAIN (RFC8345 gap, requires extension)
7. REQ-BIDIR (RFC8345 gap, requires extension)
8. REQ-MULTI-POINT (RFC8345 gap, requires extension)
9. REQ-SUBNETWORK (RFC8345 gap, requires extension)



The first 3 requirements identified as supported by RFC8345 
(REQ-BASIC-MODEL-SUPPORT, REQ-LAYERED-MODEL, REQ-LAYER-NAVIGATE) are 
more important than gap requirements for the purpose of agreeing the 
overall approach. 

Therefore, we agreed to start analysis from these requirements (1, 2, 3) 
and go into the others only if needed (4,5, ..). We will probably
need to go into REQ-SEMANTIC and REQ-SUPPORTING as they may be the 
reasons that RFC8795 added additional topological entities/relations 
outside of RFC8345.  

The following are the requirement definitions from
https://datatracker.ietf.org/doc/draft-ietf-nmop-simap-concept/.

### REQ-BASIC-MODEL-SUPPORT

SIMAP requires a basic model with network, node, link, and termination 
point entity types.                                    

This means that users of SIMAP must be able to reconstruct a topology 
at any layer in an unambiguous manner via these core concepts only, 
without the need to understand layer or technology specific information.

### REQ-LAYERED-MODEL

Topology layers from physical up to Service layer.  
SIMAP must provide views for all layers of network topology,  
from physical network (ideally optical), Layer 2, Layer 3 up to 
Service and intent views.  It must provide flexibility to support 
both the same network topology instance with multiple layers (e.g., 
Layer 2 and Layer 3) or separate network topology instances with 
supporting relations between them (e.g., separate Layer 2 and 
Layer 3). Multiple topology layers can  be grouped into the same 
network topology instance, if solution requires.

### REQ-LAYER-NAVIGATE

SIMAP must provide capability to navigate both  within a topology 
layer and between topology layers.

Within-layer navigation means that SIMAP client applications
should be able to move among entities that belong to the same
layer.  For example, in the IGP layer, the navigation should allow
moving between OSPF/IS-IS management domains, OSPF/IS-IS areas,
OSPF/IS-IS processes, OSPF/IS-IS interfaces, and OSPF/IS-IS links.

Between-layer navigation is the navigation across layers that
should display the dependencies of entities in one layer on those
in another.  For instance, an IP interface that is supported by an
Ethernet interface should be visible when moving between the
corresponding layers.

### REQ-SEMANTIC

Network topology semantics. SIMAP must provide semantics for layered 
network topologies and for linking external models/data

### REQ-SUPPORTING

SIMAP must provide a mechanism to model supporting relationships 
between different types of topological entities (e.g., a termination 
point is supported by a node or a node is supported by a network).  
This may be required to model supporting relationships for termination 
points which are supported by physical devices (e.g., a loopback 
interface on IP router).

### REQ-MULTI-DOMAIN

SIMAP must provide a mechanism to model links and
nodes between networks when the implementation requires multi-
domain topologies, topologies with multiple IGP areas or any
network partitioning.  This requirement is about covering
connectivity between different networks, sub-networks, or domains.

### REQ-BIDIR

SIMAP must provide a mechanism to model bidirectional
links.  While data flows are unidirectional, the bidirectional
links are also common in networking.  Examples are Ethernet
cables, bidirectional SONET rings, socket connection to the
server, etc., where a link is modeled as bidirectional, which in
turn might be supported as unidirectional links at the lower
layer.

### REQ-MULTI-POINT

SIMAP must provide a mechanism to model multipoint
links.  A topology model should be able to model any topology
type, including point to multipoint, bus, ring, star, tree, mesh,
hybrid and daisy chain.  A topology model should also be able to
model any link cardinality, including point-to-point, point-to-
multipoint, multipoint-to-multipoint

### REQ-SUBNETWORK

SIMAP must provide a mechanism to model network
decomposition into sub-networks.  The requirement is about
modelling hierarchical networks , Autonomous Systems (ASes) with
multiple areas, or a network with multiple domains (e.g., access,
core, data center).

The network can be partitioned by providing capability to have
multiple child network instances as part of a single parent
network, with a relation between the parent network and child
networks.
