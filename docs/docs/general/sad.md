# SAD (**S**oftware **A**rchitecture **D**ocument)

## 1. Introduction

### 1.1 Purpose

This document provides a comprehensive architectural overview of the system, using a number of different architectural views to depict different aspects of the system. It is intended to capture and convey the significant architectural decisions which have been made on the system.

### 1.2 Scope

This Software Architecture Document provides an architectural overview of the Green-Sprout Restaurant Search-and Review System. This Document has been generated under the input of all members participating as part of the Software Engineering project using a Software Architecture Document template.

### 1.3 Definitions, Acronyms and Abbreviations

The following Definitions, Acronyms and Abbreviations are used.:

- API  Application Programming Interface
  
- CRUD  Short for "Create, Read, Update and Delete"
  
- JWT  Jason Web Token

- OSM  Open Street Map

- ORM  Object-Relational Mapping 

### 1.4 References

Applicable references are:

- All of the material contained in our Github Repositories
  
  - https://github.com/green-sprout/backend
    
  - https://github.com/green-sprout/frontend
    
  - https://github.com/green-sprout/green-sprout
    
  - https://github.com/green-sprout/docs
  
## 2. Architectural Representation

This document presents the architecture as a series of views:

- Use-Case View
  
- Logical View
  
- Process View
  
- Deployment View
  
- Implementation View
  

The purpose of these views is to relay the structure and function of the Software in a concise manner using xml-based Diagrams whenever possible.

## 3. Architectural Goals and Constraints

The software architecture follows a clear goal of combining user-friendliness and technical requirements. A focus is placed on aesthetics: a uniform, green-colored design system with consistent visual elements and interactive elements improves user-friendliness through direct feedback.

Backwards compatibility ensures the easy provision of new versions to guarantee problem-free updates. The performance of the application is optimized by response times of less than 2 seconds, ideally less than 1 second. A Google Page Speed Score of at least 90 points ensures fast loading times.

The modular architecture separates backend, frontend and database, which increases maintainability and simplifies future extensions. For security reasons, passwords are hashed and only stored as a hash, while JWT tokens ensure the authentication and integrity of user requests.

This architecture ensures a reliable system with a high level of user-friendliness and flexibility.

## 6. Process View
![Sequence Diagram components](../../assets/sad/full-sd.png)
The sequence diagram shows how a user selects filter criteria via the front end, whereupon the backend retrieves the appropriate map information from the Open Street Map API.
The user can select a restaurant whose details and ratings are provided by the backend.
They can also write a review, which is saved in the database via the backend.
## 8. Implementation View
### Komponentendiagramm der Webanwendung
![Komponentendiagramm](../../assets/sad/KomponentDiagram.jpeg)
Das Komponentendiagramm zeigt die Architektur der Webanwendung und illustriert die wichtigsten Softwarekomponenten sowie deren Interaktionen. Die Anwendung besteht aus einer **Frontend-** und einer **Backend-Schicht**, die miteinander sowie mit externen APIs und einer Datenbank kommunizieren.

### Komponenten und deren Verantwortlichkeiten

#### Frontend
Das Frontend umfasst folgende Komponenten:

##### Map View
- Zeigt Restaurants und Kartendaten basierend auf den vom Nutzer ausgewählten Filtern an.
- Stellt Anfragen an das Backend und die OSM-Integration, um Kartendaten zu aktualisieren.

##### Filters
- Ermöglicht Nutzern, Suchkriterien wie Küche, Diät oder Bewertung auszuwählen.
- Sendet die ausgewählten Filterkriterien an das Backend sowie direkt an die OSM-Integration, um gefilterte Daten abzurufen.

##### User Management
- Verarbeitet Benutzerregistrierung, Login und Sitzungsverwaltung.
- Kommuniziert mit dem **Authentication Service** im Backend.

##### Review Management
- Ermöglicht registrierten Nutzern, Rezensionen zu schreiben und bestehende Rezensionen anzuzeigen.
- Übermittelt neue oder aktualisierte Rezensionen an das Backend zur Speicherung.

#### Backend
Das Backend umfasst folgende Komponenten:

##### Authentication Service
- Verarbeitet die Authentifizierung von Benutzern (Login, Registrierung).
- Übermittelt und überprüft Benutzerinformationen in der **User Management**-Komponente.

##### User Management
- Verwaltet Benutzerdaten.
- Speichert die Benutzerdaten in der Datenbank über die **Database Layer**-Komponente.

##### OSM Integration
- Kommuniziert mit der OpenStreetMap API, um Kartendaten und Restaurantobjekte abzurufen.
- Bearbeitet Filterkriterien aus dem Frontend und Backend, um gefilterte Daten bereitzustellen.
- Speichert Restaurantdaten in der lokalen Datenbank, wenn notwendig.

##### Review Management
- Verarbeitet Rezensionen und Bewertungen, die vom Frontend empfangen werden.
- Speichert Rezensionen in der Datenbank über die **Database Layer**-Komponente.

##### Database Layer
- Dient als Schnittstelle zur **PostgreSQL-Datenbank**.
- Führt CRUD-Operationen (Erstellen, Lesen, Aktualisieren, Löschen) für Benutzerdaten, Rezensionen und gegebenenfalls Restaurantdaten aus.

#### Externe Komponenten
- **PostgreSQL-Datenbank**:  
  Speichert Benutzerinformationen, Rezensionen und ggf. Restaurantdaten, die von der OSM API stammen.
- **OpenStreetMap API**:  
  Stellt Kartendaten und Informationen zu Restaurants bereit. Unterstützt gefilterte Anfragen basierend auf den vom Nutzer gewählten Kriterien.

### Hauptinteraktionen

#### Frontend zu Backend
- Nutzerinteraktionen (z. B. Filtern, Rezensionen schreiben) werden vom Frontend an das Backend übermittelt, das die Anfragen verarbeitet.
- Authentifizierungsanfragen und Sitzungsmanagement werden an den **Authentication Service** weitergeleitet.

#### Backend zu OSM API
- Das Backend nutzt die **OSM Integration**, um Kartendaten und Restaurantinformationen von der OpenStreetMap API abzurufen.
- Gefilterte Anfragen werden basierend auf den vom Nutzer gesetzten Kriterien weitergeleitet.

#### Backend zur Datenbank
- Benutzerdaten, Rezensionen und Restaurantdaten werden in der **PostgreSQL-Datenbank** gespeichert und bei Bedarf abgerufen.

#### Filters zu OSM Integration
- Die **Filters**-Komponente im Frontend sendet ausgewählte Kriterien direkt an die **OSM Integration**, um eine gefilterte Ansicht der Karte zu erhalten.


## 11. Quality

### Extensibility
Vue.js as the front end enables modular and component-based development that can be easily scaled as the number of users and features grow.  

The backend in Spring Boot offers a clear separation of model and controller and implements parts of the MVC approach. Services and controllers can be easily extended and exchanged.  

By using the OpenStreetMap API in the backend, the use of this API is abstracted and easier to use for the frontend, as filters and regions have to be inserted into the URL for the request to the OpenStreetMap API in a complex manner.

### Reliability  
Spring Boot offers solid error handling and logging functions for the early detection and handling of problems.  

The PostgreSQL database system ensures data integrity and provides mechanisms for data recovery after failures.  

Authentication with JWT provides standardized methods to ensure secure user sessions and minimizes vulnerabilities compared to traditional authentication methods.  

### Portability
All components of the system are platform-independent and can be deployed on all platforms and on any infrastructure using containers.  

### Security
The use of JSON web tokens offers a robust solution for secure and reliable authentication and authorization. Security risks can be minimized by simply adjusting the lifetime of a token.  

Accessing the OpenStreetMap API through the backend as a proxy minimizes the security risks of manipulating the request in the frontend to the OpenStreetMap API.  

Using an ORM to map and interact with the database eliminates the risks of SQL injections and sniffing.
