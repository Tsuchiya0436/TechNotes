# ネットワークの基本とTCP/IPの仕組み

## TCP/IPとは
TCP/IP(Transmission Control Protocol / Internet Protocol)は、世界的に広く利用されているインターネットプロトコルであり、通信プロトコルの総称。  
このプロトコルは、インターネットやその他のネットワーク上でデータの送受信を管理し、異なるコンピュータやネットワーク機器間での情報交換を可能にする。  

## プロトコルとは
コンピュータ同士がネットワークを通じて通信するために決められた「ルールや手順」のこと。同じプロトコルを使用することで、異なるコンピュータ同士でも通信が可能になるが、異なるプロトコルを使用するコンピュータ同士では通信ができない。  
例えば、言語のプロトコルがあるとすると、日本語(プロトコル)を使用する人とイタリア語(プロトコル)を使用する人では、言語(プロトコル)が異なるため会話内容を理解することができないが、同じ言語(プロトコル)を使用している人同士であれば意思疎通が可能となる。  
コンピュータの場合、人間のように応用力や知能を使って柔軟に対応することができない。そのため、通信を行うには、全ての細かな部分において**明確なルール**が必要となる。  
このような**ルールの集合体がプロトコル**と呼ばれる。  

## 階層モデルとは
通信を改装に分けることで、各層が独立して特定の役割を持てる。例えば1つの層ではデータを物理的に転送し、別の層では送受信されるデータの内容を扱う、といったように役割が明確に分かれている。  
代表的な階層モデルにはTCP/IPモデルとOSI参照モデルがある。
<table border="1">
  <thead>
    <tr>
      <th colspan="2">OSI参照モデル</th>
      <th>TCP/IP</th>
      <th>主なプロトコル、規格</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>第7層</td>
      <td>アプリケーション層</td>
      <td rowspan="3">アプリケーション層</td>
      <td rowspan="3">DNS, HTTP, TLS/SSL, SMTP, POP, IMAP, SSH, FTP, SFTP等</td>
    </tr>
    <tr>
      <td>第6層</td>
      <td>プレゼンテーション層</td>
    </tr>
    <tr>
      <td>第5層</td>
      <td>セッション層</td>
    </tr>
    <tr>
      <td>第4層</td>
      <td>トランスポート層</td>
      <td>トランスポート層</td>
      <td>TCP, UDP等</td>
    </tr>
    <tr>
      <td>第3層</td>
      <td>ネットワーク層</td>
      <td>インターネット層</td>
      <td>IP, ICMP(ping)等, (ARP)</td>
    </tr>
    <tr>
      <td>第2層</td>
      <td>データリンク層</td>
      <td rowspan="2">リンク層 (ネットワークインターフェース層)</td>
      <td rowspan="2">(ARP), PPP, Wi-Fi(IEEE 802.11), Ethenet(IEEE 802.3), MAC等</td>
    </tr>
    <tr>
      <td>第1層</td>
      <td>物理層</td>
    </tr>
  </tbody>
</table>
※　主なプロトコル、規格の詳細については各層の説明にて記載

### 1. アプリケーション層
#### 役割
- ユーザーインターフェースの提供：  
    アプリケーション層は、ユーザーとネットワークをつなぐ役割を持っている。つまり、ユーザーがインターネットや他のネットワークリソースを利用できるようにする層。この層は、ウェブブラウザ、メールクライアント、ファイル転送アプリケーションなど、エンドユーザーが直接触れる部分。

- プロトコルの選定と動作：  
    アプリケーション層では、目的に応じたプロトコル(HTTP, SMTP, DNSなど)を選び、そのプロトコルに従って通信を行う。例えば、webページのリクエストはHTTPが、メールの送信にはSMTPが使われる。  

- データのフォーマットと処理：  
    データはアプリケーション層で処理され、特定のフォーマット(HTML, JSON, XMLなど)に変換される。webページを表示する際にはHTMLデータが処理され、表示される。

#### 主なプロトコル、規格
- **DNS(Domain Name System)：**  
    DNSは、インターネット上で使われるドメイン名とIPアドレスを対応付けるシステム。  
    例えば、「www.example.com」と入力すると、DNSがそれをIPアドレス(192.168.1.1など)に変換する。  
    これにより、ユーザーはIPアドレスではなくドメイン名を使ってWebサイトにアクセスできる.  

- **HTTP(HyperText Transfer Protocol)：**  
    HTTPは、WebサーバーとWebブラウザ(クライアント)間でデータをやり取りするためのプロトコル。  
    Webページを表示するために、ブラウザがHTTPリクエストをサーバーに送信し、サーバーがHTMLなどのデータを返すという仕組み。  
    ポート番号は80番を使用する。  

- **TLS/SSL(Transport Layer Security / Secure Sockets Layer)：**  
    HTTP通信を安全に行うためのプロトコルで、データの暗号化を行う。  
    SSLは古いバージョンで、TLSが新しいバージョンHTTPと組み合わせて使われる場合はHTTPSとなり、Webページが暗号化されることで、  
    外部からのデータ盗聴や改竄を防ぐことができる。  
    ポート番号は443番を使用する。

- **HTTPS(HyperText Transfer Protocol Secure)：**
    HTTPSは、HTTPにTLS/SSLによる暗号化を追加したプロトコルで、通信が暗号化され、盗聴や改竄のリスクが減少する。  
    HTTPSは、銀行やショッピングサイトなど、機密データのやり取りを行うWebサイトで使われる。  
    ポート番号はTLS/SSLと同じく443番を使用する。

- **SMTP(Simple Mail Transfer Protocol)：**  
    SMTPは、メールを送信するためのプロトコル。クライアントからメールサーバーへ、またはサーバー間でメールを転送する役割を持つ。  
    基本的に送信専用なので、受信にはPOPやIMAPなど別のプロトコルが使われる。  
    ポート番号は25番（暗号化なし）、または587番（暗号化あり）を使用する。
    
- **POP(Post Office Protocol)：**  
    POPは、メールをサーバーからローカルデバイスにダウンロードするためのプロトコル。  
    一度ダウンロードすると、そのメールはサーバーから削除されるのが特徴。(POP3が一般的)。  
    ポート番号は110番、または995番(暗号化)を使用する。

- **IMAP(Internet Message Access Protocol)：**  
    IMAPは、メールをサーバー上に残しつつ、複数のデバイスからアクセスできるプロトコル。  
    POPとは異なり、メールはサーバーに保存され続けるため、スマートフォンやPCなど複数のデバイスで同期した状態でメールを確認できる。  
    ポート番号は143番、または993番(暗号化)を使用する。

- **SSH(Secure Shell)：**  
    SSHは、リモートコンピュータに安全に接続して操作するためのプロトコル。  
    セキュリティが強化されている、データの暗号化や認証機能を持つため、サーバー管理やプログラミングの際に使われる。  
    Telnetと異なり、データが暗号化されているため安全。  
    ポート番号は22番を使用する。

- **FTP(File Transfer Protocol)：**  
    FTPは、ファイルをサーバーとクライアント間で転送するためのプロトコルだが、データが暗号化されないため、セキュリティ上のリスクがある。  
    ポート番号は20番と21番を使用する。

- **SFTP(SSH File Transfer Protool)：**  
    SFTPは、SSHを利用して安全にファイルを転送するプロトコル。  
    FTPに比べてデータが暗号化されているため、より安全にファイルをやり取りできる。  
    ポート番号はSSHと同じく22番を使用する。

#### 具体的なプロセス例
- **HTTPSリクエスト**  
    HTTPSで暗号化されたリクエストとレスポンスの動きを確認する。  
    `https:google.com`に`curl`コマンドを使ってリクエストを送信し、サーバーとの安全な通信の流れを見てみる。  

    #### 1. リクエストの送信
    ```bash
        curl -v https://google.com
    ```

    接続の確立
    ```bash
        * Host google.com:443 was resolved.
        * IPv6: 2404:6800:4004:80a::200e
        * IPv4: 142.250.199.110
        *   Trying 142.250.199.110:443...
        * Connected to google.com (142.250.199.110) port 443
    ```
    - DNS解決：  
        `google.com`がIPv4(142.250.199.110)とIPv6(2404:6800:4004:80a::200e)に解決され、IPv4アドレスへの接続が試みられている。
    
    - 接続確立：
        ポート 443(HTTPSの標準ポート)で、`google.com`に正常に接続された。
    ---

    #### 2. TLSハンドシェイク  
    ```bash
        * TLSv1.3 (OUT), TLS handshake, Client hello (1):
        * TLSv1.3 (IN), TLS handshake, Server hello (2):
        * TLSv1.3 (IN), TLS handshake, Certificate (11):
        * TLSv1.3 (IN), TLS handshake, Finished (20):
        * SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384
    ```    
    - TLSハンドシェイク：  
        TLS1.3が使われて、クライアントとサーバー間で安全な通信が確立された。
        - `Client hello`と`Server hello`のやり取りが行われ、セキュリティパラメータが合意される  

        - サーバーからの証明書(`Certificate`)が提供され、それがクライアント側で検証された。

        - `TLS_AES_256_GCM_SHA384`という暗号化方式が使われて、データが安全に送受信されることが確認された。

    ---

    #### 3. サーバー証明書の検証
    ```bash
        * Server certificate:
        *  subject: CN=*.google.com
        *  start date: Aug 12 06:33:49 2024 GMT
        *  expire date: Nov  4 06:33:48 2024 GMT
        *  issuer: C=US; O=Google Trust Services; CN=WR2
        *  SSL certificate verify ok.
    ```

    - サーバー証明書の情報：  
        サーバー証明書が有効であり、ドメイン名`google.com`に対して正しいことが確認された(`SSL certificate verify ok.`)。

    - 証明書の発行者は`Google Trust Services`であり、証明書の有効期限は2024年11月4日(`Nov  4 06:33:48 2024 GMT`)。

    ---

    #### 4. HTTP/2リクエストの送信
    ```bash
        * using HTTP/2
        > GET / HTTP/2
        > Host: google.com
        > User-Agent: curl/8.5.0
        > Accept: */*
    ```

    - HTTP/2リクエスト：  
        暗号化されたセッションの上で、HTTP/2による`GET /`リクエストが送信された。

    ---

    #### 5. サーバーからのリダイレクト応答
    ```bash
        < HTTP/2 301
        < location: https://www.google.com/
        < content-type: text/html; charset=UTF-8
        < content-length: 220
    ```

    - HTTP 301リダイレクト：
        Googleのサーバーはリクエストに対してステータスコード`301 Moved Permanently`を返し、新しいURL`https://www.google.com/`へのリダイレクトを指示している。

    ---

    #### 6. レスポンスのHTML
    ```bash
        <HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
        <TITLE>301 Moved</TITLE></HEAD><BODY>
        <H1>301 Moved</H1>
        The document has moved
        <A HREF="https://www.google.com/">here</A>.
        </BODY></HTML>
    ```

    - レスポンスのボディ：  
        HTMLで`301 Moved`のページが表示されており、リンク先として`https://www.googl.com/`が案内されている。