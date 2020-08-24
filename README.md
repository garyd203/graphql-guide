# Pragmatic GraphQL
A hype-free guide to GraphQL for server-side developers, with a touch of snark

## Introduction

### What is GraphQL
GraphQL is a new RPC system. That is, it is in the same category as REST, Webservices/SOAP, gRPC, XML-RPC and CORBA.

### Advantages
The key distinctive of GraphQL is that it gives the API client fine-grained control over the fields returned from an API call (the data shape). This addresses a number of issues around over-requesting, that are present in most other RPC systems.

### Disadvantages
GraphQL is not a mature technology for general-purpose use. A number of operational and development considerations are not adequately addressed at the moment (as of late 2019).

## Community

### Context
The GraphQL movement is actually 3 things:
1. The internal communication protocol for a specific technology stack (Apollo/Relay).
2. A reaction against some of the more onerous aspects of the dominant RESTful approach to implementing API's, with it's roots in a specific part of the software engineering community.
3. A tool for creating flexible general-purpose API's.

It is helpful to remember this context because whilst a lot of the online discussion about GraphQL appears to be about point 3 (GraphQL as an API technology), in reality it is often about points 1 or 2. I suspect sometimes the authors are not clear on this distinction either :-/

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
* Interfaces don't add much value - you still need to repeat the interface fields in the concrete type . It's worth noting that every graphql type is an interface (strictly speaking)
* Unions cause a lot of problems. They reflect bad API design, they require confusing queries, and they generate bad code on both client-side and server-side

### Deprecation
* Use an annotation to do deprecation for fields on output types
* You can't deprecate fields on an `input` type (!)

## About Me
I have been a professional ("paid") software developer for about 2 decades now. I have created and maintained general-purpose GraphQL API's in production.
Previously I have had extensive experience with RESTful API's, and before that Webservices/SOAP, JSON-RPC, ICE, XML-RPC, CORBA and so on.

Consequently I can give you some good reasons why SOAP in particular was a mess and why the RESTful movement was revolutionary in that context. Of course, nobody needs to know or understand this in order to benefit from GraphQL - but it provides me with the clarity and perspective to find the good in a movement that consciously rejects REST, whilst avoiding the pitfalls of history.
