# Ansible Playbook Collection

English | [日本語](README.ja.md)

## Description

This site provides Ansible Playbooks (Roles).  

## Role List

| Target Product | Version | Function | Role List | Summary | How to use | Remarks |
|---- |---- |---- |---- |---- |---- |---- |
| OS  | WS2016, RHEL7 | environmental construction | [os_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os_setup_list.yml) |This role provides functions to build the OS environment and change settings.|[Readme](https://github.com/exastro-playbook-collection/RHEL) | |
| OS  | WS2016, RHEL7 | parameter collection | [os_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os_scan_list.yml) |This role provides the ability to collect OS settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/OS_extracting) | |
| Apache 2.4 | RHEL7 | application setup | [apache24_linux_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/apache24_linux_setup_list.yml) |Install and configure Apache 2.4 on RHEL. |[Readme](https://github.com/exastro-playbook-collection/Apache_install)| |
| Apache 2.4 | WS2016| application setup | [apache24_windows_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/apache24_windows_setup_list.yml) |Install and configure Apache 2.4 on WS2016. |[Readme](https://github.com/exastro-playbook-collection/Apache24_WIN_install)| |
| Apache 2.4 | WS2016, RHEL7 | parameter collection | [apache24_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/apache24_scan_list.yml) |Collect Apache 2.4 settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/Apache24_extracting_linux) | |
| IIS | WS2016 | application setup | [iis_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/iis_setup_list.yml) |Install and configure IIS on WS2016.|[Readme](https://github.com/exastro-playbook-collection/IIS_Install)| |
| IIS | WS2016 | parameter collection | [iis_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/iis_scan_list.yml) |Collect IIS settings and create a reusable parameter file on WS2016.|[Readme](https://github.com/exastro-playbook-collection/IIS_WS2016_extracting)| |
| IIS | WS2019 | application setup | [iis_ws2019_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/iis_ws2019_setup_list.yml) |Install and configure IIS on WS2019.|[Readme](https://github.com/exastro-playbook-collection/IIS_WS2019_Install)| |
| IIS | WS2019 | parameter collection | [iis_ws2019_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/iis_ws2019_scan_list.yml) |Collect IIS settings and create a reusable parameter file on WS2019.|[Readme](https://github.com/exastro-playbook-collection/IIS_WS2019_extracting)| |
| SQL Server | WS2016 | application setup | [sql_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/sql_setup_list.yml) |Check and prepare an environment, and Install SQL Server.|[Readme](https://github.com/exastro-playbook-collection/SqlServer_preinstall)| |
| Zabbix Agent 4.0 | RHEL6,7 | application setup | [zabbix40_agent_linux_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/zabbix40_agent_linux_setup_list.yml) |Install and configure Zabbix Agent 4.0 on RHEL6 or 7.|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Agent_install)| |


## Support

For more details, refer to "How to use" of each role.  

## Usage

Shown an example of OS parameter collection below.  

### Pre-work

The following steps will be executed on Ansible server unless otherwise specified.

1. Build Ansible server and login as a user with sudo privileges.

2. Install git.  
    ```
    $ sudo yum -y install git
    ```

3. Create a working folder and change to the folder.  
    ```
    $ mkdir ansible_work
    $ cd ansible_work/
    ```

4. Download the [Role List for Parameter Generation Common Parts](https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml) and place it in the folder you created in step (3).  

5. Download a role with the ansible-galaxy Command.  
    ```
    $ ansible-galaxy install -r prerequire_list.yml -p roles
    ```

6. Create a playbook and an inventory file.  
    * Playbook(prerequire.yml)
        ```
        ---
        - hosts: local
          become: yes
          roles:
            - setup_paragen
        ```
    * Inventory(inventory)
        ```
        [local]
        localhost

        [local:vars]
        ansible_become_pass=<sudo password>
        ```

7. Run the playbook to install Parameter Generation Common Parts.
    ```
    $ ansible-playbook -c local -i inventory prerequire.yml
    ```

### Run Playbook

1. Download the roll list of the functions you want to use and place it in the folder where you want to create Playbook.  

2. Download a role with the ansible-galaxy Command.  
    ```
    $ ansible-galaxy install -r os_scan_list.yml -p roles
    ```

3. Create a playbook and an inventory file referencing "How to use" of each role.  
    * Playbook(os_scan.yml)
        ```
        ---
        - hosts: <Target Group Name>
          roles:
        　　　：
        ```
    * Inventory(inventory)
        ```
        [<Target Group Name>]
        xxx.xxx.xxx.xxx

        [<Target Group Name>:vars]
        ansible_user=<user with sudo privileges>
        ansible_password=<password for the above user account>
        　　　：
        ```

4. Run the playbook to collect OS settings.  
    ```
    $ ansible-playbook -i inventory os_scan.yml
    ```
