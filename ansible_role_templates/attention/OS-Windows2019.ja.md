# 注意事項

* 入力用メニューの一部項目ではマウスオーバーすることで入力できるパラメータの概要が表示される項目があります  
各項目の指定方法の詳細についてはRoleのReadmeなどを参照ください  

* 複数の設定を配列として指定する変数の指定可能最大数を５に設定しています
（例：ユーザアカウント機能では最大５ユーザまで作成可能）  
指定できる最大数を拡張する場合、以下の手順で変更してください  
  1. 「メニュー作成」＞「メニュー定義・管理」から対応するメニューのRepeat数を必要な値に変更します
  2. 「Ansible-LegacyRole」＞「変数ネスト管理」で対象変数の「最大繰り返し数」を必要な値に変更します
  3. 「Ansible-LegacyRole」＞「代入値自動登録設定」でメニューと変数の紐付けを行います

* Exastro IT Automation（以降、ITAと表記）で以下のロールを利用する場合、一部のパラメータ項目については[代入値管理]画面から複数の変数の値を直接json形式で入力する必要があります。
  * ロール ： WIN_NetAdapterAdvancedProperty/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-Windows2019%WIN_NetAdapterAdvancedProperty%OS_build.yml  
    * パラメータ項目名 ： VAR_WIN_NetAdapterAdvancedProperty  
    * json形式の具体値の例 ： {'vmxnet3 Ethernet Adapter':{'Enable adaptive rx ring sizing': Enabled,'IPv4 TSO Offload': Enabled}}  
