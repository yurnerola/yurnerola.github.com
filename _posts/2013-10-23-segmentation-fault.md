---
layout: post
title: "Segmentation fault"
description: ""
category: "Gdb"
tags: []
---
{% include JB/setup %}
新上线程序core down，gdb调试出现如下两个错误：
>Program terminated with signal 11, Segmentation fault.


>Program terminated with signal 7, Bus error.
 
问题分析：

1.程序容错机制不足 ，导致程序在运营程序配置出现错误时，导致程序core down.

2.由于core后程序会不停的重启，然后不停的core down，最终将会出现整个磁盘都满了！此时，进行磁盘写将会出现Bus error.
 
 
示例源码：
{% highlight cpp %}
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
 
int main(){
    char *end="";
    //配置应给8,20,运营人员却配成了20:00:00。
    char *valStart="20:00:00";
    int i=0;
    while(i<5){
        printf("%d\n",atoi(valStart));
        end= strchr(valStart,',');
        if (end!=NULL && end>valStart){
            printf("%d\n",atoi(end+1));
        //code start add by yurnerola 
        }else{
            break;
        }
        //code end add by yurnerola 
        valStart=strchr(end,'|');
        if(valStart==NULL)
            break;
        valStart++;
        i++;
    }
}
{% endhighlight %}
