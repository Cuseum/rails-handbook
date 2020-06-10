## Starting a new project

When you're starting a new project, there are a few things you need to do:

#### 1. Open a repository

Ask your team lead or DevOps to open a repository.

#### 2. Fill out Project setup sheet

We've come up with a project setup template in cooperation with DevOps team. It's purpose is to provide the DevOps with all the details needed for deploying your application to staging and production servers.

It contains general info about your project that your project manager can fill out as well as more technical information like frameworks and technologies used, build and deploy setup, third party services that need to be set up...

Ask your PM for a link to the sheet template.

**Fill in the blanks on Backend related stuff.**

If you need any other services that aren't mentioned, **provide as many information as possible**

**Project setup sheet needs to be up to date** with new changes to project setup and services used. If you're adding some new dependency or service or changing something, please update it in project setup sheet and notify DevOps to make these changes.


#### 3. Generate new application

Use [**default rails template**](https://github.com/infinum/default_rails_template/) to start your new application.

Most of our work is based on the Rails framework. We have some standard configurations and gems that are basically in every Rails application. To make our lives easier, we've made a default template to generate new Rails applications that meet those standards.


#### 4. Check for new/better gems

We usually use specific gems for some purposes, e.g. Devise for authentication, Pundit for authorization... That doesn't mean we necessarily need to use those gems.

When adding a gem to your application, check if there's some new and better gem for that purpose.

When checking out a gem, always look for these things:
* is the gem maintained? when was the last commit?
* how many stars does it have?
* what is the ratio between open and closed issues?


#### 5. Fill out readme

After setting up a project, fill out a readme file with all the necessary details about the application:
* dependencies & prerequisites
* setup instructions
* development instructions
* deployment instructions
* test instructions
* any other project specific information that someone who takes over a project needs to know


#### 6. Create ER diagram

Before you start coding, you always need to create an ER diagram for your database. Go through project specification and list all the entities needed together with their attributes and relationships between them.

For creating an ER diagram use:
* [DB diagram](https://dbdiagram.io/)
* [MySQL Workbench](https://dev.mysql.com/downloads/workbench/)

After creating an ER diagram, you need to go through architecture review. You can read more about it in [Architecture review chapter](Architecture review)

If you need to create an application or server architecture diagram use:
* [Gliffy](https://www.gliffy.com/)

If you need to create a sequence diagram use:
* [Web Sequence Diagram](https://www.websequencediagrams.com/)
