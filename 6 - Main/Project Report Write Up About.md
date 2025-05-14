2025-03-17 10:47

Status: #baby 

Tags: [[Final Year Project]]

---

Summary of Project and point of it:

To create an application that can query any data source in varying ranges of structure and data timeliness in order to generate reports.

What I want for this application to include is:
- Converting many different types of data sources into a consistent log format (possibly based on Kafka or something to do with apache beam) So it can be handled by the application in a consistent way, whilst allowing configuration for how this is done in relation to the user's system
- Process for reading data from these data sources into a production database, as well the different implementations and handling different scenarios for them
- Explanation of how this would work as both a On Premise and Enterprise solution
- Testing that includes terabytes worth of batch data, and gigabytes of real time data, and viewing it's performance as well as handling of faults and other performance metrics, once turning on and off
- Changes I would make to make this more effective as a On Premise Solution using actual functional open-source solutions
- 

**Abstract**:

**Chapter overview and layout:**

- **Abstract**: 100 -200 words

- **Introduction**:  1000 words 
	
Overview of how the rest of this report we'll be structured

- Research: 1500 words
  lambda architecture again

- Design and system requirements: 1500 words
	Final design of Lambda architecture used
	Break down of services and architectures to be used
	Technologies used
	Immediate limitations that need to be considered for deployment
  
- Implementation: 3000 words

 - Testing and success measurement: 1500 words
   Liveness and safeness
   Performance against the three metrics, accurate, timeliness and latency

- Evaluation:  500 words
	Challenges found in the project
	How well requirements have been met
	Any immediate lingering issues or additions that would be helpful
	
- Limitations and future challenges: 1000 words
	Developments necessary for better on-premises and enterprise level applications
	Fundamental changes or overhauls that would need to be necessary, to make this more functional e.g. Having converting data to a series of logs be it's own completely separate service, and just use kappa architecture and systems revolved around taht
- Conclusion: 200 words

Abstract:
1. Introduction
	Problem Statement
	Scope of Project (Explain what we are testing and kinds of things seeking to create e.g. Scalable application for generating multiple reports connecting to multiple data sources )
	Limitations
	Report Structure
2. Background Research 2000 words
	2.1 Business Intelligence in Industry
	2.2 Data Preparation and Handling
	2.3 Data Processing Architectures
	2.4 Considerations for Data Processing Engines
3. Design
	3.1 Architecture(Lay out of architecture used shown via an image both in deployment and in terms of code) 
		3.1.1 Application Architecture
		3.1.2 Server and Client Architecture
		3.1.3 Codebase Architecture
		3.1.4. Client Interaction (web sockets, REST API's, Authentication )
	3.2 Language tools
		3.2.1 Front End
		3.2.2 Backend
	3.3 Deployment (Includes CI/CD, testing, build steps, hosting, certificates etc.)
		3.3.1 CI/CD (what's included in the pipeline, description of docker file) Explanation of docker and GitLab and GitLab Runner
		3.3.2 Hosting(explanation of digital ocean, droplets and VMs')
	3.4 System Requirements (Add these as appendences although provide a brief explanation for what kinds of things are included )
		3.1 Functional Requirements
		3.2 Non - Functional Requirements
		3.3 Social and Legal Issues
	
4. Implementation
   
5. Testing 
5.1 Performance Testing
		5.1.1 Rate of throughput
	5.2 Data Quality Testing
	5.3 System Health Testing
	5.4 Code Testing
		5.4.1 Unit Testing
		5.4.2 Integration Testing 
6. Evaluation
	6.1 Requirement Specification
		6.1.1 Functional Requirements
		6.1.2 Non - Functional Requirements
	6.2 Project Management
7. Discussion
	7.1 Further work to be done
	7.2 Comparison to Enterprise Solution
	7.3 Conclusion

References

- asdasd
- asda

*Contents*
*ABSTRACT	1*
*CONTENTS	2*
***INTRODUCTION	5***
	*1.1	PROBLEM STATEMENT	5*
		- Should go over what BI and BDA is
		- Should go over what BI and BDA is used for in in various industries, explaining how different analyses gain different useful insight which can be applied back to industry, such as for generating reports, including a few of it's benefits and acheivements
		- Mention difficulties with this solution and implementing it, such as complexity, maintenance, and necessity for ssbi solution less relaint on IT 
	*1.2	SCOPE OF PROJECT	5*
		- Defines the challenges that will need to be discussed through out the rest of the report.
		- Make clear that key point of product is to implement my own system as much as I can, which includes creating my own webpage
	*1.3 LIMITATIONS	6*
	*1.4 REPORT STRUCTURE	6*
	***BACKGROUND RESEARCH	8***
		*2.1 Big Data Analysis Overview* 300 words
		-  Discuss the different types of analysis that can occur with BI and BDA, briefly discussing predictive analysis etc.. As well as mentioning the evolution of BI to include more solutions such as real-time , self serving BI etc.
		 - Describe briefly structured and unstructured data as well as what counts as big data and how it effects analysis, as well as how technology allowed for more complex analysis
		- Mention common KPI's and metrics, reports etc. necessary and used for different business e.g. cycle time, pph etc. More importantly referring to what these need to do e.g. queries that aggregate over time that is filtered or some other more categorically situation e.g. birthday inference problem 
		- Discuss an example query or report page, including sources of data and requirements for it. This might include a query across time for x amount of data sources with y different conditions to consider. This can be referenced in later situations to explain and react to situations.
		*2.2 BUSINESS INTELLIGENCE: RELATED WORKS	8* 300 words
		-Main point of this section is to give an overview of the current state solutions regarding this problem.
		- Should go over what types of works and tooling are relevant in the context of SSBI and BDA and why, such as that to do with processing, visualisation, creation of queries. This includes SSBI, LCP, BI Tool frameworks. Break it down in to data processing, analytical tools and services that support either (e.g. dbt for pipelines, conflunce ksql to provide sql's to Apache Kafka streams)
		- Should discuss and mention a few technologies for each data processing (e.g. storage, networking, processing etc,), analyical egines (for different types of analusis) and services that support them (pipeline, managing schema etc.). Divided into those sections
		- Discuss requirements for SSBI solutions, such as handling complexity, typically using SQL or simple UI as well as difficulties regarding it. Discuss state of SSBI currently tools that attempt BDA in terms of how they do it, and to what effect
		*2.3 DATA PROCESSING ARCHITECTURES	11* 300 words
		- Discusses the requirements and necessity for a data processing Architecture and what they can do, such as real-time processing combined with batch processing.
		- Discuss how the lambda architecture works, explaining how each of the layers work, as well as briefly the query layer.
		- Explain the benefits of such solution, referencing event data approach, fault tolerant solutions with tools used and implementations etc.
		- Go over lambda architecture implementation of query/report (explain through a chart, how that would work in a higher level overview)
		- Discuss Kappa architecture as well as other similar architectures that have been made since
		- Discuss how lambda architecture is a good example go over fundamental data processing components, such as DW/BI, Batch processing, Stream Processing and Distribution. 
		*2.4 DATA Pipelines	10* 300 words
		-Give a breif overview of the data pipeline approach of raw data to insight and what's included e.g. storage schema, etc.
		- Discuss how OLAP (in the context of the serving layer) and ETL process and data pipelines help with this. Discussing the requirements for such a solution, implementations . AS well as changes over time that has happened in terms of technology.
		- Refer to how schema's are related to this issue as well as how they are defined, especially in the case of BDA where unstructured data or changing data is involved.  
		- Discuss common data models used to structure analysis, such as star schemas, galaxy schemas, as well as common aggregation strategies.
		- Using this, Discuss how this would effect the solution derived and requirements for pipeline made in case of the query e.g. adding universal uuid to each event added to master data set, indexing (so table of addresses for faster lookup) and partioning field. (Explain through a chart) Refer to how these different descisons are typically handled IT development and how SSBI solutions might bridge that gap for data analysis
		- Explain the current state of tools regarding this
			  *2.5 Distributed Systems for Data Processing	11* 300 words
			- Explore the necessity for distributed system in the case of BDA
			- Explain how it scales either vertically or horizontally through machines via a distributed systems. exploring map reduce as well as modern implementations of it and distirbution in general, how they work, requirements for it
			- Explain all instances where distribution can occur for data processing e.g. storage , computaiton etc. as well tools and methods to address them, how it is handled in nathan marz's implementation with Adobe Hadoop and storm
			- Expain requirements for distribution as well as considerations necessary for it due to complications arised e.g. ACID,CAP, PACLEC, fault tolerance, pagination, indexing, replication etc.
			- Explore how lambda architecture and other data processing architectures /solutions use distributed systems in their design
			- Discuss how this effects the query in terms of how it is handed (explain through a chart), so this includes how recomputation of Refresh process happens in parallel, and how different scenarios are handled, all to get the greatest performance
			*2.6 LIMITATIONS AND CHALLENGES13* 300 words
			 - Discuss issues and limitations with Lambda architecture, such as complexity from having 2 similar but different architectures, issues , being hard to tell if there's been duplicates, requires incremental refreshing of batch layer along side full computational refresh which adds greater complexity which it is trying to avoid.
			 - Discuss complication with query layer, or querying across time which will require someway of combining results of queries against each other
			 - Discuss the various ways incremental algorithms pop up such as for refreshing for ETL Pipelines, refreshing real-time views with new data etc. and how they are done. Use the query as an example to show how continous queries are updated by explaining they are converted to incremental formats, with meta data and directed graghs managing data required and how it's integrated to get thre new data
		*2.6 LIMITATIONS DERIVED FROM RESERARCH13* 100 words
		- Define limitations and takeway from research to define design of what's being made
	 
***DESIGN	16***
	*3.1 ARCHITECTURE	16*
		*3.1.1 Application Architecture	16*
		*3.1.2 Server and Client Architecture	16*
		- Create an image that depicts every dependency and every component in terms of how it works and how it's loaded to server
		*3.1.3 Codebase Architecture	17*
		*3.1.4. Client Interaction	18*
	*3.2 LANGUAGE AND TOOLS	20*
		*3.2.1 Front-End	20*
		*3.2.2 Back-end	21*
		*3.2.3 Timescale DB	21*
		*3.2.5 Redis Cache	22*
		*3.2.5 Apache Kafka and Zookeeper	22*
		*3.2.4 Docker and Docker Compose	22*
		*3.2.5 GitLab and GitLab Runner	22*
	*3.3 DEPLOYMENT	23*
		*3.3.1 CI/CD	23*
		*3.3.2 Hosting	24*
		*3.4 SYSTEM REQUIREMENTS	24*
		*3.4.1 Requirement Specification	24*
		*3.4.2 Ethical and Legal Requirements	24*
***IMPLEMENTATION	26***
	*4.1 BACK-END	26*
		*4.1.1 Converting Data Sources to Logs	26*
		- Create a a table of data sources, stating how it is converted to log format (kafka connect, natively like that, debezium), conditions for conversion (Excels/CSV's might need to read to data)
		- Show form adding data sources to the page and how it is handled securely
		- State how schema's are defined
		*4.1.2 Batch Layer	27*
		- Mention how, using various 3rd party Golang services
		- Mention how user add’s data sources that is stored as azure key
		- Add figures showcasing this addition, as well as testing button to test how it is done
		- Mention how these are configured in terms refresh time, amount of refresh, filtered refreshes, ,
		- Constraints for each data source
		- Full load vs incremental load
		- Enforcing schema
		*4.1.3 Serving Layer	27*
		- ETL Pipelines in the ETL Page
		- How data models are made
		- How full refreshes and incremental refreshes occur
		- Metadata for each Pipeline
		- Configuration for each Pipeline
		*4.1.4 Speed Layer	28*
		- Explain how data is read in real-time from these data sources to populate read only views of the data
		*4.1.5 Query Layer	28*
		- Explain how different queries are combined across the speed layer and batch layer in accordance to time.
		- 
		*4.1.6 Incremental Refresh of Queries	28*
		- explain how pgivm is used, where incremental refreshes are necessary e.g. incremental recomputaiotn of queries etc.
		- 
		*4.1.7 Distributed Systems	28*
		- State how the applicaiton handles distribution with docker compose to create 3 different instances.
		- Explain how each application is connected to each other and share resources and different recomputation across different machines using MapReduce Pardaigms
		- Explain how it works and changes necessary for certain things to work in this implementation.
	*4.2 FRONT-END	28*
		*4.2.1 User Interface	28*
		- Discuss how and what data is serverd to the client via a page
		- How it handles interactivity with the page
		*4.2.2 Page Rendering	28*
		- Discuss the structure in which data sent from the server is renderd into visual, interactable components
		- Discuss how the renderer and server relation ship works as well as how components are defined.
		- Discuss what happens if something is filtered or there is some request to change data on the page.
		- Discuss issues that need to be handled with so much data that needs to be sent to the page, as well as interaction with live data
		*4.2.3 Page Visualizations	29*
		- Discuss the different types of compoments of the page, how they inherit from a single class as well as structure for their code.
		- Briefly discuss how each type is implemented
		- Then discuss how components for the page are created through a page designer.
***TESTING	30***
	*5.1 TESTING DATA	30*
	*5.2 PERFORMANCE TESTING	31* 150 words
	- Go over how the testing will be done and what we are trying to test for.
	- Go over metrics being used as well as well as methodology which can be a list of points e.g. Be using x amount of data sources to generate y amount of historical batch data as well as z amount of real-time data generated. What's required to make it accurate.
***EVALUATION	33***
	*6.1 REQUIREMENT SPECIFICATION	33*
	*6.1.1 Functional Requirements	33*
	- State whether or not functional requirements were met
	- Discuss key functional requirements that were unfortunately not met and why ( around 2 or 3)
	*6.1.2 Non-functional Requirements	33*
	- Go over each key non-functional requirements section and state how far they have been met
	*6.2 REVIEW OF APPROACH	33*
	- Review of approach used to solve the problem defined in the problem scope.
	*6.2.1 Advantages of Approach	33*
	- Discuss the advantages of the approach used. This includes mentioning how i have a functional self-hosted solution is containerised and would work on any given machine
	- Mention how far the problem statement is addressed by mentioning the division of labour against data analyst and it specialist in order to maintain the appliciation, as well as providing a real-time solution
	- Also briefly mentioned insight gained for batch processing, stream prrocessing and data analytics
	*6.2.2 Disadvantages of Approach	33*
	- Discuss disadvnrages of the approach used  which includes a few things. Poor design descisions early on using lambda architecture and postgres database.
	- Brief mentioing of the limited amount of data analysis, with a greater focus on KPI's and tradtional SQL queries despite their being far more many options.
	*6.3 PROJECT MANAGEMENT	34*
***DISCUSSION	36***
	*7.1 FURTHER WORK TO BE DONE	36*
	*7.1.1 CHANGES WITHIN DESIGN SCOPE	36*
	- Discussion changes that keep within design scope, So keeping within lambda architecture. that addresses solution discussed in scope. This includes PostgreSQL database used being natively single noded so how that would work to make it distrubted, 
	- Discuss what open source technologies Could be used to replace elements used such as Apache frameworks, handling data pipelines , pgIVM, handling incremental views, Stable frameworks that can be used such as gin tonic combined with Svelte
	- Using more then just SQL, such as literal code, or BI ribbon such as what is provided by Microsoft PowerBI
	- Breif mention of security, including using oAuth for authentication, and combined with middleware to confirm against requests from
	*7.1.2 CHANGES BEYOND DESIGN SCOPE	36*
	-Organise this from going self hosting to further cloud hosting instead, unloading services and technologies to third party stable sources and describing how they would implement with it.
	- Discuss how the Kappa architecture works in more detail and how i could change my solution to work for that solution. With this, offer criticism of lambda architecture and inform how it was born e.g. issues with real-time computation at the time as well as how it handles the CAP theorem.
	- Create an image similar to the deployment in design but kappa architecture, stating what is or isn't kept the same and displaying what differences there are and how it would work
	- Discuss further the limitations of postgres as opposed to HDFS solutions, in terms of distribution and how it handles message streaming 
	- Explain using modern technologies and services and this would be done. This includes all sections such as data pipelines, streaming platforms, managing websocket connections
	- Discuss how horizontal scaling platforms are relevant, could be used as well as how they would do it. 

	*7.2 CONCLUSION	37*
	- Summarise everything that comes under
***REFERENCES	38***
*A SCREENSHOTS	41*
	- Covers login page
	- Main workspace page
	- Dashboard Page
	- Data source page (including adding new data source with testing connection added, and showing performance and metric data for the given page)
	- ETL page (including depiction of metadata and performance)
	- 
*B REQUIREMENTS SPECIFICATION	42*
	*B.1 FUNCTIONAL REQUIREMENTS	42*
	*B.2 NON-FUNCTIONAL REQUIREMENTS	43*
*C GITLAB REPOSITORY	45*
	*C.1 RUNNING LOCALLY	45*
	*C.2 RUNNING IN PRODUCTION	45*



##### References
----
[Good Example Report](file:///C:/Users/Asus/Documents/final_year_project/Report/Examples/uob_examples/undergrad/CS1.pdf)
[Game Report](file:///C:/Users/Asus/Documents/final_year_project/Report/Examples/uob_examples/undergrad/CS4%20(Game%20Example).pdf)
[Roshan's example](file:///C:/Users/Asus/Documents/final_year_project/Report/Examples/Roshan's%20Final%20Year%20Project/Final_Year_Paper_9747353.pdf)
[[Project Report Notes]]