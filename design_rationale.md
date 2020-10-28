[Project Summary](index.md) | [Use Cases](use_cases.md) | [Requirements](requirements.md) | [High-Level Design](high_level_design.md) | [Design Rationale](design_rationale.md) | [Conclusion](conclusion.md)

## Design Rationale

Before getting our heads down and moving forward with any architectural design, we have brainstormed and come up with a number of questions which are crucial to the design direction. Those questions can be classified into two major categories: system architecture and business logics.

### System Architechture Questions

- If we were a real startup tech company, with a limited budget, what is the best software architectural solution for the initial hardware and equipment setup?
- If the business determined that we need to support multiple user platforms, what would be the best design to satisfy such requirements?
- If the business becomes successful and hits the market really well, is the system able to scale big and fast enough to accommodate the increased visiting volume?
- Although this is not a mission critical system, what should we do to ensure the system’s high availability to give the customer a better experience? Since the system is handling customer’s payment information, what should we do to secure customer’s financial information?

### Business Logics Questions

- Who are our target users? What are the most common use case scenarios?
- Are the customers only visiting websites through desktop browsers, or they are also using mobile applications for those use cases? Or if the mobile version can provide more benefits, should we focus more on the mobile applications?
- What is the core value proposition this system provides to our customers compared to other similar applications or websites?
- Is this a customer-centric system in which all the components are designed in such a way that support different function flows to meet customer needs?

### Client-Server Architechture and Multiple-Platform Design

With the aforementioned questions in mind, the architectural design of our hotel booking system is based on the popular client-server architecture that has been adopted by the majority of the modern websites and mobile applications. The decoupled design gives the great flexibility for multiple user platforms. It addresses the question regarding which platform should the system support. Since the server side system provides micro services and APIs for the client side systems to consume, as long as the client side systems are designed to conform with the API standard. Therefore the system allows multiple front-end user platforms, such as web, Android, iOS, or even voice assistant systems like Alexa, Google Home and Siri. However, if this is for a real startup project, the stakeholders don’t have to go all out to implement multiple front-end platforms at the same time. They have the choice to start with only one platform, and gradually expand to other platforms when budget and other resources permitted.

### Client Side System

Despite the fact that the form and appearance of different front-end platforms may vary, they share the same architectural design fundamentally. The client side system includes the main user interface, core function modules, and other system management function modules. It is running on the customer’s machine, i.e. inside the browser for websites, installed as binary code for mobile devices. Customers directly interact with it, but it cannot function by itself unless connected via micro services and APIs to the server side system. The client side system is only responsible for consuming the data passed from the server and presenting the data to the UI in the way that the designer created for the best user experience. It is not responsible for any crucial business logics. Although the binary or the content of the client side code must be encrypted and obfuscated before distributed to the customers, since once the binary or code ships out of the door, it is not under the control of the team anymore, there are still possibilities that it may be decrypted and reverse-engineered by malicious third parties. Storing and using the critical business logics in the client side system is definitely not good practices.  

### Server Side System

The server side system is the crucial component that customers cannot directly interact with and all the business logics happen within. It includes the database module, orchestrator module and other important repositories to connect third party APIs. After authenticated and verified user’s credential, server side system responses to the client side system’s requests and queries. The orchestrator module works as a black box, that client side system may ask data through certain APIs using http request calls, and it returns http responses after process request from the database module and other outside APIs. It encapsulates the business logics within its own boundary and only passes results to the client side system. Searching hotel room availability, making reservations, and confirmation payments are among the most salient function modules which are connected to the outside third party APIs provided by various hotels, platforms and financial institutions. The principle core function is the machine learning module, which is responsible for processing, organizing and sorting the hotel searching results, and passing the result back to the client side system as the recommendation.

### All-in-Cloud

To address the questions regarding the affordability, scalability, availability, and security during the planning phase of the project, the server side system does not reside in any in-house servers physically. The team decides that all-in-cloud is the best solution for addressing those topics.

- Affordability: Using cloud services like AWS, Microsoft Azure, and Google Cloud, can dramatically reduce the initial cost for purchasing, installing and managing the physical servers and other network equipment. Cloud services usually offer the pay-as-you-go payment plans, it is only a fraction of the cost to provision the same size of server instance and databases compared to purchasing those hardwares.
- Scalability: In the event of business expansion, or increased traffic volume, scale up and scale out the cloud services computational instances and resources can be achieved in a matter of minutes, instead of days and months using traditional in-house servers.
- Availability: With properly configured elastic load balancer and failover plans in multiple availability zones for redundancy, the system can be highly available around the world.
- Security: by putting databases and computational instances inside the Virtual Private Cloud with different subnets and virtual gateways, the system can also achieve a high level of data and access security.
