# Pragmatic GraphQL
A hype-free guide to GraphQL for server-side developers, with a touch of snark

## Introduction

### What is GraphQL
GraphQL is a new RPC system. That is, it is in the same category as REST, Webservices/SOAP, gRPC, XML-RPC and CORBA.

### Advantages
The key distinctive of GraphQL is that it gives the API client fine-grained control over the fields returned from an API call (the data shape). This addresses a number of issues around over-requesting, that are present in most other RPC systems.

### Disadvantages
GraphQL is not a mature technology. A number of operational and development considerations are not adequately addressed at the moment (as of late 2019).

## Requests

### Network Protocol
Requests are implemented as a text body in a HTTP(S) POST to a single URL (it is also possible, but unwise, to use HTTP GET with a URL-encoded GraphQL request). Responses always have HTTP status code 200.

### Operations
There are 3 types of request (called "operations"). Functionally, here's what they mean

1. "query": Function call with parameters, parallel execution, structured response
2. "mutation": Function call with parameters, blocking sequential execution, structured response
3. "subscription": Function call with parameters, structured response with server-push streaming data

### Errors
Over the wire, responses always have HTTP status code 200, even if there was a functional error. However, GraphQL clients should also be prepared to handle HTTP 500 (for catastrophic server errors) and network errors.

There is an unofficial extension for embedding error information into the graphql response (Apollo error format). There is a further extension-extension for embedding error codes into the error information for programmatic error handling (`error_code` field). However, there are no extension-extension-extension's for well-defined error codes or annotating your schema to indicate valid error codes for particular fields or operations

## Types

### Gotchas
* input types (`input`) are different from return types (`type`). This is a bad idea.
* input types have a lot of limitations. No good reason, just cause.
* Interfaces don't add much value - you still need to repeat the itnerface fields in the concrete type . It's worth noting that every graphql type is an interface (strictly speaking)
* Unions cause a lot of problems. They reflect bad API design, they require confusing queries, and they generate bad code both client-side and server-side

### Deprecation
* Use an annotation to do deprecation for fields on output types
* You can't deprecate fields on an `input` type.

