# Getting Started: Modifying HTTP Requests with Burp Proxy

## Platform

PortSwigger Web Security Academy

## Lab / Exercise

Getting Started: Modifying HTTP Requests with Burp Proxy

## Objective

The objective of this exercise was to learn how to use Burp Proxy to intercept, inspect, and modify HTTP requests sent by a web application.

The lab used a deliberately vulnerable shopping website provided by PortSwigger Web Security Academy.

## Tools Used

- Burp Suite
- Burp Proxy
- PortSwigger Web Security Academy

## Methodology

1. Opened the deliberately vulnerable shopping website using Burp's browser.
2. Logged into the provided shopping account.
3. Selected a product and added it to the shopping cart.
4. Enabled interception in **Proxy → Intercept**.
5. Captured the `POST /cart` request generated when adding the product.
6. Inspected the request and identified the `price` parameter in the request body.
7. Modified the value of the `price` parameter.
8. Forwarded the modified request to the server.
9. Verified that the product was added to the cart using the modified price.
10. Completed the lab successfully.

## Findings

The intercepted request contained parameters including:

productId
redir
quantity
price

The important parameter for this exercise was:

price

The application accepted the price value supplied in the client-side HTTP request instead of enforcing the correct price on the server.

This allowed the request to be modified using Burp Proxy.

## Vulnerability / Security Issue

The lab demonstrates **excessive trust in client-side controls**.

The application relied on a value supplied by the client when processing the product price. 
Since HTTP requests can be intercepted and modified before reaching the server, client-side restrictions should not be treated 
as security controls.

An attacker who can modify the request could potentially alter values that should instead be controlled and validated by the server.

## Evidence

The lab was successfully completed in PortSwigger Web Security Academy.

Evidence captured during the exercise includes:

- Intercepted `POST /cart` request
- `price` parameter identified in the request
- Modified request forwarded through Burp Proxy
- Product successfully added using the modified price
- PortSwigger completion confirmation

      #Intercepted `POST /cart` request and `price` parameter identified in the request:

<img width="1012" height="576" alt="Screenshot 2026-10-27 at 8 07 45 AM" src="https://github.com/user-attachments/assets/5d7da325-8ae6-405f-84ed-361333555266" />


    #Modified request (price changed to 1) forwarded through Burp Proxy:
    
<img width="1013" height="572" alt="Screenshot 2026-10-27 at 8 07 59 AM" src="https://github.com/user-attachments/assets/bee16fbc-8dce-4fee-8bba-6444a080f23b" />


    #Product successfully added using the modified price and PortSwigger completion confirmation:
    
<img width="1470" height="830" alt="Screenshot 2026-10-26 at 11 23 11 PM" src="https://github.com/user-attachments/assets/aed70a10-8500-4e0c-aee7-709efb2d7076" />

## Key Learning

This exercise helped me understand that:

- HTTP requests can be intercepted before reaching the server.
- Burp Proxy can be used to inspect and modify HTTP requests.
- Parameters sent by the client should not automatically be trusted by the server.
- Security-sensitive values should be validated and enforced server-side.
- Burp Proxy is an important tool for web application security testing.

## Remediation

Applications should not rely on client-controlled values for security-sensitive operations.

For example, the server should determine the actual product price from trusted server-side data rather than accepting the price supplied by the client.

Server-side authorization and validation should always be enforced even when client-side controls are present.

## Status

**Completed — 26 October 2026**

## Reference

PortSwigger Web Security Academy — Getting Started: Modifying HTTP Requests with Burp Proxy
