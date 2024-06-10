=====================================
Ansible Network Restore Release Notes
=====================================

.. contents:: Topics

v2.0.0
======

Release Summary
---------------

Starting from this release, the minimum `ansible-core` version this collection requires is `2.15.0`. The last known version compatible with ansible-core<2.15 is v1.0.0.

Major Changes
-------------

- Bumping `requires_ansible` to `>=2.15.0`, since previous ansible-core versions are EoL now.

Bugfixes
--------

- replace random Hard Coded values for Juniper restore operation.

v1.0.0
======

Minor Changes
-------------

- Add support for SCM operations to fetch backed-up files from Github.
- Fix the tasks to make the copied files cleanup for Junos.
- Implement cli_restore tasks workflow for eos appliance.
- Redesigned network restore w.r.t validated content pattern for network backup.
- Revise the task sequence for IOS XR appliance to enhance efficiency.
- Support deploy_collection action.

Bugfixes
--------

- Enable platfom specific network.restore options.

Documentation Changes
---------------------

- Amend the README file to specify the minimum required platform collections.
- Update local datastore backup example.
- Update the reference to OpenSSF Best Practices for better alignment.
