# 注意事項

1. パラメータシートには、ファイルアップロード型のパラメータを含む場合、下記２点制限があります。
   - 拡張子が「'.exe', '.com', '.php', '.cgi', '.sh', '.sql', '.vbs', '.js', '.pl', '.ini', '.htaccess'」のいずれかであるファイルをアップロードする場合、拡張子を付けてアップロードができません。この拡張子のファイルをアップロードする場合、fileパラメータに拡張?(.exe等)を削除することで制限を回避できます。
   - ファイルアップロード型の最大ファイルサイズはジョブ毎に異なります。
   
     | ジョブ                            | 最大ファイルサイズ |
     | --------------------------------- | ------------------ |
     | コマンド実行&ファイルアップロード | 100MB              |
     | ファイルアップロード              | 100MB              |
     | 上記以外                          | 1MB                |