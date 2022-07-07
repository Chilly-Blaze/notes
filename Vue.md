# Vue2

Vue就是一套构建用户界面的渐进式JavaScript框架，就是根据获得的数据，利用小巧的核心库+插件的层次结构组成的库来设计用户响应界面的框架

同时Vue还有以下特点

- 采用组件化模式，将页面中每一个模块（HTML、CSS、JS）打包成一个个组件（.vue），提高代码复用率，更好进行维护
- 声明式编码，与之相对的是命令式编码，声明式只需要通过简单的声明框架会自动帮助我们写好声明的内容，且嵌入在HTML页面中，益于开发和阅读
- 虚拟DOM技术，当页面上的内容发生变化时，Vue框架会先自动将变化后的DOM信息引入虚拟DOM中，比较更新后的内容与原先虚拟DOM内容的区别和更新，并对新内容进行合并，最终在页面中只展示更新之后的内容，而不是将整个页面重新加载

## 嵌入式

### HelloWorld

想要开始学习一门技术，正常的步骤就是从helloworld开始，同样我们可以创建一个html文件，开始制作我们的第一个Vue项目

不过在此之前我们还是需要先[下载](https://cn.vuejs.org/v2/guide/installation.html#%E7%9B%B4%E6%8E%A5%E7%94%A8-lt-script-gt-%E5%BC%95%E5%85%A5)一下Vue的js库（当然也可以使用[CDN](https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js)，并且导入进我们的项目中

![image-20220311211748796](https://s2.loli.net/2022/03/11/gzyMcrU8mKDIijX.png)

编写如下代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>测试html文件</title>
    <script src="../js/vue.js"></script> <!--引入Vue库-->
</head>

<body>
    <div id="root">
        <h1>Hello {{name}}</h1> <!-- {{}}包裹住的内容称为容器模版，其中的代码依然符合HTML规范 -->
    </div>
    <script>
        // 阻止Vue启动时生成的生产提示
        Vue.config.productionTip = false
        // 创建Vue实例，想要使用Vue就一定需要创建实例
        new Vue({
            el: '#root',  // 建立Vue实例和页面容器的关系，现在就是为上面的div服务
            // 当然上面也可以document.getElementById('root')
            data: {  // data中存储数据，数据供el所指定的容器使用，它的值可以像这样写成对象
                name: 'World'
            }
        })
    </script>
</body>

</html>
```

接着就可以在页面上显示内容了

然而上面的代码虽然简单，但是还是需要有一些注意点

- 一个Vue实例和容器之间是严格的一对一关系，比如如果存在两个容器`class`都为`root`，那么Vue中的`.root`仅会匹配DOM中从上往下的第一个`.root`容器，或者如果创建了两个Vue实例匹配`#root`，那么第二个Vue实例也会失效
- `{{}}`之内的内容看上去是在Vue实例中定义的data值，但是实际上也是js表达式，可以在其中添加任意的js表达式，但只是不建议这么写js

### 数据绑定

#### 单向数据绑定

除了上面展示的直接通过`{{}}`包含`data`对象中的内容实现包含信息之外，Vue还提供了指令语法内容，用它我们可以根据需要绑定`data`内的属性

```html
<body>
    <div id="root">
        <h1>插值语法</h1>
        <h2>Hello {{name}}</h2>
        <hr>
        <h1>指令语法</h1>
        <h2>
            <!--其中v-bind可以运用在所有标签属性之上，会把后面的引号内内容自动识别成js语句-->
            <a v-bind:href="url">v-bind进百度<br></a>
            <a :href="url">:简写直接进百度</a>
        </h2>
    </div>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            data: {
                name: 'World',
                url: "https://www.baidu.com"
            }
        })
    </script>
</body>
```

指令语法可以解析标签（包括标签体内容和绑定事件，以v-开头的指令），功能非常强大

同时注意当需要动态变化的属性值比较多的时候，我们可以通过在data中添加比如`contain:{name:'123'}`之后在容器中添加`{{contain.name}}`即可

`v-bind`可以绑定所有的标签属性，包括class指定的CSS样式等，使目标可以根据我们的需要动态调整

#### 双向数据绑定

除了`v-bind`可以进行数据绑定，但是他是单向数据绑定，意思就是虽然我们在Vue实例中修改值时页面上的内容也会发生改变，但是比如页面上有一个输入框，将其中的`value`属性通过`v-bind`绑定，那么我们如果在输入框中改变页面上`value`的值，并不会影响到实际Vue实例中data下的属性，此时如果我们想要两个内容同步变化，那么我们就需要`v-model`绑定输入框中的value值

不过注意`v-model`只能绑定表单类型的标签属性，也就是应该满足Vue实例属性和页面内容可以双向更改的情况下（存在`value`属性）才能使用，不然会报错

同时由于`v-model`只能绑定表单元素的`value`使用，因此我们可以直接省去`value`值，直接`v-model:`绑定表单内容

```html
<body>
    <deng degndiv id="root">
        <h1>Hello {{name}}</h1>
        <input type="text" v-model:value="user"><br>
        <input v-model="user" type="text" />
    </div>
    <script>
        Vue.config.productionTip = false
        nshu ju jie chiew Vue({
            el: '#root',
            data: {
                name: 'World',
                user: 'root'
            }
        })
    </script>
</body>
```

其中注意别的表单属性与这种直接输入内容的表单属性的操作有所区别，不过第一要义还是盯着value看，比如单选/多选框无论选没选都没有value值，我们就需要自己添加

在绑定监视多个值时（比如页面上的多选框）data中的默认属性应该是`[]`而不是`''`，不然数据没有办法正常添加

同时对输入的内容有要求的时候（比如必须用户输入数字），此时我们可以`v-model.number`来控制输入，否则默认在保存时默认会使用字符串，在与后端交互之中可能会出错

除此之外还有`v-model.lazy`可以当输入框失去焦点时才更新Vue实例内容，`v-model.trim`可以过滤输入前后空格

### Vue实例对象

除了之前我们在前面编写的那样定义Vue实例对象内容进行页面展示，我们可能会发现好像我们创建出来的这个实例似乎并没有用一个变量来接收，也就是因为我们在创建的时候已经设定好了它的所有属性，因此创建之后我们也不需要它了

但是显然照常理来说我们也可以在创建实例之后通过某个调用方法对实例中的属性进行操作

```html
<body>
    <div id="root">
        <h1>Hello {{name}}</h1>
    </div>
    <script>
        Vue.config.productionTip = false
        const v = new Vue({
            data() {
                return {
                    name: 'World',
                    user: 'root'
                }
            }
        })
        v.$mount('#root')
    </script>
</body>
```

其中`$mount`是Vue实例父类的一个属性，我们可以通过修改它来实现Vue的el初始化

![image-20220312115511557](https://s2.loli.net/2022/03/12/xyPutHclAYkv2Vo.png)

同时data除了可以通过创建对象来指定，还可以如上面一样直接写一个函数，返回一个map表即可

#### MVVM模型

MVVM是一种软件架构模式，Vue也参考了这个模型，代表了三个东西，分别是模型（Model），视图（View），视图模型（ViewModel），在我们上面的代码中，分别对应着JavaScript对象（data中存储的所有数据），DOM页面和Vue实例，其中Vue实例作为视图模型，连接着页面内容和JavaScript对象，将JavaScript中的数据封装展示在页面中

> 因此我们常常使用变量名vm接收Vue实例对象

同时我们还可以发现，当我们在data中添加了属性之后，当我们输出Vue实例时，它的属性正包含了我们data中的属性，因此我们可以大胆猜测，是不是我们在`{{}}`中嵌入的数据，实际上就是生成Vue实例中的属性名呢？

显然这是正确的，因此我们可以在页面代码中嵌入任何Vue实例中的属性内容，且不需要在之前添加比如`vm.[属性名]`，Vue会自动帮助我们解析内容

#### Object.defineProperty

在进行进一步学习之前，我们要先复习一下这个方法，它的作用是为某个对象添加属性，但是还是有一些注意点

```html
<body>
    <script>
        let person = {
            name: "ZS",
            sex: "man"
        }
        Object.defineProperty(person, 'age', {
            value: 18,
            // enumerable:true,  // 控制添加的属性可以被枚举，默认false
            // writable:true,  // 控制属性是否可以被修改
            // configurable:true  // 控制属性是否可以被删除
        })
        console.log(person)
        console.log(Object.keys(person))  // 枚举
    </script>
</body>
```

我们可以在控制台验证一下

![image-20220312122531485](https://s2.loli.net/2022/03/12/akOHAxRmJcKIY9n.png)

可以发现通过这个方法直接添加的属性，在不指定其他内容的情况下，默认是不可枚举，不可修改，不可删除的

同时如果直接在定义对象的时候指定死了某一个属性的值，就等于在构造方法中传入了一个值，因此无论传入的值是不是一个变量，比如（`let person = {age:num}`，然而我们如果之后改变了num变量的值，person的属性并不会跟着变化，如果想要实现两者的同步变化，`defineProperty`也可以做到

```javascript
let num = 18
Object.defineProperty(person, 'age', {
    // 当有人读取person的age属性的时候，get方法就会被调用，实时更改属性的值
    get: function () {
        return num
    }
})
```

此时我们可能在控制台中没有明确显示age的属性，但是一点开就会发现其实age属性是在的，只是需要我们点一点三个点才能显示

![image-20220312123557072](https://s2.loli.net/2022/03/12/SYkfCGMQWmbjBwP.png)

这时候如果我们修改num的值，person中的内容也就会跟着变了

![image-20220312123912690](https://s2.loli.net/2022/03/12/lZQJMhuBHDpqnCR.png)

与此同理的是set方法，在修改属性的时候会被调用，此处不举例了

#### 数据代理

数据代理就是通过对一个对象属性的修改，来达到对另一个对象属性修改的效果，而实现这个效果的底层原理其实就是上面讲过的`defineProperty`来定义属性的

此时我们看一下上面原始程序的控制台信息

![image-20220312130233461](https://s2.loli.net/2022/03/12/QVvmR6BbGgOLXuE.png)

在了解了defineProperty方法之后，我们对为什么在页面代码中直接使用`{{name}}`就能展示数据也有了更深层次的了解

明白了这个道理，我们可以尝试在页面中直接添加`{{_data.name}}`，页面中也可以正常显示

> 但是我们如果在控制台直接打开`_data`属性，可能会惊讶的发现里面的数据好像还经过了一次get，也就是核心数据仍然是使用三个点实时获取的，实际上这并不是get效果，而是Vue在其中做了数据劫持的操作，为的是能让页面显示的内容和实时修改内容相匹配，为了每当我们修改了（set）data中的属性时，页面能实时显示修改后的内容

### data数据处理

#### 事件处理（methods）

除了能够调用数据之外，JavaScript还有一个功能就是对于页面的各种事件（点击，键盘），能够进行捕捉并处理，为了能够在页面中响应用户的操作，Vue也贴心地提供了以`v-on`开头的指令（可简写为`@`），使得容器事件可以被Vue实例捕获并处理

同时为了相应按钮能够正确执行内容，我们理应为我们创建的实例添加某些方法，Vue提供了`methods`供我们编写执行函数

##### 点击事件

```html
<body>
    <!-- 
        prevent:阻止跳转
        stop:阻止冒泡事件
        once:只执行一次
		同时也可以写在一起比如.prevent.stop
    -->
    <div id="root">
        <h2>Hello {{name}}</h2>
        <button @click="showinfo()">show Tips</button>
        <a href="http://www.baidu.com" @click.prevent="showinfo()">阻止跳转</a>
        <div @click="showinfo()">
            <button @click.stop="showinfo()">事件冒泡测试</button>
        </div>
        <button @click.once="showinfo()">只执行一次</button>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    const vm = new Vue({
        el: '#root',yu fa
        data: {
            name: 'World'
        },
        methods: {
            showinfo() {
                alert('Tips')
            }
        },
    })
</script>
```

> 注意为指令添加比如`.prevent`细节时并没有提示信息，应该牢记语法

与`data`类似，`methods`定义之后我们也可以在Vue实例中看到它作为一个方法显示在属性中，这意味着如果我们定义了一个比如`show()`的函数，我们除了在标签属性中使用，还可以在页面中利用`{{show()}}`调用

但是注意`methods`定义的内容并不会像`data`一样生成代理数据属性，因为方法中的内容是不常修改的，因此不需要时刻检查是否发生变动，同时也节省了资源和时间

> 除了click之外，form表单的submit属性也可以设置事件处理（比如前端监测内容输错了可以不提交后台`@submit.prevent`等等）

##### 键盘指令

除了能够捕获点击指令之外，我们还可以捕获键盘的输入

```html
    <!-- 
        Vue提供了常见按键的别名，比如enter,delete,esc,space,tab等
        如果我们需要检测别的按键的情况可以通过e.key查看某按键的名字，接着@keyup.[按键名即可]
        如果涉及到多单词，比如CapsLock需要改为caps-lock，不过不是很方便就是了
        同时注意tab只能绑定在keydown上，因为默认会切走光标
		系统修饰键也可以比如@keyup.ctrl.e来绑定快捷键
    -->

    <body>
        <div id="root">
            <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo">
        </div>
    </body>
    <script>
        Vue.config.productionTip = false
        new Vue({
            el: '#root',
            methods: {
                showInfo(e) {
                    // if (e.keyCode !== 13) return 与这条语句相等
                    alert(e.target.value)
                }
            },
        })
    </script>
```

#### 计算属性（computed）

当我们需要在页面上显示比如两个`data`中属性的拼接值，我们当然可以通过页面中直接拼接或增加`methods`方法来实现，但是用起来总是感觉怪怪的，这时候就需要使用计算属性了

和前面讲过的`data`和`methods`一样，计算属性`computed`我们也需要将其添加到Vue实例中

```html
<body>
    <div id="root">
        <input v-model="first" type="text" />
        <input v-model="second" type="text" /> <br>
        <span>{{merge}}</span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            first: '1',
            second: '2'
        },
        computed: {
            merge: {
                // 当有人读取这个方法时，get就会被调用
                get() {
                    // 同时如果返回值没有被改变，那么会放进缓存里，再次在页面中调用时get方法不会被重复调用
                    return this.first + this.second
                }
            }
        }
    })
</script>
```

同理只要有get，那么按道理计算属性也有set方法，用法也和上面的内容相同，当merge被修改的时候就会被调用，不过总之就是不太好用，不如直接修改被计算属性调用的data或其他内容比较好

> 需要特别注意，虽然我们是按函数的样子去写的merge，但是它返回的是一个确定的计算出来的值，同时它的名字就叫做计算**属性**，因此他在Vue实例内部实际上是一个属性，因此我们在页面中调用这个计算属性的时候千万不要变成比如`merge()`这样的函数调用写法

同时计算属性还可以通过简写，但是必须只有get而没有set方法才可以使用，可以直接把比如上面的merge当做一个函数使用，返回get所需要的值即可

```javascript
merge() {
    return this.first + this.second
}
```

#### 监视属性（watch）

监视属性就是监视某一个值的变化，直接上案例，在上一个文件的基础上只需要添加

```
watch: {
    merge: {
        handler(newV, oldV) {
        console.log("新:" + newV + "老" + oldV)
        }
    }
}
```

即可实现监视merge函数，在我们输入内容使之发生改变时在控制台提示我们改变内容

![image-20220312215605586](https://s2.loli.net/2022/03/12/rO5zsqhivt26mTo.png)

当我们监视的属性中存在多级结构时（比如`data:{a{b:{c:1}}}`），想要监视其中的子结构（`watch:{a:{...}}`）改变情况，可以在watch监视属性中开启`deep=true`，实现深度检测

> 如果只监测多级结构中的某一个子属性，也可以通过`watch:{'a.b.c':{...}}`进行监视（注意单引号）

同时上面的监视属性同样可以进行简写，同样和计算属性一样，当监视属性内部只需要handler的时候，也可以直接把监视属性定义成一个函数即可

#### 对比计算属性

学了监视属性之后，我们可能发现监视属性似乎和计算属性差不太多，好像上面的案例中的merge也可以在watch中进行更新，只需要在data下再定义一个merge属性即可

但实际上两者还是有差别的，比如watch不依靠返回值来确定属性内容，而是直接在watch内更改属性内容，没有返回结果，但是computed计算属性却要靠返回值确定属性内容，我们还是需要择机使用，不过当两者都可以实现的情况下，我们优先还是使用计算属性

#### 函数管理

假设有这么一个情况，我们在watch监视属性内部调用了一个`setTimeout()`函数，此时应该如何编写内容？

```
watch: {
    merge(newV, oldV) {
        setTimeout(() => {
        	console.log("新:" + newV + "老" + this.second)
        }, 1000)
    }
}
```

此时看上去十分自然，但实际上其中却学问不小，假设我们将函数改为`setTimeout(function(){...})`你会很惊讶的发现this的地方报了一个错，事实上是因为如果是`function`定义函数，那么它的this就在setTimeout函数上，显然这时Window底下的函数，但是如果是箭头函数定义，那么this默认没有，就会去它的外边寻找this，显然就找到了merge所对应的受Vue实例控制的this了

这也同时说明了为什么我们不能将merge定义为一个箭头函数，因为它的外部是window对象，因此其中的this也就变成了window对象了

因此我们总结出两个规律

- 所有被Vue管理的函数，应该写成普通函数，这样其中的this才是vm对象
- 所有不能被Vue所管理的函数，应该写成箭头函数，这样才能使内部的this为vm对象

#### 过滤器（filters）

当我们页面上存在某些简单的数据处理需求时（比如`1000->1,000`或日期格式的转换），且该要求需要被多个内容数据复用（比如界面上多个位置都有`1000`需要处理），当然使用methods或者是computed都能够处理，但是我们还可以使用过滤器这个方案

比如以下场景

```vue
<body>
    <div id="root">
        <span>{{msg | dotF}}</span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            msg: 1000
        },
        filters: {
            dotF(msg) {
                return '1,000'
            }
        }
    })
</script>
```

可以发现在页面中调用时使用管道符将data属性传给过滤器，而且过滤器支持多层传递，可以比如再将`dotF`的返回值作为参数传递给下一个过滤器，进一步的是我们可以在过滤器中指定多个参数，除了第一个参数默认由外部传入，其他参数都可以直接在调用过滤器时添加，比如`msg | dotF('111')`这样

由于过滤器存在不同数据的复用性，因此我们还可以为全局所有的Vue实例添加全局过滤器，只需要使用`Vue.filter('[名称]',function(value){..return ...})`来指定即可，不可避免的增大了

### 渲染

#### 控制标签显示

当我们需要隐藏页面上的某些容器时，我们可以用两个指令实现

- `v-show:[bool]`，自动将容器的`display: none`，这样的隐藏效果可以在页面检查中看到
- `v-if:[bool]`，直接将容器的结构移除，在页面中哪都找不到了，除此之外还有`v-else-if`和`else`，不过控制的容器需要紧紧写在if控制的容器后面才可以生效

其中`v-if`可以与template连用，在不影响原本结构的前提下批量为连续的容器添加样式

#### 枚举列表

与之相类似的是`v-for`标签属性，它可以遍历指定数组的内容，并创建多个与数组元素个数相同数量的容器用以列表展示列表内不同属性

其结构需要了解一下，常规的结构如下

```vue
<body>
    <div id="root">
        <ul>
            <li v-for="(item, index) in items" :key="index">
                {{item.id}}-{{item.name}}-{{item.age}}
            </li>
        </ul>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            items: [
                { id: 1, name: 2, age: 3 },
                { id: 2, name: 2, age: 3 },
                { id: 3, name: 2, age: 3 },
            ]
        }
    })
</script>
```

对于其中的内容，有`v-for:"([列表遍历出每一项存放的变量名],[索引变量名]) in [列表]" :key="[遍历出的每一个容器的唯一标识位]"`

当然`v-for`也可以遍历对象，这样的话上面小括号内的第一项就是属性值，第二项就是属性名

#### Key详细探讨

其实我们会发现，上面的`:key`似乎我们不写内容也可以正常显示，我们可能会疑惑这个key到底有什么卵用zhe yzhe yzhe y呢，更重要的是，我们会发现好像这个`key`属性并不存在在页面上，同时如果我们设置了两个相同的key，页面还会报错，这就好玩了，既然不写也没事，在真实页面中也不作为标签内属性展示，写了还有可能错，那我干嘛要写它呢？

其实它虽然名为标签标识位，但是它只在Vue生成的虚拟DOM中使用，其中最重要的一点，就是如开篇所说的，对比更换的内容并进行有选择的修改真实DOM而不是浪费大量时间直接重新生成DOM

教程中展示了一个案例，当我们将遍历的`<li>`标签中的内容进行变化，并改变顺序重新加载DOM之后，在虚拟DOM中发生的变化

![image-20220313174023242](https://s2.loli.net/2022/03/13/HlVczSu9hGqIvem.png)

之后又在`<li>`标签中添加了一个输入框

![image-20220313174155944](https://s2.loli.net/2022/03/13/P2MAkanTdz6eDyH.png)

点击按钮之前和之后

![image-20220313174254051](https://s2.loli.net/2022/03/13/tY5fKQ24HPdM3Z8.png)

![image-20220313174310943](https://s2.loli.net/2022/03/13/a1UkfHw5rcL28WY.png)

这就是典型的如果无脑采用`:key=index`之后会出现的问题，下面是解释图

![image-20220313175149768](https://s2.loli.net/2022/03/13/wfniY2bNXW8kCOQ.png)

可以发现不止是显示的错误操作，同时也使得更换效率极其低下，虚拟DOM的优越性没有被体现，这也就说明了为什么数据库中的记录一般都有一个`id`属性，为前端的页面显示提供了方便

但是这种问题一般不会出现，只有当真实DOM上的显示内容顺序发生改变的时候才会出现（逆序增加，逆序删除等）

同时当我们没有写key的时候，Vue也会自动把`index`作为默认的key

#### 列表过滤案例

学习了上面的内容之后，我们应该可以编写一个在前端筛选数据并实时展示的案例了 

就沿用上一个案例内容，稍作修改，形成了这样的代码

```vue
<body>
    <div id="root">
        <input v-model="searchKey" type="text" />
        <button @click="sortType=-1">升</button>
        <button @click="sortType=1">降</button>
        <button @click="sortType=0">不操作</button>
        <ul>
            <li v-for="selItem in selItems">
                {{selItem.id}}-{{selItem.name}}-{{selItem.age}}
            </li>
        </ul>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            items: [
                { id: 1, name: '123', age: 2 },
                { id: 2, name: '145', age: 1 },
                { id: 3, name: '647', age: 3 },
            ],
            searchKey: '',
            sortType: 0
        },
        computed: {
            selItems() {
                const arr = this.items.filter((p) => {
                    return p.name.indexOf(this.searchKey) !== -1
                })
                if (this.sortType !== 0) {
                    arr.sort((p1, p2) => {
                        return (p2.age - p1.age) * this.sortType
                    })
                }
                return arr
            }
        }
    })
</script>
```

注意其中JavaScript对数组排序和筛选条件的使用

形成效果

![image-20220313223952710](https://s2.loli.net/2022/03/13/swDnVQaUruNGg9E.png)

当然联系我们前一节讲过的内容，上面这个代码key值不是数据的id，且在执行排序之后对数据的顺序进行了改变，因此在排序上其实效率并不是很高

### 内部数据监视

我们会发现我们虽然学习了watch检测属性，但是当我们对data中的某一个属性在页面上进行绑定的时候，会发现data中的内容一旦变化，页面内容即跟着改变了，这显然也存在着一个Vue内部的监视机制，会帮助用户检测Vue中的内容并在页面上给出改变

#### 产生问题

比如有以下这样的代码

```vue	
<body>
    <div id="root">
        <button @click="updateD">更新数据</button>
        <span v-for="(item, index) in items" :key="index">{{item.id}}-{{item.name}}-{{item.age}}</span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            items: [{
                id: 1,
                name: '1',
                age: 1
            }]
        },
        methods: {
            updateD() {
                // this.items[0].id = 2
                this.items[0] = { id: 2, name: '2', age: 2 }
            }
        }
    })
</script>
```

看上去似乎十分正常，页面的展示也没有存在问题

![image-20220314203452319](https://s2.loli.net/2022/03/14/8AQ9qkz3tvMaghT.png)

但是如果当我们点击一下按钮之后，想象当中的页面上出现`2-2-2`的情况并没有出现，而只有当我们把上面注释解除掉之后页面上的id值才会被修改，这显然是不符合我们的常理的，而更加不符合常理的事情是当我们点击按钮之后打开f12的，会发现Vue开发者工具中又出现了我们修改的内容，这也太诡异了

![image-20220314203926179](https://s2.loli.net/2022/03/14/yZgBIMDrvJSA21b.png)

而这种情况一旦不注意在实际开发中就会造成十分大的困扰，究其原因还是没有理解Vue自带的监视对象

#### 模拟对象监视

如何才能实现我们修改一个data中的内容之后立刻提醒用户哪个内容被修改了呢？在不看Vue提供的源代码的基础上，我们可能会写出以下代码

```javascript
let data = {
    id: 1
}
let tmp = data.id
setInterval(() => {
    if (data.id !== tmp) {
        tmp = data.id
        console.log('被更改了')
    }
}, 100);
```

这确实能够实现效果，但是这样一个个设置定时器，data一多直接报废了，这时候就需要效仿一下别人的结构了

![image-20220314205414693](https://s2.loli.net/2022/03/14/EbfVcOxCkhqnKFB.png)

在Vue实例中我们找到了`_datad`属性，这个属性我们之前也提到过，就是用来存储在实例化的时候指定的data数据的，但是明明直接将data内容放进去就可以万事大吉，为什么Vue要设定一个get和set方法来控制name项呢？

相信经过上面的示例我们已经知道这个get和set方法是为了能够时刻监视`_data`中的属性变动，但是其中到底是如何实现的呢，我们不妨自己模拟一下，由前面所提到的内容可以知道，`Object.defineProperty`似乎满足了我们的需求

```javascript
Object.defineProperty(data,'id',{
    get(){
        return data.id
    },
    set(val){
        data.id = val
    }
})
```

这样子写吗，显然是不对的，虽然设定了只要想查看id就调用get方法，但是get方法内却又调用了id属性，从而形成爆栈，而`set`方法也与此类似，都不能完成目标操作，这时候就需要我们对其中的内容稍稍改动一下

```javascript
let data = {
    id: 1
}
const obs = new Observer(data)
let vm = {}
vm._data = data = obs
console.log(vm._data)
function Observer(obj) {
    const keys = Object.keys(obj)
    keys.forEach((k) => {
        Object.defineProperty(this, k, {
            get() {
                return obj[k]
            },d
            set(val) {
                obj[k] = val
            }
        })
    })
}
```

看到这个代码的第一眼我们一定是懵逼的，这也正是这个代码能够实现实时监控变量变化的巧妙之处，接下来是对这个代码的解释

1. 页面进行第一次渲染，data初始赋值，新建实例`obs`和`Observer`对象内的内容

2. 注意此时data作为行参传入了`obs`对象（注意此时行参已经和data分开了），同时新创建了一个`obs.k`局部属性，值为传入的局部变量data内的内容

3. 同时在`obs`内部为这个`obs`实例的局部属性`k`新建了一个监听方法（`k=id`，外部可以通过`obs.id`访问到`k`），直到检测到`k`被修改或者在页面上被访问

4. 比如当`k`被修改的时候（比如`obs.id=2`），此时立即调用`set()`方法，虽然`obs.id`的值已经被改变了，但是`set()`的第一个参数就是带着这个修改之后的参数进入方法内，接着我们让`obs的行参obj.id=2`，注意，这里总的来说就是`obs的obj.id=obs.id`，这样就直接避免了像之前一样爆栈的问题

   > 注意到监听属性的`get`方法是在调用想查看监听属性值时被调用，而`set`方法是属性已经被改变之后才被调用

5. 这样就实现了巧妙的属性监听，同时由于最巧妙的是`obj`是`obs`的一个形参，同时还巧妙的利用了JavaScript的特性，即函数内的非`this.[属性]`在实例化之后都只作为构造函数内的局部变量出现，而不作为实例内的属性出现，因此我们在外部是不能通过`obs.obj`或`obs.keys`访问到其中的内容的

6. 当我们打开`Console`的时候可以惊讶的发现`obs`实例的内容似乎与data如出一辙

   ![image-20220314231154351](https://s2.loli.net/2022/03/14/K7y1JogzksYRXC4.png)

   甚至我们可以通过`obs==data`来确定他们俩的内容其实是一样的，这就很好玩了，结合之前我们创建Vue实例之后`Vue._data==[传入data]`判断也是true来看，我们似乎已经复现了Vue中的内容了

这种把原本数据遍历并添加监视方法的行为就称为数据劫持

#### 数组监视

上面所模拟的案例显然并不能解释为什么会产生第一节中的问题，因此我们还需要了解一下Vue的数组监视原理

回到[第一个案例](#产生问题)，我们打开控制台看一看Vue实例的结构

![image-20220315090256503](https://s2.loli.net/2022/03/15/o1dHKADMEWiyFGR.png)

我们会很惊讶的发现，即使`items[0]`里面存在相对应的比如`id.get`方法，然而外层的`items[0]`本身却没有相对应的`get/set`方法，通过上一节的分析，我们就非常好理解为什么我们单独`items[0]=...`的时候不能即时更新页面了，因为它根本没有`set`去监测修改！

所以这是Vue的一个bug吗，显然可能性比较小，真实的情况是，Vue故意避免了我们使用直接赋值的方法为Vue的data内管理的数组进行改动，假如我们需要改动，就需要对这个数组调用Vue为我们写好的七种函数

他们分别是`push/pop/shift/unshift/splice/sort/reverse`，一般来说，这几种函数可以满足我们的所有数组改动需要

你可能注意到了，为什么说是Vue为我们写好的函数呢，这些数组操作函数难道不是本身数组就有吗？当然是的，但是为了调用此方法后实现数据的实时监测，Vue就必须要重写这些方法，我们可以通过控制台验证

![image-20220315091137773](https://s2.loli.net/2022/03/15/WOHmITBXGawenJi.png)

说清楚了数组监测，我们就正式理解了Vue对实例中数据改动的监测原理

> 想要修改数组中的某一项也可以`Vue.set(vm.items,1,{...})`实现实时数据监测
>
> 同时如果使用filter过滤数组并赋值给原数组，事实上是替换掉了整个数组而不是其中的一个下标，因此是会被Vue监测到的

### 其他指令

常见的指令在之前都已经介绍过了，因此接下来的指令可能在开发中不常见，但是部分场景中还是可能会遇到，纯当增长见识了

#### v-text

直接对标`{{}}`，可以在标签属性中直接指定该标签下显示的内容（如`<span v-text="msg"></span>==<span>{{msg}}</span>`不解析，纯文本显示），没什么用

#### v-html

在上面`v-text`的基础上，Vue会将传入的内容经过html解析之后传到页面上，不过注意如果作为用户输入可能会造成XSS攻击

#### v-cloak

不带任何参数`<span v-cloak>{{...}}</span>`当内容存在解析模版时使用，当比如模版还没被加载的时候（此时如果什么都没做会显示`{{...}}`而不是`...`的值）存在`v-cloak`属性，而当模版被加载完毕之后这个属性就会消失，我们可以通过配置`style`样式定位这个属性，当这个属性存在的时候比如不显示内容（`display: none`），直到模版加载成功，`v-cloak`消失，也就显示出来了

#### v-once

同样不带任何参数，在初次动态渲染之后就被视为静态元素，无论data或其他指令中的内容怎么修改这个标签内的这个内容都不会实时更新

#### v-pre

比起`v-once`更狠，直接将其中的内容直接强行不经过Vue渲染直接输出，`{{}}`该咋样就咋样，不仅可以节省Vue加载速度，这也可以防止一些奇怪的注入获取我们创建的Vue实例（当然不知道有没有用）

#### 自定义指令

我们如果发现Vue内置的指令并不能满足我们的需求，此时就需要自定义指令了

我们可以直接在Vue实例创建时添加上配置项`directives`，之后直接写上自定义指令的名称（`v-[指令名]`）定义的函数，并在函数中指定内容即可，下面是简单的案例

```vue
<body>
    <div id="root">
        <span v-test="msg"></span>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            msg: 1000
        },
        directives: {
            test(element, binding) {
                // 其中element是使用这个指令的标签信息，binding是传入data属性的各种属性
                // 自定义指令中，不得不涉及DOM操作指令
                console.log(element, binding)
                element.innerText = binding.value * 10
            }
        }
    })
</script>
```

控制台显示

![image-20220315122725531](https://s2.loli.net/2022/03/15/n2kGCcBeMEvdJqI.png)

综上，指令的自定义就需要拿着指令返回给我们的真实DOM元素进行修改，并且我们还需要注意每一次当模版发生解析的时候（不一定是指令控制的数据发生改变），所有的指令都会被调用一次，确保界面展示的正确性

除此之外，上面这个函数其实和计算属性中的内容一样也是简写形式，完整的写法每一个自定义指令其实都是一个对象，结构如下

```
directives:{
	test:{
		bind(){}
		inserted(){}
		updated(){}
	}
}
```

其中我们知道其实我们页面上的标签只要打上了Vue的某个指令，实际上在页面展示这个标签之前都会前经过一次Vue解析，然后才在DOM中添加解析之后的内容，但是细分开来其实还有不少细节，而这三个函数第一个`bind`就是将页面标签交由Vue解析的时候执行的，`inserted`就是在解析之后将要插入页面的时候执行的（比如可以在`isnerted`里获取到该标签的父标签，而`bind`里就获取不到），`update`则是在模版被重新解析的时候执行的（第一次展示时不执行）

这三个函数都有上面所说的两个参数，我们可以对其修改DOM并根据需求进行自定义

而简写方式就是将我们写的DOM操作内容复制到`bind`和`update`两个函数中

> 注意指令名多个单词的时候，单词之间用`-`分隔，同时在定义时要在整个单词外加引号，同时自定义指令也和过滤器一样，可以在全局配置`Vue.directive`，用法大差不差

### 生命周期

学习一项技术最重要的内容就是了解这个框架或应用的生命周期，它何时产生，何时运行，何时终止，我们在自定义指令的时候已经关注到了指令执行时所在阶段的重要性，在创建Vue实例的时候，Vue实例也为我们提供了标识Vue工作不同阶段开始或结束时的函数供我们使用，默认函数都不存在内容，但是我们可以根据我们自己的需求，在不同时间点执行不同的操作

这么多的时间点函数就是Vue的生命周期回调函数（生命周期钩子）

所有的函数我们可以在官网看到，但我们放一张网上的中文的解析图

![img](https://www.icode9.com/i/ll/?i=20200709180519923.png?,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Nhb19NYXJ5,size_16,color_FFFFFF,t_70)

其中红框白底的内容就是Vue为我们提供的生命周期函数

看着似乎不太好理解，我们可以做个案例试验一下

```vue
<body>
    <div id="root">
        <h2>{{n}}</h2>
        <button @click="addN">n++</button>
        <button @click="destroyV">destory</button>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    new Vue({
        el: '#root',
        data: {
            n: 1
        },
        methods: {
            addN() {
                this.n++
            },
            destroyV() {
                this.$destroy()
            }
        },
        beforeCreate() {
            // 此时只有一个Vue实例，里面的_data和method属性等我们指定的初始化属性都还没出来，数据代理未开始
            console.log('beforeCreate:', this._data)
        },
        created() {
            // 开启数据监测和数据代理，Vue实例的内容终于完整了
            console.log('create:', this._data)
        },
        beforeMount() {
            // 虚拟DOM已经生成了，但是还没来得及将其放到页面上
            console.log('beforeMount:页面显示{{n}}而不是1')
        },
        mounted() {
            // 初始化结束，页面正常显示，也就是我们不做任何操作时页面展示的内容，其中当前页面的DOM信息存在vm.$el中
            console.log('mounted')
        },
        beforeUpdate() {
            // data被修改了，但是页面上的真实DOM还没更新
            console.log('beforeUpdate:页面显示n=1但是实例中n=', this.n)
        },
        updated() {
            // 更新完成
            console.log('updated')
        },
        beforeDestroy() {
            // vm.$destroy被调用的时候调用，一般会清空一下一生加载或订阅的内容，料理后事
            console.log('beforeDestroy:', this)
        },
        destroyed() {
            // 已经死完了，但是注意给比如某个按钮绑定的事件还在（但是自定义事件不在了），addN会执行，但是页面上内容不更新
            console.log('destroyed:', this)  // 好像也能输出实例，但是实际上已经不作用了
        },
    })
</script>
```

![image-20220315185623768](https://s2.loli.net/2022/03/15/zApDrxXFtQ17JBH.png)

可以发现，生命周期都是成对出现的，每一个时刻都分为进行之前和之后，其中某些函数是之后常用的，之后也会介绍到

## 组件化编程

组件化编程就是将完整的页面进行拆分，拆分成不同的几大块，之后先把每一大块进行封装，再将其中更细分的内容进行进一步拆分并封装，其中封装内容包括但不限于CSS/html/js/ttf等资源，保证每一块无论是大块还是小块都可以在下一页面中被完全的复用

### 非单文件组件

#### 简单的组件添加和使用

创建一个组件和我们之前`new Vue()`的操作十分类似，此时只需要调用`Vue.extend()`即可创建一个组件，不过需要注意的是我们不应该在组件中为其添加`el`属性，因为这个组件到底是给谁用的是由之后创建的Vue实例指定

同时data属性不能再和之前一样写成对象了，必须写成一个函数形式，因为对象被多变量引用时并不会创建多个不同实例，而函数的返回值永远是全新的新的对象，不用担心耦合的问题

而由于我们的组件没有指定`el`，因此我们肯定不能直接拿来用，此时第二步我们就需要将其添加到我们创建的Vue实例中，在创建实例的过程中，只需要添加`components`指令即可

```Vue
new Vue({
	el:...,
	components:{
		[组件名(随便取)]:[接收了Vue.extend的对象名],
		...
	}
})
```

第三步就是添加组件标签，直接在界面上添加组件名所指定的标签即可，比如以下这样的案例

```html
<body>
    <div id="root">
        <comp1></comp1>
        <br> <!-- 普通标签结构不用修改 -->
        <comp2></comp2>
    </div>
</body>
<script>
    Vue.config.productionTip = false
    const comp1 = Vue.extend({
        template: `
            <h2>{{name}}</h2>
        `,
        data() {
            return {
                name: '组件1'
            }
        },
    })
    const comp2 = Vue.extend({
        template: `
            <h2>{{name}}</h2>
        `,
        data() {
            return {
                name: '组件2'
            }
        },
    })
    new Vue({
        el: '#root',
        components: {
            comp1,  // 等于comp1: comp1
            comp2
        }
    })
</script>
```

> 其中`template`可以代替`el`属性，组件会直接像解析原本`div#root`一样解析`template`里面的标签

在开发者调试工具中，我们也可以看到组件的身影

![image-20220316182103596](https://s2.loli.net/2022/03/16/CWxEuzPfRjiBsH7.png)

同时即使我们在页面上添加了多个组件标签，各个组件之间也是隔离的关系，数据的改变并不会互相造成影响，即实现了复用，又简洁美观使用性强

但是这个文件还是存在很多问题，比如我们在单文件中创建了多个组件，但是在实际开发中实际上一个文件内仅有一个组件，同时我们还要将创建的Vue实例扩展到全局，这些内容在接下来的学习中都会涉及

#### 一些注意点

- 组件名（即在Vue实例中注册的名），当为单个单词时，Vue推荐我们当使用大写开头的单词，多个单词则使用小写字母开头+`-`连接，比如`my-name`等，要注意的是大驼峰命名法会让Vue无法识别内容报错，不过之后学习脚手架环境之后会对这种错误进行修正
- 组件名也不能和html原有的标签名重名，不然也会报错
- 页面上的组件标签支持自闭合，但是最好是在脚手架环境下，不然会出奇怪问题
- 可以省略`Vue.extend`，直接`const [名] = {}`之后在实例中注册即可
- 除此之外组件之间也可以嵌套，也只需要在组件内添加`components`即可，不过这样需要在父组件的`template`属性里编写`<[子组件]>`标签
- 在非单文件组件的编写中，需要将子组件定义在父组件之前
- 在一般的开发中我们一般会开发一个`app`组件，由它而不是Vue实例管理所有组件，而这样Vue实例（root组件）就只需要管理`app`一个组件了

### VueComponent

如果我们在上面通过`console.log(comp1)`那么我们会看到在控制台输出了一个名叫`VueComponent`对象，那这个东西到底是什么呢？我们好像也没有通过`new`创建这个函数啊？

实际上当我们在页面中添加组件的标签时，Vue就会调用`new`一次这个对象，也就是说，页面上引用了多少次组件标签，就会生成多少个`VueComponent`对象

而我们的`extend`方法实际上是调用了一下这个对象的构造函数`this._init`之后就返回给变量`comp1`了，而不是直接new出来给变量

因此在调用`extend`的时候其中的`this`也就是`VueComponent`对象了，只不过这个对象如果我们通过控制台输出会发现它和`new Vue`出来的内部结构长得基本一模一样

> 之后就把`VueComponent`创建的**组件实例**称为vc了，我们创建的Vue**根实例**则理所当然叫做vm了，我们发现对于vc我们往往会对其命名，但是vm我们一般就不拿变量去接收它了，这也是组件所必须的

#### 构造方法和原型对象

我们首先得弥补一下之前欠下的JavaScript的债，好好讲一讲函数这个东西和类这个东西在其中的区别和联系

我们之前只是提了一下原型和原型链的概念，但是如果不巧碰到了以下代码

```javascript
function Test(name) {
    this.name = name
    console.log("构造方法")
}
let test = new Test("123")
```

常识来说，Test应该是一个函数，而常识又告诉我们，函数是不可能被`new`出来一个对象的，更不可能在函数内存在什么`this`之类的，但是JavaScript显然不信这个邪，就是要反其道而行之

于是我们打算换一种角度思考，盯着它看了一会儿，我们发现这个函数的内容怎么这么像一个构造函数，这么一想好像突然有点道理，但是执行这个构造函数的类跑到哪里去了呢

这时候`prototype`属性隆重登场，如果我们在控制台输出这个函数的信息（注意要用`console.dir`），那么我们会发现这个函数像一个类一样拥有好多属性

![image-20220317230340960](https://s2.loli.net/2022/03/17/v5YNVoZTtEXngxS.png)

这个函数居然真的像一个类一样被我们输出出来了，同时它的`prototype`正指向他所服务的那个类，为了验证这个假设，我们输出我们`new`出来的实例

![image-20220317231222449](https://s2.loli.net/2022/03/17/x5HqQoXrCJNGyuh.png)

这下我们明白了，这个函数的的确确是某个类的构造函数，于是我们就把定义函数时自动那个创建的这个类叫做原型对象，而这个函数即为构造函数，`new`出来的内容叫做实例

当然我们会发现每一个输出的类都有一个`[[prototype]]`的方法，看似和之前的`prototype`很像，但是它的功能唯一且任何对象上都有（`prototype`只有定义构造函数的时候会出现），就是指向其原型对象，无论是实例还是构造函数都一样，而如果本身就是原型对象那就指向更高层次的原型对象，直到最终的`Object`

![img](https://pic2.zhimg.com/80/v2-c4fad77a39802a292c71792559d7ea99_720w.jpg)

#### 内置关系

介绍完了这些知识，我们再回过头来看看`VueComponent`和`Vue`的关系就一目了然了

接下来我只需要给出一张图，估计就能领会其中的意思

![image-20220317232421156](https://s2.loli.net/2022/03/17/FWLK7owQZXjyksp.png)

这样我们就搞清了这vm和vc之间到底是什么牛马关系，进一步为我们巩固了构造函数，原型对象，实例之间的关系

### 单文件组件

接下来我们就需要写一些`.vue`文件了，但是显然浏览器并不会自动帮我们解析这种类型的文件，这时候就需要我们借助别人提供的工具对`.vue`进行编译组装成浏览器看的懂的内容（HTML、CSS、JS等）

而这工具就叫做脚手架

不过在此之前我们先要了解一下`.vue`文件中应该怎么写代码

#### 目录结构

首先我们需要创建几个`[组件].vue`，文件名称就应该就是你组件注册的名字，采用大驼峰命名法，这么一来就和Java类的创建和命名方式非常类似

```vue
// Demo.vue
<template>
	<!-- 组件的html结构写在这 -->
	<div class=".demo">
		<h1>{{name}}</h1>
	</div>
</template>

<script>
	// 组件交互相关方法比如data和method方法
	// export default是默认暴露
	export default { // 简略形式，简略了const vc = Vue.extend{...}，和最后的export default vc
		name: 'Demo1',  //最好写一下组件的名字
		data() {
			return {
				name: '单组件测试'
			}
		}
		// .methods等等
	};
</script>

<style>
	/* CSS样式 */
	.demo {
		background-color: orange;
	}
</style>
```

创建好了一个组件，下一步就是创建所有组件的管理者，`App.vue`

```vue
// App.vue
<template>
	<div>
		<Demo1 />
	</div>
</template>

<script>
	// 汇总所有的组件
	// 引入
	import Demo1 from "./Demo1.vue";
	export default {
		name: "App",
		// 注册
		components: {
			Demo1,
		},
	};
</script>

<style>
</style>
```

仅有组件肯定是不行的，还有个老大哥没有定义，他就是vm，因此下一步就是创建一个`main.js`文件，来创建一个vm

```js
// main.js
import App from './App.vue';

new Vue({
	template: '<App></App>',
	components: { App }
})
```

当然这样我们仅有组件和vm并不能使页面进行运行，更不能通过浏览器访问，因为没有结构网页可不管那么多，他只会执行`.html`文件，因此下一步就是创建一个html文件

```html
<!--index.html-->
<!DOCTYPE html>
<html lang="en">

<head>
	<meta charset="UTF-8">
	<meta http-equiv="X-UA-Compatible" content="IE=edge">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>单文件组件</title>
</head>

<body>
	<script src="../js/vue.js"></script>
	<script src="./main.js"></script>
</body>

</html>
```

这样我们Vue项目的基础就完成了，当然由于没有脚手架，因此这么四个文件还是不能运行的，这时候就需要我们先安装一下脚手架再说了！

## 脚手架

脚手架到底是什么牛马，其实他是Vue提供的标准化开发工具，我们需要通过npm安装它

### 安装

1. 先下载一个npm，可以网上搜一搜先安装一个Node.js（最好，指不定直接装npm就和我一样乱报错），要确认npm可以使用
2. `npm config set registry https://registry.npm.taobao.org`，设置国内镜像源
3. `sudo npm install -g @vue/cli`，如果是Windows下可能要开管理员模式
4.  跑到桌面上，确定需要在此处生成一个Vue文件，则运行`sudo vue create [项目名]`，接着选择Vue版本构建项目即可
5. 之后会在指定位置生成一个项目名的文件夹，我们先不急打开它，接下来注意我们现在创建的文件夹所有者好象是root，我们把它改成我们自己`sudo chown chillyblaze:chillyblaze vue_test/**`
6. 接着进入文件夹，执行`npm run serve`即可开启Vue项目
7. 打开网站查看效果

> 如果你像我一样发现不知道为什么下载内容跑不动或者报了什么错，这时候我们就需要检查是否已经正确设置镜像库，检查是否设置了代理，检查缓存是否清空等等，可以用如下指令`npm config get registry proxy`查看仓库和代理，接着`npm cache clean --force `清理缓存，这还不行就重启电脑，我反正是重启之后就好了

### 内部结构

看完了网站效果，这时候我们就需要通过代码编辑器打开这个文件夹，我们首先了解一下其中的项目结构

![image-20220318223943885](https://s2.loli.net/2022/03/18/nzTmJOb7HsKVAUi.png)

我们扫一扫src下面的组件内容，好像和我们之前自己写的东西都差不多，但是我们还是发现了一个我们不熟悉的东西

```js
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
	render: h => h(App),
}).$mount('#app')

```

这个render是什么东西啊，这个东西我们之后会详细说明，此处我们只需要了解到这个指令让我们的App组件被放入到了vm中即可，可以暂时约等于`component`的效果

### 运行项目

接下来我们只需要把之前写完的组件**（仅`.vue`组件！）**直接拷到相应的src目录下即可运行，且在修改之后只需要保存一下Vue就会帮我们自动重新构建项目展示

接下来的项目结构是这样的

![image-20220318225928605](https://s2.loli.net/2022/03/18/6o7lw9SLpKIgrkv.png)

同时注意要在`App.vue`里面修改一下组件的路径，注意到`App.vue`组件在components文件夹之外

> 但是如果像上面那样做之后你重启服务，可能就会被报一个错了
>
> ![image-20220318230135768](https://s2.loli.net/2022/03/18/shcgjz3LKQvSZ7I.png)
>
> 这牛马东西居然不认我们的Demo单个单词组成的组件！简直是无法无天，我们需要直接在`vue.config.js`里面把这个垃圾语法判定给他关了
>
> ![image-20220318230329454](https://s2.loli.net/2022/03/18/yIuqPLWFSaT4CXl.png)
>
> 之后再次执行即可成功运行，除非你之前代码写错了

### render配置项

上面已经提过，render配置项让我们看不太懂，而且我们发现我们自己写的`main.js`好像也就和他给出的差了一个这个render，那么我们不妨就将我们自己的`main.js`拷进来执行看看到底会发生什么

![image-20220319211348031](https://s2.loli.net/2022/03/19/m52uvgZqbTXia9y.png)

很可惜，启动的时候报了一个错误，这个错误好像说的是我们什么导入的Vue包不包含叫什么`compiler`的编译器，所以没有办法解析模版`template`，这时候我们如果打开点进头部包含的vue包里面，会发现这个包深藏在一大堆`node_module`里面，而我们如果看到`vue`目录下的`package.json`我们会发现有一条`  "module": "dist/vue.runtime.esm.js"`语句，而它指定了当我们仅引入vue包的时候它默认引用的就是这个`runtime`包，而这个包中正巧没有我们解析`template`所用的解析器

终于知道了原来不能在创建vm的时候使用`el`或者和`template`有关的属性，而这时候允许我们使用的就是这个render函数了，它的原本样子长得是这个样子

```vue
render(h){
	return h(App)
}
```

经过简化就变成了我们所见到的这个模样，其中`h`参数原本的名字叫做`createElement`，这个函数的作用就是给我们创建一个页面标签元素，比如我们`h('h1','test')`就可以创建一个`<h1>test</h1>`

render函数还是比较简单的，之后我们除了在`main.js`里面用一下之外一般也不会在别的地方用到了

### 默认配置

我们可以通过`vue inspect > [输出文件].js`来将vue的所有配置内容输出到文件中

我们可以看到很多乱七八糟的属性，如果真的要改配置，我们就需要在目录下的`vue.config.js`里面修改所需要修改的默认属性，而什么东西可以修改，我们可以在[官网上](https://cli.vuejs.org/zh/config/)查找

但是默认的配置也挺好的，尽量不要改吧。。

## 其他特性

接下来我们介绍一些当前阶段常用的杂项内容，涉及到了各个方面的重要的新知识

### ref属性

当我们想要拿到某个标签时，我们往往会给他打上一个id，之后我们在其他地方通过`document.getElementById()`来获得DOM内容，但是手动操作DOM显然是不理想的，Vue提供了`ref`代替频繁设置`id`供我们使用，同时其中的标签内容都会存在当前vc下的`$refs`属性中

还有一个优点就是当我们把`ref`属性打在组件标签上时，我们还得到这个组件标签的vc实例内容，在之后的组件通信中有大用

```vue
<template>
	<div>
		<h1 ref="title">测试ref</h1>
		<Demo ref="demo" />
		<button @click="showref">点我展示ref</button>
	</div>
</template>

<script>
	import Demo from "./components/Demo.vue";
	export default {
		name: "App",
		components: {
			Demo,
		},
		methods: {
			showref() {
				console.log(this.$refs);
			},
		},
	};
</script>

<style>
</style>
```

![image-20220319220342671](https://s2.loli.net/2022/03/19/6LzgpAWUfT8tFKc.png)

### props配置

我们可能发现了，当我们在比如App组件当中引入多个子组件的时候，好像子组件的内容都是一样的？既然内容都一样那我们引入多个的意义是什么呢？假如某两个组件之间仅有数据不一致，难道我们还需要重新写一遍组件吗？那Vue高复用性的优点又如何体现呢？

这时候就需要`props`属性隆重登场，我们只需要通过在组件标签中传入我们需要的内容，之后在子组件内引入`props`属性，最后即可正常展示内容了

- `Demo.vue`

  ```vue
  <template>
  	<div class="demo">
  		<h1>{{ name }}</h1>
  		<h2>{{ age }}</h2>
  		<h2>{{ sex }}</h2>
  	</div>
  </template>
  
  <script>
  	export default {
  		name: "Demo",
  		data() {
  			return {
  				name: "张三",
  			};
  		},
  		props: ["age", "sex"], // 最简单写法
  		// props:{
  		// 	age:Number,  // 指定传入类型，不然控制台会报错
  		// 	sex:String
  		// },  // 稍微复杂一点写法
  		// props:{
  		// 	age:{
  		// 		type:Number,
  		// 		required:true  // 这个参数是必须的，不然控制台会报错
  		// 	},
  		// 	sex:{
  		// 		type:String,
  		// 		default:"男"  // 不传入的话默认值
  		// 	}
  		// }  // 最完整写法
  	};
  </script>
  ```

- `App.vue`

  ```VUE
  <template>
  	<div>
  		<Demo :age="10" :sex="'男'" />
  	</div>
  </template>
  
  <script>
  	import Demo from "./components/Demo.vue";
  	export default {
  		name: "App",
  		components: {
  			Demo,
  		}
  	};
  </script>
  ```

> 注意其中传入的标签属性最好在之前加上比如上述这样的`:age`，根据`v-bind`的特性，这样后面引号内的内容就会被当作js表达式执行，之后如果我们传入为数字就可以在子组件中被正常识别为数字，如果单`age="18"`子组件只会认为是字符串18

当然这其中还有一些底层的注意点

- 传入的参数在子组件的vc实例中只作为属性存在，并不会跑到`_data`里面去，这也意味着传入的这个参数和data中指定的组件属性还是有一定的区别的
- 传入组件的属性不允许在组件内部再进行修改了，虽然我们在组件内通过`this.[参数名]`访问，但是Vue并不推荐我们去修改它，如果我们真的需要修改，请在`data`中指定一个属性`[属性名]:this.[传入参数名]`这样将传入的参数交给`data`处理，就可以正常通过比如`methods`修改了
- 如果在`data`中存在和`props`指定的参数同名，`props`的优先级更高，`data`是什么牛马
- 注意在传值的时候我们不能使用Vue自带的标记了，比如`key`、`ref`等等

同时注意`props`不仅解决的是多数据在不同组件之间的重用问题，更重要的是它还能解决父子组件之间的通信问题，它不仅可以父组件给子组件传数据，甚至可以在父组件中定义一个方法传给子组件，之后子组件通过调用父组件传给它的方法，来调用父组件的方法，控制父组件的数据内容发生改变，特别注意无论是传值还是方法，都像是在子组件里面打开了一个快捷方式，最终的数据和方法存储位置还是父组件，因此这也进一步说明了为什么不建议在子组件中改变父组件传过来的参数内容了

### mixin混入配置

如果说上面的`props`是在高复用的前提下添加个性化，那么`mixin`就是在本就高组件话的基础上进一步提高复用效率，比如你的`Worker`组件和`Student`组件都有一段代码叫做

```vue
methods:{
	showName(){
		alert(this.name);
	}
}
```

难道我们需要在两个组件中都写一遍吗，这时候就可以使用mixin，我们可以先在Vue项目中创建一个`mixin.js`，里面写上如下内容

```js
export const mixin1 = {
    methods:{
        showName(){
			alert(this.name);
		}
    }
}  // 分别暴露
```

这时候我们就可以在Student组件中添加

```vue
<script>
	import { mixin1 } from "./mixin";
	export default {
		name: "Student",
		data() {
			console.log(this);
			return {
				name: "张三",
			};
		},
		mixins: [mixin1],
	};
</script>
```

当然使用的过程中同样有一些注意点

- 当混入内容`mixin`与原本定义的属性存在重复时，会进行合并（比如在已有`data`段的时候`mixin`内还存在`data`段），而当`data`内的属性存在重复时，优先忽略`mixin`内的
- 当遇到重复的生命周期钩子函数时，内部的内容都会执行，同时以`mixin`内的先执行
- 同时我们还可以在`main.js`中通过`Vue.mixin({...})`定义全局混入

### 插件

解决完了复用性，我们还需要解决耦合性，回顾我们之前学习过的某些指令，比如`Vue.mixin`、`Vue.filter`、`Vue.directive`等等全局的方法，这些方法往往都需要占用不少的代码空间，而且由于我们的Vue实例对象仅在`main.js`里面创建，因此我们这些代码难道只能一大堆放在`main.js`里面吗？

不，这时候我们就需要使用插件技术，我们只需要创建一个`plugin.js`，像是这么一写

```js
export default {
    install(Vue){
        Vue.directive...,
        Vue.filter...,
    }
}
```

紧接着我们只需要在`main.js`里面引入内容`import plugin from './plugin'`，之后在后面轻轻的引入一个`Vue.use(plugin)`即可完成所有配置的导入

比如我们在`Vue.prototype`上添加了一个方法，那么我们在全局的vm和vc上都能使用了，对于某些效果来说简直不要太方便

这同样便利了第三方插件的提供商，我们只需要简单的`use`一下，被人配置好的所有的插件内容都可以即时使用了

同时我们在`main.js`里面调用插件的时候，我们甚至能够往插件内再传入参数，之后插件内对我们传入的参数进行接收，从而做出相应的个性化反应

### scoped样式

当我们在不同组件内写了名字一样的样式时，如果我们在页面中引入了这个样式，我们可能会发现所有的样式都变成了某一个组件中定义的样式了（按照`main.js`中加载的顺序），这显然不是我们想要看到的，假如我们团队中有一大堆人开发组件，难道每一个样式还需要先统一注册避免冲突吗？

此时我们就需要在样式标签中添加`scoped`属性，这样里面写的样式就只属于这一个组件了

![image-20220319233721368](https://s2.loli.net/2022/03/19/xW6igbtfoeFG7Yw.png)

![image-20220319233745047](https://s2.loli.net/2022/03/19/LhPQk7NeTXVsbxE.png)

这样我们就可以愉快的在里面写代码了

### $nextTick

我们都知道，当想让页面上的input输入框获取焦点，页面上必须要有一个输入框才行，也就是说如果我们在`methods`某个函数内直接比如`this.$refs.inputT.focus()`是没用的，因为此时页面内容还在虚拟DOM里，自然没办法获取焦点，此时我们就可以在前面加一个`this.$nextTick(()=>{this.$refs.inputT.focus()})`即可让Vue在将虚拟DOM放到页面上之后再执行内部的代码

### 过度与动画

除了我们自己在CSS上写一些动画效果，Vue还内置提供了使用动画效果的方式

#### 动画组成

一般的动画都分为入场动画和离开动画，于是Vue内置了自动调用这两个动画效果的`transition`标签，只需要将其包裹所要执行动画效果的标签即可

同时Vue也内置了三种调用动画效果的方式，请看下面范例

```vue
<template>
	<div class="demo">
		<button @click="isShow = !isShow">animate</button>
		<!-- name指定需要调用哪一个样式，如果不指定就会去找v-enter/v-leave -->
		<!-- appear指定在第一次加载标签时便执行动画效果 -->
		<transition name="test" appear>
			<h1 v-show="isShow">这是一个动画</h1>
		</transition>
	</div>
</template>

<script>
	export default {
		name: "Demo",
		data() {
			return {
				isShow: true,
			};
		},
	};
</script>

<style scoped>
	/* 第一种方式:动画实现 对整个过程直接调用进场动画*/
	/* h1 {
				background-color: skyblue;
			}
			.test-enter-active {
				animation: anim 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
			}
			.test-leave-active {
				animation: anim 0.5s cubic-bezier(0.075, 0.82, 0.165, 1) reverse;
			}
			@keyframes anim {
				from {
					transform: translateX(-100%);
				}
				to {
					transform: translateX(0);
				}
			} */
	/* 第二种方式:过度实现 对起末位置进行指定并额外指定动画过程*/
	h1 {
		background-color: skyblue;
		transition: 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
	}
	/* 上方也可改成 */
	/* .test-enter-active,.test-leave-active{
			transition: 0.5s cubic-bezier(0.075, 0.82, 0.165, 1);
		} */
	.test-enter,
	.test-leave-to {
		transform: translateX(-100%);
	}
	.test-enter-to,
	.test-leave {
		transform: translateX(0);
	}
</style>
```

> 同时如果像一下子让一堆标签都共用一个动画样式，则可以通过`<transition-group>`包裹，不过注意内部元素必须包含`key`值，或者通过`v-for`枚举

而第三种方式便是直接在标签中指定动画样式的类名，不过一般用于引入第三方动画库 的动画效果时使用

#### 集成第三方

当然我们自己写的肯定没有别人写的动画效果好，我们可以直接下载别人写好的动画库进行引用使用

首先选择一个第三方动画库，这里以`animate.css`做范例

1. `npm install animate.css`

2. 进入[官网](https://animate.style/)找一个自己喜欢的样式

3. 在上面案例的`transition`标签中写入

   ```html
   		<transition
   			name="animate__animated animate__bounce"
   			enter-active-class="animate__bounceIn"
   			leave-active-class="animate__bounceOut"
   			appear
   		>
   			<h1 v-show="isShow">这是一个动画</h1>
   		</transition>
   ```

   即可

### Ajax请求

在前端的开发中，常常会遇到需要通过Ajax的方式请求其他服务器的资源并返回显示在页面上，Vue自身并不拥有模拟发送请求的功能，因此我们需要借助第三方库帮助我们发送请求获取数据

#### 简单获取请求

我们可以借助`axios`库来实现请求功能，直接`sudo npm i axios`即可

让我们借助github的开放api实现一个查询用户的案例

```vue
<template>
	<div>
		<input
			type="text"
			v-model="keyWord"
			placeholder="请输入需要翻译的词语"
			@keydown.enter="sendInfo"
		/>
	</div>
</template>

<script>
	import axios from "axios";
	export default {
		name: "Translate",
		data() {
			return {
				keyWord: "",
			};
		},
		methods: {
			sendInfo() {
				axios
					.get(
						`https://api.github.com/search/users?q=${this.keyWord}`
					)
					.then(
						(Response) => {
							console.log(Response.data);
						},
						(Error) => {
							console.log(Error.message);
						}
					);
			},
		},
	};
</script>
```

还是十分简单的，但是现实当中的情况并不如此顺利，可能你会遇到这样的报错

![image-20220322203028265](https://s2.loli.net/2022/03/22/ShMw1sYvXpBlGcF.png)

总之就是会出现`CORS policy`的错误，这其实就是因为Ajax请求的资源必须满足同源关系，当外来的内容与本机并不同源并且还在响应头中没有包含`cors`的头信息，那么浏览器会拒收返回的内容，自然也不能被我们获取到了

当然这仅限于Ajax，如果我们可以找一个代理服务器，帮助我们通过正常的http请求到我们所需要的资源，并返回给我们，那我们岂不是就可以获取到本获取不到的内容了吗

#### Vue设置代理

虽然Vue没有内置请求模块，但是却为我们提供了代理服务

我们只需要在`vue.config.js`中设置一下代理即可

```js
module.exports = defineConfig({
	transpileDependencies: true,
	lintOnSave: false,
	devServer: {
		proxy: {
			'/test': {
				target: 'http://translate.google.cn',
				pathRewrite: { '^/test': '' }
			}
		}
	}
})

```

其中通过pathRewirte来重写请求路径并将剩下结果拼接到目标路径后，请求之后再返回结果给我们的组件内容

之后我们只需要在组件内修改前缀`http://localhost:8080/translate_a/single?client=at&sl=en&tl=zh-CN&dt=t&q=${this.keyWord}`即可

### 组件事件

#### 浏览器本地存储

我们可以通过`localStorage.setItem('[key]','[value]')`来设置本地存储值，接着接着我们可以在浏览器的检查元素中的`Application`中看到我们设定的键值对

> 注意我们设定的`value`和`key`都必须是字符串，如果不是字符串类型那么它就会给你调用`tostring`方法，因此如果我们需要在用户本地存一个对象，就需要调用`JSON.stringify()`方法

除此之外，`localStorage`的`getItem`和`removeItem`和`clear`可以对存储的内容进行读取，删除，清空操作，同时如果读取到的是一个对象记得调用`JSON.parse`方法

除此之外我们还可以将`localStorage`改成`sessionStorage`，此时设定的就是当前会话临时创建的本地缓存，当浏览器关闭的时候会自动消失

> 当然这两个对象都是在`Window`里面的，但是由于ES6的特性可以省略`Window.`

#### 自定义事件

之前我们说到的自定义指令是与标签相关的，涉及到DOM元素的操作，而现在我们需要学习自定义事件，也就是`v-on`绑定的标签属性，我们可以直接在**子组件标签**上通过`@[自定义事件名]`来绑定自定义事件

注意，当我们为一个子组件添加自定义事件时，这个自定义事件就会被添加到子组件实例的vc身上，此时我们可以在**子组件内**通过`this.$emit('[自定义事件名]',[参数])`的方式触发这个事件

比如我们想要实现一个一点击按钮，就让子组件将自己的信息传给父组件，当然我们可以通过`props`将父组件的一个方法传给子组件，但是我们也可以通过自定义事件实现

```vue
// 父组件
<template>
	<div>
		<Demo @eventN="getDemoName" />
	</div>
</template>

<script>
	import Demo from "./components/Demo.vue";
	export default {
		name: "App",
		components: {
			Demo,
		},
		methods: {
			getDemoName(name) {
				console.log(name);
			},
		},
	};
</script>
```

```vue
// 子组件
<template>
	<div class="demo">
		<h1>{{ name }}</h1>
		<button @click="sendName()">click me and send name to App component</button>
	</div>
</template>

<script>
	export default {
		name: "Demo",
		data() {
			return {
				name: "张三",
			};
		},
		methods: {
			sendName() {
				this.$emit("eventN", this.name);
			},
		},
	};
</script>
```

同时当事件不使用之后我们还可以通过`this.$off()`，解绑所有事件，如果只想解绑某一个事件，可以通过数组`[自定义事件1,自定义事件2]`并传入`off`函数指定解绑

> 同时补充一个生命周期的知识，当一个组件实例或者是vm实例被销毁的时候，实例身上的所有自定义事件会被销毁，但是普通交互标签身上的固定比如`@click`事件不受影响

当然我们如果真的想在子组件上使用预先定义好的事件比如`@click`那么也不是不能用，我们只需要通过加上`@click.native`即可正常使用原生事件

以后对于子组件给父组件传递信息最好还是使用自定义事件，通过`props`让父组件给子组件传递一个方法之后子组件再调用实在是有点膈应了

#### 全局事件总线

上面我们已经将父子之间的通信关系介绍清楚了，那么两个兄弟之间通信用什么办法呢？这时候就需要使用全局事件总线的知识了，它理论上可以让任意的两个组件进行通信

此时我们已经学习过了自定义事件的创建，这时我们可以设想一个场景，由于我们知道我们自定义的事件是绑定在vc实例身上的，同时我们可以通过在实例内启动这个事件来让带有这个标签的父组件接收到事件被启动的信息

那么我们有没有一种方法，可以创建一个所有vc实例都可以访问到的组件，然后在一个组件内往这个组件上绑定自定义事件，再由另外一个组件调用这个事件并传递一些信息，接着绑定这个事件的组件通过接收这个事件是否启用并且使用时携带的信息，达到组件之间通信的要求呢？

我们之前介绍过，所有组件的原型都是vm，也就是所有vc实例都可以访问到vm原型对象，更巧的是，当我们输出vm原型对象的属性时（`Vue.prototype`），我们惊讶的发现这个对象上居然有`$emit`属性，也就是说咱们上一回说到的事件触发函数并不是在vc身上的，而是在vm身上的

那么根据上面的猜想，我们只需要在vm身上绑一个事件，就可以在任何一个vc身上查询并触发这个事件了！

##### $on

当然我们现有的方法是通过直接在标签上设定`@[事件名]`来开启一个事件，然而这种方法显然是对vm不奏效的，因为它根本不是一个组件，更不要说通过什么牛马标签来实例化它，面对我们遇上的难题，这里介绍另一种不在组件实例化时的标签内绑定事件的方法

我们可以在某个组件内的`mounted`生命周期中调用`this.$on('[自定义事件名]',([触发事件时接收的参数])=>{[触发事件时做的内容]})`，来开启一个自定义事件，而相对应的，这个`$on`函数同样是在Vue原型对象上的，之所以要将这个函数调用放在`mounted`中，还是因为这个函数在vc的生命周期中仅调用一次，且所有内容都加载完毕，正是绑定事件的好时机

而我们要认清的是，组件的自定义事件，从来都是绑定一次，触发多次的原则，而`mounted`钩子完全符合了我们的要求罢了

除此之外，我们也不用在组件标签中写什么`@`事件了，只不过比起那样绑定事件的方便，这种方式更加底层也更加不便罢了

##### 解决问题

就算我们知道了如何在组件内绑定自己的事件，但是问题依旧很多，我们不妨梳理一下某些可能性

1. 无论哪种方式绑定事件，都是在vc**实例化时**调用**Vue原型对象上的`$on`**方法在**自己身上**绑上一个事件，也就是说虽然调的是别人的方法，但是产生的结果却在自己身上，同理，在触发事件时调用**Vue原型对象上的**某个方法`$emit`**为自己**开启事件
2. 既然谁调用的方法自定义事件就在谁身上，那么我们直接找到Vue原型对象给他绑一个事件不就完了？但显然这又是理解不够透彻，任何原型对象我们都是无法直接拿到的，况且以往绑事件都是在创建实例时调用的`$on`方法，那能够直接原型对象调用自己的方法给自己绑事件？
3. 就算我们拿到了Vue原型对象，同样还有问题，Vue早就已经实例化完了，我们根本找不到任何一个函数或者是方法能让其唯一的绑定一个事件，而就算给Vue实例绑定了一个事件，但是他是实例啊，我们在别的组件中又怎么调用这个**实例**的方法？

综上，整理一下我们当前所掌握的信息

- 无论在哪个组件中，我们都可以调用到Vue**原型对象**上的方法，且是毫无阻碍的
- 除了在自己组件内，我们无法在任何地方访问到任何组件的**实例化内容**
- 事件是绑定在**实例化后的内容**上的，如果存在某个公共的绑定事件的位置，那么它必须是**实例对象**
- 事件只能在一个实例化对象上绑定一次（意味着必须通过`mounted`），但是能够被多次调用

现在揭晓答案，你会发现这个解决方案完美的符合了上述所有要求，直接贴代码

```js
new Vue({
	el: '#app',
	render: h => h(App),
	beforeCreate() {
		Vue.prototype.$bus = this  // 安装全局事件总线
	},
})
```

我们在Vue的原型对象上增加了一个`$bus`属性，而这个属性又刚好是刚实例化到一半的Vue实例化对象的拷贝，这样，我们就可以在任意组件内，通过`this.$bus`时时刻刻都访问到这个实例化对象（因为本地没有`$bus`属性，就会往外找），同时，我们只需要在组件内的`mounted`函数内，使用`this.$bus.$on`绑定事件即可建立一个全局的自定义事件，在其他组件中`this.$bus.$emit`就可以随时调用这个事件了！

#### 消息订阅和发布

除此之外我们还可以通过第三方库实现组件内的通信，我们只需要在组件内订阅某一个消息，在另一个组件中发布被订阅的某条消息并提供消息内容，订阅消息的组件就可以获得消息的内容了

1. 安装`sudo npm i pubsub-js`
1. 在组件内引用`import pubsub from 'pubsub-js'`
1. 在`mounted`中订阅某条消息`pubsub.subscribe('[消息名]',([消息参数])=>{[接收到消息时执行]})`，注意第一个参数是消息名，因此发布者携带的参数放在第二个接收，同时请设置一个比如`this.pubId`接收`subscribe`函数的返回值id，之后要利用它取消订阅
1. 在其他组件发布消息`pubsub.publish('[消息名]',[携带消息参数])`即可
1. 组件被销毁时记得`pubsub.unsubscribe(this.pubId)`

但是还是使用全局事件总线比较香，毕竟是Vue自带的

### 插槽

当我们需要在不同的容器中添加不同的内容，但是大体上不变时，我们当然可以通过`props`配置通过标签属性传参的方式引入内容，但是如果不同组件实例内的标签结构有所不同呢？我们目前的方法就是在组件内通过比如`v-show`并判断`props`接收到的内容比较并选择性的展示结构内容，但是这种方式一旦组件实例一多就要写一大堆判断，而且毕竟是整个标签结构整个标签结构的置换，全部塞在组件里显然显得不太合适

此时我们就可以借助插槽的功能了

#### 默认插槽

我们之前从没在组件使用标签内添加过别的内容，但是如果想要使用插槽，我们就需要在标签中添加自定义内容

```vue
// 父组件
<template>
	<div>
		<slot-test>
			<span>自定义的插槽功能</span>
		</slot-test>
		<slot-test />
	</div>
</template>

<script>
	import SlotTest from "./components/SlotTest.vue";
	export default {
		name: "App",
		components: {
			SlotTest,
		},
	};
</script>
```

```vue
// 子组件
<template>
	<div>
		<h1>测试插槽功能</h1>
		<slot>默认值</slot>
	</div>
</template>

<script>
	export default {};
</script>

<style>
</style>
```

这样外层的父组件就会自动将内部属性添加到子组件的`slot`标签中了

![image-20220322214546640](https://s2.loli.net/2022/03/22/Sdq4Uky76VMLlwK.png)

#### 具名插槽

非常简单，直接在上面的基础上在子组件中的slot标签中添加`name`属性，并在父组件的标签中添加`slot='[子组件name名]'`即可，这样就可以在子组件中定义多个插槽，在父组件中根据不同插槽的位置添加不同内容

> 注意，Vue推荐我们在使用具名插槽时，在父组件中的不同插值标签外包裹上`<template>`标签，并且支持我们在使用`<template v-slot:[子组件name]>...</template>`（注意不需要加引号，同时前面是冒号）的方式同样实现绑定子组件内的具名插槽，当然也支持简写`#[子组件name]`快速绑定

#### 作用域插槽

现在我们要明确一个概念，插槽就是子组件提供了一个接口，然后给父组件使用，而父组件使用时可以往这个接口里丢不一样的东西，实现个性化

但是！说到底还是父组件在使用这个插入的标签，这个标签的渲染也是在父组件中执行的，但是由于这个标签是给子组件使用的，难免会出现标签内的数据来自于子组件而不是父组件，假设现在子组件中有一个`msg`属性要显示在个别组件实例中的插槽里，这时候就会报错了

```vue
<slot-test>
    <span>自定义的插槽功能,{{ msg }}</span>
</slot-test>
```

![image-20220322220555357](https://s2.loli.net/2022/03/22/NBIqnSiveL1Eabr.png)

这时候就需要用到作用域插槽，我们必须在子组件中将`msg`属性传给父组件，之后才能让父组件使用这个数据

```vue
// 子组件
<template>
	<div>
		<h1>测试插槽功能</h1>
		<slot :msg="msg">默认值</slot>
	</div>
</template>

<script>
	export default {
		name: "SlotTest",
		data() {
			return {
				msg: "hello",
			};
		},
	};
</script>
```

```vue
// 父组件
<template>
	<div>
		<slot-test>
            <!-- 特别注意这里是等于号+引号的v-slot！ -->
            <!-- 传到父组件里被v-slot接收的是一个对象！里面有msg这个属性，这里使用的是ES5的解构赋值-->
			<template v-slot="{ msg }">
				<span>作用域插槽功能,{{ msg }}</span>
			</template>
		</slot-test>
	</div>
</template>
```

在这个案例中我们也了解到`v-slot`在不同形式下的两种用法，它通过冒号指定插槽名称，通过等号指定作用域传来的数据内容，所以正式的`v-slot`用法即为`#[子组件插槽name]='{[子组件传出数据]}'`

```vue
<template #test="{ msg }">
	<span>{{ msg }}</span>
</template>
// 其中子组件
<slot :msg="msg" name="test">默认值</slot>
```

作用域插槽一般用于父组件指定标签结构，子组件提供数据的情况

## Vuex

它是专门在Vue中实现集中式状态管理的一个插件，它可以对Vue应用中多个组件的共享状态进行集中式的管理，同时也是一种组件间通信的方式

假设我们还是使用全局事件总线进行一大堆组件的通信，比如A组件中的某个值其他一大堆组件都需要使用，因此在我们目前看来只能在每一个要使用这个数据的组件内`$on`一个事件，再由A组件`$emit`一下才能实现，但这显然比较麻烦，虽然确实`$bus`谁都能用，但是似乎并没有什么工具对其进行管理，频繁的调用事件效率十分低下，如果我们有另一个类似全局变量池的地方既能帮助我们管理数据，对于每一个独立的组件都能访问这个全局变量池，同时可以实时对其上的数据进行修改等等操作，岂不美哉

这时候，Vuex就出现了

### 原理图

Vuex有三个重要的组成部分，分别是`Actions`、`Mutations`和`State`，我们需要保管的数据交由`State`对象进行保管，而我们需要对保管的数据进行操作时（`dispatch`）我们会先将指令交给`Actions`去检查和整理，接着我们将被`Actions`整理好的数据进行`commit`，然后`Mutations`就会将数据进行操作并更新到`State`中，并对我们页面上的数据重新进行渲染，于是我们只需要在组件内调用Vuex提供给我们的几个api，就可以对Vuex中保管的数据进行操作

![vuex](https://vuex.vuejs.org/vuex.png)

这么一讲好像`Actions`比较多余，确实当我们已知操作的所有内容时直接可以`commit`跳过`Actions`，但是如果我们对数据操作的某个步骤不清楚，需要请求后端时，`Actions`就会自动帮助我们请求后端内容

这样好像组件是用户，`Actions`是服务员，`Mutations`是厨师，`State`是菜，我们当然可以直接叫厨师给我们做饭，但是服务员可以将我们点的菜进行分析并给出建议，同时将我们的菜记录到菜单中，这些都是只会做菜的厨师没办法做到的

同时Vuex的三个组件都是在store大的对象的领导之下的，因此我们在使用api的过程中调用的都是`store.xxx`，这在图中没有体现，需要注意

### 基础使用

首先我们还是先要安装Vuex，`npm install vuex@3.6.2`，因为我们目前还没用到Vue3，因此需要指定版本号，用最新的四点多的版本会出问题

接着在`main.js`里面引入一下，顺便尝试在`store`里面存个值试试

```js
import Vue from 'vue'
import App from './App.vue'
import Vuex from 'vuex';

Vue.config.productionTip = false
Vue.use(Vuex)

new Vue({
	el: '#app',
	render: h => h(App),
	store: 'hello',
})
```

接着我们可以在所有的vc和vm上看到存在一个`$store`属性，并且内部有一个`hello`值

但是这样显然和前面讲过的组成部分一点关系没有，因此我们需要真正创建一个store

### 简单案例

Vuex由于是和Vue同一个团队开发的，因此我们如果需要使用Vuex，正确的做法就是和创建vm一样创建一个Vuex实例

当然Vuex要求我们在创建实例的时候应该提前导入Vuex插件，同时官方也建议我们在创建实例时应该额外创建一个`store/index.js`用以存储Vuex实例

于是我们在根目录下创建一个`store/index.js`，接着在里面写上上面所示的三个内容

```js
// index.js
import Vuex from 'vuex';
import Vue from 'vue';

Vue.use(Vuex)

const actions = {
	// 业务逻辑写在这，写完之后调用commit
	handle(context, value) {
		// 我们在这里还可以通过context.dispatch调用其他处理逻辑
        // 当然我们
		value += "!"
		context.commit('EXEC', value)
	}
}
const mutations = {
	// 对state的操作写在这里，注意函数名最好大写
	EXEC(context, value) {
		// 注意这里不是context.state.x，Vuex直接把整个x都给你了
		context.x.push(value)
	}
}
const state = {
	// 所有全局数据都保存在这，之后在页面中通过this.$store.state.x访问
	x: []
}

export default new Vuex.Store({
	actions,
	mutations,
	state
})
```

```js
// main.js
import Vue from 'vue'
import App from './App.vue'
import store from './store';

Vue.config.productionTip = false

new Vue({
	el: '#app',
	render: h => h(App),
	store,
	beforeCreate() {
		Vue.prototype.$bus = this  // 安装全局事件总线
	},
})
```

```vue
// 父组件,App.vue
<template>
	<div>
		<vuex-test />
	</div>
</template>

<script>
	import VuexTest from "./components/VuexTest.vue";
	export default {
		name: "App",
		components: { VuexTest },
	};
</script>
```

```vue
// 子组件
<template>
	<div>
		<ul>
			<li v-for="(item, index) in $store.state.x" :key="index">{{ item }}</li>
		</ul>
		<input type="text" v-model="x" />
		<button @click="dispatchV(true)">添加一个元素</button>
		<button @click="dispatchV()">添加一个元素并加感叹号</button>
	</div>
</template>

<script>
	export default {
		name: "VuexTest",
		data() {
			return {
				x: "",
			};
		},
		methods: {
			dispatchV(f = false) {
                // 如果不需要数据处理可以直接调用commit
				if (f) this.$store.commit("EXEC", this.x);
				else this.$store.dispatch("handle", this.x);
			},
		},
	};
</script>
```

这样就实现了一个简单的添加内容的业务逻辑

![image-20220323224855030](https://s2.loli.net/2022/03/23/aoN52FEHiYwUJkK.png)

### Getters

Vuex还有一些不必需配置项，当我们需要的时候也可以在其中进行配置

其中有一个`getters`配置项和组件内的`computed`计算属性非常类似，只不过是全局版的，我们只需要在其中编写函数对`state`数据源中数据进行操作，之后在页面中调用`{{$store.getters.[函数名]}}`即可使用Vuex内置的计算属性

```js
const getters = {
	xNew(state) {
		return state.x[0] + "!!"
	}
}

export default new Vuex.Store({
	actions,
	mutations,
	state,
	getters
})
```

### mapState/mapGetters

我们会发现上面的代码中在页面里我们频繁的使用`$store.state.xxx`调用，一旦Vuex管理的数据越来越多，我们可能在页面中写的同样的代码也越来越长，这样显然不符合代码的简洁原则，因此Vuex提供了map方法帮助我们批量的生成简便形式的参数名

我们只需要在前引入`mapState`和`mapGetters`即可

可以将之前的代码改为

```vue
<template>
	<div>
		<ul>
			<li v-for="(item, index) in x" :key="index">{{ item }}</li>
		</ul>
		<div>{{ xNew }}</div>
		<input type="text" v-model="x1" />
		<button @click="dispatchV(true)">添加一个元素</button>
		<button @click="dispatchV()">添加一个元素并加感叹号</button>
	</div>
</template>

<script>
	import { mapState, mapGetters } from "vuex";
	export default {
		name: "VuexTest",
		data() {
			return {
				x1: "",
			};
		},
		computed: {
			// 下面代码等价于
			// x(){
			// 	return this.$store.state.x
			// }
			...mapState({ x: "x" }), // 不能简写为｛x},因为属性值不是变量
			// 当存在属性名和字符串内容一致时，可以写为数组形式...mapState(['x'])
			...mapGetters(["xNew"]), // 同上
		},
		methods: {
			dispatchV(f = false) {
				if (f) this.$store.commit("EXEC", this.x1);
				else this.$store.dispatch("handle", this.x1);
			},
		},
	};
</script>
```

### mapActions/mapMutations

当然我们也可以对`methods`里面的内容进行简写

同上引入`mapActions`和`mapMutations`之后，我们只需要在methods内仿照上面的样子写即可

但是注意在调用方法的时候注意要手动传入value值，对于上述的案例只需要修改dispatchV即可

```vue
		methods: {
			...mapActions(["handle"]),
			...mapMutations(["EXEC"]),
			dispatchV(f = false) {
				// 注意调用生成的方法时传入给Mutation的value值this.x1
				if (f) this.EXEC(this.x1);
				else this.handle(this.x1);
			},
		},
```

### 模块化设计

当我们的Mutations和Actions里面的内容越来越多的时候，我们的Vuex也需要进行模块化拆分，将部分包括`Actions`、`Mutations`、`State`等等内容拆分再重新打包，那么我们只需要对每一个模块进行命名，接着在创建`Vuex.Store`的时候添加`modules`属性即可

```js
const moduleA = {
	actions:{},
	mutations:{},
	state:{},
	getters:{}
}
const moduleB = {
	actions:{},
	mutations:{},
	state:{},
	getters:{}
}
export default new Vuex.Store({
	modules:{
		moduleA,
		moduleB
	}
})
```

接着在页面中引入时只需要比如`...mapState(['moduleA',moduleB])`，接着在页面中引用时需要`{{moduleA.x}}`即可

当然可能会觉得每一个属性都要`moduleA.`很不爽，那么我们就需要在定义`moduleA`的时候添加一个属性`namespaced:true`，接着在mapState中多传一个参数`...mapState(moduleA,['x'])`，这样我们在页面中就可以直接`{{x}}`引用了，如果还需要引用`moduleB`的，那么必须得在加一个`mapState`了，其他的map都类似

当然如果不知道map这个东西，我就要硬用`$store`取值，那么我就要这样写`$store.state.moduleA.x`，而如果要调用方法，则`$store.commit('moduleA/EXEC',this.x1)`这么写，注意要`/`斜杠分开，而且如果调用getters会发现更加复杂，直接不演示了

这么一对比简写方式就很香了

## router

路由就是一个对应关系，将某一个key与另一个value进行配对，同时所有的路由都需要有一个路由器进行管理才有意义

Vue里的路由效果与之十分类似，通过它，我们可以实现炫酷的单页面应用（SPA）

经典的实际案例就是当我们点击某个网站的导航栏时页面中的内容可以在页面中显示不同内容，但是导航和页脚都是不变的

这个Vue中的路由器会监测浏览器的地址变化，与预置的内容进行比对，只要比对上了，就会响应预先配置好的组件进行展示，而同样这个请求也会通过AJAX的方式被发送到后端，后端通过地址的信息去处理返回给我们要显示的组件的必要数据，从而实现完整的页面展示

### 简单的使用

同样它也是一个插件库，我们如果需要在vue2中使用也和vuex差不多，`npm i vue-router@3`即可

同样的，由于这两个插件都是Vue团队开发的，因此我们依葫芦画瓢，同样要在根目录下创建一个`router`目录，同时在里面创建`index.js`文件，里面的内容是这样的

```js
// 该文件专门用于创建整个应用的路由器
import Router from 'vue-router';
import RouterF from '../pages/RouterF.vue';
import RouterS from '../pages/RouterS.vue';

// 创建一个路由器
export default new Router({
	routes: [
		{
			path: '/demo1',
			component: RouterF
		},
		{
			path: '/demo2',
			component: RouterS
		}
	]
})
```

可以看出来，在这里我创建了一个路由器，并且让路由器给两个组件绑定了两个路径，这样我们路由器的配置项就写完了

接下来同样学着Vuex的样子，修改`main.js`的内容，使用路由插件内容

```js
import Vue from 'vue'
import App from './App.vue'
import router from './router';
import VueRouter from 'vue-router';

Vue.config.productionTip = false
Vue.use(VueRouter)

new Vue({
	el: '#app',
	render: h => h(App),
	router
})
```

之后我们会发现页面的地址栏中的最后出现了`/#/`的标识，意味着我们的路由器已经在正常运行了

然后我们需要在引用被路由代理的组件的组件里写上`<router-link>`标签和`<router-view>`标签，用于为用户实现交互和展示预定组件，此时在页面中我们只需要点击`<router-link>`标签内容（相当于一个`<a>`标签），那么在`<router-view>`标签中就会显示当前路由到的组件内容`/demo1->RouterF...`（等于是将`<router-view>`标签替换为了`<RouterF/>`）

正因为路由代理组件不再需要在父组件中编写组件标签的方式引入组件内容，因此我们常常对被路由管理的组件单独拎出来放在`pages`目录中（范例中的`RouterF`和`RouterS`），而普通的组件内容则放在components目录里

```vue
// 父组件,App.vue
<template>
	<div>
		<!-- 这个router-link和a标签完全一致，只需要修改href到to属性即可 -->
        <!-- 内部active-class可以指定被选中时展示的样式 -->
		<router-link to="/demo1" active-class="">查看第一个测试页面</router-link>
		<router-link to="/demo2">查看第二个测试页面</router-link>
		<!-- 在这里展示个性化内容 -->
		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
	};
</script>
```

```vue
// pages/RouterF.vue
<template>
	<h2>这是第一个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
	};
</script>
// RouterS与此类似
```

接着我们就可以在页面中看到完整效果了

![image-20220326124154938](https://s2.loli.net/2022/03/26/gJPkbixLQv6eulK.png)

> 如果我们查看被路由管理的组件内容，我们会发现里面的vc实例中出现了`$route`和`$router`两个属性，这两个属性分别代表了我们在路由`index.js`配置的路由信息（即数组中的每一项）和这些组件的路由器信息（即new的Router），其中路由信息每一个组件不同，但是路由器是组件间共用的，其中的方法使用之后会提到
>

### 嵌套

当我们在一个路由到的组件中想要继续配置路由结构，即继续配置子路由，那么我们就需要在`index.js`中给需要配置路由的配置项添加`children`属性，比如下面这样

```js
{
    routes:[
        {
            path:'/father',
            component:Father
            children:[
            	{
					path:'son',  // 注意不要加横杠
            		component:Son,
        		}
            ]
        }
    ]
}
```

接下来我们就可以通过在组件内的`<router-link>`标签中添加路径`/father/son`即可

### query传参

上面的案例有一些问题，因为界面中的内容变化不大，即仅变化了一个字，但是我们为了展示变化不大的内容却用到了两个组件，没有满足组件间的复用要求，有没有一种办法，我们仅用一个组件，同时告诉路由往该组件中传入不同的参数，实现页面内容的变化呢？

此时我们就需要用到get请求的知识，假装发了一个请求，实际上每一个子组件内将会收到地址栏中传入的参数，根据这个参数调整显示内容即可

```vue
// 父组件,App.vue
<template>
	<div>
		<!-- 直接将to写成对象模式，推荐 -->
		<router-link
			:to="{
				path: 'demo1',
				query: {
					id: 1,
				},
			}"
			active-class=""
		>查看第一个测试页面</router-link>
		<!-- 模版字符串，里面可以加变量的引用 -->
		<router-link :to="`/demo1?id=2`">查看第二个测试页面</router-link>

		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
	};
</script>
```

```vue
<template>
	<h2>这是第{{ $route.query.id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
	};
</script>
```

### params传参

#### 命名

当我们的路由嵌套层级越来越多的时候，我们每一次在页面中引用都显得很麻烦，因此我们可能需要一个简写形式，这时候就可以在路由器的配置中给指定的路由结构增加一个name属性，紧接着在页面中引用时直接`:to="{name:'[name名]'}"`，即可快速访问指定路由，但是必须写成对象形式

#### params

但是可能会觉得这种方式定义name还是有点反人类，不知道为什么要这么做，直接写路径不香吗？其实是因为给通过params传参提供方便，这是除了query之外另一种传递参数的方式

在之前的学习中我们知道了地址通过Restful传参的方式，实际上params传参就是利用Restful进行的，我们只需要如此配置

```js
// 该文件专门用于创建整个应用的路由器
import Router from 'vue-router';
import RouterF from '../pages/RouterF.vue';
import RouterS from '../pages/RouterS.vue';

// 创建一个路由器
export default new Router({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF
        },
        {
            path: '/demo2',
            component: RouterS
        }
    ]
})
```

```vue
// 父组件,App.vue
<template>
	<div>
		<!-- 对象式传参，注意必须是name属性，如果还是path会报错 -->
		<router-link
			:to="{
				name: 'demo1',
				params: {
					id: 1,
				},
			}"
			active-class=""
		>查看第一个测试页面</router-link>
		<!-- Restful风格传参 -->
		<router-link :to="`/demo1/2`">查看第二个测试页面</router-link>

		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
	};
</script>

```

```vue
<template>
	<h2>这是第{{ $route.params.id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
	};
</script>
```

可以发现在params传参的过程中，如果涉及到参数传递的对象写法，那么就必须通过指定name的方式进行传递，但是总体上来说和query的取得参数区别不大，具体怎么选择就看个人习惯了

#### props

除此之外，我们可能会发现在子组件内调用父组件传过来的参数时，似乎也不是那么方便，我们每次都要写一个`$route.params/query.xx`的方式调用参数，一旦传过来的参数变多了，写一大堆内容显得十分繁琐，此时我们就需要借助路由器的props属性，它可以帮助我们简化组件内代码

```js
export default new Router({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF,
            // 第一种写法，将参数写死
            // props:{id:1}
            // 第二种写法，直接打开，router默认会将params里面携带的参数变成props的内容传给子组件
            // props:true
            // 第三种写法，函数方式返回值，可以指定接收参数，参数为将要传给子组件的route对象
            props(route) {
                return { id: route.params.id }
            }
        },
        {
            path: '/demo2',
            component: RouterS
        }
    ]
})
```

这三种方式的效果都是一样的，会给子组件内通过props传入一个id属性，当然指定props参数之后我们还需要在组件内接收

```vue
<template>
	<h2>这是第{{ id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
		props: ["id"],
	};
</script>
```

### 编程式导航

我们发现我们现在进行跳转的时候必须将跳转内容设置在`<router-link>`也就是最后显示的`<a>`标签上，但是实际开发中我们肯定不止会在`<a>`标签上添加跳转需求，比如目标是一个按钮，那目前我们就一筹莫展了

此时就需要进行编程式导航了，而实现这个方法的基础，就是每个路由组件身上的`$router`属性

```vue
// 父组件,App.vue
<template>
	<div>
		<button @click="showD()">按钮实现查看第一个页面</button>
		<router-view>内容</router-view>
	</div>
</template>

<script>
	import RouterF from "./pages/RouterF.vue";
	import RouterS from "./pages/RouterS.vue";
	export default {
		name: "App",
		components: { RouterF, RouterS },
		methods: {
			showD() {
				this.$router.replace({
					name: "demo1",
					params: {
						id: 1,
					},
				});
			},
		},
	};
</script>
```

> 其中`$router.replace`可以替换为`$router.push`，其他都一样，他们的区别是路由之后可不可以回退到上一次的操作界面，如果设置为`replace`那么按下本次操作之后浏览器上的后退按钮就无法回退到按下按钮前的页面
>
> 另外`$router`还有`back()/forward()/go()`，他们的效果和浏览器的后退和前进按钮差不多

### 新生命周期钩子

#### 缓存路由组件

我们如果为两个路由组件添加了`beforeDestroy`钩子，那么我们会发现当展示的组件进行切换的时候，上一个展示的组件立即被销毁了，意味着每一次点击后产生的页面vc实例都是不一样的，路由器帮助我们对不需要使用的实例内容进行销毁

但是有时候比如当页面上存在表单的时候用户输了一大堆内容结果不小心将界面切走了，切回来的时候由于产生了一个新的实例，因此表单内的数据都不存在了，这时候我们就需要将填写表单的页面进行缓存，以便下一次回到页面的时候能够重新展示内容

此时我们只需要在`<router-view>`标签外包一个`<keep-alive>`标签就可以了

```html
<keep-alive include="RouterF">
    <router-view>内容</router-view>
</keep-alive>
```

注意include里面一定是**组件名**，就是组件内的name属性

#### activated/deactiveted

但是虽然我们知道了可以避免组件销毁，但是比如我们在缓存组件中开了一个定时器，那么在组件切换的过程中我们后台的定时器依旧在运作，一旦类似组件越来越多也会极大的占用资源，因此我们需要一个钩子来对我们是否切换出组件做一个判断

这时就引入了两个新的生命周期钩子，他们分别代表组件被启动和组件被切走（无论是否配置`keep-alive`，比起直接在`beforeDestroy`钩子里写内容，用这两个钩子能够更方便的对路由组件进行管理

### 路由守卫

路由守卫就是保护路由的权限，用于保护用户的信息安全，比如用户的用户中心，当然需要当用户登录时判断用户信息才决定究竟是否能够查看，这时候就需要配置路由守卫

#### 全局

```js
const router = new VueRouter({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF,
            props(route) {
                return { id: route.params.id }
            },
            meta: { a: 123 }
        },
        {
            path: '/demo2',
            component: RouterS
        }
    ]
})

// 前置路由守卫，在每次页面初始化和路由切换的时候进行调用（即页面交互引起地址栏路径变化时）
router.beforeEach((to, from, next) => {
    // to和from可以查看当前路由组件和跳转到的路由组件内的$route属性信息，包括路径名称参数等信息
    // 同时我们还可以对每一个路由的meta属性进行编辑，使得我们可以在守卫里面拿到路由信息
    console.log(to, from, meta.a);
    // 在这判断是否对其放行，对放行的请求使用next函数
    next()
})

// 后置路由守卫，用的不多，在路由切换之后调用，可以配置一些页面标题之类的信息，没有next参数
router.afterEach((to, from) => {
    console.log(to, from);
})
export default router
```

![image-20220326195816873](https://s2.loli.net/2022/03/26/SegyQvjLTq7Z9Rh.png)

#### 独享

原理同上，在每一个路由之前添加`beforeEnter`属性即可

```js
const router = new VueRouter({
    routes: [{
            name: 'demo1',
            path: '/demo1/:id',
            component: RouterF,
            props(route) {
                return { id: route.params.id }
            },
            meta: { a: 123 },
            beforeEnter: (to, from, next) => {
                console.log(to, from)
                next()
            }
        }]
}
```

注意独享路由守卫没有后置守卫

#### 组件内

在组件内添加`beforeRouteEnter`和`beforeRouteLeave`属性即可，在从路由器进入组件的时候和从组件中离开的时候调用

```vue
<template>
	<h2>这是第{{ id }}个测试文件</h2>
</template>

<script>
	export default {
		name: "RouterF",
		props: ["id"],
		beforeRouteEnter(to, from, next) {
			console.log(to, from);
			next();
		},
		beforeRouteLeave(to, from, next) {
			console.log(to, from);
			next();
		},
	};
</script>
```

注意两个方法都有next参数

### 项目上线

当前我们会发现我们的所有地址前面都有一个`#`号，十分的不美观，导致的原因其实是路由默认使用了hash模式，我们只需要在定义路由器时指定为`mode:history`即可

```js
const router = new VueRouter({
    mode: 'history',
    routes: [
        ...
    ]
})
```

接着我们在浏览器中路由到指定内容就会在地址栏显示仅以`/`分隔的地址了

![image-20220326210813514](https://s2.loli.net/2022/03/26/oeFBvLpItwqu8DJ.png)

但是当项目正式上线的时候，这种history风格的地址名很可能会给后端带来困扰，因为前端路由是不发送请求的，因此我们很可能在点了半天之后一按刷新，于是给后端发了一个不存在的请求，从而产生404错误，当然为了好看我们可以解决一切问题，其中如果用Nginx作为代理服务器，仅一行代码就可以[解决问题](https://router.vuejs.org/zh/guide/essentials/history-mode.html#nginx)

但是做好的前端项目如何上线呢，我们就需要通过`npm run build`来打包项目，接着会在当前目录下生成一个dist文件，里面有我们写的纯html和css，js文件，当然直接打开`index.html`是行不通的，模块化处理需要我们搭建一个服务器管理项目，比如直接将里面内容拷贝粘贴到在本机的Nginx上默认目录下即可

## ElementUI

Vue最好的UI库还得是饿了么UI，当然也有别的各种不同的UI库可以用，但是一通俱通，我们就拿ElementUI作为例子

官网在这，直接按照里面的内容依葫芦画瓢即可，但是其中有些内容可能过时了，因此我们需要进行一下修改

最后的文件修改内容如下

- `main.js`

  ```js
  import Vue from 'vue'
  import App from './App.vue'
  
  Vue.config.productionTip = false
  
  // 所有的组件都被注册了，发的包会很大
  // import ElementUI from 'element-ui' 
  // import 'element-ui/lib/theme-chalk/index.css';
  // Vue.use(ElementUI)
  
  // 按需引入
  import { Button, Row } from 'element-ui';
  Vue.component(Button.name, Button)
  Vue.component(Row.name, Row)
  
  new Vue({
      el: '#app',
      render: h => h(App),
  })
  ```

- `babel.config.js`

  ```js
  module.exports = {
      presets: [
          '@vue/cli-plugin-babel/preset', ["@babel/preset-env", { "modules": false }]
      ],
      "plugins": [
          [
              "component",
              {
                  "libraryName": "element-ui",
                  "styleLibraryName": "theme-chalk"
              }
          ]
      ]
  }
  ```

- `App.vue`

  ```vue
  <template>
  	<div>
  		<el-row>
  			<el-button>Default</el-button>
  			<el-button type="primary">Primary</el-button>
  			<el-button type="success">Success</el-button>
  			<el-button type="info">Info</el-button>
  			<el-button type="warning">Warning</el-button>
  			<el-button type="danger">Danger</el-button>
  		</el-row>
  	</div>
  </template>
  
  <script>
  	export default {
  		name: 'App',
  	}
  </script>
  ```

即可运行

# Vue3

终于进入了Vue3的学习，从上面对于Vue2的学习，我们还是发现了Vue2的某些缺陷，于是Vue3应运而生，它

- 打包大小减少41%
- 初次渲染快55%，更新渲染快133%
- 内存减少54%

还有更多乱七八糟的更新，牛逼就完了

## 简单使用

1. 为了避免和之前的内容相重复出现问题，因此我们先直接卸载所有模块

   `npm uninstall * && npm rm -rf node_module package.json package-lock.json`，如果不知道`node_module`在哪，可以通过`npm root`查看，并通过`npm ls`看看是不是真的卸载成功

2. 安装vue，同时我选择不安装脚手架，直接梭哈另一个Vue团队开发的前端构建工具vite

3. 在想要的目录下部署vite项目文件`npm create vite@latest`然后跟着选项一路选下来即可

4. vite并没有预先帮助我们下载好依赖包，因此我们需要`cd vite-project && npm install`来安装内容

5. `npm run dev`启动项目，接着可以在`localhost:3000`看到部署的项目

## 文件结构

进入项目目录，我们发现大体上的文件结构和Vue2十分类似

![image-20220327100533896](https://s2.loli.net/2022/03/27/KhYbvEiatZdRxpF.png)

因此我们还是从入口文件`main.js`开始分析，众所周知这里应该就是原本我们创建vm的地方

```js
// 引入的不是Vue构造函数了，引入的是名为createApp的工厂函数
import { createApp } from 'vue'
import App from './App.vue'

// 可以直接调用这个函数
const app = createApp(App) // 页面容器的id
app.mount('#app') // 挂载
console.log(app); // 这个app比起下面之前写的vm显得非常的轻量
// app.unmount('#app')  // 我们也可以直接通过unmount解除挂载，页面上的东西直接没了

// const vm new Vue({
// 	render:h=>h(App)
// })
// vm.$mount('#app')
```

 可以发现初始的代码就三行，明显比之前简单了许多，而进行逐行分析我们还是可以发现与Vue2的`main.js`一对比相似程度还是很高的，但是Vue3更加精简了我们需要编写代码的内容，仅需要一行，就达到了我们之前`new Vue...`一大堆的配置内容

接着我们看一看预先给我们配置好的`App.vue`组件内容

```vue
<script setup>
	// This starter template is using Vue 3 <script setup> SFCs
	// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
	import HelloWorld from './components/HelloWorld.vue'
</script>

// Vue3可以没有根标签
<template>
	<img
		alt="Vue logo"
		src="./assets/logo.png"
	/>
	<HelloWorld msg="Hello Vue 3 + Vite" />
</template>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
```

总的结构和之前大差不差，只是多了一个setup标签属性和在template内的多个标签内容，不过还是可以勉强进行阅读的

稍微对目录结构有了一个大致的印象，接下来就可以开始Vue的学习了

## Composition API

一看这标题名字是什么鬼啊，暂且将其理解为组合式API，这是Vue3运行的基础，而接下来所有的学习内容都是组合式API的一部分，我们会发现在使用这些函数的时候我们都需要在顶部加上`import ... from 'vue'`来引入这些API，不然在页面运行时会报错，而这些API都需要写在setup中才能被使用，如果还是不理解，我们在接下来的学习中一定会不断的接触这个概念

### setup

它是所有Compositon API表演的舞台也是接下来内容中唯一不需要引入的配置项，是Vue3新的配置项，是一个函数，组件中所用到的所有的数据方法都要配置在这

```vue
<script>
	export default {
		name: 'App',
		setup() {
			let name = '123'
			function sayHi() {
				alert(`${name},hi!`)
			}
			return {
				name,
				sayHi
			}
		}
	}
</script>

<template>
	<h2>{{name}}</h2>
	<button @click="sayHi">欢迎</button>
</template>
```

除了setup函数之外，几乎没有别的任何不同，同时setup返回的对象属性和方法可以直接在页面模版对象中使用，相当于在之前配置了data和methods项

借助提供的`script setup`标签，我们还可以进一步简化代码

```vue
<script setup>
	let name = '123'
	function sayHi() {
		alert(`${name},hi!`)
	}
</script>
```

> 要注意的是setup函数执行的时机比beforeCreate还要早，同时它的this是undefined

### ref

此时上面这个案例是没有存在响应式的，就算我们在函数内`name='234'`但是反映到页面中并不会修改页面内容，因为Vue3没有对里面的这个参数进行跟踪，如果我们想要让他真的变成原本Vue2中的`data`属性，我们就要借助ref对setup内的参数进行包装，使得在内部函数修改之后能够正确响应到页面上

```vue
<script setup>
    // 引入ref函数
	import { ref } from 'vue'
	// 因为ref产生一个代理对象，因此使用const来接收内容
	const name = ref('123')
    // 定义对象类型的响应数据
	const person = ref({
		name: '123',
		age: '456',
	})
	function sayHi() {
		// 这样就可以修改数据了
		name.value = '234'
		person.value.name = '345' // 只需要一个value
	}
</script>

<template>
	<h2>{{ name }}</h2>
	<button @click="sayHi()">欢迎</button>
</template>
```

至于为什么修改数据时需要调用`value`属性，其实是由于ref默认帮我们给数据打包成了一个`RefImpl`对象，我们可以通过控制台输出来确认，而我们的数据，正是存在这个对象中的`value`属性中

### reactive

reactive专门用以定义对象类型的响应数据，当然ref也可以定义对象类型，但是reactive作为管理响应对象的专家，显然有它的优势

```vue
<script setup>
	import { reactive } from 'vue'
	const reac = reactive({
		name: '234',
	})
	function test() {
        // 不需要加value，直接修改即可
		reac.name = '456'
	}
</script>

<template>
	<h2>{{ reac.name }}</h2>
	<button @click="test()">改名</button>
</template>

```

如果我们输出reac变量和上面通过ref定义的person对象，我们会发现两个对象的内容其实都是一个Proxy响应对象，意味着Vue3为了达到响应式的对象内容将我们定义的对象变成了一个个Proxy实例

```js
console.log(person)
console.log(reac)
```

![image-20220327171006923](https://s2.loli.net/2022/03/27/1Eu4TyUDt7Xsoip.png)

这也说明了为什么我们使用ref的时候修改对象内属性不是`person.value.name.value`，因为有比起Vue2更强大的Proxy类型帮我们对对象进行响应式操作

Proxy更强大的地方在于，只要把需要监测的对象丢给它，无论对象里面是怎么复杂的结构，不管到底里面还包了几层对象，只要其中某个对象的某个值被修改了，就一定会被Proxy监测到，不仅是对象，Proxy还支持数组的监测，对我们而言，也就只需要将数组内容抛给`reactive`方法就行了

也就是说Proxy除了不能处理，已经是全面碾压ref了（因为ref还是使用的是Vue2的`$getter`和`$setter`实现响应式），既然Proxy这么强大，因此不到万不得已，我们一般都不会使用ref了（甚至可以自创一些对象为了不使用ref）

### 响应式原理

Vue2要修改数组内容，必须使用给定的五个数组修改方法，或者直接换一个数组，或者使用`this.$set`方法，但是Vue3有了Proxy，可以直接通过下标来修改数组内容，一样会被监测到，不仅如此，反正只要setup方法把其中定义的对象交出去了，不管你在里面函数里怎么调教定义的属性，Vue3都能监测到对被Proxy管理的属性

那为什么这个Proxy那么给力呢，这时候就需要介绍Vue3的响应式原理了，为了形成对比，我们可以先复习一下Vue2的[响应式原理](#Object.defineProperty)

强大的Proxy实现主要还是靠`window.Proxy`这个内置对象和`Reflect`反射对象的内容操作，我们不妨对Vue3中的响应式数据操作进行简单的模拟，先看案例

```html
<body>
    <script>
        const person = {
            name: '测试',
            age: 12
        }
        const p = new Proxy(person, {
            // 查
            get(target, propsData) {
                console.log(`检测到你读取了${propsData}`)
                return Reflect.get(target, propsData)
            },
            // 增和改
            set(target, propsData, value) {
                console.log(`检测到将${target[propsData]}修改为${value}`)
                Reflect.set(target, propsData, value)
            },
            // 删
            deleteProperty(target, propsData) {
                console.log(`检测到删除${propsData}`)
                return Reflect.deleteProperty(target, propsData)
            }
        })
    </script>
</body>
```

![image-20220327183551590](https://s2.loli.net/2022/03/27/hTHKmpdrsC3ENOv.png)

可以发现创建的这个Proxy代理实例p，不仅能对所有他自己身上属性的修改并对person进行镜像操作，同时对于自己身上的每一次修改都能够被内置的方法所监测到，而这个比起Vue2中单纯的只有get和set方法的`defineProperty`阉割版数据代理不知道强到哪里去了

同时顺便提一下Reflect反射对象，其中内置了很多正常使用也完全没问题的镜像方法，比如说上面的代码可以直接用我们常用的形式替换，比如`Reflect.get(target, propsData)`完全等价于`target[propsData]`，但是优点是通过反射对象所进行操作无论成不成功都不会以报错的方式展示（一旦报错程序立即终止，整个项目就瘫痪了），而是在返回值中确定操作是否被完成，这样对于大型框架的开发有着举足轻重的作用，完全可以通过返回值人为设置一些友好的报错信息，不然就得在代码中写满`try...catch`了

### 传参/事件/插槽

作为父组件给子组件传递的三个内容，由于Vue3中不再有methods属性了，因此也需要提一下，直接给一个样例就过

```vue
// 父组件
<template>
	<div>
		<Demo02 @event="showEvent" :msg="msg">
			<template #test="{ msg1 }">
				<h2>这是一个插槽内容,从子组件传来的参数为{{ msg1 }}</h2>
			</template>
		</Demo02>
	</div>
</template>
<script>
	import Demo02 from './components/Demo02.vue'
	export default {
		name: 'App',
		components: { Demo02 },
		setup() {
			const msg = 'test'
			function showEvent(value) {
				console.log(`触发了event事件，收到了${value}参数`)
			}
			return {
				showEvent,
				msg,
			}
		},
	}
</script>
```

```vue
// 子组件
<template>
	<h1>从父组件中获得的参数为{{ data.para }}</h1>
	<button @click="execEvent">按下触发事件</button>
	<span v-show="data.flag">事件被触发了</span>
	<slot name="test" :msg1="data.msg1">默认值</slot>
</template>

<script>
	// 当然如果组件内需要配置多个属性项，自然是不适合用setup的语法糖效果的
	import { reactive } from 'vue'
	export default {
		name: 'Demo2',
		props: ['msg'],
		emits: ['event'],
		// setup可以收到两个参数，分别是父组件里传过来的参数内容(props)和调用开启事件的上下文(context)
		// 当然context的用处不仅是开启事件
		// 如果前面没有声明props属性，那么父组件传过来的参数就会被放在context.attr中
		// 而父组件传入的插槽信息也会存在context.slot里
		setup(props, context) {
			// 一定要记得写reactive内容，不然所有的修改都会失效
			const data = reactive({
				msg1: 123,
				// 将父组件的传参通过行参的方式传给子组件，避免了父组件的参数被直接调用修改，子组件要在页面上使用就必须重新赋一个变量
				para: props.msg,
				flag: false,
			})
			function execEvent() {
				data.flag = true
				context.emit('event', 123)
			}
			return {
				execEvent,
				data,
			}
		},
	}
</script>
```

![image-20220327202006594](https://s2.loli.net/2022/03/27/QCMtfOHNoPzxLR8.png)

注意当子组件与父组件有信息交互的时候，不能用setup语法糖

### computed

Vue3同样支持计算属性，具体代码如下

```vue
<template>
	<input type="text" v-model="data.name" />
	<input type="text" v-model="data.age" />
	<br />
	<span>{{ merge }}</span>
</template>

<script setup>
	import { reactive, computed } from 'vue'
	const data = reactive({
		name: 'test',
		age: 12,
	})
	const merge = computed(() => {
		return data.name + '-' + data.age
	})
</script>
```

其中`computed`也是简写形式，具体的形式可以使用`get`和`set`方法，和Vue2差不太多

### watch

Vue3里面的watch就比较奇葩了，一共会分为六种情况，需要分别掌握

```vue
<template>
	<button @click="name += '1'">修改ref属性name</button>
	<button @click="data.name += '1'">修改reactive属性data.name</button>
	<button @click="data.obj.a.b++">修改reactive属性obj.a.b</button>
</template>

<script setup>
	import { ref, reactive, watch } from 'vue'
	let name = ref('test1')
	let age = ref(12)
	const data = reactive({
		name: 'test',
		age: 12,
		obj: {
			a: {
				b: 1,
			},
		},
	})
	watch(name, (newValue, oldValue) => {
		console.log('第一种情况，监视单个ref属性', newValue, oldValue)
	})
	watch([name, age], ([newname, newage], [prevname, prevage]) => {
		console.log('第二种情况，监视多个ref属性', newname, newage)
	})
	watch(data, (newValue, oldValue) => {
		console.log('第三种情况，监视单个reactive对象，则oldValue无效，无法知道谁被修改了', newValue, oldValue)
	})
	watch(
		() => data.name,
		(newValue, oldValue) => {
			console.log('第四种情况，监视单个reactive对象的某个属性', newValue, oldValue)
		},
	)
	watch([() => data.name, () => data.age], ([newname, newage], [prevname, prevage]) => {
		console.log('第五种情况，监视多个reactive对象的多个属性', newname, newage)
	})
	watch(
		() => data.obj,
		(newValue, oldValue) => {
			console.log('第六种情况，监视reactive对象里的深度属性', newValue, oldValue)
		},
		{ deep: true, immediate: true },
	) // 在这里可以配置Vue2里面提到过的参数内容
</script>

```

![image-20220327212538758](https://s2.loli.net/2022/03/27/fUdjECZaiQ7PAch.png)

同时还需要注意监视ref的时候不应该加`.value`，因为我们监视的必须是一个结构而不是单单的一个值

#### watchEffect

Vue3还提供了一个过程监视的方法， 有点类似计算属性，但是不返回计算结果给某个变量，调用这个方法时会自动检测在此代码块中的参数内容，一旦发生改变便会自动调用这个函数

```vue
<template>
	<button @click="data.name += '1'">修改reactive属性data.name</button>
</template>

<script setup>
	import { reactive, watchEffect } from 'vue'
	const data = reactive({
		name: 'test',
		age: 12,
	})
	watchEffect(() => {
		// 一些包含了参数内容的业务逻辑，只需要当里面参数的内容被修改就会调用
		console.log('当前的data.name被修改了', data.name)
		// 上面代码调用了data.name，因此我们不需要指定去监视它
		// 由于注重过程内容，因此不需要返回值
	})
</script>
```

### Vue3生命周期

Vue3取消了Vue2中的`beforeDestroy`和`Destroy`两个生命周期，代替的是`BeforeUnmount`和`Unmounted`，代表着的是组件的卸载，在Vue2中组件不使用的时候会销毁，而在Vue3中销毁就是将其不再挂载在父组件上了，也不算难理解

同时Vue3为大多数生命周期钩子配置了组合式API，我们可以在setup属性中直接调用

```vue
// 子组件
<template>
	<div>
		<button @click="num++">num++</button>
	</div>
</template>

<script>
	import { ref, onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted } from 'vue'
	export default {
		setup() {
			console.log('----setup')
			let num = ref(1)
			onBeforeMount(() => {
				console.log('----BeforeMount')
			})
			onMounted(() => {
				console.log('----Mounted')
			})
			onBeforeUpdate(() => {
				console.log('----BeforeUpdate')
			})
			onUpdated(() => {
				console.log('----Updated')
			})
			onBeforeUnmount(() => {
				console.log('----BeforeUnmount')
			})
			onUnmounted(() => {
				console.log('----Unmounted')
			})
			return {
				num,
			}
		},
		beforeCreate() {
			console.log('----beforeCreate')
		},
		created() {
			console.log('----create')
		},
	}
</script>
```

```vue
// 父组件
<template>
	<button @click="isShow = !isShow">是否显示</button>
	<Demo05Vue v-if="isShow" />
</template>

<script>
	import Demo05Vue from './components/Demo05.vue'
	import { ref } from 'vue'
	export default {
		name: 'App',
		components: { Demo05Vue },
		setup(props) {
			let isShow = ref(true)
			return { isShow }
		},
	}
</script>
```



![image-20220327221213469](https://s2.loli.net/2022/03/27/xBq5mgWVsufaZ4Y.png)

### Hook函数

当我们的项目中可能会产生某些可以复用的小功能，比如获取鼠标在屏幕上的位置并显示，这些功能和组件本身是没什么关系的，而且往往需要在多个组件内灵活使用，这时候我们就可以把他们封装成一个个Hook函数，Hook的本质就像是一个钩子，当我们需要的时候随时把他勾过来使用就行

一般来说，我们会在src目录下建立一个`hooks`目录，在其中以`usexxxx.js`定义钩子的名字，接着在里面写上全套的可以被`setup`使用的函数内容，接着提供一个返回值，保证`setup`函数每一次钩到这个钩子都能够获取到一个返回值

尤其是当这个功能内存在对生命周期钩子函数的使用，那么将其封装为一个钩子还可以减少在setup中引入的过量API

```js
import { reactive, onMounted, onBeforeUnmount } from "vue";
export default function() {
    let point = reactive({
        x: 0,
        y: 0
    })

    function savePoint(event) {
        point.x = event.pageX
        point.y = event.pageY
        console.log(event.pageX, event.pageY);
    }
    onMounted(() => {
        window.addEventListener('click', savePoint)
    })
    onBeforeUnmount(() => {
        window.removeEventListener('click', savePoint)
    })
    return point
}
```

同时由于传出来的天然是reactive对象，因此在组件内直接`let`接收即可

```vue
<template>
	<div>
		<h2>当前点击{{ p.x }},{{ p.y }}</h2>
	</div>
</template>

<script setup>
	import usePoint from '../hooks/usePoint.js'
	let p = usePoint()
</script>
```

### toRef

我们都知道我们推荐使用Vue3新增的reactive作为响应式数据，但是它也有缺点，就是我们把一般数据都包裹在一个对象中，在页面上引用的时候免不了要先引用`[对象名].[属性]`来引用数据，一旦数据比较多就需要写一大堆对象名，可不可以直接在返回时将对象内属性拆解，使得在页面中只使用属性名来显示属性内容呢

我们可以先思考一下用仅有的API可不可以做到

- 直接`return{a.b}`显然不行，因为a是Proxy对象而里面的属性b不是，因此返回的是一个干巴巴的数据，根本没有办法进行响应
- `return{ref(a.b)}`也是不行的，虽然好像在页面上进行了代理，但是实际上返回出去的根本就是一个新的数据，Vue将`a.b`这个reactive代理的数据重新包装成了ref数据，如果在setup中有修改a的方法一下子就会发现并不能做到响应式

这时候就需要请出我们的`toRef(s)`了，它可以在拆分reactive属性的基础上仅引用其中的属性内容，形成一个二次代理，从而使所有的数据修改都保持一致性

```vue
<script>
	import { reactive, toRefs } from 'vue'
	export default {
		setup() {
			const data = reactive({
				a: 1,
				b: {
					c: 2,
				},
			})
			return {
				// 等于toRef(data,'a')和toRef(data.b,'c')
				// 如果单用ref(data.a)会使页面上的响应式数据与setup中的reactive数据脱离关系，toRef是引用数据并不是无脑复制
				...toRefs(data),  // 返回的若干对象的对象集合，需要使用解构赋值
			}
		},
	}
</script>
```

但是toRef有一个局限，就是当其中被拆解的对象中又新添了一个新的属性时，我们并不能在页面上捕获到新增的属性信息，遇到这种情况就不得不直接传出整个data对象了

### 其他API

- Vue3还提供了能够让祖先给他的后代所有组件传数据的方式，只需要在父组件中添加`privide([变量共享名字],[变量名])`，接着在任意层级子组件中添加`inject([变量共享名字])`即可直接使用数据，但是注意这个数据和父组件里面共用的一个响应式，修改的时候应该注意对父组件的影响，同时这个API比较适用于祖孙之间传递数据，父子之间还是使用`props`比较好
- 当我们从别人手上拿到一个响应式数据（比如父组件），但是要提醒自己不要修改它时，我们可以使用`readonly([变量名])`，会让这个变量还是响应式数据，但是我们已经无法修改了，真的要修改就会控制台报错提醒我们

### 优势

通过对各种组合式API的学习，我们发现了我们所有的内容都写在setup方法里，写程序更加畅快了，这就是它的最大优势，原本我们在Vue2的时候，假设要增加一个响应式数据，我们得从`data`配置项开始改，一路改`computed`、`methods`、`watch`里面的配置项，一个数据的流程都被拆散了，当然拆散也有拆散的好处，在查找时可以方便的查到内容，但是如果我们需要跟踪一个数据就麻烦了，我们得每个配置项一个个找，才能理出一条数据的操作流程，而使用组合式API，所有数据的定义和操作流程是流畅的，我们可以方便的找到我们需要的内容，下面是几张动图

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/568b0ced69f241d282cf2c512e4e5f33~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

![See the source image](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d05799744a6341fd908ec03e5916d7b6~tplv-k3u1fbpfcp-watermark.image)

![img](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4146605abc9c4b638863e9a3f2f1b001~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp)

同时我们注意到第三张gif，当所有的数据内容高度集中化之后，我们就可以将每一个数据的操作流程进行一个打包，成为一个个Hook，既提高了复用效率，更加提高了代码的精简程度，方便维护者进行修改维护，这么一想也有点面向对象的意思了

## 特殊功能标签

讲完了setup里面的各种API，接下来我们就需要学习一些写在默认`<template>`里面的一些具有特殊功能的标签，他们都是Vue3不可缺少的组成成分

### Fragment

我们会发现在Vue3项目中，它不要求我们每一个组件内部最外层必须仅套一个标签了，我们可以在`<template>`标签下写任意个数的标签，其实是Vue3在渲染的时候默认会贴心的给我们所有标签加了一层`Fragment`标签，同时在显示在页面上的时候再将其去掉，我们可以从开发者工具中看到端倪

![image-20220328225644915](https://s2.loli.net/2022/03/28/LhoASFCZVpKMIR5.png)

### Teleport

我们可以在任意组件中用这个标签包裹其他标签，并在标签属性中指定需要将其中内容摆放的位置，这时候我们在观察程序结构的时候会惊讶的发现我们的组件已经不再遵循父子关系了

```html
<template>
	<h2>{{ a }}--{{ b.c }}</h2>
	<teleport to="body">
		<h2>你好</h2>
	</teleport>
</template>
```

![image-20220328225404935](https://s2.loli.net/2022/03/28/phkY52AvdGTFq4P.png)

当然我们也可以在`to`属性中写比如`#app`，实现组件内的部分结构到处乱飞的效果，还是十分有用的，尤其适合各种弹窗效果

