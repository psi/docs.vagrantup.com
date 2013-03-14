---
sidebar_current: "gettingstarted-up"
---

# Up And SSH

It is time to boot your first guest machine. Run the following:

```
$ vagrant up
```

In less than a minute, this command will finish and you'll have a
virtual machine running Ubuntu. You won't actually _see_ anything though,
since Vagrant runs the virtual machine without a UI. To prove that it is
running, you can SSH into the machine:

```
$ vagrant ssh
```

This command will drop you into a full-fledged SSH session. Go ahead and
interact with the machine, `rm -rf /` (in the SSH prompt!), do whatever you want.

Take a moment to think what just happened: With just one line of configuration
and one command in your terminal, we brought up a fully functional, SSH accessible
virtual machine. Cool.

When you're done fiddling around with the machine, run `vagrant destroy`
back on your host machine, and Vagrant will remove all traces of the
virtual machine.
