# Use-Case-Realization Specification: View Restaurant

**Version 1.0**

---

## Revision History

| Date       | Version | Description                      | Author            |
|------------|-------|----------------------------------|-------------------|
| 28.10.2024 | 1.0   | UCRS for the Filter Map use case | Green Sprout Team |

---


## 1. Introduction

### 1.1 Purpose
The purpose of this Use-Case Realization Specification is to detail the design of the “View Restaurant” use case, where a user selects a restaurant from the map to see further information and reviews of it.

### 1.2 Scope
This document covers the interaction flow between the User, Front-End, Back-End, and OpenStreetMap API for filtering and displaying points of interest based on user-selected criteria.

### 1.3 Definitions, Acronyms, and Abbreviations
- POI: Point of Interest
- API: Application Programming Interface
- n/a: not applicable
- UCRS : Use-Case-Realization Specification

### 1.4 References
n/a

### 1.5 Overview
This document is organized into sections detailing the purpose, scope, and flow of events in this use case, followed by derived requirements for implementation.

---

## 2. Flow of Events—Design

The following describes the flow of events in the "View Restaurant" use case. The sequence diagram is shown below for visual reference:

![Sequence Diagram to view restaurant](../../assets/srs/selectrestaurant-sd.svg)

**Flow Steps:**
- **User Action:** The user clicks on a POI on the Map  
- **Front-End Request:** The front-end sends a "get restaurant info" request to the back end, including the id of the selected POI.  
- **Back-End to OpenStreetMap API:** The back end processes the request and sends a "request Restaurant info" request to the OpenStreetMap API. This request includes the id of the selected POI. To load the reviews the backend queries the database ("request reviews") using the POI id as well.  
- **API Response:** The OpenStreetMap API returns all available information about the requested POI.  
- **Back-End to Front-End:** The back combines the data from the OpenStreetMap API and the Database query and sends it back to the frontend ("display restaurant information").  
- **Map Display:** The frontend opens the restaurant "card" on the left side of the screen and displays the retrieved information.

---

## 3. Derived Requirements

1. **Amount of Data:** The Backend should only return a certain amount of reviews for this action. To reload more reviews the user just scrolls down the loaded reviews and more will be loaded.
2. **Error Handling:** If the database query or the OpenStreetMap request fails, the frontend still recieves an answer with the successfully recieved data. If both fail the backend responds with an error message.  
3. **Scalability:** The back end must efficiently handle multiple requests to the OpenStreetMap API and database queries without performance degradation.  
4. **Data Accuracy:** The data recieved by the frontend should be displayed accurately without formatting errors.
