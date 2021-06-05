---
layout: post
title:  "Challenges in Developing Microservices"
date:   2019-05-15
categories: [microservices]
---

With **microservices** designing & architecting of application is changed not just implementation but the way you think as a developer, QA & Architect is also changed because with microservices you are building an application which comprises of interconnected small components whereas each component has its own unique responsibilities. Before microservices all the applications are **Monolithic** applications where application is not divided into components but it may contain modules but that are internal to application and those modules are depended on each other.

##### As per my experience following are the challenges you may face while developing application using micro services architecture:

### Security

*More the number of components, more is the chances of chaos & risk*. As stated above in microservices based application multiple components are connected to each other in order to fulfill application use cases. Hence security becomes major concern here. While developing different services you have to make sure that transaction between multiple services are **Secure** and **Reliable**. Now what does secure means? Secure means data between transactions should be encrypted and Service to Service authentication should be enabled. Reliable means? Transaction should be either **committed** or **rollback** i.e. it should not remain in **inconsistent** state. Reliability also means data should not be manipulated between the transactions. Here transaction refers to multiple API call involved in fulfilling application use case.

### Logging

**Logging** becomes critical while debugging issues, If application has well implemented logging then for a developer it becomes fairly easy to debug the issue and find out the root cause but if not then it became a night mare. In case of microservices logging is challenging because here we have multiple components and for single transaction multiple api calls involved from multiple services then how would you trace the issue. In case of Monolithic it is fairly easy as there is only a single source of logs. But in case micro services there are multiple source of logs. To solve this challenge we can use concept of **Trace Id** & **Span Id** to track the transaction & use tools like [**Kibana**](https://www.elastic.co/products/kibana) to visualize logs from single dashboard.

### Decoupling

As mentioned [**here**](https://martinfowler.com/articles/microservices.html) as per **Martin Fowler** "microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API". This small services should be developed in such as way that each service represents unique functionality and should be independent to each other. Why we want **Decoupling** ? If services are dependent on each other then it becomes difficult to **upgrade** any service independently then what is the use of micro services. lets take an example we are developing a micro service based application and after moving into production we got a issue which involved changes only in one service then it would be better to roll out the new release for that service instead of rolling out a new release or fix pack for complete application.

### Testing

**Unit** Tests, **Performance** Tests, **Manual** Tests, **API** Tests & **Automation** Tests are common for both monolithic & microservices based applications but in case of microservices we have to write other forms of tests as well which are **Integration** Tests & **Service to Service** communication tests. Integration Tests may or may not be require in both Monolithic & micro services as it depends whether your application is integrated with any other application or not but Service to Service communication tests plays crucial role in micro services based application as there are lot of interaction happens betwen multiple services even for a single transaction. **Contract** based tests should be written in this case so that one service should not break contract with other service.

This are some of the challenges I faced while implementing micro services.

### Support Me

You can support my work through the following If you find it useful:

- [Buy me a coffee](https://www.buymeacoffee.com/sagarjadhv23)
- Tweet me [@sagarjadhv23](https://twitter.com/sagarjadhv23)

### Feedback

Report an issue [here](https://github.com/developersthought/roadmap/issues/new) If you find a bug or want to improve the content.
