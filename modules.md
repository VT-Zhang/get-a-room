[Project Summary](index.md) | [Use Cases](use_cases.md) | [Requirements](requirements.md) | [High-Level Design](high_level_design.md)
[Modules](modules.md) | [Design Rationale](design_rationale.md) | [Conclusion](conclusion.md)

## Modules

![Happy_Path_Flow_Chart](https://user-images.githubusercontent.com/24898162/95685389-94edb000-0bc5-11eb-9427-1003c1e89001.jpg)

## Orchestrator

The “Orchestrator” is one of the most important modules of the system. It works as the centralized relay controller for passing http requests of various modules from client side system to the target micro services and APIs endpoints of the server side system, and returns the http responses with payload data from the server side system back to the client side system. It authorizes and authenticates each and every service call by checking the http header and session token to ensure that the client who initiates the request is a legitimate user and has appropriate level of authorizations. Since almost all the steps from the following flow involve the Orchestrator, therefore description of passing the request and response to and from the Orchestrator will be omitted.

## Happy Path Flow

The “Happy Path” flow of our “get-a-room” online hotel booking system:

1. User logs on to the system by entering appropriate credentials to the “Authentication” module.
2. User interacts with the “Main Interface”.
3. User chooses the “Search Hotels” module by entering search criteria, i.e. date, address, zip code, star of the hotel, and price preferences. 
4. “Hotel Search Engine” module from the server side system receives the search criteria and forwards the search request to an array of exterior hotels and platforms APIs.
5. Upon gathering a list of available hotels per the search criteria, the “Hotel Search Engine” module hands the raw list over to the “Machine Learning Engine” module.
6. “Machine Learning Engine” processes, optimizes and reorganizes the raw list and returns the hotel search results back to the client side system.
7. “Recommendation” module of the client side system presents and displays the search results to the user.
8. User picks one hotel from the results that best fits his/her preference and criteria.
9. User is prompted with the “Payment” module, and enters the payment information.
10. “Payment Process Service” of the server side system connects to exterior APIs from banks or financial institutions for processing payments.
11. Upon payment is confirmed, “Reservation Processing Service” returns the confirmation response to the client side system.
12. User receives the payment and hotel reservation confirmation.
13. User may choose to go to the “Itinerary Management” module to manage the trip or go to the “Main Interface” to interact with other function modules.
