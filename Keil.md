## Keil 及 单片机的学习

### Keil 程序新建工程

1. `project` - `New μVision Project`

2. 选择路径，指向一个预先创建好的文件夹

3. `Atmel` - `AT89C52` 

4. 任何对话框均点”否“

5. 点击左上角的 :page_facing_up: 新建一个空白文件

6. `Ctrl + S` 保存文件，后缀名为`.c` 

   >  项目名尽量为Template，文件名则为main.c

7. 右击`Source Group 1` - `Add Files to Group 'Source group 1'` - `main.c` 

8. 快乐写程序

   > `.hex` 文件在左上魔棒按钮里面的 `Output` -`Creat HEX File` 选项

### 51-单核-A2 单片机

- 初始代码

  ```c
  #include "reg52.h" // 如果选择的是AT89C51则就是"reg51.h"
  
  void main()
  {
  	while(1)
      {
          
      }
  }
  ```

- `sbit [变量名] = [地址值]` 给某个引脚取名

  - `LED P20/SDA ` 就是 `P2^0` 是单片机上第一个LED灯
  - `P15` 是蜂鸣器的输入端口，蜂鸣器为无源蜂鸣器，需要给一个震荡信号

- 检查`delay` 函数究竟延时了多少秒

  1. 在delay函数前后设置断点（双击）
  2. `Debug`- `Start/Stop Debug Session` 调出调试界面
  3. 左上角`RST` 复位初始时间
  4. 左上角`RUN` （F5） 单步执行
  5. 注意右方`Registers` - `sec` 查看每一步执行了多少时间
  6. `(Δ[显示时间])*1000` 即为毫秒数

- 循环移动函数

  ```c
  #include <intrins.h> 
  _crol_(a,b); 			// 二进制循环左移函数 
  _cror_(a,b); 			// 二进制循环右移函数
  // 其中a是移动的值，b是移动的位数
  ```

- 利用移动函数编写LED灯轮换

  ```c
  #define led P2
  led = 0xfe;					// 1111 1110	第一盏灯亮
  for (i = 0; i < 7; i++)
  {
      delay(50000);			// 延时450ms后
      led = _crol_(led, 1);	// 1111 1101	第二盏灯亮
  }
  ```

- `~` 表示取反

- 用`P22/P23/P24` 三个端口控制数码管发光，设`P22` 为A，`P23` 为B，`P24` 为C

  - `A=0;B=0;C=1` 第一个数码管亮，八进制编码以此类推

    ```c
    switch(i)
    		{
    			case(0):
    				lsc=1;lsb=1;lsa=1;break;	// P0指向第一个数码管
    			case(1):
    				lsc=1;lsb=1;lsa=0;break;	// P0指向第二个数码管
    			case(2):
    				lsc=1;lsb=0;lsa=1;break;	// 以此类推
    			case(3):
    				lsc=1;lsb=0;lsa=0;break;
    			case(4):
    				lsc=0;lsb=1;lsa=1;break;
    			case(5):
    				lsc=0;lsb=1;lsa=0;break;
    			case(6):
    				lsc=0;lsb=0;lsa=1;break;
    			case(7):
    				lsc=0;lsb=0;lsa=0;break;
    		}
    ```

  - 对于某个数码管，编码

    ```c
    int code smgduan[16] = {0x3f,0x06,0x5b,0x4f,0x66,		//0 ~ 4
                         	0x6d,0x7d,0x07,0x7f,0x6f,		//5 ~ 9
                         	0x77,0x7c,0x39,0x5e,0x79,0x71};	//A ~ F
    P0 = smgduan[0];		//默认用P0口连接数码管的插针，此时显示数字0
    ```

    > 该代码中`code`的作用是告诉单片机，定义的数据要放在ROM（程序存储区）里面，写入后就不能再更改。因为`C`中没办法详细描述存入的是ROM还是RAM（寄存器），所以在软件中添加了这一个语句起到代替汇编指令的作用，对应的还有`data`是存入RAM的意思。

    > 事实上，每一组数码管用二进制编码确定是否亮灯<img src="https://s2.loli.net/2021/12/05/Xm95NGOCzp6RVyQ.png" alt="image-20210126151206622" style="zoom:50%;" /> 
    >
    > - 从a ~ f分别表示八位二进制 `0000 0000` 从右往左的位数
    > - 例如代表1的数就是b,c两管亮起，编码为`0000 0110 = 0x06` 

