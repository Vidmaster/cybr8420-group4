# Team 4 Project Proposal

CYBR8420 Software Assurance, University of Nebraska Omaha, Fall 2020

## Proposed Software

Our proposed software for this semester's project is [Spring Security](https://spring.io/projects/spring-security), one of the components of the [Spring Framework](https://spring.io/). This project can be found on GitHub at https://github.com/spring-projects/spring-security. Our team is tentatively planning to address [an issue pertaining to the default cycles used by BCrypt](https://github.com/spring-projects/spring-security/issues/7411) but may change course as needed.

## Hypothetical Operating Envrionment

Spring Security is commonly used for securing websites and APIs. Here is where we'll describe a hypothetical website that uses it.

`Systems engineering view diagram here`

### Threats perceived by users

Scary things!

### Security features in the software

Authentication! Authorization! Passwords! Things!

## Team Motivation

TBD

## Project Description

All about spring security

## Licensing and Contributions

About licensing and contributing to spring

## Security History of Spring Security

The Spring Security software is composed of several modules built with Java.  These modules provide security features for Spring-based applications. The latest stable release is Spring Security 5.3.4, which was released on August 5th 2020. 

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

## Teamwork Reflection

Everything was awesome!
