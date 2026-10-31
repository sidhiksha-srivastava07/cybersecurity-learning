<img width="1470" height="839" alt="Screenshot 2026-10-31 at 5 31 25 PM" src="https://github.com/user-attachments/assets/a353f1fb-e100-4878-8e49-29b1d50aec7c" /># Reissuing Requests with Burp Repeater

## Platform

PortSwigger Web Academy

## Lab / Exercise

Reissuing requests with Burp Repeater

## Objective

The objective of this exercise was to learn how to use Burp Repeater to repeatedly send an HTTP request with different input values and 
analyze how the server responds.

The lab demonstrated how Repeater can be used to investigate unexpected application behaviour and identify an information disclosure 
vulnerability.

## Tools Used

- Burp Suite
- Burp Proxy
- Burp Repeater
- PortSwigger Web Security Academy

## Methodology

1. Accessed the deliberately vulnerable shopping website using Burp's browser.
2. Observed requests made while browsing the product pages.
3. Identified a 'GET /product' request containing a 'productId' query parameter.
4. Sent the request from Burp Proxy's HTTP history to Burp Repeater.
5. Used Repeater to resend the request multiple times with different 'productId' values.
6. Compared the server responses for different inputs.
7. Tested unexpected input by supplying a string ('test') instead of the expected integer value.
8. Observed that the server returned a verbose error response containing a stack trace.
9. Examined the error response and identified the web framework ('Apache Struts') and its version ('2 2.3.31').
10. Submitted the discovered framework version to the lab and successfully completed the exercise.

## Request Analysis

The interesting request contained a parameter similar to:

GET /product?productId = [integer value]

The 'productId' parameter appeared to expect an integer.

Using Burp Repeater, I modified this parameter and resent the request repeatedly without intercepting a new request each time.

This allowed me to compare the application's responses to both expected and unexpected input.

## Finding

When unexpected input (a string) was supplied to the 'productId' parameter, the application returned a verbose error response containing a 
stack trace.

The response disclosed information about the web application framework, including its version.

The lab revealed that the application was using 'Apache Struts 2.3.31'.

## Vulnerability / Security Issue

The exercise demonstrates information disclosure through verbose error messages.

The application exposed internal implementation details when it encountered unexpected input. 
In a real application, detailed stack traces and framework version information should not be returned to users because such information can 
help an attacker understand the application's technology stack and identify potentially relevant vulnerabilities.

## Evidence

Evidence from the exercise includes:

    # The original 'GET /product' request + the request sent to Repeater:
<img width="1470" height="842" alt="Screenshot 2026-10-31 at 5 24 01 PM" src="https://github.com/user-attachments/assets/1d2f2291-804e-47c2-94a7-6b2f8967d048" />

    # Different 'productID' values tested using Repeater:
<img width="734" height="273" alt="Screenshot 2026-10-31 at 5 26 17 PM" src="https://github.com/user-attachments/assets/287cceec-f93e-4f62-a4ad-8f62a0066666" />

    # The unexpected input (productID=test) + verbose error response showing the disclosed information + the disclosed framework/version 
    information (Apache Struts 2 2.3.31):
<img width="737" height="827" alt="Screenshot 2026-10-31 at 5 28 45 PM" src="https://github.com/user-attachments/assets/0fe2d017-c896-4569-9d77-2fbefdf47707" />

    # Successful lab completion
<img width="1470" height="846" alt="Screenshot 2026-10-31 at 5 31 47 PM" src="https://github.com/user-attachments/assets/eb9b0c5b-764a-4a5f-a531-99f6189a23e6" />

## Key Learning

This exercise helped me understand that:

- Burp Repeater allows an HTTP request to be modified and resent repeatedly.
- Repeater is useful for testing how an application responds to different inputs.
- Comparing responses can reveal unexpected application behaviour.
- Unexpected input can sometimes trigger verbose error messages.
- Error messages can disclose sensitive technical information such as frameworks and versions.
- Burp Repeater is useful for manually investigating and confirming potential vulnerabilities.

## Remediation

Applications should avoid exposing detailed technical errors to users.

Recommended measures include:

- Return generic error messages to users.
- Do not expose stack traces in production output.
- Avoid revealing framework and software version information through error responses.
- Log detailed errors securely on the server instead.
- Validate and handle unexpected input safely.

## Status

Completed — 31 October 2026

## Reference

PortSwigger Web Security Academy — Getting Started: Reissuing requests with Burp Repeater
