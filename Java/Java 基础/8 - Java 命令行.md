## javac

编译生成 .class 文件
### 相关参数

- -p 指定生成路径
## java

运行编译文件
### 相关参数

- -cp 指定 classpath
## Examples

- junit-4.13.2.jar
	- org.junit.runner.JUnitCore                                                                
	- org.junit.runner.OrderWith                                                                
	- org.junit.runner.OrderWithValidator                                                       
	- org.junit.runner.Request
	- ...
- hamcrest-core-1.3.jar
### TestApp.java

```java
public class TestApp {
	@Test
	public void say() {
		System.out.println("Test method say success");
	}
}
```
### 命令行测试

```sh
# 生成 TestApp.class 文件
javac -p . -cp .:junit-4.13.2.jar:hamcrest-core-1.3.jar TestApp.java
# 测试
# 使用 junit 中测试相关的类
java -cp .:junit-4.13.2.jar:hamcrest-core-1.3.jar org.junit.runner.JUnitCore testApp
```