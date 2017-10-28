---

title: Reinstalling Biztalk 2004
date: 2005-03-29 21:29:36 +02:00
categories: Biztalk
---
<P dir=ltr style="MARGIN-RIGHT: 0px"><post><BR><note_to_self><BR>When adding the MSMQT-adapter, a message is shown that it's not possible to uninstall the adapter. This doesn't seem to be very important ... what you should remember is that this will torch the 'regular' MSMQ. Save a couple of hours and think this over.<BR></note_to_self></P>
<P dir=ltr style="MARGIN-RIGHT: 0px"><note_to_self><BR>Enterprise SSO - When this happens:<BR><FONT size=1>SSO AUDIT<BR>Function: GetConfigInfo<BR>Tracking ID: fb5fe349-6437-4773-ac42-5582a6114aea<BR>Client Computer: pareto53 (BTSNTSvc.exe:3616)<BR>Client User: PARETO53\BtsService<BR>Application Name: {B57ABA8F-AB28-4BE8-A759-90516B8EFFB2}<BR>Error Code: 0x80070005, Access is denied.</P>
<P dir=ltr style="MARGIN-RIGHT: 0px"></FONT>Do this:<BR>HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\<BR>Create the following Registry Key [RPC]<BR>Under that create a new DWORD value called [EnableAuthEpResolution]<BR>Set the value of this new value to [1]<BR><BR></note_to_self><BR></post></P>
