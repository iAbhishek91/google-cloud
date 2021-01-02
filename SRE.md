# SRE

By google: "what happens when you ask a software engineer to design an operations team."

Embedding software engineers(mainly focuses on designing and building software application) in operation(where and how the code is deployed and maintained). (40 - 90)% cost are incurred after the launch.

**SRE is the practices of balancing the velocity of development features with the risk to reliability.Site Reliability Engineering is "how to think about, measure and incentivize reliability"**.

**Role/Mission of SRE is to protect, provide for and progress software and system consistent focus on availability, latency, performance and capacity. SRE helps IT team to work with high velocity while maintaining the reliability**.

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

**VERY IMPORTANT:** Above DevOps philosophies are guidance to solve the problem, however it do NOT explicitly mention how to implement these philosophies.**Hence SRE comes into play**.

### Origin of SRE?

SRE was born in google in early 2000, separate from DevOps. In 2003, Google appointed a bunch of software engineers to look after development as well as operation. They were responsible for operation of the software they develop. This gave birth to new role called SRE.

**SRE is a concrete set of principles. Its both role and practice**. However, title is not necessary to practice SRE.

SRE both comes of **Technical** and **cultural** practices.

Now how do we map DevOps practices with SRE:

- *Reduce organization silos | share ownership*: SRE defines service level objective(SLO) & error budgets in collaboration developer to define production system. They define reliability and prioritize work. Culturally, it promotes shared vision and knowledge with improved collaborations and communication. **Discussed below in details**.
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

### Step-1: Define reliability

**SRE also are responsible to make everyone(from dev to VP) agree on how to measure service reliability and what to do if you fall short**.

Simple approach to define reliability: *good time / total time = fraction of time the service is available and working*

The above approach do not work well for complex distributed system. *How do you measure good time if one of the server is down*
Thus sophisticated approach is: *good interactions / total interaction = fraction of real user for whom service is available and working*

### Step-2: Error budget

**Amount of unreliability you or organization wants to tolerate is called error budget**. However reliability should not be 100% as it results in 0% error budget, in this case pushing new features, system patches, security upgrade, network upgrade will become very difficult/impossible.

**Error budget helps prioritize engineering work**. It gives right balance between innovation and reliability. Dev team can now manage their own error budget, as they know setting unrealistic error budget will slow down their work.

### Step-3: SLO

**In simple words, SLO is precise numerical target for system reliability**. There targets are shared between the stakeholders.

Need to define SLO with consequences. **Performance of the services relative to SLO should guide business decisions**.

For defining SLO we need SLI **how well a service is doing at any point in time**. Its a quantifiable measure of service reliability. SLI recommended to be percentage of good events and valid events. *SLI of any parameter 0 means nothing is working and 100% means everything is working*.

SLI are **mapped to user expectation** such as *response time*, *latency*, *availability*, *data collection processes and freshness*, *storage latency and throughput*.

Now, **SLO is aggregated of SLI over time**. SLO is a line between **happy and unhappy customers**. SLO are just short of 99.9%.

**SLA is a promise to your customer about the health of the service**. What you are going to do **if SLO fails**, such as refunding money.

### Step-4: Cultural shift due to SLO and error budgets

create **Unify vision** | foster **collaboration** | improve **communication** and share **knowledge** b/w teams.

**Unified vision**:

- Team vision should align with company's vision.
- Vision consist of **values**, **purpose**, **mission**, **strategy** and **goals**.
  - **Values**: response to others | commitment to goals | way we spend time | how to operate a team. *this helps to create psychological safety with each other* | *take risk for innovation* | *greater sense of inclusion and commitments*.
  - **Purpose**: why that team exists | improve life & work satisfactions | stronger connections | reduce conflicts.
  - **Mission**: clear and compelling goal that the team want to achieve. for ex *To organize the world information and make it universally accessible and useful*
  - **Strategy**: how it realise its mission. can be single initiative | change in investment and how work is done | can be leveraged. Building block of strategies are to *identify* threats and opportunities, *Understand* and *consider* strategies for addressing threats and opportunities and *create*.
  - **Goal**: what team or company is striving to attain. Goals can be defined using **OKR** - Objectives and key results. OKR helps to set our ambitious goal and track our progress.
    - **OKR**: purpose of OKR is to set very ambitious goals
    - *Try* new things, *prioritize* new work, and *learn* from success and failure.
    - Every OKR may not be fulfilled, but team can strive to meet the goals.

**Collaboration and communication**:

- One of the high priority within the SRE teams.
- helps in solving common approaches to platform.
- Ways to improve:
  - *Service-Oriented meeting*: SRE team review the state of the service they are in charge | audience: stakeholders and its compulsory | objective is to raise awareness and to improve the operation of the service. | weekly for 30 - 60 mints | designated lead | agenda: downtime, production changes, patches, metrics, paging and non-paging events and action items.
  - *Good team composition*: SRE is a distributed organization spread across different geographies, on-site, or virtual team. Communication is important between the SRE teams and SRE team and dev team. All the roles within SRE should have excellent communication skills. Suggested roles:
    - *tech leads*: to set the technical direction of the team | looks & comments at everybody's code | organize quarterly direction presentations and makes consensus within the team.
    - *Manager*: is the first point of contact within the team | runs performance management of the team.
    - *Project Manager*: comments on design doc and writes code.
  - *Communication between SRE and Dev Team*: This is vital. its best when company is at the early stage and single line of code is not written. SRE generally recommendation about the software architecture and behaviors. OKR are also used to track progress of the teams. Cross functional team generally share a OKR b/w multiple teams.(this helps in creating a share agreement in the outputs).

**Knowledge sharing**:

- SRE are expected to perform more than one job function as required.
- Organization should encourage knowledge sharing between team members.
  - *Cross training*: train team to be more flexible. This helps in helps reduce costs | improves morals , job satisfactions & productivity | enhanced flexibility.
  - *employee to employee network*: its recommended to by google. This is to teach other interested employee when someone have firsthand knowledge of something. Volunteer teaching network | helps peers learn new skills. It can be Courses | one to one training and | design documents.
  - *Job shadowing*: this is a effective way to share knowledge. Share day to day communication to new hires | hands-on experience | opportunity to ask questions | typical issues faced | nuances of a job role | pair up with team members to scale and retain knowledge.
  - *postmortem result sharing*: postmortem DevOps practice leads to docs and action item, we can use tools like google docs where people are allowed to comment, annotate and real-time.

### Step-5: Releasing small change

CODE >> BUILD >> INTEGRATE >> TEST >> RELEASE >> DEPLOY >> OPERATE
`<--agile dev-->`
`<----------------CI--------------->`
`<-----------------------CD-------------------->`
`<--------------------------DevOps------------------------------->`

**CI/CD**: CI (building, integrating and testing code within development environment).CD delivery (deployment of code to production frequently (as business opted) in a automated fashion).

**Canarying**

- Release small to detect early failure in production environment.
- Canary population **should be large enough** to be represented subset of the control.
- Canary population **should be small enough** not to endanger the whole service if broken.
- Canary deployment **should NOT be overly complicated** for those who monitor it.

**Design thinking and prototyping** this is a cultural change.

- Design thinking combines *creativity* and *structure* to *solve complex problems*.
- consists of five phases:
  - *Empathize*: observe and engage with intended user. Learn more about the real problem, and immerse yourself in their environment.
  - *Define*: the problem you are trying to solve from the user point of view.
  - *Ideate*: start generating ideas to solve the problems. this is time to think out-of-box and innovate.
  - *prototype*: create small model of the solution. This work is experimental in nature. Think out-of-box, or probably implement multiple solution and compare.
  - *test*: test the prototype solution with real world environment and user.
- Once the prototype is complete with user as focus, we can think about 10x thinking. Then test your solution again.
- Brain storm and apply above SRE practices CI/CD and Canarying.
- *Without prototyping*: fewer ideas are tested | slower failures | few success.
- Prototype can be using video | clickable | pencil & paper | act | physical prototype. With simple prototype and power of imagination we can solve very complicated problems.

## Google Free SRE books

https://sre.google/books/