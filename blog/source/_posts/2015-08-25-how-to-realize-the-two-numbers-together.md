---
layout: post
title: Javascript实现两个超大数字的相加
date: 2015-08-25
comments: true
categories: [javascript]
---

两个超大数字相加的实现

分析：由于数字类型长度限制，故两个超大数字应为字符串类型。因此两个超大数字相加实则为两个字符串按”加法规则“计算即可，下面为一个简单的实现方式：

    function result(str1, str2){
        var arr1 = str1.split('').reverse();
        var arr2 = str2.split('').reverse();
        var step = 0, arr3 = [], 
            max = Math.max(arr1.length, arr2.length),
            min = Math.min(arr1.length, arr2.length);

        for(var i = 0; i < min; i++){
            var tmp = Number(arr1[i]) + Number(arr2[i]) + step;
            console.log(tmp,step);
            if( tmp >= 10){
                step = 1;
                arr3.push(tmp -10);
            } else {
                step = 0;
                arr3.push(tmp);
            }
        }

        if(arr1.length == arr2.length){
            if(step > 0){
                arr3.push(step);
            }
        } else {
            arr3 = arr3.concat(arr1[min] ? arr1.slice(min) : arr2.slice(min));
        }

        return arr3.reverse().join('');
    }

    result('11111111111111111111111111111111','2222222222222222222222222222222'); //结果 13333333333333333333333333333333

如果有错误之处，欢迎指正，谢谢！

