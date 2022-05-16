# 制限事項

本パッケージは以下の制限事項があります  

* OS-RHEL8 Roleに実装された機能の内、以下機能の「設定値収集」「環境構築、設定値変更」には現時点では対応しておりません  
  * RH_group  
  * RH_rpm  
  * RH_systemctl  
  * RH_user  

* 「RHEL8_構築」Symphonyを実行した際にバリデーションエラーが発生し、以下のようなメッセージが表示されることがあります  
  ```
  Movementに作業対象ホストが登録されていません。（MovementID:xx）'''  
  ```
  これは、表示されたMovementIDに紐づくMovementのパラメータが未設定の場合に出力されるエラーです  
  Symphony実行時に「Skip」をチェックして当該Movementの実行をスキップするか、「構築_RHEL8_＜ロール名＞」メニューからパラメータを登録した後Symphonyを実行してください  
