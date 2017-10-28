---

title: Sybase feature #221
date: 2006-02-06 15:00:22 +01:00
categories: Main
---
<P>The project I'm working on at the moment requires the use of a Sybase database. To ensure we started with the correct version, the client made a dump of the current database. After installing the Sybase software - which went fairly smooth - we ran into the following error:</P>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE>"The database you are attempting to LOAD was DUMPed under a different sort order ID (44) or<BR> character set ID (2) than the ones running on this server (SortOrd = 41, CharSet = 2).<BR>If the sort orders differ, at least one of them is non-binary."</PRE></BLOCKQUOTE>
<P>For some reason Sybase removed the characterset with id #44 from ASE in the 12.5 release.<BR>The following steps were needed to resolve the issue:<BR>- Make a copy of C:\sybase\charsets\cp850\nocase.srt and name it nocase44.srt<BR>- Edit the contents: change the id to 0x2C and the name to nocase_44<BR>- CD to c:\sybase\ase-12_5\bin<BR>- run charset nocase44.srt cp850<BR>- Change the default sortorder id to 44 (sp_configure)<BR>- Restart the server</P>
<P>Now you should be able to load the dump.</P>
