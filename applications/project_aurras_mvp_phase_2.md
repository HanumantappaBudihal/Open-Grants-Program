TODO : need to add the content
# Open Grant Proposal

> This document is referenced in the terms and conditions and therefore needs to contain all the required information. Don't remove any of the mandatory parts presented in bold letters or as headlines! See the [Open Grants Program Process](https://github.com/w3f/Open-Grants-Program/blob/master/README_2.md) on how to submit a proposal.

* **Project Name:** Project Aurras - MVP - Phase 2
* **Team Name:** HugoByte AI Labs Private Limited
* **Payment Address:** TODO : Need to add the payment address

*The above combination of your GitHub account submitting the application and payment address will be your unique identifier during the program. Please keep them safe.*

## Project Overview :page_facing_up: 

### Overview

Aurras is a middleware that acts as an event processor and a low code workflow orchestration platform. Aurras is being pitched as a next-generation system for enabling decentralized push notification. This middleware solution listens to events from blockchain applications and propagates them to a registered pool of MQTT brokers. The broader architecture consist of parachain from which the middleware listens for the events.

Aurras as a part of Substrate / Kusama / Polkadot / Web 3 Ecosystem
* A core part of Decentralized Push Notification Architecture
* Can be used for business-critical and production-grade IoT devices to listen to events from blockchain
* Can be used with microservices across industry verticals
* Can be expanded to get integrated with data analytics, knowledge visualization, and machine and deep learning (ML/DL) algorithms
  

### Project Details

#### Architecture
![](https://storage.googleapis.com/hugobyte-2.appspot.com/Aurras%20Architecture.png)

#### Technologies
1. [Apache OpenWhisk](https://openwhisk.apache.org) is an open source, distributed Serverless platform that executes functions (fx) in response to events at any scale. OpenWhisk manages the infrastructure, servers and scaling using Docker containers. The OpenWhisk platform supports a programming model in which developers write functional logic (called Actions), in any supported programming language, that can be dynamically scheduled and run in response to associated events (via Triggers) from external sources (Feeds) or from HTTP requests
2. [Apache Kafka](https://kafka.apache.org) is an open-source distributed event streaming platform. Kafka works well as a replacement for a more traditional message broker. Message brokers are used for a variety of reasons (to decouple processing from data producers, to buffer unprocessed messages, etc.). In comparison to most messaging systems, Kafka has better throughput, built-in partitioning, replication, and fault-tolerance which makes it a good solution for large scale message processing applications.
3. Docker 
4. Substrate
5. Rust  
6. Go

TODO : Need to add more info about the technologies

#### Components
1. **Event Sources (Substrate Event Feed)**  
This is the source for events from the blockchain and the events will be sent to the OpenWhisk system. The MVP event source will be implemented using [polkadot-js/api](https://github.com/polkadot-js/api). For the actual implementation, we will be using a custom version of the substrate archive. Substrate archive will be indexing the blocks and an event actor will be decoding the events and data from the block and posting them to the OpenWhisk system. The indexer will use a NoSQL database to store the last indexed block and metadata. Using the substrate indexer as our event source will help us in solving many challenges ranging from fault tolerance to scalability to uniquely identifying multiple events with the same payload within a single block. The indexer will be connected to a substrate-based chain and RocksDB where the chain data is stored. When a new block is produced by the chain, the indexer collects the raw blocks from the RocksDB and sends it to the event actor. The event actor processes the block. The block data is decoded using the parity scale codec and mapped with the data types provided to the runtime. Once the event is decoded, the event actor posts a trigger to the event trigger manager.  

2. **Event Trigger Manager**  
Event trigger manager is composed of multiple actions including using a database to store trigger URLs and their respective auths, and Kafka provider, consumer and producer. Once the event manager receives an event from the event feed, this data is produced to a topic. The feed action in the trigger manager lets the user hook into the system. That is,  once an event is indexed to a particular topic, it can invoke a particular action. While creating the workflow, users can choose the event trigger as feed and provide necessary parameters from which chain it should be listening to and from which block it should start listening. Under the hood, a feed action is invoked with create lifecycle, which accepts the mandatory parameters the lifecycle, auth, trigger name, and other optional parameters of the event source. The feed action invokes the related actions of creating the entry in the database, adding to the Kafka consumer group, etc. The next component in the event trigger manager is a persistent connection to Kafka where it is used to produce and consume the stream of data. Once data is received in Kafka, the event trigger manager invokes the action to check the consumer groups for that particular topic and if found any, the trigger for the users under that particular group is invoked, which in turn invokes the workflow action.  

3. **Workflow Composer**  
TODO : Need to add the description  

4. **Web API Gateway and Backend Service**   
TODO : Need to add the description 

### Ecosystem Fit
TODO : Need to add the description

* https://github.com/playproject-io/datdot-service
* https://github.com/open-web3-stack/guardian

Similar projects
* https://github.com/PipedreamHQ/pipedream
* https://github.com/snakemake/snakemake
* https://github.com/aelassas/Wexflow

What makes us different is

As a part of the Web 3 Community and Ecosystem
* First class support to connect blockchains
* Deployment and definition of workflows will be done through easy-to-write YAML configuration.
* Workflow tasks can be written in multiple languages - NodeJS, Go, Java, Scala, PHP, Python, Ruby, Ballerina, .NET and Rust (We prefer and recommend WASM compatible Rust)
* First class support to MQTT Endpoints.  

## Team :busts_in_silhouette:

### Team members
* Muhammed Irfan K - Team Lead, Fullstack Developer, CTO & Co-Founder - HugoByte AI Labs
* Hanumantappa Budihal - CIO & Solutions Architect, DevOps - HugoByte AI Labs	
* Shreyas Kura Subramanya - Development Team Lead - HugoByte AI Labs Pvt Ltd

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

**Muhammed Irfan K**  
Muhammed Irfan K is a strategic thinker and implementer of innovative ideas with an emphasis on educating and bringing back privacy to the people. Having co-founded HugoByte AI Labs and serving as its CTO, he envisions a world where AI is open, distributed and democratized by building a decentralized infrastructure and policy framework to regulate it. He has extensive experience in designing and building Highly Scalable Enterprise Architecture, leading high-impact teams, Full-Stack Development, Microservices and Machine Learning.

**Hanumantappa Budihal**  
Hanumantappa Budihal is the Chief Information Officer and Solutions Architect at HugoByte AI Labs. He has worked for 4 years as an Application Developer and Azure DevOps Engineer. He is adept at designing, describing and managing the solution engineering for specific business problems by finding the best tech solution by analysing all possibilities. He is proficient in defining features, phases, and solution requirements. He is currently invested in decentralising the blockchain space and is working on the enhancement of the Blockchain Transmission Protocol to achieve it. 

His technical skills include ML, AI ,Blockchain, .NET Core Framework, Azure DevOps, SQL Developer, ASP .NET MVC, REST Web API, WPF, Microsoft Azure, Cognitive Services, Algorithms Design for a complex business requirement, and Watson Discovery, with good knowledge of Application Architecture and Design pattern implementation and data analysis skills. He has also worked on cognitive application development using various IBM Bluemix services such as Conversation, Natural language understanding, Watson discovery, and has developed chatbots using Api.ai and Microsoft bot framework. As a testimony to his exemplary technical skills, he is now pursuing his MTech in computer science at IIT Madras.

**Shreyas Kura Subramanya**  
Shreyas is an experienced software developer with great zeal in implementing solutions in the software domain. He is skilled in Blockchain, smart contracts, ethical hacking, RUST and GOlang. He currently is the Development Tech Lead at HugoByte AI Labs and is instrumental in driving the team to great success. He obtained his Bachelor's degree focused in Computer Science from Bapuji Institute of Engineering & Technology, Davanagere. 
 
 
### Team Code Repos
Source codes will reside in
* https://github.com/hugobyte

Repos for further reference
* https://github.com/MuhammedIrfan
* https://github.com/HanumantappaBudihal  
* https://github.com/shreyasbhat0

### Team Profiles
* Muhammed Irfan K - https://www.linkedin.com/in/muhammed-irfan-k  
* Hanumantappa Budihal - https://www.linkedin.com/in/hanumantappa-budihal/  
* Shreyas Kura Subramanya - https://www.linkedin.com/in/shreyas-ks/

## Development Roadmap :nut_and_bolt: 

### Overview
* **Description** Development of Project Aurras - MVP - Phase 2
* **Total Estimated Duration:** 320 Person Days
* **Full-time equivalent (FTE):**  Milestone 4 - 1.5 ( TODO : Need to edit); Milestone 5 and 6 - 3 (TODO : Need to edit)
* **Total Costs:** 1.16 BTC (TODO : Need to edit)

### Milestone 4 — Workflow Composer - Part 1
* **Estimated Duration:** TODO
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | Apache 2.0  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Composer Configuration Documentation, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests|
| 1a. | Workflow Composer: Rust Openwhisk Client Library | Minimal Implementation to Openwhisk Rust Client |
| 1b. | Workflow Composer: Composer | Wrapper Library to integrate plugging operators and Openwhisk Client |
| 1c. | Workflow Composer: Pipe | Interface to connect other operators and tasks |
| 1d. | Workflow Composer: structured YAML file | A YAML with a predefined structure to configure the workflow composer. |
| 1e. | Workflow Composer: Concat Operator | Operator interface to merge two flows. |
| 1f. | Workflow Composer: Map Operator | Operator to map the inputs to the outputs of each type. |
| 2   | Predefined boiler plate | Predefined Rust code for flow generation. |
| 3a. | Flow Provider for Tackle Box |Create the necessary hooks for the workflow |
| 3b. | Task Provider for Tackle Box | Generate Rust code with structure for the given arguments |
| 3c. | Workflow Provider for Tackle Box  | Interface to connect other operators and tasks |


### Milestone 5 — Workflow Composer - Part 2
* **Estimated Duration:** TODO
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | Apache 2.0  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Operator Documentation, Flow design, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |
| 1a. | Workflow Composer: Flow Macro | To build Rust code with methods for the flow design. |
| 1b. | Workflow Composer: Derive Macro | To build Rust code from the Struct created from the YAML file |


### Milestone 6 — Web API/Backend
* **Estimated Duration:**  TODO
* **FTE:**  
* **Costs:** 

| Number | Deliverable | Specification |
| ------------- | ------------- | ------------- |
| 0a. | License | Apache 2.0  |
| 0b. | Documentation | Documentation includes Inline Code Documentation, Operator Documentation, API doc, Readme file |
| 0c. | Testing Guide | The code will have unit-test coverage (min. 50%) to ensure functionality and robustness. In the guide we will describe how to run these tests |
| 1a. | Web API: Workflow Registration | API Exposed as a part of workflow deployment, Workflow will be registered and made available to specific namespace |
| 1b. | Web API: User Registration | Basic User Registration API to register user to the system |
| 1c. | Web API: User Workflow Management | User to select workflow and provide argument values, Pause Workflow, Delete Workflow |


## Future Plans

We have planned immediate grant as second phase of our development (Draft with Complete deliverables can be found here https://github.com/MuhammedIrfan/Open-Grants-Program/blob/master/applications/project_aurras_mvp.md)

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
