# STEPS FOR CREATING THE COMPOSER APP THROUGH UBUNTU

# Prerequisites:

Please follow the README.md steps for Ubuntu

# Step One: Creating a business network structure

The key concept for is the business network definition (BND). It defines the data model, transaction logic and access control rules for your blockchain solution. To create a BND, we need to create a suitable project structure on disk.

The easiest way to get started is to use the Yeoman generator to create a skeleton business network. This will create a directory containing all of the components of a business network.

1.	Create a skeleton business network using Yeoman. This command will require a business network name, description, author name, author email address, license selection and namespace.

Do not run the command using root 

yo hyperledger-composer:businessnetwork

2.	Enter tutorial-network for the network name, and desired information for description, author name, and author email.

3.	Select Apache-2.0 as the license.

4.	Select org.example.mynetwork as the namespace.

5.	Select No when asked whether to generate an empty network or not.

# Step Two: Defining a business network

A business network is made up of assets, participants, transactions, access control rules, and optionally events and queries.
In the skeleton business network created in the previous steps, there is a model (.cto) file which will contain the class definitions for all assets, participants, and transactions in the business network.
 The skeleton business network also contains an access control (permissions.acl) document with basic access control rules, 
a script (logic.js) file containing transaction processor functions
a package.json file containing business network metadata.
Modelling assets, participants, and transactions
The first document to update is the model (.cto) file. This file is written using the Hyperledger Composer Modelling Language. The model file contains the definitions of each class of asset, transaction, participant, and event. It implicitly extends the Hyperledger Composer System Model described in the modelling language documentation.

# Step Three: Generate a business network archive

Now that the business network has been defined, it must be packaged into a deployable business network archive (.bna) file.
1.	Using the command line, navigate to the tutorial-network directory.
2.	From the tutorial-network directory, run the following command
3.	composer archive create -t dir -n .

# Step Four: Deploying the business network

After creating the .bna file, the business network can be deployed to the instance of Hyperledger Fabric. Normally, information from the Fabric administrator is required to create a PeerAdmin identity, with privileges to deploy chaincode to the peer. However, as part of the development environment installation, a PeerAdminidentity has been created already.
After the runtime has been installed, a business network can be deployed to the peer. For best practice, a new identity should be created to administrate the business network after deployment. This identity is referred to as a network admin.
A PeerAdmin business network card with the correct credentials is already created as part of development environment installation.
Deploying the business network
Deploying a business network to the Hyperledger Fabric requires the Hyperledger Composer business network to be installed on the peer, then the business network can be started, and a new participant, identity, and associated card must be created to be the network administrator. Finally, the network administrator business network card must be imported for use, and the network can then be pinged to check it is responding.

1.	To install the business network, from the tutorial-network directory, run the following command:

composer network install --card PeerAdmin@hlfv1 --archiveFile tutorial-network@0.0.1.bna

ex:
ubuntu@ip-172-16-1-181:~/fabric-dev-servers/tutorial-network$ sudo composer network install --card PeerAdmin@hlfv1 --archiveFile tutorial-network@0.0.1.bna

The composer network install command requires a PeerAdmin business network card (in this case one has been created and imported in advance), and the the file path of the .bna which defines the business network.

2.	To start the business network, run the following command:

composer network start --networkName tutorial-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

ex:
ubuntu@ip-172-16-1-181:~/fabric-dev-servers/tutorial-network$ sudo composer network start --networkName tutorial-network --networkVersion 0.0.1 --networkAdmin admin --networkAdminEnrollSecret adminpw --card PeerAdmin@hlfv1 --file networkadmin.card

The composer network start command requires a business network card, as well as the name of the admin identity for the business network, the name and version of the business network and the name of the file to be created ready to import as a business network card.

3.	To import the network administrator identity as a usable business network card, run the following command:

composer card import --file networkadmin.card

The composer card import command requires the filename specified in composer network start to create a card.

4.	To check that the business network has been deployed successfully, run the following command to ping the network:

composer network ping --card admin@tutorial-network

ex:
root@ip-172-16-1-181:/home/ubuntu/fabric-dev-servers/tutorial-network# composer network ping --card admin@tutorial-network

The composer network ping command requires a business network card to identify the network to ping.

# Step Five: Generating a REST server

Hyperledger Composer can generate a bespoke REST API based on a business network. For developing a web application, the REST API provides a useful layer of language-neutral abstraction.

1.	To create the REST API, navigate to the tutorial-network directory and run the following command:

composer-rest-server

2.	Enter admin@tutorial-network as the card name.

3.	Select never use namespaces when asked whether to use namespaces in the generated API.

4.	Select No when asked whether to secure the generated API.

5.	Select Yes when asked whether to enable event publication.

6.	Select No when asked whether to enable TLS security.

The generated API is connected to the deployed blockchain and business network.

# Step Six: Generating an application

Hyperledger Composer can also generate an Angular 4 application running against the REST API.
1.	To create your Angular 4 application, navigate to tutorial-network directory and run the following command:

yo hyperledger-composer:angular

2.	Select Yes when asked to connect to running business network.

3.	Enter standard package.json questions (project name, description, author name, author email, license)

4.	Enter admin@tutorial-network for the business network card.

5.	Select Connect to an existing REST API

6.	Enter http://localhost for the REST server address.

7.	Enter 3000 for server port.

8.	Select Namespaces are not used

The Angular generator will then create the scaffolding for the project and install all dependencies. To run the application, navigate to your angular project directory and run npm start . This will fire up an Angular 4 application running against your REST API at http://localhost:4200 

