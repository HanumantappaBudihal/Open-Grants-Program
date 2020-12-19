# Open Grant Proposal

> This document is referenced in the terms and conditions and therefore needs to contain all the required information. Don't remove any of the mandatory parts presented in bold letters or as headlines! See the [Open Grants Program Process](https://github.com/w3f/Open-Grants-Program/blob/master/README_2.md) on how to submit a proposal.

* **Project Name:** Project Aurras - MVP
* **Team Name:** HugoByte AI Labs Private Limited
* **Payment Address:** 

*The above combination of your GitHub account submitting the application and payment address will be your unique identifier during the program. Please keep them safe.*

## Project Overview :page_facing_up: 

### Overview

Aurras is a middleware that acts as an event processor and a low code workflow orchestration platform. Aurras as a part of decentralized push notification is a middleware that acts as an event processor which listens to the event from the blockchain and propagate to the registered pool of MQTT brokers. The broader architecture consist of parachain from which the middleware listens for the events.

Aurras as a part of Substrate / Kusama / Polkadot / Web 3 Ecosystem
* Core part of Decentralized Push Notification Architecture  
* Can be Used for Business critical and Industry grade IoT devices to listen to events from blockchain  
* Can be used with other microservices  

### Project Details

#### Architecture
![](https://drive.google.com/uc?export=view&id=1Qk3B65AOVYaDLdxhFmvksZ6Zw2zKKzgX)

#### Technologies
1. [Apache OpenWhisk](https://openwhisk.apache.org) is an open source, distributed Serverless platform that
executes functions (fx) in response to events at any scale. OpenWhisk manages the
infrastructure, servers and scaling using Docker containers. The OpenWhisk platform
supports a programming model in which developers write functional logic (called
Actions), in any supported programming language, that can be dynamically
scheduled and run in response to associated events (via Triggers) from external
sources (Feeds) or from HTTP requests
2. [Apache Kafka](https://kafka.apache.org) is an open-source distributed event streaming platform. Kafka works
well as a replacement for a more traditional message broker. Message brokers are
used for a variety of reasons (to decouple processing from data producers, to buffer
unprocessed messages, etc.). In comparison to most messaging systems, Kafka has
better throughput, built-in partitioning, replication, and fault-tolerance which makes it
a good solution for large scale message processing applications.
3. Docker 
4. Substrate
5. Rust  
6. Go

#### Components
1. **Event Sources (Substrate Event Feed)**  
This is the source for events from the chain which will be sent to the openwhisk system. The MVP event source will be implemented using [polkadot-js/api](https://github.com/polkadot-js/api). For the actual implementation, We will be using a custom version of the substrate archive. Substrate archive will be indexing the
blocks and an event actor will be decoding the events and data from the block and posting them to the OpenWhisk system. The indexer will use a NoSQL database to store the last indexed block and metadata. Using the substrate indexer as our event source will help us in solving many challenges ranging from fault tolerance to scalability to uniquely identifying multiple events with the same payload within a single block. The indexer will be connected to a substrate-based chain and RocksDB where the chain data is stored. When a new block is produced by the chain, the indexer collects the raw blocks from the RocksDB and is sent to the event actor. The event actor processes the block. The block data is decoded using the parity scale codec and mapped with the data types provided to the runtime. Once the event is decoded, the event actor posts a trigger to the event trigger manager.
2. **Event Trigger Manager**  
Event trigger manager is composed of multiple actions, database to store trigger URLs and
their respective auths, and Kafka provider, consumer and producer. Once the event manager receives an event from the event feed, this data is produced to a topic. The feed action in the trigger manager lets the user hook into the system so once an event is indexed to a particular topic, it can invoke a particular action. While creating the workflow, users can choose the event trigger as feed and provide necessary parameters from which chain it should be listening to and from which block it should start listening. Under the hood, a feed action is
invoked with create lifecycle, which accepts the mandatory parameters the lifecycle, auth,
trigger name, and other optional parameters of the event source. The feed action invokes the
related actions of creating the entry in the database, adding to the Kafka consumer group, etc. The next component in the event trigger manager is a persistent connection to Kafka where it is used to produce and consume the stream of data. Once data is received in Kafka, the event trigger manager invokes the action to check the consumer groups for that particular
topic and if found any the trigger for the users under that particular group is invoked, which in
turn invokes the workflow action.
3. **Workflow Composer**  
Workflow composer consists of an async Rust library to compose multiple triggers,
deployment configuration generator, and whisk deployment tool. For creating the workflow,
the only input is the configuration file which is a YAML file. The workflow composition is laid out
in the YAML which in turn takes care of the deployment and composing the triggers. Once a
workflow is deployed to a namespace it creates a specific topic unique workflow id in Kafka.
Workflow configuration comprises the input URL of workflow tasks, primarily GitHub repo,
the sequence of processing tasks, and argument structure. Arguments must match the task input parameters.
4. **Web API Gateway and Backend Service** 
This is the end user facing component to utilize the workflow. This component comprises of a
backend application which is responsible for user registration, selecting the workflow,
managing / creating workflow using friendly APIs, providing input parameters. API gateway /
Machine gateway where the external world can connect to the Aurras system.
### Ecosystem Fit
We have identified many great teams had to build their own implementation of event listeners/monitoring tools, we intend to make it easier for the community to avoid most of the boilerplate and just focus on workflow actions/task which is related to their project.

* https://github.com/playproject-io/datdot-service
* https://github.com/open-web3-stack/guardian

Similar projects
* https://github.com/PipedreamHQ/pipedream
* https://github.com/snakemake/snakemake
* https://github.com/aelassas/Wexflow

What makes us different is

As a part of Web 3 Community and Ecosystem
* First class support to connect blockchains
* Deployment and definition of workflows will be done through easy to write YAML configuration.
* Workflow tasks can be written in multiple languages -  NodeJS, Go, Java, Scala, PHP, Python, Ruby, Ballerina, .NET and Rust (We prefer and Recommend WASM compatible Rust)
* First class support to MQTT Endpoints.

## Team :busts_in_silhouette:

### Team members
* Dr. C. Pethuru Raj Ph.D - Principal Advisor, Chief Architect and Vice-President, Site Reliability Engineering (SRE) Division - Reliance Jio Platforms Ltd.
* Muhammed Irfan K - Team Lead, Fullstack Developer, CTO & Co-Founder - HugoByte AI Labs
* Hanumantappa Budihal - Solutions Architect, DevOps - HugoByte AI Labs	

We will be hiring two Rust Developers

### Contact
* **Contact Name:** Muhammed Irfan K
* **Contact Email:** muhammedirfan@hugobyte.com
* https://hugobyte.com

### Legal Structure 
* **Registered Address:**  
HugoByte AI Labs Private limited  
1st & 2nd Floor, IBIS Hotel, Hosur Road, Bommanahalli, Bengaluru  
Bangalore, Karnataka, India, 560068 
* **Registered Legal Entity:**  
HugoByte AI Labs Private limited  
CIN: U72900KA2020PTC140106
### Team's experience
* Dr. C. Pethuru Raj Ph.D  
Dr. C. Pethuru Raj is currently working as Chief Architect and Vice president in the Site Reliability Engineering (SRE) Center of Excellence, Reliance Jio Infocomm Ltd. (RJIL), Bangalore. Previously worked as a cloud infrastructure architect in the IBM Global Cloud Center Of Excellence (CoE), IBM India Bangalore for four years. Before that, He had a long stint as TOGAF-certified enterprise architecture (EA) consultant in Wipro Consulting Services (WCS) Division, Also worked as a lead architect in the corporate research (CR) division of Robert Bosch Bangalore. In total, He has gained
more than 17 years of IT industry experience and 8 years of research experience. Completed the CSIR-sponsored Ph.D. degree at Anna University, Chennai, and continued with the UGC-sponsored postdoctoral research in the Department of Computer Science and Automation, Indian Institute of Science, Bangalore. Thereafter, He was granted a couple of international research fellowships (JSPS and JST) to work as a research scientist for 3.5 years in two leading Japanese universities. Published more than 30 research papers in peer-reviewed journals such as IEEE, ACM, Springer-Verlag, Inderscience, etc. Having authored 25 books thus far that focus on some of the emerging technologies such as IoT, Cognitive Analytics, Blockchain, Digital Twin, Containerization, Data Science, Microservices Architecture, fog/edge computing, etc. Also have contributed more than 30 book chapters thus far for various technology books edited by highly acclaimed and accomplished professors and professionals. He is currently advising the team at HugoByte AI Labs on impactful technology innovations.

* Muhammed Irfan K  
Muhammed Irfan K is a strategic thinker and implementer of innovative ideas with
an emphasis on educating and bringing back privacy to the people. Having Co-Founded HugoByte AI Labs and Serving as CTO. He envisions a world where AI is open, distributed, and democratized by building a decentralized infrastructure and policy framework to regulate it. He has extensive experience in designing and building Highly Scalable Enterprise Architecture, Leading Team, Full-Stack
Development, Microservices, Machine Learning.

* Hanumantappa Budihal  
Hanumantappa Budihal has 4 years of experience as an Application Developer and Azure DevOps Engineer. His technical skills include .NET Core Framework, Azure DevOps, SQL Developer, ASP .NET MVC, REST Web API, WPF, Microsoft Azure, Cognitive Services, Algorithms Design for a complex business requirement, and Watson Discovery, with good knowledge of Application Architecture and Design pattern implementation and data analysis skills. He is a hard worker moreover eager to learn new skills. He has also worked on cognitive application development using various IBM Bluemix services such as conversation, Natural language understanding, Watson discovery, and developed few chatbots using Api.ai and Microsoft bot framework. He is currently working as a Solutions Architect in HugoByte AI Labs.
 
### Team Code Repos
* https://github.com/i7326/hackusama ([Hackusama Submission](https://devpost.com/software/contact-tracing-chain))
* https://github.com/hugobyte
* https://github.com/MuhammedIrfan
* https://github.com/HanumantappaBudihal  

### Team Profiles
* Dr. C. Pethuru Raj Ph.D - https://sweetypeterdarren.wixsite.com/pethuru-raj-books  
* Muhammed Irfan K - https://www.linkedin.com/in/muhammed-irfan-k  
* Hanumantappa Budihal - https://www.linkedin.com/in/hanumantappa-budihal/ 

## Development Roadmap :nut_and_bolt: 

### Overview
* **Description** Development of Project Aurras - MVP 
* **Total Estimated Duration:** 3.5 months
* **Full-time equivalent (FTE):**  5
* **Total Costs:** 

### Milestone 1 — Event Source - Substrate Event Feed
* **Estimated Duration:** 
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Configuration Documentation, Event Post Action Deployment guide, Openwhisk Setup Documentation, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests | 
| 1a. | Substrate Event Feed: Configuration | Reading Configuration based on Environment, Override Configuration if Environment Variables provided, Configrations for Chain endpoint Sections and Methods from extrinsic to Exclude, types, Openwhisk Endpoint, Openwhisk Auth Key, Trigger Endpoint, Kafka Topic and Brokers |
| 1b. | Substrate Event Feed: Chain Module | Connects to the chain, Add custom type to chain intialization if provided, Subscribes to system.events |  
| 1c. | Substrate Event Feed: Event Module | Filters Events based on excludes provided, Post Events to trigger Endpoint |  
| 1d. | Substrate Event Feed: Docker Image | Dockerfile for Containerization  |  
| 1e. | Substrate Event Feed: Docker Compose Configuration | Docker Compose Configuration  |
| 2. | Event Manager: Event Post Action | Minimal JS Implementation of Event POST Action with Payload as Kafka Topic, Broker and Event Data such as section, method and Event Payload |


### Milestone 2 — Event Manager - Phase 1
* **Estimated Duration:** 
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Configuration Documentation, Kafka and Zookeeper Deployment guide, wskdeploy guide, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |  
| 1. | Kafka Provider: Fork | Fork Existing [openwhisk-package-kafka](https://github.com/apache/openwhisk-package-kafka/) |
| 2a. | Event Manager: Event Source Registration | Register Source with Chain Name, Chain Specification, Create Unique topic for provided Section-Method, Return created topics - Section-Method Map |
| 2b. | Event Manager: Kafka provider feed action | Implement CouchDB integration, Connect DB provided through environment variable, Add CREATE, READ, UPDATE, DELETE lifecycle methods for trigger, Validate parameters (topic, broker, isJSONData, isBinaryValue, isBinaryKey), Record topic and related trigger to DB on CREATE lifecycle |
| 2c. | Event Manager: Deployment Config | Deployment Config for [wskdeploy](https://github.com/apache/openwhisk-wskdeploy) tool | 
| 2d. | Event Manager: Intermediate Container | Dockerfile for Containerization, Container with wsk cli and wskdeploy util, Script to add Openwhisk auth key, Deploy Openwhisk Actions and Create Triggers and Rules |
| 2e. | Event Manager: Docker Compose Configuration | Docker Compose Configuration  |

### Milestone 3 — Event Manager - Phase 2
* **Estimated Duration:** 
* **FTE:**  
* **Costs:** 


| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Configuration Documentation, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |
| 1a. | Event Manager: Kafka Produce Action | Validate for parameters, Connect to provided brokers, Produce data to provided topic, Add deployment config to wskdeploy config |
| 1b. | Event Manager: Kafka provider feed action | Delete trigger from DB on DELETE lifecycle, Read trigger from DB on READ lifecycle, Update trigger from DB on UPDATE lifecycle |
| 2a. | Substrate Event Feed: Configuration | CouchDB Config, Available Sections and Methods of the chain to create unique topics |
| 2b. | Substrate Event Feed: Event Source Registration | CouchDB Integration, Save Unique ID in DB for topic provided through Event Manager: Event Source Registration | 
 

### Milestone 4 — Workflow Composer - Phase 1
* **Estimated Duration:** 
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Composer Configuration Documentation, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |
| 1a. | Workflow Composer: YAML Config Specification | JSON Schema, Configuration Specification |
| 1b. | Workflow Composer: YAML Config Parser | Parse the config file with the specification provided |
| 1c. | Workflow Composer: Build Script | Convert YAML to struct |
| 1d. | Workflow Composer: Rust Openwhisk Client Library | Minimal Implementation to Openwhisk Rust Client |
| 1e. | Workflow Composer: Composer | Wrapper Library to integrate plugging operators and Openwhisk Client |
| 1f. | Workflow Composer: Pipe Operator | Operator Interface to connect other operators |


### Milestone 5 — Workflow Composer - Phase 2
* **Estimated Duration:** 
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Operator Documentation, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |
| 1a. | Workflow Composer: Derive Macro | Procedural Macro to build rust code from the Struct created from the YAML file |
| 1b. | Workflow Composer: Concat Operator | Operator to concat the tasks in a sequential order |
| 1c. | Workflow Composer: Map Operator | Operator transform the output of a task |

### Milestone 6 — Web API/Backend
* **Estimated Duration:** 
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | MIT  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Operator Documentation, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |
| 1a. | Web API: Workflow Registration | API Exposed as a part of workflow deployment, Workflow will be registered and made available to specific namespace |
| 1b. | Web API: User Registration | Basic User Registration API to register user to the system |
| 1c. | Web API: User Workflow Management | User to select workflow and provide argument values, Pause Workflow, Delete Workflow |
| 2a. | Workflow Composer:  Workflow Registration | Action to communicate to Web API: Workflow Registration with workflow and arguments specification |


## Future Plans
Immediate Plans in the timeline Includes
* Develop full fledge system
* Implement Custom Version of Substrate Archive
* Add more operators
* Add Analytics and Monitoring  
* MQTT Endpoints  
* Decentralized push notification  

Our Roadmap includes
* Decentralized Pub/Sub Network to replace Apache Kafka in Aurras
* WASI Runtime for Openwhisk

## Additional Information :heavy_plus_sign: 
Any additional information that you think is relevant to this application that hasn't already been included.

Possible additional information to include:
* What work has been done so far?  
This is our first grant as a part of bringing innovation to the web3 Ecosystem.
* Are there are any teams who have already contributed (financially) to the project?  
No
* Have you applied for other grants so far?  
No
