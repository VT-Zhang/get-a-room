[Project Summary](index.md) | [Use Cases](use_cases.md) | [Requirements](requirements.md) | [High-Level Design](high_level_design.md) | [Design Rationale](design_rationale.md) | [Conclusion](conclusion.md)

## Project Summary

**Get-a-room** is an online hotel booking system. Our idea is inspired by existing successful travel and booking websites like Expedia.com and Hotels.com. There are a number of reasons why we considered this software system to be a good fit for this project. The application is medium in size, not too trivial like the cruise control system introduced in the course, and it is not too big and complicated. Systems like this one have been designed by others but our solution is an original design that presents a challenge for the members of our group.

This is how the system works: customers are able to access the application by logging on to the website, or mobile app available on iOS and Android. Once logged in, customers can search for hotel rooms by typing in an address or zip code and their desired check-in and check-out date. After a hotel room is selected, the system communicates with the appropriate hotels and financial institutions for reservations and payment processing. In this application, customers can find the best available hotel deals, manage their upcoming itineraries, and even utilize the contactless check-in feature with their mobile devices. The application consists of two main components:

**Client-side System**, i.e. website and mobile apps. This component is responsible for rendering the user interface, authenticating the user session, and other client-side functions.

**Server-side System**, i.e. database, business logic module, network modules for connecting hotels and financial institutions’ APIs, security modules for protecting customer privacy and payment safety. One of the new features that sets this application apart from the crowd is the machine learning recommendation engine that decides which hotel rooms appear as the top search results. The machine learning model considers the number of stars, prices, reviews, previous search results, and promotions in producing recommendations for the user.

One improvement to the architecture we made during the design was the addition of an all-in-cloud server solution to address affordability, scalability, availability, and security for the system. get-a-room is designed to be a sophisticated, easy-to-use hotel booking software that provides the best recommendation every time.
