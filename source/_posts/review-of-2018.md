---
title: review-of-2018
date: 2019-01-25 15:22:10
tags: 
    - 工作日志
    - 年终总结
category: 工作
---

## 统计

### 外包项目

1.  HHCrawler - 上海车险保单爬虫一期 (2018/03/14 - 2018/04/23)

    该项目是 2018 年做的第一个外包项目，主要功能是一个需要手动触发的爬虫系统，系统难点是数据需要通过短信验证码登陆和过滑块验证才能够获取。

    一期项目基本功能完成，稳定性在 80 % 左右，即 100 个请求 大概会失败 20 个。

    所用架构依然是我最熟悉的 python 爬虫架构， 即 : django/celery/selenium/web-driver/rabbitmq/mysql


2. HHCrawler - 上海车险保单爬虫二期 (2018/05/01 - 2018/07/12)

    该项目二期主要任务目标是为客户对接多家手机验证码接收平台和 ip 代理平台，以保证程序运转的稳定性。

    原因是很多三方接码平台的手机号质量不同，有些号码无法正常收码，而且这些三方平台大多使用同一套系统，会不定时 DOS ，所以应客户需求，对接了多家平台。


3. HHBchain - 区块链虚拟货币对冲交易系统 (2018/04/23 - 2018/08/29)

    该项目是 2018 年最有挑战性，最难做的项目，陆陆续续开发了 4 个月左右的时间，由于这个项目需要
    我独立开发完成，而且客户很多细节没有想好，业务中途变更频繁，导致了开发时间的延长。

    该项目的主要业务是根据各个不同交易所对同种虚拟货币的不同市价，在多个交易所同时对一种货币进行交易
    赚取交易所之间的差价头寸的软件平台。

    由于对业务不是很熟，开发期间我还专门去研究了对冲基金的相关金融知识，简单来说就是如果机场想在油价升高而不提交票价的条件下拥有和油价升高之前相同利润的话，那就需要去买入石油期货或是股票就可以了。

    技术上使用了 zeromq 这个组件来接收客户自己写的一套交易行情信息系统发出的数据，收到之后发到 rabbitmq， rabbmtmq 再到后端的 celery 里， 最终 celery 负责执行任务。

    架构也很朴素， zeromq/rabbitmq/celery/mysql/django , 交易所中间件使用  ccxt-python 来规避不同交易所的 api 差异问题。

4. HHRobot - 苹果园机器人采摘可视化仿真程序 (2018/09/01 - 2018/10/16)

    该项目是受一位新西兰客户的委托，开发一套机器人采摘苹果的仿真程序。

    该客户是一名大学的研究员，该客户的同事完成了仿真系统的开发，需要加上可视化的功能给客户去做演示，我的主要工作就是去开发可视化系统，但是后期出了一些问题，我发现客户那边开发的仿真程序是有问题的，没有
    办法和可视化程序集成在一起，具体就是，客户的程序不是实模式仿真，可视化的组件需要实时仿真，只要软实时就可以，所以我重写了仿真程序。

    该程序的难点是对仿真程序的理解，因为是第一次写这样的程序，期间为了完成项目，经历了 3 个连续通宵，不过好在最终还是如期完成了项目。

    使用的架构也是我第一尝试使用， PyQT/Python3.7/SimPY 

5. HHSpider - 百度百家爬虫系统  (2018/11/26 - 2019/01/04)

    该项目的主要业务是爬取百度百家每个账号的前 20 篇文章，业务很简单，但是却出了大问题。

    问题就是，项目结尾的时候，客户问我爬取效率，我跟他说如果要速度块就最好准备一台配置
    高一点的机子，起初他给了我一台 2H4G ， 这个是绝对没办法秒抓的，我就如实告诉了他，
    他没有办法只好升级配置到 8H16G, 等我调优之后，cpu 跑满可以每秒抓取  800 篇文章。
    这个时候代理流量和 阿里云流量就不太够用了，客户不愿意花钱太多，而且我感觉那个时候他就已经有了
    不想付款的打算。

    之后他以各种理由推托付款，到最后不付款，我只好找了经理仲裁他，最后少收了他好多钱。
    做项目挣的都是辛苦钱，但是总有居心不良的人，所以还是得为万事防备着点。

6. HHPrinter - 热敏打印机数据转发程序 (2018/09/05)

    这是本地一个想创业的朋友拜托我给他做的，软件的功能非常简单，
    用笔记本电脑开蓝牙伪装成热敏打印机，手机连接之后，发送要打印的数据过来，
    程序收到数据，做一些更改，再传给打印机完成打印。

    这个项目的完成度不高，项目价钱也很低，完成了第一期之后，客户就不了了之了，
    依我看，现在的年轻人太浮躁了，恨不得创业的项目就是造一台印钞机。


### 开源项目

*  [django-easy-validator](https://github.com/youngershen/django-easy-validator)

    非常简单的 django 的数据校验模块，模仿了 laravel 的调用方式，完成度  9.
        
    写这个的原因也非常简单， django form 我是从来不用的。

* [easy-captcha](https://github.com/youngershen/easy-captcha)

    非常简单的验证码图片生成模块，自带中文字体，而且有几种风格可选，未来还会加入语音。
    完成度 7.

    做这个的原因也是 django-simple-captcha 不太好用，自己干脆写一个自己用得了。现在
    比较遗憾的是目前支持的样式比较少，而且不支持字体的拉伸和变形, 今年抽时间完善.

* [django-easy-captcha](https://github.com/youngershen/django-easy-captcha)

    [easy-captcha](https://github.com/youngershen/easy-captcha) 与 django 的集成，目前
    还没开发到可用状态，一直没有时间做，希望年后可以完善。

    完成度 1.

* [kungfucms](https://github.com/youngershen/kungfucms)

    KungfuCMS, 名字我想了很久，最终取了 功夫 这个词，感觉很棒。

    做这个的原因是没有找到适合我平时开发业务的 CMS， 所以抽时间
    自己写一套，目前还没有到可用状态。

    完成度 3.

### 学习

#### 为学历提升而进行的学习

因为荒废了学生时代的学业，所以如果想成为为高等级的程序员的话，有些知识是跨越不了的，所以
学历提升计划一定要贯彻。

1. 计算机操作系统 (学到了第一章)
2. 计算机网络 (学到了第三章)
3. c 语言 (还没有开始)
4. 高等数学 (还没有开始)
5. 数据结构 (还没有开始)

总的来说，专业知识的学习是非常困难的，因为它很枯燥，而我则有时候脑袋里天马行空，无法安静下来，
所以这对我来说，不只是学习知识，更是内心的修行。

#### 电吉他技术学习

电吉他是我小时候就非常喜欢的一种乐器，记得以前第一次听的独奏曲目是 小泽正成的 "Attraction",也就是
天下足球的配乐，真的是非常好听，那个时候我就想如果能拥有一把自己的电吉他就好了，现在终于通过自己
的努力，拥有了好几把虽然不算好，但是至少可以弹奏的电吉他，但学习的路途任重道远。

在这个追名逐利的年代，有时候感觉自己戾气太重太浮躁，所以我把电吉他的修行当作修身养性，如果时常做一些不为追求利益的事情，会让我的心境变得平和起来，我觉得这对人是很有帮助的，所以我会坚持做这些事。

而且我会用我自己的方法练习，我自己喜欢的方法，我没必要非要成为职业乐手，出名，一天挣几十万，这样想就完全与我的目标冲突了，我只想自己安静的享受这把吉他带给我的快乐，一种禅的快乐。

1. 爬格子 (基本熟练)
2. 自然音阶 (目前只练了 C 大调的几首歌曲)
3. 和弦 （只学会了两首儿歌的弹唱）
4. 乐理 (只买了书，还没有开始学习)


### 游戏

最近几年游戏玩的越来越少，主要是有了其他的 想法，所以游戏对生活的调节作用大大降低了，但是我还是有朝一日希望能和瑞瑞一起玩游戏，比如他选 敌法，我就选 光法， 就这样，我会让他知道，无论如何我都会设法保护他，哪怕是在游戏里，但是他也得有深入敌军，孤军奋战的时候，到他习惯这件事了，他也就长大了，人生需要自己去品位，哪怕是困苦潦倒无助的一生。

1. 守望先锋 (300+ 小时)
2. Dota2 (100+ 小时)
3. 传奇私服 (100+ 小时)
4. 火炬之光2 (20+ 小时)

### 电影/电视剧

我一直很热衷于看电影看电视剧，特别喜欢美剧，所以我的思想被西化的比较厉害，平时工作虽然紧张，但是美剧没有落下，“堕落街” 是我本年度最喜欢的片子, 其次是风骚律师。

1. 堕落街 (The Deuce)
2. 创业公司 (Start Up)
3. 权力的游戏 (Game Of Throne)
4. 西部世界 (West World)
5. 风骚律师 (Better Call Saul)

等，其他的都没有印象了，最喜欢的就是这几个系列.

### 音乐

这一年听的歌不多，看的现场也不多，所以记忆中的内容就很少，内心深处还是想学吉他。

* 最喜欢的曲子 Andy Timmons -> Electric Gypsy .
* 最佳现场 Scarlet Aura -> 邯郸魔符 LiveHouse .

## 工作

* 这一年一共做了 6  个项目， 成功获得客户好评的有 4 个， 我给自己评价为 7 分， 满分是十分，原因是有些事确实是我出了披漏，在这里向客户道歉。

* 这一年收入尚可，由于和父母一起居住，省了很多钱，所以自己也能够存一些钱以备不时之须。

* 工作方式上已经可以逐渐总结出自己的一套方法论了，所以觉得工作上的事成熟了不少，但是还是有待提高的。

## 生活

* 瑞瑞的出生让我的生活焕然一新，自己也体会到了父亲爱孩子的那份感动。
* 和小坏熊的生活更融洽了，我也更爱她了，她已经是我最好的朋友了，我只想和小坏熊还有瑞瑞在一起，谁也不能让我们分开。
* 对自己目前的生活还是很满意的，已经能体会到这种平淡真实的幸福滋味了，但是对生活的探索还需要继续，谁知道明天会不会打仗呢!

## 总结

对生活的探索还要继续，所以在这里给自己一些忠告，争取能够早日改进自己的这些问题。

* 执行力有待提高。我实在是有点肉，做事不够快狠准，有点拖沓，这一点坏了不少事，急需改正。


* 情商有待提高。 平时和客户交流的时候，有时候不能使用恰当的方法，没有仔细揣摩客户的意图导致了很多问题，所以从现在开始必须认真揣摩客户的意图，并且选用适当的方法和客户沟通。


* 分析问题的能力有待提高。 有时候不能够站在高处看问题，如果一直在局部看问题，那么难免会横看成岭，让自己的方案不够完美。


* 专注力有待提高。 三心二意一直是我的一个大毛病，具体就是体现在工作当中，我没法快速的进入状态，总是要玩几个小时游戏，听几个小时音乐之后再开始工作，所以遇到紧张的项目非得通宵不可，这是一个大问题，必须要在 2019 年克服掉。

* 业务能力需要提到。 目前公司已经注册满 3 年了， 每年都要交很多钱，但是这个公司资质并没有派上用场，目前我所有的业务都是从程序员客栈接到的项目，所以在新的一年，我希望能够用上这个公司，实现自给自足的项目盈利，逐渐摆脱外包，毕竟这不是长久之计。

* 顶级程序员的能力。 我的理想职业是成为 Linus 那样的内核开发者，把自己的代码留存在这个繁华的世界里，是一件很有趣的事情，我的代码会替我活着，要为了这个目标努力才可以。

大概就是这么多了，希望 2019 年能有新的发现！
