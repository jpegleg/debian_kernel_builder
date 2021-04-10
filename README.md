# debian_kernel_builder
CI to build and compile custom kernels on Debian

The 'deb' build server should match the kernel version coded for best results.

A program called /usr/local/sbin/kbuildmods is maintained on the build server
separately from this repo. The kbuildmods program can be anything actually,
but the point is to do things such as make edits to the kernel code before
compiling.

The kernel version is intentionally hardcoded in the Jenkinsfile.
Just edit the Jenkinsfile to match the kernel version of your 'deb' Jenkins build server.
