##Tomcat可以通过catalina.properties的server和shared设置，为webapp提供公用类库。

##使一些公用的、不需要与webapp放在一起的设置信息单独保存，在更新webapp的war的时候无需更改webapp的设置。

 org.apache.tomcat.util.net.JIoEndpoint 
```java
 if (getAddress() == null) {
                    serverSocket = serverSocketFactory.createSocket(getPort(),
                            getBacklog());
                } else {
                    serverSocket = serverSocketFactory.createSocket(getPort(),
                            getBacklog(), getAddress());
                }
```

http://www.2cto.com/kf/201606/518709.html

---
acceptCount参数（socket的backlog）（重要）
对于acceptCount这个参数，含义跟字面意思并不是特别一致（个人感觉），容易跟maxConnections,maxThreads等参数混淆；实际上这个参数在tomcat里会被映射成backlog:

```java
static {
    replacements.put("acceptCount", "backlog");
    replacements.put("connectionLinger", "soLinger");
    replacements.put("connectionTimeout", "soTimeout");
    replacements.put("rootFile", "rootfile");
}
```
tomcat Standard IO中acceptcount其实就是backlog
tomcat默认会设置为100，java则默认是50。

<http://blog.csdn.net/yanli1979/article/details/52086734>



