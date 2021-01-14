# Architecture Design and Process

## Defining Services

### Describing user in terms of roles and personas

#### Qualitative requirement gathering defines systems from the user point of view

- **Who** are the user? are the developers? are the stakeholders?
  - *Goal: to identify who the system will impact both directly and indirectly*
- **What** the system do? are the main features?
  - *Goal: to define the both simple and difficult, we need to establish the main areas of functionality required, but clear and unambiguous manner.*
- **Why** needed? the system exists & what problem this proposed system solves?
  - *Goal: if there is no clear direction or need then there is high probability that extra feature will be added. WHY also helps in understanding KPIs, SLOs, and SLAs.*
- **When**: the user need/want the solution? developers are done?
  - *Goal: helps define the timeline of the project. Also it help to limit(or contain) the scope.*
- **How**: many expected user? will the system work? much data will be there? much the avg payload of the service request? latency impact system and users?
  - *Goal: helps the non-functional requirements.*

- **ROLE**: *Role represent the goal of a user at some point. In other word its a actor on the system who does some action(verb), lik account holder - holds a account, shopper - shops etc*
  - *roles are NOT people or job titles: people can have multiple roles, and single role can be played by multiple people*
  - *role should describe a user objective: what does the user want to do? for example "user" is not a good example of role as everyone is user*
  - *role are defined based on the requirement: each requirement should have a role(s)*
  - *example of roles: shopper, account holders, customer, administrator, Manager. it can be a non-human like micro-service client accessing a micro-service*
  - *to find out roles, we can brainstorm all the we can think of, then identify overlapping roles and group them together, create a final list of consolidated roles. Then categorize it as internal and external roles, Further we can add few more details like what is the frequency of the role, level of expertise.*

- **PERSONAS**: *For important roles we can create personas.*
  - *Personas are imaginary representation of a user role. They tell a story of who they are*
  - *personas helps architect and developer to think about the characteristics of a user.*
  - *mostly a role have multiple personas.*
  - *personas are NOT list of job functions, unlike role.*
  - *personas helps to build fuller picture of the system. For example: in below scenario says "Jocelyn is a busy person", hence as architect we need to design something automated and simple to use*
  - *example: Jocelyn is a person who's a busy working mom. Jocelyn wants to save time and money as well as perform these standard banking operations online and receive benefits such as cashback.*
  - *to define personas, in real world application: We need to find users and talk through them, and how they want to use the system.*

### write qualitative requirements with user stories

- **USER STORIES**: *user stories describes a(ONE THING) feature from user's point of view(THAT USER WANT SYSTEM TO DO).*
  - *user stories are always structured, below are few common format*
  - *its better to give a TITLE to the user story*
    - *Balance Enquiry*: **AS AN** *<<role>> account holder,* **I WANT TO** *check my available balance at anytime of the day* **SO THAT** *I am sure not to overdraw my account.*
    - **GIVEN** *some context*, **WHEN I** *do something* **THEN** *this happens*.
  - *evaluate user stories using INVEST criteria*.
    - **I***(Independent): it helps in prioritizing, planning and development.*
    - **N***(Negotiable): they are not contract, they are subject to change an refinement based on the discussion between business, dev & users.*
    - **V***(Valuable): each story should add value to users - directly or indirectly. It may include non-functional stories as well, but not technical debts. Think about outcome and impacts, not outputs and deliverables*
    - **E***(Estimatable): technical dependencies and should be estimatable, else something is missing.*
    - **S***(Small): good stories should be small. this keeps scope small, less ambiguous and small feedback loop*
    - **T***(Testable): should be testable, to verify that developer have implemented what is expected.*

### write qualitative requirements using KPIs

### Use SMART criteria to evaluate your service requirements

### Determine approach SLO and SLI for your services

## Micro service Design and architecture

## DevOps & Automation

## Hybrid Network architecture

## Deploying application to google cloud

## Designing Reliable System

## Security

## Maintenance & Monitoring
