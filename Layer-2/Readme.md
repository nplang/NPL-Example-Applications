
# Layer-2 Switching

We have created sample ```l2_switch``` NPL example which define packet pipeline with Layer-2 Switching for ethernet packets. 

Main features of this NPL program includes:
 - Basic L2 unicast switching
 - Basic L2 multicast support
 - VLAN membership and spanning tree checks

At a high level below is how Layer-2 packet pipeline looks like based on this NPL Program. 

![Layer-2 Pipeline](IMAGE)

Directory Structure of Layer-2 Examples

`````
(ncsc-1.3.3rc4) npl@npl-VirtualBox:~/ncsc-1.3.3rc4/examples/l2_switch$ tree
.
├── bm_tests
│   ├── l2_test
│   │   ├── tbl_cfg.txt
│   │   └── test.py
│   └── sf_definition
│       └── bm_sfc.cpp
├── Makefile
└── npl
    ├── config.ini
    ├── l2_bus.npl
    ├── l2_header_format.npl
    ├── l2_parser.npl
    ├── l2_sf_defines.npl
    └── l2_switch.npl

4 directories, 10 files
(ncsc-1.3.3rc4) npl@npl-VirtualBox:~/ncsc-1.3.3rc4/examples/l2_switch$ 


`````

To execute this example, follow below steps

1. Make sure [build environment](https://github.com/nplang/NPL-Tutorials#npl-build-enivronment) was properly setup as described earlier
2. Once the environmental variables were setup execute below commands. 
````

export NPL_EXAMPLES=/home/npl/ncsc-1.3.3rc4/examples
cd $NPL_EXAMPLES/l2_switch
make fe_nplsim
make nplsim_comp
make nplsim_run

````

Now you will see two xterm windows one with name ```BMODEL``` and another with ```BMCLI```. 

Before you inject packets you need populate Logical tables using pre-defined table configurations through ```BMCLI``` window. Command to use is as below 

````

rcload /home/npl/ncsc-1.3.3rc4/examples/l2_switch/bm_tests/l2_test/tbl_cfg.txt

````

You can now inject packet using below command  from original console widow where you compiled the NPL code. 

````
python bm_tests/l2_test/test.py

````

The above test.py sends an ingress packet to port 1. And you can see packet being switched to Port 2 based on NPL switching program. 

You can experience complete NPL program for this example located at below location

````

$NPL_EXAMPLES/l2_switch/npl/

````

## Next Tutorial 

Congratulations !!

You have experienced how a simple ```Layer-2 Swicthing``` works. You can now move on to next example [Layer-3 Routing & tunneling example](https://github.com/nplang/NPL-Example-Applications/tree/master/Layer-2)
