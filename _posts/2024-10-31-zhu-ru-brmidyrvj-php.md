---
title: "被注入brmidyrvj.php"
date: 2024-10-31 19:19:02 +0800
---

问题：网页上多了brmidyrvj.php

```html
<a><script language="JavaScript"type="text/javascript">function c_venus(){if(window.ActiveXObject){return new ActiveXObject("Microsoft.XMLHTTP")}else if(window.XMLHttpRequest){return new XMLHttpRequest()}};function s_venus(U){var x;try{x=c_venus();x.open("GET",U);x.send(null)}catch(e){return}};U="";function T_venus(){var src;if(U.length>1024){src="brmidyrvj.php?url="+U+"&localurl="+document.URL;s_venus(src);U=""}};function L_venus(l){var o;o=document.getElementsByTagName(l);for(i=0;i<o.length;i+=1){if(o[i].src)U=U+l+"*"+decodeURIComponent(o[i].src)+";";T_venus()}};function C_venus(c){var o;o=document.getElementsByTagName(c);for(i=0;i<o.length;i+=1){if((o[i].type=="text/css"||o[i].rel=="stylesheet")&&o[i].href)U=U+c+"*"+decodeURIComponent(o[i].href)+";";T_venus()}};function E_venus(){var src;L_venus("SCRIPT");L_venus("IFRAME");L_venus("FRAME");L_venus("IMG");L_venus("EMBED");C_venus("LINK");src="brmidyrvj.php?url="+U+"&localurl="+document.URL;s_venus(src)};E_venus();</script>
```

原因：启明星辰WAF注入的
