# Exastro Playbook Collection - Ansible Role Template

## Description

本サイトではAnsible Role Templateを公開しています  
Ansible Role TemplateはExastro IT AutomationにAnsible Role Packageの組込みやRole実行に必要なメニュー／ジョブ等の構築などを行った上でエクスポートしたイメージファイルです  
公開パッケージ(kym)をダウンロードし、Exastro IT Automationへのインポートと初期設定を行うことでロールの実行を行えます  

## Ansible Role Template

**現時点では限定的に機能を実装したTrial Versionのみの配布となります**  
**制限事項については「How to use」欄の「制限事項」を参照ください**  

| 対象製品 | Version    | 機能     | ITA Version | パッケージ(kym)                                              | 機能概要                                                                                              | How to use                                                     |  
| -------- | ---------- | -------- | ----------- | ------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |  
| OS       | WS2019     | 環境構築 | Ver. 1.9.0  | [OS-Windows2019](https://github.com/exastro-playbook-collection/OS-Windows2019/releases/download/v21.04/ansible-template-os-windows2019-ce-trial2-exastro-1.9.0.kym) | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-Windows2019/blob/master/README.md)<br>[注意事項](attention/OS-Windows2019_1.9.0_Trial2.ja.md)<br>[制限事項](limitation/OS-Windows2019_1.9.0_Trial2.ja.md) |  
| OS       | RHEL8      | 環境構築 | Ver. 1.9.0  | [OS-RHEL8](https://github.com/exastro-playbook-collection/OS-RHEL8/releases/download/v21.04/ansible-template-os-rhel8-ce-trial2-exastro-1.9.0.kym)                   | OSの環境構築、設定変更、およびOS設定値収集、再利用可能なパラメータファイルの生成を行う | [Readme](https://github.com/exastro-playbook-collection/OS-RHEL8/blob/master/README.md)<br>[注意事項](attention/OS-RHEL8_1.9.0_Trial2.ja.md)<br>[制限事項](limitation/OS-RHEL8_1.9.0_Trial2.ja.md) |  

## Support

対象ホストの諸元等については「Ansible Role Template」一覧の「How to use」／「Readme」を参照ください  


## Usage

ここではITAにWS2019の環境構築用Ansible Role Template Trial VersionをインポートしてRoleを実行する場合の例を示します  


### システム構成

以下の構成で作業を行います  
![system.png](../parts/system.ja.png)  


### ITAサーバーの環境構築を行う

本手順はITAで設定収集を行う場合に一度だけ実行する必要があります  
以降の手順は特に明記の無い限りITAホストサーバ上で実行します  

1. ITAホストサーバにITAのインストールを行います  
   * インストール手順は[「Exastro IT Automation を導入しよう」](https://exastro-suite.github.io/it-automation-docs/install_ja.html)を参照ください  
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


### ITAホストサーバーの初期設定を行う

以降の手順は特に明記の無い限り操作端末上で実行します  

1. 「Ansible Role Template」一覧から対象製品のパッケージ(kym)をダウンロードし、操作端末の適当なフォルダに格納します  
    - 「How to use」欄に「制限事項」「注意事項」のリンクがある場合は内容を確認し、必要に応じて対応を行ってください  

2. ITAに"administrator"でログインし、パスワードを変更します  
    - この後の手順で変更したパスワードとは異なるパスワードへの変更を求められるため、ここでは使用予定のパスワードとは別の適当な値に変更してください  

3. 「メインメニュー」＞「エクスポート／インポート」＞「メニューインポート」メニューを開きます  
「ファイルを選択」からダウンロードしたパッケージ(kym)を選択し、「アップロード」ボタンを押します  
「インポート」の「すべてのメニュー」が選択されていることを確認し、画面下部の「インポート」を押してインポートを開始します  

4. 「メインメニュー」＞「エクスポート／インポート」＞「メニューエクスポート・インポート管理」メニューを開きます  
「フィルタ」ボタンを押して画面更新し、実行中のインポート処理のステータスが「完了」になるのを待ちます  
    - インポートによってパスワードは初期化され、初期パスワード"password"に戻ります  
    - パスワード変更画面が表示された場合、旧パスワード"password"からパスワード変更します  

5. ログアウトした後に"administrator"で再ログインします  
    - インポート中にパスワード変更していない場合、パスワードは初期パスワード"password"になります  
    - パスワード変更画面が表示された場合、旧パスワード"password"からパスワード変更します  

6. インポート中にパスワード変更していない場合、画面右上の「パスワード変更」ボタンを押してパスワードを変更します  

7. 「メインメニュー」＞「基本コンソール」＞「機器一覧」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済ホストを更新するか「登録」から新規ホストを登録します  
    - 登録済データのホスト名、IPアドレス、ログインユーザID、パスワード等にはサンプル値が入力されています  

8. 「メインメニュー」＞「基本コンソール」＞「オペレーション一覧」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済オペレーションを更新するか「登録」から新規オペレーションを登録します  
    - 実施予定日時はここでは任意の日時を指定して問題ありません  


### ターゲットサーバーの設定値収集を行う

以降の手順は特に明記の無い限り操作端末上で実行します  
「設定値収集」機能を持たないパッケージをご利用の場合は本章はスキップします  

1. 「メインメニュー」＞「Ansible共通」＞「収集インターフェース情報」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済のホスト情報を更新し、ITAホストサーバに接続するための情報を設定します  
    - 通常はRESTパスワードに初期設定で変更したパスワードを入力する以外の操作は必要ありません  

2. 「メインメニュー」＞「入力用」＞「＜利用するロール名＞_収集」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済パラメータを更新するか「登録」から新規パラメータを登録します  
    - ホスト、オペレーションには、本手順で更新、新規登録したものを選択します  

3. 「メインメニュー」＞「Conductor」＞「Conductor作業実行」メニューを開きます  
実行するConductorと、本手順で更新、新規登録したオペレーションを選択します  

4. 「Conductor実行」に表示されているロールの内、利用しないロールを選択して「Skip」をチェックします  
    - Conductorに含まれる全てのロールを実行する場合、本手順は不要です  

5. 画面下部の「実行」ボタンを押してConductorを実行します  
全てのロールが「SKIP」もしくは「Done」になれば実行は完了です  
    - 作業状況、結果の詳細については、対象のロールを選択して「Operation Status」の「作業状態確認」から確認できます  

6. 「メインメニュー」＞「入力用」＞「＜利用するロール名＞_構築」メニューを開きます  
「フィルタ」ボタンを押して表示されるパラメータから収集内容を確認します  


### ターゲットサーバーの環境構築、設定変更を行う

以降の手順は特に明記の無い限り操作端末上で実行します  

1. 「メインメニュー」＞「入力用」＞「＜利用するロール名＞_構築」メニューを開きます  
「フィルタ」ボタンを押して表示される登録済パラメータを更新するか「登録」から新規パラメータを登録します  
    - ホスト、オペレーションには、本手順で更新、新規登録したものを選択します  

2. 「メインメニュー」＞「Conductor」＞「Conductor作業実行」メニューを開きます  
実行するConductorと、本手順で更新、新規登録したオペレーションを選択します  

3. 「Conductor実行」に表示されているロールの内、利用しないロールを選択して「Skip」をチェックします  
    - Conductorに含まれる全てのロールを実行する場合、本手順は不要です  

4. 画面下部の「実行」ボタンを押してConductorを実行します  
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

