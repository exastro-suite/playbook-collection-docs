# Ansible Playbook Collection

English | [日本語](README.ja.md)

## Description

This service publishes Ansible Playbook code (Role).  

## Role List

| Target Product | Version | Functionality | Role List | Summary | How to use | Remarks |
|---- |---- |---- |---- |---- |---- |---- |
| OS  | WS2016, RHEL7 | environmental construction | [os_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os_setup_list.yml) |This role provides functions to build the OS environment and change settings.|[Readme](https://github.com/exastro-playbook-collection/RHEL) | |
| OS  | WS2016, RHEL7 | setting value collection | [os_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os_scan_list.yml) |This role provides the ability to collect OS settings and create a reusable parameter file.|[Readme](https://github.com/exastro-playbook-collection/OS_extracting) | |

## Support

See "How to use" for each role.  

## Usage

An example of OS configuration collection is shown below.  

### Pre-work

Perform this procedure only once when building the environment.  
The following steps will be performed on the Ansible server unless otherwise specified.

1. Build the Ansible server and log in as a user with sudo privileges.  

2. Install git.  
    ```
    $ sudo yum -y install git
    ```

3. Create a Playbook executable folder and move it under the folder.  
    ```
    $ mkdir ansible_work
    $ cd ansible_work/
    ```

4. Download the [Role List for Parameter Generation Common Parts](https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml) and place it in the folder you created in step (3).  

5. Download a Role with the ansible-galaxy Command.  
    ```
    $ ansible-galaxy install -r prerequire_list.yml -p roles
    ```

6. Make Playbook and Inventory referring to the following.  
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

7. Run Playbook to install common parts for parameter generation.  
    ```
    $ ansible-playbook -c local -i inventory prerequire.yml
    ```

### Run Playbook

1. Download the roll list of the functions you want to use and place it in the folder where you want to create Playbook.  

2. Download a Role with the ansible-galaxy Command.  
    ```
    $ ansible-galaxy install -r os_scan_list.yml -p roles
    ```

3. Create Playbook and inventory with reference to "How to use" for each role.  
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

4. Run Playbook to collect information about the OS.  
    ```
    $ ansible-playbook -i inventory os_scan.yml
    ```
