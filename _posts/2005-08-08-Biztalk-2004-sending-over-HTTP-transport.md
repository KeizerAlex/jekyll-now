---
layout: post
title: Biztalk 2004: sending over HTTP-transport
date: 2005-08-08 13:59:31 +02:00
categories: Biztalk
---
<P>Very early this morning I fixed an issue we were having with sending messages over a HTTP-transport. As the final step in the orchestration the result was posted back to an existing application. Although the entire chain worked, larger messages would be sent by Biztalk but would never be picked up by the application.</P>
<P>Initially we assumed that this was the result of IIS limiting the maximum number of bytes in a single request. After changing a lot of different settings, we finally found the reason:</P>
<UL>
<LI>When the message-size is over 48Kb Biztalk uses chunked encoding to post the messages</LI>
<LI>The receiving application was written in 'classic ASP'; ASP does not deal with chunked encoding very well.</LI></UL>
<P>After installing Biztalk SP1 it is possible to disable chunked encoding for the HTTP-transport. Look at this <A href="http://support.microsoft.com/default.aspx?scid=kb;en-us;839663">article</A> for more details on how to do this.</P>
