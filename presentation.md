Understanding Frontend Security

Hello my name is Anton and today i would like to Speak with about Understanding Frontend Security.
As the web is growing, modern web applications are changing rapidly. Frontend code, now, shares almost equal responsibility as the backend code, if not more.
This means a client, has become more complex, does more things, and hence is more powerful. But with great power comes great responsibility.
To do all of the things safely, we need a better security model for client-side code. In this presentation, we will be discussing how to not fail our users and protect them from the potential perpetrators.
We will be discussing various security issues, types of attacks and preventive measures against them to build a secure frontend. Let’s dive right into it.

Cross-Site Scripting (XSS) Attack — XSS is a type of attack in which an attacker inputs a malicious script into the web application. When other users access the web application, since the browser does not know that it is malicious as it was served by the backend, this malicious script is executed.
Let’s understand it better using this diagram.
a) An attacker with a malicious script accesses the application.
b) He fills up a form and inputs malicious script in the form field.
c) The malicious script reaches back-end systems via a form field data and is saved in the database.
d) When some legitimate user accesses the application, he is served with the malicious script by the application’s backend. The browser doesn’t know it is a malicious script and executes it.
The script could do anything like it can expose and send the user’s session token, cookies, etc to the attacker’s remote server.
Prevention -
•	Filter input on arrival- When the input is received, filter data based on what is expected or valid input.
•	Encode data on output- When user-controllable data is provided in HTTP responses, encode the output to prevent it from being executed by HTML parser. Depending on the output context, this might require applying combinations of HTML, URL, JavaScript, and CSS encoding.
•	Use appropriate response headers- To prevent XSS in HTTP responses that aren’t intended to contain any HTML or JavaScript, we can use the Content-Type and X-Content-Type-Options headers to ensure that browsers interpret the responses in the way you intend. Eg. A JSON data should never be encoded as text/html, to prevent it from accidental execution.

Cross-Site Request Forgery (CSRF) — CSRF is an attack that tricks the victim into submitting a malicious request.
If a user is currently authenticated to a website, any HTTP requests made to that website will have any credentials associated with the site, such as the user’s session cookie, IP address, etc, automatically attached to it.
If the request is initiated by an attacker, when this request reaches the backend, the server will have no way to distinguish between a malicious request and a legitimate request.
CSRF attacks target functionality that causes a state change on the server, such as changing the victim’s email address or password or purchasing something.
How does the attack work?
Suppose a user John is logged in to his net banking website (http://bank.com). He receives a malicious mail from an attacker :
Using GET Request —
•	The email can contain a bank’s URL which is disguised as an ordinary link, and when John clicks on it, the browser makes a GET call with all the credentials of John’s user session on his net banking website.
•	Or the email can simply render a 0 X 0 image with the bank’s URL which triggers a GET request automatically.

Using POST Request
•	If the bank does not allows GET requests for such transactions, the attacker can trick John to make a POST request by tricking him to click on malicious URL. This redirects John to a website where this malicious form is executed.
The user just has to press the submit button, but this can also be executed using javascript.

Prevention -
For every session of a user, the server should generate a randomized token (CSRF Token) and send it to the client. The client can save the token, from where javascript can read it.
When a web application is making an HTTP request, the application should include that randomized token (CSRF Token) in the header of each request.
The value of this token should be randomly generated such that it cannot be guessed by an attacker. We should use a well-known hashing algorithm such as SHA256/512 for generating tokens.
When the request is made from the application, the server must verify the existence and validity of the token in the request compared to the token found in the user session. If the token was not found within the request, or the value provided does not match the value within the user session, then the request should be dropped, and the event can be logged as a potential CSRF attack in progress.

DOS (Denial Of Service) Attack — DOS attack is a cyber-attack in which a perpetrator seeks to make a server resource unavailable to the actual users by disrupting the services of a server connected to the internet.
This attack is carried out by overloading the system by a huge number of requests in a very short interval of time (every millisecond) and prevent legitimate requests to be served.
In a distributed denial-of-service attack (DDoS attack), the incoming traffic flooding the victim originates from many different sources. This effectively makes it impossible to stop the attack simply by blocking a single source/IP address.
Prevention — Using Captcha at public-facing endpoints (login, registration, contact) — a captcha is a computer program or system intended to distinguish humans from bots.
Most of the DOS attacks are carried out using bots. Captcha identifies bots and prevents them from making requests.
Google’s reCaptcha is a highly advanced service to protect bots from abusing your applications.

Now I'd like to give few tips how to improve frontend security and no get hacked. 
1. Security must be part of the development process
2. Use a modern framework that handles security automatically 
3. Avoid typical XSS mistakes
4. Consider Trusted Types
5. Consider using textContent instead of innerHTML
6. Compartmentalize your application 
7. Be careful when using Google Tag Manager
8. Be more selective with third-party scripts
9. Audit your dependencies
10. Use Subresource Integrity for third-party CDN hosting
11. HTML encoding is not enough
12. Implement Content Security Policy
CSP is a mechanism to significantly reduce the risk and impact of XSS attacks in modern browsers.
13. Be mindful of what you’re exposing

And at the end of this presentation I want to say that security at the frontend code is, sadly, often overlooked. It is something that should be considered as a top priority. Something, which cannot be bargained with. Only then we can ensure a secure ecosystem of the users and applications.
We as the builder of these applications should always strive for a security-first approach. I hope this article provided you useful insight into web security.
Thanks for attention!


