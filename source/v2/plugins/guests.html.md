---
sidebar_current: "plugins-guests"
---

# Plugin Development: Guests

This page documents how to add new guest OS implementations to Vagrant,
allowing Vagrant to properly configure new operating systems.
Prior to reading this, you should be familiar
with the [plugin development basics](/v2/plugins/development-basics.html).

<div class="alert alert-warn">
	<p>
		<strong>Warning: Advanced Topic!</strong> Developing plugins is an
		advanced topic that only experienced Vagrant users who are reasonably
		comfortable with Ruby should approach.
	</p>
</div>

Vagrant has many features that requires doing guest OS-specific
actions, such as mounting folders, configuring networks, etc. These
tasks vary from operating system to operating system. If you find that
one of these doesn't work for your operating system, then maybe the
guest implementation is incomplete or incorrect.

## Definition Component

Within the context of a plugin definition, new guests can be defined
like so:

```ruby
guest "ubuntu" do
  require_relative "guest"
  Guest
end
```

Guests are defined with the `guest` method. The first argument is the
name of the guest. This name isn't actually used anywhere, but may in the
future, so choose something helpful. Then, the block argument returns a
class that implements the `Vagrant.plugin(2, :guest)` interface.

## Implementation

Implementations of guests subclass `Vagrant.plugin(2, :guest)`. Within
this implementation, various methods for different tasks must be implemented.
Instead of going over each task, the easiest example would be to take a look
at an existing guest implementation.

There are [many guest implements](https://github.com/mitchellh/vagrant/tree/master/plugins/guests),
but you can view the [Linux guest implementation](https://github.com/mitchellh/vagrant/blob/master/plugins/guests/linux/guest.rb) as a starting point.
