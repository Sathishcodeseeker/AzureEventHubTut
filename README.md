# Azure Event Hubs - Complete Guide

This repository contains comprehensive documentation for Azure Event Hubs, covering security, architecture, and integration patterns.

## Table of Contents

1. [Least Privilege Access Policy](01-least-privilege-access.md)
2. [Managed Identities Overview](02-managed-identities.md)
3. [System-Assigned vs User-Assigned Identities](03-system-vs-user-assigned.md)
4. [Partition Keys - When and How to Use](04-partition-keys.md)
5. [Ordering Requirements](05-ordering-requirements.md)
6. [Offset and Checkpointing in Banking Apps](06-offset-and-checkpointing.md)
7. [How Offset is Maintained Internally](07-offset-maintenance.md)
8. [Databricks Integration with Event Hubs](08-databricks-integration.md)

## Quick Start

For a quick overview, start with:
- [Managed Identities Overview](02-managed-identities.md)
- [Partition Keys Guide](04-partition-keys.md)

For banking/financial applications:
- [Offset and Checkpointing](06-offset-and-checkpointing.md)
- [Ordering Requirements](05-ordering-requirements.md)

## Use Cases

### E-commerce Platform
- Use partition keys with `orderId`
- Implement checkpointing after database commits
- Use System-Assigned identities for isolated services

### Banking Application
- Mandatory ordering for transactions
- Checkpoint after every event
- Implement idempotency checks
- Use User-Assigned identities for shared services

### IoT Platform
- Use partition keys with `deviceId`
- Time-series ordering required
- Batch checkpointing acceptable

## Contributing

This documentation is based on real-world scenarios and best practices. Feel free to suggest improvements.

## License

MIT License
