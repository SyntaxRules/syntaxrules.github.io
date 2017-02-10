

# Restricting User Access via SLURM

Files to edit:

Edit $CHROOT/etc/pam.d/password-auth: 
```
account     required      pam_unix.so 
account     required      pam_slurm.so   # Add this line, below pam_unix.so, but above everything else 
account     sufficient    pam_localuser.so 
account     sufficient    pam_succeed_if.so uid < 500 quiet 
account     required      pam_permit.so 
```

Edit $CHROOT/etc/security/access.conf: 
```
# All other users should be denied to get access from all sources. 
+ : root : ALL    <======== uncomment this line 
- : ALL  : ALL    <======== uncomment this line
```

Now rebuild and apply your vnfs to the nodes. (Not covered here.)

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

How to set resource limits with ins slurm: https://slurm.schedmd.com/faq.html#pam

Using PAM to secure userspace: https://groups.google.com/forum/#!topic/slurm-devel/sVkZ1FFVq5s
