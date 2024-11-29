# SAD (**S**oftware **A**rchitecture **D**ocument)

# 1. Introduction

## 1.1 Purpose

This document provides a comprehensive architectural overview of the system, using a number of different architectural views to depict different aspects of the system. It is intended to capture and convey the significant architectural decisions which have been made on the system.

## 1.2 Scope

This Software Architecture Document provides an architectural overview of the Green-Sprout Restaurant Search-and Review System. This Document has been generated under the input of all members participating as part of the Software Engineering project using a Software Architecture Document template.

## 1.3 Definitions, Acronyms and Abbreviations

See the Glossary: ```[if it exists / ref here]```

## 1.4 References

Applicable references are: ```[add referenced documents here]```

## 1.5 Overview

```
[This subsection describes what the rest of the Software Architecture Document contains and explains how the Software Architecture Document is organized.]
```

# 2. Architectural Representation

This document presents the architecture as a series of views:

- Use-Case View
  
- Logical View
  
- Process View
  
- Deployment View
  
- Implementation View
  

The purpose of these views is to relay the structure and function of the Software in a concise manner. 
```[Explanation on how the views are represented] ```

# 3. Architectural Goals and Constraints

The software architecture follows a clear goal of combining user-friendliness and technical requirements. A focus is placed on aesthetics: a uniform, green-colored design system with consistent visual elements and interactive elements improves user-friendliness through direct feedback.
Backwards compatibility ensures the easy provision of new versions to guarantee problem-free updates. The performance of the application is optimized by response times of less than 2 seconds, ideally less than 1 second. A Google Page Speed Score of at least 90 points ensures fast loading times.
The modular architecture separates backend, frontend and database, which increases maintainability and simplifies future extensions. For security reasons, passwords are hashed and only stored as a hash, while JWT tokens ensure the authentication and integrity of user requests.

This architecture ensures a reliable system with a high level of user-friendliness and flexibility.

