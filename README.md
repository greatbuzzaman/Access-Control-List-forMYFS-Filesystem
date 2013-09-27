Access-Control-List-forMYFS-Filesystem
======================================



New ACL mechanism for UFS based “MYFS” filesystem in FreeBSD


TO modify the "myfs" filesystem to implement "Access control lists".
I firstly implemented two structures to hold the permissions for each "User-id" and "group-id", in myfs_dinode.h file.
Then implemented the setacl() according to requirement, making and array for both the structures of maximum 16 entries.
I compared on the basis of whether its the owner of file who is setting the permissions for different users or root,
 depending on the type passed in the system call function for Type 0 -uid and Type -1 for gid.
Permissions:
        - As usual root should be able to do anything so should be allowed
        - Only the owner can modify ACLs for a file.
        - Other users can see the ACL setting if it applies to them (so
          they are the UID mentioned in the ACL, or they are in the
          group being asked about) but not other ACL settings.
        - An ACL for a group can only be added if the calling process
          is a member of that group.

similarly implemented teh clearacl() to clear permissions entry in Acl Lists byt the owner or root.

And finally implemented getacl() to check for its permissons in acl list for file.
