[Requirement Summary](index.md) | [High-Level Design](high_level_design.md) | [Modules](modules.md) |
[Design Rationale](design_rationale.md)

## Online Hotel Booking System

Our team is proposing to design an online hotel booking system for this project named Get-a-Room. Our idea is inspired by existing successful travel and booking websites like Expedia.com and Hotels.com. There are a number of reasons why we consider this software system to be a good fit for this project. The application is medium in size, not too trivial like the cruise control system introduced in the course, and it is not too big and complicated. Meanwhile, we believe there are places in the architecture as well as the available features that can be redesigned to bring new value to customers and vendors. Enhancements to the functions could add features such as allowing customer reviews, which would need to be considered when selecting an architecture. Systems like this one have been designed by others but our solution is an original design that presents a challenge for the members of our group.

This is how the system works: customers are able to access the application by logging on to the website, or mobile app available on iOS and Android. Once logged in, customers can search for hotel rooms by typing in an address or zip code and their desired check-in and check-out date. After a hotel room is selected, the system communicates with the appropriate hotels and financial institutions for reservations and payment processing. In this application, customers can find the best available hotel deals, manage their upcoming itineraries, and even utilize the contactless check-in feature with their mobile devices.
The application consists of two main components:

1) Client-side system, i.e. website and mobile apps. This component is responsible for rendering the user interface, authenticating the user session, and other client-side functions.
2) Server-side system, i.e. database, business logic module, network modules for connecting hotels and banks’ APIs, security modules for protecting customer privacy and payment safety. One of the new features that will set this application apart from the crowd is the machine learning recommendation engine that decides which hotel rooms appear as the top search results. Customers' past search records, price preferences, and geolocation information can all be used as the classifiers to the algorithm.
Designing Get-a-Room will challenge our group’s ability to analyze architecture options, make an appropriate decision, and implement design choices accordingly.

You can use the [editor on GitHub](https://github.com/VT-Zhang/get-a-room/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text
```
