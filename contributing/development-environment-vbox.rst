.. _development-environment-kvm:

====================================
Development environment (VirtualBox)
====================================

I have VirtualBox running on my desktop.

1. Create a NAT Network (a private vlan) to be used for the Warewlf Server and compute nodes inside the VirtualBox.

2. Make sure to turnoff the DHCP service within this NAT Network.

3. Create a Centos 7 development Virtual machine (wwdev) to be used as the Warewulf Server. Enable two Network adapters one with a standard NAT and SSH port mapping such that you can access this VM from the host machine. Assign the second network adapter to the NAT Network created in step #1. Assign sufficient memory (e.g: 4GB) to the VM. 

4. Build and install warewulf on wwdev

.. code-block:: bash

    # Login to VM and install @development group and go language

    $ ssh root@wwdev

    # Disable selinux by modifying /etc/sysconfig/selinux
    $ vi /etc/sysconfig/selinux

        SELINUX=disabled

    # Disable firewall
    $ systemctl stop firewalld
    $ systemctl disable firewalld

    # Centos prerequisites
    $ sudo yum -y install tftp-server tftp
    $ sudo yum -y install dhcp
    $ sudo yum -y install ipmitool
    $ sudo yum install http://repo.ctrliq.com/packages/rhel7/ctrl-release.rpm
    $ sudo yum install singularityplus
    $ sudo yum install gpgme-devel
    $ sudo yum install libassuan.x86_64 libassuan-devel.x86_64

    # Upgrade git to v2+
    $ sudo yum install https://packages.endpoint.com/rhel/7/os/x86_64/endpoint-repo-1.7-1.x86_64.rpm
    $ sudo yum install git
    $ sudo yum install golang
    $ sudo yum install nfs-utils

    # Install Warewulf and dependencies
    $ git clone https://github.com/ctrliq/warewulf.git
    $ cd warewulf

    $ make all
    $ sudo make install

    # Configure the controller
    $ Edit the file /etc/warewulf/warewulf.conf and ensure that you've ser the approprite configuration parameters

    # Configure system service automatically
    $ sudo wwctl configure dhcp # Create the default dhcpd.conf file and start/enable service
    $ sudo wwctl configure tftp # Install the base tftp/PXE boot files and start/enable service
    $ sudo wwctl configure nfs  # Configure the exports and create an fstab in the default system overlay
    $ sudo wwctl configure ssh  # Build the basic ssh keys to be included by the default system overlay

    # Pull and build the VNFS container and kernel
    $ sudo wwctl container import docker://warewulf/centos-8 centos-8 --setdefault
    $ sudo wwctl kernel import build $(uname -r) --setdefault

    # Set up the default node profile
    $ sudo wwctl profile set default -K $(uname -r) -C centos-7
    $ sudo wwctl profile set default --netdev eth0 -M WW_server_subnet_mask -G WW_server_ip
    $ sudo wwctl profile list

    # Add a node and build node specific overlays
    $ sudo wwctl node add n0000.cluster --netdev eth0 -I n0000_ip --discoverable
    $ sudo wwctl node list -a n0000

    # Review Warewulf overlays
    $ sudo wwctl overlay list -l
    $ sudo wwctl overlay list -ls
    $ sudo wwctl overlay edit default /etc/hello_world.ww
    $ sudo wwctl overlay build -a

    # Start the Warewulf daemon
    $ sudo wwctl ready
    $ sudo wwctl server start
    $ sudo wwctl server status

5. Create a new guest VM instance inside the VirtualBox to be the warewulf client/compute node. Under the system configuration make sure to select the optical and network options only for the boot order. The default iPXE used by VirtualBox does not come with bzImage capability which is needed for warewulf. Download the ipxe.iso available at ipxe.org and mount the ipxe.iso to the optical drive. Enable one Network adapter for this VM and assign it to the NAT Network created in step #1 above. 

6. Boot your node and watch the console and the output of the Warewulfd process
