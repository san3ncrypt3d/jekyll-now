---
layout: post
title: Static code Analysis Tool
---

Hey Guys, For anyone who is intrested in code review and don't know where to start, I am going to be reviewing some of the static code review tools.

Running codes in a static code analyzer is a great way to find out if you missed any vulnerability while reviewing codes line by line. 



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

RECOMMENDED TOOLS

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


 
 Brakeman

| Source | [https://github.com/presidentbeef/brakeman](https://github.com/presidentbeef/brakeman) |
| --- | --- |
| Configuration and setup | Easy |
| Description | This tool checks for Ruby on Rails applications for security vulnerabilities. Moreover, this tool checks for most common vulnerabilities and produce best results. However, some of the results can be false positives. vulnerabilities checked: - Cross-site scripting - Command injection - SQL injection - File access - Mass assignment - Unsafe code evaluation / code injection - Disabled cross-site forgery protection - Unsafe deserialization - Open redirects - Hard-coded secrets in source code - Unsafe metaprogramming - Session manipulation - Unsafe session settings - Unscoped database queries - Weak hashing algorithms - Skipped SSL certificate verification - Dynamic render locations - Unquoted HTML attributes - Exposed error information - Denial of service via dynamic regular expressions - Basic Authentication with hard-coded passwords - Missing httponly flag on cookies - Rails-related CVEs|
| Pros | - Easy setup, configuration and fast scans. - Because it&#39;s specifically built for Ruby on Rails apps, it does a great job at checking configuration settings for best practices. - With the ability to check only certain subsets, each code analysis is able to be customizable to specific issues.|
| Con | High rate of false positives |
| Comment | This is preferred tool for ruby code analysis for finding vulnerability. |
