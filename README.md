# SSRS : BI Tools for Android & iOS

* To modify the Web.config file for Report Server:
Open the Web.config file in a text editor. By default, the file is located in the <install>\ReportServer directory.
Locate the <identity> element and set the Impersonate attribute to false. * <identity impersonate="false" /> *
Locate the <authentication> element and change the Mode attribute to Forms.
Add the following <forms> element as a child of the <authentication> element and set the loginUrl, name, timeout, and path attributes as follows:
```
<authentication mode="Forms">
	<forms loginUrl="logon.aspx" name="sqlAuthCookie" timeout="60" path="/"></forms>
</authentication>
```
* To add a code group for your custom security extension that grants FullTrust permission for your extension. You do this by adding the code group to the RSSrvPolicy.config file.
To modify the RSSrvPolicy.config file
Open the RSSrvPolicy.config file located in the <install>\ReportServer directory.
Add the following <CodeGroup> element after the existing code group in the security policy file that has a URL membership of $CodeGen as indicated below and then add an entry as follows to RSSrvPolicy.config. Make sure to change the below path according to your ReportServer installation directory:
```
<CodeGroup
	class="UnionCodeGroup"
	version="1"
	Name="SecurityExtensionCodeGroup"
	Description="Code group for the sample security extension"
	PermissionSetName="FullTrust">
	<IMembershipCondition 
	class="UrlMembershipCondition"
	version="1"
	Url="C:\Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.CustomSecurity.dll"/>
</CodeGroup>
```
* To modify the RSReportServer.config file
Open the RSReportServer.config file with Visual Studio or a simple text editor such as Notepad. RSReportServer.config is located in the <install>\ReportServer directory.
Locate the <AuthenticationTypes> element and modify the settings as follows:
```
<Authentication>
	<AuthenticationTypes> 
		<Custom/>
	</AuthenticationTypes>
	<RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>
	<RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>
	<EnableAuthPersistence>true</EnableAuthPersistence>
</Authentication>
```
Locate the <Security> and <Authentication> elements, within the <Extensions> element, and modify the settings as follows:
```
<Security>
	<Extension Name="Forms" Type="Microsoft.Samples.ReportingServices.CustomSecurity.Authorization, Microsoft.Samples.ReportingServices.CustomSecurity" >
		<Configuration>
			<AdminConfiguration>
				<UserName>username</UserName>
			</AdminConfiguration>
		</Configuration>
	</Extension>
</Security>


<Authentication>
	<Extension Name="Forms" Type="Microsoft.Samples.ReportingServices.CustomSecurity.AuthenticationExtension, Microsoft.Samples.ReportingServices.CustomSecurity" />
</Authentication>
```
Locate the <UI> element and update it as follows:
```
<UI>
	<CustomAuthenticationUI>
		<loginUrl>/Pages/UILogon.aspx</loginUrl>
		<UseSSL>True</UseSSL>
	</CustomAuthenticationUI>
	<ReportServerUrl>http://<server>/ReportServer</ReportServerUrl>
	<PageCountMode>Estimate</PageCountMode>
</UI>
```
* To deploy the sample
  1. Copy Microsoft.Samples.ReportingServices.CustomSecurity.dll and Microsoft.Samples.ReportingServices.CustomSecurity.pdb to the <install>\ReportServer\bin directory.
  2. Copy Microsoft.Samples.ReportingServices.CustomSecurity.dll and Microsoft.Samples.ReportingServices.CustomSecurity.pdb to the <install>\ReportManager\bin directory.
Copy the Logon.aspx page to the <install>\ReportServer directory.
  3. Copy the UILogon.aspx page to the <install>\ReportManager\Pages directory.