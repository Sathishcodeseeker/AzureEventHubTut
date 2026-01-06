# Least Privilege Access Policy

## Overview

**Least Privilege** is a fundamental security principle that states users, programs, and processes should be granted only the **minimum levels of access** necessary to perform their job functions.

## Core Principle

Grant the **bare minimum** permissions required:
- Users get access to only what they need, when they need it
- Reduces the attack surface and potential damage from breaches

## Main Components

### 1. Need-to-know basis
Access only to data/systems required for specific tasks

### 2. Time-limited access
Temporary elevated privileges when needed

### 3. Role-based access
Permissions tied to job roles, not individuals

### 4. Regular reviews
Periodic audits to remove unnecessary permissions

## Benefits

✅ **Reduces security risks** - Limits damage from compromised accounts  
✅ **Minimizes insider threats** - Restricts what malicious insiders can access  
✅ **Improves compliance** - Meets regulatory requirements (GDPR, HIPAA, SOC 2)  
✅ **Limits lateral movement** - Attackers can't easily move through systems  
✅ **Better audit trails** - Easier to track who accessed what

## Azure Event Hubs RBAC Roles

| Role | Permissions | Use Case |
|------|------------|----------|
| **Azure Event Hubs Data Owner** | Full access (send, receive, manage) | Admins only |
| **Azure Event Hubs Data Sender** | Send events only | Producer applications |
| **Azure Event Hubs Data Receiver** | Receive events only | Consumer applications |
| **Reader** | Read metadata only | Monitoring/auditing |

## Best Practices

1. **Separate sender and receiver identities**
   - Producer apps: Only "Data Sender" role
   - Consumer apps: Only "Data Receiver" role

2. **Use Managed Identities** (avoid storing credentials)
   - System-assigned or User-assigned identities
   - No secrets in code or config files

3. **Scope permissions to specific resources**
   - Namespace level (all Event Hubs)
   - Event Hub level (specific hub)
   - Consumer Group level (specific consumer group)

4. **Avoid "Owner" or "Data Owner" roles** in production

5. **Use separate Event Hubs** for different security zones

## Examples

### Good Practice ✅
