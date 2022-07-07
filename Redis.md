# Redis

Redis是一个典型的NoSQL非关系型数据库，其中的数据都是以键值对的形式进行保存的，同时运行时仅有单线程运行，保证了命令的原子性，虽然是单线程但是由于基于内存、IO多路复用、编码优良的原因，使得它反而具有极低的延迟和极高的速度，同时虽然基于内存存储，但是Redis会定时备份数据到磁盘中，保证了数据的安全性，同时它还支持主从集群和分片集群和多语言客户端，可谓是优势满满

## 基础入门

### NoSQL

显然，NoSQL数据库与常规的SQL语言关系数据库有很大的差别，想要说明NoSQL的特点，我们就需要将其与SQL数据库进行对比

1. SQL数据库是结构化的，里面所有的数据都有格式的要求，一旦里面的数据约束被定义好了，之后所有的数据都应该严格遵守里面的约定，同时表的结构在项目运行之后一般不允许修改，而NoSQL数据库是非结构化数据库，意味着我们所有的字段和结构都能够任意修改，灵活性更高
2. SQL数据库所有的字段与字段之间往往是有关联的，表与表的关系由外键进行联系，而NoSQL虽然也可以表示关系，但是往往也是用JSON存储，数据免不了会产生冗余
3. SQL数据库增删改查的语法都是固定的，只要是SQL数据库，我们就可以用同一条语句进行查询，而NoSQL则根据不同的平台有不同的查询信息的方式，没有统一的标准，不同的库之间语法差别很大
4. SQL数据库在增删改的过程中是需要满足事务的ACID原则，数据库软件也会帮助我们实现ACID原则，但是NoSQL一般都无法全部满足ACID，而是基本满足，称为BASE原则
5. SQL数据库往往存储在硬盘中，调用和查询相对比较麻烦和耗时，而NoSQL大多数都运行在内存中，查询性能非常高
6. SQL数据库在设计的时候就没有考虑到分布式的功能，影响性能的仅是本机这台服务器的质量，而NoSQL数据库是具有水平扩展性的，考虑到了数据拆分的需求，根据数据的id哈希计算结果判断数据应该被存储在何处，很容易就能够做到分布式的要求

### 安装

1. 创建一个服务器环境，当然直接Docker一把梭

2. [下载](https://redis.io/download/)最新redis压缩包，拷贝到服务器`docker cp /home/chillyblaze/Downloads/redis-6.2.6.tar.gz redist:/root/`

3. `tar -zxvf redis-6.2.6.tar.gz`解压

4. 进入安装目录，`make && make install`

5. 检查安装成果，`cd /usr/local/bin && ls -al`，会看到如下内容

   ![image-20220330125042719](https://s2.loli.net/2022/03/30/repBNLb1SxWngHK.png)

其中的可执行文件的用处之后会讲解，由于这个目录正属于我们的path路径，因此我们可以在任意位置直接`redis-server`即可运行redis

![image-20220330125307031](https://s2.loli.net/2022/03/30/uQYRc2UOiw6Vgtx.png)

但是这个是前台启动方式，如果需要后台启动，我们就需要修改配置文件

回到安装目录，备份初始配置文件`cp redis.conf redis.conf.bak`

修改一些其中的配置项

```conf
# 允许哪台主机访问
bind 0.0.0.0  # 允许所有主机访问
# 是否后台启动redis服务
daemonize yes
# 设置redis访问密码
requirepass 1351
# redis监听的端口
port 6379
# 工作目录，默认是当前运行redis-server的安装目录
dir . 
# 数据库数量，设置为1代表只使用一个库，默认有16个库
databases 1
# redis最大可使用内存
maxmemory 521mb
# 日志文件，如果为空则不记录日志
logfile "redis.log"
```

修改之后我们要让redis根据我们的配置文件启动，因此需要`redis-server redis.conf`（因为当前就在安装目录下）

`ps -ef | grep redis`查看服务

### 常用命令

在介绍命令之前我们需要连接上我们的redis服务端才行，因此我们直接`redis-cli -h 127.0.0.1 -p 6379`即可连接本地redis，但是这样我们也仅仅是连上了，什么都干不了，因此我们需要在连接时指定密码或者连接上之后设置密码

![image-20220330151248127](https://s2.loli.net/2022/03/30/kQPEJxLcsCtvUZR.png)

接下来我们就可以在给定命令行界面中愉快的输入命令了，预先我们需要了解到Redis除开key值必须为字符串之外，value支持五种基本数据类型：string（字符串），hash（哈希），list（列表），set（集合）及zset(sorted set：有序集合)，而每一种数据类型都相应有着不同的操作命令和操作方式，我们可以在官网上看到所有命令的[帮助文档](https://redis.io/commands/)，同时也可以在redis命令行界面中通过比如`help @string`来查看和string数据类型有关的所有命令

接下来也会按照分组的方式介绍各组的命令内容

- `ping`和redis服务端打乒乓球（验证连接情况）

- 通用命令（`Generic`组）

  - `set [key] [string]`设置一个key和字符串类型的value，==当然这个命令不属于通用命令==
  - `keys [key名，支持*和?通配符]`查看符合模版的所有key，但是由于查询效率不高因此在生产环境下不建议使用`keys *`查询所有key
  - `del [key]`删除一个指定的key，支持多个key，并返回正确删除的key数，因此如果删不存在的key就会返回少一个
  - `exists [key]`查看key是否存在
  - `expire [key] [seconds]`给一个key设置有效期，有效期到期时自动删除，建议我们将存入redis里的所有key都设置有效期
  - `ttl [key]`查看该key还能活多长时间，同时-2代表不存在这个key，-1代表该key永久有效

  ![image-20220330153552600](https://s2.loli.net/2022/03/30/YSyac8D3VJGurX9.png)

- Sring类型命令

  > 注意到如果设置的值为纯数字，虽然也属于String类型，但是底层编码为二进制数字，因此我们可以对其进行一些额外操作

  - 上面提到的set
  - `get`通过key获取String类型的value
  - `mset/mget`批量添加/获取键值对/键值
  - `incr [key]/incrby [key] [num]`自增/自增某个指定数（可以是负数，那就是自减
  - `incrbyfloat [key] [step]`指定浮点数增长固定值
  - `setnx [key] [string]/set [key] [string] nx`没有该key的时候添加，两条命令完全一致
  - `setex [key] [seconds] [string]/set [key] [string] ex [seconds]`在设置值时指定有效期

  > 在redis中，key可以进行分层，中间由`:`隔开，常用是`[项目名]:[业务名]:[类型]:[id]`

- Hash类型命令

  > Hash类型就是在redis外部的键值对之外又在内部分为了field和value，称为哈希键和哈希值，这何尝不是一种套娃

  其中几乎所有的命令都是在String类型的基础上在前面加了一个`H`，因此直接上图说明，顺便把之前的演示补上

  ![image-20220330161531769](https://s2.loli.net/2022/03/30/AVksHqpMm7d3cTQ.png)

- List类型命令

  > 是一个双向链表，也可以看做一个栈，支持正向检索和反向检索，插入和删除速度表较快，有序

  - `lpush/rpush [key] [element...]`从左/右侧插入一个或多个元素
  - `lpop/rpop [key] [count]`左/右移除某count个元素
  - `lrange [key] [start] [end]`返回一段下标范围内的所有元素，第一位为0，支持负下标，-1为最后一位
  - `blpop/rlpop [key] [seconds]`在规定时间内阻塞式获取栈顶元素，当监视的链表中插入元素时立即退出并返回弹出的值

  这种类型可以轻松的模拟栈和队列等数据结构

- Set类型命令

  > 可以看做是集合类型，像一个池子，内部元素无序，支持集合间运算

  - `sadd [key] [member...]`往`key`池子里丢一个元素
  - `srem [key] [member...]`移除某一个指定元素
  - `scard [key]`返回元素个数
  - `sismember [key] [member]`判断某个元素是否在这个池子里
  - `smembers`获取所有元素（无序）
  - `sinter/sdiff/sunion [set1key] [set2key]`取两个set交/差/并集

- SortedSet类型命令

  > 是一个内置了排序的Hash类型，内部score值必须为数值类型

  - `zadd [key] [score] [member]`添加一个或多个键值到某个key中，默认会对该key中的score进行升序排序，同时如果已存在member键则更新其score值
  - `zrem [key] [member]`删除一个指定元素
  - `zscore [key] [member]`获取指定元素的score值
  - `zrank [key] [member]`获取指定元素score值的升序排名
  - `zcard [key]`获取元素个数
  - `zcount [key] [min] [max]`统计score值在给定范围内所有元素的个数
  - `zincrby [key] [count] [member]`让指定能够元素自增count值
  - `zrange [key] [min] [max]`获取升序中指定排名范围内的元素
  - `zrangebyscore [key] [min] [max]`获取指定score范围内的元素
  - `zdiff/zinter/zunion`求差交并同set类型
  - 所有的排序指令的z后加rev则为降序排序的某项值（比如`zrevrange`）

### Spring data redis

单单一个Redis搞不出什么花样，Redis的所有服务都需要依靠着某种语言的客户端进行运行，因此我们以Java客户端为例，对Redis进行与客户端的交互测试

可以参考[官方网站](http://www.redis.cn/clients.html)，给出了各种语言的客户端类型

![image-20220330185616656](https://s2.loli.net/2022/03/30/UumaG68vDwMfONj.png)

每一个客户端都有它的优势，但是优势最大的还是Spring，直接将最火爆的`jedis`和`lettuce`进行了一个整合，搞出来了一个`spring data redis`，我们直接跳过基础的原生客户端，直接用spring整合包

Spring进一步把上述的各种数据结构进行了一个封装，提供了RedisTemplate工具类，用以将不同的数据类型的操作API封装到了不同的类型中

![image-20220330192901439](https://s2.loli.net/2022/03/30/VvZF7iJoSmOdDNI.png)

#### 简单项目测试

1. 创建一个SpringBoot项目

   ![image-20220330193406596](https://s2.loli.net/2022/03/30/QZF8T2RXIagzrDi.png)

2. 引入连接池依赖

   ```xml
   <dependency>
       <groupId>org.apache.commons</groupId>
       <artifactId>commons-pool2</artifactId>
       <version>2.11.1</version>
   </dependency>
   ```

3. 配置`application.yaml`

   ```yaml
   spring:
     redis:
       host: 172.17.0.2
       port: 6379
       password: 1351
       lettuce:
         pool:
           max-active: 8
           max-idle: 8
           min-idle: 0
           max-wait: 100ms
   ```

4. `src/test/java/com/example/redisdemo/RedisDemoApplicationTests.java`编写测试程序测试连接

   ```java
   package com.example.redisdemo;
   
   import org.junit.jupiter.api.Test;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.test.context.SpringBootTest;
   import org.springframework.data.redis.core.RedisTemplate;
   
   @SpringBootTest
   class RedisDemoApplicationTests {
   
       @Autowired
       private RedisTemplate redisTemplate;
   
       @Test
       void testString() {
           // 写入一条数据
           redisTemplate.opsForValue().set("name", "test");
           Object name = redisTemplate.opsForValue().get("name");
           System.out.println(name);
       }
   
   }
   ```

#### 自定义序列化器

但是我们如果现在打开redis，会发现并没有`name=test`这个键值，而是多了一个类似`\xac\xed\x00\x05t\x00\x04name`这个样子的键，里面的值一般来说还取不出来，硬要取还得加个双引号，而且里面的值也乱七八糟的，这是怎么回事呢

![image-20220330204728224](https://s2.loli.net/2022/03/30/itfsuJ41eSjvbo3.png)

其实是因为我们调用Java的方法之后所有的内容在存入redis之前都需要经过序列化操作，而当我们不指定序列化器时，默认将所有的键和值都用`JdkSerializationRedisSerializer`（想找到这个序列化器就在set方法上打个断点单步调试）这个序列化器将我们的键值全部当作Java对象进行序列化存储进redis，因此就会在存储时出现乱码

我们想避免这种状况，就需要自己修改RedisTemplate的序列化方式了

我们可以先进到`RedisTemplate`里面，选中`RedisSerializer`按`Ctrl+H`即可看到这个接口的实现类层次结构

![image-20220330213952420](https://s2.loli.net/2022/03/30/6pO8awqgLRYvuIG.png)

根据这个要求，我们可以写一个自己的Template去进行个性化定制序列化器

```java
package com.example.redisdemo.redis.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.GenericJackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.RedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

@Configuration
public class RedisConfig {
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
        // 创建RedisTemplate对象
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        // 设置连接工厂
        template.setConnectionFactory(connectionFactory);
        // 创建JSON序列化工具
        StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();
        GenericJackson2JsonRedisSerializer jsonRedisSerializer = new GenericJackson2JsonRedisSerializer();
        // 设置Key的序列化
        template.setKeySerializer(RedisSerializer.string());  // 相当于传入stringSerializer
        template.setHashKeySerializer(stringRedisSerializer);
        // 设置Value的序列化
        template.setValueSerializer(jsonRedisSerializer);
        template.setHashValueSerializer(jsonRedisSerializer);  // 用两种不同的方式序列化指定类型
        // 返回
        return template;
    }
}
```

> ~~我是真的日了，这他妈是人写的？！！！~~
>
> 写完之后记得在`pom.xml`里面加依赖
>
> ```xml
>         <!--Jackson依赖-->
>         <dependency>
>             <groupId>com.fasterxml.jackson.core</groupId>
>             <artifactId>jackson-databind</artifactId>
>             <version>2.13.2</version>
>         </dependency>
> ```

接着在测试文件中指定接收的redisTemplate的泛型类型即可

```java
private RedisTemplate<String,Object> redisTemplate;
```

为了验证其是否真的能将Java对象转为JSON形式，我们可以创建一个类来测试一下

```java
@Data
@NoArgsConstructor
@AllArgsConstructor
public class User {
    private String name;
    private Integer age;
}
```

```java
@Test
void testSaveUser(){
    // 写入数据
    redisTemplate.opsForValue().set("user:100",new User("test",10));
    // 获取数据，自动反序列化成User对象
    User user = (User) redisTemplate.opsForValue().get("user:100");
    System.out.println("user = " + user);
}
```

测试结果

![image-20220330221436437](https://s2.loli.net/2022/03/30/XLyhUG1S4kFaRsY.png)

![image-20220330221509171](https://s2.loli.net/2022/03/30/qVDO4mZdIAYWKpQ.png)

成功了，同时可以发现在我们写入对象的时候它自动帮我们写入了一个`@class`的字节码，使得反序列化的时候可以直接找到所属的对象类进行，还是十分巧妙的

#### 本地序列化

但是这并不是最优解，因为我们发现就这个数据来看，`@class`里面的内容实在太多了，我们实际用到的数据才占了一小部分，一旦数据多起来之后，`@class`会占用大量内存，因此我们在存储小体量数据的时候应该考虑直接用`String`序列化器

因此在实际开发中，我们往往还是将数据通过字符串的形式进行传输，而在项目内部进行对传出数据和Redis返回字符串数据的序列化和反序列化

```java
@Autowired
private StringRedisTemplate stringRedisTemplate;
@Test
void testGsonHandler(){
    User user = new User("test", 10);
    Gson gson = new Gson();
    String s = gson.toJson(user);
    stringRedisTemplate.opsForValue().set("user:90",s);
    String sG = stringRedisTemplate.opsForValue().get("user:90");
    User user1 = gson.fromJson(sG, User.class);
    System.out.println("user1 = " + user1);
}
```

> 注意导入Gson依赖

即可实现内容，注意到如果我们存入的内容都是字符串的时候，我们可以直接调用封装好的`StringRedisTemplate`类来代替原本不太好用还需要自己配置序列化器的`RedisTemplate`，不过应该注意此时传入的数据参数都应为字符串

除开String类型的操作和Redis内置命令差不多相同之外，像是Hash类型，Set类型的命令在Spring data redis里面都有不同程度的改动，不过也是比较简单就能上手，稍微摸索一下即可

## 实际应用

在开始实际应用之前，我们得先把别人的项目导进来，顺便熟悉一下引入项目的步骤

1. 导入数据库，复制`.sql`文件内的SQL脚本到数据库可视化的脚本页面，直接粘贴执行即可，也可以在非可视化界面下`source xxx.sql`来引入文件（未尝试）

2. 导入java后端项目，直接在IDEA里面打开项目，接着点击`构建->构建项目`即可

3. 部署前端项目，这就坑了，docker里面的nginx和外面装的不太一样，遇上好多坑

   - `/etc/nginx`里面存放的是配置文件，这狗docker居然连`conf`目录都不愿意建一个，着实是坑了我一手，其中的`/etc/nginx/conf.d`专门存放的是server块的内容，因此我们不能直接把配置文件搞到`conf.d`中

   - 默认项目会去`html/xxx`里面找我们的页面，但是docker里面坑就坑在`html`目录居然在`/usr/share/nginx/html`里面，因此我们如果直接覆盖配置文件的话必须修改`root`位置

   - 总的docker指令如下`docker run --name project-nginx -v /home/chillyblaze/Documents/Development/Java/RedisLearning/nginx-1.18.0/conf:/etc/nginx -v /home/chillyblaze/Documents/Development/Java/RedisLearning/nginx-1.18.0/html:/usr/share/nginx/html -v /home/chillyblaze/Documents/Development/Java/RedisLearning/nginx-1.18.0/logs:/var/log/nginx -d nginx`

     千万注意配置文件和页面文件的存放位置

### 短信登录

#### 基于Session

总的流程如下，分别表示不同部分对于该短信登录的职责，我们要做的就是按照流程图的要求填充内容

![image-20220409212141208](../../.config/Typora/typora-user-images/image-20220409212141208.png)

##### 发送验证码

我们在前端输入手机号之后，点击发送验证码，就可以对后端发起一个AJAX请求`http://172.17.0.4:8080/api/user/code?phone=12345678910`，而后端也已经准备好了控制层来对请求到的内容进行处理

```java
@Slf4j
@RestController
@RequestMapping("/user")
public class UserController {

    @Resource
    private IUserService userService;

    @Resource
    private IUserInfoService userInfoService;

    @PostMapping("code")
    public Result sendCode(@RequestParam("phone") String phone, HttpSession session) {
        // TODO 发送短信验证码并保存验证码
        return Result.fail("功能未完成");
    }
}
```

接下来就不再粘贴模版代码内容，直接通过最终效果来展示代码内容

```java
@PostMapping("code")
public Result sendCode(@RequestParam("phone") String phone, HttpSession session) {
    // 发送短信验证码并在本地保存验证码
    return userService.sendCode(phone,session);
}
```

Controller将把内容交给Service层处理

```java
@Slf4j
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements IUserService {

    @Override
    public Result sendCode(String phone, HttpSession session) {
        // 1.校验手机号
        if (RegexUtils.isPhoneInvalid(phone)) {
            // 2.如果不符合，返回错误信息
            return Result.fail("手机号格式错误");
        }
        // 3.符合，返回验证码
        String code = RandomUtil.randomNumbers(6);
        // 4.保存验证码到session
        session.setAttribute("code",code);
        // 5.发送验证码
        log.debug("发送短信验证码成功，验证码：{}",code);
        // 6.返回ok
        return Result.ok();
    }
}
```

接下来我们在前端输入正确的手机号，点击发送验证码，就会看到控制台中打印出来了发送验证码成功的日志消息

![image-20220409214821629](https://s2.loli.net/2022/04/09/s6tjiXT18SA3fwR.png)

##### 登录和注册功能

当我们点击登录按钮之后，就会把我们的手机号和验证码传给后端，按照之前的流程所示进行验证即可

```java
@Override
public Result login(LoginFormDTO loginForm, HttpSession session) {
    // 1.校验手机号和验证码
    String phone = loginForm.getPhone();
    if (!phone.equals(session.getAttribute("phoneNum").toString())) {
        return Result.fail("更改了手机号，请重新获取验证码");
    }
    // 2.校验验证码
    if (!loginForm.getCode().equals(session.getAttribute("code").toString())) {  // 小技巧，用equal判断是否相等
        // 3.不一致，报错
        return Result.fail("验证码错误!");
    }
    // 4.根据手机号查询用户
    User user = lambdaQuery().eq(User::getPhone, phone).one();// 顺便复习了一下MybatisPlus

    // 5.判断用户是否存在
    if (user == null) {
        // 6.不存在，则创建新用户并保存
        user = creatUserWithPhone(phone);
    }
    // 7.保存用户信息到session中
    // 注意保存在Session中的内容不应该是用户的所有信息，不然有泄露的风险，因此此处我们需要创建并保存一个专门用于传输给前端的简化User信息
    // UserDTO userDTO = new UserDTO();
    // userDTO.setNickName(user.getNickName());
    // userDTO.setId(user.getId());  // 当然可以这样笨办法一个个设置，但是也可以善用工具类
    session.setAttribute("user", BeanUtil.copyProperties(user, UserDTO.class));
    return Result.ok();
}

private User creatUserWithPhone(String phone) {
    // 1.创建用户
    User user = new User();
    user.setPhone(phone);
    user.setNickName(USER_NICK_NAME_PREFIX + RandomUtil.randomString(10));
    // 2.保存用户
    save(user);
    return user;
}
```

> 如果报错，可能不是你的问题，选个高版本的MybatisPlus使用即可

##### 校验登录状态

由于当用户处于登录状态时，我们肯定不能让每一个Controller都去验证一下用户信息是否为登录状态，因此我们需要编写一个拦截器，在请求进入后端的时候直接判断用户登录状态，并且将用户的信息保存在共用的ThreadLocal中，以便后续Controller使用

因此我们需要自己编写一个拦截器，就写在`utils`里面即可

![image-20220410164131660](https://s2.loli.net/2022/04/10/XFIVz2G8mwZL6Qs.png)

```java
public class LoginInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        // 1.获取session
        HttpSession session = request.getSession();
        // 2.获取session中的用户
        UserDTO user = (UserDTO) session.getAttribute("user");
        // 3.判断用户是否存在
        if (user==null) {
            // 4.不存在拦截
            response.setStatus(401);
            return false;
        }
        // 5.存在，保存信息到ThreadLocal
        UserDTOHolder.saveUser(user);
        // 6.放行
        return true;
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        // 移除用户，避免内存泄露
        UserDTOHolder.removeUser();
    }
}
```

当然只有拦截器并没有什么卵用，所以我们还需要将拦截器注册到MVC环境中

```java
@Configuration
public class WebMVCConfigurer implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor()).excludePathPatterns(
                "/user/code",  // 白名单
                "/user/login",
                "/blog/hot",
                "/shop/**",
                "/shop-type/**",
                "/voucher/**",
                "/upload/**"
        );
    }
}
```

#### 基于Redis

Session共享问题导致一旦进行分布式部署的时候用户体验极差，因此我们需要借助Redis代替Session替我们缓存用户信息

但是Redis也有一定的问题，就是所有用户都会使用同一个Redis，而不是像Session一样每一个人的Session都不一样，因此设计一个可以分别存储每一个用户的Redis数据结构就比较重要，总的流程图如下

![image-20220410173015711](https://s2.loli.net/2022/04/10/fNVD3AHuBwKCcZI.png)

当然为了实现这个效果，还需要前端进行配合，我们可以在前端利用浏览器缓存和AJAX请求工具的拦截器功能，在浏览器缓存中时刻保存从后端返回过来的Token内容，并且在每次在往前端发送请求的时候都在请求头中加上`authorization`字段携带Token，以此使得后端总能接收到Token信息，并通过这个信息去Redis里面寻找数据内容

于是我们可以这样修改我们的代码

```java
@Slf4j
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements IUserService {

    @Resource
    private StringRedisTemplate stringRedisTemplate;

    @Override
    public Result sendCode(String phone, HttpSession session) {
        // 1.校验手机号
        if (RegexUtils.isPhoneInvalid(phone)) {
            // 2.如果不符合，返回错误信息
            return Result.fail("手机号格式错误");
        }
        // 3.符合，返回验证码
        String code = RandomUtil.randomNumbers(6);
        // 4.1保存验证码到session
        // session.setAttribute("code", code);
        // session.setAttribute("phoneNum", phone);
        // 4.2保存验证码到Redis
        stringRedisTemplate.opsForValue().set(LOGIN_CODE_KEY + phone, code, LOGIN_CODE_TTL, TimeUnit.MINUTES);  // 建议加一个前缀，标明这条数据是用来作为验证的，同时需要设置有效期
        // 5.发送验证码
        log.debug("发送短信验证码成功，验证码：{}", code);
        // 6.返回ok
        return Result.ok();
    }

    @Override
    public Result login(LoginFormDTO loginForm, HttpSession session) {
        // 1.校验手机号和验证码
        String phone = loginForm.getPhone();
        String cacheCode = stringRedisTemplate.opsForValue().get(LOGIN_CODE_KEY + phone);
        if (cacheCode == null) {
            return Result.fail("更改了手机号，请重新获取验证码");
        }

        // 2.校验验证码
        if (!cacheCode.equals(loginForm.getCode())) {
            // 3.不一致，报错
            return Result.fail("验证码错误!");
        }

        // 4.根据手机号查询用户
        User user = lambdaQuery().eq(User::getPhone, phone).one();// 顺便复习了一下MybatisPlus

        // 5.判断用户是否存在
        if (user == null) {
            // 6.不存在，则创建新用户并保存
            user = creatUserWithPhone(phone);
        }

        // 7.保存用户信息到Redis中
        // 7.1.随机生成Token，作为登录令牌
        String token = UUID.randomUUID().toString(true);
        // 7.2.将User对象转为Map便于接下来存储进Redis
        UserDTO userDTO = BeanUtil.copyProperties(user, UserDTO.class);
        Map<String, Object> userMap =
                BeanUtil.beanToMap(userDTO, new HashMap<>(), new CopyOptions()
                .setIgnoreNullValue(true)
                .setFieldValueEditor((a, b) -> b.toString()));  // 由于默认的字段id属性为Long，之后存入Redis的时候无法自动转换为String，因此我们要在这里手动通过自定义方式规定转换方式
        // 7.3.存储为Hash类型
        String tokenKey = LOGIN_USER_KEY + token;
        stringRedisTemplate.opsForHash().putAll(tokenKey, userMap);
        // 7.4.设置有效期，同时要满足只要用户不断的访问我，我的有效期就一直在（拦截器操作）
        stringRedisTemplate.expire(tokenKey, LOGIN_USER_TTL, TimeUnit.MINUTES);
        return Result.ok(token);
    }

    private User creatUserWithPhone(String phone) {
        // 1.创建用户
        User user = new User();
        user.setPhone(phone);
        user.setNickName(USER_NICK_NAME_PREFIX + RandomUtil.randomString(10));
        // 2.保存用户
        save(user);
        return user;
    }
}
```

```java
public class LoginInterceptor implements HandlerInterceptor {

    // 这个类是我们手动创建的，因此我们不能通过AutoWired注入，然后我们从创建这个类的地方引入所需内容
    private final StringRedisTemplate stringRedisTemplate;

    public LoginInterceptor(StringRedisTemplate stringRedisTemplate) {
        this.stringRedisTemplate = stringRedisTemplate;
    }

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        // 1.获取请求头中的token
        String token = request.getHeader("authorization");
        if (StrUtil.isBlank(token)) {
            response.setStatus(401);
            return false;
        }
        // 2.获取Redis中的用户
        String tokenKey = LOGIN_USER_KEY + token;
        Map<Object, Object> userMap = stringRedisTemplate.opsForHash().entries(tokenKey);
        if (userMap.isEmpty()) {
            response.setStatus(401);
            return false;
        }
        // 3.将Hash数据转换为UserDTO对象
        UserDTO userDTO = BeanUtil.fillBeanWithMap(userMap, new UserDTO(), false);
        // 4.存在，保存信息到ThreadLocal
        UserDTOHolder.saveUser(userDTO);
        // 5.修改用户登录时间
        stringRedisTemplate.expire(tokenKey,LOGIN_USER_TTL, TimeUnit.MINUTES);
        // 6.放行
        return true;
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        // 移除用户，避免内存泄露
        UserDTOHolder.removeUser();
    }
}
```

就可以运行了

但是还是会存在一点问题，就是当用户访问不需要进行用户验证的页面时，同样还是会不刷新token信息，从而一段时间后token失效的情况

为了避免这种情况，我们可以再加一层拦截器`RefreshTokenInterceptor`

虽然叫拦截器，但是里面并没有进行拦截，只是单纯的做了一个刷新ttl的操作

之后在拦截器注册类中进行注册

```java
@Configuration
public class WebMVCConfigurer implements WebMvcConfigurer {

    @Resource
    private StringRedisTemplate stringRedisTemplate;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new RefreshTokenInterceptor(stringRedisTemplate));
        registry.addInterceptor(new LoginInterceptor()).excludePathPatterns(
                "/user/code",
                "/user/login",
                "/blog/hot",
                "/shop/**",
                "/shop-type/**",
                "/voucher/**",
                "/upload/**"
        ).order(1);  // order值越大，优先级越低，如果不指定，就按照注册顺序来
    }
}
```

### 商户缓存

  我们知道，一旦我们打开一些商户内容，那么里面的内容是十分复杂的，一旦我们对其反复访问，就会给数据库造成很大的负担，因此我们需要对重复商户的查询放在Redis缓存中，不仅查询速度加快了，访问效率也会变高

```java
@Service
public class ShopServiceImpl extends ServiceImpl<ShopMapper, Shop> implements IShopService {

    @Resource
    private StringRedisTemplate stringRedisTemplate;

    @Override
    public Result queryById(Long id) {
        // 1.尝试从Redis查询缓存
        String key = CACHE_SHOP_KEY + id;
        String shopJson = stringRedisTemplate.opsForValue().get(key);
        if (StrUtil.isNotBlank(shopJson)) {
            Shop shop = JSONUtil.toBean(shopJson, Shop.class);
            return Result.ok(shop);
        }
        // 2.不存在，查询数据库
        Shop shop = getById(id);
        // 3.数据库也不存在，返回错误
        if (ObjectUtil.isNull(shop)) {
            return Result.fail("店铺不存在");
        }
        // 4.数据库存在，写入Redis
        stringRedisTemplate.opsForValue().set(key,JSONUtil.toJsonStr(shop));
        // 5.返回
        return Result.ok(shop);
    }
}
```

可以看出在上面的基础上还是比较简单的

#### 缓存更新策略

我们知道，商户的信息是不会一直都是不变的，指不定某一天商户就调整了自己的商品信息，这样就会使缓存内和数据库中的内容不一致，此时我们就需要制定策略更新缓存

- 内存淘汰，不需要自己维护，当系统内存被占满的时候Redis会自动清除部分数据
- 超时剔除，在添加数据的时候指定缓存超时时间，到时直接删除
- 主动更新，编写业务逻辑，当我们修改数据库的同时更新缓存

其中由于主动更新比较复杂，因此其中还细分为三种不同的方式

- `Cache Aside Pattern`当我们更新数据库的时候，手动编写策略去修改缓存内容
- `Read/Write Through Pattern`将缓存和数据库整合为一个服务，我们调用该服务更新数据库，不用管缓存一致性问题
- `Write Behind Caching Pattern`直接修改缓存内容，由某一个线程定时将我们修改的内容持久化到数据库，但是可能修改数据会丢失

第二种看上去不错，但是目前暂时没有高可复用的解决方案，一般要实现还是得手撸，相对还是比较麻烦的，因此一般我们都使用第一种方式，同时当数据库中一旦被修改了，我们直接把缓存给删了，被迫让下一次查询直接去查询数据库

但是究竟是先删缓存还是先修改数据库呢，在多线程并发状态下，不同的选择会引起不同的结果

![image-20220410214824538](https://s2.loli.net/2022/04/10/qH75nG1JoiUxWK3.png)

根据这种分析，我们需要先操作数据库再操作缓存，同时也需要给缓存设置一个超时时间，以便真的发生第二种情况时能够减少影响时间

同时为了保证缓存与数据库的操作同时成功或失败，我们还可以采用TCC分布式事务方案，此处涉及到分布式的知识因此暂且不表

加超时时间很简单，而同时删除相对来说比较复杂

#### 实践

我们直接添加Service方法，虽然一通分析猛如虎，但是实际操作起来十分简单

```java
@Override
@Transactional  // 由于是单体操作，可以直接添加事务支持，如果涉及分布式，则可以使用TTC等
public Result syncUpdate(Shop shop) {
    Long id = shop.getId();
    if (id==null) {
        return Result.fail("ID不能为空");
    }
    // 更新数据库
    updateById(shop);
    // 删除缓存
    stringRedisTemplate.delete(CACHE_SHOP_KEY + id);
    return Result.ok();
}
```

接着我们通过postman给我们的服务器发一条修改消息

```json
{
    "id": 1,
    "name": "101茶餐厅",
    "typeId": 1,
    "area": "大关",
    "address": "金华路锦昌文华苑100号",
    "avgPrice": 80,
    "comments": 3035,
    "score": 37,
    "openHours": "10:00-22:00"
}
```

![image-20220411200115036](https://s2.loli.net/2022/04/11/8WS4xAOMtGQ1ynI.png)

第一次使用这么高端的东西，还是有以上几个点需要注意一下

#### 缓存穿透

上面的方法会存在一些问题，比如某个不怀好意的黑客自己构建了一个payload，人为传给我们后端，但是它所请求的ID并不存在，于是乎缓存中找不到自然就跑去数据库找了，但是坏就坏在数据库也找不到，于是给前端返回了一个错误，然而黑客却不善罢甘休，直接狂发错误请求，于是每一次请求都会穿透到数据库，从而给数据库造成很大的负担，甚至会直接把数据库搞坏，这就是缓存穿透

一般来说为了避免这种情况，我们也有很多对策

- 缓存空对象，一旦发了一个错误的请求给我，那么我数据库就返回给Redis一个空对象比较短TTL的缓存，使得下一次请求的时候仿佛Redis里面有数据，但是实际上是空的，还是会返回错误，这种方式比较简单，但是会产生额外的内存消耗，同时也可能会出现数据的不一致性
- 布隆过滤，在Redis和用户之间再加一层过滤器，其中存储了数据库中每一条数据的比如Hash值，用户请求过来的时候和请求的Hash值进行比对，如果不存在就直接返回错误，拒绝访问Redis

但是这些方式都比较被动，其他主动的方式还有增增强id的复杂度，在后端进行校验，对不合规范的id直接返回错误等等

当然这些都是比较温和的解决方式，正确的防止此类事件解决方式就是直接给他妈ip给封了，居然给我发错误请求，胆挺肥啊

#### 缓存雪崩

缓存雪崩就是同一段时间突然Redis大量缓存key同时失效，或者Redis服务突然宕机，此时就会导致大量请求到达数据库，从而带来巨大压力

第一种情况看上去似乎发生概率比较小，但是当我们启动一个服务的时候往往要进行缓存预热，也就是将数据库的数据提前导入到缓存中，此时如果TTL设置的是一样的话，到某一个时间突然全部挂了就直接完蛋，对于这种情况，我们可以通过给不同Key添加随机值的方式来解决

而对于第二种情况，就需要Redis集群服务了，或者给缓存业务添加降级限流策略，又或者给业务添加多级缓存（浏览器本地缓存，Nginx缓存等等在每一层都缓存一次就行）

#### 缓存击穿

缓存击穿就是对于某些热点Key（比如某促销商品）突然某一个时间点挂掉了，这时候刚挂掉就有一大堆请求发过来想买这个促销商品，这时候就会有一大堆请求打到数据库，同样有可能把数据库搞坏了

对于这种情况，常见的也有两种方式解决

- 互斥锁，在查询缓存未命中的时候该用户获得一把锁，并请求数据库进行写入缓存，这时候如果有别的请求过来，获得不了这把锁了，于是我们命令它休眠一会再试试，直到缓存重新加载，第一个用户还回了锁，后面被阻塞的进程才被放行

  但是也有一些问题，就是在其他用户被阻塞的时候耽误了大量时间，影响用户的体验，更可怕的是可能还会出现死锁问题

- 逻辑过期，为存入缓存的数据添加一个逻辑过期值而不设置TTL，当请求发过来的时候先比对数据中逻辑过期值是否过期，如果过期了就提醒一声数据库要缓存了，但是返回的还是原来逻辑已经过期了的数据，而与此同时就开启另一个线程拿到一把锁去重写缓存，这过程中所有来访问这条数据的用户在重写缓存成功之前都拿到老数据即可，这种方式就不像上一个方法一样用户需要等待了

这两个方案体现了解决方案的可用性和一致性的矛盾，这种矛盾也是接下来我们会经常碰到的

可以发现这两种方式都需要设置锁，而这个互斥锁应该怎么设置也是一个问题，此时我们可以利用Redis的`setnx`指令，这个指令只会对第一个执行该指令的用户设置内容，后面无论设置多少次都只会返回0即设置失败，通过它我们就可以避免在Java代码中写一大堆自自定义锁的代码

![image-20220411212934046](https://s2.loli.net/2022/04/11/sa3G2ULmVCAdKOr.png)

这时候就可以编写代码实现了

##### 互斥锁方式实现

```java
public Shop queryWithMutex(Long id){
    String lockKey = null;
    Shop shop = null;
    lockKey = LOCK_SHOP_KEY + id;
    try {
        // 尝试从Redis查询缓存
        String key = CACHE_SHOP_KEY + id;
        String shopJson = stringRedisTemplate.opsForValue().get(key);
        if (StrUtil.isNotBlank(shopJson)) {
            return (Shop) JSONUtil.toBean(shopJson, Shop.class);
        }
        // 判断命中的是否为空值
        if (shopJson != null) {
            return null;
        }
        // 实现缓存重建
        // 获取互斥锁
        boolean isLock = tryLock(lockKey);
        // 判断是否获取成功
        if (!isLock) {
            // 失败，则休眠并重试
            Thread.sleep(50);
            return queryWithMutex(id);  // 递归调用，从头开始判断
        }
        // 成功，根据id查询数据库
        shop = getById(id);
        Thread.sleep(200);
        // 数据库也不存在，返回错误
        if (ObjectUtil.isNull(shop)) {
            // 将空值写入Redis
            stringRedisTemplate.opsForValue().set(key,"",CACHE_NULL_TTL,TimeUnit.MINUTES);
            return null;
        }
        // 4.数据库存在，写入Redis
        stringRedisTemplate.opsForValue().set(key,JSONUtil.toJsonStr(shop),CACHE_SHOP_TTL, TimeUnit.MINUTES);
    } catch (InterruptedException e) {
        throw new RuntimeException(e);
    } finally {
        // 释放互斥锁
        unlock(lockKey);
    }
    // 返回
    return shop;
}
```

测试时，我们只需要在查询数据库之前添加一个延时，就可以模拟实际情况了

然后我们使用专业的压力测试工具Apache Jmeter

1. 先添加一个线程组，在里面这样设置![image-20220411223646314](https://s2.loli.net/2022/04/11/w3bAN2dJYipn7Hj.png)

2. 添加一个HTTP请求，在里面这样设置![image-20220411223838396](https://s2.loli.net/2022/04/11/8eK95BanU417loQ.png)

3. 添加一个监听器，这么设置![image-20220411223925066](https://s2.loli.net/2022/04/11/19SpKi6kENOgfFM.png)

4. 最后样子

   ![image-20220411224009747](https://s2.loli.net/2022/04/11/3zZIyiUkLnsvOB7.png)

5. 开始发送请求，冲冲冲，右上角会实时显示目前发送的线程堵塞的情况和完成情况

6. 最后展示图表如下，可以根据自己要求进行配置

   ![image-20220411224700462](../../.config/Typora/typora-user-images/image-20220411224700462.png)

##### 逻辑过期解决

设置逻辑过期内容，就需要在存入Redis的时候添加字段，于是如何添加这个字段就成了一个问题，于是我们可以设置一个专门用于存储缓存数据的实体类，进一步封装从数据库中查到的内容，在解耦合的同时也进一步提高的复用性

```java
@Data
public class RedisData {
    private LocalDateTime expireTime;
    private Object data;
}
```

接下来我们配置一个测试类测试一下，同时也是模拟今后后台系统的方式，在服务启动的时候先预先将热点数据通过后台存入缓存中，为了使用户进行首次访问的时候就直接命中缓存

```java
public void saveShop2Redis(Long id, Long expireSeconds) {
    // 查询店铺数据
    Shop shop = getById(id);
    // 封装逻辑过期时间
    RedisData redisData = new RedisData();
    redisData.setData(shop);
    redisData.setExpireTime(LocalDateTime.now().plusSeconds(expireSeconds));
    // 写入Redis
    stringRedisTemplate.opsForValue().set(CACHE_SHOP_KEY + id, JSONUtil.toJsonStr(redisData));
}
```

 此时数据库中就有了我们的数据了，新添加的`expireTime`属性规定了过期时间

```java
// 开启一个线程池
private static final ExecutorService CACHE_REBUILD_EXECUTOR = Executors.newFixedThreadPool(10);

public Shop queryWithLogicalExpire(Long id) {
    // 1.尝试从Redis查询缓存
    String key = CACHE_SHOP_KEY + id;
    String shopJson = stringRedisTemplate.opsForValue().get(key);
    if (StrUtil.isBlank(shopJson)) {
        // 返回为空，说明不存在
        if (shopJson !=null) {
            return null;
        }
        // 查询数据库
        Shop shop = getById(id);
        // 数据库也不存在，返回错误
        if (ObjectUtil.isNull(shop)) {
            // 将空值写入Redis
            stringRedisTemplate.opsForValue().set(key, "", CACHE_NULL_TTL, TimeUnit.MINUTES);
            return null;
        }
        // 数据库存在，写入Redis
        stringRedisTemplate.opsForValue().set(key, JSONUtil.toJsonStr(shop), CACHE_SHOP_TTL, TimeUnit.MINUTES);
        // 返回
        return shop;
    }
    // 返回不为空
    // 先将json反序列化为对象
    RedisData redisData = JSONUtil.toBean(shopJson, RedisData.class);
    Shop shop = JSONUtil.toBean((JSONObject) redisData.getData(), Shop.class);
    LocalDateTime expireTime = redisData.getExpireTime();
    // 判断是否过期
    if (expireTime.isAfter(LocalDateTime.now())) {
        // 未过期，直接返回店铺信息
        return shop;
    }
    // 过期，需要缓存重建
    // 获取互斥锁
    String lockKey = LOCK_SHOP_KEY + id;
    boolean isLock = tryLock(lockKey);
    // 判断是否获取锁成功
    if (isLock) {
        // 成功，开启独立线程，实现缓存重建，开启线程池做
        CACHE_REBUILD_EXECUTOR.submit(() -> {
            try {
                saveShop2Redis(id, 10L);
            } catch (Exception e) {
                throw new RuntimeException(e);
            } finally {
                // 一定要记得释放锁，同时保证释放的过程不被某些Runtime异常给错过
                unlock(lockKey);
            }
        });
    }
    // 返回过期的商铺信息
    return shop;
}
```

这样我们的逻辑过期的情况也实现解决了

##### 缓存工具封装

今后如此繁琐的代码我们肯定不会每次都写这么麻烦的程序，因此我们会将其封装成一个个缓存工具，但是在封装的过程中也会出现一些问题，比如说万恶的泛型和函数式编程

以下是花了将近两个小时搞的工具类，我对前途充满了绝望，这么简单的东西也要搞这么久，还是对着案例做的，我是个废物

```java
@Component
public class CacheProblemSolve {

    @Resource
    private StringRedisTemplate stringRedisTemplate;

    public void saveByTTL(String key, Object value, Long time, TimeUnit unit) {
        String jsonValue = JSONUtil.toJsonStr(value);
        stringRedisTemplate.opsForValue().set(key, jsonValue, time, unit);
    }

    public void saveByLogical(String key, Object value, Long time, TimeUnit unit) {
        RedisData redisData = new RedisData();
        redisData.setData(value);
        redisData.setExpireTime(LocalDateTime.now().plusSeconds(unit.toSeconds(time)));
        String jsonRedisData = JSONUtil.toJsonStr(redisData);
        stringRedisTemplate.opsForValue().set(key, jsonRedisData);
    }

    public void saveByNull(String key) {
        stringRedisTemplate.opsForValue().set(key, "", CACHE_NULL_TTL, TimeUnit.MINUTES);
    }

    // 缓存穿透预防，防止无效请求过度打到数据库
    public <O, ID> O queryWithPassThrough(String prefix,
                                          ID id,
                                          Class<O> type,
                                          Function<ID, O> dataBaseMethod,
                                          Long timeY,
                                          TimeUnit unitY) {
        // 尝试从Redis查询缓存
        String key = prefix + id;
        String objectJson = stringRedisTemplate.opsForValue().get(key);
        if (StrUtil.isNotBlank(objectJson)) {
            return JSONUtil.toBean(objectJson, type);
        }
        // 判断命中的是否为空值
        if (objectJson != null) {
            return null;
        }

        // 不存在，查询数据库
        O object = dataBaseMethod.apply(id);  // 调用apply方法
        // 数据库也不存在，返回错误
        if (ObjectUtil.isNull(object)) {
            // 将空值写入Redis
            saveByNull(key);
            return null;
        }
        // 数据库存在，写入Redis
        saveByTTL(key, object, timeY, unitY);
        // 返回
        return object;
    }

    // 开启一个线程池
    private static final ExecutorService CACHE_REBUILD_EXECUTOR = Executors.newFixedThreadPool(10);

    // 缓存击穿预防，防止热点数据缓存超时段时间大量请求打到数据库，逻辑过期
    public <O, ID> O queryWithLogicalExpire(String prefixID,
                                            String prefixLock,
                                            ID id,
                                            Class<O> type,
                                            Function<ID, O> dataBaseMethod,
                                            Long overDueTime,
                                            TimeUnit unit) {
        // 1.尝试从Redis查询缓存
        String key = prefixID + id;
        String objectJson = stringRedisTemplate.opsForValue().get(key);
        if (StrUtil.isBlank(objectJson)) {
            // 返回为空，说明不存在，存入第一次数据
            if (objectJson != null) {
                return null;
            }
            O object = dataBaseMethod.apply(id);
            saveByLogical(key, object, overDueTime, unit);
            return object;
        }
        // 返回不为空
        // 先将json反序列化为对象
        RedisData redisData = JSONUtil.toBean(objectJson, RedisData.class);
        O object = JSONUtil.toBean((JSONObject) redisData.getData(), type);
        LocalDateTime expireTime = redisData.getExpireTime();
        // 检查逻辑过期时间，判断是否过期
        if (expireTime.isAfter(LocalDateTime.now())) {
            // 未过期，直接返回对象
            return object;
        }
        // 过期，需要缓存重建
        // 获取互斥锁
        String lockKey = prefixLock + id;
        boolean isLock = tryLock(lockKey);
        // 判断是否获取锁成功
        if (isLock) {
            // 成功，开启独立线程，实现缓存重建，开启线程池做
            CACHE_REBUILD_EXECUTOR.submit(() -> {
                try {
                    O databaseObject = dataBaseMethod.apply(id);
                    saveByLogical(key, databaseObject, overDueTime, unit);
                } catch (Exception e) {
                    throw new RuntimeException(e);
                } finally {
                    // 一定要记得释放锁，同时保证释放的过程不被某些Runtime异常给错过
                    unlock(lockKey);
                }
            });
        }
        // 返回过期的商铺信息
        return object;
    }

    public <O, ID> O queryWithMutex(String prefixID,
                                    String prefixLock,
                                    ID id,
                                    Class<O> type,
                                    Function<ID, O> dataBaseMethod,
                                    Long time,
                                    TimeUnit unit) {
        String lockKey = prefixLock + id;
        try {
            // 尝试从Redis查询缓存
            String key = prefixID + id;
            String objectJson = stringRedisTemplate.opsForValue().get(key);
            if (StrUtil.isNotBlank(objectJson)) {
                return JSONUtil.toBean(objectJson, type);
            }
            // 判断命中的是否为空值
            if (objectJson != null) {
                return null;
            }
            // 实现缓存重建
            // 获取互斥锁
            boolean isLock = tryLock(lockKey);
            // 判断是否获取成功
            if (!isLock) {
                // 失败，则休眠并重试
                Thread.sleep(50);
                while (StrUtil.isBlank(stringRedisTemplate.opsForValue().get(key))) {
                    Thread.sleep(50);
                }
                ;
                return JSONUtil.toBean(stringRedisTemplate.opsForValue().get(key), type);  // 递归调用，从头开始判断
            }
            // 成功，根据id查询数据库
            O object = dataBaseMethod.apply(id);
            Thread.sleep(200);
            // 数据库也不存在，返回错误
            if (ObjectUtil.isNull(object)) {
                // 将空值写入Redis
                saveByNull(key);
                return null;
            }
            // 4.数据库存在，写入Redis
            saveByTTL(key, object, time, unit);
            return object;
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        } finally {
            // 释放互斥锁
            unlock(lockKey);
        }
        // 返回
    }

    public void deleteByKey(String key) {
        stringRedisTemplate.delete(key);
    }

    private boolean tryLock(String key) {
        Boolean flag = stringRedisTemplate.opsForValue().setIfAbsent(key, "1", 10, TimeUnit.SECONDS);
        return BooleanUtil.isTrue(flag);  // 注意此处最好不要直接返回，Java会自动拆箱，可能会返回空指针（比如连接不上redis，此时flag就为空）
    }

    private void unlock(String key) {
        stringRedisTemplate.delete(key);
    }

}
```

虽然不复杂，但也不简单，属于是已经让我有点晕了，未来写大项目代码该怎么办那

### 优惠券秒杀

