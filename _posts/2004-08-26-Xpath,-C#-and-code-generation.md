---
title: Xpath, C# and code-generation
date: 2004-08-26 21:59:54 +02:00
categories: Tools
---
<P>I tend to use code-generation to avoid "dumb" work where possible. Xslt is a valueable tool to create the templates for the code that is to be generated. The available functions in Xpath have been limited in number; with the advent of C# the following becomes possible:</P>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE><?xml version="1.0" encoding="UTF-8" ?> <BR><stylesheet version="1.0" xmlns="<A href="http://www.w3.org/1999/XSL/Transform">http://www.w3.org/1999/XSL/Transform</A>"<BR> xmlns:msxsl="urn:schemas-microsoft-com:xslt" xmlns:user="<A href="http://pareto.nl/PAS">http://pareto.nl/PAS</A>"><BR>  <msxsl:script language="CSharp" implements-prefix="user"><BR>     <![CDATA[ </PRE>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px">
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE> public string CamelCase(string value)<BR> {<BR>  return value[0].ToString().ToLower() + value.Substring(1);<BR> }<BR> <BR> public string UpperCase(string value)<BR> {<BR>  return value.ToUpper();<BR>  <BR> }</PRE></BLOCKQUOTE></BLOCKQUOTE></BLOCKQUOTE>
<P>Although it'll probably be some time before we can use this within an application as client-side script, it sure does make the Xsl/Xpath-combination a more powerful solution for generating code.</P>
