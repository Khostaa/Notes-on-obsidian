URL - Uniform Resource Locator
- The URL will tell Python _where_ to send the API request to.
API - Application Programming Interface
- defines a set of communication rules and abilities
- through API, systems can interact with each other to exchange or manipulate data.
- For example, clicking the "send" button will make our email application use an API to tell the email server to send an email to the recipient.
## Web APIs, clients and servers
- Web APIs are used to enable communication between two software applications over a network or the internet. 
- This communication uses the HTTP protocol, the same protocol our browser uses to retrieve webpages from the internet. 
- In practice, this means a client sends a message over the internet to a server; the server, in turn, responds by sending a message back to the client.
### Types of Web APIs
- SOAP
	- takes a very formal approach and is most often used in enterprise applications where robustness and strict protocols are required.
- REST
	- the most popular and most common type, is known for its simplicity, scalability, and ease of integration.
- GraphQL
	- takes a more sophisticated approach, focusing on precise and flexible data retrieval, minimizing data transfer, and optimizing for performance.
## Working with APIs in Python
- well-known Python libraries for integrating Web APIs, urllib and requests.
### urllib
- comes bundled with python
- powerful but not very developer friendly
- making a request to the music catalog Web API to get a list of music albums.
```python
from urllib.request import urlopen
api = 'http://api.music-catalog.com/'

with urlopen(api) as response:
	data = response.read() # to get the response data
	string = data.decode() # to extract the raw data
	print(string)
```
### requests
- many powerful built-in features
- easier to use
```python
import requests
api = "http://api.music-catalog.com/"

response = requests.get(api)
print(response.text)
```

## The basic anatomy of an API request
URL: Uniform Resource Allocator
- is a structured address pointing to a specific resource
- via URL, what resource we want to interact with can be specified.
- e.g: http://350.5th-ave.com/unit/243
	- URL is the addresss of a single unit in the building
	- it contains all the information needed to navigate to that specified unit.
### Dissecting the URL
![[dissecting the url.png]]Domain: uniquely identifies the location of API server on the internet
Port - entrance/gateway into the building. common default ports are 80 and 443.
Path - with APIs, each resource has a unique location on the server, defined by its path
query - contains additional information like, 'take a elevator'
-  By constructing a URL with a path and parameters, we can control where to send our API requests to.
### Adding query parameters with requests
```python
# Append query parameter to the URL string
response = requests.get('http://350.5th-ave.com/unit/243?floor=77&elevator=True')
print(response.url)
# output - http://350.5th-ave.com/unit/243?floor=77&elevator=True
```
- use the *params* argument to add query parameters
```python
# create dictionary
query_params = {'floor':77, 'elevator': True}

# pass the dictionary using 'params' argument
response = requests.get('http://350.5th-ave.com/unit/243', params = query_params)
print(response.url)
# output - http://350.5th-ave.com/unit/243?floor=77&elevator=True
```
### HTTP Verbs
- 9 verbs - commonly used 4 - GET, POST, PUT, DELETE
Destination: Unit 243 of the 350the Ave office building
URL: http://350.5th-ave.com/unit/243
Actions

| verb   | Action | Description                                              |
| ------ | ------ | -------------------------------------------------------- |
| GET    | Read   | READ A RESOURCE - Check the mailbox contents             |
| POST   | Create | CREATE A RESOURCE - drop a new package in the mailbox    |
| PUT    | Update | UPDATES A RESOURCE - replace all packages with a new one |
| DELETE | Delete | REMOVES RESOURCE -remove all packages from the mailbox   |
- each verb has its own *method* in **requests** package.
- use the *data* argument to pass data to *POST* or *PUT* request.
```python
# Sending data via POST and PUT

# GET = Retrieve a resource
response = requests.get('http://350.5th-ave.com/unit/243')

# POST = Create a resource
response = requests.post('http://350.5th-ave.com/unit/243', data={"key": "value"})

# PUT = Update an existing resource
response = requests.put('http://350.5th-ave.com/unit/243', data={"key": "value"})

# DELETE = Remove a resource
response = requests.delete('http://350.5th-ave.com/unit/243')
```
## Headers and status codes
### Status code categories
- 1XX : informational responses
- 2XX : Successful responses
- 3XX : Redirection messages
- 4XX : Client error responses
- 5XX : Server error responses
### Frequently used status codes
- 200 : OK - requests.codes.ok
- 401 : Authentication failed
- 404 : Not Found - requests.codes.not_found
- 406 : Server not accept request - requests.code.not_acceptable
- 500 : Internal Server Error
![[Request and response message anatomy.png]]
- In request messages, start line -> response line
- contains the request type such as `GET` or `POST`, along with the path where the message should be delivered to.

- In response line, start line -> status-line
- contains a three-digit numerical `status-code` and `status message`

### Headers
- Headers contain information that describe the message or data being sent or received, such as the type of content we are sending or the date the requested resource was last modified.
- Headers are always formatted as key-value pairs separated by a colon. 
- Each header starts with a case-insensitive key, followed by a colon, and then the value of that header.

- In order to effectively communicate, client and server use message headers to agree on the language they are using to exchange information. This is called content negotiation.
- for example, the client sends the `accept` header to inform the server it can accept a response in JSON format. When the server responds, it includes the content-type header to let the client know what format it responded with.

#### Headers with requests
- The Python requests package allows us to add and read headers. 
- Each request method like requests.get or requests.post accepts an additional headers parameter with key-value pairs in the form of a dictionary.
```python
# Adding headers to reqeust
response = requests.get('https://api.datacamp.com', headers = {'accept':'application/json'})
```

- The response object has a headers attribute, which is a dictionary containing one key-value pair for every header received back in the response. We can access individual response headers by subsetting the dictionary using square brackets, or by using the .get() method on the dictionary.
```python
# Reading response headers
# using square brackets
response.headers['content-type']
# output - 'application/json'

# alternatively - using .get() method
response.headers.get('content-type')
```
### Status code with requests
- Each response object has a status-code attribute which contains the numeric value of the status-code.
- By chaining the status-message to the `requests.codes` lookup object we can easily find any status code, without the need to know the code. Like here where we use the lookup object to find the status-code for `Not Found`.
```python
# Accessing the status code
response = requests.get('https://api.datacamp.com/users/12')
response.status_code == 200
# output - True

# Looking up status codes using requests.codes
response = requests.get('https://api.datacamp.com/this/is/the/wrong/path')
response.status_code = requests.codes.not_found
# output - True
```
## API Authentication
- APIs we interact with frequently contain private, personal, or sensitive data. To protect this sensitive information, APIs require clients to authenticate before granting access
![[Before authentication.png]]
- When we add information to the request to identify ourselves, the server knows it's us and responds as expected, with a 200 OK status code.
![[after authentication.png]]
![[Authentication methods.png]]
- Basic Authentication - It uses a username and password for authentication. This method is easy to integrate but also the least secure, as it sends your password unencrypted over the internet to the server.

- API key/token Authentication - API Key or Token Authentication works by attaching a unique authentication key or token to each request. API keys are simple to implement but pose a security risk if compromised, as they also transmit unencrypted data.

- JWT Authentication - JWT or JSON Web Token Authentication is similar to API key authentication, but the main difference is that a JWT token has a limited lifespan and can contain additional encrypted data, such as user information.

- OAuth 2.0 - OAuth 2.0 is a comprehensive authentication framework that allows fine-grained access to resources without sharing any credentials.

### Basic Authentication
- to use basic authentication, we need to add an authorization header to the request we're sending to the API.
- This header must contain a base64-encoded combination of our username and password. 
- Base64 encoding is a two-way algorithm that anyone can easily decode, so unfortunately it provides no additional security.
- Implementing basic authentication using the requests package is easy.
- Instead of adding a header and doing the base64 encoding yourself, you can just pass a tuple containing your username and password using the auth function argument, requests takes care of all the encoding and adds the header.
```python
# Basic authentication with requests package
# This will automatically add a Basic Authentication header before sending the request
requests.get('http://api.music-catalog.com', auth=('username', 'password'))
```
### API key/token authorization
Tow options to add authentication to our request
- Simply adding the API key to URL as a query parameter
	- using a query parameter
	```python
# http://api.music-catalog.com/albums?access_token=faaa1c97bd3f4bd9b024c708c979feca
params = {'access_token': 'faaa1c97bd3f4bd9b024c708c979feca'}
requests.get('http://api.music-catalog.com/albums', params=params)
	```
- adding an authorization header
	- using the "Bearer" authorization header
```python
headers = {'Authorization': 'Bearer faaa1c97bd3f4bd9b024c708c979feca'}
requests.get('http://api.music-catalog.com/albums', headers=headers)
```
## Working with Structured data
### Complex data structures: JSON
- Javascript Object Notation
- widely Supported
- Human readable and Machine readable
- other types:
	- XML
	- CSV
	- YAML
#### from python to JSON and back
- using built in `json` package
- `json.dumps()` - turns a python object into a JSON string
- `json.loads()` - converts a JSON string into a python object
```python
import json
album = {'id': 42, 'title':'Back in Black'}
string = json.dumps(album) # encode a python object into a JSON string
album = json.loads(string) # Decodes a JSON string to a python object
```
### Requesting JSON data
- Without adding additional headers, the server will respond in plain text.
```python
# get request without headers
response = requests.get('http://api.music-catalob.com/lyrics')
print(response.text)

# Output - N' I never misss Cause I'm a problem child - AC/DC, Problem child
```
- When we add an `Accept` header with the value `application/json`, the server will respond with JSON text
- Using the `json()` function on the response object, we can now decode the JSON text into a Python object
- To decode JSON data from a response, use the `json()` method on the response object
```python
# GET request with an accept header
response = requests.get('http://api.music-catalog.com/lyrics', headers={'accept':'application/json'})

# Print the JSON text
print(response.text)

# Output - {'artist': 'AC/DC', 'lyric': "N' I never miss Cause I'm a problem child", 'track': 'Problem Child'}

# Decode into a python object
data = response.json()
print(data['artist'])

# output - AC/DC
```
### Sending JSON data
- - To send JSON data, use the `json` argument in `requests.post()` or `requests.put()`, which automatically sets the necessary headers.
- When using the `json` function argument to send the playlist object, requests will automatically add the necessary content-type headers and do all of the encoding for us.
```python
import requests
playlist = {'name': 'Road trip', 'genre':'rock', 'private':'true'}

# Add the playlist using via the 'json argument'
response = request.post('http://api.music-catalog.com/playlists', json=playlist)

# Get the request object
request = response.request

# Print the request content-type header
print(request.headers['content-type'])

# Output - application/json
```
## Error handling
- To determine if an error occurred or if the request was successful, REST APIs utilize the `status_code` in the response.
### Error status codes
- A status code in the 4XX or 5XX range indicates an issue. 
#### **4xx** Client errors
- Errors in the 400 range are client errors, indicating the request from the client could not be handled properly. These are usually caused by sending a wrong header or failing to authenticate. Typically, clients can handle or manage these errors easily by fixing the request. 
- **401 Unauthorized** - when trying to access a protected resource and need to add authentication to the request.
- **404 Not Found** - indicates that the server cannot find the resources that was requested.
- **429 Too Many Requests** - The client has sent too many requests in a give amount of time. in this case we need to implement a rate limiter to spread out our requests over a larger period of time.
#### **5xx** Server errors
- Errors in the 500 range indicate server problems. These errors are beyond the client's control, as the server acknowledged the request but faced difficulties handling it due to server-side issues. These are typically caused by server overload, or configuration errors. Clients cannot resolve these errors but should address them in the code to prevent unexpected behavior or bugs.
- **500 Internal Server Error** - The server experienced an unexpected issue which prevents it from responding
- **502 Bad Gateway** - The API server could not successfully reach another server it needed to complete the response
- **504 Gateway Timeout** - The server (which acts a gateway) did not get a response from the upstream server in time.
### Handling error
#### API errors
- to handle API errors is by checking the response status code for any codes in the 400 and 500 ranges, which indicate an error has occurred. 
- We can then use this status code to decide how to handle the error.
```python
import requests

url = 'http://api.music-catalog.com/albums'

r = requests.get(url)
if r.status_code >= 400:
	# oops, something went wrong
else:
	# all fine, let's do something
	# with the response
```
#### Connection errors
- An error might occur even before the request reaches the server, in which case we would not receive a response containing an error code.
- Fortunately, the requests library raises a ConnectionError in this case, which we can check for using a try/except block.
- To properly check for any errors with the API request, we should combine both approaches. The requests library makes this process straightforward.
```python
import requests
from requests.exceptions import ConnectionError
url = ''

try:
	r = requests.get(url)
	print(r.status_code)
except ConnectionError as conn_err:
	print(f'Connection Error! {conn_err}.')
	print(error)
```
### raise_for_status()
- requests library has a convenient feature that automatically raises errors for any responses containing an error status code.
- immediately after sending the request, any error code returned from the API will raise an `HTTPError` using the `raise_for_status` function
- This way, after checking for Connection errors, we can easily also check for any HTTPErrors that might have occurred.
```python
import requests
# 1: Import the requests library exceptions
from requests.exceptions import ConnectionError, HTTPError

try: 
	r = requests.get("http://api.music-catalog.com/albums") 
	# 2: Enable raising exceptions for returned error statuscodes
	r.raise_for_status()
	print(r.status_code)

# 3: Catch any connection errors
except ConnectionError as conn_err: 
	print(f'Connection Error! {conn_err}.')

# 4: Catch error responses from the API server
except HTTPError as http_err:
	print(f'HTTP error occurred: {http_err}')
```

```python
import requests
from requests.exceptions import ConnectionError, HTTPError

try:    
	response = requests.get("http://api.music-catalog.com/albums")
	response.raise_for_status()
	
except ConnectionError as conn_err: 
	print(f'Connection Error! {conn_err}.')

except HTTPError as http_err:
	print(f'HTTP error occurred: {http_err}')
```