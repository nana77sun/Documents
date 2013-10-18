
#### 参考： 
 [https://jp.globalsign.com/support/ssl/list.php?cat=csr]

----
#### 秘密鍵を生成

    # openssl genrsa -des3 -out ./ssl.yi-manage.jp.2013.key 2048

 - file name : ssl.yi-manage.jp.2013.key
 - pass phrase : mu6bXpiG

----
#### CSRを生成

    # openssl req -new -key ./ssl.yi-manage.jp.2013.key -out ./ssl.yi-manage.jp.2013.csr

----
#### CSRの内容を確認

    # openssl req -text -noout -in ./ssl.yi-manage.jp.2013.csr

----
#### 証明書の内容を確認

    # openssl x509 -text -noout -in /[FilePath]/[CertFile]
