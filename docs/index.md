---
slug: '/'
sidebar_label: 'SAPBO Connector'
---

# SAPBO Connector
SAP Business Objects is a suite of front-end applications that allows business users to view, sort and analyzes business intelligence data. 
The suite contains the following applications.

- **Crystal Reports**       Allows users to design and generate reports.
- **Dashboards**            Allows users to create interactive dashboards that contains charts and graphs for visualizing data.
- **Web Intelligence**      Provides a self-service for creating ad hoc queries and analysis of data both online and offline. 
- **Publication**           Consists of a collection of Web Intelligence documents to be run as a single task. 

The SMA OpCon SAP Business Objects Connector interacts with the Business Objects scheduler allowing reports (Web Intelligence, Crystal reports and Publications) to be scheduled by OpCon. 
It is possible to answer prompts using definitions within the OpCon job definition. This allows a single report defined within Business Objects to be used multiple times from OpCon using 
different parameters.

When used in conjunction with OpCon Self Service, it allows users to start report tasks from the web selecting answers to prompts from drop down lists. 

![SAP Business Objects Overview](/img/sapbo-connector-overview.png)

The SAP Business Objects Connector supports a START job type which can used be used to communicate with the SAP Business Objects batch environment.

- **START**    can be used to schedule a report defined within the SAP Business Objects environment. The connector initiates the task and does not wait for task completion.

The job definitions are passed to the SAP Business Objects Connector as arguments. The job definition information received from OpCon is then mapped to the appropriate structures 
and the Business Objects Server is called. Each job type requires a valid user and password which the connector uses to establish the connection to SAP Business Objects. 

---