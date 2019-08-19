<Chapter 1: Loading and Execution>

# JavaScript performance in the browser can be seen as the most important usability issue facing developers. The problem is complex because of the blocking nature of JavaScript, which is to say that other things cannot be handle by browser while JavaScript code is running(being executed). Actually(In fact), most browsers uses a single process for both UI updates and JavaScript execution, so only one can happen at any given moment in time. The longer JavaScript takes to execute, the longer it takes before the browser is free to response to user input.

```
usability issue 可用性问题

complex vs complicated
  complex 指系统中组件级别的复杂，complicated 指难以解决或难以理解的复杂
```

# On a basic level, this means that presence of a <script> tag is enough to make the page wait for the script to be parsed and executed. Whether actual JavScript code is inline or included in an (unrelated) erternal file is irrelevant, the page download and rendering must stop and wait for the script to complete before proceeding. This is a necessary part of the page's lify cycle because the script may cause changes to the page content while executing. The typical case is the document.write() function, for example:

<html>
<head>
  <title>Script Example</title>
</head>
<body>
  <p>
  <script type="text/javascript">
    document.write("The date is " + (new Date()).toDateString());
  </script>
</p>
</body>
</html>

# When the browser encounters a <script> tag, just as HTML page above, there is no way of knowing whether the JavaScript will insert content into the <p> tag. Therefore, the browser stops processing the page as it comes in, executes the JavaScript code, then continues parsing and rendering the page. The same takes place for JavaScript loaded using the "src" attribute loading JavaScript. The browser have to first download the external file's code(The browser must first download the code from the external file), which takes some time, and then parse and execute the code. During this process, page rendering and user interaction are completely blocked.

# Script Positioning

# HTML 4 specification indicates that a <script> tag may be placed inside of the <head> or <body> tag in an HTML document and may appear any numbers of times within each. Traditionally, <script> tags that are used to load external JavaScript files. Besides such code, the <head> also includes <link> tags to load external CSS files and other page's middleware. That is to say, it would be better to keep as many style and behavior dependencies together, loading them first to make the page can get right appearance and behavior(loading them first so that the page will come in looking and behaving correctly). Such as:

<html>
<head>
<title>Script Example</title>
<-- Example of inefficient script positioning -->
  <script type="text/javascript" src="file1.js"></script>
  <script type="text/javascript" src="file2.js"></script>
  <script type="text/javascript" src="file3.js"></script>
  <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body> 
  <p>Hello world!</p>
</body>
</html>

# Though this code seems to be harmless(innocuous), but they actually has a performance issue: It loaded three JavaScript files in the <head>(there are three JavaScript files being laoded in the <head>). Since each <script> tag blocks the page from continuing to render until it has fully downloaded and executed the JavaScript code, users must bear this visible delay. Please remember that(Keep in mind that) browsers don't start rendering anything on the page until it encounters <body> tag(the opening <body> tag is encountered). Putting scripts at the top of page in this way typically leads to a noticeable delay, usually mainifested as: When the page is opening, a blank page is first, but at this moment, the user neither can read nor can make interactions with the page. In order to understand this process better(To get a good understanding of how this occurs), we use a waterfall diagram to describe the downloading process of each resource(it's useful to look at a waterfall diagram showing when each resuource is downloaded). Figure 1-1 shows the downloading process of each script file and each style file while page loading process(Figure 1-1 shows when each script and the stylesheet file get downloaded as the page is loading).

```
file1.js
file2.js
file3.js
styles.css
```

# Figure 1-1 shows an interesing pattern. The first JavaScript file begins to download and blocks any of the other files from downloading in the meantime. Further, there is a delay between the time at which file1.js is completely downloaded and the time at which file2.js begins to download. that is the time needed of the file1.js to be fully executeed(That space is the time it takes for the code contained in file1.js to fully execute). Each file must wait until the previous file has been downloaded and executed before the next download can begin. In the meantime, the user is met with a blank screen as the files are being downloaded one at a time. This is most of browsers's behavior in today(This is the behavior of most major browsers today).


```
__ shows an
block __ from __
Further,
__ must wait until __
__ in the meantime. In the meantime,
__ met with __
__ today.
```

# Internet Explorer 8, Firefox 3.5, Safari 4, and Chrome 2 is permitted to download JavaScript files in parallel. This good news indicate that there is not necessary block other <script> Tags while a <script> is downloading external resources(This is good news because the <script> tags don't necessarily block other <script> tags from downloading external resources.). Unfortunately, JavaScripts downloading still block downloading of other resources， such as images. (And even) Though downloading a script doesn't block other scripts from downloading, The page must still wait for the JavaScript code to be downloaded and executed before continuing. So while the latest browsers have improved performance by allowing parallel downloads. This issue is not fully resolved yet(The problem hasn't been completely solved). Script blocking still remains a problem.

```
parallel download 并行下载
Script blocking 脚本阻塞
solve vs resolve 前者用于解决难题 后者用于解决矛盾，或者大难题，强调的是问题严重性
still 一般用作副词，修饰动词，所以前面没有 is
```

# Because scripts block downloading of all resource types on the page, it's recommended to place all <script> tags as close to the bottom of the <body> tag as possible so as not to affect the download of the entire page.


For example:

```
all vs all of 两者都能用于一般名词，而代词只能用后者
so as 所以
affect 影响, is usually a verb
effect 影响, is usually a noun
```

<html>
<head>
  <title>Script Example</title>
  <link rel="stylesheet" type="text/css" href="styles.css">
</head>
<body>
  <p>Hello world!</p>
  <-- Example of recommended script positioning -->
  <script type="text/javascript" src="file1.js"></script>
  <script type="text/javascript" src="file2.js"></script>
<script type="text/javascript" src="file3.js"></script>
</body>
</html>

# This code represents the recommended position for <script> tags in an HTML page. Even though the script downloads will block one another, but the rest of the page has already been downloaded and displayed to the user so that the speed of enter the page will not looks so slowly(so that the entire page isn't perceived as slow). This exactly is the first rule about JavaScript by 'Yahoo' performance optimization group(This is the Yahoo! Exceptional Performance team's first rule about JavaScript:): place(put) scripts at the bottom.


```
even though vs though
  1. even though 等于 even if “即使”，表达退一步设想，引导的句子不一定是事实
  2. though “虽然”，引导的句子是事实
  3. although较正式，语气强；though较常用。现代英语中两者可随意换用，放前中后都行

entire vs whole vs all
  1. 有时这两个词大致同义，只是位置不同：all 要放在冠词、指示代词、物主代词等之前，而 whole 应放在这些词之后
  2. all 指一个不剩，即“全部”；whole 指一点不缺，即“整个”
  3. entire 是 adj，whole 是n+adj+adv
  4. 在复数名词和不可数名词前一般用 all，在单数可数名词前一般用 whole
  5. 在物质名词前则绝对不用 whole

perceived 被感知
```

# Grouping Scripts

# Since each <script> tag blocks the page from rendering during initial download, it's helpful to limit the total number of <script> tags (contained) in the page. This rule is suitable for(This applies to) both inline scripts and outer scripts(as well as those in external files). Whenever the page rendering encounters a <script> tag(Every time a <script> tag is encounterd during the parsing of an HTML page), there is going to be a delay while the code is executed. minimizing these delays improves the overall performance of the page.

```
each vs every
  1. each 用于离散地引用一个组中的每一项，而当我们将一个组的所有成员都作为一个整体来处理时，我们使用 every
  2. each 在我们谈论规模较小的群体中使用，而当群体相对较大时，我们使用 every

as well as vs and
  2. 很多时候和 and 相近，但 as well as 包含了“又”的含义
  1. as well as ≈ not only...but also，但 as well as 侧重前者，not only...but also 侧重后者

is going to vs will
  1. 功能基本一样，表示将来时态
  2. 前者蕴含心中有数，提前就有打算
  3. 前者表示即将发生的动作，后者表示将来，不一定是近期

overall 整体的，仅用于名词前
```

# This problem is slightly different when dealing with external JavaScript files. Each HTTP request brings with it additional performance overhead, so downloading one 100KB file will be fast than downloading four 25KB files. In a word(To that end), it's helpful to limit the number of external script files that your page references. Typically, a large website or web application needs to request JavaScript files more than once(will have several requested JavaScript files). You can combine these files as a file, just need a <script> tag, performance losses can be reduced(You can minimize the performance impact by concatenating these files together into a single file and then calling that single file with a single <script> tag). The concatenation can happen offline using a build tool(we'll discuss in Chapter 9(discussed in Chapter 9)), or in real-time using a tool such as Yahoo! combo handler.

```
bring with 带来
To that end 为了那个目的
concatenate 连接，连结
```

# This URL loads 2.7.0 versions of the yahoo-min.js and event-min.js files. These files are two separated files on the server(These files exist separately on the server) but are combined when the server received this URL request(when this URL is requested). By this way, instead of using two <script> tags(one to load each file), a single <script> tag can be used to load both. 

# This code has a single <script> tag at the bottom of the page that loads multiple JavaScript files. This is the best practice for including external JavaScript on an HTML page.

```
to vs for
  1. to 强调对象关系，for 强调目的关系
  2. to 可表示动作对象，for 表示为了
  3. to 后面加动词更多，for 后面加名词更多
```

# Nonblocking Scripts

# JavaScript's tandency to block browser processes, both HTTP requests and UI updates, is the most notable performance issue facing developers. Keeping JavaScript files small and limiting the number of HTTP requests are only the first steps in creating a responsive Web application. The richer the functionality an application requires, the more JavaScript code is required, and so keeping source code small is not always a choice(an option). Limiting yourself to downloading a single large JavaScript file will only result in locking the browser out for a long period of time, despite it being just one HTTP request. To get around this situation, You need to gradually(incrementally) add more JavaScript to the page in a way doesn't bolck the browser.

```
tendency to 倾向于
notable 显著的
responsive 及时响应的
functionality 功能（性）
result in 导致
a long period of time 很长一段时间
get around this situation 摆脱这种困境
incrementally vs gradually
  递增的 vs 逐渐的
in a way that 以一种...的方式
```


<Chapter 2: Data Access>

# One of the classic computer science problems is determining where data should be stored for optimal reading and writing. Where data is stored is related to how quickly it can be retrieved during code execution. This problem in JavaScript is somewhat simplified because of the small number of options for data storage. Similar to other languages, though, where data is stored can greatly affect how quickly it can be accessed later. there are four basic places from which data can be accessed in JavaScript:

```
optimal reading and writing 最佳的读写（效率）
retrieved 重新取回
somewhat simplified 有点（被）简化了的
similar to 与...相似

while vs as
  1. while 后面接延续性行为，这个行为一般比主语长
  2. as 意为 一边...一边，与...同时，重在表示动作同时发生、伴随进行
```