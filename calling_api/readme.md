# Calling API using Ansible Overview

Ansible can interact with APIs using the uri module, which allows you to make HTTP requests (GET, POST, PUT, DELETE, etc.). This module is useful for interacting with RESTful APIs to retrieve, create, update, or delete resources.

Here’s a basic structure on how to use APIs in Ansible:

## Example Playbook to Use an API with uri Module
Example 1 playbook demonstrates a few key types of HTTP requests (GET and POST) and how to handle the responses.

When an API requires authentication with a username and password, it often expects them to be sent as a Base64-encoded string in the Authorization header. Here’s an example of how to use Ansible's uri module with Basic Authentication, either using url_username and url_password directly or by encoding the credentials manually.

## Explanation
### Variables:
    - api_url: Base URL for the API.
    - auth_token: The API authentication token, used in the header.
    - headers: Includes necessary headers like Content-Type and Authorization for the API requests.

### GET Request:
    - url: Complete endpoint URL.
    - method: Specifies GET for retrieving information.
    - return_content: true: Ensures the response content is stored in the register variable.
    - register: get_response: Registers the output for further processing.

### POST Request:
    - method: Specifies POST to create a new resource.
    - body_format: json: Sets the body format to JSON.
    - body: Contains the data to be sent in the POST request.

### Authentication
    - Bearer Token: Most APIs require a token in the Authorization header. Replace your_api_token_here with an actual token.
    - Basic Auth: If the API uses basic authentication, you can specify url_username and url_password instead of Authorization in the headers.

### Handling Responses
Use the register keyword to capture the output of each request. The response typically includes:
    - .json: Parsed JSON data.
    - .status: HTTP status code.
    - .content: Raw content of the response.

### Error Handling
To handle errors, use failed_when to control task failure conditions based on the HTTP response code. Example:
```
failed_when: post_response.status != 201
```
Example: Using Dynamic Variables
To pass variables dynamically into an API call, such as making a POST request with a variable payload, you could define payload as a dictionary:
```
vars:
  payload:
    key1: "{{ some_variable }}"
    key2: "static_value"
```
Then, use payload as the body in your uri task:
```
body: "{{ payload }}"
```

## Example 2: Using url_username and url_password
This is the simplest method, as Ansible will handle Base64 encoding for you automatically.

## Explanation
### Basic Authentication (basic_auth_base64):
Authorization: "Basic <Base64 encoded credentials>" is the standard format for Basic Auth headers, where the credentials are encoded as username:password.
The b64encode filter encodes the string to Base64, allowing you to build the authorization header manually.

## Example 3: Manually Encoding Credentials with Base64
If you want to manually encode the credentials in Base64 and set them in the Authorization header, here’s how you could do it:

Use Ansible’s b64encode filter to encode the credentials.
Add the Authorization header manually.

## Explanation
### force_basic_auth (basic_auth):
When set to yes, Ansible forces Basic Authentication even if the server is using HTTPS. This is useful when the API is hosted on HTTPS but still requires Basic Auth.
This approach gives flexibility in situations where credentials need to be encoded explicitly for headers.