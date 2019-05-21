# spock

Online test

[https://meetspock.appspot.com/](https://meetspock.appspot.com/)

Example:

```text
import spock.lang.*

// Hit 'Run Script' below
class MyFirstSpec extends Specification {
  def "let's try this!"() {
    expect:
    Math.max(1, 2) == 3
  }
  /*def "test Action getHtml2"(){
    given:     
        def action2 = new Action()     
        def html          
    when:     
        html = action2.getHtml('Hello World')          
    then:     
        html != null     
        html == 'html:Hello World2'//与预期不符 
    
    expect:    
        'html:Hello World' == action2.getHtml('Hello World')
  }*/

  static boolean skip = true 
  @IgnoreIf({ MyFirstSpec.skip }) 
  def "should not execute this test if `IgnoreIfSepc.skip` is set to TRUE"() { 
      when: 
        def res = 1 + 1 

      then: 
       res == 3 
  } 

  def "should execute this test every time"() { 
      when: 
         def res = 1 + 1 

      then: 
      res == 2 
    } 
}
​
```



另一种方法，这是通过使用[spock](https://stackoverflow.com/questions/tagged/spock)的配置文件，以包括/排除测试或基类。

首先您在测试中创建自己的注释和地点。   
然后你写一个Spock配置文件。   
当你运行你的测试，你可以在`spock.configuration`属性设置为您所选择的配置文件。   
这种方式可以包含/排除你想测试和基类。斯波克配置文件的

例子：

```text
runner { 
    println "Run only tests" 
    exclude envA 
} 
```

您的测试：

```text
@envA 
def "some function"() { 
    .. 
} 
```

然后，您可以运行：

```text
./gradlew test -Pspock.configuration=mySpockConfig.groovy 
```

这里是一个[github example](https://github.com/roy424/spock-annotations)

