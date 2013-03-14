---
sidebar_current: "vmwarefusion-configuration"
---

# Configuration

While VMware Fusion is a drop-in replacement for VirtualBox, there are
some additional features that are exposed that allow you to more finely
configure Fusion-specific aspects of your machines.

## Virtual Machine GUI

The VMware Fusion provider generally starts the virtual machines
in headless mode. If you'd like to see the UI because you're running
a desktop within the VM, or if you need to debug potential boot issues
with the VM, you can configure the Fusion provider to boot with the
GUI:

```ruby
config.vm.provider :vmware_fusion do |v|
  v.gui = true
end
```

## Sudo vs. Setuid

In order to control some aspects of Fusion, Vagrant requires root
privileges for some tasks. Instead of constantly asking for your password,
and to keep `vagrant up` as interaction-free as possible, the VMware Fusion
provider installs a binary with the [setuid](http://en.wikipedia.org/wiki/Setuid)
flag set to run as root to run these tasks. setuid binaries are generally
frowned upon because they pose potential security risks.

If you are uncomfortable with this, you can ask the provider to just use `sudo`
directly instead of attempting to use the setuid binary:

```ruby
config.vm.provider :vmware_fusion do |v|
  v.disable_setuid = true
end
```

<div class="alert alert-info">
	<h3>setuid uninstallation</h3>
	<p>
		If you previously installed the sudo helper with setuid privileges,
		then the configuration above will not uninstall it. A command
		to do this will be added in a future release.
	</p>
</div>

## VMX Customization

If you want to add or remove specific keys from the VMX file, you can do
that:

```ruby
config.vm.provider :vmware_fusion do |v|
  v.vmx["custom-key"]  = "value"
  v.vmx["another-key"] = nil
end
```

In the example above, the "custom-key" key will be set to "value" and the
"another-key" key will be removed from the VMX file.

VMX customization is done as the final step before the VMware machine is
booted, so you have the ability to possibly undo or misconfigure things
that Vagrant has set up itself.

VMX is an undocumented format and there is no official reference for
the available keys and values. This customization option is exposed for
people who have knowledge of exactly what they want.
