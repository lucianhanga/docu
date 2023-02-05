# Application vs Business Logic

## Introduction

In this article, we will discuss the difference between application logic and business logic.

## Application Logic

Application Logic is concerned only with the code related to the application implementation. Concerned mainly with handling the requests and responses, database access, and the user interface.

Related more to the technical side of the application. Is a bridge between the user and the business logic.

## Business Logic

Business Logic is concerned with the code related to the business rules. Code related to the business rules, the business logic is the core of the application.

## Example

Let's take a simple example of a bank application. The application logic will be concerned with the user interface, the database access, and the requests and responses. The business logic will be concerned with the business rules, such as the interest rate, the minimum balance, and the maximum balance.

## Conclusion

Its impossible to keep them separated and sometimes they will overlap.
But the developer should try to keep the **Application Logic** in the `Controllers` and **Business Logic** in the `Model`. (if we follow the `MVC` pattern)

## Fat Models, Skinny Controllers

The `Fat Model` pattern is a design pattern that is used in the `Model-View-Controller` (MVC) architecture. The `Fat Model` pattern is used to separate the business logic from the user interface. The `Fat Model` pattern is also known as the `Business Logic Layer` pattern.

The `Skinny Controller` pattern is a design pattern that is used in the `Model-View-Controller` (MVC) architecture. The `Skinny Controller` pattern is used to separate the business logic from the user interface. The `Skinny Controller` pattern is also known as the `Business Logic Layer` pattern.

The Model is fat because we offload all the business logic to it to keep the controllers as simple as possible. The Controller is skinny because it only handles the requests and responses.

