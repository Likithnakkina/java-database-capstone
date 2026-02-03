## Architecture Summary

This application is built using Spring Boot and follows a layered architecture. It uses a combination of MVC controllers and REST controllers to handle different types of user interactions. Thymeleaf templates are used to render views for Admin and Doctor dashboards, providing a server-side rendered user interface. Other parts of the application interact with the system through RESTful APIs.

The application connects to two databases to manage data efficiently. MySQL is used to store structured relational data such as patients, doctors, appointments, and admin information using JPA entities. MongoDB is used to store prescription data as document models. All incoming requests are handled by controllers, passed through a common service layer for business logic, and finally processed by repository layers specific to each database.

## Numbered Flow of Data and Control

1. A user accesses the application through the Admin dashboard, Doctor dashboard, or other client interfaces.

2. The request is directed to either a Thymeleaf MVC controller or a REST controller based on the type of action.

3. The controller forwards the request to the service layer for processing.

4. The service layer applies business logic and determines which database needs to be accessed.

5. For relational data, the service communicates with JPA repositories connected to the MySQL database.

6. For prescription data, the service interacts with MongoDB repositories using document models.

7. The processed data is returned back through the service and controller layers and finally presented to the user as a web page or API response.
