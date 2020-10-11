# Assurance Cases for Software Security Engineering

## Top Level Claims
LucidChart diagrams for the following can be found at https://app.lucidchart.com/invitations/accept/6b240b88-099a-4812-8fa8-2c0a375d9efe

### Claim 1
The application securely stores personal and financial data

![Assurance claim 1](/images/claim1.png)

### Claim 2
Users can't access application resources for which they are not authorized

![Assurance claim 2](/images/claim2.png)

### Claim 3
The website mitigates fradulent purchases

![Assurance claim 3](/images/claim3.png)

### Claim 4
Authentication protocols prevent unauthorized access to a user's account

![Assurance claim 4](/images/claim4.png)

### Claim 5
The website secures online purchases

![Assurance claim 5](/images/claim5.png)

## Alignment with Spring Security
In our assurance cases, we present a number of pieces of supporting evidence. For each of these pieces, we will discuss whether it aligns with functionality provided by Spring Security or not. If it does not align with Spring Security we will also discuss whether it might be a good candidate for inclusion in the framework in the future.
### Evidence in Claim 1
1. AES encryption module in Sprig Security - Spring Security provides an [Encryptors module](https://github.com/spring-projects/spring-security/blob/master/crypto/src/main/java/org/springframework/security/crypto/encrypt/Encryptors.java) which by default uses AES encryption with a 256 bit key in Galois Counter Mode (GCM). This module is primarily targeted at password encryption, but due to the reversible nature of the functions used it is also suitable for simple data encryption.
2. FIPS-compliant Hardware Security Module - Currently Spring Security does not provide any functionality for interfacing with a hardware security module, and users are required to implement their own functions or use another library to support this. An [open issue exists](https://github.com/spring-projects/spring-security/issues/8349) to address this functionality in the project backlog.
3. HSM security audit - This type of assurance artefact would be out of the scope of a library such as Spring Security
4. Spring Security HTTPS Configuration - In Spring Security's HTTP Filter Chain, a filter which calls `ServerHttpSecurity.redirectToHttps()` can be added to always forward traffic to HTTPS. Additionally, in the security configuration, the `requiresSecure()` method can be used on matchers to require communication over HTTPS as discussed in [this tutorial](https://www.baeldung.com/spring-channel-security-https).
5. Password creation policy - Spring Security does not provide any utilities for enforcing a password creation policy. This is typically enforced through regular expressions, but it could be beneficial to add a simple utility for checking password strength which provides accepted default patterns that can be used easily.
6. Password rotation policy - Spring Security does not provide any utilities for tracking or enforcing password rotation, as this is highly dependent on how the user data is stored. Because of the modular approach taken by Spring, this sort of utility would be out of the project's scope.
7. Web server configuration - The enforcement of particular SSL/TLS versions typically belongs to the specific web server being used, such as Tomcat or Jetty. This configuration can be enforced by passing in flags to the server or using environment variables.

### Evidence in Claim 2
1. Spring HttpSecurity configuration - One of the fundamental components of Spring Security is the `HttpSecurity` class and its associated configuration. A configuration will use `antMatchers` to specify paths and then provide access rules for each one. These rules are executed in sequential order, and would typically be configured from most to least specific. A sample configuration [can be found in the API documentation](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/config/annotation/web/builders/HttpSecurity.html) which restricts access to all (`/**`) resources unless the user has the role `USER`, and redirects to form-based login if the session is not authenticated.
2. Static analysis report - Spring Security does not provide any mechanisms for conducting static analysis, and this type of functionality would be provided by an external application such as SonarQube or Fortify typically.
3. Role mapping review - Spring Security does not provide any mechanisms for analyzing how HTTP endpoints are secured. The related project Spring Boot Actuator can be enabled in a project and the endpoing `/actuator/mappings` called to show a list of all MVC mappings in the application, but this doesn't show what roles or authorities can access each one, whether HTTP or HTTPS is enforced, etc. This is an a feature which could be useful to implement, but it would likely need to be added to Spring Boot Actuator instead of Spring Security.
4. HttpSecurity configuration contains default denyAll rule - Similar to the discussion of claim 1 above, this would be accomplished with a final statement in the `HttpSecurity` configuration such as `http.antMatchers("\**").denyAll()`. Such a statement would require a more specific authorization rule to be configured for any newly added HTTP endpoints in the application, and would render them inaccessible until such a rule was configured. This serves as a safeguard against developers forgetting to secure their methods. Unfortunately the only way of knowing such a rule is present and enforced is by reviewing the code.
5. Spring HttpSecurity authorizeRequests rules - Similar to claim 1 above, these rules would be coded into a security configuration class and implemented from most to least specific. Unfortunately these rules would need to be audited by reviewing the source code of the application.

### Evidence in Claim 3
1. Claim 1 used as supporting evidence - Kept for numbering consistency. See claim 1 above.
2. CVV Entry Module - Spring Security does not provide any functionality for credit card processing or validation. This functionality would typically be handled by another library developed by a payment services provider.
3. Salt Function For Transactions - Spring's password encoder previously required a user provided SaltSource, but this has been removed in recent versions and salting has been integrated into the `Encryptors` module.

### Evidence in Claim 4
1. Account sign-on network traffic logs - Spring Security doesn't specifically provide for network traffic logs, as this would be captured outside of the application. Spring Boot Actuator does provide some functionality for capturing [audit events](https://docs.spring.io/spring-boot/docs/current/actuator-api/html/#audit-events) when users log in or out of the application, and logging libraries can easily be integrated into the application to capture these events as well.
2. Account creation logs - Spring Security does not provide logs of account creation, but logging libraries can easily be integrated to provide this functionality and capture relevant information.
3. Audit report of Account creation logs - Log auditing and integrity checking is not provided by Spring Security and would typically be handled outside of the application producing the logs.
4. Password creation code review - Similar to the discussion in Claim 1 #5 and #6 above, Spring Security doesn't provide specific mechanisms for enforcing password complexity rules. The default password encoder used in Spring Security is BCrypt with 10 rounds and a salt, and other password hashing functions such as SHA-256 are available as well. BCrypt is widely regarded as secure, but with a goal of checking a password in roughly 500ms on modern computers, the default 10 rounds falls somewhat short, making the default hash easier to brute force than it should be.

### Evidence in Claim 5
1. Payment Data Audit logs - Spring Security doesn't provide any functionality around payments or logging, so this behavior would need to be captured in another library or built into the application.
2. Network Traffic logs - Spring Security doesn't provide functionality for capturing and logging network traffic, and this behavior would be most appropriate to implement in other software. One thing that can be done easily within Spring however is the addition of a simple HTTP request/response logging filter that lives in Spring's filter chain and logs some or all HTTP requests that come through the application.
3. Review of Network Traffic enforcement code - Such a review would be conducted outside the scope of our hypothetical application or Spring Security.
4. Spring Security HTTPS Configuration - Same evidence as Claim 1 #4.
5. Web server configuration - Same evidence as Claim 1 #7.


## Project Board
The project board for this assignment is located at https://github.com/Vidmaster/cybr8420-group4/projects/3


## Teamwork Reflection
Based on what we learned on the last assignment, we started working on this together to give our group a better sense of how this project needed to be done. After meeting with the professor we found that we were going into too much depth on some of the cases, and should focus more closely on claims that are appropriate to make about Spring Security and its capabilities. What we had done was correct but we were making it too hard on ourselves by making broad claims about the system rather than more specific ones around Spring Security. As with the last assignment we had to work around our jobs again, this has been a issue with Bryan as he has had to work late hours multiple times. Bob needed family time over the weekend, and worked hard to get a lot of the claim work done before he left. Henry also had issues with work this week and is taking care of his injured dog.

Overall our teamwork felt improved on this assignment, with our main challenges being externally motivated and difficult to anticipate. As usual, the team has done a good job of picking up each other's slack where necessary. Our goal for next assignment is to get the team through the lectures and quiz earlier so our first team meeting can be more productive, and the second one can be used to finalize details. Currently we've had to cancel or cut short several of the early meetings because the majority of the team hasn't gone far enough on the module to have a discussion around the assignment, but we're also unable to easily move the meeting due to everyone's scheduling constraints.
