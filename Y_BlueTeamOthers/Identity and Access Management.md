*NIST 800-63B: Digital Identity Guidelines*

## Access Control
**1. DAC (Discretionary AC)**
  - Policy determined by the owner (often used)
  - Each object needs an owner
  - Owner has to determine the access rights
      - chown, chmod, chroot

**2. MAC (Mandatory AC)**
  - Policy determined by the computer system
  - Security labels assigned to every user (subject)/data (object)
  - MAC uses "need-to-know" method prior accessing a file
  - Labels: Top Secret, Secret, Confidential, Classified etc.
  - Usually used in FreeBSD / SELinux / High-Sec Systems
  - Complex configuration!

**3. RBAC (Role-Based AC)**
  - Policy determined by computer system
  - Uses a set of permissions i/o single data label (MAC)
  - Different groups have specific permissions
  - Recommended for enterprises with >500 employees

**4. ABAC (Attribute-Based AC)**
  - Dynamic and context-aware using IF-THEN statements
  - Exp: If Jason is in HR, then give access to \\fileserver\HR
  - Most complex to implement but also most flexible !

## Propagation of Permissions
- Permissions are passed to subfolder from parent by inheritance
- Propagation is default setting in Windows
- Propagation can be disabled under folder settings

*--> copy: permissions are inherited from parent folder it is copied into*

*--> move: permissions are retained from its original parent folder*

## Best Practices
1. Implicit deny: only ressource-permission when explicitly stated
2. Disable Administrator account
3. Create new Admin account with discreet name
4. Least Privilege
   - Privilege creep violates principle of Least Privilege (!)
   - Rotating through diff. depts but keeping each depts permissions(!)
   - User Access Recertification: Revalidate Permissions (annually) (!)
5. Separation of Duties: e.g. sign/counter sign
6. Job rotation: reduce boredom, enhance skills, increase security
7. Mandatory vacation: Someone has to take over while you are away (fraud can be detected)
