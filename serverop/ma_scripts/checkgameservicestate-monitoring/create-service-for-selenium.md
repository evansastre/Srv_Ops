# Create service for selenium

#### install selenium on client part <a id="Createserviceforselenium-installseleniumonclientpart"></a>

```bash
sudo yum install centos-release-scl # install SCL
sudo yum install python27
scl enable python27 bash
pip install --upgrade pip
yum install gcc
pip install psutil
pip install -U selenium
```

#### install selenium and java support units on server part <a id="Createserviceforselenium-installseleniumandjavasupportunitsonserverpart"></a>



selenium-server file need:

1. selenium-server: [http://selenium-release.storage.googleapis.com/3.6/selenium-server-standalone-3.6.0.jar](http://selenium-release.storage.googleapis.com/3.6/selenium-server-standalone-3.6.0.jar) or find latest version below: [http://www.seleniumhq.org/download/](http://www.seleniumhq.org/download/)
2. chrome webdriver [http://www.seleniumhq.org/docs/03\_webdriver.jsp](http://www.seleniumhq.org/docs/03_webdriver.jsp) or [https://sites.google.com/a/chromium.org/chromedriver/](https://sites.google.com/a/chromium.org/chromedriver/)
3. java JRE [http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)
4. Run.

{% code-tabs %}
{% code-tabs-item title="start\_selenium\_server.bat" %}
```bash
java  -jar selenium-server-standalone-3.6.0.jar
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### Create service <a id="Createserviceforselenium-Createservice"></a>

1.Download tools : srvany.exe and instsrv.exe from microsoft.

2.Put them into C:\software\python\selenium\

3.Run cmd.

```bash
pushd C:\software\python\selenium\
instsrv.exe selenium C:\software\python\selenium\srvany.exe
```

4.Add new key to registry

```bash
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceName\Parameters /v Application /t REG_SZ /d "java -jar selenium-server-standalone-3.8.1" /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceName\Parameters /v AppDirectory /t REG_SZ /d "C:\software\python\selenium" /f
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceName\Parameters /v AppParameters /t REG_SZ /d "" /f
```

5.Start service and set automatic start

```text
sc start selenium
sc config selenium start= auto
```

