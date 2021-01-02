# SRE

By google: "what happens when you ask a software engineer to design an operations team."

Embedding software engineers in operation.

**SRE is the practices of balancing the velocity of development features with the risk to reliability.Site Reliability Engineering is "how to think about, measure and incentivize reliability"**.

**Role/Mission of SRE is to protect, provide for and progress software and system consistent focus on availability, latency, performance and capacity**.

**SRE need cultural and organizational support to be successful**.

## Example: concern related to service reliability

Service reliability issue: *Online retailer finds that one of their Key matrices are showing increase in time taken between click and showing the status*.

*The team marks that as low priority issue, and continued to work in silos to fix the latency issue. As well as from the business side, new feature request was made and developer keep pushing the new feature*.

*Due this developer started working overtime and started to burn out working on the new features as well as the small latency bug that was identified earlier*.

*There were no shared standard communication between IT and business team and hence the prioritization of latency was not addressed properly*.

Internal and external factors:

How do you address the issue:

## Problem we are trying to solve

- decline in reliability of services(*Customer's experience with your services tell you how reliable it is.*) - it can be internal and external factors.
- decline in customer engagement (in spite everything seems to work)
- customer disruption while deploying minor patches or huge releases.
- Silos between development and operation due to conflicting priorities. How can IT and business team can communicate better.

## Rules

- SRE principle can have a positive and lasting impact on IT Projects/Teams and daily work, regardless of on-premise or cloud.
- Organization size and maturity can affect implementation of SRE principle.

## DevOps practices, similarities and difference b/w SRE

### What is DevOps, and why they exists?

*Traditionally software team consists of developer and operators*.

*Dev are responsible for developing new feature (they want to work in agile and faster, pushing features quicker) and operation team was focused on consistency & reliability of the software and their operation, so that the customer are happy. They generally work slower without understanding of the code*.

*This was not sustainable, between the two groups*. *This was due to difference in priorities and they were not aligned with the need of the business*.

**Hence DevOps was born, with below principle in mind**. *DevOps is a philosophy and not a development technology or methodology*.

- *Reduce organization silos*, and break the barriers b/w the teams.
- *Accept failure as normal*. Computers are unreliable by nature and hence we need to accept failure, and addition of manual process increases the chances of failure. Things failing should be part of the process.
- *Implement gradual change*. Small and incremental change are easy to implement, review, deploy and recover/revert in case of failure.
- *Leverage tooling and automation*. Replace manual work and automate. It helps IT team to focus on the task that matters.
- *Measure everything*. This act as the gauge to measure success or failure of a team.

**VERY IMPORTANT:** Above DevOps philosophies are guidance to solve the problem, however it do NOT explicitly mention how to implement these philosophies.

**Hence SRE comes into play**.

### Origin of SRE?

SRE was born in google in early 2000, separate from DevOps. In 2003, Google appointed a bunch of software engineers to look after development as well as operation. They were responsible for operation of the software they develop. This gave birth to new role called SRE.

**SRE is a concrete set of principles. Its both role and practice**. However, title is not necessary to practice SRE.

SRE both comes of **Technical** and **cultural** practices.

Now how do we map DevOps practices with SRE:

- *Reduce organization silos | share ownership*: SRE defines service level objective(SLO) & error budgets in collaboration developer to define production system. They define reliability and prioritize work. Culturally, it promotes shared vision and knowledge with improved collaborations and communication.
- *Accept failure | use blamelessness postmortem*: Under the failure instead of blamelessness. Define strategy to reduce the likelihood of the same failure again. SRE are **comfortable with failure**, by **removing ambiguous monitoring**, and **documenting the process**.Culturally it **promotes RCA(retrospective)** and how to prioritize work.
  - *Component of postmortem* - document:
    - details of the incident and its timeline.
    - action taken to mitigate the issue.
    - incident's impact
    - root cause(s) or trigger of the issue
    - follow-up actions to prevent from reoccurrence.
  - *cultural & psychological safety*:
    - no one will be blamed for ideas, questions, concerns or mistake.
    - frame work as a learning problem and not as a execution problem.
    - acknowledge your own fallibility.
    - model curiosity in the organization.
    - low psychological safety: keep ideas to themselves | afraid of incompetent or ignorant.
    - impact: bridging is encouraged | cooperation is high | people are not blamed | failure is treated as opportunity | Lead time | deployment frequency | time to share.
    - hindsight bias: is a tendency to overestimate their ability to have predicted an unpredicted outcome. it leads to blameful culture.
    - discomfort discharge: is when people others to discomfort discharge.
    - focus on system and process and not people.
    - fear hinders innovation as innovation is always risk taking activity
    - implement blamelessness by intense training, couple with management change.
- *Implement gradual change | Reduce cost of failure*: Reduce cost of failure by implementing small changes. SRE deploys changes to small % of users rather than generally available. Culturally it promotes design thinking and prototyping.
- *Leverage tooling and automation | toil automation*: SRE follow toil(work) automation reducing the amount of manual steps using tools and automation.
- *Measure everything | measure toil and reliability*: SRE measure everything using the work(hard work), systems reliability and health of their systems.

To achieve all these above, organization need to culture of goal setting, transparency and data driven decision making.

**The goal of SRE is serve the business and the users, not the other way round**.

### Relation between DevOps and SRE

DevOps is a philosophy that bridges the gap between dev, ops. SRE is a way to implement DevOps.

## Who practices SRE

SRE is a role, who practices SRE policies. However role is not required to practice SRE, anyone from IT team can implement SRE principles.

## Benefits of organization by implementing SRE

As discussed previously, implementing SRE practices like **more automation**, **blameless postmortem of failures**, **reduce cost of failure**, along with **bridging the gap b/w dev and ops** help organization to deliver quickly, reducing cost per release along with maintaining the reliability of the services.

Automation helps in scaling as per business needs and customer usage pattern. It also improves innovations within the team as team can focus more on useful work.

Smaller releases and iteration allows fail fast.

## Adopting and embrace SRE culture in organization

### First step is define SLO

Need to define SLO with consequences. **Performance of the services relative to SLO should guide business decisions**.

## Google Free SRE books

https://sre.google/books/