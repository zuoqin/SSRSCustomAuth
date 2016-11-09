# SSRS : BI Tools for Android & iOS

1. To modify the Web.config file for Report Server:

Open the Web.config file in a text editor. By default, the file is located in the <install>\ReportServer directory.
Locate the <identity> element and set the Impersonate attribute to false. * <identity impersonate="false" /> *
Locate the <authentication> element and change the Mode attribute to Forms.
Add the following <forms> element as a child of the <authentication> element and set the loginUrl, name, timeout, and path attributes as follows:
```
<authentication mode="Forms">
	<forms loginUrl="logon.aspx" name="sqlAuthCookie" timeout="60" path="/"></forms>
</authentication>
```
Add the following <authorization> element directly after the <authentication> element.
```
<authorization> 
	<deny users="?" />
</authorization> 
```
