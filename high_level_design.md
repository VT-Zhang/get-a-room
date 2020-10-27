[Project Summary](index.md) | [Use Cases](use_cases.md) | [Requirements](requirements.md) | [Design Rationale](design_rationale.md) | [High-Level Design](high_level_design.md) | [Conclusion](conclusion.md)

## High-Level Design

![project_structure](https://user-images.githubusercontent.com/24898162/95663810-2dc1f400-0b10-11eb-8895-3442f89bb910.png)

In this section, we will introduce each core module's fuction, flow as well as illustrate the UML diagram for main variables and methods inside each class. As mentioned before, with the decoupled design, the client side system does not contain any core business logics. It only interacts with the user and visually presents the data passed from the server side system. Therefore, the main focus of this section is on the core modules of the server side system.

## 1. The Happy Path Flow

![Happy_Path_Flow_Chart](https://user-images.githubusercontent.com/24898162/95685389-94edb000-0bc5-11eb-9427-1003c1e89001.jpg)

The following is the “Happy Path” flow of our “get-a-room” online hotel booking system. "Happy Path" is a default scenario featuring no exceptions or error conditions occured during the complete end-to-end flow.

1. User logs on to the system by entering appropriate credentials to the **Authentication** module.
2. User interacts with the **Main Interface**.
3. User chooses the **Search Hotels** module by entering search criteria, i.e. date, address, zip code, star of the hotel, and price preferences.
4. **Hotel Search Engine** module from the server side system receives the search criteria and forwards the search request to an array of external hotels and platforms APIs.
5. Upon gathering a list of available hotels per the search criteria, the **Hotel Search Engine** module hands the raw list over to the **Machine Learning Engine** module.
6. **Machine Learning Engine** processes, optimizes and reorganizes the raw list and returns the hotel search results back to the client side system.
7. **Recommendation** module of the client side system presents and displays the search results to the user.
8. User picks one hotel from the results that best fits his/her preference and criteria.
9. User is prompted with the **Payment** module, and enters the payment information.
10. **Payment Process Service** of the server side system connects to external APIs from banks or financial institutions for processing payments.
11. Upon payment is confirmed, **Reservation Process Service** calls the selected hotel's API and confirms the booking with the payment verification.
12. Once the reservation is confirmed by the hotel API, **Reservation Process Service** sends the results back to the client side system.
13. User receives the payment and hotel reservation confirmation.
14. User may choose to go to the **Itinerary Management** module to manage the trip or go to the **Main Interface** to interact with other function modules.

## 2. Orchestrator Module

The **Orchestrator** module is one of the most important modules of the system. It works as the centralized relay hub for passing HTTP requests of various modules from client side system to the target micro services and APIs endpoints of the server side system, and returns the HTTP responses with payload data from the server side system back to the client side system. It authorizes and authenticates each and every service call by checking the HTTP header and session token to ensure that the client who initiates the request is a legitimate user and has appropriate level of authorizations. And it also defends and filters DDOS attacks and botnet calls ensuring only human-initiated service requests can reach the target micro services and APIs. The Orchestrator design provide benefits for the following quality attributes from McCall's quality list:

- Flexbility: Flexbility is the effort required to modify an existing system. In this case, adding an additional funtional module to the server side system is extremely easy and effortless. Because all the micro services are connected the Orchestrator hub, and the interface is universally formated - HTTP protocal and JSON format payload. As long as the client side module is designed per the API contract specification.
- Interoperability: Interoperability is the effort required to couple one system to another. At the beginning, the system maybe only support one client side system, say website, to consume the mirco services and data provided by the server side modules through the Orchestrator. Again, no matter what form of the client side system appears, web, Android, iOS or even voice assistant, as long as the client side systems are designed per API contract, they are able to consume the data from the server side system. Adding another client side system requires very low modification of the server side system.

## 3. Hotel Search Engine Module

The **Hotel Search Engine** module of the server side system is one of the core functions of application. It is responsible to collect the research queries sent from the Hotel Seach module of the client side system. Upon received the search queries, it checks the similar cached entries from the database. If the similar queries do not exist, it sends out HTTP requests to an array of external hotels and other trip managing company APIs to further query the desired results. Finally when all the responses come back from those third party APIs, the Search Engine conglomerates and organizes the results as a list and passes down to the Machine Learning Engine to further process and optimize.

The caching mechanism of the Hotel Search Engine is a special module to increase user searching experiences. It takes time for all the requests and reponses going to and coming back from those external hotel and platform APIs, since they are not under control of our own hands. The Cache module saves the most searched criteria for a given period. When the new search queries come from the client side system, the Search Engine looks into the Cache module first. If it is a hit, the Search Engine skips the external search and forwards the results immediately to the Machine Learning Engine. If it is a miss, the Search Engine then goes out to the external APIs for further search. This caching mechanism greatly boosts the search efficiency and reduces the average wait time for external APIs queries.

<img src="https://user-images.githubusercontent.com/24898162/96627794-6071a680-12df-11eb-8b2d-177e65c196d0.png" width="600">

## 4. Machine Learning Engine Module

The **Machine Learning Engine** module of the server side system and the Recommendation module of the client side system together provide the unique feature and design of our hotel booking system and differentiates from the rest of the crowd. Essentially, the Machine Learning Engine is building on top of the well-trained neural network classifier models which takes the input variables like date, address, zip code, star of the hotel preference, customer price preference, previous search and confirmed trip results, and hotel discount and promotion information etc. It processes, optimizes and reorganizes the raw hotel list passed from the Hotel Search Engine. Then the sorted and reorganized list of hotels search result is sent back to the Recommendation module of the client side system for customer to view and choose from. The optimized search results put the recommended hotels on the first page or on top of the list, therefore making them more visible and easier been selected as the result. It benefits all the parties involved in this activity, customers enjoy the best hotel prices and intelligent search and booking experience, hotels with higher room inventory and provides great rates can promote a wider exposure, and eventually since our booking system  brings value to both our customers and vendors, it becomes a profitable and sustainable business.

- ### Neural Network Schema Model
![Machine_Learning_Schema](https://user-images.githubusercontent.com/24898162/96504867-54281380-1223-11eb-910d-074890128183.png)

<img src="https://user-images.githubusercontent.com/24898162/96629821-248c1080-12e2-11eb-9ffe-dd4230066085.png" width="800">

## 5. Payment Process Service Module

The **Payment Process Service** module of the server side system stores, processes, relays and confirms payment information remitted from the client side Payment module and forward the payment to the external payment processing entities' APIs, like major banks or other financial institutions. Once the customer chooses a desired hotel to book, the Payment module of the client system takes the customer's payment information, and passes to this Payment Process Service module. It first validates and verifies the paymant information, and then it encrypts the data before the payment remission is sent out. After the payment is accepted by the external vendors, it relays the payment success confirmation message to the Reservation Processing Service. Otherwise it returns the error message back to the client side Payment module to inform the customer the payment processing is not successful.

<img src="https://user-images.githubusercontent.com/24898162/96635645-2063f100-12ea-11eb-8f09-7516dc0d72aa.png" width="700">

## 6. Reservation Process Service Module

The **Revervation Process Service** module serves as the final section of the booking flow. When the payment confirmation passed from the Paymen Process Service module, it carries the confirmed payment data payload along with other necessary booking information and sends the HTTP request to the selected hotel APIs for the final reservation confirmation. Once the hotel API returns the acknowledgement of the reservation, this module saves the reservation data to the database and forwards the response back to the client side system to let the custom know reservation is successful.

<img src="https://user-images.githubusercontent.com/24898162/96667915-fd583200-1327-11eb-9f4c-1abbee082ea8.png" width="700">

## 7. Traceability Matrix

### Functional Requirements

| #####     | Authentication | Itinerary Management | Search Hotels | Hotel Search Engine | Machine Learning Engine | Recommendation | Payment | Payment Processing Service | Reservation Processing Service | Database |
|-----------|:--------------:|:--------------------:|:-------------:|:-------------------:|:-----------------------:|:--------------:|:-------:|:--------------------------:|:------------------------------:|:--------:|
| **FR-1**  |        X       |                      |               |                     |                         |                |         |                            |                                |     X    |
| **FR-2**  |        X       |                      |               |                     |                         |                |         |                            |                                |     X    |
| **FR-3**  |                |           X          |       X       |          X          |                         |        X       |         |                            |                                |     X    |
| **FR-4**  |                |           X          |               |                     |                         |                |         |                            |                                |     X    |
| **FR-5**  |                |           X          |               |                     |                         |                |         |                            |                                |     X    |
| **FR-6**  |                |           X          |               |                     |                         |                |         |                            |                                |     X    |
| **FR-7**  |                |                      |               |                     |                         |                |    X    |              X             |                                |          |
| **FR-8**  |                |           X          |               |                     |                         |                |         |                            |                X               |          |
| **FR-9**  |                |           X          |               |                     |                         |                |         |                            |                X               |          |
| **FR-10** |                |                      |       X       |          X          |                         |                |         |                            |                                |          |
| **FR-11** |                |                      |       X       |          X          |                         |                |         |                            |                                |          |
| **FR-12** |                |                      |       X       |          X          |            X            |        X       |         |                            |                                |          |
| **FR-13** |                |                      |               |                     |            X            |        X       |         |                            |                                |          |
| **FR-14** |                |                      |       X       |                     |                         |        X       |         |                            |                                |          |

### Non-Functional Requirements

| ######    | Authentication | Itinerary Management | Search Hotels | Hotel Search Engine | Machine Learning Engine | Recommendation | Payment | Payment Processing Service | Reservation Processing Service | Database |
|-----------|:--------------:|:--------------------:|:-------------:|:-------------------:|:-----------------------:|:--------------:|:-------:|:--------------------------:|:------------------------------:|:--------:|
| **NFR-1** |        X       |           X          |       X       |          X          |            X            |        X       |    X    |              X             |                X               |     X    |
| **NFR-2** |                |                      |               |          X          |                         |                |         |                            |                X               |          |
| **NFR-3** |                |                      |               |                     |                         |                |         |              X             |                                |          |
| **NFR-4** |                |                      |               |                     |                         |                |         |                            |                                |     X    |
| **NFR-5** |                |                      |               |                     |                         |                |         |                            |                                |     X    |
| **NFR-6** |                |                      |       X       |          X          |                         |                |    X    |              X             |                X               |     X    |
| **NFR-7** |        X       |           X          |       X       |          X          |            X            |        X       |    X    |              X             |                X               |     X    |
