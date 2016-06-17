# How to create a self-signed SSL Certificate ...


## Step 1: Generate a Private Key

    $> openssl genrsa -des3 -out server.key 1024

  Generating RSA private key, 1024 bit long modulus
  .............................++++++
  .........++++++
  e is 65537 (0x10001)
  Enter pass phrase for server.key:
  3058:error:28069065:lib(40):UI_set_result:result too small:/SourceCache/OpenSSL098/OpenSSL098-52.30.1/src/crypto/ui/ui_lib.c:850:You must type in 4 to 1023 characters
  Enter pass phrase for server.key:
  3058:error:28069065:lib(40):UI_set_result:result too small:/SourceCache/OpenSSL098/OpenSSL098-52.30.1/src/crypto/ui/ui_lib.c:850:You must type in 4 to 1023 characters
  Enter pass phrase for server.key:
  Verifying - Enter pass phrase for server.key:

## Step 2: Generate a CSR (Certificate Signing Request)

    $> openssl req -new -key server.key -out server.csr
  
  Enter pass phrase for server.key:
  You are about to be asked to enter information that will be incorporated
  into your certificate request.
  What you are about to enter is what is called a Distinguished Name or a DN.
  There are quite a few fields but you can leave some blank
  For some fields there will be a default value,
  If you enter '.', the field will be left blank.
  -----
  Country Name (2 letter code) [AU]:GB
  State or Province Name (full name) [Some-State]:Cornwall
  Locality Name (eg, city) []:Hayle
  Organization Name (eg, company) [Internet Widgits Pty Ltd]:Freshsauce      
  Organizational Unit Name (eg, section) []:dev
  Common Name (e.g. server FQDN or YOUR name) []:local.dev
  Email Address []:support@tyourdomain.com

  Please enter the following 'extra' attributes
  to be sent with your certificate request
  A challenge password []:
  An optional company name []:

## Step 3: Remove Passphrase from Key

    $> cp server.key server.key.org
    $> openssl rsa -in server.key.org -out server.key

  Enter pass phrase for server.key.org:
  writing RSA key

## Step 4: Generating a Self-Signed Certificate

    $> openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

  Signature ok
  subject=/C=GB/ST=Cornwall/L=Hayle/O=Freshsauce/OU=dev/CN=local.dev/emailAddress=support@tyourdomain.com
  Getting Private key

## Step 6: Configuring SSL Enabled Virtual Hosts

  We're good to go build of nginx-custom will reference the certificates