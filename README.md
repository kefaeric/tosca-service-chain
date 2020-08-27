# tosca-service-chain
TOSCA simple cloud automation
description: Demo example with auto image creation
metadata: {template_name: sample-tosca-vnfd-image}
topology_template:
  inputs:
   availabilityzone:
    type: string
    description: The controller availability zone.
  node_templates:
#networks for 1st VNF  
    CP1:
      requirements:
      - virtualLink: {node: VL1}
      - virtualBinding: {node: VDU1}
      type: tosca.nodes.nfv.CP.Tacker
    CP2:
      requirements:
      - virtualLink: {node: VL2}
      - virtualBinding: {node: VDU1}
      type: tosca.nodes.nfv.CP.Tacker
    CP3:
      requirements:
      - virtualLink: {node: VL3}
      - virtualBinding: {node: VDU1}
      type: tosca.nodes.nfv.CP.Tacker
    CP4:
      requirements:
      - virtualLink: {node: VL4}
      - virtualBinding: {node: VDU1}
      type: tosca.nodes.nfv.CP.Tacker
#networks for 2nd VNF
    CP11:
      requirements:
      - virtualLink: {node: VL11}
      - virtualBinding: {node: VDU2}
      type: tosca.nodes.nfv.CP.Tacker
    CP12:
      requirements:
      - virtualLink: {node: VL12}
      - virtualBinding: {node: VDU2}
      type: tosca.nodes.nfv.CP.Tacker
    CP13:
      requirements:
      - virtualLink: {node: VL13}
      - virtualBinding: {node: VDU2}
      type: tosca.nodes.nfv.CP.Tacker
    CP14:
      requirements:
      - virtualLink: {node: VL4}
      - virtualBinding: {node: VDU2}
      type: tosca.nodes.nfv.CP.Tacker
      
    VDU1:
      properties: {availability_zone: { get_input: availabilityzone }, image: "Firewall" , flavor:  "Fortinet_Flavor1" }
      type: tosca.nodes.nfv.VDU.Tacker
      
    VDU2:
      properties: {availability_zone: { get_input: availabilityzone }, image: "vRouter" , flavor:  "vRouter_Flavor1" }
      type: tosca.nodes.nfv.VDU.Tacker

    VL1:
      properties: {cidr: 1.1.1.0/24, ip_version: 4, network_name: Net1, network_type: flat, physical_network: physnet1, vendor: Tacker}
      type: tosca.nodes.nfv.VL
    VL2:
      properties: {cidr: 2.1.1.0/24, ip_version: 4, network_name: Net2, network_type: vlan, physical_network: physnet2, segmentation_id: 2, vendor: Tacker}
      type: tosca.nodes.nfv.VL
    VL3:
      properties: {cidr: 5.1.1.0/24, ip_version: 4, network_name: Net5, network_type: vlan, physical_network: physnet5, segmentation_id: 5, vendor: Tacker}
      type: tosca.nodes.nfv.VL

    VL11:
      properties: {cidr: 4.1.1.0/24, ip_version: 4, network_name: Net4, network_type: flat, physical_network: physnet4, vendor: Tacker}
      type: tosca.nodes.nfv.VL
    VL12:
      properties: {cidr: 3.1.1.0/24, ip_version: 4, network_name: Net3, network_type: vlan, physical_network: physnet3, segmentation_id: 3, vendor: Tacker}
      type: tosca.nodes.nfv.VL
    VL13:
      properties: {cidr: 6.1.1.0/24, ip_version: 4, network_name: Net6, network_type: vlan, physical_network: physnet6, segmentation_id: 6, vendor: Tacker}
      type: tosca.nodes.nfv.VL
    VL4:
      properties: {cidr: 99.1.1.0/24, ip_version: 4, network_name: Net99_Chain, network_type: vlan, physical_network: physnet99, segmentation_id: 99, vendor: Tacker}
      type: tosca.nodes.nfv.VL

