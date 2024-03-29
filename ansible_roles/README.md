# Exastro Playbook Collection - Ansible Roles

## Description

本サイトではAnsibleによりOS/MWの環境構築、設定変更や設定情報収集を行うためのAnsible Roleを提供しています

## Ansible Role List

| 対象製品 | バージョン | 機能 | ロールリスト | 機能概要 | 利用方法 |
|---- |---- |---- |---- |---- |---- |
| OS  | WS2019 | 環境構築 ＆ 設定収集 | [os2_ws2019_list.yml](requirements/os2_ws2019_list.yml) |OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う|[Readme](https://github.com/exastro-playbook-collection/OS-Windows2019/blob/master/README.md) |
| OS  | RHEL8  | 環境構築 ＆ 設定収集 | [os2_rhel8_list.yml](requirements/os2_rhel8_list.yml)   |OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う|[Readme](https://github.com/exastro-playbook-collection/OS-RHEL8/blob/master/README.md) |
| OS  | WS2016 | 環境構築 ＆ 設定収集 | [os2_ws2016_list.yml](requirements/os2_ws2016_list.yml) |OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う|[Readme](https://github.com/exastro-playbook-collection/OS-Windows2016/blob/master/README.md) |
| OS  | RHEL7  | 環境構築 ＆ 設定収集 | [os2_rhel7_list.yml](requirements/os2_rhel7_list.yml)   |OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う|[Readme](https://github.com/exastro-playbook-collection/OS-RHEL7/blob/master/README.md) |
| Apache 2.4 | RHEL7 | 環境構築 | [apache24_linux_setup_list.yml](requirements/apache24_linux_setup_list.yml) |Apache 2.4のインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/Apache_install)|
| Apache 2.4 | WS2016| 環境構築 | [apache24_windows_setup_list.yml](requirements/apache24_windows_setup_list.yml) |Apache 2.4のインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/Apache24_WIN_install)|
| Apache 2.4 | WS2016<br>RHEL7 | 設定収集 | [apache24_scan_list.yml](requirements/apache24_scan_list.yml) |Apache 2.4の設定値を収集し、再利用可能なパラメータファイルを作成する|[Readme](https://github.com/exastro-playbook-collection/Apache24_extracting_linux) |
| IIS | WS2016 | 環境構築 | [iis_setup_list.yml](requirements/iis_setup_list.yml) |IIS(WS2016)のインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/IIS_Install)|
| IIS | WS2016 | 設定収集 | [iis_scan_list.yml](requirements/iis_scan_list.yml) |IIS(WS2016)の設定値を収集し、再利用可能なパラメータファイルを作成する|[Readme](https://github.com/exastro-playbook-collection/IIS_WS2016_extracting)|
| SQL Server | WS2016 | 環境構築 | [sql_setup_list.yml](requirements/sql_setup_list.yml) |SQL Serverのインストール前の環境チェック、準備、インストールを行う|[Readme](https://github.com/exastro-playbook-collection/SqlServer_preinstall)|
| Zabbix Agent 4.0 | RHEL6<br>RHEL7 | 環境構築 | [zabbix40_agent_linux_setup_list.yml](requirements/zabbix40_agent_linux_setup_list.yml) |Zabbix Agent 4.0(RHEL6,7)のインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Agent_install)|
| Zabbix Agent 4.0 | WS2012R2<br>WS2016 | 環境構築 | [zabbix40_agent_windows_setup_list.yml](requirements/zabbix40_agent_windows_setup_list.yml) |Zabbix Agent 4.0(WS2012R2,2016)のインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Agent_WIN_install)|
| Zabbix Server 4.0 | RHEL7 | 環境構築 | [zabbix40_server_linux_setup_list.yml](requirements/zabbix40_server_linux_setup_list.yml) |Zabbix Server 4.0(RHEL7)のインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/Zabbix40-Server_install)|
| Zabbix Agent 4.0  Zabbix Server 4.0 | RHEL6<br>RHEL7<br>WS2012R2<br>WS2016 | 設定収集 | [zabbix40_scan_list.yml](requirements/zabbix40_scan_list.yml) |Zabbix Agent 4.0(RHEL6,7),(WS2012R2,2016) と Zabbix Server 4.0(RHEL7)の設定値を収集し、再利用可能なパラメータファイルを作成する|[Readme](https://github.com/exastro-playbook-collection/Zabbix40_Agent_extracting_linux)|
| Nginx | RHEL7 | 環境構築 | [nginx_setup_list.yml](requirements/nginx_setup_list.yml) |Nginxのインストール、環境構築を行う|[Readme](https://github.com/exastro-playbook-collection/Nginx_Install)|
| Nginx | RHEL7 | 設定収集 | [nginx_scan_list.yml](requirements/nginx_scan_list.yml) |Nginxの設定値を収集し、再利用可能なパラメータファイルを作成する|[Readme](https://github.com/exastro-playbook-collection/Nginx_extracting)|

## Support

各ロールの利用方法を参照  

## Usage

ここではOSの設定収集を行う場合の例を示します  

### 準備作業

本手順は環境構築時に一度だけ実行する  
以降の手順は特に明記の無い限りAnsibleサーバー上で操作を行います  

1. Ansibleサーバーを構築し、sudo権限を付与したユーザでログインします  

2. 必要なツールをインストールします  
    ```
    sudo yum -y install git wget
    ```

3. Playbook実行フォルダを作成し、フォルダ下に移動します  
    ```
    mkdir ansible_work
    cd ansible_work/
    ```

4. [パラメータ生成共通部品のロールリスト](../requirements/prerequire_list.yml)をダウンロードし、手順(3)で作成したフォルダに配置します  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml
    ```

5. ansible-galaxyコマンドでロールをダウンロードします  
    ```
    ansible-galaxy install -r prerequire_list.yml -p roles
    ```

6. 以下を参考にPlaybookとインベントリを作成します  
    * Playbook(prerequire.yml)
        ```
        ---
        - hosts: local
          become: yes
          roles:
            - setup_paragen
        ```
    * インベントリ(inventory)
        ```
        [local]
        localhost

        [local:vars]
        ansible_python_interpreter=/usr/bin/python3
        ansible_become_pass=<sudoパスワード>
        ```
        (*) AnsibleをPython2で動作させる場合、ansible_python_interpreterの定義は不要

7. Playbookを実行してパラメータ生成用共通部品をインストールします  
    ```
    ansible-playbook -c local -i inventory prerequire.yml
    ```

### Playbook実行（Windows Server 2016 OS情報収集の例）

1. 利用したい機能のロールリストをダウンロードし、Playbookを作成するフォルダに配置します  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/os2_ws2016_list.yml
    ```

2. ansible-galaxyコマンドでロールをダウンロードします  
    ```
    ansible-galaxy install -p roles -r os2_ws2016_list.yml
    ```

3. 各ロールのreadmeを参考にPlaybookとインベントリを作成します  
    * Playbook(os_scan.yml)
        ```
        ---
        - hosts: <ターゲットグループ名>
          roles:
            - OS-Windows2016/WIN_ALL/OS_gathering
          　　　：
        ```
    * インベントリ(inventory)
        ```
        [<ターゲットグループ名>]
        xxx.xxx.xxx.xxx

        [<ターゲットグループ名>:vars]
        ansible_user=<sudo権限を持つユーザアカウント>
        ansible_password=<上記ユーザアカウントのパスワード>
        　　　：
        ```

4. Playbookを実行してOSの情報情報収集を行います  
    ```
    ansible-playbook -i inventory os_scan.yml
    ```
