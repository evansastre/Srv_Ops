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

