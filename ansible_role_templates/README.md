# Exastro Playbook Collection - Ansible Role Template

## Description

本サイトではAnsible Role Templateを公開しています  
Ansible Role TemplateはExastro IT AutomationにAnsible Role Packageの組込みやRole実行に必要なメニュー／ジョブ等の構築などを行った上でエクスポートしたイメージファイルです  
公開パッケージ(kym)をダウンロードし、Exastro IT Automationへのインポートと初期設定を行うことでロールの実行を行えます  


## Ansible Role Template

**制限事項については「How to use」欄の「制限事項」を参照ください**  

| 対象製品 | Version    | ITA Version | パッケージ(kym)                                              | 機能概要                                                                                              | How to use                                                     |  
| -------- | ---------- | ----------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |  
| OS       | RHEL8      | Ver. 1.9.1  | [OS-RHEL8](https://github.com/exastro-playbook-collection/OS-RHEL8/releases/download/v21.04/ansible-role-template-os-rhel8-ce-exastro-1.9.1.kym)                     | OSの環境構築、設定変更、およびOS設定値収集、<br>再利用可能なパラメータファイルの生成を行う | [Role Readme](https://github.com/exastro-playbook-collection/OS-RHEL8/blob/master/README.md)<br>[注意事項](attention/ansible-role-template-os-rhel8-ce-exastro-1.9.1.ja.md)<br>[制限事項](limitation/ansible-role-template-os-rhel8-ce-exastro-1.9.1.ja.md) |  


## Support

Ansible Role 対象ホストの諸元等については「Ansible Role Template」一覧の「How to use」／「Role Readme」を参照ください  


## Usage

ここではITAにRHEL8の環境構築用Ansible Role TemplateをインポートしてRoleを実行する場合の例を示します  


### システム構成

以下の構成で作業を行います  
![system.png](../parts/system.ja.png)  


### ITAサーバーの環境構築を行う

本手順はITAサーバで一度だけ実行する必要があります  
以降の手順は特に明記の無い限りITAホストサーバ上で実行します  

1. ITAホストサーバにITAのインストールを行います  
   * インストール手順については[「Exastro IT Automation を導入しよう」](https://exastro-suite.github.io/it-automation-docs/install_ja.html)を参照ください  
   * インストールするITAのバージョンは、「Ansible Role Template」一覧の「ITA Version」を参照ください  

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


### Ansible Role Templateを利用する

以降の手順は特に明記の無い限り操作端末上で実行します  


【ITAホストサーバーの初期設定を行う】  

以降の手順は特に明記の無い限り操作端末上で実行します  

1. 「Ansible Role Template」一覧から対象製品のパッケージ(kym)をダウンロードし、操作端末の適当なフォルダに格納します  
    - 「How to use」欄に「制限事項」「注意事項」のリンクがある場合は内容を確認し、必要に応じて対応を行ってください  

2. ブラウザでITAホストサーバーに接続し、"administrator"（システム管理者）でログインします  

3. 「メインメニュー」＞「エクスポート／インポート」＞「メニューインポート」メニューを開きます  
「ファイルを選択」からダウンロードしたパッケージ(kym)を選択し、「アップロード」ボタンを押します  
「インポート」の「すべてのメニュー」が選択されていることを確認し、画面下部の「インポート」を押してインポートを開始します  

4. 「メインメニュー」＞「エクスポート／インポート」＞「メニューエクスポート・インポート管理」メニューを開きます  
「フィルタ」ボタンを押して画面更新し、実行中のインポート処理のステータスが「完了」になるのを待ちます  

5. 「メインメニュー」＞「基本コンソール」＞「機器一覧」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済ホスト情報をターゲットサーバーの設定にあわせて更新します  
    - 登録済ホスト情報のホスト名、IPアドレス、ログインユーザID、パスワード等にはサンプル値が入力されています  

6. 「メインメニュー」＞「基本コンソール」＞「オペレーション一覧」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済オペレーションを必要に応じて更新します  
    - 実施予定日時にはここでは任意の日時を指定して問題ありません  


【ターゲットサーバーの設定値収集を行う】  

1. 「メインメニュー」＞「Ansible共通」＞「収集インターフェース情報」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済のホスト情報をITAホストサーバ（自身）に接続可能となるよう更新します  

2. 「メインメニュー」＞「入力用」＞「収集_RHEL8_＜利用するロール名＞」メニューを開きます
「フィルタ」ボタンを押し、必要に応じてパラメータを更新します  

3. 「メインメニュー」＞「Symphony」＞「Symphony作業実行」メニューを開きます  
「RHEL8_収集」Symphonyと前述の手順で更新したオペレーションを選択します  

4. 「Symphony」に表示されているロールの内、利用しないロールは「Skip」をチェックします  
    - Symphonyに含まれる全てのロールを実行する場合、本手順は不要です  

5. 画面下部の「実行」ボタンを押してSymphonyを実行します  
全てのロールが「SKIP」もしくは「Done」になれば実行は完了です  
    - 作業状況、結果の詳細については、対象のロールを選択して「Operation Status」の「作業状態確認」から確認できます  

6. 「メインメニュー」＞「入力用」＞「構築_RHEL8_＜利用するロール名＞」メニューを開きます  
「フィルタ」ボタンを押して表示されるパラメータから収集内容を確認します  


【ターゲットサーバーの環境構築、設定変更を行う】  

以降の手順は特に明記の無い限り操作端末上で実行します  

1. 「メインメニュー」＞「入力用」＞「構築_RHEL8_＜利用するロール名＞」メニューを開きます  
必要に応じて「フィルタ」ボタンを押して表示されるパラメータを更新します  

2. 「メインメニュー」＞「Symphony」＞「Symphony作業実行」メニューを開きます  
「RHEL8_構築」Symphonyと前述の手順で更新したオペレーションを選択します  

3. 「Symphony実行」に表示されているロールの内、利用しないロールは「Skip」をチェックします  
    - Symphonyに含まれる全てのロールを実行する場合、本手順は不要です  

4. 画面下部の「実行」ボタンを押してSymphonyを実行します  
全てのロールが「SKIP」もしくは「Done」になれば実行は完了です  
    - 作業状況、結果の詳細については、対象のロールを選択して「Operation Status」の「作業状態確認」から確認できます  


### 備考

* 複数の設定を配列として指定する変数の指定可能最大数を拡張する場合、以下の手順で変更します  
    1. 「メニュー作成」＞「メニュー定義・管理」から対応するメニューのRepeat数を必要な値に変更します  
    2. 「Ansible-LegacyRole」＞「変数ネスト管理」で対象変数の「最大繰り返し数」を必要な値に変更します  
    3. 「Ansible-LegacyRole」＞「代入値自動登録設定」でメニューと変数の紐付けを行います  
    4. （設定値収集機能を持つパッケージの場合のみ）「Ansible共通」＞「収集項目値管理」で収集データとメニューの紐付けを行います  

* 各作業手順の詳細については[ITAの利用手順マニュアル](https://exastro-suite.github.io/it-automation-docs/documents_ja.html)の以下を参照ください  
　「利用手順マニュアル Ansible-driver」  

