	2025-04-01 11:02

Status:

Tags: [[Final Year Project]]

---
Abstract: 150 words
- Problem I am trying to solve or area of topic
- What I am making
- Point of the project
- What will b


In various industries, logistics and management of various nuanced and unique components can be incredibly difficult visualise and summarise, making it hard to make nuanced decisions, due to the sheer complexity. Although numerous business intelligence tools aim to address these challenges, integrating and analysing diverse data sets remains a significant hurdle.
This report details the implementation of a application designed to safely take data from various data from various data sources in order to generate queries and reports for analysis. It will also detail the performance and data quality of the application in the context of accuracy, latency and timeliness of results as well as system performance, This report will then evaluate how a such a system on both a local and enterprise scale , as well as how it compares to similar industry standard solutions.

# Introduction:

## Problem Statement

**What's Included:**
- Briefly explain what the issue is, with a few figures and explanations to demonstrate the issue.
- State briefly current solutions used as well difficulties 

Businesses—both small and large—incorporate various systems in their daily activities, storing and utilizing data across a myriad of third-party vendors. Although this can be incredibly helpful and necessary to avoid building every system dependency from scratch and to ease maintenance, it can prove to be cumbersome navigating all of these services in order to draw useful insight. Over many decades, there have been vast improvements in the fields of data integration, data warehousing, and business intelligence to address these challenges. The continuous growth in data volume and variety has necessitated the development of robust, scalable systems capable of aggregating, analysing, and visualizing data in efficiently both in real-time and across large amounts of historical data. Despite that, there isn't really an "easy" solution for data analysis 
## Scope of Project

**What's Included:**
- 

This project aims to design, implement, and evaluate a unified system that integrates data from disparate third-party sources. The primary objectives include:

- **System Design and Deployment:** Architecting a solution that aggregates data efficiently and deploying it on a virtual machine (VM) to ensure scalability and ease of maintenance.

- **Testing and Validation:** Utilizing a carefully generated testing dataset that mirrors common business intelligence scenarios. Performance benchmarks, data quality assessments, and enterprise production simulations are integral to this evaluation.

- **Comparative Analysis:** Detailing how the system’s performance, scalability, and reliability compare to current industry solutions. Special focus is given to the trade-offs inherent in using a row-based database architecture versus a columnar storage system.

This report examines on a system named "myProject", detailing its design, implementation, and evaluation, while comparing it against current industry solutions.

## Limitations

**What's Included:**
- Limitation to do with, how data is stored, amount of resources available, testing, in both of use case as well as accurately demonstrating the performance of an application like this

- Limitations to data storage (row based database as opposed to column file system storage) and tools used (not using already established Apache tools)
- Limitations to the amount of resources (since won't be able to have petabytes of data for testing)
- There is a limitation of the  amount of resources used. I can't generate or store 
- For this project, a key element is the making of test data. Although this allows greater customisation, such as a wide, diverse range of reports, more intricate querying and greater system testing to etc. it still fundamentally introduces bias. To minimise bias, I've attempted to incorporate frequently use data models and querying found in typical Business Intelligence applications in industry. Unfortunate limitation, but still provides valuable insight for this report.
## Report Structure

**What's Included:** 
- Brief section describing each section as well as what to expect from each

This paper begins with a literature review in section 2, acting as comparison and analysis of the theory, strategies, and algorithms used for similar projects, as well as better defining the issues presented. Requirements and design of the application are explored in sections in 3 and 4, to clearly explain what's to be expected of the project, as well as defining a structure for our implementation in section 5. The system is then tested against performance and data quality metrics in section 6, as well as going over the testing strategies used for the differences of the application. There is a final evaluation of the project against it's requirements and structure of the project management in section 7. A discussion on Section 8 explores further work to be done, retrospective of things to change, as well as a comparison of how it compares to industry solutions. Finally, it ends with a summary of key findings, results and discussion of objectives met.






# Literature Review

Business Intelligence in Industry

Data Preparation and Handling

Data Processing Architectures

Considerations for Data Processing Engines


# Design


## Architecture

**What's included:**
- Explananation of Applicate Architecture
- Explanation of the Deployment architecture, in terms of how it looks on the server, in terms of the different aspects of the container, as well as how inputs and outputs are managed Between services/components
- Explanation of Code Base architecture, in terms of how it a monolithic application, that attempts to break down into microservice, with each service being it's own package, controlled by a service manager, as well as why not a traditional micro service approach was not done
- Explanation of how messaging and connections, and requests are handled by the application, in terms of REST API's, Web Sockets,  Publish and subscribe, Authentication Middleware

### Application Architectures

$$\text{Figure: Image displaying the architecture for the application looks in terms of workspaces, how user's and login work}$$

For "MyQueryProject", I wanted to define multiple "workspaces" for my application, to define were different a clients add's their infrastructrue and generate reports and queries. To minimise complexity, a multi-tenancy with a shared database and schema is used.

### Server and Client Architecture


$$\text{Figure 0: Final Architecture of Application Deployed on VM  }$$
On a server, a container the application is running, handling backend, front-end, as well as offline-processing, and generating test data. The application will be monolithic to avoid the complexity of managing microservices but will still have services as decoupled as possible (e.g., separating Test data generation from request handling), helping with debugging, testing and ease of development.

Front-end web application is served from our server with NGINX when user visits [http://www.queryproject.tech](http://www.queryproject.tech).

User’s connection details to sources of details as well as conditions of access to the system, which is checked, cleaned, added to a master data set to be handled by a data processing engine followed by a reporting engine.
### Codebase Architecture

$$\text{Figure 0: 2 Images. One showing the structure of services in terms of nesting out of service manager,  and the other displaying the folder strcture in terms of packages}$$

This system is composed of several distinct components that must be managed whether that be the entirely independent test simulation data, backend request handling, constant offline batch request etc. Ideally a microservice approach would be used as opposed to a large monolithic application,  but due to being conscious of time as well as not  focusing too hard outside of the scope of the project, a monolithic approach is used. With Golang, each component can be encapsulated as "packages", whose functinoality and data can be accessed via imports. With that, a package that is it's own folder of the same name is defined as a service that are all intialised and managed via the main function, in `main.go` as well as a dedicated service manager. This allows for greater management, by defining an order of intialisations, handling of faliure, pinging services to test performance and functinality etc.


### Client Interaction

$$\text{Figure 0: Displaying how requests and response and live connections from server is handled. Should demonstrate both, server side rendering, RestAPI's and Websocket connections}$$

When it comes to handling connection to client, Security and handling of inputs as well as how outputs are handled must be carefully considered. Explained further in a different section [TODO: Complete references to section], the language used for handling reports and generating visual components (Typescript )on the client side, is different then the language (Golang)used on server. A complete server side rendering approach of serving the entire completed page, although would be possible, would add further complication, as it's much simpler to have JavaScript render on the browser. 

Since there will also be login's separating workspaces and levels of access within the application. 

## Language tools

**What's Included:**
- Including every major tool that needs to be considered:
- Front-end, so typescript, GridJS and ChartJS, Web pack, Golang HTML Templating
- Back-end, so Golang and it's benefits, NGINX and Hosting, as well as Gorilla web sockets and specifically http requests
- Explanation of docker, docker compose, GitLab and GitLab runner. Just explain what they do and how are typically used. You can explain how it would be. Explain how docker is used to contain the application
- External services worth considering,
#### Front-End

 

Since I am making a full stack web app that can generate visual report elements such as charts and tables, it's necessary return to the client valid HTML, CSS and JavaScript in order to render the web application on browser. In order to not get overwhelmed, I won't be using a framework such as React or Svelte, and will simply be using HTML,CSS and TypeScript.

**Typescript**

TypeScript is Superset of JavaScript, which with the cost of an additional compilation build step, provides static type checking.

This is a positive over traditional JavaScript, since it not only provides strict compilation, helping immensely with debugging. As the project grows larger, and the use of external libraries or creating my own classes which pass different inputs and outputs, enforced types ensure data at every point during the runtime is of expected type. It also has the benefit of working better with IDE, working well with IntelliSense and strict compilation, making dependencies and potential faults easier to recognise at development time.


**GridJS and ChartJS**

As a part of the report generation section for the application, it necessary to have both charts (e.g. Barcharts, PieCharts, Scatter graphs etc.) as well as simply tables to display data. With NPM Package manager, we import packages "GridJS" and "ChartJS" into our project for these visual components. For the front end, these are our only dependencies necessary. This will require a bundler into to build these dependencies alongside our project. Various bundlers work for in  this application, Web pack is used, as is required to be added as another step to our total build step.


**Golang HTML Templating**

For my application, data for the page will need to be served from the server to the clients browser to be rendered. For this, I can simply use the Golang package `html/template` in order simply serve the rendered application. Despite being very simple compared to other HTML renderers e.g. REACT, it works well enough for serving the HTML as well as providing an effective text-based templating language in order to pass data as objects to the page with simple functionality such as looping and conditions.

```HTML
{{if .IsAdmin}}
	<p>You have admin privileges.</p>
{{else}}
	<p>You are a regular user.</p>
{{end}}

```




#### Back-End

**Golang** 
- Include: goroutines, package management to run as services, 

Golang is a programming language developed by google that is frequently referred to as "C for the 21st Century". Reason for this being, it benefits from having a very expansive standard library, rich ecosystem of external libraries as well as architecture designed to break large code bases in to a nested graph of packages.

It's main advantage being it's standard library such as `database/sql` which provides a universal interface for interacting with databases, or `net/http`, again providing a interface for hosting and creating middleware.

Golang also by default supports unit testing with  `go test ./...` . Unlike JavaScript which requires ESLint, Golang has by default has strict compilation, including strong type checking and managing imports.

Although it's easier to have Typescript on front-end and back-end via NodeJS and NPM packages, Golang carries enough benefits to warrant two different languages. It's also worth noting, that the similar syntax of Golang and Typescript makes it considerably easier to work between

``` go
func add(a int, b int) int {
    return a + b
}
```

```typescript
function add(a: number, b: number): number {
    return a + b;
}
```

#### External Services

## Deployment

**What's Included:**
- Explanation of CI/CD pipeline. So brief explanation of the docker file, the deployment file and what's included in it testing, such as building image, pushing it to docker hub registry
- For hosting, explain how it's hosted on digital ocean using droplet  on a Linux VM, how it is SSH on to as well as the configuration of NGINX

### CI/CD



### Hosting

## System Requirements

**What's included:**
- Add these as appendences although provide a brief explanation for what kinds of things are included
- Link to appendix for functional and non-functional requirements
- Brief mention of the social and legal issues

### Requirement Specification

The requirement specification defines the functional and non-functional requirements of the system,  as defined by our research for what is expected from a data processing and reporting solution. The functional requirements of the system are defined using MoSCoW prioritisation [38], and should be reviewed alongside the non-functional requirements when evaluating the solution. These are both defined in Appendix [TODO: Add Appendix section]

### Social and Legal Issues

Due to not working with any used or ongoing production data or infrastructure, the ethical obligations are more laxed, with only needing to ensure:

- **Legal**
- Social
- Ethical
- Professional

# Implementation

# Testing

# Evaluation





##### References
----
