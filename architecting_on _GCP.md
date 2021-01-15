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

### write quantitative requirements using KPIs

-----**IMPORTANT**-----

*Once the requirement are in place, along with User stories, we will move on the business side. How to measure technical and business requirement are met*.

*To manage a service well its important to **understand**, **measure** and **evaluate** the behaviors that matters. And they are done in context of business constraints. These are called Quantitative requirement. Mostly they are Time, People and Money*

*Keeping the constraints in mind we can now determine what we can achieve, what we can build, what are important feature, how many potential users are there, how much data are there to be stored or processed.*

*Once we know what we can build, and how virtually application will look like, we start measuring the matrices. As we know matrices mostly depends on the type of application.*

*Business decision maker wants to measure the value of the project, WHY? This enable them to better support the most valuable project and not waste resource on those that are not beneficial. Hence to get the value of the project we can measure success of the project and its commonly done via KPI.*

*KPI are matrices that can be used to measure success. KPI are further divided into Business KPI(defining how successful a business is) and software(how successful a software is) KPI. **Example of business KPI**: ROI in relation to product and service | EBIT(earning before interest and taxes) is companies net income(revenue - expenses) before tax and interest expenses | customer impacts like customer churn(loss of clients of customer) or employer turnover. **Example of software KPI**: Page view, User registration, click through, checkouts*

*KPIs are also aligned with business objectives - commonly OKR. **How are OKR and KPI related?** KPI indicate whether you are on track to achieve the goal. Goal is a result or outcome that we want to achieve, and KPI are metric that help you track your progress. Hence KPI need to have accompanying goal. So each goal will have a KPI which will help us to track and measure progress. KPIs also have defined target, target to measure success. **Example of goal/objective and KPI:** GOAL: Increase turnover for an online store, KPI: % of conversion on the website*

---------------------

### Use SMART criteria to evaluate your service requirements

- *To make KPI effective use the **SMART** tool*
  - **S***(Specific)- KPI should be very specific rather than general. For example: making website user friendly is not specific, instead it can be stated as "Section 508 accessible*.
  - **M***(Measurable)- KPI should be monitored, the whole purpose will be defeated if NOT*.
  - **A***(Achievable)- API should NOT be too ambitious to achieve, like 100% available, may not be possible*.
  - **R***(Relevant)- it should be matter to user or business, it should help to achieve application goals*.
  - **T***(Time-bound)- helps measuring the KPI,few KPI can be sensitive to time. Like availability per day or month*.

### Determine approach SLO and SLI for your services

- **SLI**: *service level indicators is measure that attributes a service. They are aligned with user happiness and business goal. Its common to consider KPI as SLIs. For eg: availability, latency, durability. How we measure SLI are explained in SRE.md.*

- **SLO**: *success threshold for a SLI. For eg: 99.99%*

- **SLA**: *promise to external user, it comes with compensation*.

*NOTE: availability is just a idea: SLI in real world can be stated as: "HTTP POST photo uploads complete within 100ms aggregated per minute". Similarly for latency, durability and error rate.*

## Micro service Design and architecture

## DevOps & Automation

## Hybrid Network architecture

## Deploying application to google cloud

## Designing Reliable System

## Security

## Maintenance & Monitoring
