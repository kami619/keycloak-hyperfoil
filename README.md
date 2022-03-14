# keycloak-hyperfoil
This is a proof of concept for Hyperfoil load testing tool with Keycloak as the Application Under Test.

Scenario: A Basic scenario of Keycloak application, where users from various realms, login and logout of the application.

### Key Indicators of the Tool:

#### Ability to run in a distributed mode

Yes, hyperfoil tool is natively run in controller and agent verticles, which is designed to be run in a distributed mode
Usefulness of test reports and reported statistics

#### The reports sections are detailed but seems to be little raw and lacks the UX some of the other tools such as Gatling provide
Also the information seems to be splintered and the graphs and tables could be swapped in their current positions to be able to assist better with performance result analysis
The stats themselves are useful and specific to each resource thats fetched in addition to the API requests, which is unique to this tool

#### Ability to define test assertions based on measured statistics (for example Gatling allows to define quite sophisticated assertions)

We can perform assertion per request, but I didn't find references to perform assertions at global benchmark/scenario level and also other forms of error count based validations

#### Ability to export test data into external data sources (DB, influx, elastic, etc.), that would allow for easier comparison of performance results across multiple version of the product

Hyperfoil currently generates results in an html file
Hyperfoil currently exports results in a raw json format, but I didn't find any reference to write it to a time-series/transaction db. However the json schema seems easy enough to be parsed and fed to a db with a custom post processing script

#### How to run a stress test. I.e. how to find the maximum performance of the system with a particular test scenario.

As the test execution is done via a cli tool, we can look at ways to automate the options for this and externalize the parameters specified within the yaml file, but I didnt find anything which is out of the box to perform such activity

#### Result evaluation on-the-fly during a single test run:

We can look at some live metrics using the Hyperfoil shell using cli.sh script, which gives you status about the current sessions, connections, run stats at a high level during the test


### Things that could be better: 

The examples from here, https://hyperfoil.io/userguide/examples.html are little overwhelming, as a lot of stuff is crammed into one big scenario 
I didn't find the docs to be adequate enough to follow along for a real life chaining of API requests scenario (Keycloak Login Flow from existing benchmark scripts) without having to re-read the examples and check with the Author of the tool.
Paradigm shift needed to be able to code at a comfortable pace in yml syntax, as its new DSL and the way we write custom logic would also be different to regular IDE based development (java, Scala, python etc.,) 
Almost no community support like other performance benchmark tools (Gatling, k6), little to no mention on stack overflow, Reddit or google search results in general, so we would be the first to hit issues, potentially slowing things down and increased debug and development times with the scripts

### Things that are great about the tool

I liked the readability portion of the yml syntax, it takes lesser effort to understand whats going on in the scenario, as the DSL is relatively self-explanatory. But would need to understand typical terms which are specific to the Hyperfoil DSL such as `metric`, `sequence`, `processor` etc.,
It enables us to create faster and distributed load scripts which are native to open-shift Eco-system.
Given it follows similar Service Loader and Service Provider concepts to build our own extensions akin to Keycloak, it would have more flexibility to do things from that stand point than simply relying on the yml based scripting approach (but that means more effort to build the base framework)
The fact that Hyperfoil is a home grown product, we would have exclusive access to requesting new features and improvements and potential customization and extensions to the tool.
