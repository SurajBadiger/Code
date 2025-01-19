 Smart Product Search for Marketplace 

 
Module 1: Home Page 

User Story: Categorized Display (Story Points: 3) 

Description: Implement the backend functionality to display categorized products on the homepage, showing top products for each category. 

In Scope: 

Actor: End Customer 

Product: Categorized Products Display 

Event: Viewing categorized products on the homepage 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific product management 

Event: Admin product display 

Background: End customers need to see categorized products on the homepage to easily browse and find products of interest. 

API Endpoint: 

URL: /api/v1/products/categories 

Method: GET 

Response: A JSON object containing categories with up to 5 sub-categories each. 

Controller Layer: 

Class: ProductController 

Method: getCategorizedProducts() 

Service Layer: 

Class: ProductService 

Method: getCategorizedProducts() 

Repository Layer: 

Class: ProductRepository 

Method: findTop5ByCategoryOrderByPopularityDesc(String category) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleCategoryNotFoundException(CategoryNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they visit the homepage, THEN categorized products are displayed with products per category. 

GIVEN an end customer, WHEN there are no products in a category, THEN an empty list is returned for that category. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testGetCategorizedProducts_Success() 

Method: testGetCategorizedProducts_EmptyCategory() 

Shape 

User Story: Display Product - Home Page (Story Points: 3) 

Description: Implement the backend functionality to display featured products on the homepage, showcasing selected products prominently. 

In Scope: 

Actor: End Customer 

Product: Featured Products Display 

Event: Viewing featured products on the homepage 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific product management 

Event: Admin product display 

Background: End customers need to see featured products on the homepage to highlight special or popular items. 

 

API Endpoint: 

URL: /api/v1/products/featured 

Method: GET 

Response: A JSON object containing a list of featured products. 

Controller Layer: 

Class: ProductController 

Method: getFeaturedProducts() 

Service Layer: 

Class: ProductService 

Method: getFeaturedProducts() 

Repository Layer: 

Class: ProductRepository 

Method: findTopFeaturedProducts() 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleNoFeaturedProductsException(NoFeaturedProductsException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they visit the homepage, THEN featured products are displayed prominently. 

GIVEN an end customer, WHEN there are no featured products, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testGetFeaturedProducts_Success() 

Method: testGetFeaturedProducts_NoFeaturedProducts() 

Shape 

 

 

Module 2: Search Bar 

User Story: Search Bar Functionality (Story Points: 3) 

Description: Implement the backend functionality for the search bar, allowing users to search for products by name or description. 

In Scope: 

Actor: End Customer 

Product: Search Bar 

Event: Searching for products 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific search 

Event: Admin search results 

Background: End customers need a search bar to quickly find products by entering keywords. 

API Endpoint: 

URL: /api/v1/products/search 

Method: GET 

Request Parameters: 

query: The search query string 

Response: A JSON object containing a list of products matching the search query. 

Controller Layer: 

Class: ProductController 

Method: searchProducts(@RequestParam String query) 

Service Layer: 

Class: ProductService 

Method: searchProducts(String query) 

Repository Layer: 

Class: ProductRepository 

Method: findByNameContainingIgnoreCaseOrDescriptionContainingIgnoreCase(String name, String description) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleNoProductsFoundException(NoProductsFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they search for products, THEN the search results are displayed. 

GIVEN an end customer, WHEN there are no products matching the search query, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testSearchProducts_Success() 

Method: testSearchProducts_NoResults() 

Shape 

User Story: Autocomplete Search Suggestions (Story Points: 3) 

Description: Implement the backend functionality to provide autocomplete suggestions for the search bar, helping users quickly find products as they type. 

In Scope: 

Actor: End Customer 

Product: Autocomplete Search Suggestions 

Event: Typing in the search bar 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific search suggestions 

Event: Admin search operations 

Background: End customers need real-time search suggestions to enhance their search experience and quickly find relevant products. 

API Endpoint: 

URL: /api/v1/products/search-suggestions 

Method: GET 

Request Parameters: 

query: The search query string 

Response: A JSON object containing a list of search suggestions. 

Controller Layer: 

Class: ProductController 

Method: getSearchSuggestions(@RequestParam String query) 

Service Layer: 

Class: ProductService 

Method: getSearchSuggestions(String query) 

Repository Layer: 

Class: ProductRepository 

Method: findTop5ByNameContainingIgnoreCase(String query) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleNoSuggestionsFoundException(NoSuggestionsFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they type in the search bar, THEN autocomplete suggestions are displayed based on the query. 

GIVEN an end customer, WHEN there are no suggestions matching the query, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testGetSearchSuggestions_Success() 

Method: testGetSearchSuggestions_NoSuggestions() 

Shape 

Module 3: Login/Sign-Up 

User Story: Forgot Password (Story Points: 2) 

Description: Implement the backend functionality for the forgot password feature, allowing users to reset their password if they forget it. 

In Scope: 

Actor: End Customer 

Product: Forgot Password 

Event: Resetting a forgotten password 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific password reset 

Event: Admin password reset 

Background: End customers need the ability to reset their password if they forget it to regain access to their account. 

API Endpoint: 

URL: /api/v1/forgot-password 

Method: POST 

Request Body: 

{ 

  "email": jane.doe@example.com 

} 

Response: A JSON object with a message indicating that a password reset link has been sent to the email. 

Controller Layer: 

Class: UserController 

Method: forgotPassword(@RequestBody ForgotPasswordDTO forgotPasswordDTO) 

Service Layer: 

Class: UserService 

Method: sendPasswordResetLink(ForgotPasswordDTO forgotPasswordDTO) 

Repository Layer: 

Class: UserRepository 

Method: findByEmail(String email) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleUserNotFoundException(UserNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they submit a valid email, THEN a password reset link is sent to their email. 

GIVEN an end customer, WHEN they submit an email that does not exist, THEN an error message is returned indicating the email is not found. 

Testing: 

Unit Tests: 

Class: UserServiceTest 

Method: testForgotPassword_Success() 

Method: testForgotPassword_EmailNotFound() 

Shape 

User Story: User Signup (Story Points: 2) 

Description: Implement the backend functionality for user signup, allowing new users to create an account by providing their details. 

In Scope: 

Actor: End Customer 

Product: User Signup 

Event: Creating a new user account 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific signup 

Event: Admin account creation 

Background: End customers need the ability to sign up on the platform to access personalized features and make purchases. 

API Endpoint: 

URL: /api/v1/signup 

Method: POST 

Request Body: 

{ 

  "name": "Jane Doe", 

  "email": "jane.doe@example.com", 

  "password": "password123", 

  "phone_number": "0987654321" 

} 

Response: A JSON object with a success message and the user ID. 

Controller Layer: 

Class: UserController 

Method: signupUser(@RequestBody UserSignupDTO userSignupDTO) 

Service Layer: 

Class: UserService 

Method: signupUser(UserSignupDTO userSignupDTO) 

Repository Layer: 

Class: UserRepository 

Method: save(User user) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleUserAlreadyExistsException(UserAlreadyExistsException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they submit valid signup details, THEN a new user account is created, and a success message is returned. 

GIVEN an end customer, WHEN they submit an email that already exists, THEN an error message is returned indicating the email is already in use. 

Testing: 

Unit Tests: 

Class: UserServiceTest 

Method: testSignupUser_Success() 

Method: testSignupUser_EmailAlreadyExists() 

Shape 

User Story: User Login (Story Points: 3) 

Description: Implement the backend functionality for user login, allowing users to authenticate and access their account. 

In Scope: 

Actor: End Customer 

Product: User Login 

Event: Authenticating a user 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific login 

Event: Admin authentication 

Background: End customers need the ability to log in to the platform to access personalized features and make purchases. 

API Endpoint: 

URL: /api/v1/login 

Method: POST 

Request Body: 

{ 

  "email": "jane.doe@example.com", 

  "password": "password123" 

} 

Response: A JSON object with a success message and a JWT token. 

Controller Layer: 

Class: UserController 

Method: loginUser(@RequestBody UserLoginDTO userLoginDTO) 

Service Layer: 

Class: UserService 

Method: authenticateUser(UserLoginDTO userLoginDTO) 

Repository Layer: 

Class: UserRepository 

Method: findByEmail(String email) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleInvalidCredentialsException(InvalidCredentialsException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they submit valid login details, THEN they are authenticated, and a success message with a JWT token is returned. 

GIVEN an end customer, WHEN they submit invalid login details, THEN an error message is returned indicating invalid credentials. 

Testing: 

Unit Tests: 

Class: UserServiceTest 

Method: testLoginUser_Success() 

Method: testLoginUser_InvalidCredentials() 

 

Shape 

 

Module 4: Search Product Results 

User Story: Search Result Display (Story Points: 3) 

Description: Implement the backend functionality to display search results for products based on user queries. 

In Scope: 

Actor: End Customer 

Product: Search Product Results 

Event: Viewing search results 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific search 

Event: Admin search results 

Background: End customers need to search for products and view the results in a user-friendly format. 

API Endpoint: 

URL: /api/v1/products/search 

Method: GET 

Request Parameters: 

query: The search query string 

page: The page number for pagination 

size: The number of results per page 

Response: A JSON object containing a paginated list of products matching the search query. 

Controller Layer: 

Class: ProductController 

Method: searchProducts(@RequestParam String query, @RequestParam int page, @RequestParam int size) 

Service Layer: 

Class: ProductService 

Method: searchProducts(String query, int page, int size) 

Repository Layer: 

Class: ProductRepository 

Method: findByNameContainingIgnoreCase(String query, Pageable pageable) 

 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleNoProductsFoundException(NoProductsFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they search for products, THEN the search results are displayed in a paginated format. 

GIVEN an end customer, WHEN there are no products matching the search query, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testSearchProducts_Success() 

Method: testSearchProducts_NoResults() 

ShapeUser Story: Filter Search (Story Points: 3) 

Description: Implement the backend functionality to filter search results based on various criteria. 

In Scope: 

Actor: End Customer 

Product: Filter Search 

Event: Filtering search results 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific filters 

Event: Admin filter results 

Background: End customers need to apply filters to narrow down their search results based on specific criteria. 

API Endpoint: 

URL: /api/v1/products/search 

Method: GET 

Request Parameters: 

query: The search query string 

category: The product category 

priceMin: The minimum price 

priceMax: The maximum price 

brand: The product brand 

ratingMin: The minimum rating 

page: The page number for pagination 

size: The number of results per page 

Response: A JSON object containing a list of filtered products. 

Controller Layer: 

Class: ProductController 

Method: filterSearchProducts(@RequestParam String query, @RequestParam(required = false) String category, @RequestParam(required = false) Double priceMin, @RequestParam(required = false) Double priceMax, @RequestParam(required = false) String brand, @RequestParam(required = false) Double ratingMin, @RequestParam int page, @RequestParam int size) 

Service Layer: 

Class: ProductService 

Method: filterSearchProducts(String query, String category, Double priceMin, Double priceMax, String brand, Double ratingMin, int page, int size) 

Repository Layer: 

Class: ProductRepository 

Method: findByCriteria(String query, String category, Double priceMin, Double priceMax, String brand, Double ratingMin, Pageable pageable) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleNoProductsFoundException(NoProductsFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they apply filters to their search, THEN the filtered search results are displayed in a paginated format. 

GIVEN an end customer, WHEN there are no products matching the filter criteria, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testFilterSearchProducts_Success() 

Method: testFilterSearchProducts_NoResults() 

Shape 

Module 5: Product View Display 

User Story: Product Detail View (Story Points: 3) 

Description: Implement the backend functionality to display detailed information about a product. 

In Scope: 

Actor: End Customer 

Product: Product Detail View 

Event: Viewing product details 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific product details 

Event: Admin product view 

Background: End customers need to view detailed information about a product, including images, specifications, and customer reviews. 

 

API Endpoint: 

URL: /api/v1/products/{productId} 

Method: GET 

Response: A JSON object containing detailed information about the product. 

Controller Layer: 

Class: ProductController 

Method: getProductDetails(@PathVariable Long productId) 

Service Layer: 

Class: ProductService 

Method: getProductDetails(Long productId) 

Repository Layer: 

Class: ProductRepository 

Method: findById(Long productId) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleProductNotFoundException(ProductNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they view a product's details, THEN the detailed information about the product is displayed. 

GIVEN an end customer, WHEN the product does not exist, THEN an error message is returned indicating the product is not found. 

Testing: 

Unit Tests: 

Class: ProductServiceTest 

Method: testGetProductDetails_Success() 

Method: testGetProductDetails_ProductNotFound() 

Shape 

User Story: Quick Add to Cart (Story Points: 3) 

Description: Implement the backend functionality to allow users to quickly add a product to their cart from the product detail page. 

In Scope: 

Actor: End Customer 

Product: Quick Add to Cart 

Event: Adding a product to the cart 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific cart management 

Event: Admin cart operations 

Background: End customers need the ability to quickly add products to their cart from the product detail page. 

API Endpoint: 

URL: /api/v1/cart/add 

Method: POST 

Response: A JSON object with a success message and the updated cart item count. 

Controller Layer: 

Class: CartController 

Method: addToCart(@RequestBody AddToCartDTO addToCartDTO) 

Service Layer: 

Class: CartService 

Method: addToCart(AddToCartDTO addToCartDTO) 

Repository Layer: 

Class: CartRepository 

Method: save(CartItem cartItem) 

Response: A JSON object containing the products in the user's cart and the total price. 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleProductNotFoundException(ProductNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they add a product to their cart, THEN the product is added to the cart, and a success message is returned. 

GIVEN an end customer, WHEN the product does not exist, THEN an error message is returned indicating the product is not found. 

Testing: 

Unit Tests: 

Class: CartServiceTest 

Method: testAddToCart_Success() 

Method: testAddToCart_ProductNotFound() 

Shape 

Module 6: Cart Page 

User Story: Display Cart Products (Story Points: 3) 

Description: Implement the backend functionality to display the products in the user's cart. 

In Scope: 

Actor: End Customer 

Product: Cart Page 

Event: Viewing cart products 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific cart management 

Event: Admin cart operations 

Background: End customers need to view the products they have added to their cart, including details like quantity and total price. 

API Endpoint: 

URL: /api/v1/cart 

Method: GET 

Request Parameters: 

userId: The ID of the user 

Response: A JSON object containing the products in the user's cart and the total price. 

Controller Layer: 

Class: CartController 

Method: getCartItems(@RequestParam Long userId) 

Service Layer: 

Class: CartService 

Method: getCartItems(Long userId) 

Repository Layer: 

Class: CartRepository 

Method: findByUserId(Long userId) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleCartNotFoundException(CartNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they view their cart, THEN the products in the cart are displayed with details like quantity and total price. 

GIVEN an end customer, WHEN there are no products in the cart, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: CartServiceTest 

Method: testGetCartItems_Success() 

Method: testGetCartItems_EmptyCart() 

ShapeUser Story: Delete From Cart (Story Points: 2) 

Description: Implement the backend functionality to allow users to delete products from their cart. 

In Scope: 

Actor: End Customer 

Product: Cart Page 

Event: Deleting products from the cart 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific cart management 

Event: Admin cart operations 

Background: End customers need the ability to remove products from their cart to manage their purchases effectively. 

API Endpoint: 

URL: /api/v1/cart/delete 

Method: DELETE 

Response: A JSON object containing the products in the user's cart and the total price. 

Controller Layer: 

Class: CartController 

Method: deleteFromCart(@RequestBody DeleteFromCartDTO deleteFromCartDTO) 

Service Layer: 

Class: CartService 

Method: deleteFromCart(DeleteFromCartDTO deleteFromCartDTO) 

Repository Layer: 

Class: CartRepository 

Method: deleteByUserIdAndProductId(Long userId, Long productId) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleProductNotFoundException(ProductNotFoundException ex) 

 

Acceptance Criteria: 

GIVEN an end customer, WHEN they delete a product from their cart, THEN the product is removed from the cart, and a success message is returned. 

GIVEN an end customer, WHEN the product does not exist in the cart, THEN an error message is returned indicating the product is not found. 

Testing: 

Unit Tests: 

Class: CartServiceTest 

Method: testDeleteFromCart_Success() 

Method: testDeleteFromCart_ProductNotFound() 

Shape 

Module 7: User Profile 

User Story: End User Profile Management (Story Points: 3) 

Description: Implement the backend functionality for end users to view and update their personal profile information. 

In Scope: 

Actor: End Customer 

Product: User Profile Management 

Event: Viewing and updating profile information 

Out of Scope: 

Actor: Admin accounts 

Product: Admin profile management 

Event: Admin account modifications 

Background: End customers need the ability to manage their profile details such as contact information, address, and order history to ensure personalized and efficient service. 

API Endpoint: 

URL: /api/v1/profile 

Method: GET 

 

Request Parameters: 

userId: The ID of the user 

Response: A JSON object containing the user's profile details and order history. 

Controller Layer: 

Class: UserProfileController 

Method: getUserProfile(@RequestParam Long userId) 

Service Layer: 

Class: UserProfileService 

Method: getUserProfile(Long userId) 

Repository Layer: 

Class: UserRepository 

Method: findById(Long userId) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleUserNotFoundException(UserNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they view their profile, THEN their profile details are displayed. 

GIVEN an end customer, WHEN the user does not exist, THEN an error message is returned indicating that the user needs to login. 

Testing: 

Unit Tests: 

Class: UserProfileServiceTest 

Method: testGetUserProfile_Success() 

Method: testGetUserProfile_UserNotFound() 

Shape 

 

User Story: Update User Profile (Story Points: 2) 

Description: Implement the backend functionality for end users to update their personal profile information. 

In Scope: 

Actor: End Customer 

Product: User Profile Management 

Event: Updating profile information 

Out of Scope: 

Actor: Admin accounts 

Product: Admin profile management 

Event: Admin account modifications 

Background: End customers need the ability to update their profile details such as contact information and address to ensure personalized and efficient service. 

API Endpoint: 

URL: /api/v1/profile/update 

Method: PUT 

Response: A JSON object with a success message indicating that the profile has been updated. 

Controller Layer: 

Class: UserProfileController 

Method: updateUserProfile(@RequestBody UserProfileDTO userProfileDTO) 

Service Layer: 

Class: UserProfileService 

Method: updateUserProfile(UserProfileDTO userProfileDTO) 

Repository Layer: 

Class: UserRepository 

Method: save(User user) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleUserNotFoundException(UserNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they update their profile, THEN the profile details are updated, and a success message is returned. 

GIVEN an end customer, WHEN the user does not exist, THEN an error message is returned indicating the user needs to login. 

Testing: 

Unit Tests: 

Class: UserProfileServiceTest 

Method: testUpdateUserProfile_Success() 

Method: testUpdateUserProfile_UserNotFound() 

Module 8: Order Management 

User Story: Place Order (Story Points: 5) 

Description: Implement the backend functionality for users to place an order for the products in their cart. 

In Scope: 

Actor: End Customer 

Product: Order Management 

Event: Placing an order 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific order management 

Event: Admin order operations 

Background: End customers need the ability to place orders for the products they have added to their cart. 

API Endpoint: 

URL: /api/v1/orders/place 

Method: POST 

Response: A JSON object with a success message and the order ID. 

Controller Layer: 

Class: OrderController 

Method: placeOrder(@RequestBody PlaceOrderDTO placeOrderDTO) 

 

Service Layer: 

Class: OrderService 

Method: placeOrder(PlaceOrderDTO placeOrderDTO) 

Repository Layer: 

Class: OrderRepository 

Method: save(Order order) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleOrderPlacementException(OrderPlacementException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they place an order, THEN the order is created, and a success message is returned. 

GIVEN an end customer, WHEN there is an issue with placing the order, THEN an error message is returned. 

Testing: 

Unit Tests: 

Class: OrderServiceTest 

Method: testPlaceOrder_Success() 

Method: testPlaceOrder_Failure() 

Shape 

User Story: View Order History (Story Points: 2) 

Description: Implement the backend functionality for users to view their order history. 

In Scope: 

Actor: End Customer 

Product: Order Management 

Event: Viewing order history 

Out of Scope: 

Actor: Admin accounts 

Product: Admin-specific order management 

Event: Admin order operations 

Background: End customers need the ability to view their past orders to track their purchases and order statuses. 

API Endpoint: 

URL: /api/v1/orders/history 

Method: GET 

Request Parameters: 

userId: The ID of the user 

Response: A JSON object containing the user's past orders. 

Controller Layer: 

Class: OrderController 

Method: getOrderHistory(@RequestParam Long userId) 

Service Layer: 

Class: OrderService 

Method: getOrderHistory(Long userId) 

Repository Layer: 

Class: OrderRepository 

Method: findByUserId(Long userId) 

Exception Handling: 

Class: GlobalExceptionHandler 

Method: handleOrderNotFoundException(OrderNotFoundException ex) 

Acceptance Criteria: 

GIVEN an end customer, WHEN they view their order history, THEN the past orders are displayed. 

GIVEN an end customer, WHEN there are no past orders, THEN an empty list is returned. 

Testing: 

Unit Tests: 

Class: OrderServiceTest 

Method: testGetOrderHistory_Success() 

Method: testGetOrderHistory_NoOrders() 

Shape 
