# Operation

The Enterprise Manager includes job subtype definitions for the SAP Business Objects Scheduler. The job subtype can be accessed by selecting 
the SAP Business Objects job subtype from the drop down list when the Windows Job Type has been selected. 

It should be remembered that the SAP Business Objects Connector does not create job definitions in the SAP Business Objects database, 
but rather only uses existing job.

## SAP Business Objects Job definitions
The SAP Business Objects Connector currently contains a single **START** job that can be selected.
 
When defining a SAP Business Objects job, select a Job Type of Windows and then a Job Sub-Type of SAP Business Objects. 

The SAP Business Objects Definition screen will then appear.

The job definition consists of two separate areas, with a general area required by all jobs and specific information required depending on the selected job type. 

General Definition contains the following fields

Field | Description
--------- | -----------
**Connector Path**     | Required field that contains the installed location of the Connector. This should not be changed and the location should be defined in the **SAPBOPath** property. If more than one SAP Business Objects Connectors is installed on the same system, then a new global property should be defined and the entry in this field updated.
**Function**           | Required field that contains the function to execute. Currently only a **START** function is available. Depending which function is selected, additional information can be entered in the appropriate TAB definitions.
**User Name**          | Required field that contains the name of a SAP Business Objects user that has the required privileges to execute the job. 
**User Password**      | Required field that contains the password of the defined user. Encrypted global properties should be used for the password. The value is then decrypted by the Windows Agent.
**CMS Authentication** | Required field that contains authentication mode associated with the user defined in the User Name field. Select a value from the drop-down list that matches your installation (**Enterprise**, **LDAP**, **WinAD** or **SAPR3**).

The **START** job type can be used to schedule a report within the SAP Business Objects environment. When the START job type is selected, the Start and Failure Criteria TABs are available for defining additional information with the Start TAB displayed.

Field | Description
--------- | -----------
**Report Type**        | Required field that contains the type of Business Objects report to schedule. Currently **Crystal Reports**, **Publications** and **Web Intelligence** reports are supported.
**Report ID**          | Required field that contains ID of the Business Objects report to schedule. This information can be extracted from the Business Objects system by examining the properties of the report on the Business Objects system.

The Report Attributes, Report Prompts and Report Destinations fields are currently only supported for Web Intelligence Reports.

### Report Attributes
Report Attributes TAB field definitions are used to define attributes that will be passed to the report. 
Attributes are entered in name/value pairs using the attribute name and the value. 

To enter an attribute, enter the attribute name in the **Attribute** field and the attribute value in the **Value** field and then select the **Add** button. 
To modify an attribute, select the attribute in the Table and the entry will be displayed in the **Attribute** and **Value** fields. Modify the value and select the **Update** button. 
To remove an attribute, select the attribute in the Table and the entry will be displayed in the **Attribute** and **Value** fields and then select the **Remove** button.

Two special attributes **SCHEDULE-TITLE** and **SCHEDULE-FORMAT** can be used to define the title of the report and the format of the report.
- **SCHEDULE-TITLE**     Free format title. If omitted a title consisting of the report ID and a date timestamp will be used (i.e. 7793_201512011535). 
- **SCHEDULE-FORMAT**    Output format (webi, pdf, xls or csv). If omitted the default value defined in the Connector.config file will be used. 

### Report Prompts

Report Prompts TAB field definitions can be used to submit a response to a prompt when a report is scheduled. The value consists of the message associated with the prompt and the value to be submitted. It is possible to define multiple prompts for a schedule. These prompt types can be character, integer or date / time values. The values are passed as strings in the xml submitted to the web service and the web service then converts this to the appropriate format.

To enter a prompt, start typing in the **Prompt** field enter the message and value pairs and then select the **Add** button. 
To modify a prompt, select the prompt in the **Prompt** List and the entry will be displayed in the **Prompt** field. Modify the value and select the **Update** button. 
To remove a prompt, select the prompt in the **Prompt** List and the entry will be displayed in the **Prompt** field and then select the **Remove** button.

It is possible to enter more than one value for a prompt by separating the values with a semi colon. In the example a second Category value can be added to the ‘Enter values for Category:’ prompt as follows:

Prompt ‘Enter values for Category:’
Value  ‘Evening Wear;Jackets’

Examples:

```
Enter values for Lines:                     Dresses
Enter values for Category:                  Evening Wear;Jackets

```

### Report Destinations

Report Destinations TAB field definitions are used to define destinations for the report. The destinations will override the default values associated with the report. Destinations are entered in type/value pairs using a destination type identifier and the value. Report Destinations supports **DiskUnmanaged**, **FTP**, **Managed** (Business Objects user inbox) and **SMTP** definitions. 

#### DiskUnmanaged
Report Destinations DiskUnmanaged TAB field definitions are used to define disk directories for the report.

Field | Description
--------- | -----------
**Directory**           | Defines the directory where the report will be placed (i.e. c:\temp). 

#### Ftp
Report Destinations Ftp TAB field definitions are used to define FTP definitions. The FTP definitions are used in conjunction with a defined FTP server in the Connectopr.config file. 

Field | Description
--------- | -----------
**Indicator**           | Defines a FTP destination. The value FTP1 is matched with the value of a FTP Server definition in the Connector.config file (i.e. [FTP1]). The values associated with the FTP1 definition in the Connector.config file are used to define the FTP Server.   
**Directory**           | The definition defines the directory where the generated file be placed on the ftp server.   

#### Managed(Inbox)
Report Destinations Managed(Inbox) TAB field definitions are used to define SAP Business Objects users that will receive a copy of the report in their mailbox. 

Field | Description
--------- | -----------
**Selected Users**      | To insert a user into the **Selected Users** List, enter the **user ID** number in the **Users** field and then select the **Add button**. Currently the web services interface does not provide the capability to use a name instead of the user ID. To modify a user in the **Selected Users** List, select the **user** in the list and the user will appear in the **Users** field. When modification is complete, select the **Update** button to save the new value. 
To remove a user from the **Selected Users** List, select the **user** in the list and the user will appear in the **Users** field then select the **Remove** button to remove the name from the list.

#### Smtp
Report Destinations Smtp TAB field definitions are used to define SMTP definitions. The SMTP definitions are used in conjunction with a defined SMTP server in the Connector.config file. 

Field | Description
--------- | -----------
**Indicator**           | Defines a SMTP destination. The value SMTP1 is matched with the value of a SMTP Server definition in the Connector.config file (i.e. [SMTP1]). The values associated with the SMTP1 definition in the Connector.config file are used to define the SMTP Server.  
**Subject**             | Defines the information to be placed in the subject field of the email message. 
**Message**             | Defines a message that will be added to the email message body. If no message submitted, the default value ‘Created by OpCon from SMA Solutions’ will be used.  
**Email Addresses**     | To insert a user into the **Email Address List**, enter the email address in the **Email Address** field and then select the **Add button**. To modify an email address in the **Email Address List** list, select the **Email Address** in the list and the email address will appear in the **Email Address** field. When modification is complete, select the **Update** button to save the new value. To remove an email address from the **Email Address List** list, select the **Email Address** in the list and the email address will appear in the **Email Address** field then select the **Remove** button to remove the email address from the list.

## Job Finished processing 

The START job type require a Failure Criteria definition. A SAP Business Objects Scheduled task has the following possible return codes:

200	FINISHED_OK, the job has been successfully initiated.
201	FINISHED_OK, the job has been successfully initiated.
1	ERRORED, an exception occurred during job initiation.

This means that to check for a successful completion, the Failure Criteria should be set to NE (Not Equal) to 200 as this is the completed successfully (OK) code returned when using Restful web services. It should be noted that a returned code from SAP Business Objects of warning, will be logged and mapped to an ERRORED condition.

## Logging

The default logging implemented by the connector consists of a maximum cycle of five log files. The log files contain information about the SAP BUsiness Objects Connector and any jobs run by the SAP BUsiness Objects Connector. The log files (sapbo.log - sapbo.log.5) are located in the ***installation_dir***\log directory. Information is appended into the log files and any error messages, return codes can be viewed in these log files.

