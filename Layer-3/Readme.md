

# Layer-3 Switching NPL Example

We have created ```l3_app``` which is simple NPL Program  to define swithcing pipeline with basic L3 Routing and Tunneling function for IP Packets. 


Main features of basic router NPL program include:
 - Packet parser supports single vlan tagged or untagged packets, IPv4, IPv6 and TCP/UDP header
 - Basic L3 switching
 - Basic L3 tunneling
 - ECMP support

This NPL program defines several data paths, one of them is for basic layer 3 routing of IPv4 packets shown below:

![Layer-3 Pipeline](/Layer-3/Layer-3.png)

### Directory Structure of Layer-3 Examples

`````
npl@npl-VirtualBox:~/ncsc-1.3.3rc4/examples/l3_app$ tree
.
├── bm_tests
│   ├── ipv4_test
│   │   ├── tbl_cfg.txt
│   │   └── test.py
│   ├── ipv4_tunnel_test
│   │   ├── tbl_cfg.txt
│   │   └── test.py
│   ├── ipv6_test
│   │   ├── tbl_cfg.txt
│   │   └── test.py
│   ├── multi_protocol_test
│   │   ├── tbl_cfg.txt
│   │   └── test.py
│   └── sf_definition
│       └── bm_sfc.cpp
├── Makefile
└── npl
    ├── config.ini
    ├── l3_app_bus.npl
    ├── l3_app.npl
    ├── l3_header_format.npl
    ├── l3_parser.npl
    └── l3_sf_defines.npl

7 directories, 16 files

`````

To execute above example tests, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc4/examples
cd $NPL_EXAMPLES/l3_app
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

### Packet Tests

There are several tests available under ```bm_tests``` directory for l3_app program. Each test has its respective table configurations in ```tbl_cfg.txt```

 - 'ipv4_test' : Simple l3 routing test with IPv4 host entry
 - 'ipv4_tunnel_test' : IPv4 tunnel termination test case.
 - 'ipv6_test' : Simple l3 routing test with IPv6 host entry
 - 'multi_protocol_test' : Collective multiple datapath (IPV4/6, tunnel, L2) simulation test


Before you inject packets you need populate Logical tables using pre-defined table configurations through ```BMCLI``` window. Command to use is as below 

````

# Change the below command based on the test you exercise. Example given for 'ipv4_test'
rcload /home/npl/ncsc-1.3.3rc4/examples/l3_app/bm_tests/ipv4_test/tbl_cfg.txt

````

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````

python bm_tests/ipv4_test/test.py

````

The above test.py sends two IPV4 packets (under ipv4_test)

````
1. The first packet ingress on port 0 with vlan 1 and  is routed to the destination host on port 3 with vlan 6 based on dest. IP of the packet. 

2. The test packet with vlan 1 ingresses on port 5 which is switched to dest port 18 using l2_host table entries. 

`````

Make sure you execute other sample tests created for you to experience IPv6 Forwarding, IP tunneling and ECMP. 

Complete NPL program for this example is located at below location

````

$NPL_EXAMPLES/l3_app/npl/

````

## Congratulations :+1: You have finished working with NPL Example Applications.
