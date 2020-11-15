# Designing For Software Security Engineering

## Threat Modeling
The full report from the Microsoft Threat Modeling Tool can be viewed at https://vidmaster.github.io/cybr8420-group4/DFD_Final.htm, with the raw HTML accessible at https://github.com/Vidmaster/cybr8420-group4/blob/master/DFD_Final.htm.

For the purposes of this project, we found the model above to capture all of the critical interactions of the system and their associated vulnerabilities. Other flows relating to our other assurance cases or use cases simply replaced the ordering service interactions with a differently named process or removed it entirely, and did not introduce any new threats to the model.

## Observations
### Relation to Spring Security
When creating an account or logging in to the account, the user's account can be vulnerable to password-related attacks such as dictionary attacks. Spring security can stop these attacks by using Pre-Authentication Scenarios; this is where Spring security Authenticates and then waits for external authentication from SiteMidner or Java EE security to authenticate before it allows account access. Pre-Authentication can also stop credential stuffing and unauthorized password changing. 

Another attack against a user's account can be brute force, to stop brute force spring security can implement an Authentication Failure Event Listener. The Listener will record all authentication failures. If a user fails more than a predetermined amount, the account will be locked for 24 hours and the IP address that is linked to the attempt will be stored.

The login password can be vulnerable to MITM attack, as the password is sent in plaintext to the authentication service where it is checked against a hashed value to determine if it matches. Pre-Authentication would not stop this attack, it would just stop the Attacker from gaining immediate access to the account. Salting and Hashing passwords before sending to the database, then only sending thru TLS sessions is the best way to stop MITM from getting anything of value.

Login can also be threatened by SQL Injection. SQL Injection could allow an attack to query the data base for passwords. SQL injection could also threaten the websites product information. SQL Injection could also threaten stored payment info. To stop or mitigate this attack Spring Security uses DelegatingPasswordEncoder and PasswordEncoderFactories which allows the security expert to implement the latest changes such as salting and hashing all data at rest with bcrypt. This also allows for implementing SQL sanitizations so that SQL code can not be ran out of the proper environment. An extra step is involved for stored payment info and that is to not store the CVV. Spring security can also encrypt credit card numbers.    

To mitigate the website from being attacked by Cross Site Scripting (XSS), Spring Security uses Security HTTP Response Headers, Spring Security also disables content sniffing so that polyglots cannot be used to perform a XSS attack. Spring Security can also use Content Security Policy to mitigate XSS.

To stop privilege escalation in the website Spring security can use DelegatingSecurityContentExecutor which can wrap any Runnable that is passed to the execute method. This keeps the same Security Content for every Runnable submitted. Spring Security can also use WebInvocationPrivilegeEvaluator in the application context. This can test web requests by creating dummy requests and test if they succeed or fail.

The primary design flaw we encountered in Spring Security is that while it is possible to implement a number of these security measures, the defaults and provided implementations are typically not viable for a production system. This typically leaves developers in a situation of going to Stack Overflow and finding an implementation for some extremely common behavior, such as capturing failed login attempts. It could be beneficial to add some more robust solutions to common problems to the project that would work in many production environments but could be extended or replaced entirely if more advanced custom functionality was necessary.

### GitHub Project Board
Our project board for this assignment can be found at https://github.com/Vidmaster/cybr8420-group4/projects/4.

### Teamwork Reflection
For this Data Flow Diagram (DFD) project, the team completed the videos and quiz earlier, so that we could spend more time focusing on the content of the project. 

We used the Microsoft Threat Modeling Tool to create our DFDs and quickly noticed that unlike the Lucid Chart application, the TMT app did not allow multi-user collaboration.  We overcame this limitation by Zipping our files and sharing them via Slack. This allowed the team to build on each other’s work without wasting time re-drawing the same models.

We had a productive team meeting prior to this project’s meeting with the instructor. This was a major benefit because we were able to receive valuable feedback from our instructor about some of our initial DFDs, and that helped us move forward with a better idea of how to model the addition DFDs required of the project.

Our teamwork continues to improve with each project, and we are able to quickly adapt in order to accommodate when team members have personal issues to overcome during the project. As in previous projects, we have had members taking care of family members and covering extra shifts at work due to COVID-19 quarantines. 
