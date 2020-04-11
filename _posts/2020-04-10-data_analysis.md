---
layout: post
title: "Data analysis"
date: 2020-04-10 22:11:09
image: '/assets/img/'
description: 'Data analysis note'
tags:
- data
categories:
- Research
twitter_text: 'Do you know these?'

---

## Everyday sentence

11-29: I don't like rasins. They used to be fat and jucy, and now they are twisted. They had their lives stolen. They taste sweet, but really they are humiliated grapes.

12-1: We all fear death and question our place in the universe. The artist's job is not to succumb to despair, but to find an antidote for the emptiness of existence.

12-2: You know the only thing that has made the whole thing worthwhile...has been those... few times that I've been able to really, truly connect with another human being.

12-3: We are made of dreams, and dreams are made of us.

12-5: Funny, how just when you think life can't possibly get any worse it suddenly does.

12-6: 美丽的梭罗河/ 我为你歌唱 / 你的光荣历史 / 我永远记在心上 / 旱季来临 / 你轻轻流淌 / 雨季时波涛滚滚 / 你流向远方

## Pandas的基础操作

pd.read_csv('xxx.csv', names=new_columns, header=0)读取文件

pandas读取成的结构叫dataframe，他其中的每一列都叫一个series，操作类似于numpy中的矩阵，但是它还拥有行名和列名。

df.columns 可以查看所有列名。访问可以直接跟在点号后面或者以字典的方式访问。`DataFrame(df, columns=['Change', 'Ratings'])`可以取出某一些子列形成新的dataframe。赋值和修改可以用字典的方法，递交一个series列。如果用pd.Series(xxx, index = [ ])，index里还可以指定xxx的数值赋在第几个位置。

df.columns可以在直接传入列名的列表来实现批量修改，或者`df.rename(columns={'a': 'A'}，inplace=True)`取修改列名。相应的index参数是行名。

df.sum()对列求和，sum(1)对行求和。df.apply( )对每个元素进行操作，里面可以设置一个lamda函数。或者直接df ** 2也等同于对元素操作。

列扩充直接进行赋值，行扩充用df.append( )里面放一个列名对应的键值字典，index参数指定行名。

 df_b.join(df_a) 进行合并，如果索引不完全相同的话就只保留dfb的索引，缺失值用NaN填补。如果想合并并集就加上参数how='outer'

