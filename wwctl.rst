.. _wwctl:

=====
wwctl
=====

wwctl - Control interface to the Cluster Warewulf Provisioning System

Usage: wwctl [GLOBAL OPTIONS] [SUBCOMMAND]

Global options:

``-v`` ``--verbose`` Run with increased verbosity

``-d`` ``--debug`` Run with debugging messages enabled

build
-----

Warewulf build is used to build VNFS, kernel, and system-overlay objects for provisioning. The default usage will be to build and/or update anything that seems to be needed.

``-V`` ``--container`` Build and/or update VNFS images.

``-K`` ``--kernel`` Build and/or update Kernel images.

``-R`` ``--runtime`` Build and/or update runtime overlays

``-S`` ``--system`` Build and/or update system overlays

``-A`` ``--all`` Build and/or update all components

``-f`` ``--force`` Force build even if nothing has been updated.

configure
---------

This application allows you to manage and initialize Warewulf dependent system services based on the configuration in the warewulf.conf file.

dhcp
~~~~

DHCP is a dependent service to Warewulf. This command will configure DHCP as defined.

``-s`` ``--show`` Show configuration (don't update)

``--persist`` Persist the configuration and initialize the service

hosts
~~~~~
Write out the /etc/hosts file based on the Warewulf template (hosts.tmpl) in the Warewulf configuration directory.

``-s`` ``--show`` Show configuration (don't update)

``--persist`` Persist the configuration and initialize the service

nfs
~~~
NFS is an optional dependent service of Warewulf, this tool will automatically configure NFS as per the configuration in the warewulf.conf file.

``-s`` ``--show`` Show configuration (don't update)

``--persist`` Persist the configuration and initialize the service

ssh
~~~
SSH is an optionally dependent service for Warewulf, this tool will automatically setup the ssh keys nodes using the 'default' system overlay as well as user owned keys.

``--persist`` Persist the configuration and initialize the service

tftp
~~~~
TFTP is a dependent service of Warewulf, this tool will enable the tftp services on your Warewulf master.

``-s`` ``--show`` Show configuration (don't update)

``--persist`` Persist the configuration and initialize the service

container
---------

Starting with version 4, Warewulf uses containers to build the bootable VNFS images for nodes to boot. These commands will help you import, management, and transform containers into bootable Warewulf VNFS images.

build
~~~~~
This command will build a bootable VNFS image from an imported container image.

``-a`` ``--all`` (re)Build all VNFS images for all nodes

``-f`` ``--force`` Force rebuild, even if it isn't necessary

``--setdefault`` Set this container for the default profile

delete
~~~~~~
This command will delete a container that has been imported into Warewulf.

exec
~~~~
This command will allow you to run any command inside of a given warewulf container. This is commonly used with an interactive shell such as ``/bin/bash`` to run a virtual environment within the container.

imprt
~~~~~
This command will pull and import a container into Warewulf so it can be used as a source to create a bootable VNFS image.

``-f`` ``--force`` Force overwrite of an existing container

``-u`` ``--update`` Update and overwrite an existing container

``-b`` ``--build`` Build container when after pulling

``--setdefault`` Set this container for the default profile

list, ls
~~~~~~~~
This command will show you the containers that are imported into Warewulf.

controller
----------

Management of group settings and power management

add
~~~

delete
~~~~~~

list
~~~~

``-a`` ``--all`` Show all node configurations

set
~~~

``-a`` ``--all`` Set all controllers

``-I`` ``--ipaddr`` Set the controller's IP address

``-F`` ``--fqdn`` Set the controller's FQDN

``-C`` ``--comment`` Comments describing this controller


kernel
------

This command is for management of Warewulf Kernels to be used for bootstrapping nodes.

imprt
~~~~~
This will import a Kernel version from the control node into Warewulf for nodes to be configured to boot on.

``-a`` ``--all`` Build all overlays (runtime and system)

``-n`` ``--node`` Build overlay for a particular node(s)

``--setdefault`` Set this kernel for the default profile

list, ls
~~~~~~~~
This command will list the kernels that have been imported into Warewulf.

node
----

Management of node settings

add
~~~
This command will add a new node to Warewulf.

``-g`` ``--group`` Group to add nodes to

``-c`` ``--controller`` Controller to add nodes to

``-N`` ``--netdevDefine`` the network device to configure

``-I`` ``--ipaddrSet`` the node's network device IP address

``-M`` ``--netmaskSet`` the node's network device netmask

``-G`` ``--gatewaySet`` the node's network device gateway

``-H`` ``--hwaddrSet`` the node's network device HW address

``--discoverable`` Make this node discoverable

console
~~~~~~~
Start IPMI console for a singe node.

delete
~~~~~~
This command will remove a node from the Warewulf node configuration.

``-f`` ``--force`` Force node delete

``-g`` ``--group`` Set group to delete nodes from

``-c`` ``--controller`` Controller to add nodes to

list
~~~~
This command will show you configured nodes.

``-n`` ``--net`` Show node network configurations

``-i`` ``--ipmi`` Show node IPMI configurations

``-a`` ``--all`` Show all node configurations

``-l`` ``--long`` Show long or wide format

sensors
~~~~~~~
Show IPMI sensors for a single node.

``-F`` ``--full`` show detailed output

set
~~~
This command will allow you to set configuration properties for nodes.

``--comment`` Set a comment for this node

``-C`` ``--container`` Set the container (VNFS) for this node

``-K`` ``--kernel`` Set Kernel version for nodes

``-A`` ``--kernelargs`` Set Kernel argument for nodes

``-c`` ``--cluster`` Set the node's cluster group

``-P`` ``--ipxe`` Set the node's iPXE template name

``-i`` ``--init`` Define the init process to boot the container

``--root`` Define the rootfs

``-R`` ``--runtime`` Set the node's runtime overlay

``-S`` ``--system`` Set the node's system overlay

``--ipmi`` Set the node's IPMI IP address

``--ipminetmask`` Set the node's IPMI netmask

``--ipmigateway`` Set the node's IPMI gateway

``--ipmiuser`` Set the node's IPMI username

``--ipmipass`` Set the node's IPMI password

``-p`` ``--addprofile`` Add Profile(s) to node

``-r`` ``--delprofile`` Remove Profile(s) to node

``-N`` ``--netdev`` Define the network device to configure

``-I`` ``--ipaddr`` Set the node's network device IP address

``-M`` ``--netmask`` Set the node's network device netmask

``-G`` ``--gateway`` Set the node's network device gateway

``-H`` ``--hwaddr`` Set the node's network device HW address

``--netdel`` Delete the node's network device

``--netdefault`` Set this network to be default

``-a`` ``--all`` Set all nodes

``-y`` ``--yes`` Set 'yes' to all questions asked

``-f`` ``--force`` Force configuration (even on error)

``--discoverable`` Make this node discoverable

``--undiscoverable`` Remove the discoverable flag

overlay
-------

Management interface for Warewulf overlays

build
~~~~~

chmod
~~~~~

create
~~~~~~

delete
~~~~~~

edit
~~~~

imprt
~~~~~

list
~~~~

mkdir
~~~~~

show
~~~~

power
-----

This command can control the power state of nodes.

cycle
~~~~~

off
~~~

on
~~

status
~~~~~~

profile
-------

Management of node profile settings

add
~~~

delete
~~~~~~

list
~~~~

set
~~~

ready
-----

Warewulf Status Check

server
------

This command will allow you to control the Warewulf daemon process.

start
~~~~~

status
~~~~~~

stop
~~~~
