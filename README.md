Update your corda project jars with new jars. 

Steps 1 :- 
Download latest bootstrapped jar https://software.r3.com/artifactory/corda-releases/net/corda/corda-tools-network-bootstrapper/4.4/

Step 2:- 
Suppose your old project has following flows

    com.template.flows.Initiator
    net.corda.core.flows.ContractUpgradeFlow$Authorise
    net.corda.core.flows.ContractUpgradeFlow$Deauthorise
    net.corda.core.flows.ContractUpgradeFlow$Initiate


Step 3:- 
Suppose you have new flows like  

    Mon May 25 14:26:30 IST 2020>>> flow list
    com.template.flows.Initiator
    com.template.flows.test
    net.corda.core.flows.ContractUpgradeFlow$Authorise
    net.corda.core.flows.ContractUpgradeFlow$Deauthorise
    net.corda.core.flows.ContractUpgradeFlow$Initiate

Now you can use the command java -jar network-bootstrapper-4.4.jar --dir <nodes-root-dir> to update your Project with new jars

Project Before 

    .
    ├── notary
    │   ├── node.conf
    │   ├── network-parameters
    │   └── cordapps
    │       └── cordapp-a.jar
    ├── partya
    │   ├── node.conf
    │   ├── network-parameters
    │   └── cordapps
    │       └── cordapp-a.jar
    ├── partyb
    │   ├── node.conf
    │   ├── network-parameters
    │   └── cordapps
        │       └── cordapp-a.jar
    └── cordapp-b.jar               // The new cordapp to add to the existing nodes

Step 4:- 
   java -jar network-bootstrapper-4.4.jar --copy-cordapps Yes --dir //pathhereto nodebuild

Step 5:- 

    .
    ├── notary
    │   ├── node.conf
    │   ├── network-parameters      // The contracts from cordapp-b are appended to the whitelist in network-parameters
    │   └── cordapps
    │       ├── cordapp-a.jar
    │       └── cordapp-b.jar       // The updated cordapp is placed in the nodes cordapp directory
    ├── partya
    │   ├── node.conf
    │   ├── network-parameters      // The contracts from cordapp-b are appended to the whitelist in network-parameters
        │   └── cordapps
    │       ├── cordapp-a.jar
    │       └── cordapp-b.jar       // The updated cordapp is placed in the nodes cordapp directory
    └── partyb
    ├── node.conf
    ├── network-parameters      // The contracts from cordapp-b are appended to the whitelist in network-parameters
    └── cordapps
        ├── cordapp-a.jar
        └── cordapp-b.jar       // The updated cordapp is placed in the nodes cordapp directory
        
        
 Run the netwrok again. You got new flows    
