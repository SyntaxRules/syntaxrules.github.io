---
layout: post
title:  "Restricting User Access via SLURM"
tags: hpc software slurm
---
Making it so users can only ssh into the nodes they have reserved is built into SLURM. I had a hard time finding all the steps in one place, here's what I did.

Using centos 7.x you'll need to edit two files (both in the compute node image a.k.a vnfs):
1. $CHROOT/etc/pam.d/password-auth
2. $CHROOT/etc/security/access.conf

Where $CHROOT is the location to your image. Edit the files like so:

Edit $CHROOT/etc/pam.d/password-auth:

```
account     required      pam_unix.so
account     required      pam_slurm.so  # Add this line, below pam_unix.so, but above everything else
account     sufficient    pam_localuser.so
account     sufficient    pam_succeed_if.so uid < 500 quiet 
account     required      pam_permit.so 
```

Edit $CHROOT/etc/security/access.conf:

```
# All other users should be denied to get access from all sources. 
+ : root : ALL    # Uncomment or add this line at the bottom of the file
- : ALL  : ALL    # Uncomment or add this line at the bottom of the file
```

Now rebuild and apply your image/vnfs to the nodes. (Not covered here.)

Test it out:

```
[sr@sms ~]$ ssh compute-1
Access denied: user sr (uid=1) has no active jobs on this node.
Connection closed by 192.168.x.x
[sr@sms ~]$ salloc -n 1
salloc: Granted job allocation 71
[sr@sms ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                71    shared     bash     sr   R       0:04      1 compute-1
[sr@sms ~]$ ssh compute-1
[sr@compute-1 ~]$ # Note we can log in now!
[sr@compute-1 ~]$ exit
logout
Connection to knl-36 closed.
[sr@sms ~]$ scancel 71
salloc: Job allocation 71 has been revoked.
```

## References:

[How to set resource limits within SLURM](https://slurm.schedmd.com/faq.html#pam)

[Using PAM to secure userspace with SLURM](https://groups.google.com/forum/#!topic/slurm-devel/sVkZ1FFVq5s)
