---
layout: post
title:  "Automatic Test"
date:   2020-09-22 20:13:07 +0800
categories: pcloud
---

# Tools:

* Node.js: Mocha
* Ruby on Rails: Cucumber, Rspec
* Frontend: Capybara, Selenium
* Version control: Git, Gitflow
* CI(Continuous Integration): Gitlab-CI, Travis-CI, Circle-CI, Jenkins

    [Travis CI Example](https://travis-ci.org/github/calvinchu8172/pcloud-portal-dockerize/builds/653035120)

* CD(Continuous Deployment): Docker, Kubernetes, AWS ElasticBeanstalk
* TDD and BDD
* Test Driven Development to Deployment Flow:

    ![CI CD]({% link /assets/automatic-test/ci-cd-flow.png %})


# Compare TDD and BDD

|             | TDD(Test Driven Development)   | BDD(Behavior Driven Development)  |
|Definition   | TDD is a development technique that focuses more on the implementation of a feature, function or method| BDD is a development technique that focuses on the system’s behavior, like user flow or response of API |
|Participants  | Developer |  Developer, PM, QA, Customers |
|Language used     | Coding language, NodeJS, Ruby... | Natual language, English, Mandarin... |
|Main Focus| Unit Test|Understanding Requirements|
|Tools used| Rspec, Mocha| Cucumber|

* Automatic test tools like Cucumber and Mocha can produce a test report.

    [Test Report]({% link /assets/automatic-test/report.html %})



