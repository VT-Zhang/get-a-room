[Project Summary](index.md) | [Use Cases](use_cases.md) | [Requirements](requirements.md) | [High-Level Design](high_level_design.md) | [Modules](modules.md) | [Design Rationale](design_rationale.md) | [Conclusion](conclusion.md)

## Requirements

### Functional Requirements

| **#** | **Description** |
|---|---|
| **FR-1** | Users have the ability to create an online account. Email address, password, and name required to create an account. |
| **FR-2** | Authentication requires email address and password. |
| **FR-3** | User is able to complete booking request as a guest or with a saved account. |
| **FR-4** | Ability to view and manage previous and future bookings and itineraries will be available to users with a saved account. |
| **FR-5** | Bookings can be canceled by accessing a saved account or searching by confirmation number. |
| **FR-6** | Check-in/checkout-out dates, number of guests, number of rooms, and type of room can be edited after a booking is completed, if available at the selected hotel. |
| **FR-7** | Users may be required to provide a form of payment at the time of booking; UI must be able to accept payment information. User receives an error message if payment fails. |
| **FR-8** | Confirmation page with a confirmation number will be displayed once booking is completed. |
| **FR-9** | Confirmation email will be sent to the user email address with confirmation number once booking is completed. |
| **FR-10** | The following search criteria are required to search for available hotel rooms: Address (full address, city, or zip code), check-in and check-out dates, number of rooms, number of adults and children. |
| **FR-11** | The following search criteria are optional: Distance from location entered, price range, star rating of hotel, guest rating of hotel. |
| **FR-12** | If a saved account is being used, search results will be ranked based on machine learning algorithms. |
| **FR-13** | Machine learning engine utilizes the following inputs based on the user's previous hotel choices: distance from location entered, price range, star rating of hotel, guest rating of hotel. Engine will generate ranked results based on the user's preferences. |
| **FR-14** | Search results can be manually filtered or sorted by the user based on: distance from location entered, price high-to-low, price low-to-high, star rating of hotel, guest rating of hotel. |

### Non-Functional Requirements

| **#** | **Description** |
|---|---|
| **NFR-1** | get-a-room will support a website and mobile app for Android and iOS devices. |
| **NFR-2** | Search engine and booking processing service must interface with multiple hotel APIs to retrieve search results. |
| **NFR-3** | Payment processing service must interface with multiple financial institution APIs to process payments. |
| **NFR-4** | Cloud database solution will be utilized. |
| **NFR-5** | Database must have capability to scale up or down if/when necessary. |
| **NFR-6** | User personal data and payment information must be secured. |
| **NFR-7** | Website and mobile application must be available 99.99% of the time. |
