.. _wwctl-build:

===========
wwctl build
===========

Warewulf build is used to build VNFS, kernel, and system-overlay objects for provisioning. The default usage will be to build and/or update anything that seems to be needed.

-V, --container  Build and/or update VNFS images.
-K, --kernel  Build and/or update Kernel images.
-R, --runtime  Build and/or update runtime overlays
-S, --system  Build and/or update system overlays
-A, --all  Build and/or update all components
-f, --force  Force build even if nothing has been updated.
