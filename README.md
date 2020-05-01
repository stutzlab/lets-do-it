# lets-do-it
See here the practices and behaviors we employ at creating things

Join us and improve those practices by experience...

## For Developers


### People - who does

The core development orbits around:

* A **Client** that is someone that needs the software for doing his things, normally for helping other people
* A **Technical Leader** is a programmer who talks to architects/specialists to define architecture, prioritize issues, reviews Merge/Pull Requests and acts like a Scrum Master when needed for helping programmers do their job. Development decisions go here. Lots of communication with programmers must occur here.
* A **Programmer** (backend/ui/datascientist/infrastructure etc), that does most of the hard work
* A **Tester** which helps the developer to certify the software, normally when the software is already running on staging server
* A **Infrastructure Guy** who is concerned about runtime costs, cloud engineering, monitoring and platform availability


### Backlog - things to do

For describing the **backlog** of a project, we use **Issues/Milestones** from Github or Gilab both for public and private projects.

**Milestones** indicates what must be delivered when and normally is where we anchor a public or internal contract with who is paying the bills. Milestones are important because it is a means of communication to people outside the project. Without milestones it is hard to explain to someone what is being done, what will be delivered when and what are the priorities when you have dozens of open issues!

Please take a look at https://guides.github.com/features/issues/

### Codebase - things done

During development we use **Git** and adopt the **Gitflow** way for doing **commits/branching/tagging**.
Take a time and read https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow carefully.

#### Build/Release repositories

There is a great difference between the software component itself and its instantiation on diverse infrastructures, but both has something in common: they can both be code in Git. So all our deployments are done by scripts, normally using a docker-compose.yml file for describing environment variables, passwords, tunabble configurations and so on.

Always try to represent everything a software needs to be run in the repository. Deployment has bugs, enhancements, discussions and releases as a regular software component has, so use Git there!

As a practise we differentiate Software Components in **/build** groups and deployment scripts etc in **/release** groups in Gitlab. For example, a web site may use the following projects structure

* **/mygreatsite/build/hotpage** - a repo with some pages which runs a simple http server with html pages - normally the application developer spends most part of his time doing work here

* **/mygreatsite/release/hotpage-vpsdime-stage** - an instantiation of the site which references the built Docker Image during "build" and serves pages at http://stage.mysite.com

* **/mygreatsite/release/hotpage-aws-prod** - an instantiation of the site which references the same built Docker Image during "build" and is serves pages at http://www.mysite.com


#### Readme everywhere - documentation may be loosy too

It is part of the developer job to document, implement and test technical things so that other developers know how to collaborate in a project without too much burden.

Do you have a certain POSTMAN file, or and tricky command line that you used during development for testing parts of the software? Probably other developers would like to have access to this line too. A great place to put those things is in the README.md file inside the Git repository itself. Be a friend of other developers! You don't have to wait until having a component of great documentation about something. Use the README as the place for storing even loosy or incomplete commands that you use. It is better than nothing.


### Typical Workflow - putting all together

1. A client needs something and someone thinks about a product that could solve that problem
2. What have to be done is written and discussed in **Issues**
3. According to the client perspective, we define a **Milestone** and associate issues that will be prioritized. All others issues won't be done.
4. So the Milestone work starts...
5. The Technical Leader will communicate the architecture to other programmers by documenting it in a README.md
6. The Technical Leader will mark the next issues to be done with label "TODO"
7. The Programmer will get any issues marked with "TODO" and develop in a feature branch with the name of the issue (see Gitflow)
  * If the programmer need any help (help coding, help deciding, help explaning), ask for help in comments. Mention who you think would better help you.
8. Commits in this branch must have a reference to the issue being developed in commit log. Ex.: "#closes 24"
  * During your work, comment the issue your are working on with "/spend 30min" etc so that you will get paid ;)
9. After finished the issue development, send a Merge/Pull Request to the "develop" branch with label "Review" so the Technical Leader or someone he asks to will review the code, preferably run it locally and accept the new code
 * If there are any doubts or requests to the programmer use comments in Merge/Pull Request and apply the label "TODO"
 * MR/PR will be closed and the feature branch will be removed after it is accepted
 * After accepting MR/PR, the Technical Leader must change the label of the refered issue to "Test"
10. A tester will look for issues marked with "Test" and test them in a stage server
  * normally the team will have a automatic CI/CD environment setup for that
  * when finding an error, comment about the error, take print screens showing details about the context the error ocurred and change the label of the issue to "TODO" so that the programmer will take a look
  * if you think something is strange here, ask people to use it in staging
11. After all tests are passed and you have a stable code running, the Technical Leader will release the software by merging it to the "master" branch and running it in production
  * planning is needed here when real customers are using your software to avoid blackouts
  * release the software for partial users and monitor logs
  * plan and do "production tests" being near real users and hearing/taking to them

**TL/DR**:
* Technical Leaders will check for Issues and MR/PR with labels "Review"
* Programmers will check for Issues and MR/PR with labels "TODO"
* Testers will check for Issues marked with "Test"
* Everyone will communicate mainly using comments and mentions on Issues and MR/PR
* Everyone will continuously check and communicate if something seems out of order to help one another
* If the project is too simple, some of the practices above may be skipped, but the communication must still work well

### Typical Architecture/Engineering Guidances

* Microservices
 * one microservice may have several containers
 * database is part of the microservice
 * the microservice talks to one another mainly using REST interfaces (Kafka interfaces or other means may be used, but must be stable and documented)
 * Keep the containers as small as feasible for good testing
 * https://martinfowler.com/articles/microservices.html
* Docker 99.9% of the time - for development, staging, production
 * Check https://github.com/flaviostutz/docker-manifest for best practices using Docker
* Docker Swarm for Container Clusters
* Always Web/Internet/Cloud protocols based
* Golang/NodeJS for Backend
* React Native iOS/Android/Web for Frontend
* MQTT for async UI interconnections
* Kafka for async messaging between server nodes
* Jupyter Python for low scale or exploratory datascience/ML
* Spark Scala/HDFS for high scale production datascience/ML
* InfluxDB for TSDB
* Grafana for monitoring infrastructure/business panels
* Prometheus for microservices monitoring
* MySQL/PostgreSQL for relational database
* Check for some tools/pocs/components as example at http://github.com/flaviostutz and http://github.com/tiagostutz
