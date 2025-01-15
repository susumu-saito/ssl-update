# SSLサーバ証明書の更新
SSLサーバ証明書を更新する手順

1. 中間証明書（JPRS_OVCA_G4_PEM.cer）とサーバ証明書(server.cer)を下記に配置
```shell
$sudo mv JPRS_OVCA_G4_PEM.cer /root/home/ssl/
$sudo mv sundms.cer /root/home/ssl/
$cd /root/home/ssl/
$sudo chown apache:apache *
$sudo chmod 644 *
```

2. 再起動
```shell
systemctl restart httpd
```

3. 補足
````shell
SSLCertificateFile /root/home/ssl/server.cer
SSLCertificateKeyFile /root/home/ssl/servername.key.pem
SSLCertificateChainFile /root/home/ssl/JPRS_OVCA_G4_PEM.cer
````