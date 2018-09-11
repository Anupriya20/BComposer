# BComposer

# Hyperledger Composer Introduction:
What is Hyperledger Composer?
•	Hyperledger Composer is a set of collaboration tools for building blockchain business networks.
•	Hyperledger Composer is an extensive, open development toolset and framework to make developing blockchain applications easier.( https://hyperledger.github.io/composer/latest/introduction/introduction.html)
•	Hyperledger Composer enables architects and developers to quickly create "full-stack" blockchain solutions. I.e. business logic that runs on the blockchain, REST APIs that expose the blockchain logic to web or mobile applications, as well as integrating the blockchain with existing enterprise systems of record.
(https://hyperledger.github.io/composer/latest/introduction/solution-architecture.html)

Points to be considered:
•	It make it simple and fast for business owners and developers to create smart contracts and blockchain applications to solve business problems.
•	Build with JavaScript
•	including node.js, npm, CLI and popular editors (vscode),
•	 primary goal is to accelerate time to value
•	Make it easier to integrate your blockchain applications with the existing business systems.
•	Hyperledger Composer supports the existing Hyperledger Fabric blockchain infrastructure and runtime, which supports pluggable blockchain consensus protocols to ensure that transactions are validated according to policy by the designated business network participants.

# Composer Business network include:
Assets: tangible or intangible goods, services, or property (houses and listings)
Transaction: that interact with the assets (buying or selling houses, and creating and closing listings)
Participates: Participants that interact with the business network, each of which can be associated with a unique identity, across multiple business networks.( buyers and homeowners)

# Businnes n/w definition (BND) of composer consist of the below files:

Asset, Transaction and Participants comes under Model file. (.cto)
Transaction func or logic comes in script file. (.js)
ACR comes under Access control file.(.acl)
Query definations comes under Query file.(.qry)

This BND get packaged up into archieve file with .bna extention

# Hyperledger Composer Architecture

Hyperledger Composer is composed of the following high-level components:
•	Execution Runtimes
•	JavaScript SDK
•	Command Line Interface
•	REST Server
•	LoopBack Connector
•	Playground Web User Interface
•	Yeoman code generator
•	VSCode and Atom editor plugins

Execution Runtimes:
Hyperledger Composer has been designed to support different pluggable runtimes, and currently has three runtime implementations:
•	Hyperledger Fabric v1.2: State is stored on the distributed ledger.
•	Web: which executes within a web page, and is used by Playground. State is stored in browser local storage.
•	Embedded component: which executes within a Node.js process, and is used primarily for unit testing business logic. State is stored in an in-memory key-value store.
Connection Profiles:
Connection Profiles are used across Hyperledger Composer to specify how to connect to an execution runtime. There are different configuration options for each type of execution runtime.
For example, the connection profile for a Hyperledger Fabric v1.2 runtime will contain the TCP/IP addresses and ports for the Fabric peers, as well as cryptographic certificates etc.
Connection Profiles are part of Business Network cards.

JavaScript SDK	
The Hyperledger Composer JavaScript SDK is a set of Node.js APIs the enables developers to create applications to manage and interact with deployed business networks.
The APIs are split between two npm modules:
•	composer-client:
1.	Used to submit transactions to a business network 
2.	perform Create, Read, Update, Delete operations on assets and participants

•	composer-admin
1.	used to manage business networks (install, start, upgrade)
JSDocs consists of the above API details
composer-client:
This module would usually be installed as a local dependency of an application. 
It provides the API that is used by business applications to connect to a business network to access assets, participants and submitting transactions. 
In production this is only module that needs to be added as a direct dependency of the application.
composer-admin:
This module would usually be installed as a local dependency of administrative applications. 
This API permits the creation of and deployment of business network definitions.

Command Line Interface
The composer command line tool enables developers and administrators to deploy and managed business network definitions.

REST Server
automatically generates a Open API (Swagger) REST API for a business network. 
(Based on LoopBack technology) converts the Composer model for a business network into an Open API definition, and at runtime implements Create, Read, Update and Delete support for assets and participants and allows transactions to be submitted for processing or retrieved.

LoopBack Connector
The Hyperledger Composer LoopBack Connector is used by the Composer REST Server, however it may also be used standalone by integration tools that support LoopBack natively. 
Alternatively it may be used with the LoopBack tools to create more sophisticated customizations of the REST APIs.

Playground Web User Interface
Hyperledger Composer Playground is a web user interface to define and test business networks. 
It allows a business analyst to quickly import samples and prototype business logic that executes on the Web or Hyperledger Fabric runtime.

Yeoman Code Generators
Hyperledger Composer uses the Open Source Yeoman code generator framework to create skeleton projects:
•	Angular web application
•	Node.js application
•	Skeleton business network

VSCode and Atom Editor Extensions
Hyperledger Composer has community contributed editor extensions for VSCode and Atom. 
The VSCode extension is very powerful and validates Composer model and ACL files, providing syntax highlighting, error detection and snippets support.
The Atom plugin is much more rudimentary and only has basic syntax highlighting.	

# Installing the development environment

Follow these instructions to obtain the Hyperledger Composer development tools (primarily used to createBusiness Networks) and stand up a Hyperledger Fabric (primarily used to run/deploy your Business Networks locally). 
Note that the Business Networks you create can also be deployed to Hyperledger Fabric runtimes in other environments e.g. on a cloud platform.

Installing pre-requisite on Ubuntu:
The following are prerequisites for installing the required development tools:
•	Operating Systems: Ubuntu Linux 14.04 / 16.04 LTS (both 64-bit), or Mac OS 10.12
•	Docker Engine: Version 17.03 or higher
•	Docker-Compose: Version 1.8 or higher
•	Node: 8.9 or higher (note version 9 is not supported)
•	npm: v5.x
•	git: 2.9.x or higher
•	Python: 2.7.x
•	A code editor of your choice, we recommend VSCode.
*Note:
•	Login as a normal user, rather than root.
•	Do not su to root.

# Installing components

1. Install CLI Tool:
Note that you should not use su or sudo for the following npm commands.
a. composer-cli
npm install -g composer-cli@0.20
b. generator-hyperledger-composer
Useful utility for generating application assets:
npm install -g generator-hyperledger-composer@0.20
c. composer-rest-server
Utility for running a REST Server on your machine to expose your business networks as RESTful APIs:
npm install -g composer-rest-server@0.20
d. Yeoman
Yeoman is a tool for generating applications, which utilises generator-hyperledger-composer:
npm install -g yo
	
2. Install Playground:
You can run this locally on your development machine too, giving you a UI for viewing and demonstrating your business networks.
Browser app for simple editing and testing Business Networks:
npm install -g composer-playground@0.20

3. Set up IDE
Install VSCode or Atom

4. Install Hyperledger Fabric
This step gives you a local Hyperledger Fabric runtime to deploy your business networks to.
a. In a directory of your choice (we will assume ~/fabric-dev-servers), get the .tar.gz file that contains the tools to install Hyperledger Fabric:
mkdir ~/fabric-dev-servers && cd ~/fabric-dev-servers
curl -O https://raw.githubusercontent.com/hyperledger/composer-tools/master/packages/fabric-dev-servers/fabric-dev-servers.tar.gz
tar -xvf fabric-dev-servers.tar.gz

b. Use the scripts you just downloaded and extracted to download a local Hyperledger Fabric v1.2 runtime:
cd ~/fabric-dev-servers
export FABRIC_VERSION=hlfv12
./downloadFabric.sh
Start & Stop Hyperledger Fabric
./startFabric.sh
./stopFabric.sh
Created PeerAdmin Card
./createPeerAdminCard.sh

c.
export FABRIC_VERSION=hlfv12
./startFabric.sh
./createPeerAdminCard.sh

5. Start the web app ("Playground"):
    composer-playground
Check:  http://localhost:8080/login
We should see the PeerAdmin@hlfv1 Card you created with the createPeerAdminCard script on your "My Business Networks" screen in the web app: if you don't see this, you may not have correctly started up your runtime!


