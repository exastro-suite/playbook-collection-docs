# 制限事項

本パッケージはTrial Versionのため、以下の制限事項があります  

* 以下機能の「環境構築、設定値変更」にのみ対応しています  
  * RH_chrony  
  * RH_default_target  
  * RH_directory  
  * RH_grub2  
  * RH_systemd  
  * RH_cron  
  * RH_cronconf  
  * RH_file_access  
  * RH_firewalld  
  * RH_fstab  
  * RH_group  
  * RH_hosts  
  * RH_hosts_allow_deny  
  * RH_init  
  * RH_initfunc  

* インポート時にシステム管理者のアカウント情報が上書きされます  
既存のExastro IT Automation環境には適用せず、必ず新規に作成した県境をご利用ください  

* 「入力用」メニューグループの各メニューに登録されているパラメーターはサンプルデータのため、実環境への適用は行わないでください  

* オペレーション一覧に登録済のオペレーションはサンプルデータに紐づいているためロール実行が失敗する可能性があります
試行の際はオペレーションを新規登録してご利用ください  

* 以下変数の入力可能サイズは最大8192bytesとなります  
それ以上のデータを設定することはできませんのでご注意ください  
  * RH_chrony / VAR_RH_chrony / text  
  * RH_cron / VAR_RH_cron / text  
  * RH_cronconf / VAR_RH_cronconf / text  
  * RH_firewalld / VAR_RH_firewalld / text  
  * RH_fstab / VAR_RH_fstab / text  
  * RH_hosts / VAR_RH_hosts / text  
  * RH_hosts_allow_deny / VAR_RH_hosts_allow_deny / text  
  * RH_initfunc / VAR_RH_initfunc / text  
  * RH_init / VAR_RH_init / text  

* 配列として複数設定可能な変数の指定可能最大数を拡張する場合、以下手順で行ってください  
但し「Repeat数」は99以下且つ「Repeat数」×「Repeatに含まれる変数の数」が200以下という宣言がありますのでご注意ください  
（「代入順序」という入力項目が存在するものが本件に該当します）  
  1. 「メニュー作成」＞「メニュー定義・管理」から対応するメニューのRepeat数を必要な値に変更します  
  2. 「Ansible-LegacyRole」＞「変数ネスト管理」で対象変数の「最大繰り返し数」を必要な値に変更します  
  3. 「Ansible-LegacyRole」＞「代入値自動登録設定」でメニューと変数の紐付けを行います  

