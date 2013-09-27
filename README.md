Access Control List-for MYFS Filesystem
======================================



New ACL mechanism for UFS based “MYFS” filesystem in FreeBSD
This project involves a new kind of filesystem called "MYFS" filesystem. This file system is based on UFS but with no system ACL support. 
This project involved modification to MYFS filesystem to incorporate a new ACL mechanism which supplements normal file permissions but 
in slightly different way than what actual system ACLs do.

This ACL is only for the files stored in MYFS filesystem. These do not apply to the files stored elsewhere in the system. 
This new ACL support is added to the filesystem by modifying the on disk inode structure to hold the ACLs for the group-ids and user-ids. 
Three new system calls have been added to the FreeBSD kernel in order to implement this ACL mechanism.

int setacl(char *name, int type, int idnum, int perms)

int getacl(char *name, int type, int idnum)

int clearacl(char *name, int type, int idnum)

Manual pages have also been created for these system calls as a part of the projects

The vnode access operation of the MYFS filesystem has been modified such that open(2) and exec(2) system calls follow the new ACL while 
accessing the files in MYFS filesystem. When accessing the files not in MYFS filesystem, these two system calls behave as usual.
