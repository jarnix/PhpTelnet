PhpTelnet
=========

(amazing) php telnet client.

Basic http example :

```
$client = new \PhpTelnet\Client('www.google.com', 80);
$html=$client->execute('GET /');
echo $html;
$client->disconnect('');
```


Example connecting to a varnish telnet server ("varnish1" is the name of the host, "wonderfulpassword" is the password)

```
$client = new \PhpTelnet\Client('varnish1', 6082);
$client->connect();

// authentication
$resp = $client->getResponse();
$arrResp = explode("\n", $resp);
$challenge = $arrResp[1];
$authCode = hash('sha256', $challenge . "\n" . "wonderfulpassword" . "\n" . $challenge . "\n");
$resp = $client->execute('auth ' . $authCode);
$arrResp = explode("\n", $resp);
if (substr($arrResp[0], 0, 3) == '200') {
    echo "logged in";
} else {
    echo "login failure";
}
$client->disconnect('quit');`
```
