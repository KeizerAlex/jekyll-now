---

title: Mapping certificates to Windows-users with IIS and SSL
date: 2004-10-18 21:33:34 +02:00
categories: Main
---
<P>Note to self: when using a CA that you have created yourself, make sure that the Machine Account has access to the CA-certificate.</P>
<P>Errors that you'll encounter are:</P>
<UL>
<LI>0x800B0109 
<LI>HTTP Error 403.16 - Forbidden: Client certificate is ill-formed or is not trusted by the Web server. 
<LI>The page requires a valid SSL client certificate Your client certificate is untrusted or invalid. A Secure Sockets Layer (SSL)client certificate is used for identifying you as a valid user of the resource.</LI></UL>
