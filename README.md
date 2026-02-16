# Foodlane-backend
## Online Food Delivery System-Backend(Spring Boot)
### Overview
This project is a backend application for an Online Food Delivery System built using Spring Boot. It provides RESTful APIs for user authentication, restaurant management, food ordering, cart operations, and secure payments.
The system implements JWT-based authentication and role-based authorization to ensure secure access for customers and administrators.
## Features

### JWT-Based Authentication & Authorization
Secure login and registration using Spring Security with role-based access (ADMIN, OWNER, CUSTOMER).

### Restaurant Management
Admin can create, update, and manage restaurants with address and contact details.

### Food & Category Management
Add, update, and categorize food items with price, description, availability, and vegetarian/seasonal flags.

### Cart Management
Users can add, update, and remove food items from their cart before placing an order.

### Order Processing System
Secure order placement and order tracking functionality.

### Stripe Payment Integration
Integrated payment gateway for secure and seamless online transactions.

### Role-Based Access Control (RBAC)
Different access levels for Admin, Restaurant Owner, and Customer.

### Search & Filtering
Filter food items by category and restaurant.

### MySQL Database Integration
Persistent data storage using Spring Data JPA and Hibernate.
###
RESTful API Architecture:Clean and structured REST APIs following standard HTTP methods.
## Technologies Used

### Backend
- Java 11
- Spring Boot
- Spring Security
- JWT (JSON Web Tokens)

### Database
- MySQL
- Spring Data JPA (Hibernate)

### Build & Tools
- Maven
- Postman
- Git & GitHub
- Stripe (for payment processing)

## Installation and Setup

- Install Java 11
- Install MySQL and create a database
- Configure application.properties with your database credentials
- Set up a Stripe account for payment processing
- Clone the repository:
  git clone <your-repository-link>
- Navigate to the project directory
- Run the application using:
  mvn spring-boot:run
- Access the API at:
  http://localhost:8080


## Controllers Documentation

This document provides a concise reference for the controllers in the `com.spring.controller` package. For each controller you'll find the base path, the exposed endpoints (HTTP method + path), a short description, required headers (Authorization JWT where applicable), request payload classes, and response types.

> Note: Most endpoints require an `Authorization` header with a JWT. The header is shown as `Authorization: Bearer <token>` though the controllers read the full header string.

---

### AuthController

- Base path: `/auth`

Endpoints:

- POST `/auth/signup`
	- Description: Register a new user. Creates a `User` and an empty `Cart`, returns a JWT on success.
	- Request body: `User` (email, fullName, role, password)
	- Response: `AuthResponse` (jwt, message, role)
	- Response status: `201 Created`

- POST `/auth/signin`
	- Description: Authenticate an existing user. Returns JWT and role.
	- Request body: `LoginRequest` (email, password)
	- Response: `AuthResponse` (jwt, message, role)
	- Response status: `200 OK`

---

### CartController

- Base path: `/api`

Endpoints:

## Controllers Documentation

This document provides a concise reference for the controllers in the `com.spring.controller` package. For each controller you'll find the base path, the exposed endpoints (HTTP method + path), a short description, required headers (Authorization JWT where applicable), request payload classes, and response types.

> Note: Most endpoints require an `Authorization` header with a JWT. The header is shown as `Authorization: Bearer <token>` though the controllers read the full header string.

---

### AuthController

- Base path: `/auth`

Endpoints:

- POST `/auth/signup`
	- Description: Register a new user. Creates a `User` and an empty `Cart`, returns a JWT on success.
	- Request body: `User` (email, fullName, role, password)
	- Response: `AuthResponse` (jwt, message, role)
	- Response status: `201 Created`

- POST `/auth/signin`
	- Description: Authenticate an existing user. Returns JWT and role.
	- Request body: `LoginRequest` (email, password)
	- Response: `AuthResponse` (jwt, message, role)
	- Response status: `200 OK`

---

### CartController

- Base path: `/api`

Endpoints:

- PUT `/api/cart/add`
	- Description: Add an item to the authenticated user's cart.
	- Request body: `AddCartItemRequest`
	- Required header: `Authorization` (JWT)
	- Response: `CartItem` (`200 OK`)

- PUT `/api/cart-item/update`
	- Description: Update quantity of a cart item.
	- Request body: `UpdateCartItemRequest` (cartItemId, quantity)
	- Required header: `Authorization` (JWT)
	- Response: `CartItem` (`200 OK`)

- DELETE `/api/cart-item/{id}/remove`
	- Description: Remove a cart item by id.
	- Path param: `id` (cart item id)
	- Required header: `Authorization` (JWT)
	- Response: `Cart` (`200 OK`)

- PUT `/api/cart/clear`
	- Description: Clear the authenticated user's cart.
	- Required header: `Authorization` (JWT)
	- Response: `Cart` (`200 OK`)

- GET `/api/cart`
	- Description: Get the authenticated user's cart.
	- Required header: `Authorization` (JWT)
	- Response: `Cart` (`200 OK`)

---

### CategoryController

- Base path: `/api`

Endpoints:

- POST `/api/admin/category`
	- Description: Create a new category (admin).
	- Request body: `Category` (name)
	- Required header: `Authorization` (JWT)
	- Response: `Category` (`201 Created`)

- GET `/api/category/restaurant/{id}`
	- Description: Get categories for a restaurant.
	- Path param: `id` (restaurant id)
	- Required header: `Authorization` (JWT)
	- Response: `List<Category>` (`201 Created` in code, logically `200 OK`)

---

### FoodController

- Base path: `/api/food`

Endpoints:

- GET `/api/food/search?name={name}`
	- Description: Search foods by name.
	- Query param: `name`
	- Required header: `Authorization` (JWT)
	- Response: `List<Food>` (`201 Created` in code, logically `200 OK`)

- GET `/api/food/restaurant/{restaurantId}`
	- Description: List foods for a restaurant, optional filters: `vegetarian`, `seasonal`, `nonVegetarian`, `food_category`.
	- Path param: `restaurantId`
	- Query params: `vegetarian`, `seasonal`, `nonVegetarian`, `food_category` (all optional)
	- Required header: `Authorization` (JWT)
	- Response: `List<Food>` (`200 OK`)

---

### HomeController

- Base path: `/` (root)

Endpoints:

- GET `/`
	- Description: Simple welcome endpoint used as a health/info route.
	- Response: `String` (`200 OK`)

---

### IngredientController

- Base path: `/api/admin/ingredients`

Endpoints:

- POST `/api/admin/ingredients/category`
	- Description: Create ingredient category for a restaurant.
	- Request body: `IngredientCategoryRequest` (name, restaurantId)
	- Response: `IngredientCategory` (`201 Created`)

- POST `/api/admin/ingredients`
	- Description: Create an ingredient item.
	- Request body: `IngredientRequest` (restaurantId, name, categoryId)
	- Response: `IngredientsItem` (`201 Created`)

- PUT `/api/admin/ingredients/{id}/stock`
	- Description: Update stock for an ingredient item by id.
	- Path param: `id`
	- Response: `IngredientsItem` (`200 OK`)

- GET `/api/admin/ingredients/restaurant/{id}`
	- Description: List all ingredients for a restaurant.
	- Path param: `id`
	- Response: `List<IngredientsItem>` (`200 OK`)

- GET `/api/admin/ingredients/restaurant/{id}/category`
	- Description: List ingredient categories for a restaurant.
	- Path param: `id`
	- Response: `List<IngredientCategory>` (`200 OK`)

---

### OrderController

- Base path: `/api`

Endpoints:

- POST `/api/order`
	- Description: Create an order for the authenticated user and return a payment link.
	- Request body: `OrderRequest`
	- Required header: `Authorization` (JWT)
	- Response: `PaymentResponse` (`200 OK`)

- GET `/api/order/user`
	- Description: Get order history for the authenticated user.
	- Required header: `Authorization` (JWT)
	- Response: `List<Order>` (`200 OK`)

---

### RestaurantController

- Base path: `/api/restaurants`

Endpoints:

- GET `/api/restaurants/search?keyword={keyword}`
	- Description: Search restaurants by keyword.
	- Query param: `keyword`
	- Required header: `Authorization` (JWT)
	- Response: `List<Restaurant>` (`200 OK`)

- GET `/api/restaurants` 
	- Description: List all restaurants.
	- Required header: `Authorization` (JWT)
	- Response: `List<Restaurant>` (`200 OK`)

- GET `/api/restaurants/{id}`
	- Description: Get a restaurant by id.
	- Path param: `id`
	- Required header: `Authorization` (JWT)
	- Response: `Restaurant` (`200 OK`)

- PUT `/api/restaurants/{id}/add-favorites`
	- Description: Add a restaurant to the authenticated user's favorites; returns a `RestaurantDto`.
	- Path param: `id`
	- Required header: `Authorization` (JWT)
	- Response: `RestaurantDto` (`200 OK`)

---

### UserController

- Base path: `/api/users`

Endpoints:

- GET `/api/users/profile`
	- Description: Get profile information for the authenticated user.
	- Required header: `Authorization` (JWT)
	- Response: `User` (`200 OK`)

---

### AdminRestaurantController

- Base path: `/api/admin/restaurants`

Endpoints:

- POST `/api/admin/restaurants`
	- Description: Create a restaurant (admin/owner).
	- Request body: `CreateRestaurantRequest`
	- Required header: `Authorization` (JWT)
	- Response: `Restaurant` (`201 Created`)

- PUT `/api/admin/restaurants/{id}`
	- Description: Update restaurant details.
	- Path param: `id`
	- Request body: `CreateRestaurantRequest`
	- Required header: `Authorization` (JWT)
	- Response: `Restaurant` (`201 Created`)

- DELETE `/api/admin/restaurants/{id}`
	- Description: Delete a restaurant.
	- Path param: `id`
	- Required header: `Authorization` (JWT)
	- Response: `MessageResponse` (`200 OK`)

- PUT `/api/admin/restaurants/{id}/status`
	- Description: Toggle/update restaurant status (active/inactive).
	- Path param: `id`
	- Required header: `Authorization` (JWT)
	- Response: `Restaurant` (`200 OK`)

- GET `/api/admin/restaurants/user`
	- Description: Get restaurant for the authenticated user (owner).
	- Required header: `Authorization` (JWT)
	- Response: `Restaurant` (`200 OK`) or `403 Forbidden` on error

---

### AdminOrderController

- Base path: `/api/admin`

Endpoints:

- GET `/api/admin/order/restaurant/{id}`
	- Description: Get orders for a restaurant, optional `order_status` filter.
	- Path param: `id`
	- Query param: `order_status` (optional)
	- Required header: `Authorization` (JWT)
	- Response: `List<Order>` (`200 OK`)

- PUT `/api/admin/order/{id}/{orderStatus}`
	- Description: Update order status for a given order.
	- Path params: `id`, `orderStatus`
	- Required header: `Authorization` (JWT)
	- Response: `Order` (`200 OK`)

---

### AdminFoodController

- Base path: `/api/admin/food`

Endpoints:

- POST `/api/admin/food`
	- Description: Create a food item for the authenticated user's restaurant.
	- Request body: `CreateFoodRequest`
	- Required header: `Authorization` (JWT)
	- Response: `Food` (`201 Created`)

- DELETE `/api/admin/food/{id}`
	- Description: Delete a food by id.
	- Path param: `id`
	- Required header: `Authorization` (JWT)
	- Response: `MessageResponse` (`201 Created` in code, logically `200 OK`)

- PUT `/api/admin/food/{id}`
	- Description: Toggle/update food availability status by id.
	- Path param: `id`
	- Required header: `Authorization` (JWT)
	- Response: `Food` (`201 Created` in code, logically `200 OK`)

---

## Notes & Next Steps

- I summarized each controller's endpoints and inputs/responses from the source. I preserved the status codes as used in code but noted where `201 Created` is used in places that are logically `200 OK` (this may be intentional or a minor inconsistency to clean).
- Next steps (optional):
	- Add example request/response JSON for key endpoints.
	- Generate an OpenAPI/Swagger spec (Springdoc) for automated API docs.
	- Add method-level JavaDoc in controllers for richer documentation.

