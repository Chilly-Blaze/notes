# Nginx

## 背景

Nginx （engine x）是一个开源、高性能的 HTTP 和反向代理 Web 服务器，同时也提供了 IMAP/POP3/SMTP 服务

> 正向代理：我们知道我们要请求的服务器内容，接着我们带着我们知道的请求服务器信息先给代理服务器，代理服务器根据我们传给他的内容代理我们发送请求
>
> 反向代理：我们不知道服务器的详细信息，但是我们知道某个代理服务器的地址，我们直接将请求发送给代理服务器，由代理服务器读取请求并选择他管理下的合适服务器执行我们的要求，从而达到负载均衡的目的

1. 速度更快，并发更高(epoll函数解决高并发)

2. 配置简单，扩展性强

3. 高可靠性

4. 热部署

5. 成本低，BSD许可证（我们可以免费商用并盈利，更可以直接对其源码进行修改并成为自己的项目）

   > 各种开源许可证一览：
   >
   > ![See the source image](https://tse1-mm.cn.bing.net/th/id/R-C.c06456a0fe2f8e911401cd66d0096a2c?rik=8De0vQ8YPiObSw&riu=http%3a%2f%2fwww.vip1993.com%2fuploads%2fallimg%2f200628%2f1-20062Q34453R1.jpg&ehk=LRjjO31gtVjjUCEEK8%2bhrAPzdumv8%2f4YJRsUmommrKs%3d&risl=&pid=ImgRaw&r=0)

   由于这个特性，衍生出了许多拓展nginx版本，比如OpenRestry（Nginx+Lua）等

下面的演示内容均在Docker中的Centos系统进行演示执行，其它系统类似

## 安装/卸载

### 通过源码安装

1. 环境准备

   - 由于Nginx是由C语言编写的，因此我们需要先安装一个GCC编译器
   - Nginx编译过程中需要用到PCRE（正则表达式）库，也得安装这个库
   - 除此之外还需要压缩算法库zlib和安全通信包OpenSSL
   - `yum install -y gcc pcre pcre-devel zlib zlib-devel openssl openssl-devel`安装
   - 安装检查可以通过`rpm -qa [包名]`来查看

2. 下载源码，我们可以通过`https://nginx.org/en/download.html`复制源码链接，接着在终端中`wget https://nginx.org/download/nginx-1.20.2.tar.gz`即可

   ![image-20220130132357064](https://s2.loli.net/2022/01/30/xoNyLhSQl9fWJqt.png)

3. 解压内容，执行内部的configure文件

   ​	![image-20220130133319457](https://s2.loli.net/2022/01/30/HUGiJKIedxWCaB6.png)

4. 编译内容`make && make install`即可

5. 完成之后我们进入`/usr/local/nginx/sbin`里面执行一下`./nginx`即可直接启动nginx

6. 接着通过`ip addr`查看一下docker内部的ip地址，在外部直接访问ip即可

   ![image-20220130134453566](https://s2.loli.net/2022/01/30/etA43hOgTlfPC7H.png)

### yum安装

上述的方法显然十分不方便，所以我们可以直接通过yum一步到位

1. 先查看`https://nginx.org/en/linux_packages.html`内部提供的用于安装的方式（通过Document一项进入），跟着步骤一步步来即可

   ![image-20220130135311713](https://s2.loli.net/2022/01/30/NJdX7TliMbjrSIG.png)

   > 上面的步骤事实上就是引入了一个yum库，不然直接`yum install nginx`可能会找不到内容

2. 通过`whereis nginx`找到安装到哪里去了

3. 选择一个在`sbin`目录下的文件，执行即可（或者直接nginx也可以执行）

![image-20220130140343549](https://s2.loli.net/2022/01/30/tLHI1siC9M4Rqjv.png)

> 发现和之前的界面不太一样了哦

我们可以比对一下两种方式安装之后的版本信息（`nginx -V`）可以发现两种安装方式的区别是很大的

- 源码安装

  ![image-20220130141610198](https://s2.loli.net/2022/01/30/HDdeBTs3noUqv6Y.png)

- yum安装

  ![image-20220130141705013](https://s2.loli.net/2022/01/30/drlsaL7TFEUZPt6.png)

可以明显发现，肯定是我们源码安装的过程中比起直接安装还是漏了许多东西的

### 编译参数

首先我们先了解一下源码安装的时候各个目录之间的关系

![image-20220130162509183](https://s2.loli.net/2022/01/30/nxRgqKGLWHjZlNE.png)

我们发现在通过源码进行安装的时候，我们似乎只运行了一下`configure`这个文件，这就说明，如果我们需要像如同yum安装那样多那么多参数，那么势必需要在执行`configure`的时候告诉电脑我的想法才行

我们可以通过`--help`来查看如何添加参数

![image-20220130181039452](https://s2.loli.net/2022/01/30/YIf6A2bkhtRBpOE.png)

在yum安装中冒出来的每一个参数/属性，我们都可以跟上面的对应起来，也就是说，我们进行编译时，只需要添加上这些参数，就可以手动模拟通过yum安装的效果了

当然要自己加参数，首先我们还是要了解一些这些参数的作用

- `--with`开头的往往是为Nginx添加某个模块，相反`--without`就是编译时排除某些模块
- `--prefix=PATH`Nginx安装路径。如果没有指定，默认为 `/usr/local/nginx`
- `--sbin-path=PATH`Nginx可执行文件安装路径。只能安装时指定，如果没有指定，默认为`<prefix>/sbin/nginx`（这的prefix就是指上边指定的）
- `--conf-path=PATH `，配置文件，默认为`<prefix>/conf/nginx.conf`
- `--error-log-path=<path>`在nginx.conf中没有指定error_log指令的情况下，默认的错误日志的路径，默认为 `<prefix>/logs/error.log`
- `--http-log-path=<path>`在nginx.conf中没有指定access_log指令的情况下，默认的访问日志的路径，默认为 `<prefix>/logs/access.log`
- 其他都于此类似，`--help`指令之后也有详细说明

综上，我们可以发现比起无脑yum安装，还是手动指定参数更加让人放心，当然这也意味着学习成本的扩大

### 卸载

想要自己通过参数方式编译，我们就需要对上一次安装的程序进行卸载

1. 停止nginx服务（`./nginx -s stop`）
2. 删除nginx主文件夹（`rm -rf nginx/`）
3. 清理编译内容（`make clean`）

![image-20220130184057422](https://s2.loli.net/2022/01/30/BEC1X4V3kcvxMNT.png)

## 目录结构

![image-20220130185810929](https://s2.loli.net/2022/01/30/tDpOAfi1FT6G4Sr.png)

## 服务器起停

### 信号控制

Nginx默认是采用多进程的方式来工作的，当Nginx启动之后，后台进程中会包含一个master进程和若干个worker进程

其中master进程用于管理worker进程，包含接收外界的信息，并将接收到的信号发送给各个worker进程，监控worker进程的状态，当worker进程出现异常退出时，会自动重新启动新的worker进程

而worker进程专门处理用户请求，各个worker进程平等且独立

我们可以通过`ps -ef | grep nginx`查看nginx启动的进程相关情况

![image-20220205184757887](https://s2.loli.net/2022/02/05/CKnlTMkovQDYsFI.png)

其中master进程和worker进程的关系如下

![img](https://www.baiyp.ren/images/nginx/nginx13.png)

因此，我们想要停止Nginx进程，只需要告诉master进程即可

1. 获取master进程pid

   - `ps -ef | grep nginx`查看
   - `cat /usr/local/nginx/logs/nginx.pid`查看

2. 关闭进程`kill -signal PID`，给出指令的同时我我们也要指定信号signal

   - `TERM/INT`立即关闭整个服务

   - `QUIT`所有请求结束之后关闭整个服务

   - `HUP`重读配置文件并使用服务对新配置项生效

   - `USR1`重新打开日志文件，用于日志切割

   - `USR2`平滑升级到最新版Nginx

     > 升级之后会在目录下生成`nginx.pid.oldbin`文件，当确认新Nginx正确启动之后，我们还需要`kill -QUIT pid.old`，关闭旧的服务

   - `WINCH`所有子进程不再接收处理新连接，相当于给worker进程发送`QUIT`

   ![image-20220205214535041](https://s2.loli.net/2022/02/05/PJnEXZ61SaGut4f.png)

### 二进制文件控制

除了上述通过手动删除进程停止Nginx服务，我们还可以通过启动文件来停止

转到`/usr/local/nginx/sbin`下，通过`./nginx -h`查看帮助内容

- `-t`检查当前配置文件语法信息（`/usr/local/nginx/conf/nginx.conf`）是否符合规范
- `-s`信号控制
  - `stop`相当于`TERM/INT`
  - `quit`相当于`QUIT`
  - `reopen`相当于`USR1`
  - `reload`相当于`HUP`
- `-c`指定配置文件的位置

### 版本迭代

当新的Nginx版本发布之后，我们如果想平滑升级服务器，或者是我们如果想要在原有的服务中添加其他模块，由于Nginx的可热部署性，我们可以在改动少量文件的基础上进行快速的平滑升级

1. 同样`wget`下载最新的压缩包，以同样的参数运行`./configure`和`make`，注意不需要进行`make install`

2. 备份`/usr/local/nginx/sbin`下的二进制文件

3. 将安装目录下的`objs`内的`nginx`二进制文件拷贝到`/usr/local/nginx/sbin`，并在原目录下直接运行`make upgrade`即可

   > 如果不想用`make upgrade`，那么就需要通过`USR2`重启服务，并通过`QUIT`平滑删除原进程

### 配置系统服务

通过源码安装程序时，我们都需要在目录下通过手动执行二进制文件来开启Nginx，事实上我们可以通过将其配置为系统服务从而在任意地方一键开启服务

1. 在`/usr/lib/systemd/system/nginx.service`目录下添加`nginx.service`并添加内容

   ```
   [Unit]
   Description=nginx web service
   Documentation=http://nginx.org/en/docs/
   After=network.target
   
   [Service]
   Type=forking
   PIDfile=/usr/local/nginx/logs/nginx.pid
   ExecStartPre=/usr/local/nginx/sbin/nginx -t -c /usr/local/nginx/conf/nginx.conf
   ExecStart=/usr/local/nginx/sbin/nginx
   ExecReload=/usr/local/nginx/sbin/nginx -s reload
   ExecStop=/usr/local/nginx/sbin/nginx -s stop
   PrivateTmp=true
   
   [Install]
   WantedBy=default.target
   ```

2. 修改权限为`755`

3. 测试是否成功（`systemctl start nginx`）

   > 注意到docker内无法使用systemctl这个指令

## 配置文件概述

![image-20220205223344953](https://s2.loli.net/2022/02/05/cK18MZu3lLJ64TW.png)

### 全局块

#### user指令

通过`user user [usergroup]`来指定**worker进程**的用户和用户组，如果不指定`usergroup`则默认使用user名作为组名称，如果不设置用户名则默认使用`nobody`

注意添加的用户应该是本机中存在的用户，如果乱输入用户名会使得`./nginx -t`检查失败

将`user`修改为root后：

![image-20220205224141497](https://s2.loli.net/2022/02/05/kjbLTlnfMv4OhuD.png)

更改`user`信息之后，指定的worker进程就无法访问不属于他权限之内的内容，从而可以避免服务器被入侵

#### work process指令

其中包含两条指令：

1. `master_process [on/off]`控制是否开启worker进程，默认`on`，如果设成`off`再启动会发现进程中的worker进程不见了
2. `worker_processes [num]`用于控制Nginx服务器实现并发处理的量，默认为1，建议和服务器CPU内核数保持一致

注意以上两个命令的修改之后我们都不能直接使用`reload`来重启Nginx服务，必须`stop`之后重新启动才能生效

#### 其他指令

- `deamon [on/off]`使用守护进程启动，默认为`on`，改成`off`之后我们启动Nginx之后当前启动控制台就不能关闭，一关闭Nginx也跟着关掉了
- `pid [path]`配置pid的存储路径
- `error_log [path] [level]`错误日志存放路径，其中的`[level]`项可以设置日志级别，从低到高分别是`debug|info|notice|warn|error|crit|alert|emerg`，设置太低的话会影响磁盘性能，它也不止只能配置在全局块中，默认为`crit`
- `include [path]`用于引入其他配置文件

### events块

这个块是用来设定Nginx服务器与用户之间的网络连接

- `accept_mutex [on/off]`主要用来设置Nginx网络连接序列化，默认为`on`，当Nginx没有收到用户请求时，默认所有的worker进程都是休眠状态，当某一个用户请求到来时，如果把这个值设为`off`，那么所有的worker进程就会被同时唤醒竞争这个请求的所有权，造成惊群效应，而如果设置为`on`那么每次都会只激活一个worker进程处理请求，增强了Nginx的整体性能，然而如果用户请求过于频繁（网站一下子接收大量请求），一个个激活worker进程反而会影响连接速度，因此需根据自身服务器或网站情况进行设置
- `multi_accept [on/off]`改成`on`之后一个worker进程就只能接收一个用户请求了（默认`off`，建议不修改）
- `aorker_connections [num]`用来配置单个worker进程的最大用户连接数
- `use [method]`用于指定Nginx服务器选择哪种事件驱动来处理网络消息，其中`method`有`select/poll/epoll/kqueue`等，建议设为`epoll`采用io多路复用的方式，后面也会涉及

### Http块

#### 定义MIME-Type

这个MIME-Type定义了用户请求的网络资源的媒体类型，作为web服务器必须识别前端请求的资源类型，来做出相应的MIME-Type响应

> 浏览器通常使用MIME类型（而不是文件扩展名）来确定如何处理URL，因此Web服务器在响应头中添加正确的MIME类型非常重要。如果配置不正确，浏览器可能会曲解文件内容，网站将无法正常工作，并且下载的文件也会被错误处理。

Nginx配置文件中默认有这两行配置

```
include mime-types;
default_type application/octet_stream
```

它代表着我们通过Nginx直接返回的内容如果没有指定返回类型那么默认采用文件的方式传输内容，即访问某个内容时返回在用户本机下载目标文件内容（注意`.html`结尾的文件会自动返回`text/html`），但比如`.html.swp`就变成一个文件自动被我们下载而不是浏览器进行解析展示

#### 自定义服务日志

之前我们已经了解到，Nginx中的`access.log`用来记录用户所有的访问请求，而`error.log`则记录Nginx本身运行时的错误信息，事实上我们也可以通过自定义的方式来设置日志的记录方式

我们想要自定义日志，第一步就是要设置我们的日志记录格式，我们通过`log_format [format] [rule]`来设置格式，在默认的Nginx配置文件中也已经给出了样例，其中在`rule`中可以通过指定Nginx内部提供的变量名（之后会提及）来指定用户访问时需要展示的请求信息

我们通过`access_log [path] [format]`指定日志存储位置和日志格式名，这样在该自定义文件下我们就可以查看到用户的访问信息了

#### 其他指令

- `sendfile [on/off]`设置Nginx服务是否使用`sendfile()`传输文件，该属性打开后可以大大提高Nginx处理静态资源的性能

- `keepalive_timeout [time]`用来设定长连接的超时时间，当用户短时间请求结束之后时不会立即关闭该用户的上一次连接内容，使得当用户短时间多次请求时不会频繁创建连接，但是时间设置太长如果请求过多，大量连接没有断开，导致服务器性能下降，默认为`75s`

- `keepalive_requests [num]`设定一个长连接的使用次数，在满足上面一条的情况下，长连接在使用设定的次数之后也会强制断开

- `error_page [status code] [uri]`遇到错误代码指定访问某个页面

  > 此外还可以通过比如`error_page 404 @flag;`来跳转到某个具有`@`标识的location上`location @flag{}`

- `tcp_nopush [on/off]`在服务器开辟一个缓存区存放将要交友用户的数据，等到数据装满缓存区之后再进行发送，与之对应的`tcp_nodelay [on/off]`则指定服务器一接收到数据就将其发送出去，不等待，这两个指令同时开启的话优先使用`nopush`，当最后数据结束后不足以填满缓存，Nginx会自动再调用`nodelay`强制发送剩余数据

#### 子块元素

一个http块内还需要有别的块级元素，它中间可以放多个server块，一个server块又可以放多个location块，其中可以通过`return`来返回页面的响应内容（用于简单页面的返回内容）

用户在访问服务器资源时，默认就是通过`server_name:port/location`访问

![image-20220217123800122](https://s2.loli.net/2022/02/17/dQsRHb7NGUEgLAn.png)

同时大多数在http块中的指令也可以被指定在server和location块，同时指定时采用就近原则

在之后还会大量涉及到这两个块中的内容，此处仅简单介绍

#### listen和server_name

我们可能会疑问，明明一个服务器只有一个ip地址，为什么可以有多个server存在，因为我们可以发现，不同的server都会有`listen`和`server_name`两个字段存在，而我们只知道`listen`会决定浏览器访问时的端口信息，但是`server_name`又是干什么的呢

其实，用户在访问服务器时，一般来说我们会在地址栏输入该服务器绑定的域名，同时一个服务器ip可以绑定多个域名，而当web服务器接受到请求的时候，同时还会接收到服务器是通过哪一个域名访问的自己，而这个域名，就成为了与`server_name`匹配的条件，我们可以通过为同一个ip绑定多个域名，并在服务器内部对不同的访问请求进行筛选，来伪装拥有多个服务器的表象

同时，`server_name`除了上述所说的ip和完整域名匹配，还支持通配符（`*`）和正则表达式（以`~`开始一个正则表达式）域名匹配，同时注意可以通过在正则表达式中加`()`来框定某个变量在之后通过`return $1`来返回值（精确匹配>前通配符>后通配符>正则表达式）

注意，如果任一一个server都无法匹配接收到的请求，同时请求又确确实实发送到了服务器某个正在监听的端口上，那么默认会走第一条server处理请求（或者走存在`default_server`的server）

#### location块

除了server块中可以存在location块，location自身还可以进行嵌套使用

一般来说我们看到的如上面一样都是`location /xxx{}`直接进行匹配的，但是实际上这样匹配是不安全的，因为所有前缀为`xxx`的请求都会走这一条location，如果想要严格匹配，就需要用`=/`来进行匹配，此外还可以通过`~`和`~*`来指定使用正则表达式（不区分大小写）

在location之内可以包含root和alias指令，两者看上去差不多，但是也会有细微的差别

```
location /images{
	root /usr/local/nginx/html  # 会在root+location的位置去寻找资源
	alias /usr/local/nginx/html # 会替换location位置，直接使用alias里面的路径
}
# 第一个只能访问到html/images里面的内容，第二个只能访问到html里面的内容
```

location还可以配置index指令，是用来设置网站的默认首页，如果指定多个首页，就从左往右找到哪个就停，还是十分简单的

## 静态资源

### 压缩

众所周知，传输内容大小决定着传输效率，但是传输内容的多少同样影响着传输效率，此时就需要通过压缩让传输包尽可能的小的同时装载更多的数据

#### ngx_http_gzip_module

Nginx默认会加载模块`ngx_http_gzip_module`，之后我们可以通过在http块中添加`gzip on`来开启传输时的数据压缩

当没有开启时，我们在`html`目录下放入了一个大文件，此时会发现文件的大小和我们用户接收到的包大小是基本一致的

![image-20220219112633181](https://s2.loli.net/2022/02/19/hPCM5zLZ8sDanxf.png)

![image-20220219112757681](https://s2.loli.net/2022/02/19/slI8Wj4JBqxUYg5.png)

此时我们通过检查工具检查接收该文件的MIME并在配置文件中开启传输文件的压缩功能，我们就可以对指定类型的文件进行压缩了

![image-20220219113042059](https://s2.loli.net/2022/02/19/rYS4OtKpvN6sEZl.png)

![image-20220219113004983](https://s2.loli.net/2022/02/19/IvunUc5k8mS3wEM.png)

记得重启服务器

![image-20220219113245367](https://s2.loli.net/2022/02/19/Ln4AkWhazdGVo1v.png)

可以发现比起之前有了明显的压缩了，而其中`gzip_types [MIME]`指定了对何种返回内容的压缩（默认为`text/html`），`gzip on`则代表打开压缩功能，而其中`gzip`默认是不打开的，我们如果想要对所有的返回结果进行压缩，则可以`gzip_types *`来指定，但是不建议这么做，因为某些比如图片和视频默认情况下已经是高度压缩了，服务器进行二度压缩反而会浪费资源降低效率

除了这两个指令之外，还可以使用`gzip_comp_level [num]`来指定压缩等级，其中9压缩程度最高但是耗时也最长，1反之，默认为1，一般设置为6即可

同时还有`gzip_vary [on/off]`指令用于设置使用发送`Vary:Accept-Encoding`头部来告诉用户我们使用了gzip压缩，还有`gzip_disable [regex]`可以通过对正则表达式的设置来设置是否对某些用户的请求头，响应时不进行压缩，一般用来过滤某些低版本或特殊服务端的请求（`MSIE [1-6]\.`来过滤IE6以下版本的请求（可能不支持gzip从而出现乱码）

由于gzip的配置比较复杂，建议配置在单独的文件中，再在初始配置文件中通过`include`包含

#### ngx_http_gzip_static_module

除了上面的内置加载模块，我们还可以为我们的服务器添加其他额外的模块，比如`ngx_http_gzip_static_module`，它只提供了一个指令，即`gzip_static [on/off/always]`，开启之后服务器收到用户请求时，会寻找根目录下存在`[资源名].gz`的文件将其发送给用户，而不是直接现场压缩之后再发给客户端

注意开启这个模块之后需要关闭之前的`gzip on`指令，因为一个是传输时压缩，一个是读取本地压缩文件

而对于在现有的Nginx上额外添加模块，其实并没有什么简便的方法，我们只能对初始Nginx重新编译

1. 查看Nginx当前参数信息

   ```shell
   nginx -V
   ```

   之后复制保存所有的参数内容

2. 对原有的二进制文件进行更名

   ```shell
   cd /usr/local/nginx/sbin
   mv nginx nginxold
   ```

3. 进入Nginx安装目录，重新编译，并进行更新

   ```shell
   cd /root/nginx/core/nginx-xxxxx
   make clean
   ./configure --with-http-gzip-static-module [其他参数内容]
   make
   cp /objs/nginx /usr/local/nginx/sbin
   make upgrade
   ```

### 浏览器缓存

当用户多次访问服务器上同一个资源时，我们显然不希望用户总是频繁的对服务器进行请求，此时就需要了解用户浏览器的本地缓存机制，以便将返回信息内容保存在用户本地，便于缓解服务器的压力

最重要的过程如下图所示：

![img](https://loulanyijian.github.io/images/cache.png)

简单来说，就是当服务器设置了浏览器缓存之后，用户首次访问页面时，服务器会对浏览器返回一个标记，在第二次访问时根据标签的一致来确定两次访问之间服务端是否改动内容，未改动内容则返回304，不请求服务器直接调用本地缓存展示内容则返回200正常，其中也涉及到强缓存和协商缓存，后面内容将会细说

#### 强缓存

在浏览器缓存中，强缓存涉及到两个响应头信息`Expires`和`Cache-Control`，其中前者比较古老，只是在响应头中设置了一个目标时间，只要没到这个目标时间都直接走强缓存，也就是调用本地的页面缓存内容直接显示，返回200

但是这可能涉及到服务端与本地时间不一致的问题，此时如果浏览器版本`HTTP1.1`则直接忽略`Expires`采用`Cache-Control`，后者不设定目标时间，而是设定某个时间段，当浏览器再次请求时，会先读取上一次请求时的200请求，比对当前时间和上一次请求中的`Cache-Control`做差和请求时间比较判断是否过期

注意只要资源没有过期，也就是走强缓存，那么浏览器就不会与服务器进任何的交互，只需要本地调用内容即可，同时虽然调用本地内容，但是页面在监视器中同样返回200

同时还需要注意同一页面刷新并不会走强缓存，必须重新打开一个页面并访问相同地址才能使强缓存生效

对于Nginx配置来说，其中集成了两个内容的同一指令`expires [time]`来直接对`Cache-Control`进行设置，同时也对低于`HTTP 1.0`版本的浏览器仅设置`Expires`

![image-20220222093759895](https://s2.loli.net/2022/02/22/dTSzVU8OWDgrotp.png)

![image-20220222093533133](https://s2.loli.net/2022/02/22/xo1hWEgV3pLtTb7.png)

除了直接设定时间之外，我们还可以直接设定一些选项，比如`no-cache`表示不进行强缓存，`max`直接设定十年缓存等，我们还可以不通过`expires`指令而是直接`add_header [key] [value]`来指定设置响应头信息，因为`Cache-Control`还支持很多不同的值信息

#### 协商缓存

协商缓存不需要指令对他进行控制，但是也是需要了解的一个现象

当资源过期或者强缓存设置为`no-cache`时，浏览器就需要与服务器进行一次通信，但是由于缓存的存在，当服务器上内容未改变时，服务器可以直接通知用户采用缓存内容，这样同样可以节省大量流量资源

具体的操作流程是这样的，首次访问时，服务器会在响应头信息中添加`Etag`和`Last-Modified`两个键值，分别存储了发送信息的一段内容加密验证和在服务器上该内容的最后修改时间，浏览器接收到这两个内容就保存在自己的请求信息`If-Modified-Since`和`If-None-Match`两个键值中，下次与服务端通信时直接与下一次服务器传来的值进行比对，如果一致浏览器就可以直接调用缓存内容进行展示

![image-20220222095843543](https://s2.loli.net/2022/02/22/meHyAZjf1rwJ8Fn.png)

![image-20220222095933728](https://s2.loli.net/2022/02/22/qPzMi7E3X9LB4Fw.png)

### 安全

#### 跨域问题

*前端调用的后端接口不属于同一个域（域名或端口不同），就会产生跨域问题，也就是说你的应用访问了该应用域名或端口之外的域名或端口（来自网络）*

对于我们来说，我们想理解跨域问题，就需要逐步剖析其产生原因

首先我们需要先了解一下同源策略，浏览器的同源策略就是一种约定，是浏览器最核心也是最基本的安全功能，内容即是仅当协议，ip和端口相同时才符合同源策略（同电脑下的不同资源不满足跨域问题）

而当两台服务器不满足同源策略，就会出现跨域问题

比如我现在有两台服务器，或者同一台服务器监听多个端口，此时我通过一个端口获取用户提交的请求，并将其转发到另一个端口上，此时就会触发跨域问题，即目标服务器不允许你这台服务器对其进行转发数据，浏览器的console内会报一个错，提醒我们出现了跨域问题，而原本需要转发的数据也没有办法正常转发

此时我们只需要在接收服务器上添加头信息`add_header Acess-Control-Allow-Origin [转发服务器地址，允许*]`和`add_header Acess-Control-Allow-Methods [请求方式，如GET]`

#### 防盗链

我们可能发现，当我们希望在我们自己的网页中显示别的网站上的图片时，似乎十分靠运气，有些网站的图片直接复制url就可以通过img标签显示在我们的网站中，但是相反也存在很多网站无论我们怎么复制图片地址，都没有办法在页面中显示，那些不能显示的图片实际上就是为图片添加了防盗链

首先我们需要了解到`Referer`头信息，因为我们知道所有的图片也好实际上就是服务器上的静态资源，事实上我们在网页中访问图片时也会携带来源的`Referer`信息，而显然我们通过自己服务器引用时也会携带我们自己服务器的`Referer`信息，而显然我们只需要在服务器中限制引用的服务器地址即可实现防盗链

在Nginx里面，只需要添加以下代码即可

```
location / {
	valid_referers none blocked [allow ip];  # none表示为空时允许访问，blocked表示被防火墙伪装后的东西允许访问（用于判断访问者是否为服务器），最后一项则是指定域名允许访问，不符合该规则的话就会设置invalid_referer这个变量为1
	if ($invalid_referer){
		return 403;
	}  # if也是Nginx的一个块级结构
	return 200 "yes";
}
```

但是这个技术太垃圾了，毕竟referer头信息是可以随便改的，这时候就需要我们用第三方模块进行再次防盗，此处暂时不表

## rewrite模块

从上面的内容我们可以看到，似乎Nginx配置文件内部还可以写一些逻辑判断语句？事实也的确如此，除了上述提到的`if`语句之外，Nginx配置文件内也可以进行简单的变量赋值，判断，跳出等操作

而这些操作的指令都在Nginx默认加载的rewrite模块中

### set

比如有如下代码

```
location /server{
	set $name test;
	set $age 10;
	default_type text/plain;
	return 200 $name=$age;
}
```

即可在屏幕上显示`test=10`，可以发现Nginx里面语法的随意性，赋值变量甚至不需要`=`，而输出更加不分类型（也就是只能存储字符串，不能进行运算等操作），这也说明了在配置文件中编写程序的局限性

同时还要注意就算实在需要设置变量，也避免和Nginx全局变量同名，下面是部分常用的全局变量

```
$remote_addr		    // 获取客户端ip
$binary_remote_addr	    // 客户端ip（二进制)
$remote_port		    // 客户端port，如：50472
$remote_user		    // 已经经过Auth Basic Module验证的用户名
$host			        // 请求主机头字段，否则为服务器名称，如:blog.sakmon.com
$request		        // 用户请求信息，如：GET ?a=1&b=2 HTTP/1.1
$request_filename   	// 当前请求的文件的路径名，由root或alias和URI request组合而成，如：/2013/81.html
$status			        // 请求的响应状态码,如:200
$body_bytes_sent        // 响应时送出的body字节数数量。即使连接中断，这个数据也是精确的,如：40
$content_length	        // 等于请求行的“Content_Length”的值
$content_type	        // 等于请求行的“Content_Type”的值
$http_referer	        // 引用地址
$http_user_agent        // 客户端agent信息,如：Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.76 Safari/537.36
$args		            // 与$query_string相同 等于当中URL的参数(GET)，如a=1&b=2
$document_uri	        // 与$uri相同  这个变量指当前的请求URI，不包括任何参数(见$args) 如:/2013/81.html
$document_root	        // 针对当前请求的根路径设置值
$hostname	            // 如：centos53.localdomain
$http_cookie	        // 客户端cookie信息
$cookie_COOKIE	        // cookie COOKIE变量的值
$is_args	            // 如果有$args参数，这个变量等于”?”，否则等于”"，空值，如?
$limit_rate	            // 这个变量可以限制连接速率，0表示不限速
$query_string	        // 与$args相同 等于当中URL的参数(GET)，如a=1&b=2
$request_body	        // 记录POST过来的数据信息
$request_body_file	    // 客户端请求主体信息的临时文件名
$request_method	        // 客户端请求的动作，通常为GET或POST,如：GET
$request_uri	        // 包含请求参数的原始URI，不包含主机名，如：/2013/81.html?a=1&b=2
$scheme		            // HTTP方法（如http，https）,如：http
$uri			        // 这个变量指当前的请求URI，不包括任何参数(见$args) 如:/2013/81.html
$request_completion	    // 如果请求结束，设置为OK. 当请求未结束或如果该请求不是请求链串的最后一个时，为空(Empty)，如：OK
$server_protocol	    // 请求使用的协议，通常是HTTP/1.0或HTTP/1.1，如：HTTP/1.1
$server_addr		    // 服务器IP地址，在完成一次系统调用后可以确定这个值
$server_name		    // 服务器名称，如：blog.sakmon.com
$server_port		    // 请求到达服务器的端口号,如：80
```

一般来说，全局变量同时包括我们自己定义的变量常常可以通过在日志中[进行输出](#自定义服务日志)来便于我们进行服务器的调试

### if

Nginx里面每一个语法能做的事情都非常有限，比如`if`语句的判断括号内只允许出项七种判断方式

- 直接是一个变量名，此时如果这个变量是`0`或为空，判断不成立，其他情况判断成立（判断请求是否包含变量）
- 比较两个字符串，中间用`=`或`!=`相连，只比较两个字符串是否完全一致（判断请求方式是否为`POST`）
- 通过添加`~`或`~*`进行正则表达式判断，如`$arg ~ [regex]`，其中`~`也可以用`!~`表示取反
- `-f/!-f`判断文件是否存在，如`-f [文件路径]`，注意资源会在`locaiton`指定的目录下寻找，与此类似的还有`-d`判断目录是否存在，`-e`判断目录或文件是否存在，`-x`判断文件是否可执行

### break

`break`可以直接退出一个location内容，并且将请求重定向到根目录下的location指定的请求资源上，如果资源不存在就报404

```
location /test {
	if ($args){
		break;
	}
}
```

则如果存在参数的话直接退出在根目录下寻找`test/index.html`或者是`test`资源进行展示

### return

`return`之前我们都有了解过，它会直接返回给客户一个状态码和响应内容，但它实际上还有别的用法，比如可以直接返回一个URL地址，从而实现重定向的效果

### rewrite

既然都叫做rewirte模块了，那么最重要的指令也就肯定是这个`rewrite [regex] [url] {flag}`指令了

如何使用呢，其实也非常简单，如上面所示，我们可以通过正则表达式匹配访问的内容，同时重定向到相应的页面

```
location /rewrite {
	rewrite ^/rewrite/(test).*$ /$1;
	rewrite ^/rewrite/baidu$ https://www.baidu.com;
}
```

此时注意当我们不添加flag时，我们如果输入`ip:port/rewirte/test1111`则默认状态会被**重写**为`/test`页面（url栏不变），而访问百度则是被**重定向**到百度（返回302）

其中的`flag`为可选项，有以下几个选择

- `last`寻找其他location处理本次请求并重写页面，没有的话就去寻找本地资源重定向，和默认状态下基本一致，如果访问的是外部链接则同样是重定向
- `break`不寻找其他location内容，直接去寻找本地资源重定向，不影响外部链接访问
- `redirect`对寻找到的location内容也进行重定向，其他不变
- `permanent`和`redirect`类似，但是返回的是301表示永久重定向

同时`rewrite`指令也不止只能用在location块中， 当它用在server块中的时候就可以实现域名跳转

```
server {
	listen 80;
	server_name www.test1.com www.test2.com;
	rewrite ^(.*) http://www.test.com$1;
}
```

如上代码所示

### rewrite_log

可以通过`rewrite_log on`打开URL重写日志的输出功能，通过了`rewrite`指令的请求会以notice的形式打印在错误日志上，注意要设置错误日志的等级为`notice`不然不可见

## 反向代理

事实上Nginx还可以进行正向代理但这不是我们学习的重点，我们需要学习其中的反向代理功能

Nginx反向代理模块的指令由`ngx_http_proxy_module`模块进行解析，该模块也是默认安装模块，我们需要了解的就是这个模块中的一些主要指令内容

### proxy_pass

这个指令用于把我们的请求代理转发到固定的服务器，并展示请求之后的内容，比如有如下代码

```
location /test {
	proxy_pass http://ip:port;
	proxy_pass http://ip:port/;
}
```

那么此时我们如果访问这台服务器的任何内容，都会被分发到指定的`ip:port`

同时对于第一条指令，请求会被分发到`http://ip:port/test/index.html`或在被代理服务器上寻找`test`资源，而第二条指令则不会拼接location中的内容，而是直接分发到`http://ip:port/`去寻找内容，但如果是`location / {}`的话就无所谓了

> 注意这里代理和之前rewrite的不同，我们之前说过，当我们使用rewrite请求跨域资源时，无论加什么参数都会被**重定向**到新的URI上去，也就是会变化地址栏中的请求信息，但是我们通过proxy_pass进行代理时虽然被代理服务器收到的还是代理服务器的请求需求，但是地址栏内容不会发生变化，是一个彻底的**重写**操作
>
> 往更深层次来说，rewrite指令让用户连续发了两条请求给不同的服务器（因为第一条请求返回了另一个服务器的ip），而proxy_pass用户始终只发一条请求给代理服务器，被代理服务器始终不对用户可见

### proxy_set_header

有些时候我们在接收到用户的请求时需要在其请求头中添加一些别的信息之后在转发给被代理服务器，此时就需要用到`proxy_set_header [header_name] [value]`指令给请求内容添加指定头信息

我们可以通过构造内容进行演示

![image-20220223150949617](https://s2.loli.net/2022/02/23/M4IpwRDQoknjZx9.png)

![image-20220223151210852](https://s2.loli.net/2022/02/23/eQ1blM9pImC48Zs.png)

可以看到是的确满足了我们的要求，其中82端口就是以后我们被代理服务器，而81端口则是我们的反向代理服务器

有了这个功能，我们就可以给被代理服务器发送用户的真实ip和端口，实现了服务器知道我们的情况但是我们永远不知道被代理服务器信息的功能

### proxy_redirect

为了能够彻底隐藏被代理服务器的所有信息，不给黑客有机可乘，上面的内容显然是不够的，比如在被代理服务器下有如下代码

```
location / {
	if (!-f $request_filename) {
		return 302 http://172.17.0.2:82;
	}
}
```

当访问的资源不存在时，此处显然做了一个重定向处理，且重定向到了自己身上，对用户来讲，会发现地址栏突然就变成被代理服务器的地址，这显然是我们不想看到的，这意味着被代理服务器的地址暴露在了用户面前

究其原因，实际上是代理服务器收到了被代理服务器发来的一个包含`Location`键的响应头的响应信息，该键的值即为被代理服务器的ip地址，在不处理的情况下，代理服务器忠实的将这个响应内容交给用户，用户的浏览器一发现其中的`Location`信息，即立刻就去访问其中指定的ip内容了，这也符合重定向的定义，但我们必须解决这种情况

如果说`proxy_set_header`是修改用户的请求头信息，那么`proxy_redirect`就是修改被代理服务器的响应头信息，它会判断`Location`中的内容是否与指定内容一致，如果一致的话就把他替换为我们希望的地址，比如我们可以在代理服务器上设置

```
location / {
	proxy_pass http://172.17.0.2:82;
	proxy_redirect http://172.17.0.2:82 http://172.17.0.2:81;
}
```

此时我们就可以发现，原本的重定向内容还是被替换成了代理服务器的ip，且再次请求时会跳转到被代理服务器的首页

> 新版Nginx似乎默认这个选项就是开启状态，如果需要测试则应先`proxy_redirect off`

## HTTPS

默认Nginx是不提供HTTPS支持的，如果我们想使用HTTPS，就需要[重新编译文件](#版本迭代)，并添加上`--with-http_ssl_module`模块

重新安装完成之后，可以通过`nginx -V`查看当前模块配置情况

### 通过openssl创建证书

执行以下指令即可，之后会在该目录下生成四个文件

```
openssl genrsa -des3 -out server.key 2048
openssl req -new -key server.key -out server.csr
cp server.key server.key.org
openssl rsa -in server.key.org -out server.key
openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
```

![image-20220223171024898](https://s2.loli.net/2022/02/23/QAkBMPUzXgjEWGC.png)

这样准备工作就完成了

### 开启ssl支持

默认的Nginx文件内的最后就有开启https的配置的范例，我们只需要去掉其中的注释并修改部分内容即可使用，最后内容如下

```
# HTTPS server
    server {
        listen       443 ssl;
        server_name  localhost;

        ssl_certificate      /root/cert/server.crt;
        ssl_certificate_key  /root/cert/server.key;

        ssl_session_cache    shared:SSL:1m;  # 所有内容共享缓存
        ssl_session_timeout  5m;

        ssl_ciphers  HIGH:!aNULL:!MD5;  # 允许的密码格式
        ssl_prefer_server_ciphers  on;

        location / {
            root   html;
            index  index.html index.htm;
        }
    }
```

此时我们可以尝试通过浏览器访问`https://172.17.0.2`，会发现浏览器能够访问了，但是报了一个不安全的错误，因为我们用的是没有经过认证的证书，不用管他，点击继续前往即可正确访问我们的网站

## 负载均衡

实现负载均衡有很多种很多种方式，最原始的就像是用户手动选择自己需要的服务连接，不止如此，我们还可以通过在DNS服务中为同一个域名添加多个IP地址，从而利用DNS轮询的方式选择IP访问，但是这两个方式都不是合理的选择，比如第一种方式并不能保证所有的人都平均的选择各个连接，而DNS轮询结果将会较长时间保存在本地缓存，如果发生对应IP的服务器宕机，同样也影响我们的访问

### 四层/七层负载均衡

被大众所认可的负载均衡器实际上包括四层负载均衡和七层负载均衡，这里的四层和七层指的是OSI参考模型中的第四层（传输层）和第七层（应用层）

四层负载均衡一般以硬件的负载均衡器（F5，BIG-IP等）为主，在数据包还未解析的底层就进行了分发，性能很高，但是硬件的成本也很高，动辄就是几十万，对于我们这种穷苦开发者肯定是用不起了，当然四层负载均衡也有软件方式实现，但相对来说性能也不如硬件设备了

幕墙常见的组合是四层负载（LVS软件）+七层负载（Nginx）实现负载均衡

### Nginx简单轮询负载

Nginx实现负载均衡的原理是在反向代理的基础上把用户的请求根据指定的算法分发到不同的服务器上

由于我们拥有多个服务器，肯定不能一个个去配`proxy_pass`，因此我们需要借用一个负载均衡池（upstream）来将所有的被代理IP地址放到这个池子里，由算法帮助我们选择访问的IP

```
    upstream backend {
        server 172.17.0.2:84;
        server 172.17.0.2:85;
        server 172.17.0.2:86;
    }
    server {
        listen 83;
        server_name localhost;
        location / {
            proxy_pass http://backend;
        }
    }
    server {
        listen 84;
        server_name localhost;
        default_type text/html;
        location / {
            return 200 "<h1>port 84</h1>";
        }
    }
    server {
        listen 85;
        server_name localhost;
        default_type text/html;
        location / {
            return 200 "<h1>port 85</h1>";
        }
    }
    server {
        listen 86;
        server_name localhost;
        default_type text/html;
        location / {
            return 200 "<h1>port 86</h1>";
        }
    }
```

这样就实现了最简单的负载均衡的配置，反向代理服务器会以轮询的方式逐个访问三台被代理服务器，在我们自己的浏览器也可以通过刷新看到访问的服务器周期性变化

### upstream池负载标记

事实上，我们可以在定义的`upstream`池中对每一个IP进行标注，以优化负载均衡的效率

- `down`此IP永久不可用，用于个别服务器维护时使用
- `backup`标记该IP为备用服务器，当别的服务器无法处理请求时再用这台服务器
- `max_fails=[num]`设置允许请求代理服务器失败的次数，默认为1
- `fail_timeout=[num]`表示设置经过`max_fail`失败之后，该服务器暂停的时间，默认为10秒

比如我可以这样设置上面的三个服务器

```
upstream backend {
    server 172.17.0.2:84 down;
    server 172.17.0.2:85 backup;
    server 172.17.0.2:86 max_fails=3 fail_timeout=15;
}
```

### 负载均衡策略

在实际应用中，不同服务器的性能情况不相同，任一时刻所接收到的用户请求数也不同，默认的普通轮询不能满足我们的实际访问需求，这时候就需要为负载均衡添加一些规则

- 加权轮询，我们可以在默认情况下在每一个IP后加上`weight=[num]`设置服务器权重，默认为1，权重越大，被分配到的概率越大

- `ip_hash`负载均衡算法，一般用于不同服务器session不共享的问题，它会计算用户的IP信息进行某种hash算法，将这个用户IP固定到唯一一台被代理服务器上，从而实现用户访问内容的session一致性，使用方法就是在`upstream`块的最上方指定`ip_hash;`即可

  但是这种方式也有局限性，由于它配置的全局性，会导致一切加权内容都失效，最终可能无法实现真正的负载均衡，同时对于session不一致问题也可以通过redis解决，因此这种方式不建议使用

- `least_conn`这种负载均衡算法可以将用户的请求分发到请求连接最少的服务器上，适合处理请求处理 长短不一致造成的服务器过载情况，相对还是比较智能的，使用方式也是全局方式

- `url_hash`按照用户url的内容进行分发，也就是用一台服务器响应用户访问的相同的文件内容，一般用于避免不同服务器多次调用同一文件系统内的同一文件的状况，保证当前用户访问的每一个文件都只存在于一台被代理服务器上，用法是在头部加上`hash $request_uri`

- `fair`这个负载均衡策略相较于其他几种都更为智能，会根据访问的页面大小，加载时间长短智能的进行负载均衡，但是这个智能所付出的代价就是原生的Nginx是不支持`fair`策略的，我们需要自己手动添加第三方模块

  > 如何添加第三方模块，就拿这个案例来说，我们需要以下几步
  >
  > 1. 下载模块，`https://github.com/gnosek/nginx-upstream-fair`
  > 2. 解压缩之后将其命名为`fair`
  > 3. 编译时添加参数`--add-module=[fair路径]`即可
  > 4. 在`src/http/ngx_http_upstream.h`找到结构体`ngx_http_upstream_srv_conf_s`添加`in_port_t  default_port`再执行make即可

## 缓存集成

Nginx还可以作为web缓存服务器使用，具体流程是当用户 多次请求同一内容时，第一次请求的页面会被暂时保存在Nginx服务器某个文件夹内，再次访问时通过比对直接从服务器中取出缓存内容进行响应，这样一方面降低了被代理服务器的负载，另一方面也更快提供给用户页面返回

缓存相关的配置指令在默认安装的`ngx_http_proxy_module`模块中，接下来也只介绍常用指令

### proxy_cache_path

这个指令用于指定缓存在Nginx上存储的目录位置，同时由于将所有缓存都存放在同一目录下当缓存变多时同样会影响性能，因此可以通过参数的方式对请求进行特殊加密后创建多级文件夹存放缓存

指令的完整形态是`proxy_cache_path [path] [keys_zone=] [levels=] [inactive=] [max_size=]`，其中level即指定目录层级，假设此时我们需要一个key用于加密，比如`key=test`，则`MD5(test)=098f...7b4f6`，假设`levels=1:2`，那么我们就会在`path/6/4f`这个目录下保存这个key的所有缓存内容，缓存最多指定三层目录

其他参数比如`keys_zone`是为这个缓存区设置大小和名称，用于存放各种keys，1M大概可以存放8000个keys，而`inactive`则指定缓存数据在多少时间内未被访问则自动删除，`max_size`设定最大的缓存空间，当单个key缓存存满之后会覆盖缓存时间最长的资源

由于除了`path`后面参数不分前后，因此指定时必须说明参数名，如`proxy_cache_path /usr/local/nginx_cache levels=2:1 keys_zone=test:100m inactive=1d max_size=2g`

### 其他指令

- `proxy_cache [zone_name/off]`用于开启缓存，如果开启的话则自定义使用哪一个缓存区进行缓存（上面指定的`keys_zone`）
- `proxy_cache_key [key]`用于设置key值，一般通过全局变量获得请求信息设置key，默认为`$scheme$proxy_host$request_uri`
- `proxy_cache_valid [status] [time]`对不同的返回状态码设置缓存时间，不然默认用`inactive`，设置多个会从上往下找，注意`status`可以设置为`any`
- `proxy_cache_min_uses [num]`，设置资源被访问多少次之后开始被缓存
- `proxy_cache_methods [method]`设置缓存哪些HTTP方法（`GET`等）

### 检测缓存是否生效

一般来说我们的缓存设置在`location`块下，往往和`proxy_pass`呆在一起，我们如果想知道我们的缓存设置有没有生效，最好的办法就是在请求之后去指定的缓存目录下查看是否存在一串md5值的文件，但是如果嫌麻烦，我们也可以在缓存块之下设置`add_header nginx-cache $upstream_cache_status`，然后在访问资源时进行抓包，查看头信息中`nginx-cache`的值，如果是`HIT`则说明用到了Nginx的缓存

## 服务端集群

Nginx在处理高并发请求和静态资源的方面十分强大，但是对于后台业务代码模块相对薄弱，因此我们可以将到后台业务部署在Tomcat，接着用Nginx反向代理到后台服务器即可，这也是今后大项目开发的基本基础

### Tomcat部署

1. 直接去[官网](https://tomcat.apache.org/download-10.cgi)下载Tomcat版本，在本地目录进行解压
2. 之后将打包好的项目`.war`包拷入`webapps`目录下
3. 进入`bin/startup.sh`执行即可
4. 可以在浏览器访问`:8080`端口看看是否启动成功

### Nginx开发环境

更改配置文件

```
upstream webservice{
	server 127.0.0.1:8080;
}
server {
	listen 80;
	server_name localhost;
	location /demo{
		proxy_pass http://webservice;
	}
}
```

即可

但是这样似乎和直接访问Tomcat也没什么不同，为什么突然要在中间加一层呢，此时就需要利用Nginx的特性对被代理服务器实现动静分离和集群搭建，这才能完全体现Nginx的优势

### 动静分离

其中的动静就是只动态资源和静态资源，正如之前所讲，Nginx处理静态资源的能力是非常高的，而相反对于连接动态资源cgi显得有些疲软和复杂，因此我们正好取长补短，用Tomcat处理后端请求数据，而Nginx负责展示静态的数据即可

同时动静分离还可以降低动态资源和静态资源的耦合度，就算是后端Tomcat宕机了，也不影响静态资源的展示

### 高可用解决方案

之前我们提到过，当某台被代理服务器宕机之后，由于Nginx的负载均衡和反向代理的特性，我们可以将请求分发到其他正常的代理服务器上从而不影响用户访问，但是万一Nginx宕机了那该怎么办呢

此时我们可以介绍一种Keepalived软件来解决

#### VRRP协议

Keepalived主要使通过VRRP协议实现高可用的功能，而这个协议的核心就是将几台不同的服务器虚拟成一台设备，对外提供虚拟路由器的IP，而在这服务器组内，分为时刻接收用户请求的Master服务器，和若干台用于监听Master服务器的Backup服务器，Master服务器会每隔一段固定时间向Backup服务器发送一个心跳检测， 如果在指定时间内Backup没有接收到这个通知内容，那么Backup就会替代Master成为新的接收用户请求的Master服务器

接下来，我们只需要在两台Nginx服务器上安装Keepalived支持即可

#### 下载安装

下载[Keepalived](https://keepalived.org/download.html)，解压之后`./configure --sysconf=/etc --prefix=/usr/local`，接着`make && make install`即可安装

进入`/etc/keepalived/keepalived.conf.sample`，我们可以分析一下其中的配置内容

![image-20220225185340622](https://s2.loli.net/2022/02/25/syGUW31eRcMrgXD.png)

修改完成后，执行`/usr/local/sbin/keepalived`即可开启功能，此时我们在Master主机上通过`ip addr`可以看到新的对外虚拟ip，此时我们可以通过这个虚拟ip访问Master主机

此时如果两台服务器分别安装Keepalived，并设定虚拟主机ip相同，此时如果一台主机Keepalive服务掉线了，那么另一台主机就能够及时补充为Master进程，直到掉线主机恢复

#### 优化

但是我们发现这种情况时仅当Keepalived自己进程被切断之后才会切换节点，显然没有和服务器上的Nginx建立联系，就算Nginx服务断了也和你Keepalived没有任何关系，因此我们需要将两个内容进行绑定

这时我们就需要在配置文件中加入`VRRP`脚本，首先编写一个bash脚本，放在keepalived文件夹下

```shell
#! /bin/bash
num=`ps -C nginx --no-header | wc -l`
if [$num -eq 0];then
	killall keepalived
fi
```

之后在配置文件中加上`vrrp_script`

```
vrrp_script nginx{
	script "/etc/keepalived/nginx.sh"
	intercal 2  # 脚本执行周期
	weight -20  # 权重减20
}
```

即可

## 制作下载站点

我们有时会在某些镜像站上看到下载列表之类，点一点就可以飞速下载内容，事实上大多就是利用Nginx做到的，我们也可以尝试一下

为了实现该功能需要使用默认加载模块`ngx_http_autoindex_module`

- `autoindex [on/off]`开启目录列表输出
- `autoindex_exact_size [on/off]`指定是否展示文件的详细大小，如果off的话会显示`kB/MB`之类
- `autoindex_format [html|xml|json|jsonp]`设置目录列表格式
- `autoindex_localtime [on/off]`在目录列表上显示文件修改时服务器的时间，`off`的话显示GMT时间

```
location /download {
	    root html;
	    autoindex on;
}
```

这样就会在`html/download`下寻找下载内容，此时我们只需要在目录下创建download目录，放一些下载文件即可

![image-20220225194235249](https://s2.loli.net/2022/02/25/FAry7wenG64kxXL.png)

### 用户认证模块

每个人都可以下载 服务器内容显然是危险的，因此我们需要对访问的用户进行筛选，只有输入正确的用户名密码才能够下载内容，Nginx也提供了这样的模块，只需要在其中加上`auth_basic [string]`即可设定验证，其中`[string]`为提示信息，然后我们再指定`auth_basic_user_file [file]`文件来确认用户输入内容是否符合要求来指定是否通过请求

但是为了这个功能能够实现，我们还需要安装一下`yum install -y httpd-tools`，之后使用命令

![image-20220225203306484](https://s2.loli.net/2022/02/25/kU5YGy3nIC4bqJT.png)

然后我们在浏览器再次访问内容，就会出现输入用户名和密码的提示框

![image-20220225203431469](https://s2.loli.net/2022/02/25/sc2VZHbhijuxBkP.png)

## Lua

Nginx是可扩展的，我们可以使用Lua来扩展Nginx的功能，Lua是一个脚本语言，随意程度可以和Javascript媲美

### 安装

1. `wget http://www.lua.org/ftp/lua-5.4.4.tar.gz`，接着解压
2. 来到安装目录，`make linux test`测试是否可以在本地安装，如果报错了的话就安装它报错的安装包
3. `make install`安装
4. `lua -v`检测是否安装成功

### Lua程序

Lua有可以通过交互式或者是脚本式来运行文件，首先先介绍一下交互式运行程序

1. `lua`调出命令行
2. `print("hello word")`即可打印结果
3. `Ctrl+c`退出

脚本式也很简单，只需要创建一个`.lua`文件，接着在里面输入lua语法接着`lua [文件名]`即可

> lua和javascript差不多，语句加不加分号其实无所谓

### 语法

- `--`单行注释，`--[[  ]]--`多行注释，`---[[ ]]--`取消多行注释
- 区分大小写，不等于是`~=`，逻辑运算符是`and or`之类，变量不用声明类型
- `..`连接两个字符串，`#[变量名]`计算变量字符串长度，数字型变量会报错
- `local`声明局部变量，不声明就是全局变量，`nil`是无效值，用`{}`包起来的叫table类型，比较重要，可以通过`type([变量名])`来查看变量类型，只有`false/nil`是False，其他包括`0`都是True
- 可以通过`[变量名]=[[`的方式声明长字符串，最后记得`]]`闭合
- 数组（table 表）索引默认从1开始，但我们可以先声明`a={}`接着通过`a["key"]=value`或`a.key=value`指定索引和值，这样的话`a[1]=nil`，还可以`a={"test",key=value}`直接指定一个表
- 函数`function name(params)`开始，以`end`结束，可以返回多个返回值，名字相同会覆盖函数并不会重载，可以乱传参数，多的丢弃，少的赋值`nil`，多个参数`...`，赋值直接`local a,b,c = ...`即可，返回值也是`return`
- 判断和循环不用加括号，语法是`if [条件] then`和`while [条件] do`和`for i=exp1,exp2,exp3 do`，这仨都以`end`结尾，同时`exp1`之类的和C里面的两个`;`隔开的东西完全一致，另外还有`repeat [循环体] until [条件]`和`for i,j in ipairs(a) do`其中ipairs会返回a的索引和值
- `require [库]`引入第三方库，`[类]:new()`创建一个对象，`[对象]:[方法]`调用方法

### nginx_lua

这是一个淘宝开发的`ngx_lua`模块，将lua解释器集成进Nginx，可以使用lua脚本实现业务逻辑，降低了业务逻辑的实现成本

正常安装比较麻烦，因此我们采用安装OpenResty直接一步到位

> OpenResty是淘宝工程师开发的，集成了大量的精良lua库，第三方模块和大多数依赖项

#### 安装方式

1. OpenResty已经内置了Nginx，因此我们需要先将之前Nginx关掉`nginx -s stop`
2. 进官网查看[安装方法](https://openresty.org/cn/linux-packages.html#centos)，当然我们也可以下载源码安装`wget https://openresty.org/download/openresty-1.19.9.1.tar.gz`
3. 接着解压，进入目录`./configure`和`make && make install`
4. 进入`/usr/local/openresty/nginx`目录，会发现和我们通过二进制安装的Nginx十分类似，我们也可以在`conf/nginx.conf`更改相关配置文件，以及通过`sbin/nginx`启动服务

#### 简单程序

先让我们在配置文件中指定一个location熟悉一下openresty的基本语法

```
location /lua {
    default_type text/html;
    content_by_lua ngx.say("<h1>Hello</h1>");
}
```

![image-20220226090449325](https://s2.loli.net/2022/02/26/f6jws18vPQcBKeC.png)

我们会发现想要网页上输出指定内容，我们就需要一个`content_by_lua`的指令，而在`ngx_lua`里面还有各种各样的`xxx_by_lua`指令，这些指令的含义就是应该在这些指令后面跟上一个lua语句

#### 常用语法

下面用一段代码展示常用指令操作

```
location /test {
	default_type text/html;
	set_by_lua $param "
		local uri_args = ngx.req.get_uri_args()
		local name = uri_args.name
		local gender = uri_args.gender
		if gender=='1' then
			return name.."先生"
		return name.."女士"
	"
	charset utf-8;
	return 200 $param;
}
```

可以发现我们嵌入了一段类似lua函数的内容，赋值给了nginx的一个变量，从而实现了指令的多种变化，避免使用Nginx内置的危险`if`语句

同时官方建议我们替换`by_lua`而使用`by_block`，用法差不多一致，只是把后面的双引号改为`{}`即可，里面还是若干lua代码

其他内容库我们可以访问[官网](http://openresty.org/cn/components.html)查看各个模块里面究竟如何使用