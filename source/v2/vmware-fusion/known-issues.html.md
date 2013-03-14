---
sidebar_current: "vmwarefusion-known-issues"
---

# Known Issues

This page tracks some known issues or limitations of the Fusion provider.
Note that none of these are generally blockers to using the provider, but
are good to know.

## vmnet Device Cleanup

When creating a private network with Fusion, the Vagrant provider will
create a new `vmnet` device for your IP/subnet if one doesn't already exist.
Vagrant currently never cleans up unused `vmnet` devices. This must be
done manually via the VMware Fusion network editor.

In practice, this is not an issue because there are really only
[three IPv4 address spaces](http://en.wikipedia.org/wiki/Private_network#Private_IPv4_address_spaces)
that can be used for these networks, so not many extraneous vmnet devices
are left lying around.

However, if you use automatically generated IP addresses that use many
subnets, you may find that there are many extra vmnet devices. Manually
remove these for now. A future release of the provider will address this
limitation in some way.
