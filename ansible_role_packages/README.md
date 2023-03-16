# Exastro Playbook Collection - Ansible Role Package

## Description

本サイトではAnsible Role Packageを公開しています  
Ansible Role PackageはAnsible Roleと依存パッケージ、Exastro IT Automationへの組込みに必要となる設定ファイル(ITA readme等)を含むZip形式の圧縮ファイルです  
公開パッケージ(zip)をダウンロードし、Exastro IT Automationへの組込みとメニュー／ジョブ等の構築、パラメータ設定などを行うことでロールの実行を行えます  

## Ansible Role Package

| 対象製品 | Version    | 機能                 | パッケージ(zip)                                              | 機能概要                                                     | How to use                                                     |  
| -------- | ---------- | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |  
| OS       | WS2019     | 環境構築 ＆ 設定収集 | [OS-Windows2019](https://github.com/exastro-playbook-collection/OS-Windows2019/releases/download/v21.04/OS-Windows2019.zip) | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-Windows2019/blob/master/README.md)<br>[注意事項](attention/OS-Windows2019.ja.md) |  
| OS       | WS2016     | 環境構築 ＆ 設定収集 | [OS-Windows2016](https://github.com/exastro-playbook-collection/OS-Windows2016/releases/download/v21.04/OS-Windows2016.zip) | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-Windows2016/blob/master/README.md)<br>[注意事項](attention/OS-Windows2016.ja.md) |  
| OS       | RHEL8      | 環境構築 ＆ 設定収集 | [OS-RHEL8](https://github.com/exastro-playbook-collection/OS-RHEL8/releases/download/v23.03/OS-RHEL8.zip)                   | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-RHEL8/blob/master/README.md)<br>[注意事項](attention/OS-RHEL8.ja.md) |  
| OS       | RHEL7      | 環境構築 ＆ 設定収集 | [OS-RHEL7](https://github.com/exastro-playbook-collection/OS-RHEL7/releases/download/v21.04/OS-RHEL7.zip)                   | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-RHEL7/blob/master/README.md)<br>[注意事項](attention/OS-RHEL7.ja.md) |  

## Support

対象ホストの諸元等については「Ansible Role Package」一覧の「How to use」／「Readme」を参照ください  

## Usage

ここではITAにWS2019の環境構築・設定収集用Ansible Role PackageをインポートしてRoleを実行する場合の例を示します  

### システム構成

以下の構成で作業を行います  
![system.png](../parts/system.ja.png)  

### 準備作業

本手順はITAで設定収集を行う場合に一度だけ実行する必要があります  
以降の手順は特に明記の無い限りITAホストサーバ上で実行します  

1. ITAホストサーバにITAのインストールを行います  
   * インストール手順は[「Exastro IT Automation を導入しよう」](https://exastro-suite.github.io/it-automation-docs/install_ja.html)を参照ください  

2. ITAホストサーバにsudo権限を付与したユーザでログインします  

3. 必要なツールをインストールします  
    ```
    sudo yum -y install git wget
    ```

4. Playbook実行フォルダを作成し、フォルダ下に移動します  
    ```
    mkdir ansible_work
    cd ansible_work/
    ```

5. [パラメータ生成共通部品のロールリスト](../requirements/prerequire_list.yml)をダウンロードし、手順(3)で作成したフォルダに配置します  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml
    ```

6. ansible-galaxyコマンドでロールをダウンロードします  
    ```
    ansible-galaxy install -r prerequire_list.yml -p roles
    ```

7. 以下を参考にPlaybookとインベントリを作成します  
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

8. Playbookを実行してパラメータ生成用共通部品をインストールします  
    ```
    ansible-playbook -c local -i inventory prerequire.yml
    ```

9. 以下のように"failed=0"で終了したことを確認します  
（failed以外の値は環境によって変わる可能性があります）
    ```
    PLAY RECAP *********************************************************************************
    localhost                  : ok=4    changed=3    unreachable=0    failed=0    skipped=0 ...
    ```

### ロールの実行

以降の手順は特に明記の無い限り操作端末上で実行します  

1. 「Ansible Role Package」一覧から対象製品のパッケージ(zip)をダウンロードし、ローカル環境に格納します  

2. 「Ansible Role Package」一覧の「How to use」欄に「制限事項」「注意事項」のリンクがある場合は内容を確認し、必要に応じて対応を行ってください  

3. ITAに「Ansible Role Package」をインポートした後、ITAの仕様に沿ってロールの実行を行います  

* 作業手順については[ITAの利用手順マニュアル](https://exastro-suite.github.io/it-automation-docs/documents_ja.html)の以下を参照ください  
　「利用手順マニュアル Ansible-driver」  
　　　4.1.2 Ansible-Legacy Role 作業フロー  
