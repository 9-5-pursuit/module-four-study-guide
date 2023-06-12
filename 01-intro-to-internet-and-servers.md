# Intro to the Internet and Servers

## Components of the Internet

| Term | Definition |
| ---- | ---------- |
| __Computer&nbsp;Networks__ | Networks that allow the connection of two or more computers to exchange and share data and resources. They can be set up by location, such as a company office, metropolitan area, or global network. |
| __Internet__ | A global computer network that uses the Internet protocol suite (TCP/IP). It encompasses public and private networks and enables communication between various networks worldwide. |
| __Web__ | The World Wide Web (WWW), a subset of the internet, accessible through web browsers like Chrome, Firefox, or Safari. Websites on the web often have URLs starting with "www." |

- What is the purpose of computer networks?
- What is the internet and what protocol does it use?
- Differentiate between the internet and the World Wide Web (WWW).

---

## Components of a Request-Response Cycle

| Term | Definition |
| ---- | ---------- |
| __Client__ | Any device or software that connects to the internet and makes requests to servers. Clients can be web browsers, mobile apps, or other applications. They initiate requests to servers and receive responses. |
| __Server__ | A computer that receives requests from clients and responds to those requests. Servers are dedicated computers designed to handle requests, provide resources, and process data. They can be web servers, email servers, or other types of servers. |
| __Request-Response Cycle__ | The interaction between clients and servers, where clients send requests to servers, and servers respond with the requested data or perform requested actions. It forms the basis of communication in web applications. |

- Define a client and a server in the context of web applications.
- Describe the process of the request-response cycle.
- What is the role of servers in handling client requests?

---

## Databases

| Term | Definition |
| ---- | ---------- |
| __Database__ | A computer program that stores electronic data in organized collections. It manages data and allows clients to access and interact with the data through servers. Examples include databases storing user information, product data, or other structured information. |

- What is a database and what is its purpose?
- How does a server interact with a database?
- Give an example of a type of information stored in a database.

---

## Requests and Responses

| Term | Definition |
| ---- | ---------- |
| __HTTP__ | HyperText Transfer Protocol, the protocol used for communication between clients and servers over the internet. It allows for the transfer of various data types, including HTML, JSON, images, etc. |
| __URL__ | Uniform Resource Locator, a string of text characters that identifies the address of a resource on the internet. URLs are used in requests and responses to locate and access resources. They consist of components such as the protocol, host/domain name, port, path, query string, and hash/fragment. |
| __Header__ | The metadata included in the HTTP request or response that provides essential information about the request or response. It includes details such as the URL, request method, content type, and status code. |
| __Body__ | The optional part of an HTTP request or response that contains data or content. For example, in a request, the body may include form data entered by a user, while in a response, it may contain HTML content to be rendered by a browser. |

- What does HTTP stand for and what is its purpose?
- Explain the components of a URL.
- What is the difference between the header and body in an HTTP request or response?

---

## HTTP Protocol

| Term | Definition |
| ---- | ---------- |
| __Request&nbsp;Methods__ | The four primary ways to interact with data through HTTP: POST (create), GET (read), PUT/PATCH (update), and DELETE (destroy). These methods correspond to the CRUD operations (Create, Read, Update, Delete) commonly performed on data. |
| __HTTP Status Codes__ | Numerical codes included in the HTTP response that indicate the status of the request. Status codes in the range 100-399 confirm the request/response is OK. Codes in the 400s denote user errors, while codes in the 500s denote server errors. They provide information about the success or failure of the request and the reason for the failure. Common status codes include 200 (OK), 404 (Not Found), and 500 (Internal Server Error). |

- Name the four primary request methods in HTTP and their corresponding CRUD operations.
- How do HTTP status codes provide information about a request's outcome?
- Give examples of HTTP status codes for successful requests and common client/server errors.

---