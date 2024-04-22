=====================================
Ansible Network Restore Release Notes
=====================================

.. contents:: Topics


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
