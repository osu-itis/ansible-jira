# ansible-jira

An ansible playbook for upgrading Jira.

## Configuration

### Inventory

Place inventory files in `inventory/`

Example inventory file:

```
[dev]
jira-dev.someplace.edu
```

### Variables

Create a variable file in `group_vars/` to match the previous inventory file.

Example file `group_vars/dev`:

```
---
jira:
    installer_url: https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-7.1.9-x64.bin
    installer_filename: atlassian-jira-software-7.1.9-x64.bin
    installer_temp_path: /tmp
    app_home: /var/atlassian/application-data/jira
    app_install: /opt/atlassian/jira
    modified_files:
        - /opt/atlassian/jira/conf/server.xml
        - /opt/atlassian/jira/bin/setenv.sh
use_proxy: proxy.someplace.edu:3128
```

* `installer_url`: URL for Jira installer package file
* `installer_filename`: filename for Jira installer package file
* `installer_temp_path`: temp directory to use while upgrading
* `app_home`: Jira application home path
* `app_install`: Jira application install path
* `modified_files`: locally modified config files that should be backed up before upgrading
* `use_proxy`: (OPTIONAL) proxy to use if needed

## Usage

```
$ ansible-playbook -i inventory/dev upgrade-jira.yml
```
