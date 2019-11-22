# Ansible Playbook Collection
## Description

本サービスでは、Ansible Playbook のコード（Role）を公開しています。

## Role List

| 対象製品 | バージョン | 機能 | ロールリスト | 機能概要 | 利用方法 | 備考 |
|---- |---- |---- |---- |---- |---- |---- |
| OS  | WS2016, RHEL7 | 環境構築 | [os_setup_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os_setup_list.yml) |OSの環境構築、設定変更を行う|[Readme](https://github.com/exastro-playbook-collection/RHEL/blob/master/README.md) | |
| OS  | WS2016, RHEL7 | 設定収集 | [os_scan_list.yml](https://exastro-suite.github.io/playbook-collection-docs/requirements/os_scan_list.yml) |OSの設定値を収集し、再利用可能なパラメータファイルを作成する|[Readme](https://github.com/exastro-playbook-collection/OS_extracting/blob/master/README.md) | |

## Support

各ロールの利用方法を参照

## Usage (パラメータ生成共通部品のセットアップの例)

### 準備作業（本手順は環境構築時に一度だけ実行）

1. Ansibleサーバーを構築します

2. AnsibleサーバーにGit Clientをインストールします
    ```
    $ sudo yum -y install git
    ```

3. Ansibleサーバー上のPlaybookを作成するフォルダに移動します。
    ```
    $ mkdir ansible_work
    $ cd ansible_work/
    ```

4. [パラメータ生成共通部品のロールリスト](https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml)をダウンロードし、手順(3)で作成したフォルダに配置します

5. ansible-galaxyコマンドでロールをダウンロードします
    ```
    $ ansible-galaxy install -r prerequire_list.yml -p roles
    ```

6. 以下を参考にPlaybookとインベントリを作成します
    * prerequire.yml(Playbook)
        ```
        ---
        - hosts: ansible
          become: yes
          roles:
            - setup_paragen
        ```
    * inventory(インベントリ)
        ```
        [ansible]
        localhost

        [ansible:vars]
        ansible_user=<sudo権限を持つユーザアカウント>
        ansible_password=<上記ユーザアカウントのパスワード>
        ansible_become_pass=<上記ユーザアカウントのパスワード>
        ```

### Playbook実行(ここではOSの情報情報収集を行う場合の例を示す)

1. 利用したい機能のロールリストをダウンロードし、Playbookを作成するフォルダに配置します

2. ansible-galaxyコマンドでロールをダウンロードします
    ```
    $ ansible-galaxy install -r os_scan_list.yml
    ```

3. 各ロールのreadmeを参考にPlaybookとインベントリを作成します
    * os_scan.yml(Playbook)
        ```
        ---
        - hosts: <ターゲットグループ名>
          roles:
        　　　：
        ```
    * inventory(インベントリ)
        ```
        [<ターゲットグループ名>]
        xxx.xxx.xxx.xxx

        [<ターゲットグループ名>:vars]
        ansible_user=<sudo権限を持つユーザアカウント>
        ansible_password=<上記ユーザアカウントのパスワード>
        　　　：
        ```

9. Playbook実行
    ```
    $ ansible-playbook -i inventory os_scan.yml
    ```
