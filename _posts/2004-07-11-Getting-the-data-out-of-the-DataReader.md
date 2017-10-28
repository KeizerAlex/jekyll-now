---
title: Getting the data out of the DataReader
date: 2004-07-11 16:11:21 +02:00
categories: Coding
---
<P><SPAN>Last Friday I had a short discussion with a colleague on what the 'best' way was to get data out of the DataReader?</SPAN> 
<P><SPAN>There are a number of options: 
<P></P></SPAN>
<P></P>
<P>Use the name of the column:</P>
<P></P>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE>SqlDataReader dr = cmd.ExecuteReader();</PRE></BLOCKQUOTE>
<P></P>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE>while{dr.Read())<BR>{<BR><SPAN>  ...<BR></SPAN>  string columnvalue <SPAN> </SPAN>= dr["au_lname"].ToString();<BR>  ...<BR>}</PRE></BLOCKQUOTE>
<P></P>
<P>The benefit here is the ease in writing the code and the readability.</P>
<P></P>
<P> </P>
<P>The second way of approaching the DataReader is using an index:</P>
<P>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE>while{dr.Read())<BR>{<BR><SPAN>  ...<BR></SPAN>  string columnvalue <SPAN> </SPAN>= dr[1].ToString();<BR>  ...<BR>}</PRE></BLOCKQUOTE>
<P></P>
<P>This code is a bit harder to read, but is should be faster because there's no need to do a lookup on the column-name.</P>
<P>Once an extra column is added to the query, we'll need to go over all of the indices to confirm we didn't break anything.</P>
<P></P>
<P>To verify that this code is actually faster, I created a small test-program that retrieves data from the pubs-database. The table shows the average time to get records from the authors-table into a variable.</P>
<P></P>
<TABLE cellSpacing=0 cellPadding=0 width=207 border=0>
<TBODY>
<TR>
<TD vAlign=bottom noWrap width=77>
<P><SPAN><FONT size=2>count<BR>---------- </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65>
<P><SPAN><FONT size=2>string<BR>----- </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65>
<P><SPAN><FONT size=2>index <BR>-----</FONT></SPAN></P></TD></TR>
<TR>
<TD vAlign=bottom noWrap width=77 x:num>
<P align=left><SPAN><FONT size=2>1 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="1.6765538636893802E-2">
<P align=right><SPAN><FONT size=2>0.016766 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="1.37352652362242E-2">
<P align=right><SPAN><FONT size=2> 0.013735 </FONT></SPAN></P></TD></TR>
<TR>
<TD vAlign=bottom noWrap width=77 x:num>
<P align=left><SPAN><FONT size=2>10 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="2.4425450720692199E-3">
<P align=right><SPAN><FONT size=2>0.002443 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="1.7078148200399799E-3">
<P align=right><SPAN><FONT size=2> 0.001708 </FONT></SPAN></P></TD></TR>
<TR>
<TD vAlign=bottom noWrap width=77 x:num>
<P align=left><SPAN><FONT size=2>100 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="1.0640681986118299E-3">
<P align=right><SPAN><FONT size=2>0.001064 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="4.8499739492030298E-4">
<P align=right><SPAN><FONT size=2>0.000485 </FONT></SPAN></P></TD></TR>
<TR>
<TD vAlign=bottom noWrap width=77 x:num>
<P align=left><SPAN><FONT size=2>1000 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="6.9109761156794895E-4">
<P align=right><SPAN><FONT size=2>0.000691 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="3.8279725495838301E-4">
<P align=right><SPAN><FONT size=2>0.000383 </FONT></SPAN></P></TD></TR>
<TR>
<TD vAlign=bottom noWrap width=77 x:num>
<P align=left><SPAN><FONT size=2>10000 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="6.9728644283002404E-4">
<P align=right><SPAN><FONT size=2>0.000697 </FONT></SPAN></P></TD>
<TD vAlign=bottom noWrap width=65 x:num="3.9660727829933799E-4">
<P align=right><SPAN><FONT size=2>0.000397 </FONT></SPAN></P></TD></TR></TBODY></TABLE>
<P>As you can see, it actually turns out to be faster to use an index.</P>
<P></P>
<P>To get the best of both worlds, you can use a combination of both approaches:</P>
<P></P>
<BLOCKQUOTE dir=ltr style="MARGIN-RIGHT: 0px"><PRE>const int FIELD_AUID = 0;<BR>const int FIELD_AU_LNAME = 1;<BR>const int FIELD_AU_FNAME = 2;</PRE><PRE>...</PRE><PRE>while{dr.Read())<BR>{<BR><SPAN>  ...<BR></SPAN>  string columnvalue <SPAN> </SPAN>= dr[FIELD_AU_LNAME].ToString();<BR>  ...<BR>}</PRE></BLOCKQUOTE>
<P></P>
<P>This way changes to the query only require editing of the list of constants.</P>
<P></P>
<P>The performance gain for test-program seems to comparable to changing from the OleDbProvider to SqlClient. So making a small change to the code, has it running about twice as fast.</P>
