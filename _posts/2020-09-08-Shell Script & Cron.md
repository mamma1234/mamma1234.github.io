---
layout: post
title: "Shell Script & Cron"
description: 
headline: 
modified: 2020-09-08
category: Shell Script & Cron
imagefeature: cover3.jpg
tags: [Shell Script Cron]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# ~/.vimrc
- .vimrc 파일은 vim 에디터의 설정을 바꿀 수 있는 파일


```JavaScript
set smartindent
set tabstop=4
set expandtab
set shiftwidth=4
```

# shell script

```JavaScript
#!/bin/sh 또는  #!/bin/bash
echo "Hello Shell Script!"
printf "%s %s %d\n" aa bb 123
str="hello "
echo "${str}world"
echo "$str world"

$ hello world
$ hello  world
```


# loop

```JavaScript
#!/bin/sh 또는  #!/bin/bash
# 1 ~ 100 loop
for i in {1..100}; do ~ done

for i in {1..100}; do echo $i; done

for i in `ls *.txt`
do
    echo " -------------------- $i"
    cat $i
    echo "==================================="
done

```

# Variables

```JavaScript
echo "$0 $1 $#"
STR="abc"
echo $STR

i=100
ii=$(( $i + 100 ))
echo "i=${i}, ii=${ii}"

$ ./test.sh 12 3
$ abc
$ i=100, ii=200
```


# IF
```JavaScript
문자: ==    !=
숫자: -gt, eq, lt, ne, le, ge
파일: -f, -r, -w, -x


if [ $# -gt 0 ]; then
   cat $1
else
	echo "Input filename.."
fi
if [ -f t.txt ]; then
	cat t.txt
fi


if [ $# -eq 0 ]; then
    echo "Input the filename, please.."
    echo "usage) ./s4.sh <file>"
    exit 0
fi

cat $1

```

# date

```JavaScript
DATE=`date +%Y-%m-%d`
echo $DATE
DATE=`date +%Y-%m-%d --date=yesterday`
DATE=`date +%Y-%m-%d --date='1 day ago'`
DATE=`date +%Y-%m-%d --date='2 day ago'`
DATE=`date +%Y-%m-%d --date='2 day'`
DT=`date +%Y-%m-%d --date='1 week ago'`
DT=`date +%Y-%m-%d --date='1 month ago'`
DT=`date +%Y-%m-%d --date='1 month'`


if [ $# -eq 0 ]; then
    echo "Input the filename, please.."
    echo "usage) ./s5.sh <to-change-file>"
    exit 0
fi

DATE=`date +%Y%m%d`
FN="${DATE}.txt"
#echo "mv $1 $FN"

mv $1 $FN
```

# Array

```JavaScript
declare -a arr
arr=("aaa" "bbb" "ccc" 123)

echo $arr
echo ${arr[0]}
arr[4]="6666666"

echo ${arr[@]}
echo "${#arr} : ${#arr[@]}"
for i in ${arr[@]}; do echo $i; done



$ aaa
$ aaa
$ aaa bbb ccc 123 6666666
$ 3 : 5
$ aaa
$ bbb
$ ccc
$ 123
$ 6666666
```


# Function

```JavaScript
#!/bin/bash
echo "$0 $@ $#"
say_hello() {
	echo "Hello $0 $@ by $2!! ($#)"
}
say_hello "Jade" "Jeon"

$> ./s9.sh aaa
./s9.sh aaa 1
Hello ./s9.sh Jade Jeon by Jeon!! (2)
```


# IFS & AWK
- Internal Field Separator

```JavaScript
echo "IFS=${IFS}."

PRE_IFS=$IFS
IFS="
"
for i in `ls -al`; do
    echo $i | awk '{print $5}'
done

IFS=$PRE_IFS


```


```JavaScript
#!/bin/bash

PRE_IFS=$IFS

IFS="
"

cd /home/dooo

FileName="bin_files.txt"
touch $FileName

echo " -------------------------------------------- "
TOT=0
for i in `ls -al /bin`; do
    S=`echo $i | awk '{print $5}'`
    F=`echo $i | awk '{print $9}'`

    if [ "$F" == "." ] || [ "$F" == ".." ] || [ "$F" == "" ]; then
        continue
    # elif 
    fi

    #TOT=$(( $TOT + $S ))
    TOT=`expr $TOT + $S`

    echo "$S $F" >> $FileName
done

echo "Total Size is $TOT"

IFS=$PRE_IFS

```


# cron

```JavaScript
$> crontab -l
$> crontab -e
분 시 일 월 주
* * * * * /test.sh >> /temp.log 2>&1
(2: Standard Error, 1: Standard Out) 
$> ps -ef | grep cron

```
