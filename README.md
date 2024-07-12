# Ansible Network Restore

## Notice of Consolidation and Archival

The `network.restore` validated content has been consolidated into the `network.backup` validated content to streamline and enhance the functionality of network backup and restore operations.

### New Location

All functionalities previously provided by the `network.restore` collection are now available in the `network.backup` collection. You can find the updated and consolidated validated content at the following repository:

[network.backup Validated Content](https://github.com/redhat-cop/network.backup)

### Archival Information

As a result of this consolidation, the `network.restore` repository is now archived and will no longer be maintained. We encourage all users to transition to the `network.backup` collection for continued support and updates.

### Migration Guide

To migrate your existing playbooks and roles to the `network.backup` collection, please follow these steps:
1. Update your playbooks to include the `network.backup` collection.
2. Replace any instances of `network.restore` roles with the corresponding `network.backup` roles.
3. Review the [network.backup documentation](https://github.com/redhat-cop/network.backup) for any additional changes or enhancements.

### Support and Contributions

For any issues, questions, or contributions, please refer to the `network.backup` repository. We appreciate your understanding and cooperation during this transition.

Thank you for using `network.restore`.
