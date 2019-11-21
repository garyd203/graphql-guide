# Pragmatic GraphQL
A hype-free guide to GraphQL for server-side developers, with a touch of snark

## Introduction

### What is GraphQL
GraphQL is a new RPC system. That is, it is in the same category as REST, Webservices/SOAP, gRPC and CORBA.

### Advantages
The key distinctive of GraphQL is that it gives the API client fine-grained control over the fields returned from an API call (the data shape). This addresses a number of issues around over-requesting, that are present in most other RPC systems.

### Disadvantages
GraphQL is not a mature technology. A number of operational and development considerations are not adequately addressed at the moment (as of late 2019).

## Requests

### Network Protocol
Requests are implemented as a text body in a HTTP(S) POST to a single URL (it is aldso possible, but unwise, to use HTTP GET with a URL-encoded GraphQL request). Responses always have HTTP status code 200.

### Operations
There are 3 types of request (called "operations"). Functionally, here's what they mean

1. "query": Function call with parameters, parallel execution, structured response
2. "mutation": Function call with parameters, blocking sequential execution, structured response
3. "subscription": Function call with parameters, structured response with server-push streaming data

### Errors
Over the wire, responses always have HTTP status code 200, even if there was a functional error. However, GraphQL clients should also be prepared to handle HTTP 500 (for catastrophic server errors) and network errors.
