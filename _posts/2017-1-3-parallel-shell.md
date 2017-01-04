---
layout: post
title:  "Parallel Shell Utilities"
tags: hpc software utilities
---

> The most fundamental tool needed to administer a cluster is a parallel shell, which allows you to run the same command on a series of nodes.
>
> [Linux Magazine](http://www.linux-magazine.com/Issues/2014/166/Parallel-Shells)


There are 3 popular ways to perform parallel actions on HPC clusters:
- Using a shell script
- Using Pdsh
- Using ClusterShell

No extra installation is needed to use the shell script method but you'll have to install Pdsh and ClusterShell if you want to use them. The [OpenHPC stack](https://github.com/openhpc/ohpc) comes with them pre-packaged. I won't be going over how to install them, but installation is simple with provided package managers.

Before we dive into these 3 methods, its important to note that you should have ssh set up to authenticate with ssh keys, instead of a password for this to work. Don't skip this, or your'll have to enter your password way too many times!

## Using a shell script
This method can be done with any scripting language, but I'll use bash.

Create a script that you want ran:
```
#!/bin/bash

# You will need to run this script on a passwordless account!

for NODE in node1 node2 node3
do
    ssh $NODE uptime
done
```

And run it with `sh your-script.sh`. This will run your command on all nodes, one at a time, printing everything to the screen.

## Using Pdsh

> "Pdsh is a multithreaded remote shell client which executes commands on
 multiple remote hosts in parallel."
>
> [Pdsh Github](https://github.com/grondo/pdsh)

Using pdsh is simple enough:
```
# perform th uptime command on node1, node2, node3 and node 4
$ pdsh -w node[1-4] uptime
node1: 19:01:18 up 1 day, 19:19,  1 user,  load average: 0.29, 0.57, 0.53
node2: 19:11:25 up 1 day, 19:19,  1 user,  load average: 0.29, 0.57, 0.53
node3: 19:19:11 up 1 day, 19:19,  1 user,  load average: 0.29, 0.57, 0.53
node4: 19:20:45 up 1 day, 19:19,  1 user,  load average: 0.29, 0.57, 0.53
```


## Using ClusterShell

ClusterShell is built and maintained by CEA-HPC and claims to be effective on supercomputers with 5,000 compute nodes. Using ClusterShell is very similar to pdsh
```
$ clush -w foo[1-5] echo "Hello World"
```
ClusterShell does some merging of outputs and does a better job of handling hanging nodes than pdsh.

## References

[Bash for loop Syntax](https://www.cyberciti.biz/faq/bash-for-loop/)
[Pdsh github](https://github.com/grondo/pdsh)
[Pdsh man page](https://linux.die.net/man/1/pdsh)
[Pdsh vs ClusterShell](https://github.com/cea-hpc/clustershell/wiki/Pdsh)
[ClusterShell Github](https://github.com/cea-hpc/clustershell)
[ClusterShell main page](http://cea-hpc.github.io/clustershell/)