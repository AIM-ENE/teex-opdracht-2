# Weekopdracht 2 voor de cursus TEEX

## Introduction
De applicatie "ANSIE" betreft een prototype van een toetsapplicatie. Op dit moment is de applicatie alleen geschikt om door een aantal toetsvragen heen te navigeren die beschikbaar zijn in de back-end. In deze week werk je een spike uit waarmee je antwoord probeert te krijgen op enkele vragen en een aantal risico's vermindert. 

## Context
Je kunt behalve door de toetsvragen heen navigeren ook je antwoord invoeren. Dat antwoord wordt niet opgeslagen of onthouden maar dat is voor deze opdracht niet relevant.

## Functional Overview
In deze applicatie staan toetsvragen centraal. De back-end ondersteunt verschillende vraag-types maar de front-end alleen open vragen. 

User Story: Als architect wil ik dat de front-end kan worden uitgebreid met bijvoorbeeld multiple-choice vragen waarbij er kritisch gekeken worden naar het huidige state management van de React applicatie. 

Op dit moment is er alleen een user-interface voor de student, docenten kunnen wel vragen toevoegen, aanpassen en verwijderen maar dat moet rechtstreeks in de database.

## Quality Attributes

Modularity
* Een aanpassing aan een React component heeft een minimale impact op andere React componenten in deze applicatie.

Reusability
* Bestaande componenten, in elk geval de Navigator, moeten kunnen worden hergebruikt in andere applicaties. 

Volgens de architecten die het prototype gemaakt hebben wordt er nog onvoldoende aan deze quality attributes voldaan. De oorzaak ligt volgens hen in onhandig state management
* prop drilling
* function passing
* gebruik van [conditional rendering](https://react.dev/learn/conditional-rendering) met if-else.

De architecten hebben twee mogelijkheden voor ogen om dit state management te verbeteren:
1. Gebruik van Composition.
2. Gebruik van de Context API.

## Principles

Deze applicatie bouwt voort op de onderstaande principes uit semester 1:

Back-end
* Package by layer 
* Embedded Application Server
* Dependency Injection
* JDBC Templates

Front-end
* Prop-drilling 
* Function passing
* Conditional Rendering

## Software Architecture

### Container Diagram

![](structurizr-1-Containers.png)

### Component Diagram

![](structurizr-1-Browser-Components.png)

![](structurizr-1-Load-first-question.png)

![](structurizr-1-Load-next-question.png)

## Deployment

### Software
React
Java 17
Spring Boot
MySQL

### Building

Back-end
```mvn package```

Front-end
```npm run build```

### Configuration
Back-end: Het .env bestand bevat poorten en gebruikersnaam/wachtwoord voor toegang tot de database. Deze worden automatisch gebruikt door docker compose. Sommigen variabelen zijn gedupliceerd in een .env bestand in de backend/src/main/resources/.env voor als je zonder docker compose gaat ontwikkelen.

Front-end: Geen configuratie.

## Operation and Support

Run de hele stack met Docker Compose:

```docker compose up```

De verschillende componenten gebruiken elk een eigen netwerk port.

| **component** | **port** |
|---------------|----------|
| db            | 3306     |
| backend       | 8080     |
| frontend      | 5173     |

### Back-end
Run de back-end met Maven:

```mvn spring-boot:run```

Of met Docker Compose:
```docker compose up backend db```

### Front-end
Run de front-end:

```npm run start```

Of met Docker Compose:
```docker compose up frontend```
