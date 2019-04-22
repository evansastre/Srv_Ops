# curl

```text
# save
$ curl http://www.linuxidc.com > page.html
$ curl -o page.html http://www.linuxidc.com
$ curl -O http://cgi2.tky.3web.ne.jp/~zzh/screen[1-10].JPG
#-O can automatically save to local according to the file name on the server

$curl -o #2_#1.jpg http://cgi2.tky.3web.ne.jp/~{zzh,nick}/[001-201].JPG
#Original: ~zzh/001.JPG —-> After downloading: 001-zzh.JPG Original: ~nick/001.JPG —-> After downloading: 001-nick.JPG


# The proxy server used and its port: -x
$ curl -x 123.45.67.89:1080 -o page.html http://www.linuxidc.com

# sing cookies to record session information
$ curl -x 123.45.67.89:1080 -o page.html -D cookie0001.txt http://www.linuxidc.com

# Continue to use the last cookie message left during the next visit
$ curl -x 123.45.67.89:1080 -o page1.html -D cookie0002.txt -b cookie0001.txt http://www.linuxidc.com

# Browser Information
$ curl -A "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)" -x 123.45.67.89:1080 -o page.html -D cookie0001.txt http://www.linuxidc.com

# referer
$ curl -A "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.0)" -x 123.45.67.89:1080 -e "mail.linuxidc.com" -o page.html -D cookie0001.txt http://www.linuxidc.com

```

## Breakpoint resume

```text
curl -r 0-1024 -o "test.part1" https://sourceforge.net/projects/lep-map3/files/latest/download/scripts.zip &\
curl -r 1025-2048 -o "test.part2" https://sourceforge.net/projects/lep-map3/files/latest/download/scripts.zip &\
curl -r 2049-4096 -o "test.part3" https://sourceforge.net/projects/lep-map3/files/latest/download/scripts.zip &\
curl -r 4097- -o "test.part4" https://sourceforge.net/projects/lep-map3/files/latest/download/scripts.zip
cat test.* > test.zip
```

## Browser FTP

```text
$ curl -u name:passwd ftp://ip:port/path/file
$ curl ftp://name:passwd@ip:port/path/file
```

## Upload FTP

```text
# -T
$ curl -T localfile -u name:passwd ftp://upload_site:port/path/
```

## Upload HTTP

```text
$ curl -T localfile http://cgi2.tky.3web.ne.jp/~zzh/abc.cgi
#HTTP PUT method
```

## Read website use POST

```text
# -d
$ curl -d "user=myusername&password=12345" http://www.linuxidc.com/login.cgi

```

## File upload in POST mode



```text
<form method="POST" enctype="multipar/form-data" action="http://cgi2.tky.3web.ne.jp/~zzh/up_file.cgi">
<input type=file name=upload>
<input type=submit name=nick value="go">
</form>
Such an HTTP form, we want to use curl to simulate, it is this syntax:

$ curl -F upload=@localfile -F nick=go http://cgi2.tky.3web.ne.jp/~zzh/up_file.cgi

```



