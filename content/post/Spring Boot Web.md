+++
draft = false
image = "https://i.loli.net/2019/03/07/5c8128cbe1e4f.jpg"
showonlyimage = true
date = "2019-3-07T20:23:59+05:30"
title = "Spring Boot Web 学习记录"
writer = "子适"
categories = [ "read" ]
weight = 1
+++

Spring Boot Web 开发
<!--more-->


# SpringBoot Web

## 入门

### 0.介绍

- 微服务的基本架构
- 微服务-----》SpringCloud —> SpringBoot

### 1.启动方式

- 右键 run
- cd 到项目目录， `mvn spring-boot:run`
- cd 到项目目录 
  - `mvn install`编译，然后进入新出现的 target/ 目录
  - `java -jar demo-0.0.1-SNAPSHOT.jar`

### 2.项目属性配置

#### 2.1 基本配置

- 项目配置文件 `application.properties`

- 可以修改为 `application.yml`
  - `yml` 语法冒号后必须跟空格
- `properties` 配置文件

```properties
server.port=8081
```

- `yml` 配置文件 推荐

```yml
server:
  port: 8081
cupSize: B
age: 18
content: "cupSize: ${cupSize},age: ${age}"
```

访问网址 `http://localhost:8081/hello`

#### 2.2 使用配置文件中的变量

```java
@RestController
public class HelloController {
	// @Value 实现配置变量的注入
    @Value("${cupSize}")
    private String cupSize;

    @Value("${age}")
    private String age;

    @Value("${content}")
    private String content;

    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String say(){
        return content;
    }
}
```

#### 2.3 组合成对象使用配置属性

- 当一个对象属性过多时，`@Value` 一个一个注入太繁琐，使用`@Component` 和 `@ConfigurationProperties` 来分组注入
- 需要在 pom.xml 中添加`spring-boot-configuration-processor`组件

```xml
<dependency>
            <groupId> org.springframework.boot </groupId>
            <artifactId> spring-boot-configuration-processor </artifactId>
            <optional> true </optional>
        </dependency>
```

- GirlProperties.java

```java
@Component
@ConfigurationProperties(prefix = "girl")
public class GirlProperties {
    private String cupSize;
    private Number age;

    public String getCupSize() {
        return cupSize;
    }

    public void setCupSize(String cupSize) {
        this.cupSize = cupSize;
    }

    public Number getAge() {
        return age;
    }

    public void setAge(Number age) {
        this.age = age;
    }
}
```

- 使用

```java
@RestController
public class HelloController {

    @Autowired
    private GirlProperties girlProperties;

    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String say(){
        return girlProperties.getCupSize();
    }
}

```

#### 2.4 多个配置环境

```yml
#application.yml
spring:
	profiles:
		active: dev  #使用 dev 配置
```

![](https://i.loli.net/2019/03/07/5c812cbf44bff.png)

### 3. Controller 的使用

#### @Controller

- 处理http请求
- 返回模板和数据

#### @RestController

- 组合注解

#### @RequestMapping

- 匹配url

- 可选多个url，请求方法(推荐不要省略)

  ```java
  @RequestMapping(value = {"/hello","/hi"}, method = RequestMethod.GET)
  ```

#### @GetMapping

- 简化@RequestMapping的书写,对应还有 @PostMapping 等

  ```java
  @GetMapping(value = "/say")
  // 等价于
  @RequestMapping(value = "/say",method = RequestMethod.GET)
  ```

#### @PathVariable

- 获取url中的数据
- Localhost:8080/say/100

```java
@RequestMapping(value = "/say/{id}",method = RequestMethod.GET)
public String say(@PathVariable("id") Integer id){
    return "id" + id;
}
```

#### @RequestParam

- 获取请求参数的值
- 另一种url格式 /say?id=100

```java
public String say(@RequestParam("id") Integer myId){
    
}
```

- 设定是否必须传递，默认值等

```java
@RequestParam(value = "id", required = false, defaultValue = "0") Integer myId
```

#### @GetMapping

- 组合注解

### 3. 数据库操作

- Spring-Data-Jpa

  - JPA Java Persistence API 是一套对象持久化的标准。
  - 实现的产品有 Hibernate, TopLink 等
  - Spring-Data-Jpa 是 Spring 对 Hibernate 的封装

- 数据库使用

  - 添加组件 `mysql-connector-java`  `spring-boot-starter-data-jpa`
  - 配置文件 .yml 文件

  ```yml
  datasource:
  	driver-class-name: com.mysql.cj.jdbc.Driver
  	url: jdbc:mysql://127.0.0.1:3306/dbgirl
  	username:root
  	password:123456
  jpa:
  	hibernate:
  		ddl-auto: create	# 运行时自动创建表
  	show-sql: true
  ```

  - 创建类。 使用 `@Entity` 注解来表明这是一个表

    ```java
    @Entity
    public class Girl {
        @Id
        @GeneratedValue
        private Integer id;
        private String cupSize;
        private Integer age;
        ……
    }
    ```

    - 创建接口 GirlRepository ，来继承 JpaRepository 接口，从而获得该接口的方法

    ```java
    public interface GirlRepository extends JpaRepository<Girl, Integer> {
    }
    ```

    - 使用

      ```java
      @RestController
      public class GirlContorller {
          @Autowired
          private GirlRepository girlRepository;
      
          @GetMapping(value = "/all")
          public List<Girl> girlList(){
              // 获取所有数据
              return girlRepository.findAll();
          }
          @GetMapping(value = "/girls/{id}")
          public Girl girlFind(@PathVariable("id") Integer id){
              // findById() 返回一个 Optional 类，用 get() 拿到值
              return girlRepository.findById(id).get();
          }
          ……
      }
      ```

      

### 4. 事务管理

- 数据库的事务——作为单个逻辑单元执行的一系列操作，或者操作都成功，或者都不成功
- 例如：电商网站出库和扣款
- 在插入数据的操作函数前加 `@Transactional` 注解

```java
@Service
public class GirlService {
    @Autowired
    private GirlRepository girlRepository;

    @Transactional
    public void insertTwo(){
        // 创建 girlA girlB 两个对象
        girlRepository.save(girlA);
        girlRepository.save(girlB);
    }
}
```

- 此时，插入 girlA girlB 的操作要么都成功，要么都不成功

## 提高

### 1. 使用 @Valid 表单验证

#### 1.1 简化方法的传入参数，减少耦合

```java
@PostMapping(value = "girls/{id}")
    public Girl girlUpdate(@PathVariable("id") Integer id,
                           @RequestParam("cupSize") String cupSize,
                           @RequestParam("age") Integer age){
        Girl girl = new Girl();
        girl.setId(id);
        girl.setCupSize(cupSize);
        girl.setAge(age);
        // 因为有id值，会自动更新
        return girlRepository.save(girl);
    }
```

简化为

```java
@PostMapping(value = "girls/{id}")
    public Girl girlUpdate(Girl girl){
        girl.setId(girl.getId());
        girl.setCupSize(girl.getCupSize());
        girl.setAge(girl.getAge());
        // 因为有id值，会自动更新
        return girlRepository.save(girl);
    }
```

#### 1.2 验证传入参数

- 在对象类中设置参数限制

```java
@Min(value = 18, message = "under 18 yeas old")
private Integer age;
```

- 使用 @Valid 检查传入对象，并将检查结果封装为 BindingResult 对象

```java
public Girl girlAdd(@Valid Girl girl, BindingResult bindingResult){
        if(bindingResult.hasErrors()){
            System.out.println("Under 18 years old");
            return null;
        }
        girl.setCupSize(girl.getCupSize());
        girl.setAge(girl.getAge());
        return girlRepository.save(girl);
    }
```

- @Valid 与 BindingResult
  - @Valid 注解在参数上，表示让 Spring 验证该参数的属性
  - @Valid 参数后紧跟着一个 BindingResult 参数，用于获取校验结果，否则 Spring 会在校验不通过时抛出异常
- [常用参数限制](https://www.jianshu.com/p/f85c248294f6)

### 2. 使用 AOP 处理请求

#### 2.1 AOP 面向切面编程

- 一种编程范式，与语言无关

- 面向切面编程，不限制于具体业务。（红线就是切面）

  ![](https://i.loli.net/2019/03/07/5c812ce6f1e35.png)

  #### 2.2 使用 AOP

  - 添加依赖 `spring-boot-starter-aop`

  ```xml
  <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aop</artifactId>
  </dependency>
  ```

  - 创建类

  ```java
  @Aspect
  @Component	// 加入容器
  public class HttpAspect {
      @Before(value = "execution(public * com.cshi.girl.controller.GirlContorller.*(..))")
      public  void log(){
          System.out.println("sssssss");
      }
  }
  ```

  此时，所有调用 GirlController 类方法的 http 请求都会触发 log 方法

  - 完整 logger 切面实现

  ```java
  @Aspect
  @Component
  public class HttpAspect {
  
      private final static Logger logger = LoggerFactory.getLogger(HttpAspect.class);
  
      @Pointcut(value = "execution(public * com.cshi.girl.controller.GirlContorller.*(..))")
      public  void log(){
      }
  
      @Before("log()")
      public void doBefore(){
          logger.info("before");
      }
  
      @After("log()")
      public void doAfter(){
          logger.info("after");
      }
      // 打印返回的对象
      @AfterReturning(returning = "object", pointcut = "log()")
      public void doAfterRetruning(Object object){
          logger.info("reponse = {}", object.toString());
      }
  }
  ```

### 3. 统一异常处理

#### 3.1 异常抛出与捕获

- 异常抛出 `throws Exception`

```java
public void getAge(Integer id) throws Exception{
        Girl girl = girlRepository.findById(id).get();
        Integer age = girl.getAge();
        if(age < 10){
            throw new GirlException(100, "小学");
        }else if(age > 10 && age < 18){
            throw new GirlException(101, "中学");
        }else{
            throw new GirlException(102, "成年人");
        }
```

- 异常的捕获
  - `@ControllerAdvice`——默认应用于使用`@Controller` 和 `@RestController` 注释的所有类。可通过添加参数控制覆盖的类。
  - `@ExceptionHandler` ——异常处理。结合 `@ControllerAdvice` 处理全局抛出的异常

```java
@ControllerAdvice
public class ExceptionHandle {
    @ExceptionHandler(value = Exception.class)
    @ResponseBody	// 保证返回json数据
    public Result handle(Exception e){
        // GirlException 是自定义异常类
        if(e instanceof GirlException){
            GirlException girlException = (GirlException) e;
            return ResultUtil.error(girlException.getCode(), girlException.getMessage());
        }else{
            return ResultUtil.error(-1, "未知错误");
        }
    }
}

```



#### 3.2 自定义异常类

- 继承 RuntimeException 类
- `Error` 、`Exception`、`RuntimeException` 都继承自 `Throwable`
- 其中，继承`Exception` 的类都是检查型异常(checked exceptions)。这类异常必须被 `try...catch…` 处理或者 `throws` 到外部
- 继承 'RuntimeException' 的异常是非检查型异常 (unchecked exceptions)，不强制处理。有 NullPointerException, ArrayIndexOutOfBoundsException 等等

```java
public class GirlException extends RuntimeException {
    private Integer code;
    public GirlException(Integer code, String msg){
        // super()语句必须在方法的第一句
        // Exception() 类有 msg 属性
        super(msg);
        // 增加 Code 属性
        this.code = code;
    }
    public Integer getCode() {
        return code;
    }
    public void setCode(Integer code) {
        this.code = code;
    }
}
```



#### 3.3 定义枚举类管理 errorCode 和异常信息

- 枚举类实现

```java
public enum ResultEnum {
    UNKNOW_ERROR(-1, "未知错误"),
    SUCCESS(0, "成功"),
    PRIMARY_SCHOOL(100, "小学"),
    MIDDLE_SCHOOL(101, "初中"),
    ;
    private Integer code;
    private String msg;

    ResultEnum(Integer code, String msg){
        this.code = code;
        this.msg = msg;
    }

    public Integer getCode() {
        return code;
    }

    public String getMsg() {
        return msg;
    }
}
```

- 使用

```java
public void getAge(Integer id) throws Exception{
        Girl girl = girlRepository.findById(id).get();
        Integer age = girl.getAge();
        if(age < 10){
            throw new GirlException(ResultEnum.PRIMARY_SCHOOL);
        }else if(age > 10 && age < 18){
            throw new GirlException(ResultEnum.MIDDLE_SCHOOL);
        }
    }
```



### 4. 单元测试

#### 4.1 测试 Service

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class GirlServiceTest {

    @Autowired
    private GirlService girlService;

    @Test
    public void findOneTest(){
        Girl girl = girlService.findOne(12);
        Assert.assertEquals(Integer.valueOf(12), girl.getAge());
    }
}
```



#### 4.2 测试API

```java
@RunWith(SpringRunner.class)
@SpringBootTest
@AutoConfigureMockMvc
public class GirlContorllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void girlList() throws Exception{
        mvc.perform(MockMvcRequestBuilders.get("/girls")).
                andExpect(MockMvcResultMatchers.status().isOk()).
                andExpect(MockMvcResultMatchers.content().string("abc"));
    }
}
```

