# KVM/QEMU Windows guest drivers (virtio-win) #

## Dummy change

This repository contains KVM/QEMU Windows guest drivers, for both
paravirtual and emulated hardware. The code builds and ships as part
of the virtio-win RPM on Fedora and Red Hat Enterprise Linux, and the
binaries are also available in the form of distribution-neutral ISO
and VFD images. If all you want is use virtio-win in your Windows
virtual machines, go to
https://fedoraproject.org/wiki/Windows_Virtio_Drivers for information
on obtaining the binaries.

If you'd like to build virtio-win from sources, clone this repo and
follow the instructions in
https://github.com/virtio-win/kvm-guest-drivers-windows/wiki/Building-the-drivers.
Note that the drivers you build will be either unsigned or test-signed
with Tools/VirtIOTestCert.cer, which means that Windows will not load
them by default. See
https://docs.microsoft.com/en-us/windows-hardware/drivers/install/installing-test-signed-driver-packages
for more information on test-signing.

If you want to build cross-signed binaries (like the ones that ship in
the Fedora RPM), you'll need your own code-signing certificate.
Cross-signed drivers can be used on all versions of Windows except for
the latest Windows 10 with secure boot enabled. However, systems with
cross-signed drivers will not receive Microsoft support.

If you want to produce Microsoft-signed binaries (fully supported,
like the ones that ship in the Red Hat Enterprise Linux RPM), you'll
need to submit the drivers to Microsoft along with a set of test
results (so called WHQL process). If you decide to WHQL the drivers,
make sure to base them on commit eb2996de or newer, since the GPL
license used prior to this commit is not compatible with WHQL.
Additionally, we ask that you make a change to the Hardware IDs so
that your drivers will *not* match devices exposed by the upstream
versions of KVM/QEMU. This is especially important if you plan to
distribute the drivers with Windows Update, see
https://docs.microsoft.com/en-us/windows-hardware/drivers/dashboard/publishing-restrictions
for more details.

- - - -

[![Build Status](https://ci.appveyor.com/api/projects/status/github/virtio-win/kvm-guest-drivers-windows?branch=master&svg=true)](https://ci.appveyor.com/project/daynix/kvm-guest-drivers-windows)
