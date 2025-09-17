# Task_API
Task_api_https://gorest.co.in/
Write positive and negative test cases for the API endpoints
POST - endpoint, that creates a new and unique user in the database:
1.URL: https://gorest.co.in/public-api/users
2.https://gorest.co.in/public/v2/users
3. Headers:
a. "Accept" = "application/json"
b. “Content-Type” = "application/json"
4. Body (example JSON):
{
    "name":"Maksim Kruglov",
     "gender":"male", 
     "email":"kobbra116@mail.ru", 
     "status":"active"
}
5. Endpoint requires Authentication, by Bearer Token (‘TEST_TOKEN’) that can be generated on https://gorest.co.in/access-token after а successful login to the site.
  ii. GET - endpoint, that returns the user by the id:
            1. URL: https://gorest.co.in/public-ap...{USER_ID}
            2. Method: GET
            3. In the URL the USER_ID must be sent after ...users/

1. POST Endpoint — Create a new and unique user
URL:
https://gorest.co.in/public/v2/users
Headers:

Accept: application/json
Content-Type: application/json
Authorization: Bearer TEST_TOKEN

Body Example:
{
  "name": "Maksim Kruglov",
  "gender": "male",
  "email": "kobbra116@mail.ru",
  "status": "active"
}

Positive Test Cases for POST

Test Case Description                Steps / Input                                     Expected Result
1.Create user with valid           Valid JSON (name, gender, unique email,status)      HTTP 201 Created, response
 unique data                       + valid Bearer token                                includes created user details
2.Create user with mixed case      e.g., "email": "Test.Email@EXAMPLE.COM"             HTTP 201 Created, email saved
email and name                                                                         correctly (case-insensitive)
3.Create user with minimal         All required fields filled correctly                HTTP 201 Created
required fields
4.Valid Bearer token with          Headers include Accept, Content-Type,               Success response, Content-Type:
Valid Bearer token with            and valid Authorization                             application/json                                   5.Multiple users created           Repeating valid POST requests with different        Each returns HTTP 201 Created, no
sequentially with unique           emails                                              duplicates
emails          
 

Negative Test Cases for POST                                             

Test Case Description                   Steps / Input                                     Expected Result
1.Create user with an             Same email as an existing user                       HTTP 422 or 409; error message about
existing email                                                                         duplicate email
2.Missing required field          Omit the email field                                 HTTP 422 with appropriate validation error
(email) 
3.Omit the email field            Provide invalid email, e.g.,                         HTTP 422 with validation error message
                                  "email": "invalid-email"
4.Missing Authentication          Do not provide Authorization header                  HTTP 401 Unauthorized
 header   
5.Invalid/expired Bearer          Provide malformed or expired token                   HTTP 401 Unauthorized or 403 Forbidden
 token        
6.Invalid gender value            "gender": "unknown" or invalid string                HTTP 422 with validation error
7.Missing Content-Type            Content-Type omitted or set to text/plain            HTTP 415 Unsupported Media Type or
header or wrong value                                                                  HTTP 400 Bad Request
8.Oversized input fields          Very long name or email strings                      HTTP 413 Payload Too Large or validation error
9.Additional unexpected fields    Add fields not expected by API (e.g.,                API ignores extra fields or returns HTTP
                                  "hobby": "chess")                                    400 with error
10.Empty JSON body                {} or empty request body                             HTTP 422 or HTTP 400; validation error
11.Malformed JSON                 Broken JSON syntax                                   HTTP 400 Bad Request
                                                              






