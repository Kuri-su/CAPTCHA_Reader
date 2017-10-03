## CAPTCHA_Reader_by_zhengfang
<small>针对正方教务系统验证码 识别</small>
 
[EN]()


`安装和使用步骤整理中`<br/>
`代码重构中`<br/>
`原理与更新计划添加中`<br/>

##### 目前字典大致为2200条左右，识别率基本站稳85%,可以确保请求三次之中一定有一次是识别正确的，内网环境下单次完成时间在1.5s-2s，外网环境下完成时间可能会在2.5-3s之间，
* <small><b>PIN Identify by fangzheng.php</b> 为主文件<br/></small>
* <small><b>PIN Identify lib.php</b> 为其函数库<br/></small>
* <small><b>downloadImg.php</b> 用于download验证码<br/></small>
* <small><b>AddDictionary.php</b> 用于添加字典<br/></small>
* <small><b>zidian.sql</b> 为字典，建一个叫'yzm'的数据库导入即可<br/></small>

## Examples

    
[正确率测试 地址](http://kuri-su.cc/PIN/Identify_online.php "kuri-su.cc")<br/>

[正确率批量测试 地址](http://kuri-su.cc/PIN/AccuracyTest.php "kuri-su.cc")<br/>
> 批量测试设置了一次加载五个方正验证码，大概等待时间在13s左右

<br/>

## 更新计划
* 重构代码，改为面向对象风格，松耦合，方便更换各块的策略
* 将字典储存转为JSON储存，一次性读入内存，去掉数据库读取的时间
* 使用swoole多线程识别
* 以PHP拓展的方式重写核心函数，降低核心函数的时间复杂度

* 增加多个字典和策略
* 增加对青果验证码的支持


<hr/>

>point:如果因为获取验证码的教务系统响应缓慢或者无法响应，正确率测试的地址会因为无法获取到验证码图片而产生504错误/响应过长，可以考虑把脚本下载到本地将目标url换成本校的教务系统验证码url再做测试

>point:  <font color=#5dadff>PS：目前认为运算效率的瓶颈在 similar_text()  这个核心函数上，函数的作用在于对比两个字符串的相似程度，但是其算法时间复杂度T(n) = O(n^3) ，所以准备用T(n) = O(m*n)动态规划实现一个相类似的函数去代替该函数，以提高性能，时间未定。。。</font>

>point:  <font color=#5dadff>PSS：然后试着用php写了个动态规划，发现完全跑不出来时间太长了，然后现在考虑用C++写个拓展看看，直接封装一个函数，跑的O(m*n)的C++应该会快很多</font>


