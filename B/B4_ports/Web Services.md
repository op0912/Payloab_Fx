# Web Services

Ports in this section are related to web communication between clients and servers.

They allow:
- accessing websites and web applications
- exchanging requests and responses over the web
- delivering web content securely or insecurely
- HTTP and HTTPS are application layer protocols, not services themselves
- They define how communication happens between a client and a web server
- Web services (e.g. websites, APIs, applications) use HTTP/HTTPS to operate
- Examples include platforms like Google, Facebook, or any web-based application

---

## Port : 80 / 8080
- 80 → HTTP (default)
- 8080 → HTTP (alternative)

## Name : HTTP (HYPERTEXT TRANSFER PROTOCOL)

### Description
- HTTP is an application layer protocol used for communication between clients and web servers
- A client sends a request to a server, and the server responds with the requested resource
- It is the foundation of data exchange on the web (websites, APIs, applications)
- HTTP is stateless, meaning each request is independent

### How it communicates
- HTTP uses a request/response model:
  - client → sends request
  - server → sends response

- Transport layer:
  - TCP

- Common structure of an HTTP request:
  - Method (e.g. GET, POST)
  - Headers (metadata)
  - Body (data, optional)

- Example:
  GET /index.html HTTP/1.1
  Host: example.com

### How it can be attacked
- Man-in-the-Middle (MITM):
  Traffic is not encrypted and can be intercepted
- Request manipulation:
  Attackers can modify headers, parameters, or methods
- Injection attacks:
  Malicious input can be sent through HTTP requests (e.g. SQL injection)
- Session hijacking:
  Tokens or session data can be captured if not protected

### Observation
-

### Notes 
- HTTP is not encrypted, making it insecure for sensitive data
- Although it uses port 80 by default, it can run on alternative ports (e.g. 8080)
- HTTP is widely used for web applications and APIs
- HTTPS is the secure version of HTTP using encryption (TLS)

### What it means if open
- Web service is exposed
- Communication is not encrypted
- Data can be intercepted or modified
- Potential entry point for web application attacks
---

## Port : 443
### Name : HTTPS (HYPERTEXT TRANSFER PROTOCOL SECURE)

### Definition
Secure web communication between a client and a server using HTTP over TLS

### How it communicates
- Client sends HTTPS request
- Server responds with encrypted data
- Uses TCP with TLS encryption

### What it means if open
- Secure web service is exposed
- Web application or API is accessible
- Communication is encrypted

### How it can be attacked
- Misconfigured TLS (weak versions, weak ciphers)
- Certificate issues (self-signed, expired, invalid)
- Web application vulnerabilities (same as HTTP)
- Possible downgrade to HTTP if not enforced

### Observation
-

### Notes
- Encryption does not mean the application is secure
- Most modern applications use HTTPS by default
- Requires valid certificates to ensure trust

### Quick interpretation
- 80 open → unencrypted web communication
- 443 open → encrypted web communication
