#### 仅当笔录，都是基本使用。

## 一、 执行方式
shell 脚本执行方式有:**sh、bash、source与.**   
主要的区别是:
sh与bash：当前环境会启动一个子进程执行脚本，执行后会回到当前的shell环境。然而source与.(英文点)是在当前环境直接执行，所以如果在脚本中有cd操作的话会，在终端回跟着变化。

## 二、变量的使用

### 2.1 简单使用
随便写，没有类型申明，还可以混用，比如：
```
i=1
echo $i
i="123"
echo $i
```

以上简单的代码，信息量却不少。
- 1. i 被定义成了一个数字类型，还能重新赋值一个字符串。
- 2. 获取变量的值，需要在变量的前面加一个$符号
- 3. 赋值操作的=号两边，不能有空格（这一点特别的不爽）

### 2.2 只读属性
```
# 只读
readonly date2Build=`date "+%Y%m%d%H%M%S"`
```
之后的 date2Build 只能获取，不能赋值，否则报错。

### 2.3 字符串的长度
```
# 只读
readonly date2Build=`date "+%Y%m%d%H%M%S"`
# 字符串的长度
echo ${#date2Build}
```

### 2.4 变量不可用
```
name="CoderHG"
# 让变量不可用
# unset name
echo $name ${#name} ${name:0:5}
```

关键字是 unset 。 ${name:0:5} 是字符串的裁剪。

## 三、数组
```
# 数组
list1='value_1'
list2='value_2'
list3='value_3'
list=($list1 $list2 $list3)

echo ${list[1]}

echo 所有的元素值 ${list[@]}


# 取得数组元素的个数
length=${#list[@]}

# 或者
length=${#list[*]}

# 取得数组单个元素的长度
lengthn=${#list[1]}

echo 数组长度 $length  单个数组的长度 $lengthn
```

## 四、参数
```
echo "Shell 传递参数实例！";
echo "执行的文件名：$0";
echo "第一个参数为：$1";
echo "第二个参数为：$2";
echo "第三个参数为：$3";

# 输出所有的 参数
echo stat  $@ and $*  end

echo $*  $$ $! $-


echo "-- \$* 演示 ---"
for i in "$*"; do
    echo $i
done

echo "-- \$@ 演示 ---"
for i in "$@"; do
    echo $i
done

# 这个能判断是否有参数输入
# 当然、是可以通过参数的个数来判断的
if [ -n "$1" ]; then
echo "包含第一个参数"
else
echo "没有包含第一参数"
fi
```

## 五、运算符
```
# 执行计算
val=`expr 12 + 14`
echo "两数之和为 : $val"

# 大小比对
num=99
num1=9
if [ $num -eq $num1 ] 
	then
	echo '等于99'
else
	echo '不对啊'
fi
```

其实更重要的是 **关系运算符、字符串运算符与文件运算符**。


## 六、输入读取
```
read input
echo $input is a input
```

## 七、输出
```
echo "Hello, Shell"

printf "Hello, Shell\n"
printf "Hello, Shell122"

printf "%-10s %-8s %-4s\n" 姓名 性别 体重kg  
printf "%-10s %-8s %-4.2f\n" 郭靖 男 66.1234 
printf "%-10s %-8s %-4.2f\n" 杨过 男 48.6543 
printf "%-10s %-8s %-4.2f\n" 郭芙 女 47.9876 
```

## 八、流程控制
```
for loop in 1 2 3 4 5
do
    echo "The value is: $loop"
done

for str in 'This is a string'
do
    echo $str
done

int=1
while( $int<=5 )
do
    echo $int
    let "int++"
done

while :
do
    echo -n "输入 1 到 5 之间的数字:"
    read aNum
    case $aNum in
        1|2|3|4|5) echo "你输入的数字为 $aNum!"
        ;;
        *) echo "你输入的数字不是 1 到 5 之间的! 游戏结束"
            break
        ;;
    esac
done
```

## 九、函数
```
# 无参 无返回
demoFun(){
    echo "这是我的第一个 shell 函数!"
}
echo "-----函数开始执行-----"
demoFun
echo "-----函数执行完毕-----"

# 有参 无返回
funWithParam(){
echo "第一个参数为 $1 !"
echo "第二个参数为 $2 !"
echo "第十个参数为 $10 !"
echo "第十个参数为 ${10} !"
echo "第十一个参数为 ${11} !"
echo "参数总数有 $# 个!"
echo "作为一个字符串输出所有参数 $* !"
}
funWithParam 1 2 3 4 5 6 7 8 9 34 73

# 无参 有返回值
funWithReturn(){
    echo "这个函数会对输入的两个数字进行相加运算..."
    echo "输入第一个数字: "
    read aNum
    echo "输入第二个数字: "
    read anotherNum
    echo "两个数字分别为 $aNum 和 $anotherNum !"
    return $(($aNum+$anotherNum))
}
funWithReturn
echo "输入的两个数字之和为 $? !"

# 函数返回值在调用该函数后通过 $? 来获得。
```

## 十、与 AWK 的默契
AWK 的基本使用,可以参考 [linux-comm-awk](http://www.runoob.com/linux/linux-comm-awk.html)，这个教程中,，我仅仅对其中的正则表达式比较感兴趣。
![image.png](https://upload-images.jianshu.io/upload_images/1198135-7b475f6a36e658a4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来就做一个比较简单的试验，试验内容是通过 Shell 与 AWK 结合获取文档中的内容，然后做响应的字符处理。

### 10.1 创建一个文件
> touch demoFile

编辑内容为 ：
> 这是第一行
> 需要获取的行:http://www.runoob.com/linux/linux-comm-awk.html
> 这是第3行
> 这是第4行


### 10.2 获取文档总行数
直接见代码：
```
# 获取 demoFile 文档的行数
nm=`awk 'END{print NR}' ./demoFile`
echo "总共有 $nm 行"
# 输出 ：总共有 4 行
```
值得注意的是，nm 语句中的命令，不是被单引号所包裹，而是 Tab 键上方的那个英文状态的符号。

### 10.3 获取文档中某一行的内容
具体代码如下：
```
# 获取 demoFile 中带有 '需要获取的行:' 字样的行
content=`awk '/需要获取的行:/' ./demoFile`
# 打印
echo $content
# 打印结果: 需要获取的行:http://www.runoob.com/linux/linux-comm-awk.html
```
这样 **content** 就获取了整行的内容。

### 10.4 字符串截取
如何将 **content** 中的文件名(linux-comm-awk)提取出来?
找到一篇博文，挺不错的：[shell脚本字符串截取的8种方法](https://www.cnblogs.com/zwgblog/p/6031256.html)  内容如下：
![image.png](https://upload-images.jianshu.io/upload_images/1198135-37487999dec1a04d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![image.png](https://upload-images.jianshu.io/upload_images/1198135-727a36b81ab5805c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过以上的学习，可以写出以下代码：
```
# 保留最后一个 '/' 之后的内容
content=${content##*/}
echo $content
# 打印结果:linux-comm-awk.html

# 去掉.html
content=${content%%.*}
echo $content
# 打印结果:linux-comm-awk
```

本小节完整代码如下：
```
#!/bin/sh

# 获取 demoFile 文档的行数
nm=`awk 'END{print NR}' ./demoFile`
echo "总共有 $nm 行"

# 获取 demoFile 中带有 '需要获取的行:' 字样的行
content=`awk '/需要获取的行:/' ./demoFile`
# 打印
echo $content
# 打印结果:需要获取的行:http://www.runoob.com/linux/linux-comm-awk.html

# 保留最后一个 '/' 之后的内容
content=${content##*/}
echo $content
# 打印结果:linux-comm-awk.html

# 去掉.html
content=${content%%.*}
echo $content
# 打印结果:linux-comm-awk
```

Shell 与 AWK 的使用，还是挺强大的。要想玩转文档输入的高阶获取，还需更进一步的研究学习。


###### 以上就是一个记录而已



