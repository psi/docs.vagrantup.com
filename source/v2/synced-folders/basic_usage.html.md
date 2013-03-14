---
sidebar_current: "syncedfolder-basic"
---

# Basic Usage

## Configuration

Synced folders are configured within your Vagrantfile using the
`config.vm.synced_folder` method. Usage of the configuration directive
is very simple:

```ruby
Vagrant.configure("2") do |config|
  # other config here

  config.vm.synced_folder "src/", "/srv/website"
end
```

The first parameter is a path to a directory on the host machine. If
the path is relative, it is relative to the project root. The second
parameter must be an absolute path of where to share the folder within
the guest machine. This folder will be created (recursively, if it must)
if it doesn't exist.

## Enabling

Synced folders are automatically setup during `vagrant up` and
`vagrant reload`.
