.. _wwctl:

=====
wwctl
=====

wwctl - Control interface to the Cluster Warewulf Provisioning System

Synopsis
~~~~~~~~

wwctl [GLOBAL OPTIONS] [SUBCOMMAND]

Options
~~~~~~~

-v, --verbose  Run with increased verbosity
-d, --debug  Run with debugging messages enabled

Environment
~~~~~~~~~~~

WAREWULF_OCI_NOHTTPS
    Skip TLS verification when connecting to an OCI registry

WAREWULF_OCI_PASSWORD
    OCI registry password used in ``wwctl container imprt``

WAREWULF_OCI_USERNAME
    OCI registry username used in ``wwctl container imprt``
