# Installation

The SAP Business Objects Connector installation consists of multiple steps that are required to complete the installation successfully. This consists of installing a 
Windows Agent, the SAP Business Objects Connector, configuring the SAP Business Objects connector and installing the SAP Business Objects Windows job subtype. 

It should be noted that the SAP Business Objects connector requires a Windows Agent as it executes as a Windows batch job. 
It can be installed on a central server or an agent can be installed on the SAP Business Objects server.

## Supported Software Levels
The following software levels are required to implement the SAP Business Objects Connector.

- OpCon Release 19.0 or higher.
- Embedded Java OpenJDK 11 (part of installation).
- SAP Business Objects 4.2.

## Installation
The installation process consists of the following steps:

- OpCon Windows Agent Installation.
- SAP BUsiness Objects Connector Installation.
- Adding SAP BUsiness Objects Connector job subtype to Enterprise Manager.
- SAP Business Objects Connector Configuration.
 
### OpCon Windows Agent Installation
The SAP Business Objects Connector requires a SMA OpCon Windows Agent. The Agent can be installed either on the SAM Server or on the same system as the SAP Central Management Console server.

### SAP Business Objects Connector Installation

Copy the supplied install file SAPBOConnector-win.zip and extract it into the installation directory.

After the extraction, the root installation directory contains the connector executable (boxi.exe), the encryption software (Encrypt.exe), the Connector.config file and two directories, 
java and emplugins. The java directory contains the java software required to execute the connector (OpenJDK 11) and the emplugins directory contains the job sub-type plugin for Enterprise Manager.

### Create SAPBOPath Global Property
Create a global property **SAPBOPath** that contains the full path of the installation directory.

### Job Subtype Installation
Copy the Enterprise Manager plug-in from the ***installation_dir***\\emplugins directory to the dropins directory of the Enterprise Manager installation. 

If the dropins directory does not exist, create the dropins directory off the root directory. 

Restart Enterprise Manager and a new Windows job subtype called SAP Business Objects will be visible.

If not restart Enterprise Manager using 'Run as Administrator'. After this Enterprise Manager can be used normally.

## SAP Business Objects Connector Configuration
The configuration of the SAP Business Objects Connector requires setting the required values in the Connector.config file. The Connector.config file contains information for the SAP 
Business Objects Connector that defines the address of the Business Objects Server that the connector uses to issue requests to Business Objects. 

It also includes definitions for FTP and SMTP servers. The header name of the FTP and SMTP definitions are used to extract the correct connection definitions. It is possible to define multiple connections by changing the header value (i.e. FTP1 defines the connection for server1 and FTP2 defines the connection for server2.

Any passwords entered into the Connector.config must be encrypted using the Encrypt.exe utility provided with the connector. When executing the utility, a single argument -v is used to provide the value that must be encrypted


#### Encrypt Utility
The Encrypt utility uses standard 64 bit encryption.

Supports a -v argument and displays the encrypted value

On Windows, example on how to encrypt the value "abcdefg":

```
Encrypt.exe -v abcdefg

```

#### Connector.config configuration
Configure the Connector.config file in the installation directory setting the required information.
The Connector.config contains the following values

Property Name                              | Value
------------------------------------------ | -----------
**[CONNECTOR]**                            | header
**CONNECTOR_NAME**                         | The name of the connector. This value should not be changed.
**DEBUG**                                  | If the Connector supports a debug mode, it can be used to set the connector into DEBUG mode. Value either ON or OFF (default OFF).
**[BUSINESS OBJECTS]**                     | header 
**BUSINESS_OBJECT_SERVER_ADDRESS**         | This defines the address of the SAPBO server. This includes the port number which is the listening port defined during SAP Business Objects installation (default 6405).
**BUSINESS_OBJECTS_DEFAULT_REPORT_FORMAT** | This is the default report format if the attribute SCHEDULE-FORMAT is not present. Values consist of webi, pdf, xls or csv.
**[DISK]**                                 | Header – used to define a DISK connection and contains a valid user and password that is allowed to write files on the target disk.
**DISK_USER**                              | This defines a valid user code that has the required privileges to write onto the destination disk.
**DISK_USER_PASSWORD**                     | This defines the password of the user. It is encrypted using the Encrpyt.exe utility.
**[FTP]**                                  | Header – used to define a connection to a FTP Server. A FTP destination definition includes this name as the first parameter of the value definition so the correct FTP server definitions can be used (i.e. FTP=FTP1,..). It is possible to add multiple definitions by changing the header value.
**FTP_SERVER_NAME**                        | This defines the address of the FTP server.
**FTP_PORT_NUMBER**                        | This defines the port used by the FTP server.
**FTP_USER**                               | This defines a valid user code that has the required privileges to login to the FTP server.
**FTP_USER_PASSWORD**                      | This defines the password of the user. It is encrypted using the Encrpyt.exe utility.
**[SMTP]**                                 | Header – used to define a connection to a SMTP Server. A SMTP destination definition includes this name as the first parameter of the value definition so the correct SMTP server definitions can be used (i.e. SMTP=SMTP1,..). It is possible to add multiple definitions by changing the header value.
**SMTP_DOMAIN_NAME**                       | This defines the domain name associated with the SMTP server.
**SMTP_SERVER_NAME**                       | This defines the address of the SMTP server.
**SMTP_PORT_NUMBER**                       | This defines the port used by the SMTP server.
**SMTP_USER**                              | This defines a valid user code that has the required privileges to login to the SMTP server.
**SMTP_USER_PASSWORD**                     | This defines the password of the user. It is encrypted using the Encrpyt.exe utility.

Example configuration file. 

```
[CONNECTOR]
CONNECTOR_NAME=SAP Business Objects Connector
DEBUG=ON

[BUSINESS OBJECTS]
BUSINESS_OBJECTS_SERVER_ADDRESS= VM-TEST-BOXI:6405
BUSINESS_OBJECTS_DEFAULT_REPORT_FORMAT=pdf

[DISK]
DISK_USER=test
DISK_USER_PASSWORD=6233426a6232353463484d3d

[FTP]
FTP_SERVER_NAME=ftpserver1
FTP_PORT_NUMBER=21
FTP_USER=test
FTP_USER_PASSWORD=6233426a6232353463484d3d

[SMTP]
SMTP_DOMAIN_NAME=domain
SMTP_SERVER_NAME=smtpserver1
SMTP_PORT_NUMBER=25
SMTP_USER=test
SMTP_USER_PASSWORD=6233426a6232353463484d3d

```
