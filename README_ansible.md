# Ansible Playbook Collection

English | [Japanese](README_ansible.ja.md)  

## Description

This site provides Ansible Playbooks (Roles).  

## Role List

| Target Product | Version | Function | Role List | Summary | How to use | Remarks |
|---- |---- |---- |---- |---- |---- |---- |
| OS  | WS2019 | environmental construction & parameter collection | [os2_ws2019_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os2_ws2019_list.yml) |This role provides functions to build the OS environment and change settings and collect OS settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/OS-Windows2019/blob/master/README.md) | |
| OS  | RHEL8  | environmental construction & parameter collection | [os2_rhel8_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os2_rhel8_list.yml)   |This role provides functions to build the OS environment and change settings and collect OS settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/OS-RHEL8/blob/master/README.md) | |
| OS  | WS2016 | environmental construction & parameter collection | [os2_ws2016_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os2_ws2016_list.yml) |This role provides functions to build the OS environment and change settings and collect OS settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/OS-Windows2016/blob/master/README.md) | |
| OS  | RHEL7  | environmental construction & parameter collection | [os2_rhel7_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os2_rhel7_list.yml)   |This role provides functions to build the OS environment and change settings and collect OS settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/OS-RHEL7/blob/master/README.md) | |
| Apache 2.4 | RHEL7 | application setup | [apache24_linux_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/apache24_linux_setup_list.yml) |Install and configure Apache 2.4 on RHEL. |[Readme](https://github.com/exastro-playbook-collection/Apache_install)| |
| Apache 2.4 | WS2016| application setup | [apache24_windows_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/apache24_windows_setup_list.yml) |Install and configure Apache 2.4 on WS2016. |[Readme](https://github.com/exastro-playbook-collection/Apache24_WIN_install)| |
| Apache 2.4 | WS2016, RHEL7 | parameter collection | [apache24_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/apache24_scan_list.yml) |Collect Apache 2.4 settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/Apache24_extracting_linux) | |
| IIS | WS2016 | application setup | [iis_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/iis_setup_list.yml) |Install and configure IIS on WS2016.|[Readme](https://github.com/exastro-playbook-collection/IIS_Install)| |
| IIS | WS2016 | parameter collection | [iis_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/iis_scan_list.yml) |Collect IIS settings and create a reusable parameter file on WS2016.|[Readme](https://github.com/exastro-playbook-collection/IIS_WS2016_extracting)| |
| SQL Server | WS2016 | application setup | [sql_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/sql_setup_list.yml) |Check and prepare an environment, and Install SQL Server.|[Readme](https://github.com/exastro-playbook-collection/SqlServer_preinstall)| |
| Zabbix Agent 4.0 | RHEL6,7 | application setup | [zabbix40_agent_linux_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/zabbix40_agent_linux_setup_list.yml) |Install and configure Zabbix Agent 4.0 on RHEL6 or 7.|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Agent_install)| |
| Zabbix Agent 4.0 | WS2012R2,2016 | application setup | [zabbix40_agent_windows_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/zabbix40_agent_windows_setup_list.yml) |Install and configure Zabbix Agent 4.0 on WS2012R2 or 2016)|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Agent_WIN_install)| |
| Zabbix Server 4.0 | RHEL7 | application setup | [zabbix40_server_linux_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/zabbix40_server_linux_setup_list.yml) |Install and configure Zabbix Server 4.0 on RHEL7|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Server_install)| |
| Zabbix Agent 4.0  Zabbix Server 4.0 | RHEL6,7  WS2012R2,2016 | parameter collection | [zabbix40_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/zabbix40_scan_list.yml) |Collect Zabbix Agent 4.0(RHEL6,7), (WS2012R2,2016) and Zabbix Server 4.0(RHEL7) settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/Zabbix40_Agent_extracting_linux)| |
| Nginx | RHEL7 | application setup | [nginx_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/nginx_setup_list.yml) |Install and configure Nginx on RHEL7|[Readme](https://github.com/exastro-playbook-collection/Nginx_Install)| |
| Nginx | RHEL7 |  parameter collection | [nginx_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/nginx_scan_list.yml) |Collect Nginx settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/Nginx_extracting)| |

## Support

For more details, refer to "How to use" of each role.  

## Usage

Shown an example of OS parameter collection below.  

### Pre-work

The following steps will be executed on Ansible server unless otherwise specified.  

1. Build Ansible server and login as a user with sudo privileges.  

2.  Install the required tools.  
    ```
    sudo yum -y install git wget
    ```

3. Create a working folder and change to the folder.  
    ```
    mkdir ansible_work
    cd ansible_work/
    ```

4. Download the [Role List for Parameter Generation Common Parts](https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml) and place it in the folder you created in step (3).  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml
    ```

5. Download a role with the ansible-galaxy Command.  
    ```
    ansible-galaxy install -r prerequire_list.yml -p roles
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
        ansible_python_interpreter=/usr/bin/python3
        ansible_become_pass=<sudo password>
        ```
        (*) You don't have to set the variable 'ansible_python_interpreter' if use ansible with python2.  

7. Run the playbook to install Parameter Generation Common Parts.
    ```
    ansible-playbook -c local -i inventory prerequire.yml
    ```

### Run Playbook

1. Download the roll list of the functions you want to use and place it in the folder where you want to create Playbook.  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/os2_ws2016_list.yml
    ```

2. Download a role with the ansible-galaxy Command.  
    ```
    ansible-galaxy install -p roles -r os2_ws2016_list.yml
    ```

3. Create a playbook and an inventory file referencing "How to use" of each role.  
    * Playbook(os_scan.yml)
        ```
        ---
        - hosts: <Target Group Name>
          roles:
            - OS-Windows2016/WIN_ALL/OS_gathering
                :
        ```
    * Inventory(inventory)
        ```
        [<Target Group Name>]
        xxx.xxx.xxx.xxx

        [<Target Group Name>:vars]
        ansible_user=<user with sudo privileges>
        ansible_password=<password for the above user account>
                :
        ```

4. Run the playbook to collect OS settings.  
    ```
    ansible-playbook -i inventory os_scan.yml
    ```
