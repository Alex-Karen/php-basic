# php basic learning

困惑,如何成为高级PHP程序员or全栈程序员or架构师

## 基础巩固

PHP Hypertext Preprocessor

### 字符编码原理

双引号解析变量、转义字符(\t \r \n \\ \ddd八进制 \xhh十六位)

string中的字符可以通过一个从0开始的下标,用类似array结构中的方括号包含对应的数字来访问和修改,比如 `$str[42]`

用超出字符串长度的下标写入将会拉长该字符串并以空格填充

非整数类型下标会被转换成整数。非法下标类型会产生一个 E_NOTICE 级别错误

串行化

    大部分的 PHP 值可以转变成 string 来永久保存
    方法一：函数 serialize() 可以实现
    方法二：函数 json_encode()可以实现
    方法三：函数 var_export($items, true);

位、字节、字符

    位(bit b)指二进制中的一位,是二进制最小信息单位
    字节(Byte B)是计算机信息技术用于计量存储容量的一种计量单位
    字符( Character )是指计算机中使用的字母、数字、汗字和符号等。

字符集和字符编码

    字符集(Charset)：是一个系统支持的所有抽象字符的集合
    字符编码(Character Encoding)：是一套法则,使字符集与计算机之间建立对应关系,就是将字符转换为计算机可以接受的数字代码。就是以二进制的数字来对应字符集的字符

    ASCII

        ASCII(American Standard Code for Information Interchange,美国信息交换标准代码)是基于拉丁字母的一套电脑编码系统。
        ASCII字符集：主要包括控制字符(回车键、退格、换行键等)；可显示字符(英文大小写字符、阿拉伯数字和西文符号)
        ASCII编码：将ASCII字符集转换为计算机可以接受的数字系统的数的规则。使用7位(bits)表示一个字符,共128字符。

    ISO-8859-1

        ISO-8859-1编码是单字节编码,向下兼容ASCII,是ASCII 的扩展的一种,其编码范围是0x00-0xFF,0x00-0x7F之间完全和ASCII一致,0x80-0x9F之间是控制字符,0xA0-0xFF之间是文字符号,欧洲一些国家用,也叫Latin1

    GB 2312

        信息交换用汉字编码字符集是由中国国家标准总局1980年发布,1981年5月1日开始实施的一套国家标准,标准号是GB 2312—1980。
        GB2312编码适用于汉字处理、汉字通信等系统之间的信息交换,通行于中国大陆；新加坡等地也采用此编码。中国大陆几乎所有的中文系统和国际化的软件都支持GB 2312。
        基本集共收入汉字6763个和非汉字图形字符682个。
        GB2312的出现,基本满足了汉字的计算机处理需要,它所收录的汉字已经覆盖中国大陆99.75%的使用频率。对于人名、古汉语等方面出现的罕用字,GB2312不能处理,这导致了后来GBK及GB 18030汉字字符集的出现

        GB2312一个汉字用两个字节表示。
        原则上,两个字节可以表示 256×256＝65536 种不同的符号。
        考虑到汉字编码与其它国际通用编码,如ASCII 西文字符编码的关系,我国国家标准局采用了加以修正的两字节汉字编码方案,只用了两个字节的低7位。这个方案可以容纳 128×128=16384 种不同的汉字;
        为了与标准ASCII码兼容,每个字节中都不能再用３２个控制功能码和码值为32的空格以及127的操作码。
        所以每个字节只能有94个编码。这样,双七位实际能够表示的字数是：94×94＝8836个

    BIG5

        Big5是在1984年由台湾13家厂商与台湾地区财团法人信息工业策进会为五大中文套装软件(宏碁、神通、佳佳、零壹、大众)所设计的中文内码,所以就称为Big5中文内码。
        大五码是使用繁体中文社群中最常用的电脑汉字字符集标准,共收录13,060个中文字,其中有二字为重覆编码

    Unicode

        总数已经超过了65535,所以2个字节的数字是不够用的
        Unicode编码系统为表达任意语言的任意字符而设计,它使用4字节的数字来表达每个字母、符号,或者表意文字(ideograph)。
        Unicode 还不断在扩增,每个新版本插入更多新的字符。直至目前为止的第六版,Unicode 就已经包含了超过十万个字符。

        Unicode与utf8是什么关系:
            Unicode是字符集,UTF-32/ UTF-16/ UTF-8是三种字符编码方案

区位码

    这个方阵实际上组成一个有94个区(编号由01到94),每个区有94个位(编号由01到94)的汉字字符集。 
    一个汉字所在的区号和位号的组合就构成了该汉字的"区位码"。其中,高两位为区号,低两位为位号。这样区位码可以唯一地确定某一汉字或字符；
    反之,任何一个汉字或符号都对应一个唯一的区位码,没有重码。如“保”字在二维代码表中处于17区第3位,区位码即“1703 ”。

国标码

    国标码是由区位码稍作转换得到,是一个汉字国家标准的二进制编码。
    其转换方法为：先将十进制区码和位码转换为十六进制的区码和位码；
    这样就得了一个与国标码有一个相对位置差的代码,再将这个代码的第一个字节和第二个字节分别加上20H,就得到国标码。
    如：“保”字的国标码为3123H,它是经过下面的转换得到的：1703D－>1103H->+20H－>3123H。 (20h就是十进制的32,上文提到了“但为了与标准ASCII码兼容,每个字节中都不能再用32个控制功能码和码值为32的空格以及127的操作码”)

    国标码是汉字信息交换的标准编码,但因其前后字节的最高位为0,与ASCII码发生冲突,如 “保”字,国标码为31H和23H,而西文字符“1”和“#”的SCII也为31H和23H,现假如内存中有两个字节为31H和23H；
    这到底是一个汉字,还是两个西文字符“1”和“#”？于是就出现了二义性,显然,国标码是不可能在计算机内部直接采用的。
    于是汉字的机内码采用变形国标码,其变换方法为：将国标码的每个字节都加上128,即将两个字节的最高位由0改1,其余7位不变,如：由上面我们知道,“保”字的国标码为3123H,前字节为00110001B,后字节为00100011B,高位改1为10110001B和10100011B 即为B1A3H,因此,保字的机内码就是B1A3H;

机内码

    机内码是一个汉字在计算机内部保存的编码

    区位码前两个位换成十六进制,然后后两位换成十六进制。
    国际码=区位码(十六进制)＋2020H
    机内码=国际码＋8080H
    还记得为什么要加20H和80H么？

    01-09区为特殊符号。 16-55区为一级汉字,按拼音排序。 56-87区为二级汉字,按部首/笔画排序。 10-15区 及88-94区则未有编码。

Unicode与UCS

    国际标准化组织(ISO)、多语言软件制造商组成的统一码联盟。
    unicode,为了世界上大多数文字系统进行整理和编码。
    ISO组织也在做同样的事情, ISO开展了 ISO/IEC 10646项目,名字叫“ Universal Multiple-Octet Coded Character Set”,简称UCS。
    后来,双方意识到世界不需要2套通用的字符集,所以双方开始进行整合,到unicode2.0时,unicode的编码和ucs的编码都基本一致

unicode编码与UTF

    一个字符的Unicode编码是确定的。
    但是在实际传输过程中,由于不同系统平台的设计不一致,以及出于节省空间的目的,对Unicode编码的实现方式有所不同。Unicode的实现方式称为Unicode转换格式(Unicode Translation Format,简称为UTF)。
    简单说UCS或Unicode只是定义了从0到1114112这些数字各自对应是什么字符,而计算机上是如何实现的就是由UTF决定的。
    UTF-8、 UTF-16、 UTF-32等都是Unicode的编码实现方式。

UTF的字节序和BOM

    UTF-16编码每个字符占用了两个字节,在Macintosh (Mac)机和PC机上,对字节顺序的理解是不一致的。避免同一个文件造成错乱如何解决呢？
    Unicode规范中推荐的标记字节顺序的方法是BOM( Byte Order Mark )。
    在解释一个UTF-16文本前,首先要弄清楚每个编码单元的字节序。例如收到一个“奎”的Unicode编码是594E,“乙”的Unicode编码是4E59。如果我们收到UTF-16字节流“594E”,那么这是“奎”还是“乙”？
    Unicode规范中推荐的标记字节顺序的方法就是BOM。
    UTF-8不需要BOM来表明字节顺序,但可以用BOM来表明编码方式

    BOM含义
    开头字节        Charset/encoding
    EF BB BF　　　  UTF-8
    FE FF　　　　   UTF-16/UCS-2, little endian(UTF-16LE)
    FF FE　　　　   UTF-16/UCS-2, big endian(UTF-16BE)
    FF FE 00 00 　　UTF-32/UCS-4, little endian.
    00 00 FE FF　 　UTF-32/UCS-4, big-endia

依据UTF-8推导出汉字的unicode码

    第一步：16进制编辑模式查看UTF-8数据
    第二步：把16进制数据转为2进制数据
    第三步：依次提取3个字节末尾的4,6,6位
    第四步：组装提取出来的二进制数据,转为10进制
    第五步：放到在xml|html中显示出来

GBK和UTF8该如何选择？

    优先选择UTF-8,对程序员有利
    为了节省存储空间,选择GBK
    考虑其它系统兼容,适当选择。
    要给外国人看(韩国人),支持多语言,就选 UTF-8

### 正则

元字符 + 文本

反向引用

    使用小括号指定一个子表达式（分组）后，匹配这个子表达式的文本可以被捕获，从而在表达式或其它程序中作进一步的处理。

    默认情况下，每个分组会自动拥有一个组号，规则是：以分组的左括号为标志，从左向右，第一个分组的组号为1，第二个为2，以此类推。

    \b(\w+)\b\s+\1\b

引擎

    正则引擎主要可以分为两大类：一种是DFA，一种是NFA。
    NFA表达式主导
    DFA文本主导
    解释正则表达式 /pe(nciil|mcil|ncil)/ 尝试匹配“this is pencil”两种引擎的不同。
    一般而论，DFA引擎则搜索更快一些。但是NFA以表达式为主导，更容易操纵，因此一般程序员更偏爱NFA引擎！

    如何判断当前程序使用的引擎？

    是否支持忽略优先量词和分组捕获？
    支持  NFA
    不支持 DFA
    
    使用DFA引擎的程序主要有：
    awk,egrep,flex,lex,MySQL,Procmail等；
    使用传统型NFA引擎的程序主要有：
    GNU Emacs,Java,ergp,less,more,.NET语言,PCRE library,Perl,PHP,Python,Ruby,sed,vi；

回溯

    NFA引擎，最重要的性质就是它依次处理各个自表达式，遇到需要在两个可能成功的可能中进行选择的时候，他会选择其一同时记住另一个，以备稍后可能的需要。
    回溯就像是在道路的每个分岔口留下一小堆面包屑。
    如果需要在“进行尝试”和“跳过尝试”之间选择，对于匹配优先量词，引擎会优先选择“进行尝试”，而对于忽略优先量词，会选择“跳过尝试”。
    距离当前最近储存的选项就是当本地失败强制回溯时返回的。使用的原则是LIFO。
    回溯是NFA的灵魂。

优化技巧

    化简量词
    .*与(?:.)*在逻辑上是相等的，但是前者速度要更快，引擎内部做了优化。
    尽量使用非捕获的括号
    消除不必要的字符组
    [.]与\.在逻辑上是相等的，但是后者更快。
    字符组优于多选结构
    [abc] 优于 a|b|c
    忽略优先还是匹配优先，具体情况具体分析。
    同样情况下，匹配优先速度更快。

    视情况使用起始锚点^
    加上^，如果开头匹配不了，那么其他地方也理应匹配不上。
    从量词中提取必须的元素
    aa* 替代 a+    bbb{0,7} 替代 b{3,10}
    提取多选结构开头的必须元素
    th(?:is|at) 替代 this|thiat
    独立出起始锚点^
    ^(?:abc|123) 替代 ^abc|^123
    将最有可能匹配的多选分支放到前头（先迈最好使的腿）

### PHP编码技巧

编写代码的“四项基本原则”

    正确的实现功能
    执行的速度要快
    占用系统资源少
    后期维护方便

最重要的命名注意事项

    命名要有实际含义
    命名风格保持一致
    不用拼音命名
    不用语言关键字

适当的使用注释

    好的代码应该是自描述的
    难以理解的地方加上注释
    函数的功能加上注释说明
    类的功能和使用方法加注释

使用一个变量，需要初始化

优先使用单引号

    `$row[‘id’]的效率是$row[id]的7倍`

用“1==$a” 替换 “$a==1”

防御式编程思想

    保护程序免遭非法输入数据的危害
    错误处理技术
    异常处理
    隔离程序，使之相互影响小
    因地制宜的防御，过度防御会增加复杂度

用自己可控的环境参数

    明确包含文件的路径
    给予恰当的默认值
    自定义错误报警的级别
    不依赖系统环境参数，程序要动态了解所处的环境

    不要相信外部的一切输入

纯 PHP 代码，最好在文件末尾删除 PHP 结束标记

坚持字符编码统一

    header("Content-type: text/html;charset=utf-8");

error_reporting(7)

优先使用PHP内置函数

    usort — 使用用户自定义的比较函数对数组中的值进行排序 
    rawurlencode — 按照 RFC 1738 对 URL 进行编码
    parse_url — 解析 URL，返回其组成部分
    http_build_query — 生成 URL-encode 之后的请求字符串
    exif_imagetype — 判断一个图像的类型
    levenshtein — 计算两个字符串之间的编辑距离
    uniqid — 生成一个唯一ID
    get_browser — 获取浏览器具有的功能
    get_defined_vars — 返回由所有已定义变量所组成的数组
    str_word_count — 返回字符串中单词的使用情况

屏蔽错误非常低效

    养成不用@的习惯

时刻备份源代码

记住有效期原则

    不要随便相信网上的那些PHP优化50则之类的东西，记住一切都有有效期，要善于自己去验证

#### PHP语法糖

echo的逗号和点号

    逗号优先于点号

用i+=1代替i=i+1

用isset代替strlen

    strlen()函数函数执行起来相当快，只返回在zval 结构中存储的已知字符串长度。但是由于strlen()是函数，多多少少会有些慢。

用strtr代替str_replace

    由于底层实现原理的不一样，strtr函数的效率是str_replace函数的四倍。

PHP用yield实现协程

    好多内部函数，特别是迭代有关的函数应该都有可能进行优化

用 “[]” 定义数组

用 ** 进行幂运算

用 ... 定义变长参数函数

函数赋值默认参数：+ 运算符

?? 运算符

<=> 比较运算符

if的使用技巧之“给定初始值”

if的使用技巧之“用"&&" 替换 if”

if的使用技巧之“三元运算符替换”

简化“三元运算符”

if的使用技巧之“去掉多此一举的if”

循环语句几个要点

    用while(true) 表示无限循环，别用for
    特定情况下[发邮件、采集网页]，要加延时sleep
    循环体内尽可能不用函数或更耗资源的调用
    foreach代替while和for循环（PHP）
    避免空循环
    只做一件事,尽可能短，控制在50行以内
    循环嵌套限制在3层以内

使用更精悍短小的代码

    函数的最佳最大长度是50-150行代码
    函数参数不超过7个
    短小函数更容易理解也方便修改
    只做一件事情的函数更易于复用
    短小的函数测试更方便

复杂的逻辑表达式做成布尔函数

永远不要复制粘贴雷同的代码

PHP重点新特性

    文件上传进度 session.upload_progress
    short_open_tag 无论是否开启，都可用
    动态访问静态变量
    异常可以嵌套
    const 关键字可用来在类定义之外定义常量了
    Heredoc 结构中可以用双引号来声明标识符了
    添加 Nowdoc 语法支持
    增加 goto 操作符
    后期静态绑定
    default_charset从ISO-8859-1已经变为UTF-8
    新增了动态访问静态方法的方式
    内置用于开发的 CLI 模式的 web server
    实例化时访问类成员 (new Foo)->bar();
    对函数返回数组的成员访问解析 print func()[0];
    新增二进制直接量 $bin = 0b110011;
    boolval() 函数
    新增 array_column() 函数
    直接通过下标获取访问数组和字符串字面量的元素或字符
    empty() 支持传入一个任意表达式，而不仅是一个变量
    foreach 支持 list()
    新增 finally 关键字
    新增 Traits
    函数返回值类型声明,标量类型声明

PHP基本编码规范

    PHP代码文件必须以 <?php 或 <?= 标签开始；
    PHP代码文件必须以 不带BOM的 UTF-8 编码；
    PHP代码中应该只定义类、函数、常量等声明，或其他会产生 从属效应 的操作，二者只能选其一；
    命名空间以及类必须符合 PSR 的自动加载规范：PSR-4；
    类的命名必须遵循 StudlyCaps 大写开头的驼峰命名规范；
    类中的常量所有字母都必须大写，单词间用下划线分隔；
    方法名称必须符合 camelCase 式的小写开头驼峰命名规范。

### PHP数组原理和高级应用

什么是HashTable

    哈希表，是根据关键字（Key value）而直接访问在内存存储位置的数据结构。也就是说，它通过把键值通过一个函数的计算，映射到表中一个位置来访问记录，这加快了查找速度。这个映射函数称做哈希函数，存放记录的数组称做哈希表。

    hash table，又叫哈希表，散列表，Hash表。
    这种数据结构通过key->value的映射关系，使得普通的查找和插入、删除操作都可以在O(1) 的时间内完成。
    key->value的映射是通过Hash函数来实现的。

PHP数组Hashtable结构体

```c
typedef struct _hashtable {
    uint nTableSize;        // hash Bucket的大小，最小为8，以2x增长。
    uint nTableMask;        // nTableSize-1 ， 索引取值的优化，193491849 & 127
    uint nNumOfElements;    // hash Bucket中当前存在的元素个数，count()函数会直接返回此值。
    ulong nNextFreeElement; // 下一个数字索引的位置
    Bucket *pInternalPointer;   // 当前遍历的指针foreach比for快的原因之一,reset, current遍历函数使用
    Bucket *pListHead;          // 存储数组头元素指针
    Bucket *pListTail;          // 存储数组尾元素指针
    Bucket **arBuckets;         // 存储hash数组,实际的存储容器
    unsigned char nApplyCount; // 标记当前hash Bucket被递归访问的次数（防止多次递归）
} HashTable;
```

Bucket结构体

```c
typedef struct bucket {
    ulong h;            // 对char *key进行hash后的值，或者是用户指定的数字索引值
    uint nKeyLength;    // hash关键字的长度，如果数组索引为数字，此值为0
    void *pData;        // 指向value，一般是用户数据的副本，如果是指针数据，则指向pDataPtr
    void *pDataPtr;     //如果是指针数据，此值会指向真正的value，同时上面pData会指向此值
    struct bucket *pListNext;   // 整个hash表的下一元素
    struct bucket *pListLast;   // 整个hash表该元素的上一个元素
    struct bucket *pNext;       // 存放在同一个hash Bucket内的下一个元素
    struct bucket *pLast;       // 同一个hash bucket的上一个元素
    const char *arKey;          // 保存当前key所对应的字符串值
} Bucket;
```

数组转换为字符串（序列化、持久化）

    为什么要序列化？
    Api接口通信
    数据缓存
    数组数据持久化（例：保存到数据库中）
    序列化的方法？
    方法一：函数 serialize() 可以实现
    方法二：函数 json_encode ()可以实现
    方法三：函数 var_export($items, true);
    方法四：xml、其他自定义文件格式…
    方法五：mcpack、protobuffer等二进制序列化方式

+运算符 对比 array_merge

    array_merge
    一个数组中的值附加在前一个数组的后面
    字符串键名，则该键名后面的值将覆盖前一个值
    数字键名，后面的值将不会覆盖原来的值，而是附加到后面。
    数字键名将会被重新编号。
    也可以是一个参数，并且该数组是数字索引的，则键名会以连续方式重新索引
    +运算符
    把右边的数组元素附加到左边的数组后面，两个数组中都有的键名（索引和数字），则只用左边数组中的，右边的被忽略。

    array_merge ：覆盖，相同数字键追加。
    +运算符：补充，相同数字键忽略。

PHP数组元素的过滤和移除

    方法1：直接用unset移除元素
    方法2：array_slice从数组中取出一段
    方法3：array_splice把数组中的一部分去掉并用其它值取代
    方法4：用array_filter过滤元素
    方法5：用array_shift()将开头的元素移出数组
    方法6：用array_pop ()将最后一个元素弹出

PHP数组排序的原理

    由于数组排序并不会改变数组中的元素，而只是改变了数组中元素的位置，因而，对底层而言，实际上只是对全局的双链表进行排序。
    申请n个额外的空间（n是数组元素个数）
    然后遍历双链表，将双链表的每个节点存储到临时空间
    调用排序函数zend_qsort（内部是快速排序算法）对数组进行排序
    排序之后，双链表中节点的位置发生了变化，因而需要调整指针的指向。
    遍历数组，分别设置每一个节点的pListLast和pListNext
    最后设置HashTable的pListTail

PHP数组函数分类

    数组遍历相关函数：如prev, next, current, end,reset, each等
    数组排序相关：如sort, rsort, asort, arsort, ksort, krsort, uasort, uksort
    数组查找相关: 如in_array, array_search, array_key_exists等
    数组分割、合并相关： array_slice, array_splice, implode, array_chunk, array_combine等
    数组交并差：如array_merge, array_diff, array_diff_*, array_intersect, array_intersect_*
    作为stack/queue容器的数组： 如array_push, array_pop, array_shift
    其他的数组操作：array_fill, array_flip, array_sum, array_reverse等

输入流 php://input

    $_POST VS php://input
    仅在取值为application/x-www-data-urlencoded和multipart/form-data时，php会将http请求body相应数据会填入到数组$_POST，填入到$_POST数组中的数据是进行urldecode()解析的结果。
    只要Content-Type不为multipart/form-data， php://input会填入post数据。
    仅当Content-Type为application/x-www-form-urlencoded且提交方法是POST方法时，$_POST数据与php://input数据才是一致的。

    $HTTP_RAW_POST_DATA VS php://input
    php://input可以读取没有处理过的POST数据。相较于$HTTP_RAW_POST_DATA而言，它给内存带来的压力较小。
    This feature has been DEPRECATED as of PHP 5.6.0. 

### PHP文件核心编程

### Linux原理和应用

### PHP选项和运行原理

### 深入http协议

### javascript精髓

### PHP安全攻防

### PHP数据结构

### NoSQL技术

### MYSQL高级应用

### PHP高级特性
