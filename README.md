# Ansible Network Restore

[![CI](https://github.com/redhat-cop/network.restore/actions/workflows/tests.yml/badge.svg?branch=main)](https://github.com/redhat-cop/network.restore/actions/workflows/tests.yml)[![OpenSSF Best Practices](https://bestpractices.coreinfrastructure.org/projects/7660/badge)](https://bestpractices.coreinfrastructure.org/projects/7660)

This repository contains the `network.restore` Ansible Collection.

## About

- Ansible Network restore Collection contains the role that provides a platform-agnostic way of
  managing restore resources. This collection provides the user the capabilities to gather,
  deploy, remediate, configure and perform health checks for network restore resources.

- Network restore collection can be used by anyone who is looking to manage and maintain restore resources. This includes system administrators and IT professionals.

## Requirements

- [Requires Ansible](https://github.com/redhat-cop/network.restore/blob/main/meta/runtime.yml)
- [Requires Content Collections](https://github.com/redhat-cop/network.restore/blob/main/galaxy.yml#L5https://forum.ansible.com/c/news/5/none)
- [Testing Requirements](https://github.com/redhat-cop/network.restore/blob/main/test-requirements.txt)
- Users also need to include platform collections as per their requirements. The supported platform collections are:
  - [arista.eos](https://github.com/ansible-collections/arista.eos)
  - [cisco.ios](https://github.com/ansible-collections/cisco.ios)
  - [cisco.iosxr](https://github.com/ansible-collections/cisco.iosxr)
  - [cisco.nxos](https://github.com/ansible-collections/cisco.nxos)
  - [junipernetworks.junos](https://github.com/ansible-collections/junipernetworks.junos)

## Installation
To consume this Validated Content from Automation Hub, the following needs to be added to ansible.cfg:
```
[galaxy]
server_list = automation_hub

[galaxy_server.automation_hub]
url=https://console.redhat.com/api/automation-hub/content/published/
auth_url=https://sso.redhat.com/auth/realms/redhat-external/protocol/openid-connect/token
token=<SuperSecretToken>
```

Get the required token from the [Automation Hub Web UI](https://console.redhat.com/ansible/automation-hub/token).

With this configured, simply run the following commands:

```
ansible-galaxy collection install network.base
ansible-galaxy collection install network.restore
```

## Use Cases

#### Fetch backup and restore a network appliance's configuration.
```yaml
run.yml
---
- name: The network.restore play
  hosts: ios
  gather_facts: true

  tasks:
    - name: The network restore task
      ansible.builtin.include_role:
        name: network.restore.run
      vars:
        operation: restore
        network_backup_path: ./network_local_backup/network/backup_iosxe.cfg
        delete_backup_from_dest: true
```

#### Task Output.
```
PLAYBOOK: cli_restore_val.yaml *************************************************
1 plays in cli_restore_val.yaml

PLAY [The network.restore workflow] ********************************************

TASK [Gathering Facts] *********************************************************
ok: [<ROBIN>]

TASK [setup] *******************************************************************
ok: [<ROBIN>]

TASK [Network restore task] ****************************************************

TASK [network.restore.run : Include tasks] *************************************

TASK [network.restore.run : Set supported platform list] ***********************
ok: [<ROBIN>] => changed=false
  ansible_facts:
    supported_platforms:
    - ios
    - junos
    - eos
    - nxos
    - iosxr
    - vyos

TASK [network.restore.run : Conditional test] **********************************
task path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/validation.yaml:12
skipping: [<ROBIN>] => changed=false
  false_condition: ansible_network_os.split('.')[-1] not in supported_platforms
  skip_reason: Conditional result was False

TASK [network.restore.run : Run the platform specific tasks] *******************
task path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/tasks/main.yaml:5
included: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/restore.yaml for <ROBIN> => (item=/wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/restore.yaml)

TASK [network.restore.run : Include tasks] *************************************
task path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/restore.yaml:2
included: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/network.yaml for <ROBIN>

TASK [network.restore.run : Invoke backup task] ********************************
task path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/network.yaml:2
Loading collection ansible.netcommon from /wayne/manor/collections/ansible_collections/ansible/netcommon
included: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/cli_restore.yaml for <ROBIN>

TASK [network.restore.run : Set content specific facts] ************************
ok: [<ROBIN>] => changed=false
  ansible_facts:
    delete_backup_from_dest: false
    delete_path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/delete
    file_name: 2024-02-06_ios_10.0.148.141
    health_check_path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/health_checks
    network_os: ios
    prepare_path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/prepare
    tmplt_path: /wayne/manor/collections/ansible_collections/network/restore/roles/run/includes/health_checks/templates

TASK [network.restore.run : Check if file copy is possible] ********************
Loading collection ansible.utils from /wayne/manor/collections/ansible_collections/ansible/utils

TASK [network.restore.run : Parse free space information] **********************
ok: [<ROBIN>] => changed=false
  ansible_facts:
    appliance_dir_data:
      free_bytes: 4012376064
      total_bytes: 5183766528
  parsed:
    free_bytes: 4012376064
    total_bytes: 5183766528
  stdout: 5183766528 bytes total (4012376064 bytes free)
  stdout_lines: <omitted>

TASK [network.restore.run : Check restore file size] ***************************
ok: [<ROBIN>] => changed=false
  invocation:
    module_args:
      checksum_algorithm: sha1
      follow: false
      get_attributes: true
      get_checksum: true
      get_md5: false
      get_mime: true
      path: /wayne/manor/backup_ios_scp_osp.cfg
  stat:
    atime: 1707218551.419256
    attr_flags: ''
    attributes: []
    block_size: 4096
    blocks: 16
    charset: us-ascii
    checksum: bd60f2a14785e6fc117f1f124c0db00154f09442
    ctime: 1707219264.2849615
    dev: 40
    device_type: 0
    executable: false
    exists: true
    gid: 1000
    gr_name: sagpaul
    inode: 33165538
    isblk: false
    ischr: false
    isdir: false
    isfifo: false
    isgid: false
    islnk: false
    isreg: true
    issock: false
    isuid: false
    mimetype: text/plain
    mode: '0644'
    mtime: 1707219264.2849615
    nlink: 1
    path: /wayne/manor/backup_ios_scp_osp.cfg
    pw_name: sagpaul
    readable: true
    rgrp: true
    roth: true
    rusr: true
    size: 5929
    uid: 1000
    version: '1789007'
    wgrp: false
    woth: false
    writeable: true
    wusr: true
    xgrp: false
    xoth: false
    xusr: false

TASK [network.restore.run : Inspect appliance size] ****************************
ok: [<ROBIN>] =>
  appliance_dir_data:
    free_bytes: 4012376064
    total_bytes: 5183766528

TASK [network.restore.run : Inspect restore file size] *************************
ok: [<ROBIN>] =>
  restore_file_data:
    changed: false
    failed: false
    stat:
      atime: 1707218551.419256
      attr_flags: ''
      attributes: []
      block_size: 4096
      blocks: 16
      charset: us-ascii
      checksum: bd60f2a14785e6fc117f1f124c0db00154f09442
      ctime: 1707219264.2849615
      dev: 40
      device_type: 0
      executable: false
      exists: true
      gid: 1000
      gr_name: sagpaul
      inode: 33165538
      isblk: false
      ischr: false
      isdir: false
      isfifo: false
      isgid: false
      islnk: false
      isreg: true
      issock: false
      isuid: false
      mimetype: text/plain
      mode: '0644'
      mtime: 1707219264.2849615
      nlink: 1
      path: /wayne/manor/backup_ios_scp_osp.cfg
      pw_name: sagpaul
      readable: true
      rgrp: true
      roth: true
      rusr: true
      size: 5929
      uid: 1000
      version: '1789007'
      wgrp: false
      woth: false
      writeable: true
      wusr: true
      xgrp: false
      xoth: false
      xusr: false

TASK [network.restore.run : Assert file sizes] *********************************
ok: [<ROBIN>] => changed=false
  msg: All assertions passed

TASK [network.restore.run : Copy file from src to a network device] ************
changed: [<ROBIN>] => changed=true
  destination: flash:2024-02-06_ios_10.0.148.141.txt

TASK [network.restore.run : Prepare appliance for a restore operation] *********
Loading collection cisco.ios from /wayne/manor/collections/ansible_collections/cisco/ios

TASK [network.restore.run : Overwrite startup config - archive] ****************
changed: [<ROBIN>] => changed=true
  banners: {}
  commands:
  - archive
  invocation:
    module_args:
      after: null
      backup: false
      backup_options: null
      before: null
      defaults: false
      diff_against: null
      diff_ignore_lines: null
      intended_config: null
      lines:
      - archive
      match: line
      multiline_delimiter: '@'
      parents: null
      replace: line
      running_config: null
      save_when: never
      src: null
  updates:
  - archive

TASK [network.restore.run : Dir the flash] *************************************
ok: [<ROBIN>] => changed=false
  invocation:
    module_args:
      commands:
      - answer: null
        check_all: false
        command: dir
        newline: true
        output: null
        prompt: null
        sendonly: false
      interval: 1
      match: all
      retries: 9
      wait_for: null
  stdout:
  - |-
    Directory of bootflash:/

    20      -rw-             5929   Feb 6 2024 11:35:19 +00:00  2024-02-06_ios_10.0.148.141.txt
    131075  drwx            12288   Feb 6 2024 11:15:47 +00:00  tracelogs
    31      -rw-             5932   Feb 5 2024 11:53:55 +00:00  "<ROBIN>.txt
    131096  drwx             4096   Feb 1 2024 05:56:20 +00:00  .dbpersist
    131203  drwx             4096   Feb 1 2024 05:22:00 +00:00  pnp-tech
    131078  drwx             4096   Feb 1 2024 05:14:11 +00:00  .installer
    131074  drwx             4096   Feb 1 2024 05:11:34 +00:00  pnp-info
    17      -rw-              618   Feb 1 2024 05:10:52 +00:00  cvac.log
    19      -rw-              209   Feb 1 2024 05:10:51 +00:00  csrlxc-cfg.log
    131104  drwx             4096   Feb 1 2024 05:10:50 +00:00  license_evlog
    18      -rw-              244   Feb 1 2024 05:10:08 +00:00  .iox_dir_list
    131107  drwx             4096   Feb 1 2024 05:10:06 +00:00  guest-share
    131082  drwx             4096   Feb 1 2024 05:10:06 +00:00  iox_host_data_share
    131105  drwx             4096   Feb 1 2024 05:10:01 +00:00  onep
    131073  drwx             4096   Feb 1 2024 05:09:57 +00:00  .prst_sync
    16      -rw-               30   Feb 1 2024 05:09:55 +00:00  throughput_monitor_params
    131094  drwx             4096   Feb 1 2024 05:09:31 +00:00  virtual-instance
    14      -rw-            20109   Feb 1 2024 05:09:28 +00:00  ios_core.p7b
    15      -rw-             1923   Feb 1 2024 05:09:28 +00:00  trustidrootx3_ca_092024.ca
    13      -rw-              420   Feb 1 2024 05:09:26 +00:00  mode_event_log
    131079  drwx             4096   Feb 1 2024 05:09:25 +00:00  core
    131088  drwx             4096   Feb 1 2024 05:09:25 +00:00  .rollback_timer
    131083  drwx             4096   Feb 1 2024 05:09:21 +00:00  bootlog_history
    131080  drwx             4096   Feb 1 2024 05:09:08 +00:00  appqoe-service
    29      -rw-         51443114  Nov 24 2021 08:39:15 +00:00  c8000v-rpboot.17.06.02.SPA.pkg
    21      -rw-        754697304  Nov 24 2021 08:39:15 +00:00  c8000v-mono-universalk9.17.06.02.SPA.pkg
    27      -rw-         11568204  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_nim_shdsl.17.06.02.SPA.pkg
    23      -rw-         11760716  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_ngwic_t1e1.17.06.02.SPA.pkg
    28      -rw-          5571656  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_nim_xdsl.17.06.02.SPA.pkg
    11      -rw-             5918  Nov 24 2021 08:39:14 +00:00  packages.conf
    26      -rw-          4387912  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_nim_ge.17.06.02.SPA.pkg
    24      -rw-         12981324  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_nim_async.17.06.02.SPA.pkg
    22      -rw-          2376780  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_dsp_sp2700.17.06.02.SPA.pkg
    25      -rw-         17708104  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_nim_cwan.17.06.02.SPA.pkg
    12      -rw-            66636  Nov 24 2021 08:39:14 +00:00  c8000v-firmware_dreamliner.17.06.02.SPA.pkg

    5183766528 bytes total (4012367872 bytes free)
  stdout_lines: <omitted>

TASK [network.restore.run : Restore operation] *********************************
ok: [<ROBIN>] => changed=false
  __restore__: |-
    The rollback configlet from the last pass is listed below:
    ********
    !List of Rollback Commands:
    crypto pki certificate chain TP-self-signed-2288105345
     certificate self-signed 01
      no    quit
    crypto pki certificate chain SLA-TrustPoint
     certificate ca 01
      no    quit
    Building configuration...
    Current configuration : 5911 bytes
    crypto pki certificate chain SLA-TrustPoint
     certificate ca 01
      D697DF7F 28
            quit
    crypto pki certificate chain TP-self-signed-2288105345
     certificate self-signed 01
      C16CE4EE 8FE16F47 F7904EA1 6A3D046D E611F2D7
            quit
    end
    ********


    Rollback aborted after 5 passes
    The following commands are failed to apply to the IOS image.
    ********
    no      quit
    certificate ca 01
    Building configuration...
    Current configuration : 5911 bytes
    D697DF7F 28
    quit
    C16CE4EE 8FE16F47 F7904EA1 6A3D046D E611F2D7
    ********
  invocation:
    module_args:
      filename: 2024-02-06_ios_10.0.148.141.txt
      force: true

TASK [network.restore.run : Delete backup from appliance] **********************

TASK [network.restore.run : Make file promt quite] *****************************
changed: [<ROBIN>] => changed=true
  banners: {}
  commands:
  - file prompt quiet
  invocation:
    module_args:
      after: null
      backup: false
      backup_options: null
      before: null
      defaults: false
      diff_against: null
      diff_ignore_lines: null
      intended_config: null
      lines:
      - file prompt quiet
      match: line
      multiline_delimiter: '@'
      parents: null
      replace: line
      running_config: null
      save_when: never
      src: null
  updates:
  - file prompt quiet

TASK [network.restore.run : Delete the backup file post backup] ****************
ok: [<ROBIN>] => changed=false
  invocation:
    module_args:
      commands:
      - answer: null
        check_all: false
        command: delete /force flash:2024-02-06_ios_10.0.148.141.txt
        newline: true
        output: null
        prompt: null
        sendonly: false
      interval: 1
      match: all
      retries: 9
      wait_for: null
  stdout:
  - ''
  stdout_lines: <omitted>

PLAY RECAP *********************************************************************
<ROBIN>               : ok=22   changed=3    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```

## Testing

The project uses tox to run `ansible-lint` and `ansible-test sanity`.
Assuming this repository is checked out in the proper structure,
e.g. `collections_root/ansible_collections/network/restore`, run:

```shell
  tox -e ansible-lint
  tox -e py39-sanity
```

To run integration tests, ensure that your inventory has a `network_base` group.
Depending on what test target you are running, comment out the host(s).

```shell
[network_hosts]
ios
nxos

[ios:vars]
< enter inventory details for this group >

[nxos:vars]
< enter inventory details for this group >
```

```shell
  ansible-test network-integration -i /path/to/inventory --python 3.9 [target]
```

## Contributing

We welcome community contributions to this collection. If you find problems, please open an issue or create a PR against this repository.

Don't know how to start? Refer to the [Ansible community guide](https://docs.ansible.com/ansible/devel/community/index.html)!

Want to submit code changes? Take a look at the [Quick-start development guide](https://docs.ansible.com/ansible/devel/community/create_pr_quick_start.html).

We also use the following guidelines:

* [Collection review checklist](https://docs.ansible.com/ansible/devel/community/collection_contributors/collection_reviewing.html)
* [Ansible development guide](https://docs.ansible.com/ansible/devel/dev_guide/index.html)
* [Ansible collection development guide](https://docs.ansible.com/ansible/devel/dev_guide/developing_collections.html#contributing-to-collections)

### Code of Conduct
This collection follows the Ansible project's
[Code of Conduct](https://docs.ansible.com/ansible/devel/community/code_of_conduct.html).
Please read and familiarize yourself with this document.

## Release notes

Release notes are available [here](https://github.com/redhat-cop/network.restore/blob/main/CHANGELOG.rst).

## Related information

- [Developing network resource modules](https://github.com/ansible-network/networking-docs/blob/main/rm_dev_guide.md)
- [Ansible Networking docs](https://github.com/ansible-network/networking-docs)
- [Ansible Collection Overview](https://github.com/ansible-collections/overview)
- [Ansible Roles overview](https://docs.ansible.com/ansible/2.9/user_guide/playbooks_reuse_roles.html)
- [Ansible User guide](https://docs.ansible.com/ansible/latest/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html)
- [Ansible Community Code of Conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html)

## Licensing

GNU General Public License v3.0 or later.

See [LICENSE](https://www.gnu.org/licenses/gpl-3.0.txt) to see the full text.
