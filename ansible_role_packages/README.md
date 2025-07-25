# Exastro Playbook Collection - Ansible Role Package

## Description

本サイトではAnsible Role Packageを公開しています  
Ansible Role PackageはAnsible Roleと依存パッケージ、Exastro IT Automationへの組込みに必要となる設定ファイル(ITA readme等)を含むZip形式の圧縮ファイルです  
公開パッケージ(zip)をダウンロードし、Exastro IT Automationへの組込みとメニュー／ジョブ等の構築、パラメータ設定などを行うことでロールの実行を行えます  

## Ansible Role Package

| 対象製品 | Version    | 機能                 | パッケージ(zip)                                              | 機能概要                                                     | How to use                                                     |  
| -------- | ---------- | -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |  
| OS       | WS2022     | 環境構築 ＆ 設定収集 | [OS-Windows2022](https://github.com/exastro-playbook-collection/OS-Windows2022/releases/download/ver.2.0.1/OS-Windows2022.zip) | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-Windows2022/blob/master/README.md)<br>[注意事項](attention/OS-WS2022.ja.md) |  
| OS       | RHEL9      | 環境構築 ＆ 設定収集 | [OS-RHEL9](https://github.com/exastro-playbook-collection/OS-RHEL9/releases/download/ver.2.0.1/OS-RHEL9.zip)                   | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-RHEL9/blob/master/README.md)<br>[注意事項](attention/OS-RHEL9.ja.md) |  
| Command       | WS2022     | 環境構築 ＆ 設定収集 | [OS-Windows2022](https://github.com/exastro-playbook-collection/Cmd-Executor-Windows2022/releases/download/ver.2.0.1/Cmd-Executor-Windows2022.zip) | 任意コマンドおよびファイルアップロードを行う | [Readme](https://github.com/exastro-playbook-collection/Cmd-Executor-Windows2022/blob/master/README.md)<br>[注意事項](attention/Cmd-Executor-WS2022.ja.md) |  
| Command       | RHEL9      | 環境構築 ＆ 設定収集 | [OS-RHEL9](https://github.com/exastro-playbook-collection/Cmd-Executor-RHEL9/releases/download/ver.2.0.1/Cmd-Executor-RHEL9.zip)                   | 任意コマンドおよびファイルアップロードを行う | [Readme](https://github.com/exastro-playbook-collection/Cmd-Executor-RHEL9/blob/master/README.md)<br>[注意事項](attention/Cmd-Executor-RHEL9.ja.md) |  

## Support

対象ホストの諸元等については「Ansible Role Package」一覧の「注意事項」を参照ください  

## Usage

ここではITAにWS2022の環境構築・設定収集用Ansible Role PackageをインポートしてRoleを実行する場合の例を示します  

### システム構成

以下の構成で作業を行います  
![system.png](../parts/system.ja.png)  

### 準備作業

本手順はITAで設定収集を行う場合に一度だけ実行する必要があります  
以降の手順は特に明記の無い限りITAホストサーバ上で実行します  

1. ITAホストサーバにITAのインストールを行います  
   * インストール手順は[「Exastro IT Automation を導入しよう」](https://ita-docs.exastro.org/2.2/ja/installation/index.html)を参照ください  

2. ITAにログインして、オーガナイゼーションおよびワークスペースを作成します

3. 必要なツールをインストールします  
    ```
    sudo yum -y install git wget
    ```

4. Playbook実行フォルダを作成し、フォルダ下に移動します  
    ```
    mkdir ansible_work
    cd ansible_work/
    ```

5. [共通部品のロールリスト](../requirements/prerequire_list.yml)をダウンロードし、手順(4)で作成したフォルダに配置します  
    ```
    wget https://exastro-suite.github.io/playbook-collection-docs/requirements/prerequire_list.yml
    ```

6. ITAフォルダにコピー
    ```
    cp ./parameter_generate.tar.gz /home/<ITAユーザ>/exastro-docker-compose/ita_by_ansible_execute/templates/work/
    cp ./ita_role_adapter.tar.gz /home/<ITAユーザ>/exastro-docker-compose/ita_by_ansible_execute/templates/work/
    
    cd /home/<ITAユーザ>/exastro-docker-compose/ita_by_ansible_execute/templates/work
    tar -zxvf parameter_generate.tar.gz
    tar -zxvf ita_role_adapter.tar.gz
    ```

7. 共通部品をインストール
　　/home/<ITAユーザ>/exastro-docker-compose/ita_by_ansible_execute/templates/work/Dockfileに下記の内容を追加します。
    ```
    USER root
    
    RUN mkdir -p /usr/share/ansible/plugins/action/
    
    COPY parameter_generate /home/parameter_generate
    WORKDIR /home/parameter_generate/
    RUN cp roles/setup_paragen/files/action_plugins/parameter_generate.py /usr/share/ansible/plugins/action/parameter_generate.py
    RUN ansible-playbook -c local -i inventory prerequire.yml
    
    COPY ita_role_adapter /home/ita_role_adapter
    WORKDIR /home/ita_role_adapter/
    RUN ansible-playbook -c local -i inventory prerequire.yml
    ```

### ロールの実行

以降の手順は特に明記の無い限り操作端末上で実行します  

1. 「Ansible Role Package」一覧から対象製品のパッケージ(zip)をダウンロードし、ローカル環境に格納します  

2. 「Ansible Role Package」一覧の「How to use」欄に「制限事項」「注意事項」のリンクがある場合は内容を確認し、必要に応じて対応を行ってください  

3. ITAに「Ansible Role Package」をインポートした後、ITAの仕様に沿ってロールの実行を行います  

* 作業手順については[ITAの利用手順マニュアル](https://ita-docs.exastro.org/2.2/ja/manuals/index.html)の以下を参照ください  
　「利用手順マニュアル Ansible ドライバ」  
　　　4. Ansible-LegacyRole
