#  Last Project Description
<hr>

## Development


In the last 5 years we were working on a team which was in charge with moving the old monolithic backend of an application developed in **C/C++** to a more up to date technology which facilitates also a faster and safer updates deployment as well as a possibility to implement the continuous integration paradigm for the application. 

The old system was split in about a dozen components which were redesigned following a micro-services architecture. The time critical components were kept written in native code and modified to use the **RabitMQ** communication model which was adopted for internal backend communication.

However, most of the components were rewritten in python and **javascript (node.js)**. For internal backend communication was used RabitMQ. For interface with 3rd party backend components **REST API** which on node.js comes native (express) and on **Python** was used **Flask** with several extensions:
- **RESTful** for data interface
- **JWT** for authentication
- **Jinja2** for basic formatted HTML responses
- **Django** for more complex  HTML responses (e.g. dynamic reports )
- **SQLAlchemy** for interfacing with the **sqlite**
- **MongoDB** for interfacing with **mongo db** databases

The UI of the old system was implemented using **WPF** under Windows. Another reason for modernising the old system was to achieve the UI platform independence. One of the backend services developed in **node.js** was put in charge of serving the UI to the client applications/browsers. The main technology used was **AngularJS**. Two other micro-services which could be called also sub-applications because they are more or less independent from the main application had the UI implemented in **React**.

**React** component/sub-applications state has been implemented with **Redux** to serve as a centralized store used across many parts of application. Using Redux the state of the application was kept updated in a predictable fashion. React app backend was implemented in python/Django with embedded ORM on top on **POSTGRESQL** database. Also, the communication with a 3rd party component was implemented with gRPC framework because provides greater performance (faster and more robust, as it defines a specific set of rules each request and response should adhere to) at the expense of less flexibility, using the advantages of protobufers. **Protobuf** is faster than other serialization techniques and schemas are encoded along with data; it ensures that signals don't get lost between applications.

In order to migrate to the new WEB based system, the WPF app used a browser control which render **AngularJS** and **React** apps in separate WPF tabs/views. Also, the communication between Nodejs backed and WPF app was implemented through **WCF services** hosted by windows app so all the http requests were fully sent back and forth between old and new app.

##Testing

Unit tests for Nodejs backend were implemented with Jasmine framework especially for driven development focused with descriptive syntax.

Deployment:
Since one of the most important requirement of the system is that it should be hosted on a real hardware on the custoemer premisses the docker technology was choosen to deploy the application and its services. Once the application complexity increased and the number of services grew up the the deplo was switch to docker-compose and the cofigurations were provided as yaml files.