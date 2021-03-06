# Team 4 Project Proposal

CYBR8420 Software Assurance, University of Nebraska Omaha, Fall 2020

## Proposed Software

Our proposed software for this semester's project is [Spring Security](https://spring.io/projects/spring-security), one of the components of the [Spring Framework](https://spring.io/). This project can be found on GitHub at https://github.com/spring-projects/spring-security. Our team is tentatively planning to address [an issue pertaining to the default cycles used by BCrypt, SCrypt, and Argon2](https://github.com/spring-projects/spring-security/issues/7411) but may change course as needed.

## Hypothetical Operating Envrionment

Spring Security is commonly used for securing websites and APIs, so we will consider the hypothetical eCommerce website SpringStore for the purposes of this exercise. SpringStore is the world's top online seller of springs and spring paraphernalia, and has thousands of users who purchase springs and write product reviews. SpringStore also provides functionality for businesses to sell their own springs through their website, and offers both a web interface and a rich API to these 3rd party sellers for managing their inventory and sales. SpringStore allows users to register using an email and password or via external authentication through Facebook and Google.

Users of SpringStore expect that their accounts are secured via strong password encryption, and that their saved payment information is encrypted at rest. Users also expect that other users don't have access to their accounts or order history, and that fraudulent orders can't be placed on their behalf. 3rd party sellers using SpringStore expect that their vendor accounts are only usable by authorized members of their company, and that their inventory and prices can't be tampered with by unauthorized users. SpringStore as a company expects to provide security and privacy to its users, and to have their backend systems secured against threats so that customer data can't be compromised, financial data can't be tampered with, and confidential company operating data won't be exposed. 

### Systems Engineering View Diagram
![System Engineering View](https://github.com/Vidmaster/cybr8420-group4/blob/master/ProjectSEV.png)

### Threats perceived by users

Users of SpringStore are aware of the countless security breaches other eCommerce sites have had over the years. Hackers may try to attack a website directly to place fraudulent orders, may use stolen credit card information to order products, or may try to compromise backend services to steal user information which is then used or resold on the dark web. Individual user accounts may also be compromised by phishing attempts, and insecure passwords could be easily broken and used to place fraudulent orders or even update reseller prices and inventory. The owners of SpringStore are also aware of attacks such as denial of service and SQL injection, and work hard to prevent these from occurring.

### Security features in the software

SpringStore makes use of Spring Security to keep their springs secure. To keep passwords safe, they use Spring Security's provided BCrypt hashing algorithm so that an attacker would only recover irreversible hashes if a user database was compromised. Saved credit card information is encrypted in the database using Spring Security's AES encryption module. Requests made to all backend services are authenticated either using a username and password or by OAuth2 and JWTs. User and service accounts are assigned roles and authorities which allow access to the minimum functionality each account needs to do its job. These authorities are collected in Spring's Principal object, which is checked by the Filter Chain whenever a request is made against a backend service, and denied if the appropriate permissions are not present. Spring Security also provides protection against cross site scripting (XSS) and cross site request forgery (CSRF) through included modules, which sanitize data and restrict access to resources to only known origins.

## Team Motivation

Looking at the course syllabus learning objectives, our team chose to focus on a well-understood technical problem so that we could focus our attention on the open-source contribution process rather than the product itself. By picking a Java-coded, well understood program, we can spend less time learning the intricacies of an unknown language or spend overlong trying to ferret out a complex coding error, which is not the point of this course, and spend our time learning how to contribute to open source communities generally. 

Our specific choice for this software, Spring Security's password generation tools, are all written in Java and based on source material that has been translated into Java. Password generators are most effective when the amount of time necessary to generate a password is long enough to make brute force decryption sufficiently time intensive. Spring Software standards are for the process to take about one second. But as run now, three of the processes only take tens of milliseconds. Our goal would be to increase the time load for each of these generators in such a way that the increased load cannot be bypassed by someone attempting to break the cypher and retrieve the user's unencrypted password.

## Project Description

Spring Security is one component of the Spring Framework, and is focused on providing [authentication and authorization, as well as protection from common exploits](https://docs.spring.io/spring-security/site/docs/5.4.0/reference/html5/#features). Spring Security is meant to integrate with other libraries, which would provide functionality such as HTTP endpoints and database connectivity to a larger application. It is a very popular piece of the framework, being used in over 100,000 other projects on GitHub, and boasting over 400 contributors. The project was first released publicly in 2008, and the most recent release was version 5.4.0 on September 8, 2020. The Spring Framework is written almost entirely in Java, though some components are written in [Kotlin](https://kotlinlang.org/) as well. [OpenHub](https://www.openhub.net/p/spring-security) reports it to be nearly 270,000 lines of code, and provides a COCOMO estimate of 70 years of effort to create the library.

The Spring Framework as a whole is exceptionally well documented, and Spring Security documentation can be found at https://spring.io/projects/spring-security. This documentation includes API and reference documentation, as well as tutorials for simple tasks such as [securing a web app](https://spring.io/guides/gs/securing-web/) and [architecture overviews](https://spring.io/guides/topicals/spring-security-architecture) for the more advanced user. Numerous tutorials are available from other sources, such as [YouTube](https://www.youtube.com/watch?v=her_7pa0vrg), [Baeldung](https://www.baeldung.com/security-spring) and [javaTpoint](https://www.javatpoint.com/spring-security-tutorial) to introduce users to a variety of topics.

For this project we will be examining three password generators based on three different algorithms: Blowfish, SCrypt, and Argon2. While each of the password generators themselves are relatively short, the algorithms they run can be quite complex. We will have to be careful to adjust the parameters in keeping with the spirit, intent, and strengths of the original cyphers. 

The files we will be looking at are:
Note - all file paths begin with https://github.com/spring-projects/spring-security/tree/master/crypto/src/main/java/org/springframework/security/crypto/

BCryptPasswordEncoder.java, Dave Syer, 175 lines, ../bcrypt/BCryptPasswordEncoder.java \
Bcrypt.java, Damien Miller, 761 lines, ../bcrypt/BCrypt.java \
SCryptPasswordEncoder.java, Shazin Sadakath & Rob Winch , 186 lines , ../scrypt/SCryptPasswordEncoder.java \
Argon2PasswordEncoder.java, Simeon Macke, 144 lines, ../argon2/Argon2PasswordEncoder.java \
Argon2EncodingUtils.java, Simeon Macke, 176 lines, ../argon2/Argon2EncodingUtils.java

## Licensing and Contributions
Spring's Contributor Code of Conduct states that you will be banned if you:
* Talk about or share sexual explicit material
* If you troll
* Cyber bulling
* Plagiarize
* Engage in Unethical or Illegal behavior

Project maintainers will remove code, commits, or wiki edits, if these rules are violated. The Code of Conduct applies to the project both public and private space.

Additionally, the project provides some further guidance to contributors:
- Before submitting an issue Search GitHub to see if it is already reported.
- Discuss contribution with committers before submitting a pull request, if it is a bug fix or a typo correction that can be fixed with out bothering the committers.
- Fill out and submit the Contributor License Agreement located at https://cla.pivotal.io/sign/spring before you contribute.
- Create your branch from the master to be submitted as a pull request.
- Do not use long branch names pick short branch names. The example is the preferred branch name type. Example: pro-fixed.
- Follow whitespace and formatting convention. The formatting convention is in the Mind the whitespace section of CONTRIBUTING.adoc.
- Update spring-securityx.y.rnc for schema changes, do not change spring-securityx.y.xsd.
- Squash commits, examples are located here https://book.git-scm.com/4_interactive_rebasing.html.
- Use real name in your git commits.

The Spring framework uses the Apache License 2.0, so spring-projects/spring-security can be used for Commercial use. You can Modify and Distribute the code, and can use it in Patent use and Private use. You can not Trademark use, and there is no Liability or warranty provided.


## Security History of Spring Security

The Spring Security software is composed of several modules built with Java.  These modules provide security features for Spring-based applications. The latest stable release is Spring Security 5.4.0, which was released on September 8th 2020. 

As of September 9th 2020, the NIST NVD lists 5 records of reported vulnerabilities [1]. 
[CVE-2020-5408](https://nvd.nist.gov/vuln/detail/CVE-2020-5408)	Various versions prior to 5.3.2, used a fixed null initialization vector with CBC Mode in the implementation of the queryable text encryptor. A malicious user with access to the data that has been encrypted using such an encryptor may be able to derive the unencrypted values using a dictionary attack.

[CVE-2019-3795](https://nvd.nist.gov/vuln/detail/CVE-2019-3795)	Spring Security versions 4.2.x prior to 4.2.12, 5.0.x prior to 5.0.12, and 5.1.x prior to 5.1.5 contain an insecure randomness vulnerability when using SecureRandomFactoryBean#setSeed to configure a SecureRandom instance. In order to be impacted, an honest application must provide a seed and make the resulting random material available to an attacker for inspection.

[CVE-2018-1258](https://nvd.nist.gov/vuln/detail/CVE-2018-1258)	Spring Framework version 5.0.5 when used in combination with any versions of Spring Security contains an authorization bypass when using method security. An unauthorized malicious user can gain unauthorized access to methods that should be restricted.

[CVE-2018-1199](https://nvd.nist.gov/vuln/detail/CVE-2018-1199)	Spring Security (Spring Security 4.1.x before 4.1.5, 4.2.x before 4.2.4, and 5.0.x before 5.0.1; and Spring Framework 4.3.x before 4.3.14 and 5.0.x before 5.0.3) does not consider URL path parameters when processing security constraints. By adding a URL path parameter with special encodings, an attacker may be able to bypass a security constraint. The root cause of this issue is a lack of clarity regarding the handling of path parameters in the Servlet Specification. Some Servlet containers include path parameters in the value returned for getPathInfo() and some do not. Spring Security uses the value returned by getPathInfo() as part of the process of mapping requests to security constraints. In this particular attack, different character encodings used in path parameters allows secured Spring MVC static resource URLs to be bypassed.

[CVE-2017-4995](https://nvd.nist.gov/vuln/detail/CVE-2017-4995)	An issue was discovered in Pivotal Spring Security 4.2.0.RELEASE through 4.2.2.RELEASE, and Spring Security 5.0.0.M1. When configured to enable default typing, Jackson contained a deserialization vulnerability that could lead to arbitrary code execution. Jackson fixed this vulnerability by blacklisting known "deserialization gadgets." Spring Security configures Jackson with global default typing enabled, which means that (through the previous exploit) arbitrary code could be executed if all of the following is true: (1) Spring Security's Jackson support is being leveraged by invoking SecurityJackson2Modules.getModules(ClassLoader) or SecurityJackson2Modules.enableDefaultTyping(ObjectMapper); (2) Jackson is used to deserialize data that is not trusted (Spring Security does not perform deserialization using Jackson, so this is an explicit choice of the user); and (3) there is an unknown (Jackson is not blacklisting it already) "deserialization gadget" that allows code execution present on the classpath. Jackson provides a blacklisting approach to protecting against this type of attack, but Spring Security should be proactive against blocking unknown "deserialization gadgets" when Spring Security enables default typing.

[1] List of NIST NVD vulnerabilities as of 9 SEP 2020. [https://nvd.nist.gov/view/vuln/search-results?adv_search=true&cves=on&cpe_version=cpe%3A%2Fa%3Apivotal_software%3Aspring_security%3A5.0.0](https://nvd.nist.gov/view/vuln/search-results?adv_search=true&cves=on&cpe_version=cpe%3A%2Fa%3Apivotal_software%3Aspring_security%3A5.0.0) 


## Project Resources
### Links
* [GitHub Repository](https://github.com/Vidmaster/cybr8420-group4)
* [Project Board](https://github.com/Vidmaster/cybr8420-group4/projects/1)
* [Spring Security Repo](https://github.com/spring-projects/spring-security)

### Team roles
The team decided on shared roles after the first team meeting, so technical, writing, and administrative burdens will be shared equally across the team, with flexibility based on external obligations and other coursework as needed. Our team consists of:
* Henry McNeil (@Vidmaster) - Team Lead
* Andrew Bullock (@abullockuno)
* Bob Copley (@moezilla402)
* Bryan Tomey (@btomey)

## Teamwork Reflection

Project Planning and Reflection. Andrew Bullock, Bob Copley, Henry McNeil, Kevin Neubauer and Bryan Tomey. Mr. Neubauer contributed in the beginning and was a valued contributing member, unfortunately Mr. Neubauer had to drop the class and we lost a valuable member. One of the issues we had to overcome early on is that all of us work. Finding a time to meet and how to divide class work around everyone's work schedule was a challenge. Another challenge was matching assignments to people based on what they wanted to do. To over come this each individual was given two parts of the Project proposal to work on. This was assigned by the team leader to keep it fair.

We also initially struggled to determine a communication mechanism that would work well for everyone, as Bob and Bryan have limited communications access during business hours due to the nature of their work. We settled on Slack as the rest of the team was unlikely to be communicating much during business hours either, and this has proven to be highly effective for us so far.
