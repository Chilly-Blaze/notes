# Nvim

虽然我暂时还是觉得vscode比较香，但是这也不排除说不定配着配着nvim突然就爱上他了，但是不试试怎么知道呢，于是我走上了手撸nvim配置的道路

> 本来其实已经不想写配置过程了，但是事实是还是存在各种教程良莠不齐的情况，因此不得不自己手动进行整理一下

根据我一直以来的习惯，要用就用最新的内容，虽然Nvim+Lua的配置已经不算是新鲜内容了，但是我们还是以其作为配置基础

## 入口文件（`init.lua`）

既然是Lua作为配置的老大，那么理应在整个配置文件中不存在任何Vimsrcipt的内容，因此我宣布以往所有的`.vim`文件全部给他替换为`.lua`

首先我们需要建立一个空的配置文件用于覆盖和增强原有的配置，他被我们放在`.config/nvim/init.lua`这个地方，叫做入口文件，注意到默认装完nvim之后甚至我们找不到`.config/nvim`这个目录，所以没有不要怀疑，自己新建一个就完了

为了不让所有的配置一团乱七八糟的，我们学习分块管理的思想，在入口文件中仅引入其他各配置模块，至于Lua的语法，你就自己查去吧

最后我们的入口文件大概是长这样的

```lua
require('maps')
require('settings')
-- 还可以添加各种模块，这个名字要记住，下一步建立子配置文件时会用到
-- 同理，当我们重新拆分出去一个配置文件的时候，一定要保证在入口文件中进行导入
...
```

## 快捷键（`maps.lua`）

使用nvim当然免不了修改原有快捷键的步骤，毕竟某些操作确实有一点点的反人类，为了操作的流畅性，也为了接下来的配置方便，修改快捷键的操作刻不容缓

首先还是需要配置一下全局的Leader键，就用空格好了，在Lua中，我们可以通过`vim.g.xxx`来设置全局级别的xxx变量，而mapleader正是官方指定的全局Leader键映射变量，因此我们只需要加上`vim.g.mapleader = ' '`一行代码

而不像Vimscript中的使用什么`map/nmap`什么的设置不同级别的快捷键操作，在Lua中，提供了一个`vim.api.nvim_set_keymap`这么一个接口，而这个接口接收四个参数，分别是映射作用域、快捷键组合、映射指令和映射配置项（可以通过`:h :map-arguments`查看所有配置项），但是每次都调用这么长一个api显然不太方便，因此最好是自己设置一个简单的变量用于接收这个函数，我们直接上最终个人的设置参考

```lua
-- 全局Leader
vim.g.mapleader = ' '
-- 映射接口
local m = vim.api.nvim_set_keymap
local o = { noremap = true, silent = true }  -- 分别是开启非递归映射和静默指令执行

-- Insert
m('i','jk','<Esc>',o)
-- 撤销
m('i','<C-z>','<Esc>ua',o)
-- 保存
m('i','<C-s>','<Esc>:w<CR>a',o)

-- Normal
-- 跳转
m('n', '<C-j>', '9j', o)
m('n', '<C-k>', '9k', o)
m('n', '<C-h>', '20h', o)
m('n', '<C-l>', '20l', o)
-- 分屏
m('n','sv',':vsp<CR>',o)
m('n','sh',':sp<CR>',o)
m('n','sc','<C-w>c',o)
m('n','so','<C-w>o',o)
-- 切屏
m('n','<A-h>','<C-w>h',o)
m('n','<A-j>','<C-w>j',o)
m('n','<A-k>','<C-w>k',o)
m('n','<A-l>','<C-w>l',o)
-- 保存
m('n','<C-s>',':w<CR>',o)

-- Visual
-- 复制到系统
m('v','<C-c>','"+y',o)

-- Global
-- 全选
m('','<C-a>','<Esc>ggVG',o)
-- 保存退出
m('','<C-Q>','<Esc>:wq<CR>',o)
m('','<C-A-Q>','<Esc>:q!<CR>',o)
-- 替换
m('','<C-f>','<Esc>:%s/',o)
```

### vim.keymap.set

在我们掌握了上面提及的`vim.api.nvim_set_keymap`接口之后，事实上，在通过Lua配置时，nvim并不推荐我们使用一切带有`api`包下的接口，因为意味着存在更优化的映射接口供我们使用，他就是`vim.keymap.set`，他强就强在可以接收Lua函数作为参数进行真正可编程化的快捷键映射，同时接收Table类型作为多个指定映射场景控制，同时各个默认配置项及新增配置项也更加人性化，让人欲罢不能

经过修改之后的映射项是长这样的

```lua
-- 映射接口
local function m(mode, l, r, opts)
    if opts == nil then opts = {} end
    opts.silent = true
    vim.keymap.set(mode, l, r, opts)
end

-- Insert
m('i', 'jk', '<Esc>')
-- 撤销
m('i', '<C-z>', '<Esc>ui')
-- 保存
m('i', '<C-s>', '<Esc>:w<CR>a')

-- Normal
-- 分屏
m('n', 'sv', '<Cmd>vsp<CR>')
m('n', 'sh', '<Cmd>sp<CR>')
m('n', 'sc', '<C-w>c')
m('n', 'so', '<C-w>o')
-- 比例控制
m('n', '<C-Left>', '<Cmd>vertical resize +2<CR>')
m('n', '<C-Right>', '<Cmd>vertical resize -2<CR>')
m('n', '<C-Up>', '<Cmd>resize +2<CR>')
m('n', '<C-Down>', '<Cmd>resize -2<CR>')
-- 切屏
m('n', '<A-h>', '<C-w>h')
m('n', '<A-j>', '<C-w>j')
m('n', '<A-k>', '<C-w>k')
m('n', '<A-l>', '<C-w>l')
-- 保存
m('n', '<C-s>', '<Cmd>w<CR>')
-- 一键保存退出 or buffer退出
m('n', 'q', function()
    local n = #vim.fn.getbufinfo { buflisted = 1 }
    if n == 0 or n == 1 then return '<Cmd>q<CR>'
    else return '<Cmd>BufferClose<CR>'
    end
end, { expr = true })

-- Visual
-- 复制到系统
m('v', '<C-c>', '"+y')

-- Terminal
m('t', '<Leader>jk', '<C-\\><C-n>')

-- Global
-- 全选
m({ 'n', 'i' }, '<C-a>', '<Esc>ggVG')
-- 强制退出
m({ 'n', 'i' }, '<C-Q>', '<Cmd>q!<CR>')
-- 替换
m({ 'n', 'i' }, '<C-f>', '<Esc>:%s/')
-- 光标快速移动
m({ 'n', 'v' }, '<C-j>', '9j')
m({ 'n', 'v' }, '<C-k>', '9k')
```

可以发现有了Lua这种正规语言的支持，一下子整个配置文件的编写都变得更加优雅和灵活了，比如我们就单聚焦于`q`这个快捷键，首先我们先通过提供的`getbufinfo`这个函数接口去获得当前所有的buffer信息，然后借助Lua语言的`#`符号获取返回数组的长度，之后去掉1号初始buffer则剩下的就是我们所有打开的buffer个数，根据当前buffer个数的不同来决定是清除buffer还是关闭nvim，最后我们为其添加`expr`配置项，来保证传入函数的返回值作为映射的命令内容，行云流水，畅快不已

> 每一个buffer就对应着我们在nvim中打开的每一个页面，在nvim中每一个页面的打开会像压栈一样将旧的buffer压在底下，常用的buffer管理工具比如之后会提及的`bufferline`插件用于在顶部显示当前所有的buffer项，相对应的，我们平常的`:q`会直接关闭整个nvim，想在存在多个buffer时单独关闭当前显示的buffer，显然不能简单的映射`:q`
>
> 不过其中涉及的`BufferClose`指令其实是之后会提到的`barabar`插件中提供的，如果想要原生的关闭buffer，可以使用`:bdelete`

## 基础配置（`settings.lua`）

这一个配置文件主要用来调整nvim默认的一些不是特别合理的配置，在此之前我们需要先稍微学习一下如何在Lua文件中嵌入原本Vimscript的各种配置项

我们都知道，在原有的Vim中，我们如果想要设置一个配置，我们会使用`set`命令，比如显示行号，就需要`set number/se nu`，但是Lua显然不能支持这个神秘的set关键字，因此nvim发明出了通过`vim.[a].[b]`的方式进行配置的设置，比如还是设置行号开启，此时我们就可以在Lua文件中写上这么一段`vim.wo.number = true`，不仅符合我们常规编程的语法习惯，更增强了可读性

当然你可能会问，这个配置项中的`vim`和`number`我都知道，但是中间的这个`wo`是什么意思？

事实上，vim所有的配置项被分做了三个作用域，分别是`global options`，`window-local options`和`buffer-local options`，其分别对应着`o`，`wo`，`bo`三个标识，然后你可能会问，为什么要搞这神秘的域乱七八糟的，直接`vim.number`不香吗，道理确实是这么一回事，在Vimscript中确实也不怎么分作用域，直接set就完事了，但是进行拆分之后，从可读性来说可以说是大大提升了，以至于在配置比较复杂的场景中，我们可以通过不同的作用域来区别不同的配置内容，归类和拆分不同的配置文件

你可能还会问，这么一说好像确实有道理，但是我怎么知道这个配置项究竟是哪个作用域的呢？

此时我们就需要借助配置项的帮助文档了，不妨输入`:h nu`看一看number这个配置项的一些信息

![image-20220710200031227](https://s2.loli.net/2022/07/10/ElZM4XatzRJ1L97.png)

然后我们发现好像这个配置帮助并没有什么卵用，我们无法从其中获得任何有关其作用域的信息，但是我们注意到其中有一行`See also hl-LineNr and 'numberwidth'`这么一个东东，那么我们不妨看看这两个配置项的帮助文档

其中`hl-LineNr`里面并没有什么东东，但是在`numberwidth`的文档中，我们看到了我们需要的东西

![image-20220710200352788](https://s2.loli.net/2022/07/10/PHtIBohYpcD8gyA.png)

正是这一行，标识了我们需要的作用域，因此我们知道了，number配置项属于`window-local options`，这样以来，在一开始我提出的`vim.wo.number = true`便变得有法可依了，同时我们如果输错了作用域，在再次启动nvim的时候就会对我们进行报错提醒，也保证了输入的正确性

![image-20220710202325863](https://s2.loli.net/2022/07/10/X6pBeCAkG7TztV9.png)但是我们在上面也遇到了一些问题，比如说万一某一个配置项，我们就是找半天都找不到他的作用域怎么办？这时候Nvim还为我们提供了一种备选方案，我们可以直接通过`vim.o.xxx`来不管配置项的作用域（即o代表全局作用域，会去另外两个作用域中分别寻找xxx配置项)，但是由于真的有一些配置项是属于global作用域的（比如`shiftround`等等)，~~因此一般来说为了配置美观优雅，我们还是推荐使用明确的作用域指示~~

> 注意以上说法是错误的，最好将所有的设置都设为o即global作用域，因为某些局部作用域会因为一些很奇怪的原因无法作用于之后我们在nvim内使用的buffer窗口的情况，因此为了省时省力，最好全部设为o（见下）

以下是经过整理过的全部配置内容，之后如果还有比较好的配置项也会不断更新，主要我也不想看将近一万行的英文帮助文档，于是就直接抄别人的作业然后自己修改修改了

```lua
-- window作用域
-- jk移动时光标下上方保留8行
-- 此处当然可以vim.wo.scrolloff = 8，以下雷同，但是为了避免错误，尽量使用全局作用域o
vim.o.scrolloff = 8
-- 使用相对行号
vim.o.number = true
vim.o.relativenumber = true
-- 高亮所在行
vim.o.cursorline = true
-- 显示左侧图标指示列
vim.o.signcolumn = "yes"

-- buffer作用域
-- utf8
vim.o.fileencoding = 'utf-8'
-- 一个Tab=4个空格
vim.o.tabstop = 4
vim.o.softtabstop = 4
vim.o.shiftwidth = 4
-- 新行对齐当前行，空格替代tab
vim.o.expandtab = true
vim.o.autoindent = true
vim.o.smartindent = true
-- 当文件被外部程序修改时，自动加载
vim.o.autoread = true
-- 不生成交换文件
vim.o.swapfile = false

-- global作用域
-- 搜索大小写不敏感，除非包含大写
vim.o.ignorecase = true
vim.o.smartcase = true
-- 允许隐藏被修改过的buffer
vim.o.hidden = true
-- 鼠标支持
vim.o.mouse = "a"
-- 禁止创建备份文件
vim.o.backup = false
vim.o.writebackup = false
-- split window 从下边和右边出现
vim.o.splitbelow = true
vim.o.splitright = true
-- 自动补全不自动选中
vim.o.completeopt = "menu,menuone,noselect,noinsert"
-- 样式
vim.o.background = "light"
vim.o.termguicolors = true
-- 不可见字符的显示，这里只把空格显示为一个点
vim.o.list = true
vim.o.listchars = "space:·"
-- 补全增强
vim.o.wildmenu = true
-- 一些显示缩写
vim.o.shortmess = "a"
-- 最上面的tab栏，永久显示
vim.o.showtabline = 2
```

重启nvim，会发现界面已经变好看了不少，各种操作的反馈也比较人性化了～

## 插件配置

### packer

所有的插件都要经过插件管理器进行管理，既然使用Lua，那么首选的当然是原生Lua的Packer进行管理，安装十分简单，一行代码克隆一下仓库即可

```shell
git clone --depth 1 https://github.com/wbthomason/packer.nvim ~/.local/share/nvim/site/pack/packer/start/packer.nvim
```

之后创建并打开`plugins.lua`，添加如下代码导入包管理依赖

```lua
return require('packer').startup(function()
    use 'wbthomason/packer.nvim'
end)
```

其中，由于nvim默认情况下会自动去搜索packpath（`~/.local/share/nvim/site`）路径下的所有包，之后找到了`~/.local/share/nvim/site/pack/packer/start/packer.nvim/lua/packer.lua`这个文件，于是调用其startup函数，这个startup函数就厉害了，每当我们执行`:PackerSync`这个指令时，他都会将传给startup函数内的每一个use函数通过网络进行导入和更新，也就是说，在使用了packer之后，之后，我们每看到了一个中意的插件，只需要在`plugins.lua`内声明式的`use`一个插件路径，接着`:PackerSync`一下，和docker一样，packer会自动帮你把插件下载好放到packpath中并应用，一步到位，妈妈再也不用担心我不会装插件了

同时这个use函数不仅支持字符串传参，在一些插件需要配置的场合，还支持对象形式的传参，进一步增加了导入的灵活性

### 主题

现在你学会了packer的基本操作，不妨让我们导入一个nvim的主题玩玩先

作为忠实的light主题单推人，我选择onedarkpro这个主题，有了packer的辅助，我们的主题安装显得异常简单

只需要在`plugins.lua`内的startup函数内添加如下代码

```lua
    use({
        "olimorris/onedarkpro.nvim",
        config = function()
            require("onedarkpro").setup()
        end
    })
```

>  注意到此时传给use函数的是一个对象，除了给定了插件的包路径之外，还额外添加了一个config参数key，用于初始化主题的设置，当然，你可能会发现就算是没有加第二个参数，程序依旧照常运行，甚至如果你将require这一行加到`init.lua`中，并且设置一些插件的设置（往setup函数中传入指定对象，[详见](https://github.com/olimorris/onedarkpro.nvim#default-configuration)），同样会发现依旧生效，此处埋下一个伏笔，下一节将会详细说明

之后我们为了让主题正确配置，我们还需要跑到`init.lua`中，指定主题的名称`vim.cmd("colorscheme onedarkpro")`，同时请保证在`settings.lua`中指定了`vim.o.background = "light"`（当然如果你想要dark主题那默认就是，可以不用配置），使得在每次启动nvim之前，都保证先加载主题，接着执行`:PackerSync`，重启即可应用，效果如下

![image-20220711211729156](https://s2.loli.net/2022/07/11/PG1ub2QNaHBsiMy.png)

当然这个效果你可能觉得还是一般般，但这其实只是插件部分的初体验，当我们真正掌握了Nvim插件的使用，相信美化界面对于你来说将不再困难

### setup

在安装主题的过程中，我们体会到了在packer的帮助下，插件下载和更新，导入的方便性，同时我们也留下了一个疑问，在进行主题配置的过程中，往use函数中传入对象中的`config`参数究竟是什么，他在插件中扮演了怎样的角色

这时候，就需要引入插件的启动函数的概念了

对于一般的插件来说，都会暴露大量的配置接口，同时，单纯的下载插件到packpath并不能保证插件在nvim启动时跟随启动（当然这个主题配置是例外的，因为他直接由入口文件调用命令行colorscheme指令引用，因此就算不配config主题仍旧能正常运行），为了保证插件在nvim启动时预先启动，我们必须在入口文件或者利用config参数先一步调用插件的启动，而一般来说，插件的启动工作，往往都交给所谓的setup函数执行

至此，我们完整的了解了引入一个插件时的基本步骤

1. 对于一般插件，首先，我们需要找到这个插件的包名和相关安装文档，照着文档说明，在`plugins.lua`中通过`use`函数引入插件
2. 通过`:PackerSync`指令拉去新添加的插件内容
3. 在入口文件或者use函数内的config配置项中调用setup函数
4. 配置相关快捷键和检查适配性

你可能注意到，前文提到一般的插件会暴露大量的配置接口，可供用户自定义配置，因此setup作为插件的启动函数，也不仅仅可以通过无参调用来进行插件的初始化，在任何插件的帮助文档中，你或许都能找到有关`setup`函数的介绍，他告诉你调用setup无参时的默认参数，和所有的个性化参数的使用和可配置内容，比如说著名的`nvim-tree`插件

![image-20220712132310446](https://s2.loli.net/2022/07/12/ohEXKZCMIjvzkUR.png)

可以发现，通过往setup函数中传入对象参数，对插件的各种属性进行更加精细化的配置，使得在插件启动时呈现不同的功能

### nvim-treesitter

了解了插件的配置和启动函数，同样的，我们不妨立刻动手配置一个插件试试，nvim-treesitter就是一个很好的选择，因为它默认状态下不打开任何功能项，必须由用户开启之后才能够使用其功能

这个插件有四大功能，他们是

- 代码高亮模块
- 增量选择模块
- `=` 代码格式化模块
- Folding 模块

默认都是关闭的，因此我们需要在配置文件中设置 `enable = true` 手动开启，让我们开始

1. `plugins.lua`中use函数引入插件名`    use { 'nvim-treesitter/nvim-treesitter', run = ':TSUpdate' }`，并Sync下载包

2. 由于接下里还需要装很多插件，因此我专门设置了一个config文件夹用于存放各种插件的配置项，之后由`config/init.lua`统一引入所有配置文件，再在入口文件处直接`require'config'`即可，设置完成后的目录结构如下

   ![image-20220712133916392](https://s2.loli.net/2022/07/12/b6JdivOGroejD4q.png)

   > 注意到插件的引入（`plugins.lua`）和插件的配置（`config/xxx.lua`）是推荐分离的，更加体现功能的模块化

3. 因此，下一步是创建`treesitter.lua`，并在其中调用setup函数，同时为了开启所有功能，我们需要同时为setup函数传参

   ```lua
   require'nvim-treesitter.configs'.setup {
       -- 安装 language parser
       -- :TSInstallInfo 命令查看支持的语言
       ensure_installed = {
           'lua', 'json','html','css','javascript','bash','markdown','typescript','vue','scss'
       },
       
       -- 代码高亮
       highlight = {
           enable = true,
           additional_vim_regex_highlighting = false
       },
   
       -- 增量选择
       incremental_selection = {
           enable = true,
           keymaps = {
               init_selection = '<CR>',
               node_incremental = '<CR>',
               node_decremental = '<BS>',
               scope_incremental = '<TAB>',
           }
       },
   
       -- 代码格式化
       indent = {
           enable = true
       }
   }
   -- 折叠
   vim.wo.foldmethod = 'expr'
   vim.wo.foldexpr = 'nvim_treesitter#foldexpr()'
   -- 默认不要折叠
   vim.wo.foldlevel = 99
   ```

4. 在`config/init.lua`中引入`require'treesitter'`，重启nvim查看效果

5. 之后可以为格式化操作设置一下快捷键` m('n', '=', 'm1gg=G1', o)`（第二个1前面有个反引号，md无法打入，为的是格式化之后重新定位到当前位置），其中`gg=G`就是全屏选中并格式化，当然也可以`ggVG=`

配置完成之后，我稍微说一说这四个功能的使用，首先因为他们都是对于每个语言定制化的（比如cpp高亮和格式化的规则肯定和java不一样），因此他们都必须依赖着language parser，我们得根据我们的需要在配置项中的`ensure_installed`中添加我们需要的语言（如果不知道有哪些语言支持可以`:TSInstallInfo`），之后重新打开文件测试各种功能

- 对于语法高亮，我们可以通过`TSBufToggle highlight`来启用和禁用切换查看效果
- 对于增量选择，我们可以通过连续敲Enter/Backspace键体验逐渐扩大/缩小的括号间选区
- 对于代码格式化，配置了快捷键之后，我们只需要按下`=`键即可查看格式化效果
- 而对于折叠，我们可以将光标置于括号内，通过zc折叠代码快，通过zo展开代码块

至此，对于插件配置的所有内容都已经讲解完成了，对于各种插件，只需要依葫芦画瓢都可以完成基本的引入和配置

## LSP

在了解了一般插件的安装和使用之后，我们接下来要提到的可以算是一个重量级的功能插件——LSP，正是由于内置了他，我们的nvim才能在一定程度上和一般IDE媲美

![img](https://pic4.zhimg.com/80/v2-6f5043da2daa94e8e8d93ffbff765ddf_1440w.jpg)

看着这张图，代码补全的原理，就可以理解为就是我们在nvim中开启了一个叫做LSP的线程，他帮忙我们监控我们编写的所有内容，并将其传送给与代码文件一起启动的专门服务于该种语言的language servers（最右一部分），然后传输回language servers 返回的数据，从而实现对我们打了一半的代码提出一些建议（包括补全和纠错等）

需要注意的是，其中LSP部分是内置在Nvim当中的，这也是我们可以与language servers通信的根本依据，而language servers则是脱离Nvim独立运行的，甚至由于language servers这个概念就是vscode提出的，因此我们实际上开启一个文件之后伴生运行的language servers正是vscode中的language servers，理解了这个，我们也能够理解为什么说LSP可以解除编辑器和代码提示的耦合性了

### language servers

根据这个原理，想要使用LSP，首先需要的就是每一种语言的language servers的安装，从之前我们知道，language servers独立于Nvim运行，因此从使用角度来说，我们完全可以不通过Nvim自己跑到微软的vscode仓库中下载我们需要的language servers，但是这样显然是不方便的，为了便于各种language servers的安装，我们可以安装一个[nvim-lsp-installer](https://link.zhihu.com/?target=https%3A//github.com/williamboman/nvim-lsp-installer%23available-lsps)插件，他是一个language servers的包管理器，通过他我们可以非常方便的下载language servers并进行相关的配置

根据之前装插件的经验，我们首先得先use一下需要安装的内容，于是在`plugins.lua`文件中添加`use {'neovim/nvim-lspconfig', 'williamboman/nvim-lsp-installer'}`，其中的`nvim-lspconfig`这个官方插件我们下一节配置LSP时再说，当前我们不妨先着眼于language servers的安装部分

安装了`nvim-lsp-installer`，下一步就是通过这个插件安装特定语言的language servers，由于我们配置就是Lua语言，为了演示方便，就先拿Lua语言的language servers安装进行演示

首先，我们新建`lua/lsp`目录，并在其目录下创建`installer.lua`文件作为language servers安装总入口，在其中保存以下内容

```lua
-- the servers that should be automatically installed
local lsp_servers = {
    "sumneko_lua",
}
-- using plug "nvim-lsp-installer" to ensure the installation
-- should before the lsp config
require "nvim-lsp-installer".setup {
    ensure_installed = lsp_servers,
    automatic_installation = true,
    ui = {
        icons = {
            server_installed = "✓",
            server_pending = "➜",
            server_uninstalled = "✗",
        },
    },
}
```

可以看出作为一个安装器来说配置的内容还是比较方便的，其中我们将所有的language servers名称都存在`lsp_servers`这个数组中，同时学着treesitter的样子，通过往setup初始化函数中传入`ensure_installed`配置项来保证需要的language servers被正确下载（当然其实不加`ensure_installed`对使用来说也没有什么问题，因为只需要下面`automatic_installation`一个配置项，之后在lsp配置正确的情况下就可以自动下载了），而`sumneko_lua`就是Lua语言language servers，各种语言的Server都可以从[installer的仓库文档中](https://github.com/williamboman/nvim-lsp-installer#available-lsps)中查到，之后我们在入口文件中引入lsp目录，重启nvim

之后可以通过`:LspInstallInfo`查看指定语言的Server下载情况，同时为了进一步解耦，我在当前目录下又创建了一个`servers.lua`用以专门保存所有的language servers

```lua
return {
    "sumneko_lua",
}
```

之后一旦我们需要添加新的language servers支持，只需要在此处添加language servers名即可，记得修改`installer.lua`内的变量

### lspconfig

安装好了language servers之后，显然我们需要启用他，稍加分析我们就会发现，对于大多数编程语言来说，所需要的提示内容大多都是相同的（比如大多数语言都需要支持函数跳转和智能补全），这也是为什么在上面那张图中LSP只有一个，同样的，在Nvim中我们需要配置的LSP同样也只有一个，但是我们可以针对不同的language servers进行不同的配置

在`lua/lsp`目录下，我们专门创建一个`s_config`目录专门存放language servers的配置部分，由于我们之前已经安装过了`lspconfig`，因此此处不重复安装，他是目前为止我们使用的唯一一个官方推出的插件，只要启动它时传入指定的配置我们就可以便捷的使用Nvim内置的LSP功能，在`s_config`目录下新建`init.lua`，编写如下内容

```lua
local servers = require 'lsp.servers'
local lspconfig = require "lspconfig"

for _, server in pairs(servers) do
    local config = 'lsp.s_config.' .. server
    xpcall(function() require(config) end, function() config = 'lsp.s_config.default' end)  -- 是否能获取包，获取不到则会报错被xpcall捕获并执行传入的第二个函数
    lspconfig[server].setup(require(config))
end
```

其中，`servers`模块就是先前创建的专门返回language servers的文件，引入`lspconfig`之后，循环遍历所有language servers项，之后对每一个server，有自定义配置则载入自定义配置，无自定义配置则用默认配置文件，但针对每一项server，都调用`lspconfig`这个插件的setup函数进行带参的预加载，相信在了解了插件的使用和LSP的工作原理之后，这一段代码理解起来也并不困难，至于`lspconfig`是怎么仅通过名字找到对应language servers，或者像这样一下子看上去直接加载了所有的Server到底好不好这些细节性问题目前暂时先放在一边，从代码逻辑上来说，这一段和我们以往配置的任何一个插件都没有什么区别

理解了这段代码之后，我们就只剩下最后一个问题需要解决，即如何配置个性化language servers内容和默认配置内容

### 个性化配置

和一般插件一样，每一个language servers也可以进行个性化的配置，比如`sumneko_lua`的配置内容同样可以从[文档](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md#sumneko_lua)中看到，我们不妨直接照着文档的推荐配置来，将其粘贴到新建出来的`sumneko_lua.lua`文件中

```lua
local runtime_path = vim.split(package.path, ";")
table.insert(runtime_path, "lua/?.lua")
table.insert(runtime_path, "lua/?/init.lua")

function insert(o, t)
    for k, v in pairs(t) do
        o[k]=v
    end
    return o
end

return insert({
    settings = {
        Lua = {
            runtime = {
                -- Tell the language server which version of Lua you're using (most likely LuaJIT in the case of Neovim)
                version = "LuaJIT",
                -- Setup your lua path
                path = runtime_path,
            },
            diagnostics = {
                -- Get the language server to recognize the `vim` global
                globals = { "vim", "use", "hs" },
                disable = { "lowercase-global", "trailing-space" }
            },
            workspace = {
                -- Make the server aware of Neovim runtime files
                library = vim.api.nvim_get_runtime_file("", true),
                checkThirdParty = false,
            },
            -- Do not send telemetry data containing a randomized but unique identifier
            telemetry = {
                enable = false,
            },
        },
    },
}, require 'lsp.s_config.default')
```

可以发现，如果只看insert函数的前半部分，其中的内容都和官方上的内容大差不差，而其中这些看上去比较奇怪的配置，实际上就是我们在vscode中，下完一个语法插件之后在设置里面摆弄的那些设置，只不过在vscode里面使用json配置，而这里用Lua的表结构进行设置而已，原理上都是一样的，对于更加细致的设置项，完全可以去翻Servers的原生文档和vscode的设置内容

稍微讲解一下，这其中的runtime指的就是Lua找包的路径，而diagnostics里面的globals其实就是不检查那些单词的语法，比如说这里加了`vim`和`use`，则我们打出vim单词的过程中就不会有错误提示，可以算是一个强迫症福音了

于是我们理解了官方给我们的这些配置项的含义，但是终究我们还是有一部分内容，即后半部分附加上的的`default`模块里面到底包含了什么东西，这就牵扯到LSP在实际应用中最重要的东西——快捷键绑定了

### 快捷键绑定

为什么说这一部分相当重要，因为LSP从根本上来讲就是一大堆规范化的接口，而这些接口将交由Language Servers实现，而我们只需要去调用这些接口即可实现所谓的功能，但是坏就坏在这些接口的调用接口方法名往往比较神秘，比如跳转到定义的命令是这样的`lua vim.lsp.buf.definition()`，如果没有快捷键的帮助，显然是极没有效率的

直接在`maps.lua`中添加如下代码即可

```lua
-- LSP
-- rename
m("n", "<leader>re", "<cmd>lua vim.lsp.buf.rename()<CR>", o)
-- code action
m("n", "<leader>ca", "<cmd>lua vim.lsp.buf.code_action()<CR>", o)
-- go xx
m("n", "gd", "<cmd>lua vim.lsp.buf.definition()<CR>", o)
m("n", "gh", "<cmd>lua vim.lsp.buf.hover()<CR>", o)
m("n", "gD", "<cmd>lua vim.lsp.buf.declaration()<CR>", o)
m("n", "gi", "<cmd>lua vim.lsp.buf.implementation()<CR>", o)
m("n", "gr", "<cmd>lua vim.lsp.buf.references()<CR>", o)
-- diagnostic
m("n", "go", "<cmd>lua vim.diagnostic.open_float()<CR>", o)
m("n", "gk", "<cmd>lua vim.diagnostic.goto_prev()<CR>", o)
m("n", "gj", "<cmd>lua vim.diagnostic.goto_next()<CR>", o)
-- format
m("n", "<leader>f", "<cmd>lua vim.lsp.buf.formatting()<CR>", o)
```

当然其实真实情况中常用的内容也并没有这么多内容，而且其实也并不是每一个Language Servers都实现了这些接口的内容，比如sumneko_lua好像就不支持rename操作，同时别的接口内容的具体规则可以查看[lspconfig的文档](https://github.com/neovim/nvim-lspconfig/#suggested-configuration)

之后就可以测试使用效果了，比如故意输错一些内容看看会不会提醒错误，或者测试一下快捷键是否能够使用

### 代码补全

在了解了LSP其中一个重要的功能代码检查之后，下一个尤其重要的功能就是代码补全功能，这同样也是尤其重要的功能，但是相较于代码的自动提示和跳转等操作，代码的补全功能显得更加繁杂和不便于处理，于是乎我们还需要在LSP和Language Servers中间再加一层插件，由他帮助我们集成各种补全规则，我们只需要给他配置时传入我们喜欢的补全来源和片段规则，他就能根据我们配置的不同场景提供给我们不同的补全参考

这个插件本体就是`nvim-cmp`，但是为了能够完成补全的全部功能，我们的`plugins.lua`需要添加如下这么多行

```lua
-- 代码补全
use 'hrsh7th/nvim-cmp'
use 'hrsh7th/cmp-nvim-lsp' -- { name = nvim_lsp }
use 'hrsh7th/cmp-buffer' -- { name = 'buffer' },
use 'hrsh7th/cmp-path' -- { name = 'path' }
use 'hrsh7th/cmp-cmdline' -- { name = 'cmdline' }
use 'hrsh7th/cmp-vsnip' -- { name = 'vsnip' }
use 'hrsh7th/vim-vsnip'
use 'onsails/lspkind-nvim'
use 'rafamadriz/friendly-snippets'
```

看上去好像很恐怖，但是实际上大多都是默认的配置文件，之后我们在补全配置中就会看到他们的身影

接下来记得`:PackerSync`，之后在lsp目录下新建`cmp.lua`配置文件，添加如下代码

```lua
local lspkind = require 'lspkind'
local cmp = require 'cmp'
if cmp ~= nil then
    cmp.setup {
        -- 指定 snippet 引擎
        snippet = {
            expand = function(args)
                vim.fn["vsnip#anonymous"](args.body)
            end,
        },
        -- 补全来源，来自于我们导的四个包
        sources = cmp.config.sources({
            { name = 'nvim_lsp' },
            { name = 'vsnip' },
        }, {
            { name = 'buffer' },
            { name = 'path' }
        }),
        -- 快捷键，针对出现提示框后Tab选择下一个，Shift+Tab选择上一个，回车确认选择
        mapping = cmp.mapping.preset.insert {
            ["<CR>"] = cmp.mapping.confirm({ select = true }),
            ["<Tab>"] = cmp.mapping.select_next_item(),
            ["<S-Tab>"] = cmp.mapping.select_prev_item(),
        },
        -- 使用lspkind-nvim显示类型图标
        formatting = {
            format = lspkind.cmp_format {
                with_text = true,
                maxwidth = 50,
                before = function(entry, vim_item)
                    vim_item.menu = "[" .. string.upper(entry.source.name) .. "]"
                    return vim_item
                end
            }
        },
    }

    -- 命令行输入/时仅提供buffer补全选项，对应之前导入的cmp-buffer
    cmp.setup.cmdline('/', {
        sources = {
            { name = 'buffer' }
        }
    })

    -- 命令行输入:时仅提供path补全选项，对应之前导入的cmp-path
    cmp.setup.cmdline(':', {
        sources = cmp.config.sources({
            { name = 'path' }
        }, {
            { name = 'cmdline' }
        })
    })
end
```

之后就可以进行测试使用了

> 如果出现`No "python3" provider found. Run ":checkhealth provider"`报错
>
> 解决方案：`python3 -m pip install --user --upgrade pynvim`，没有pip的就下一个`yay -S python-pip`

同时注意其中`vsnip`叫做代码片段，他往往不会根据代码文件的实际情况进行推荐提醒，而更像是一种片段规则，比如输入`l`就会提示`l~`，当你确认选择之后会自动填充为local，或者仅需要输入`if`，就可以做到直接生成完成的if代码段而不是仅填充if两个字母

与此类似的代码片段插件还有比如`luasnip`、`ultisnips`、`snippy`等等，需要注意的是他们必须内置在cmp这个插件中使用

这样一来，整个Nvim的配置需要学习部分也就到此结束了，之后只需要多多去寻找插件，勇于测试即可不断的将普通的文本编辑器发展为功能齐全的IDE

## 进阶

如果你在上面的基础上感觉好像也就那么回事，那么相信接下来的内容一定也不会特别困难，一路上看下来，可以发现几乎所有的难点都是发生在插件的安装和配置过程中，有时候一个插件可能会需要你琢磨上一天的时间，各种各样的错误接连不断，最气人的是往往这种情况下你还无法在网络中找到任何有关的解决方案，毕竟目前来说能找到的国内Lua配置教程都寥寥无几，更不要说一个特定插件的bug问题了，而相较于在对应插件的仓库中翻半天issue，如果这个笔记当中记录了解决方案那自然是再好不过

因此虽说是进阶，实际上就是介绍一些插件的使用姿势，同时可能会发现，虽然上面曾经介绍过部分插件的安装和配置，但是在本节中可能完全用不到之前拿来举例的插件和配置，毕竟从我个人的体验角度来说，某些似乎广受好评的插件在我用起来其实并不是那么顺手

为了避免越讲越乱，现在直接将插件列表和最终的目录内容给出，直接照着上面的顺序进行讲解，同时除了特殊情况，一律省略插件配置部分在`init.lua`内的引用操作

```lua
return require('packer').startup(function()
    -- Packer
    use 'wbthomason/packer.nvim'
    -- 主题
    use "olimorris/onedarkpro.nvim"
    -- 语法高亮，折叠
    use { 'nvim-treesitter/nvim-treesitter', run = ':TSUpdate' }
    -- LSP
    use { 'neovim/nvim-lspconfig', 'williamboman/nvim-lsp-installer' }
    -- 悬浮定义
    use 'tami5/lspsaga.nvim'
    -- 代码补全
    use 'hrsh7th/nvim-cmp'
    use 'hrsh7th/cmp-nvim-lsp' -- { name = nvim_lsp }
    -- 补全源
    use 'hrsh7th/cmp-buffer' -- { name = 'buffer' },
    use 'hrsh7th/cmp-path' -- { name = 'path' }
    use 'hrsh7th/cmp-cmdline' -- { name = 'cmdline' }
    use 'hrsh7th/cmp-vsnip' -- { name = 'vsnip' }
    use 'hrsh7th/vim-vsnip'
    use 'hrsh7th/cmp-nvim-lsp-signature-help' -- { name = 'nvim_lsp_signature_help' }
    -- 使代码片段源可用
    use 'rafamadriz/friendly-snippets'
    -- 补全UI
    use 'onsails/lspkind-nvim'
    -- Ranger
    use 'kevinhwang91/rnvimr'
    -- 顶部panel
    use { 'romgrk/barbar.nvim', requires = { 'kyazdani42/nvim-web-devicons' } }
    -- 起始页
    use { 'glepnir/dashboard-nvim' }
    -- 文件查找，项目打开
    use { 'nvim-telescope/telescope.nvim', tag = '0.1.0', requires = { { 'nvim-lua/plenary.nvim' } } }
    use 'ahmedkhalf/project.nvim'
    -- 括号匹配
    use { "windwp/nvim-autopairs", config = function() require("nvim-autopairs").setup {} end }
    -- surround
    use 'ur4ltz/surround.nvim'
    -- 自动注释
    use 'numToStr/Comment.nvim'
    -- 终端
    use { "akinsho/toggleterm.nvim", tag = 'v2.*' }
    -- 底部状态栏
    use({ 'nvim-lualine/lualine.nvim', requires = { 'kyazdani42/nvim-web-devicons' }, })
    use 'arkav/lualine-lsp-progress'
    -- 彩虹括号
    use 'p00f/nvim-ts-rainbow'
    -- 代码执行
    use { 'CRAG666/code_runner.nvim', requires = 'nvim-lua/plenary.nvim' }
    -- 前置缩进增强
    use "lukas-reineke/indent-blankline.nvim"
    -- 代码格式化
    use({ "jose-elias-alvarez/null-ls.nvim", requires = "nvim-lua/plenary.nvim" })
    -- Git信息显示
    -- use 'lewis6991/gitsigns.nvim'
end)
```

![image-20220729163853157](https://s2.loli.net/2022/07/29/49xsGWNmfBtVAKw.png)

### 主题配置

https://github.com/olimorris/onedarkpro.nvim

虽然之前曾经也配置过主题内容了，但是我也曾放下狠话，当我们进一步掌握了nvim之后主题也将会被调教的更加美观，于是现在我们不妨稍微进行一下进一步的配置

由于我们选择的这个主题会对其支持的插件自动适配相关颜色主题，因此我们只需要简单的开启一下字体样式的支持，我觉得就已经很美观了，在`colorscheme.lua`中添加

```lua
require("onedarkpro").setup({
    styles = { -- Choose from "bold,italic,underline"
        strings = "bold", -- Style that is applied to strings.
        comments = "italic", -- Style that is applied to comments
        keywords = "NONE", -- Style that is applied to keywords
        functions = "underline", -- Style that is applied to functions
        variables = "NONE", -- Style that is applied to variables
        virtual_text = "undercurl", -- Style that is applied to virtual text
    },
    options = {
        bold = true, -- Use the themes opinionated bold styles?
        italic = true, -- Use the themes opinionated italic styles?
        underline = true, -- Use the themes opinionated underline styles?
        undercurl = true, -- Use the themes opinionated undercurl styles?
        cursorline = true, -- Use cursorline highlighting?
        transparency = true, -- Use a transparent background?
        terminal_colors = true, -- Use the theme's colors for Neovim's :terminal?
        window_unfocussed_color = true, -- When the window is out of focus, change the normal background?
    }
})
vim.cmd 'colorscheme onedarkpro'
```

选择是全部开启，包括是透明背景，注意调整终端的背景色，当然也可以根据喜好选择，让不同的代码拥有不同的样式

### 语法高亮内插件

https://github.com/nvim-treesitter/nvim-treesitter

https://github.com/p00f/nvim-ts-rainbow

虽然上面对于treesitter的讲解已经比较详细了，但是实际上这个语法高亮插件其中还是支持套娃插件的，因此不得不提一下，比如这个彩虹括号的插件，还有之后会提及的自动注释插件（可选），我们可以在配置文件中直接引入，像是这样子配置`treesitter.lua`

```lua
require 'nvim-treesitter.configs'.setup {
    -- 代码高亮
    -- 安装 language parser
    -- :TSInstallInfo 命令查看支持的语言
    ensure_installed = require 'lsp.usable'.language,
    -- 启用
    highlight = {
        enable = true,
        additional_vim_regex_highlighting = false
    },

    -- 增量选择
    incremental_selection = {
        enable = true,
        keymaps = {
            init_selection = '<CR>',
            node_incremental = '<CR>',
            node_decremental = '<BS>',
            scope_incremental = '<TAB>',
        }
    },
    indent = {
        enable = true,
    },
    -- rainbow
    rainbow = {
        enable = true,
        extended_mode = true, -- Also highlight non-bracket delimiters like html tags, boolean or table: lang -> boolean
        max_file_lines = nil, -- Do not enable for files with more than n lines, int
        colors = {
            "#95ca60",
            "#ee6985",
            "#D6A760",
            "#7794f4",
            "#b38bf5",
            "#7cc7fe",
        },
    },
}
```

之后就可以看到漂亮的彩虹括号了（虽然没什么卵用）

### 悬浮定义

https://github.com/glepnir/lspsaga.nvim

同样是一个重量级插件，他可以提供无比美观的悬浮LSP信息提示，在之前我们可能会发现，当我们想要查询一个函数的定义，往往一敲`gd`就直接跳转到定义去了，但是实际应用中我们极少情况需要修改定义内容，往往都只是看看这个函数该怎么用而已，频繁的跳转和跳回往往让人烦不胜烦

同时由于本身主题对于该插件的支持，需要我们的配置项也就相对减少了，最终的效果如下

![image-20220729165218208](https://s2.loli.net/2022/07/29/D43VUPGaxzFdWwb.png)

虽然减少了一些色彩上面的配置，但是其余的配置还是较为繁琐，同时需要修改大量的原生LSP配置，转而使用saga提供的自定义接口，以下是配置项

- `saga.lua`

  ```lua
  require 'lspsaga'.setup({
      debug = false,
      use_saga_diagnostic_sign = true,
      -- 代码诊断相关
      error_sign = "",
      warn_sign = "",
      hint_sign = "",
      infor_sign = "",
      diagnostic_header_icon = "   ",
      -- 智能提示相关
      code_action_icon = " ",
      code_action_prompt = {
          enable = true,
          sign = true,
          sign_priority = 40,
          virtual_text = true,
      },
      -- 查询用法
      finder_definition_icon = "  ",
      finder_reference_icon = "  ",
      -- 最大显示行数
      max_preview_lines = 10,
      -- LSP不同功能快捷键
      finder_action_keys = {
          open = "<CR>",
          vsplit = "s",
          split = "i",
          quit = "q",
          scroll_down = "<C-f>",
          scroll_up = "<C-b>",
      },
      code_action_keys = {
          quit = "q",
          exec = "<CR>",
      },
      rename_action_keys = {
          quit = "<ESC>",
          exec = "<CR>",
      },
      -- 查询定义
      definition_preview_icon = "  ",
      border_style = "single",
      -- 全局改名
      rename_prompt_prefix = "➤",
      rename_output_qflist = {
          enable = false,
          auto_open_qflist = false,
      },
      server_filetype_map = {},
      diagnostic_prefix_format = "%d. ",
      diagnostic_message_format = "%m %c",
      highlight_prefix = false,
  })
  ```

- `maps.lua`

  ```lua
  m('n', 'gd', '<Cmd>Lspsaga preview_definition<CR>')
  m('n', 'gh', '<Cmd>Lspsaga hover_doc<CR>')
  m('n', 'ga', '<Cmd>Lspsaga code_action<CR>')
  m('n', 'gf', '<Cmd>Lspsaga lsp_finder<CR>')
  m('n', 'gr', '<Cmd>Lspsaga rename<CR>')
  m('n', 'gs', '<Cmd>Lspsaga signature_help<CR>')
  m('n', 'ge', '<Cmd>Lspsaga diagnostic_jump_next<CR>')
  ```

  注意将之前所有的`g*`快捷键全部替换，这才是LSP的完全体！

### 补全

改动最小的也就是代码补全了，只是额外提供了一个函数参数提示的源用以调用函数时方便查看，其余的内容都没有太大变化

要注意的是如果我们需要使用代码片段的补全源，请保证引入了`    use 'rafamadriz/friendly-snippets'`，不然会导致代码片段无法应用

### Ranger

https://github.com/kevinhwang91/rnvimr

比起用起来怪膈应的`nvim-tree`从我个人的角度来说还是更喜欢ranger的，他也是我为数不多使用的不用lua编写，不受主题支持的插件之一，想要使用也十分简单，首先我们应该保证启动环境无误

```shell
# 其中ueberzug可选，是用来显示图片类型文件的
yay -S ranger python-pynvim ueberzug
```

之后通过`checkhealth rnvimr`检查所有安装是否准备完毕

接着在`rnvimr.lua`中配置

```lua
-- 用ranger代替默认文件浏览器
vim.g.rnvimr_enable_ex = 1
-- 选择文件后自动隐藏ranger
vim.g.rnvimr_enable_picker = 1
-- 删除文件时自动删除buffer
vim.g.rnvimr_enable_bw = 1
vim.g.rnvimr_action = {
    -- 新打开文件sv和sh进行横向和纵向分屏
    sv = 'NvimEdit vsplit',
    sh = 'NvimEdit split',
}
```

### 顶部panel

https://github.com/romgrk/barbar.nvim

bufferline虽好，但是使用的主题不支持，默认的配置看上去有点膈应，因此选用了配置更简单，同样满足需求的barbar插件

在`bar.lua`中配置

```lua
require 'bufferline'.setup {
    -- 仅剩一个buffer时自动隐藏
    auto_hide = true,
}
```

会发现明明下载的是barbar，但是为什么这里引用的是bufferline，其实具体原因我也不清楚，可能是防止两个插件同时工作起冲突，总之这里的配置内容没有问题就是了

在`maps.lua`中配置

```lua
-- barbar
m('n', '<S-Tab>', '<Cmd>BufferPrevious<CR>')
m('n', '<Tab>', '<Cmd>BufferNext<CR>')
m('n', '<A-1>', '<Cmd>BufferGoto 1<CR>')
m('n', '<A-2>', '<Cmd>BufferGoto 2<CR>')
m('n', '<A-3>', '<Cmd>BufferGoto 3<CR>')
m('n', '<A-4>', '<Cmd>BufferGoto 4<CR>')
m('n', '<A-5>', '<Cmd>BufferGoto 5<CR>')
m('n', '<A-6>', '<Cmd>BufferGoto 6<CR>')
m('n', '<A-7>', '<Cmd>BufferGoto 7<CR>')
m('n', '<A-8>', '<Cmd>BufferGoto 8<CR>')
m('n', '<A-9>', '<Cmd>BufferGoto 9<CR>')
m('n', '<A-0>', '<Cmd>BufferLast<CR>')
m('n', '<A-p>', '<Cmd>BufferPin<CR>')
```

注意之前还给`q`绑定了一个关闭buffer的快捷键，如下

```lua
m('n', 'q', function()
    local n = #vim.fn.getbufinfo { buflisted = 1 }
    if n == 0 or n == 1 then return '<Cmd>q<CR>'
    else return '<Cmd>BufferClose<CR>'
    end
end, { expr = true })
```

其中的`BufferClose`同样是barbar中的指令接口

### 文件查找

https://github.com/nvim-telescope/telescope.nvim

我们经常会遇到有时候需要寻找一个藏得很深的目录文件，或者想打开一个最近刚刚打开过的文件，但是这个文件显然不在根目录下，通过ranger一级一级点显然是极没效率的，因此我们需要一个文件查找的工具辅助ranger提高生产力

此时telescope就变成了不二之选，可以说，每一个想要使用nvim办公的人一定离不开telescope，这个插件就是这么牛逼

需要在`telescope.lua`中配置

```lua
local t = require 'telescope'
t.setup({
    defaults = {
        -- 打开弹窗后进入的初始模式，默认为 insert，也可以是 normal
        initial_mode = "normal",
        -- 窗口内快捷键
        mappings = {
            i = {
                -- 预览窗口上下滚动
                ["<C-u>"] = "preview_scrolling_up",
                ["<C-d>"] = "preview_scrolling_down",
            },
            n = {
                ["q"] = "close",
            }
        },
    },
})
t.load_extension('projects')
```

同样由于主题自带了telescope的主题样式，因此免去了很多的配置工作

最主要的是还需要设置快捷键，在`maps.lua`配置

```lua
-- Telescope
m('n', '<Leader>ff', '<Cmd>Telescope find_files<CR>')  -- 全局寻找
m('n', '<Leader>fr', '<Cmd>Telescope oldfiles<CR>')  -- 最近打开
m('n', '<Leader>fg', '<Cmd>Telescope live_grep<CR>')  -- 全局文件内容寻找
m('n', '<Leader>fc', '<Cmd>Telescope current_buffer_fuzzy_find<CR>')  -- 单文件查找
m('n', '<Leader>fp', '<Cmd>Telescope projects<CR>')  -- 项目查找
```

### 项目配置

https://github.com/ahmedkhalf/project.nvim

细心的人可能发现了，在telescope的配置文件中，悄悄的混进了一行`t.load_extension('projects')`，这到底是什么玩意，其实他就是专门用来快速定位项目的插件，使用了他之后，每当我们打开一个文件，这个插件都会自动的去寻找打开文件的目录下是否存在指定名称的文件，或者指定项目的标志，就像是vscode中每一个项目一定有的`.vscode`目录，一旦检测到了指定内容，于是立即将整个目录都放进一个project的列表中，之后我们可以通过telescope读取这个列表，从而实现项目的快速定位和打开

在`project.lua`中配置

```lua
require 'project_nvim'.setup({
    detection_methods = { "pattern" },
    patterns = {
        '.git',
        '.p'
    },
})
```

非常简单是不是，之后对于任意一个打开的文件，如果该文件的目录下存在`.git`或`.p`目录或文件，这个插件就会立刻定位该目录并将其添加到`~/.local/share/nvim/project_nvim/project_history`这个文件中，之后若telescope引入project插件，并在调用`Telescope projects`的时候，就会自动去该文件中读取项目路径并显示，使我们可以快速打开项目

### 起始页

https://github.com/glepnir/dashboard-nvim

想要有一个心情愉悦的编程环境就需要有一个好的开始，因此一个漂亮的起始页肯定是不可或缺的，与此同时在起始页中我们还可以通过不同的选项卡来进入不同的工作环境，可以说是居家常备了

配置文件`dashboard.lua`如下

```lua
local d = require 'dashboard'
d.custom_header = {
    [[]],
    [[]],
    [[]],
    [[]],
    [[         _________  /\     __ __   __         __________ __                                  ]],
    [[         \_   ___ \|  |__ |__|  | |  | ____ __\______   \  | _____  _______ ____             ]],
    [[         /    \  \/|  |  \|  |  | |  | \   |  | |   |  _/  | \__  \ \___  // __ \            ]],
    [[         \     \____      \  |  |__  |__\___  | |   |   \  |__/ __ \_/   /\  ___/_           ]],
    [[          \______  /___|  /__|____/____// ____|/______  /____/____  /____ \\___  /           ]],
    [[                 \/     \/              \/            \/          \/     \/    \/            ]],
    -- [[t1111111111ifft1;1. ...............::,11t11iiiii1111111t11i11ii;L;1..,.,:,:.,;:f1111ft1111111]],
    -- [[111iii1i1tfii1t1.....................1,11;;;iii;1i11ti11i111iiii1t,;i1;..,;0CC.:L11tf1t111111]],
    -- [[1111111tt1111i:........,,,,.......,....11;1;;;;;1iiiiiitiiiii1i1i8...i0ft1LGttfi80t1t1t111111]],
    -- [[11111f11111,f....CGii;:...,.,.ifiLiGi,...1,i1;;;tiiiiiiiiiii;it,,.1G8CCtttGCCC0G00C008t1i1111]],
    -- [[1f1i111i1ff..,.;,iC8GCLttttL8GCLG8L;,.::..:1,f;;1;i;i;iii1ii11.,LCGGLttffGLi.LGG0G8Lt;t;;iit1]],
    -- [[11i1111t:.0L8LG;LGCLftffffGCGLffLGL8ffi.....1;i1;;;;;ii;iiiii.:1CC:111ftG:,,,,80L1i;;i;;;iL:;]],
    -- [[iii1i;t..G8fGLLtL88C8CtttfGiGC;,itLG8;t:;....,:1i;;;;;i;iiii:.,fCff8G:t1G,,,,fL1ft;;;1;;;;;::]],
    -- [[11itt8fCtffLLGLLG1fftLCGGiffGL:,,,,,.,f........;;;;;;i;it;i;...CftC8111G.,,.,C,Ltt;i;1:;;::;:]],
    -- [[11111it;GG0C.:,GGt11fGCGLtftGf,,,,,,,.........;;;;;;;;f:ii1.,..1ttt111f.,,,,,,1f;f;i;;;;;::::]],
    -- [[111i11t;,.,t1:,iGtti1111i11ii1,,,,,,,.........;;;;;;f,.fi1.,...,t::,,;,,,,,,,,t:if;i;if;;::::]],
    -- [[t1iiti1i,,,,,,;, t11i;i;::;:i.,,..i........,,i;;;;,,,,.f;.......tiiG1fG1i,,,,f,i;t;i;t1;::::1]],
    -- [[111ii11f1,,,,,,,,,:,ittf;1;;ii;,,i,,.......,1;;;;:..,t,.........,,,,,,,,,,,,ii,1t;iit;i;;;:;:]],
    -- [[i1i111111i,,,,,,,,,,,,,,,,,,,,,,,,,,......,;;;t,.,.,i..,........,,,,,,,,,,,,;:ifti1;i;1;;;i;;]],
    -- [[itiiii1i1i:,,,,,,,,,,,,,,,,,,,,,,,,,,...,;:i,.....,...        ..,,,,,,,,,,,,t,f1ii;ii;f;;:i1;]],
    [[]],
    [[]],
}
d.custom_center = {
    {
        icon = "  ",
        desc = "Projects       ",
        action = "Telescope projects",
    },
    {
        icon = "  ",
        desc = "Recently files ",
        action = "Telescope oldfiles",
    },
    {
        icon = "  ",
        desc = "Find file      ",
        action = "Telescope find_files",
    },
    {
        icon = "  ",
        desc = "Edit Maps      ",
        action = "edit ~/.config/nvim/lua/maps.lua",
    },
    {
        icon = "  ",
        desc = "Edit Projects  ",
        action = "edit ~/.local/share/nvim/project_nvim/project_history",
    },
}
d.custom_footer = {
    '夏の花の如く艶やかに生き、秋の枯葉の如く穏やかに终りを迎えよ',
}
```

如果看不惯字符画，那么dashboard在linux中还支持图片形式的绘制，同样是借助ueberzug，可以实现启动页彩色图片的绘制，当然从我个人来说看着终端界面显示的图片还是感觉怪怪的

```lua
d.preview_command = 'ueberzug'
d.preview_file_path = '[图片路径]'
d.preview_file_height = 12
d.preview_file_width = 80
```

字符画的网站还是比较多的，自己寻找一下即可

而对于其余的配置项，大概是看看也能看懂，无非是第一行图标，第二行说明，第三行执行指令

### 符号环绕

https://github.com/kylechui/nvim-surround

https://github.com/windwp/nvim-autopairs

对于编程的舒适度来说，第一重要的就是符号是否能够自动生成匹配的问题和选中指定单词之后时候是否能快速生成符号环绕的问题，这时候就需要两个功能强大的插件出马，同时由于这两个插件默认配置就已经很够用了，因此也就不多做介绍了，稍微需要提及的是一般来说只需要记住固定的几个快速环绕指令即可

- `ysiw[环绕符号]`可以在光标指定的单词周围生成符号，其实关键的是`ys`指令，后面跟着的`iw`指的是一个单词，可以[参考vim手册](https://vimhelp.org/motion.txt.html#object-select)
- `ds[环绕符号]`删除光标外最近符号
- `cs[原符号][替换符号]`替换光标周围最近指定符号

### 自动注释

https://github.com/numToStr/Comment.nvim

对于编程的舒适度来说，第二重要的就是是否能够快速的生成注释，需要注意的是这个插件需要注意一些奇奇怪怪的事情，比如说他就不支持在`use`函数内内置`config`的方式进行插件的注册，必须创建一个`comment.lua`在里面注册

```lua
require('Comment').setup()
```

总之就是非常诡异，之后我们还需要配一下快捷键，在`maps.lua`内配置

```lua
-- Comment
m('n', '<C-_>', 'gcc', { remap = true })
m('v', '<C-_>', 'gc', { remap = true })
```

其实是可以在配置中更改一键注释的快捷键的，但是亲测下来好像并没有效果，因此选择强行配置快捷键且关闭`noremap`，此处注意到在`vim.keymap.set`这个接口中似乎`noremap`配置项并没有什么卵用，必须使用新配置项`remap`才能生效

### 悬浮终端

https://github.com/akinsho/toggleterm.nvim

这个虽然没有那么的重量级，但是为了优化体验来说一个漂亮的悬浮终端还是非常赏心悦目的，同时这个插件也是我研究的相对久的一个，其中比较考验自己的编程能力，需要手动对终端的一些内容进行配置才能获得我自认为比较良好的体验

直接上配置文件`toggleterm.lua`

```lua
require 'toggleterm'.setup({
    size = function(term)
        if term.direction == 'vertical' then return vim.o.columns * 0.4
        elseif term.direction == 'horizontal' then return 15 end
    end,
    persist_size = false,
    open_mapping = [[<C-t>]]
})

local t = nil
local M = {}

function tm(s)
    t:close()
    t:change_direction(s)
    t:open()
end

function ifnil()
    if t == nil then
        t = require("toggleterm.terminal").Terminal:new({
            direction = 'float',
            dir = '%:p:h',
            count = 100
        })
    end
end

function M.toggleM()
    ifnil()
    if not t:is_open() then t:open()
    elseif t.direction == 'float' then tm('vertical')
    elseif t.direction == 'vertical' then tm('horizontal')
    else tm('float')
    end
end

function M.toggleS()
    ifnil()
    t:shutdown()
    t = nil
end

return M
```

看上去似乎没头没脑的，但是如果把它和快捷键映射一起看，就会理解其编写思路，下面是`maps.lua`

```lua
-- ToggleTerm
m({ 'n', 't' }, '<C-n>', require 'p_config.toggleterm'.toggleM)
m({ 'n', 't' }, '<Leader>q', require 'p_config.toggleterm'.toggleS)
```

通过结合使用`vim.keymap.set`接口的函数传参和`toggleterm`提供的个性化Terminal类，我们自定义了一个可控的个性化终端，我们可以通过`Ctrl+n`唤醒他，并连续敲打`Ctrl+n`更改终端显示位置，通过`Leader+q`关闭它，关闭后再次唤醒时，保证终端的启动目录位于当前buffer文件所在目录，此外，对于非自定义终端，我们还可以通过`[数字] Ctrl+t`（`open_mapping`设定项）来唤醒一个新的指定编号默认终端，当此终端编号不为上面`count`属性值（100）时，此终端与自定义终端互相独立不影响

之所以在初始化时为终端设定`count = 100`，为的也是不与默认启动的终端产生冲突，比如当我们单纯的按下`Ctrl+t`时toggleterm会自动启动一个终端并编号1，如果我们的终端不设定count值那同样是编号1，此时比如我们使用接下里介绍的代码执行插件在还未生成自定义终端的情况下自动启动toggleterm终端时，接着启动自定义终端，就会出现一长串的报错和警告，让我们措手不及

以上看不懂也无所谓，总之上面的配置代码就是为我们自己定制了唯一一个高度定制化的终端，严格上讲，这个自定义终端只受`Ctrl+n`和`Leader+q`控制，打开，切换和关闭，当然我们如果想要暂时隐藏挂起终端，可以使用之前配置过的`sc`快捷键隐藏，而一般的toggleterm终端，则只受`[数字] Ctrl+t`打开和隐藏，且似乎没有办法完全关闭，各个编号之间的终端相互独立

同时注意到，之前曾经我们在`maps.lua`中配置过一行`m('t', '<Leader>jk', '<C-\\><C-n>')`，这一行就是为了现在用的，在终端输入模式下，按下`leader+jk`就可以回到`normal`模式进行`sc`操作

### 底部状态栏

https://github.com/nvim-lualine/lualine.nvim

https://github.com/arkav/lualine-lsp-progress

要说美化nvim的头号种子选手，除开treesitter，那肯定就是Lualine没跑了，他可以提供十分美丽的底部状态显示，虽然其中的大多数可能我们一辈子都不会关注到到底显示了什么，但是有和没有，就是帅不帅的问题，这可是涉及到能不能装到一个好逼的重要条件

同样是由于主题默认提供了一定程度上的色彩搭配，因此省了我很多事，在`lualine.lua`中配置

```lua
require 'lualine'.setup({
    options = {
        -- 指定皮肤
        -- theme = "tokyonight",
        -- 分割线
        component_separators = {
            left = "",
            right = "",
        },
        -- https://github.com/ryanoasis/powerline-extra-symbols
        section_separators = {
            left = " ",
            right = "",
        },
        globalstatus = true,
    },
    sections = {
        lualine_c = {
            "filename",
            {
                "lsp_progress",
                spinner_symbols = { ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ' },
            },
        },
        lualine_x = {
            "filesize",
            {
                "fileformat",
                symbols = {
                    unix = ' ', -- e712
                    dos = ' ', -- e70f
                    mac = ' ', -- e711
                },
            },
            "encoding",
            "filetype",
        },
    },
})
```

和我们的p10k一个鸟样，在option内的是各个在状态之间的连接符号，而后面sections内的就是需要显示的各个状态的名称，其中`lualine_c`显示在左边，`lualine_x`显示在右边，还是十分好理解的，其中的小框框其实都是图标，安装一个nerd font就全部显示出来了

而在其中还偷偷藏了一个`lsp_pregress`配置项，他的功能十分简单，就是提示我们LSP是不是加载完了，比如我们的保存需要涉及到格式化处理，那么我们就可以等下面的进度条转完了再进行保存，避免报超时错误

### 代码执行

https://github.com/CRAG666/code_runner.nvim

一款基础的IDE，必不可少的自然是自己编写的代码能够被优雅的执行，由于通用化的项目代码的执行显然是有一丢丢的困难，要不然也不会每一种语言都可以开发一种大型的IDE了，对于我们这种菜鸟来说，能够快速的进行单文件的代码编译执行就已经很不错了，这时候我想到了vscode中的coderunner插件，在nvim中，同样存在着同类的替代插件，详细的配置如下，是不是非常熟悉

```lua
require 'code_runner'.setup({
    filetype = require 'lsp.usable'.script,
})
-- 其中script为
M.script = {
    lua = 'lua',
    cpp = 'cd $dir && g++ $fileName -o ./$fileNameWithoutExt && ./$fileNameWithoutExt && rm ./$fileNameWithoutExt'
}
```

至于为什么要将语言脚本分开写，包括之前的`treesitter.lua`中同样引用了这个模块，等到讲到格式化插件时就会详细了解

### 前置缩进增强

https://github.com/lukas-reineke/indent-blankline.nvim

在之前，我们的tab虽然代表着四个点点，但是如果面对某些内含大量不同层次缩进的语言（比如HTML标签），代码前的一大堆点点往往让我们辨认不能，不知道当前写的代码到底在哪一个缩进内，这时候一个缩进增强的插件就很有必要了

效果大概是这样的

![image-20220730000927351](https://s2.loli.net/2022/07/30/UkvqwExRaOzGKej.png)

可以显著的标识出当前光标所在缩进位

配置文件`blankline.lua`如下

```lua
require 'indent_blankline'.setup {
    space_char_blankline = " ",
    show_current_context = true,
    show_current_context_start = true,
    char = "▏"
}
```

不仅美观，实用性来说也不错

### 代码格式化

https://github.com/jose-elias-alvarez/null-ls.nvim

看到这可能有些人就疑惑了，不是说好了LSP的server已经自带了代码格式化的功能吗？咋地了，怎么又搞出来一个代码格式化的插件？

说到底，还是LSP本身的各种接口封装性太好了，导致如果我们对于某个language server的代码格式化规则不满意，我们根本没有办法对其中的规则进行修改，这时候`null-ls`就横空出世了，他学习aop的先进思想，在LSP的各个功能之间横插一刀，往language server中注入部分个性化的LSP配置覆盖原有内容，从而实现各部分功能的个性化设置，而相较于什么代码诊断，错误提醒之类的LSP接口，代码的格式化功能可以算是相对容易定制化且可定制化水平高的了，因此也就成为了大多数nvim用户引入`null-ls`的最主要原因

这也就意味着，在加入了`null-ls`之后，许多我们的LSP配置势必也将发生比较大的改变，至少我们应该根据不同的language server制定不同的策略，来判断这个language server是否应该交由`null-ls`去接管

就拿C++举例，目前唯一可用的language server仅有`clangd`一家，但是其内置的`clang-format`格式化工具好死不死的默认缩进是两个空格，这显然不符合我们设定的四个空格的要求，因此我们必须对这个格式化规则进行修正

首先我们为了区分某个language server是否交由null-ls接管，我们需要专门创建一个文件用于存储，这就是`usable.lua`文件由来

```lua
local M = {}

-- 使用的语言 :TSInstallInfo
M.language = { 'lua', 'cpp', 'markdown' }
-- LSP服务器名称 :LSPInstallInfo
M.servers = { 'sumneko_lua', 'clangd', 'marksman' }
M.n_servers = { 'clangd' }
-- 代码运行脚本
M.script = {
    lua = 'lua',
    cpp = 'cd $dir && g++ $fileName -o ./$fileNameWithoutExt && ./$fileNameWithoutExt && rm ./$fileNameWithoutExt'
}

return M
```

其中规定了由`null-ls`接管的`clangd`语言服务器，单独存放在一个table中，同时我们在`s_config`目录下相应的创建一个`n_default.lua`文件，其中内容如下

```lua
return {
    on_attach = function (client,_)
        client.resolved_capabilities.document_formatting = false
        client.resolved_capabilities.document_range_formatting = false
    end,
    flags = {
        debounce_text_changes = 150,
    }
}
```

比起`default.lua`，实际上就是在启动配置中禁用了语言服务器自带的代码格式化功能，当然你也可以所有的语言服务器都禁用，但是总该有些还是可以一用的，因此在此处做了区分

相对应的，还需要修改一下`s_config`底下的`init.lua`文件

```lua
local servers = require 'lsp.usable'.servers
local lspconfig = require "lspconfig"

for _, server in pairs(servers) do
    -- 是否个性化语言服务器
    local config = 'lsp.s_config.' .. server
    xpcall(function() require(config) end, function() config = 'lsp.s_config.default' end)
    -- 是否null-ls接管
    for _, v in pairs(require 'lsp.usable'.n_servers) do
        if v == server then config = 'lsp.s_config.n_default' end
    end
    lspconfig[server].setup(require(config))
end
```

之后我们就可以快乐的配置`null-ls.lua`了

```lua
local null_ls = require("null-ls")
local formatting = null_ls.builtins.formatting

null_ls.setup({
    debug = false,
    sources = {
        -- C/C++
        formatting.clang_format.with({
            filetypes = { 'c', 'cpp' },
            args = { '-style={IndentWidth: 4}' }
        }),
    },
    -- 保存自动格式化
    on_attach = function(client)
        if client.resolved_capabilities.document_formatting then
            vim.cmd("autocmd BufWritePre <buffer> lua vim.lsp.buf.formatting_sync()")
        end
    end,
})
```

从代码上可以看出，其中调用了`null-ls`提供的formatting接口，实现了对于LSP功能的植入，可以理解为就是在`clangd`这个language server的边上又开了一个叫做`null-ls`的language server，他们俩一起来服务于我们的某个cpp文件，对于一般的代码诊断，就交由正常的`clangd`执行，而针对所有的格式化处理（即调用了`vim.lsp.buf.formatting_sync()`这个接口的请求）则全部交由`null-ls`处理，实现了分工的明确性

同时因为有了`usable.lua`的存在，因此在接下来一旦需要添加新的编程语言支持，只需要单独修改`usable.lua`，必要时修改`null-ls.lua`即可，实现了语言与配置之间的大解耦

以上就是对我来说常用插件的配置内容了，所有的插件部分我都附上了仓库链接，篇幅限制我也肯定不能每一个插件都将其所有的功能全部写到，不然还不如直接将readme翻译一遍来的迅速，因此在了解了插件的性质之后我们要做的还是仔细阅读插件官方仓库的readme文件，从而实现真正的插件个性化配置
