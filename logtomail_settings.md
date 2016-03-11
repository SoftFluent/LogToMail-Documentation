# LogToMail Settings

Settings specific to LogToMail are located under the `<LogToMail.service>` element. There is only one element to specify, *Watcher*, with one collection, *Rules*.

Declare a `<rule>` element under the `<rules>` element to specify rules in LogToMail. Each rule defines who the alert emails are sent to, and which Windows events will trigger the emails.

The rule element also provides the following set of attributes to specify rule-level options:

| Attribute | Required | Default | Description |
| -- | -- | -- | -- |
| **name** | Yes | Empty | Name of the rule. |
| **sendTo** | Yes | Empty | The  mail  address  to  send  the  notification email to. |
| **sendFrom** | No | Empty | The mail address to use as the "from" field. |
| **sendFromDisplayName** | No | Empty | A string to use as the sender display name. |
| **enabled** | No | True | A  boolean  indicating  whether  the  rule  is enabled or not. |
| **setPriority** | No | True | A boolean indicating whether to set priority on mail message (high for errors and security failures, normal for warnings, low for successes and information). |
| **mailSubject** | No | \#Type\# \#SourceName\# \#Message\# | The mail subject to be used. |
| **mailsubjectMaxLenght** | no | 128 |The mail subject maximum length. |
| **mailBody** | No | A html table containing all event values. | The mail body to use.  |
| **dataFileName** | No | data.hex | The data filename to use to send event data if any. |
| **scriptLanguage** | No | javascript | The script language to evaluate the rule.|

**Example**

The example below will send you an email every time an event with the type "1" will be triggered on the monitored Windows environment. "1" corresponds to Errors. With this setting, you will get only errors, but all errors, from all applications and from Windows itself.

```xml
<rule name="default"
    sendFrom="logtomail@softfluent.com"
    sendTo="LogToMail@example.com">
  Event.EventType == 1
</rule>
```
To go further and specify which errors you want to catch, define your rule(s) in JavaScript between the opening and closing tags of the rule element.

You have probably noticed that the filter on the type of events is based on a object "Event". You actually have full access to this object when writing your rule. Please find below the available properties.

| Property | Type | Description |
| -- | -- | -- |
| **EventCode** | Short | The event code.|
| **EventIdentifier** | Int | The event identifier.|
| **EventType** | Byte | The event type. For all possible values, see [http://msdn.microsoft.com/enus/library/system.diagnostics.eventlogentrytype.aspx](http://msdn.microsoft.com/enus/library/system.diagnostics.eventlogentrytype.aspx)|
| **Category** | Short | The application-specific category number for this event.|
| **CategoryString** | String | Gets the text associated with the Category property for this event.|
| **ComputerName** | String | The computer name.|
| **Data** | Byte[] | Gets the binary data associated with the event.|
| **InsertingStrings** | String[] | Gets the replacement strings associated with this event.|
| **Message** | String | Gets the message associated with this event.|
| **SourceName** | String | Gets the name of the application that generated this event.|
| **TimeGenerated** | DateTime | Gets the local time at which the event was generated.|
| **TimeWritten** | DateTime | Gets the local time at which this event was written to the log.|
| **User** | String | Gets the user name related to this event.|

More advanced example:

The following rule will send all error events except the ones with event codes 1058 and 1126 to users user1, user2 and user3.

```xml
<rule name="SendToUsers" sendFrom=LogToMail@softfluent.com
      sendTo="user1@example.com,user2@example.com,user3@example.com"
      sendFromDisplayName="LogFluent '#::Environment.MachineName#'">
   Event.EventType == 1)&amp;&amp; (Event.EventCode != 1058) &amp;&amp;
    (Event.EventCode != 1126)
</rule>
```

*__Notes__*:
* *As the configuration file is in XML and that the ampersand is a reserved character in XML, you have to use its escaped form (i.e. "&amp;" instead of "&")*.
* *In this example, by adding "'#::Environment.MachineName#'" in the sendFromDisplayName field, all senders names will include the name of the machine where the event happened. This makes it easier to identify the issue without even opening the email.*