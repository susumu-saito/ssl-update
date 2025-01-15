# Gitlab起動・停止
Gitlabの起動、停止方法
[起動方法]
```shell
$ sudo gitlab-ctl start
```
[停止方法]
```shell
$ sudo gitlab-ctl stop
```


# SSLサーバ証明書の更新
SSLサーバ証明書を更新する手順
Gitlabの場合、サーバ証明書に中間証明書の内容を記載する必要がある

1. 下記のように中間証明書（ここではJPRS_OVCA_G3_PEM.cer）をサーバ証明書(server.cer)に書き込む
````shell
$sudo vi server.cer
※server.cerの最後の行（-----END CERTIFICATE-----）に改行を1つ入力
$sudo cat JPRS_OVCA_G4_PEM.cer >> server.cer
````

2. 編集したサーバ証明書を下記に配置
```shell
/etc/gitlab/ssl/server.cer
```

3. 秘密鍵を変更した場合は下記に秘密鍵を配置
```shell
/etc/gitlab/ssl/servername.key.pem
```

4. つづいて下記のコマンドを実行してください。
```shell
sudo gitlab-ctl reconfigure
```

5. Gitlabを再起動
```shell
sudo gitlab-ctl restart
```

6. 補足:SSLサーバ証明書のパスの設定
GitLabのSSLサーバ証明書のパスの設定は下記のように設定ファイル(/etc/gitlab/gitlab.rb)に設定されている。
````shell
nginx['ssl_certificate'] = "/etc/gitlab/ssl/server.cer"　←サーバ証明書
nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/servername.key.pem" ←秘密鍵
```





