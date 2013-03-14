---
sidebar_current: "providers-configuration"
---

# Configuration

While well-behaved providers should work with any Vagrantfile with sane
defaults, providers generally expose unique configuration
options so that you can get the most out of each provider.

This provider-specific configuration is done within the Vagrantfile
in a way that is portable, easy to use, and easy to understand.

## Portability

An important fact is that even if you configure other providers within
a Vagrantfile, the Vagrantfile remains portable even to individuals who
don't necessarilly have that provider installed.

For example, if you configure VMware Fusion and send it to an individual
who doesn't have the VMware Fusion provider, Vagrant will silently ignore
that part of the configuration.

## Configuration

Configuring a specific provider looks like this:

```
Vagrant.configure("2") do |config|
  # ... (other config)

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :name, "--cpuexecutioncap", "50"]
  end
end
```

Multiple `config.vm.provider` blocks can exist to configure multiple
providers.

The configuration format should look very similar to how provisioners
are configured. The `config.vm.provider` takes a single parameter: the
name of the provider being configured. Then, an inner block with custom
configuration options is exposed that can be used to configure that
provider.

This inner configuration differs among providers, so please read the
documentation for your provider of choice to see available configuration
options.

Remember, some providers don't require any provider-specific configuration
and work directly out of the box. Provider-specific configuration is meant
as a way to expose more options to get the most of the provider of your
choice. It is not meant as a roadblock to running against a specific provider.
