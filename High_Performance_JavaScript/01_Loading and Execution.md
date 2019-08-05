# JavaScript performance in the browser can be seen as the most important usability issue facing developers. The problem is complex because of the blocking nature of JavaScript, which is to say that other things cannot be handle by browser while JavaScript code is running(being executed). Actually(In fact), most browsers uses a single process for both UI updates and JavaScript execution, so only one can happen at any given moment in time. The longer JavaScript takes to execute, the longer it takes before the browser is free to response to user input.

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

# When the browser encounters a <script> tag, just as HTML page above, there is no way of knowing whether the JavaScript will insert content into the <p> tag. Therefore, the browser stops processing the page as it comes in, executes the JavaScript code, then continues parsing and rendering the page. The same takes place for JavaScript loaded using the 'src' attribute loading JavaScript. The browser have to first download the external file's code(The browser must first download the code from the external file), which takes some time, and then parse and execute the code. During this process, page rendering and user interaction are completely blocked.

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

# Internet Explorer 8, Firefox 3.5, Safari 4, and Chrome 2 is permitted to download JavaScript files in parallel. This good news indicate that there is not necessary block other <script> Tags while a <script> is downloading external resources(This is good news because the <script> tags don't necessarily block other <script> tags from downloading external resources.). Unfortunately, JavaScripts downloading still block downloading of other resources， such as images. (And even) Though downloading a script doesn't block other scripts from downloading, The page must still wait for the JavaScript code to be downloaded and executed before continuing. So while the latest browsers have improved performance by allowing parallel downloads. This issue is not fully resolved yet(The problem hasn't been completely solved.). Script blocking still remains a problem.

```
parallel download 并行下载
Script blocking 脚本阻塞
solve VS resolve 前者用于解决难题 后者用于解决矛盾，或者大难题，强调的是问题严重性
still 一般用作副词，修饰动词，所以前面没有 is
```

# Because scripts block downloading of all resource types on the page, it's recommended to place all <script> tags as close to the bottom of the <body> tag as possible so as not to affect the download of the entire page.


For example:

```
all VS all of 前者用于一般名词，后者用于代词
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