# Exastro Playbook Collection - Ansible Roles

## Description

本サイトではAnsibleによりOS/MWの環境構築、設定変更や設定情報収集を行うためのAnsible Roleを提供しています

## Ansible Role List

| 対象製品 | バージョン | 機能 | ロールリスト | 機能概要 | 利用方法 |
|---- |---- |---- |---- |---- |---- |
| OS  | WS2022 | 環境構築 ＆ 設定収集 | [os2_ws2022_list.yml](requirements/os2_ws2022_list.yml) |OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う|[Readme](https://github.com/exastro-playbook-collection/OS-Windows2022/blob/master/README.md) |
| OS  | RHEL9  | 環境構築 ＆ 設定収集 | [os2_rhel9_list.yml](requirements/os2_rhel9_list.yml)   |OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う|[Readme](https://github.com/exastro-playbook-collection/OS-RHEL9/blob/master/README.md) |
| Command  | WS2022  | 環境構築 | [cmd2_ws2022_list.yml](requirements/cmd2_ws2022_list.yml)   |任意コマンドおよびファイルアップロードを行う|[Readme](https://github.com/exastro-playbook-collection/Cmd-Executor-Windows2022/blob/master/README.md) |
| Command  | RHEL9  | 環境構築 | [cmd2_rhel9_list.yml](requirements/cmd2_rhel9_list.yml)   |任意コマンドおよびファイルアップロードを行う|[Readme](https://github.com/exastro-playbook-collection/Cmd-Executor-RHEL9/blob/master/README.md) |

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

4. [共通部品のロールリスト](../requirements/prerequire_list.yml)をダウンロードし、手順(3)で作成したフォルダに配置します  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml
    ```

5. ansible-galaxyコマンドでロールをダウンロードします  
    ```
    ansible-galaxy install -r prerequire_list.yml -p roles
    ```

7. Playbookを実行してパラメータ生成用共通部品(parameter_generate)をインストールします  
    ```
    cd parameter_generate
    ansible-playbook -c local -i inventory prerequire.yml
    ```

9. Playbookを実行して収集結果変換用共通部品(ita_role_adapter)をインストールします  
    ```
    cd ita_role_adapter
    ansible-playbook -c local -i inventory prerequire.yml
    ```

### Playbook実行（Windows Server 2022 OS情報収集の例）

1. 利用したい機能のロールリストをダウンロードし、Playbookを作成するフォルダに配置します  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/ansible_roles/requirements/os2_ws2022_list.yml
    ```

2. ansible-galaxyコマンドでロールをダウンロードします  
    ```
    ansible-galaxy install -p roles -r os2_ws2022_list.yml
    ```

3. 各ロールのreadmeを参考にPlaybookとインベントリを作成します  
    * Playbook(os_scan.yml)
        ```
        ---
        - hosts: <ターゲットグループ名>
          roles:
            - OS-Windows2022-ITA/WIN_AutoMount_ITA/OS_gathering
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
