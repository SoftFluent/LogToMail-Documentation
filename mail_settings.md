# Mail Settings

Mail settings can be configured under the `<mailSettings>` element.

This entire section, including the `<system.net>` for network settings and the `<mailSettings>` element specific to mail settings, follows .NET configuration standards.

Three options are available: *network*, *pickupDirectoryFromIis* and *specifiedPickupDirectory*. The three options are documented below. Should you need to go futher, go to msdn:
[http://msdn.microsoft.com/en-us/library/w355a94k.aspx](http://msdn.microsoft.com/en-us/library/w355a94k.aspx)


## network

With this setting, notification emails are sent through an SMTP server. The minimum needed information is the server host, but you might need to specify more details.

Simlpe Example:
```xml
<system.net>
  <mailSettings>
    <smtp from="logtomail@softfluent.com">
      <network host="MailServer"/>
    </smtp>
  </mailSettings>
</system.net>
```

Of course, you might have to specify more than just the server name. Full list of attributes is available below: (extract from [https://msdn.microsoft.com/en-us/library/ms164242.aspx](https://msdn.microsoft.com/en-us/library/ms164242.aspx)

| Attribute | Description |
| -- | -- |
| clientDomain | Specifies the client domain name to use in the initial SMTP protocol request to connect to the SMTP mail server. The default value is the localhost name of the local computer sending the request. |
| defaultCredentials | Specifies whether the default user credentials should be used to access the SMTP mail server for SMTP transactions. The default value is **false**. |
| enableSsl | Specifies whether SSL is used to access an SMTP mail server. The default value is **false**. |
| host | Specifies the hostname of the SMTP mail server to use for SMTP transactions. This attribute has no default value. |
| password | Specifies the password to use for authentication to the SMTP mail server. This attribute has no default value. |
| port | Specifies the port number to use to connect to the SMTP mail server. The default value is 25. |
| targetName | Specifies the Service Provider Name (SPN) to use for authentication when using extended protection for SMTP transactions. This attribute has no default value. |
| userName | Specifies the user name to use for authentication to the SMTP mail server. This attribute has no default value. |


## pickupDirectoryFromlis

If the monitored PC or server runs IIS, the easiest and most effective is to let IIS SMTP service handle the emails.

```xml
<system.net>
  <mailSettings>
    <smtp from="logtomail@softfluent.com"
        deliveryMethod="pickupDirectoryFromIis">
      <network host="localhost"/>
    </smtp>
  </mailSettings>
</system.net>
```


## specifiedPickupDirectory

With this option, the generated emails are dropped in the specified folder. This folder might be monitored by a mail server application… or not.

Specifically, if it is not monitored, this option is a great way to troubleshoot and test your emails, as you have the option to check it directly on the file system.

```xml
<system.net>
  <mailSettings>
    <smtp from="logtomail@softfluent.com"
        deliveryMethod="specifiedPickupDirectory">
      <specifiedPickupDirectory pickupDirectoryLocation="c:\temp"/>
    </smtp>
  </mailSettings>
</system.net>
```