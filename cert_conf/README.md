## Setup Links

[Create Valid Certificate For Local Domain](https://justmarkup.com/articles/2018-05-31-https-valid-certificate-local-domain/)<br/>
[Tell Browser To Trust Certificate File](https://www.dionysopoulos.me/forge-your-own-ssl-certificates-for-local-development/#Install_the_Certificate_Authority_529)<br/>

### key takeaways

<p>The script will ask for a PEM pass phrase – enter something – it should be secure and you should remember it.<p>
<code>openssl req -x509 -new -keyout root.key -out root.cer -config root.cnf</code><br/>

<p>You have to change the following things here. First, change organizationName to the same name you have set in your root.cnf. Next, change DNS.1 to your local domain name. You can also use multiple here by using DNS.2, DNS.3 and so on.

After saving the file, open your command line again and run the following:<p>
<code>openssl req -nodes -new -keyout server.key -out server.csr -config server.cnf</code><br/>

### Generate the certificate
<code>openssl x509 -days 3650 -req -in server.csr -CA root.cer -CAkey root.key -set_serial 123 -out server.cer -extfile server.cnf -extensions x509_ext</code><br/>

### Install the Certificate Authority

<p>On every OS there are different ways, how to install the Certificate Authority. Please see this [post](https://www.dionysopoulos.me/forge-your-own-ssl-certificates-for-local-development/#Install_the_Certificate_Authority_529) to find out how to install it on your OS. Note that for Firefox you need an additional installation as they use their own certificate authority store.

In all cases you need to install the root.cer and not the server.cer – took me some time to figure this out.

After installing it and restarting the browser, the ceritificate is now valid and you can test everything related to https on your local machine. 🎉</p>

