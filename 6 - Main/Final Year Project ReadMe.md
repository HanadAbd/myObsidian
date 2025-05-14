# MyQueryProject

This repository contains the implementation for the "MyQueryProject" system described in my Final Year Report. It's purpose is to get data across different types and timeliness and efficiently and safety in order to aggregate data and generate reports and queries for analysis.

It is currently hosted on [queryproject.tech](https://queryproject.tech)

Table of contents
--
1. Installation and Setup
2. Usage

## Installation and Setup

### Running Locally

For running the application locally, on your machine for deployment and testing:

**Prerequisites for local machine:** 

- Docker
- Docker-Compose
- Golang
- Tsc

**Steps:**  

1. Clone the repository to local folder: 
```
git clone git@git.cs.bham.ac.uk:projects-2024-25/hxa063.git
```

2. Initialise NPM Dependencies: 
```
npm install
```

3. Initialise Golang dependencies:
```
git clone git@git.cs.bham.ac.uk:projects-2024-25/hxa063.git
```

4. Run make file with: 
```
git clone git@git.cs.bham.ac.uk:projects-2024-25/hxa063.git
```

5. Local version of app should be running on port 8080, so http://localhost:8080

### Running in Production

For deploying to a server:

**Prerequisites for Server:** 

- Docker
- Docker-Compose

**Steps:**


1. Set up a Linux webserver
	1.1 Install Docker
	1.2 Install Docker Compose
2. Setup GitLab Repository
	2.1 Initialize environment Variables
	2.2 Initialize Runner
	2.3 Initialize Variables for GitLab runner
3. Git clone the repository 
```
git clone git@git.cs.bham.ac.uk:projects-2024-25/hxa063.git
```

4. Set remote to the new repository
```
git remote set-URL origin
```

5. Push to your new Repository
```
git push -u origin master
```


## Usage

If using previously created workflow