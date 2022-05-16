# 注意事項

* 「入力用」メニューグループの各メニューの入力項目についてマウスオーバーすることで入力できるパラメータの概要が表示される項目があります  
各項目の指定方法の詳細についてはRoleのReadmeなどを参照ください  

* Exastro IT Automation（以降、ITAと表記）で以下のロールを利用する場合、一部のパラメータ項目については[代入値管理]画面から複数の変数の値を直接json形式で入力する必要があります  
  * ロール ： WIN_NetAdapterAdvancedProperty/OS_build  
    * ITA readmeファイル名 ： ita_readme_OS-Windows2019%WIN_NetAdapterAdvancedProperty%OS_build.yml  
    * パラメータ項目名 ： VAR_WIN_NetAdapterAdvancedProperty  
    * json形式の具体値の例 ： {'vmxnet3 Ethernet Adapter':{'Enable adaptive rx ring sizing': Enabled,'IPv4 TSO Offload': Enabled}}  

