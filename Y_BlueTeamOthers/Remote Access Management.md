## Best Practices

1. Establish "Acceptable Use Policy"
2. Enforce Encryption 
3. Implement Multi-Factor Authentication (MFA)
4. When possible, only allow connections from company provisioned devices
5. Forbid Shared Access Accounts (better: individual basis!)
6. Evaluate the risks of remote access architecture you chose
   - Example: Web SSO may need WAF 
7. Enforce credential management security policies
8. Limit length and duration of sessions
9. Enforce network monitoring, least privilege and segregation of duty
   - Allows isolation, containment and deny of compromised users
10. Select "Network Level Authentication" in Remote Desktop Client Config (RDSG@Win)
    - prevent non-compliant clients and some hacking tools
