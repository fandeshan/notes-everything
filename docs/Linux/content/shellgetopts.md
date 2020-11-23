# shell脚本获取参数

## 场景介绍

shell 脚本中经常需要传入一些命令参数，如 ``cmd -a abc -b -c dddd``或者，``cmd -name nick -disable``,本文介绍如前面列子中的参数在脚本中如何提取。


## 提取办法  

### 按位置获取 

如下shell脚本中传入的参数依次值如下：

```bash 
echo "第一个参数:"$1
echo "第二个参数:"$2
echo "第三个参数:"$3
```


### getopts获取

如脚本[getopts.sh](getopts.sh)

```bash 
while getopts 'a:bcd:' OPT; do
    case ${OPT} in
      a)
        echo "选项-a已经生效"
        echo "选项-a是可以带参数的,参数值为:"${OPTARG}
        ;;
      b)
        echo "选项-b已经生效"
        echo "选项-b是不需要参数的"
        ;;
      c)
        echo "选项-c已经生效"
        echo "选项-c是不需要参数的"
        ;;
      d)
        echo "选项-d已经生效"
        echo "选项-d是可以带参数的,参数值为:"${OPTARG}
        ;;
      *)
        echo "无效的参数"
        ;;
    esac
done
```

执行``./getopts.sh -a dd -b``,打印如下结果 

```bash 
选项-a已经生效
选项-a是可以带参数的,参数值为:dd
选项-b已经生效
选项-b是不需要参数的
```

### 遍历获取  


如脚本[for.sh](for.sh)

```bash
# ./for.sh -a --banana blala
while true; do
    case "$1" in
      -a | --apple)
          echo "I have an apple!"
          shift
          ;;
      -b | --banana)
          echo "I have a banana,banana is $2"
          shift 2
          ;;
      -c | --cherry)
          case $2 in
            '')
                echo "I have a cherry!"
                shift 2
                ;;
            *)
                echo "I have a cherry!It is $2"
                shift 2
                ;;
          esac
          ;;
      -d)
          echo "I have a dog!"
          shift
          ;;
      --)
          shift
          break
          ;;
      *)
          echo "get parameters success.!"
          # exit 1
          break
          ;;
    esac
done
echo "end of get parameters success."
```

* 执行命令测试 

```bash 
nick@nicks-MacBook-Pro  ~/Desktop/study/notes-everything/docs/Linux/content   master ●  ./for.sh -a --banana blala
I have an apple!
I have a banana,banana is blala
get parameters success.!
end of get parameters success.
```
