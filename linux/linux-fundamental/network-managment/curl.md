# curl

```text
# save
$ curl http://www.linuxidc.com > page.html
$ curl -o page.html http://www.linuxidc.com
$ curl -O http://cgi2.tky.3web.ne.jp/~zzh/screen[1-10].JPG
#-O can automatically save to local according to the file name on the server


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

