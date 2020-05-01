# lets-do-it
See here the practices and behaviors we employ at creating things

Join us and improve those practises by work!

## For Developers

### Backlog - things to do!

For describing the **backlog** of a project, we use **Issues/Milestones** from Github or Gilab both for public and private projects.

**Milestones** indicates what must be delivered when and normally is where we anchor a public or internal contract with who is paying the bills. Milestones are important because it is a means of communication to people outside the project. Without milestone it is hard to explain to someone what is being done and what are the priorities when you have dozens of open issues in a lake!

Please take a look at https://guides.github.com/features/issues/.

#### Typical flow

The core development orbits around:

* A **Client** that is someone that needs the software for doing his things, normally for helping other people
* A **Programmer** (backend/ui/datascientist/infrastructure etc), that does most of the hard work
* A **Technical Coordinator** who talks to architects/specialists to define architecture, prioritize issues, reviews Merge/Pull Requests and acts like a Scrum Master when needed for helping programmers do their job. Development decisions go here. Lots of communication with programmers must occur here.
* A **Tester** which helps the developer to certify the software, normally when the software is already running on staging server
* A **Infrastructure Guy** which is concerned about runtime costs, cloud engineering, monitoring and platform availability

### Codebase - things done!

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



