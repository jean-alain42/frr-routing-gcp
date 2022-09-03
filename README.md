# frr-routing-gcp
These routing labs are based on Containerlab is a new open-source network emulator that quickly builds network test environments in a devops-style workflow. 
It provides a command-line-interface for orchestrating and managing container-based networking labs and supports containerized router images available
from the major networking vendors.

These labs will demonstrate how Containerlab works with the FRR open-source router. There are 2 main labs one to test OSPF dynamic routing protocols with 
three routers and another one with BGP peerings between two AS (AS 100 and AS 200), to understand how prefix are progated with BGP protocols between AS, 
also internal BGP is shown.  

Lab 1: just type the command after having Containerlab installed and launch on your machine, example for MacOS, 

CLAB_WORKDIR=~/clab

docker run --rm -it --privileged \
    --network host \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /run/netns:/run/netns \
    --pid="host" \
    -w $CLAB_WORKDIR \
    -v $CLAB_WORKDIR:$CLAB_WORKDIR \
    ghcr.io/srl-labs/clab bash
    
where the first command in the script above sets the working directory which you intend to use on your Mac OS. The ~/clab in the example above expands to /Users/<username>/clab and means that we intent to have our containerlab labs to be stored in this directory.

To deploy first lab on OSPF just run: 

bash-5.1# sudo clab deploy --topo frrlab.yaml

INFO[0000] Containerlab v0.27.1 started
INFO[0000] Parsing & checking topology file: frrlab.yaml
WARN[0000] it appears that container host has low memory available: ~0Gi. This might lead to runtime errors. Consider freeing up more memory.
INFO[0000] Creating lab directory: /Users/jean-alainmignon/clab/clab-frrlab
INFO[0000] Creating docker network: Name="clab", IPv4Subnet="172.20.20.0/24", IPv6Subnet="2001:172:20:20::/64", MTU="1500"
WARN[0000] errors during iptables rules install: missing DOCKER-USER iptables chain. See http://containerlab.dev/manual/network/#external-access
INFO[0000] Creating container: "PC3"
INFO[0000] Creating container: "PC2"
INFO[0000] Creating container: "router1"
INFO[0000] Creating container: "router2"
INFO[0000] Creating container: "router3"
INFO[0000] Creating container: "PC1"
INFO[0014] Creating virtual wire: PC1:eth1 <--> router1:eth3
INFO[0015] Creating virtual wire: router1:eth1 <--> router2:eth1
INFO[0015] Creating virtual wire: router2:eth2 <--> router3:eth2
INFO[0015] Creating virtual wire: router1:eth2 <--> router3:eth1
INFO[0015] Creating virtual wire: PC3:eth1 <--> router3:eth3
INFO[0015] Creating virtual wire: PC2:eth1 <--> router2:eth3
INFO[0016] Adding containerlab host entries to /etc/hosts file
INFO[0016] 🎉 New containerlab version 0.31.1 is available! Release notes: https://containerlab.dev/rn/0.31/#0311
Run 'containerlab version upgrade' to upgrade or go check other installation options at https://containerlab.dev/install/



