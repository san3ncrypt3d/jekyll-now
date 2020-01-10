---
layout: post
title: Static code Analysis Tool
---

Hey Guys, For anyone who is intrested in code review and don't know where to start, I am going to be reviewing some of the static code review tools.

Running codes in a static code analyzer is a great way to find out if you missed any vulnerability while reviewing codes line by line. 


|------ ---------------------
| Tool | Language supported |
| --- | --- |
| Brakeman  | Ruby, Rails |
| Reek | Ruby |
| Rubocop| Ruby  |
| Hawkeye | Ruby, Node.js, Python, PHP and Java |
| Rails best practice | Ruby, Rails |
| TruffleHog | Review Git code to find secrets (*) |
| Salus | Ruby, Node, Python and Go |
| Bandit | python |
| Pyright | python |
| VCG | C/C++, Java, C#, VB, PL/SQL & PHP |
| jshint | JavaScript  |
| Rips | PHP |
| PMD | Java, Js |
| SonarQubes | Java, JavaScript, C#, TypeScript, Kotlin, Ruby, Go, Scala, Flex, Python, PHP, HTML, CSS, XML and VB.NET |
| JSPrime | JavaScript |
| NodeJsScan | NodeJs |
| Microsoft FxCop| .Net |
| YASCA | .Net, Java, C/C++, HTML, JavaScript, ASP, ColdFusion, PHP, COBOL  |
| Code Warrior | C, C#, PHP, Java, Ruby, ASP, JavaScript |

## RECOMMENDED TOOLS

| Language | Tools |
| --- | --- |
| Ruby | Brakeman, Hawkeye |
| Git repo for finding secrets | TruffleHog |
| Java | Code Warrior, Visual Code Grepper, Hawkeye |
| Php | Rips, Visual Code Grepper |
| Python | Bandit, Hawkeye, Code Warrior |
| Go | Gosec |
| Js | Code Warrior, JSPrime |
| sql | Visual Code Grepper |
| C# | Visual Code Grepper, Code Warrior |
| Nodejs | NodeJsScan |
| .Net | Microsoft FxCop |
| C | Code Warrior, VCG |


 
 ## Brakeman

| Source | [https://github.com/presidentbeef/brakeman](https://github.com/presidentbeef/brakeman) |
| --- | --- |
| Configuration and setup | Easy |
| Description | This tool checks for Ruby on Rails applications for security vulnerabilities. Moreover, this tool checks for most common vulnerabilities and produce best results. However, some of the results can be false positives. vulnerabilities checked: - Cross-site scripting - Command injection - SQL injection - File access - Mass assignment - Unsafe code evaluation / code injection - Disabled cross-site forgery protection - Unsafe deserialization - Open redirects - Hard-coded secrets in source code - Unsafe metaprogramming - Session manipulation - Unsafe session settings - Unscoped database queries - Weak hashing algorithms - Skipped SSL certificate verification - Dynamic render locations - Unquoted HTML attributes - Exposed error information - Denial of service via dynamic regular expressions - Basic Authentication with hard-coded passwords - Missing httponly flag on cookies - Rails-related CVEs|
| Pros | - Easy setup, configuration and fast scans. - Because it&#39;s specifically built for Ruby on Rails apps, it does a great job at checking configuration settings for best practices. - With the ability to check only certain subsets, each code analysis is able to be customizable to specific issues.|
| Con | High rate of false positives |
| Comment | This is preferred tool for ruby code analysis for finding vulnerability. |


## Reek

| Source | [https://github.com/troessner/reek](https://github.com/troessner/reek) |
| --- | --- |
| Configuration and setup | Requires additional Gem dependencies |
| Description | Reek checks for code smells and programming mistakes such as tab detection. Less focused on security vulnerability and more focused on business logical errors and hygiene errors. |
| Comment | Not the best for vulnerability analysis, good for best coding practices. |

## Rubocop

| Source | [https://github.com/rubocop-hq/rubocop](https://github.com/rubocop-hq/rubocop) |
| --- | --- |
| Configuration and setup | Easy setup |
| Description | Rubocop check for offenses in codes such as formatting issues and RuboCop can also automatically fix some of the problems present in the code.  Additionally, returns hardcoded values &amp; public keys present in the code. |
| Comment | More focused on code hygiene. |



## Rails\_best\_practice



| Source | [https://github.com/flyerhzm/rails\_best\_practices](https://github.com/flyerhzm/rails_best_practices) |
| --- | --- |
| Configuration and setup | Time consuming but easy set up |
| Description | A static code analyzer for Ruby on Rails applications that finds - among other things - common patterns that might lead to security vulnerabilities such as use of dangerous attributes. Focused both on security vulnerability and code hygiene. However, it doesn&#39;t notify user any common vulnerabilities in the code. Based on a set of rules. |
| Comment | We can customize this configuration file. Returns too many warnings which makes it difficult to find any high vulnerabilities returned. |

## TruffleHog

| Source | [https://github.com/dxa4481/truffleHog.git](https://github.com/dxa4481/truffleHog.git) |
| --- | --- |
| Configuration and setup | Easy setup |
| Description | Go through git source code, find secrets that&#39;s committed on top over or revision history. A lot of false positives. Reduced noise due to use of regex. (entropy detection-based tool). |
| Comment | Good as an initial scan tool for git source codes, High manual effort needed due to false positives. |

## Pyright

| Source | [https://githulb.com/Microsoft/pyright](https://githulb.com/Microsoft/pyright)  |
| --- | --- |
| Configuration and setup | Easy if you have npm installed, otherwise will have to configure node/npm.   |
| Description | - Based on type-checking. Pyright doesn't look for most common vulnerabilities. However, returns a lot of errors based on code hygiene. |

## Jshint

| Source | [https://jshint.com/](https://jshint.com/)  |
| --- | --- |
| Configuration and setup | Configuration and setup are really easy using npm command.  |
| Description |  This static code analyzing tool returns a lot of errors based on code hygiene. However, doesn&#39;t returns any security vulnerabilities in the code. |
| Comment | Results include: semicolon missing, function already defined etc. |

## Rips

| Source | [https://sourceforge.net/projects/rips-scanner/](https://sourceforge.net/projects/rips-scanner/) |
| --- | --- |
| Configuration and setup |   Configuration is a little complicated since it runs on local host.
- Set up apache2
- Set up mysql
Access the rip downloaded folder via localhost. |
| Description |  This is a great tool for PHP code review. Its vulnerability based and check for client-side attacks and server-side attacks. The scan runs fast, and results looks neat. Additionally, it has features such as verbosity level, regex-based searches etc.|

| Pros | - Fast results with range of security controls - Nice reporting with visualizations makes fixing vulnerabilities faster |

## Jsprime

| Source | https://github.com/dpnishant/jsprime |
| --- | --- |
| Configuratinn and setup | Easy setup |
| Description | This static code analyzer is focused on vulnerability and checks for common vulnerabilities such as XSS. However, it returns a lot of false positives . Moreover, high level of manual effort is necessary since each JS file have to be copy pasted into the jsprime interface for analysis. |

## NodeJsScan

| Source | https://github.com/ajinabraham/NodeJsScan |
| --- | --- |
| Configuratinn and setup | Easy setup with python.&quot;python NodeJsScan.py -d \&lt;dir\&gt;&quot; |
| Description | Security vulnerability focused and has a minimum of false positive. |
| Comment |    |



## YASCA

| Source | http://www.scovetta.com/yasca.html |
| --- | --- |
| Configuratinn and setup | Install the msi |
| Description | The scanner returns a lot of false positives. Although the scanner is not focused on security vulnerabilities, it returns some bad practices implemented in the source code. |
| Comment |  It is a multi-language scanner |

## Code Warrior

| Source | https://github.com/CoolerVoid/codewarrior |
| --- | --- |
| Configuratinn and setup | Install using make |
| Description | This is a Multilanguage scanner focused on security vulnerabilities. The scanner is only supported in Linux operating system and have a GUI. Returns good results comparatively and low number of false positives. |


LOL I was lazy to make tables for all the tools metioned above with additional details so if you have any questions let me know and I will clarify/answer your question(s).
