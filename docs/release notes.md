# Release Notes SAP Business Objects 21.0.1

## General

The release removes log4j and replaces it with slj4j and logback.

## Migration Considerations

This release includes the new format installer where the files are extracted from the zip file into the desired directory. 
It contains an embedded java version for connector so there is no reliance on installed Java versions.
The connector also implements new encryption capabilities and the documentation explains how to use the new Encrypt.exe mechanism.
The configuration file name has also been changed from Agent.config to Connector.config

### New Features

### Fixes

**CONNUTIL-543**    
                    CVE-2021-44228 adjustment removing log4j as the logging component.
**CONNUTIL-558**    
                    Added libraries to implement missing jaxb classes moved during Java 11 implementation  
			