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
- Organization size and maturity can affect implementation of SRE principle. We will see in the "implementing SRE" section.

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

**VERY IMPORTANT:** Above DevOps philosophies are guidance to solve the problem, however it do NOT explicitly mention how to implement these philosophies. **Hence SRE comes into play**.

### Origin of SRE?

SRE was born in google in early 2000, separate from DevOps. In 2003, Google appointed a bunch of software engineers to look after development as well as operation. They were responsible for operation of the software they develop. This gave birth to new role called SRE.

**SRE is a concrete set of principles. Its both role and practice**. However, title is not necessary to practice SRE.

SRE both comes of **Technical** and **cultural** practices.

Now how do we map DevOps practices with SRE:

- *Reduce organization silos | share ownership*: SRE defines service level objective(SLO) & error budgets in collaboration developer to define production system. They define reliability and prioritize work. Culturally, it promotes shared vision and knowledge with improved collaborations and communication. **Discussed below in details**.
- *Accept failure | use blamelessness postmortem*: Understand the failure instead of blame. Define strategy to reduce the likelihood of the same failure again. SRE are **comfortable with failure**, by **removing ambiguous monitoring**, and **documenting the process**.Culturally it **promotes RCA(retrospective)** and how to prioritize work.
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

**SRE are class implementing DevOps interface**.

## Who practices SRE

SRE is a role, who practices SRE policies. However role is not required to practice SRE, anyone from IT team can implement SRE principles.

## Benefits of organization by implementing SRE

As discussed previously, implementing SRE practices like **more automation**, **blameless postmortem of failures**, **reduce cost of failure**, along with **bridging the gap b/w dev and ops** help organization to deliver quickly, reducing cost per release along with maintaining the reliability of the services.

Automation helps in scaling as per business needs and customer usage pattern. It also improves innovations within the team as team can focus more on useful work.

Smaller releases and iteration allows fail fast.

## Adopting and embrace SRE culture in organization

Before adopting SRE culture and principles *access organization maturity level for SRE*. Next understand the *skill required* and how to *train your workforce*. Then SRE team implementation and how google cloud can support your organization.

**Access organization maturity level for SRE**:

Three pillar of SRE as we have seen are *SLO with consequences*, (form SRE team here)| *make tomorrow better than today* | *regulate workload*.

Maturity level:

- LOW: No adaptation of SRE principles, practices and cultures
- HIGH: Well established SRE team or widely embraced principles, practices and culture.
  - Well documented and user centric SLO
  - Error budgets - difference between perfection and SLO. They allow IT team to move fast until and unless budget is exhausted.
  - Blameless postmortem culture.
  - low tolerance for toil.

First steps before staffing SRE in the organization are (google recommends) to **define TECHNICAL***(SLOs, err budgets)* **and CULTURAL***(psychological safety, shared vision and knowledge, foster collaboration, design thinking, prototyping and change management, goal settings, transparency, data driven decision)* principals of SRE. SLO and principles are important.

After that(staffing SRE team) we can define automation and regulating workloads.

**SRE skills and trainings**:

Who to hire? either experienced in SRE or need to upscale that engineer(like system administrators with scripting experience) for the SRE role. Train them with engineering skills

Skill and training for SRE? *the below is not a comprehensive list, but good for starting*

- Operation and software engineering
- Monitoring systems
- Production automation
- System architecture
- Troubleshooting
- Culture of trust - communication, agreement and trust
- Incident management- has two sides technical troubleshooting and communication framework.
- Time and task management
- Record keeping.

**SRE team implementation**: google SIX recommended implementation of SRE team.

- Kitchen sink or everything SRE:
  - Scope is unbounded
  - its a good place to start if there you have never created a SRE team.
  - best fit for organization with few application and user journeys.
  - dedicated SRE team is necessary team is required even tough there it's only one SRE team.
  - advantages:
    - no coverage gaps as only team is in place.
    - its easy to spot patters and similarities between services and projects.
    - act as a glue between desperate dev teams.
  - disadvantages:
    - usually lack of team charter
    - risk of overloading a team
    - in overtime it grows from deep understanding of everything to sallow contribution.
    - Team issues can have a negative impact on the business.
- Infrastructure
  - this type of team focus on behind the scene tasks.
  - it help in other team's jobs easier and faster.
  - maintain services related to infrastructure.
  - best fit for large organization with multiple dev teams.
  - they define common standard for IT(dev) teams
  - its common for large organization to have both infrastructure DevOps team and SRE team. DevOps team focus on features and SRE focus on reliability.
  - advantages:
    - allow developer to use DevOps practice without divergence across business.
    - focus on highly reliable infrastructure.
    - define production standards.
  - disadvantage:
    - depending on scope of infrastructure sometime it has possible negative impact on the business following a team issue.
    - lack of direct contact to the customers, improvements the team make not necessarily be tied to customer.
    - further growth of the company, there may be split in the team which may lead to split of the team. this may lead to duplication of infrastructure and divergence of practices. This is against SRE practice of knowledge sharing and collaboration.
- Tools
  - focus on tools
  - it builds software to help developers with aspects of SRE work. such as capacity planning tool.
  - they are generally not aware of the actual problem faced by frontline SRE team to develop proper tools are required.
  - fit for organization that need highly specialized on reliability-related tooling.
  - advantages
    - similar to infrastructure team
  - disadvantages
    - similar to infrastructure team and
    - they can unintentionally turn into an infrastructure team.
    - risk of increase toil and overall workload on the team. This can be controlled by appointing a team charter.
- Product/Application
  - work to improve the reliability of a critical application or business area.
  - Best fit for team which already have a kitchen sink, infrastructure and tool SRE team and also have a application with high reliability needs.
  - advantage:
    - clear focus on the team effort.
    - it also provides clear link between business priorities and team effort expenditure.
  - disadvantages
    - when team grows companies will need new team for every complex application.
    - it can duplication of infrastructure divergence of practices.
- Embedded:
  - SRE embedded with developers
  - SRE and developer have  a project or time bounded relationship
  - SRE are hands on and capable of changing codes and configuration of services.
  - they can augment infrastructure or tool team.
  - best fit for teams to start a team or scale another implementation.
  - advantages:
    - it focus on expertise directed to specific problems or teams
    - it allows side-side demonstration of SRE practices. Very effective teaching method.
  - disadvantage
    - lack of standardization between the team (hence it should not be for long times)
    - it can lead to divergence in practice
- Consulting
  - very similar to embedded. Consulting SRE are less hands on and hence they don't change the code or configuration.
  - they may write code and maintain tools for themselves and developer.
  - one or two part-time consultants are recommended before you first stuff your SRE teams.
  - best for large organization which have very complex systems.
  - advantages:
    - help with the scaling of an existing SRE teams positive impact.
    - its is decoupled from directly changing application code or configuration.
  - disadvantages:
    - sometime consultant lacks sufficient context to offer useful advice.

Below are technical and cultural behavior and how to achieve these.

### Step-1: Define reliability

**SRE also are responsible to make everyone(from dev to VP) agree on how to measure service reliability and what to do if you fall short**.

Simple approach to define reliability: *good time / total time = fraction of time the service is available and working*

The above approach do not work well for complex distributed system. *How do you measure good time if one of the server is down*
Thus sophisticated approach is: *good interactions / total interaction = fraction of real user for whom service is available and working*

### Step-2: SLO

**In simple words, SLO is precise numerical target for system reliability**. There targets are shared between the stakeholders.

Need to define SLO with consequences. **Performance of the services relative to SLO should guide business decisions**.

For defining SLO we need SLI **how well a service is doing at any point in time**. Its a quantifiable measure of service reliability. SLI recommended to be percentage of good events and valid events. *SLI of any parameter 0 means nothing is working and 100% means everything is working*.

SLI are **mapped to user expectation** such as *response time*, *latency*, *availability*, *data collection processes and freshness*, *storage latency and throughput*.

Now, **SLO is aggregated of SLI over time**. SLO is a line between **happy and unhappy customers**. SLO are just short of SLI 99.9%.

**SLA is a promise to your customer about the health of the service**. What you are going to do **if SLO fails**, such as refunding money. SLA are associated with consequences when violated.

**Why SLO is required when SLA is already defined**? SLO are measures to catch those issues(which are potential factor for breach) before it breaches SLA, and to fix or take care of them. *SLO are generally stronger than SLA* as customer are already affected before SLA are already breached.

**Difference between SLA and SLO**? SLA are external promises made to customer and when breached it comes with costly compensation. On the other hand SLO are internal promises (generally stronger than SLA) which act as a safeguard for SLA.

**SLO are stronger than SLA, but how much stronger**? this is decided by happiness test. SLA is the breach of promises, but when SLO are breached the customer turns happy to unhappy. So SLO should be defined in such a way which can clearly distinguish happy and unhappy customer. IF target SLO are met all customer should be happy, and if they are missed there are unhappy customers.

*IMPORTANT TO NOTE: SLO should consider all the user(user differentiated by devices, user differentiated by timezone, bots - non human).Spread of a outage may not be spread out equally, but SLO are aggregates across user base*.

**How to set SLO for SLI**? SLO is a target that you need to pick (like 30 days, one quarter). SLI will tell us weather a certain point in time was good or bad. Let take an example: Suppose SLO is *99% of request is server within 300 milliseconds over a time period of 4 weeks*. then we can use SLI to check weather that is met during that time.

**Measure reliability**: As discussed above use SLI to measure reliability. SLI always correlates with users.

For example: *load balancer is slow or database is down or having low throughput do NOT impact user directly hence these are not proper SLI. What matters to user is slowness of the application, if we can quantify slowness, then only we can define how happy users are in aggregate. Now we can quantify slowness with different type of matrices - CPU utilization, Load average, Memory usage etc. But these matrices do not depict if users are happy or not. METRIC WHICH DEFINE SYSTEM AS WELL AS CUSTOMER HAPPINESS ARE TREATED AS SLI. IN OTHER WORDS, IF METRIC DATA IS SAME(or almost same) FOR BOTH HAPPY AND UNHAPPY USERS, THEN THE METRIC IS CONSIDERED AS BAD METRIC*.

There should be proper co-relation between bad events and unhappy users and good events and happy users.

Overlap creates acceptance of false positive risks, false negative risks or middle ground.

**What are the right level of reliability for the system you support**? mostly found it has different value or sometime never discussed
**What to promise and to whom**?
**What matrices to measure**?

**How much reliability is good enough**? 100% is wrong. Try to measure the current situation by analyzing SLI targets. Define target SLO slightly greater than that. Agree with all the stakeholders, developers, and product teams need to agree on the target. But don't be too reliable user tends to depend on it.

**NOTE**: there isn't a linear relationship between service reliability and user happiness. Once you pass the happiness test, increasing the availability more have a diminishing effect. Also, if service is too reliable than customer ISP, anyway its going to fail.

**Summary**:

- already thought about the characteristics of reliability that you want to measure.
- figure out SLI to measure
- set SLO as target.
- *remember*: *running service with SLO is an adaptive and iterative process. Your initial SLO may not be good fit for first 12 month. (due to many reason: such as all customer are not included, all new features are not covered)* Hence the next and last part of defining SLO is to review the SLO and SLI over time (quarterly and then iterative review after that in a duration of 6 to 12 month).

### Step-3: Error budget

**Amount of unreliability you or organization wants to tolerate is called error budget**. Reliability should not be 100% as it results in 0% error budget, in this case pushing new features, system patches, security upgrade, network upgrade will become very difficult/impossible.

**Err budgets are great incentives for devs and SRE**. Error budget can be considered as a household budget, you need a budget to buy something. Generally if error budget burns out team(dev and SRE) focus on reliability. Then when error budget is restored by making service bit reliable team focus on application feature. This loops goes on and it helps us to balance between feature and reliability.

**Error budget helps prioritize engineering work**. It gives right balance between innovation and reliability. Dev team can now manage their own error budget, as they know setting unrealistic error budget will slow down their work.

Example-1: 99.9% SLO over 30 days means (30 days * 24 hours * 60 mints) = 43200 | 99.9% of 43200 is 43156.8

hence error budget is 43200 - 43156.8 = 43.2 ~ 40 mints.

Example-2: 99.99% SLO over 30 days means out of 43200 mints, 43195.68 should be available

hence error budget is 43200 - 43195.68 = 4.32 ~ 4 mints. This is not enough for human interference, hence system should be able to detect and self heal complete outages to meet the goal.

similarly 99.999% SLO give only 24 seconds of error budget.

**Advance techniques** to utilize error budgets:

- altering the pace of feature release dynamically, based on the availability of error budget.
- Rainy day fund. Which is a cover on error budget that is kept safe for unexpected events.
- Error budget based alerts - alerts team with exhaustion of err budget.
- Silver bullets - this are error budget given to the senior member of the team. If dev team already exhausted the budget, SRE team will stop the release. In this case dev team need to present the feature and explain the importance of the feature to get a token which will allow them to release the feature. Issue of silver bullet is treated as a failure and request for a postmortem.

If you are frequently exhausting error budget, then its better to work on reliability of the service.

### Step-4: Cultural shift due to SLO and error budgets

create **Unify vision** | foster **collaboration** | improve **communication** and share **knowledge** b/w teams.

**Unified vision**:

- Team vision should align with company's vision.
- Vision consist of **values**, **purpose**, **mission**, **strategy** and **goals**.
  - **Values**: response to others | commitment to goals | way we spend time | how to operate a team. *this helps to create psychological safety with each other* | *take risk for innovation* | *greater sense of inclusion and commitments*.
  - **Purpose**: why that team exists | improve life & work satisfactions | stronger connections | reduce conflicts.
  - **Mission**: clear and compelling goal that the team want to achieve. for ex *To organize the world information and make it universally accessible and useful*
  - **Strategy**: how it realise its mission. can be single initiative | change in investment and how work is done | can be leveraged. Building block of strategies are to *identify* threats and opportunities, *Understand* and *consider* strategies for addressing threats and opportunities and *create*.
  - **Goal**: what team or company is striving to attain. Goals can be defined using **OKR**. *learn more about OKR below in the OKR section*.

**Collaboration and communication**:

- One of the high priority within the SRE teams.
- helps in solving common approaches to platform.
- Ways to improve:
  - *Service Oriented meeting*: SRE team review the state of the service they are in charge | audience: stakeholders and its compulsory | objective is to raise awareness and to improve the operation of the service. | weekly for 30 - 60 mints | designated lead | agenda: downtime, production changes, patches, metrics, paging and non-paging events and action items.
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

- CODE >> BUILD >> INTEGRATE >> TEST >> RELEASE >> DEPLOY >> OPERATE
- `<--agile dev-->`
- `<----------------CI----------------->`
- `<-----------------------CD--------------------->`
- `<--------------------------DevOps------------------------------->`

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

### Step-6: toil automation

If we touch system manually during normal operation we will have bug.

**What is toil?** is a manual, repetitive, automatable, tactical, without enduring values, scales linearly.

**Toil can lead to**:

- career stagnation(people will have too much to work on toil instead of actual project),
- low moral (too much toil leads to boredom),
- confusion,
- slower progress,
- precedence (if we are already working with toil, dev counterpart will come up with more toil, sometime shifting some of the operational task which must be done by developer are pushed to SRE),
- attrition (employee will look for other rewarding job), and
- breach of faith (mostly with new comers, who are promised with dev work are given responsible with toil)

**Bit of toil has advantages, 100% automation also has its tradeoff**. Some amount of toil is unavoidable in SRE role or any other engineering role.

Till now we have learnt about **reliability** in SRE, **Engineering** is a another main part. In engineering we mean system to scale up along with maintaining reliability and allowing dev team to work faster.

**Measure toil**: in three steps

- *identify toil*: who can identify toil depends on organization, commonly they are stakeholder who do the actual work.
- *Select an appropriate unit of measure*. Measure amount of human effort required for the toil. For example minutes and hours are often use.
- *Track these measurement continuously*. before, during and after toil reduction effort.

You can depend on a ticketing system like JIRA or directly ask the person about estimate of toil per day or week. Common ways are count the number of tickets received | Count the number of alerts | collect stats.

Benefits of measuring toil are:

- Trigger a toil reduction effort. (Identifying and quantifying toil can lead to eliminating it at its source. )
- Empowers team to think about toil.
- growth in engineering project work over time, some of which will further reduce toil,
- increase team morale and decrease team attrition and burnout,
- less context switching for interruptions, which raises team productivity,
- increased process clarity and standardization,
- enhanced technical skills and career growth for team members,
- reduced training time,
- fewer outages attributable to human errors,
- improved security and shorter response times for user requests

**Remove toil**: most important is automation - WHAT to automate & HOW to automate it.

**Benefits of automation**: consistency | reusable and applied to new platform | quicker resolution | save time.

SRE's time:
0 to ~20%: toil (must be bounded part of SRE role)
20% to 50%: remove toil
~50 to 100%: project work of reliability and engineering work.

**Psychology of change and resistance of change** : Change elicit emotions (can be of different type both positive and negative).

- **Navigators**: people who help you|team|organization succeed. You should *celebrate their behaviors* | and *use them as champions*.
- **Critics**: they have passion and energy and have valid fears. You *Shouldn't ignore them* | and *spend time to persuade them*.
- **Victims**: express emotions and considers changes as personal. You should *listen to them* | and *empathize them*.
- **By standards**: They are tricky, as we don't know what they are thinking, and often either they don't know and they continue with normal routine. You should *communicate with them* and *ascertain their feeling*.

People may have multiple emotion. Emotions are natural and they are not trying to be difficult forcefully.

Below are steps we can take to come over the emotions

- Involve people in change
- Set realistic expectation
- Identify opportunities for co-creation and provide coaching rather than solution.
- Simplifying messaging and focus on key concepts per user group.
- Ensure that communication are engaging and training is interactive.
- Allow people to build new habits.

Changes to be presented as opportunity and not as a threat.

We should speak to individual in three levels:

- head (rational) : speak about change why its happening (mission, vision and rational behind it)
- heart (emotional) : speak about why people care about this change, explain them how it will impact them positively in day to day role. Try to make them as part of the change.
- feet (behavioral): talk about the knowledge skills and resource they will be provided with to make sure they are successful with the change.

**Research have shown resistance is the primary reason why changes fail in business**. Resistance is fear of loss (it can be job, role, competency, or advantage or many)

**Handling resistance to change:** keep the below checklist handy as a SRE

- Are all your leaders and managers **role modelling** the new processes and behavior?
- Do people **understand the reason** for change?
- Do people **care about the change** being successful?
- Do people have the **knowledge and ability** to be successful in your new world?
- Are the right **reinforcement and recognition** program in place?

If any of these are NO, then leadership to brainstorm and get it in the right place before starting to change. All these are required for any major organizational changes.

### Step-7: Measuring everything

**Why to measure everything, goals**?

- IT and business can **understand** the current status of the services.
- IT can analyse the data and identify necessary actions to improve the status.
- IT can make better decisions and impact across the organizations.

**What to measure**?

- measure toil (discussed in Step-6)
- measure reliability(discussed in step-3)
- monitoring

**monitoring** allows visibility into the system.

What to monitor? - symptoms rather than causes. like error budget burn. Too much symptom based metrics may give some false alerts are which are not necessary.

four GOLDEN signals

- Latency
- Traffic
- Errors
- Saturations

Monitoring can be combined with good debugging tools like dashboard, which will give more insight to the problem.

**Cultural changes to support measurement of everything**:

- *culture of goal settings*
  - process of goal settings
    - look at KPI, for whom and for what you are measuring. *Refer to that in the `architecting_on_GCP.md`*.
    - approach, what to measure and how.
    - Example of google: OKR are treated as KPI. OKR are generally graded from 0.0 to 1.0. 1.0 indicates fully achieved OKR.
- *transparency*: "is the only way to **demonstrate** to your employees that you believe they are **trustworthy** adults and have **good judgement**. And giving them more context about **what is happening** will enable them to do their job more **effectively**.
  - to achieve transparency
    - sharing monitoring tools (between IT and SRE)
    - Sharing communication & feedback loops
    - feedback loops are: **produce** something >> **measure** information on production >> use information to **improve** production. It's a constant cycle of monitoring and improvements.
- *data-driven decision*: "is another important in SRE culture".
  - First try to remove any unconscious biases. Unconscious biases are social about particular groups that people form without realization. Removing them is necessary as they don't create inclusive environment to work with. It also corrupts healthy work environments.
    - affinity bias: bias those are similar(in race, gender, color, nationality, education level, social background) to you.
    - confirmation bias: tendency to find information, input or data that supports your pre-conceived notions.
    - labeling bias: bias against how people look, dress and show externally.
    - selecting attention bias: pay attention to things, ideas and inputs from the people whom you gravitate towards.
  - How to remove biases:
    - question your first impression, don't stop at the first impressions. Specially when you promote, hire or add to the team.
    - Justify your decision. Tell people what you did, and why. If you are accountable for any decision then you are more likely to be biased.
    - Make decision collectively.

## CRE

Customer reliability engineer are google SRE which are externally focused to bridge the gap between the organization and cloud providers. *Note we are NOT talking about reducing organizational silos within the same company*.

This is required as hosting everything cloud environment has dependencies on SLO and SLI of the cloud providers. In other words, in order to define SLI and SLO of your application (which is deployed on any cloud environment) you need to depend on SLI and SLO of other cloud provider as well.

Same aspect goes with external APIs.

Three pillars of CRE are:

- reliability is most important feature.
- User, not monitoring decide reliability.
- Well-engineered system: 99.9 or 99.99 or 99.999. Start with 99.9 and gradually target for 99.99 and so on.

CRE helps customers to create a reliable service on top of cloud stack.

## OKR

**OKR** - Objectives and key results. OKR helps to set our ambitious goal and track our progress.
    - **OKR**: purpose of OKR is to set very ambitious goals
    - *Try* new things, *prioritize* new work, and *learn* from success and failure.
    - Every OKR may not be fulfilled, but team can strive to meet the goals.

### OKR Grading consideration

- 60-70% is good score
- OKR are not synonymous with performance. Instead it shows individuals contribution and impacts.
- Organization OKRs are graded publicly so everyone can see their progress.
- Frequent check-ins throughout the quarter help maintain progress.

### Examples of sample OKR

**Objective**: Expand into the Latin American market and capture 15% of market share from our competitors in one year.
**Key Results**:
Conduct comprehensive LATAM market research and SWOT analysis report and deliver to senior management by Jan. 31st
Hire and train 4 bilingual sales executives by Feb 10th
Launch Spanish-language MVP version of product with top 5 requested features by March 1st

**Objective**: Achieve record revenue while maintaining profitability
**Key Results**:
Increase sales of new enterprise-level accounts from $31M to $50M
Expand add-on service revenue from existing customers from $12M to $22M
Optimize headcount and negotiate contracts to maintain 10-11% profit margins

## Edge cases of reliability

There are edge cases and everything is not linear. We don't always want or need the same level of reliability for a service.

There are many organization that do not confirm to a single SLO for everything. **NOTE**: impact of outage is not constant over time.

Example-1: Impact on retailers on black friday is more than impact on normal days. So retailer like amazon, ebay may shift their SLO from 99.9 to 99.99 to be more cautious. Strengthening of SLO is supported by scaling infrastructure, code freeze and war rooms.

**NOTE**: outage duration can impact customer happiness.

Example-2: four one hour outage, one four hour outage and 0.5% error rate through out are all same in terms of error budget, but customer tend to choose one over another.

**NOTE**: your customer base ca be bots for certain services. Or some user cares about SLO and some do not. We may need to have different SLO for each type of customer and based on customer feedback its important to tweak the SLO.

Example-3: automated - bots as user (probably scraping your API to get data) may get more errors than human user as they do not behave the same way user does. Hence SLO may change for those category of user.

## Example of reliability

Netflix:

**How do we measure reliability**? - as normal user we care about *time to start playing*, and *no interruption or issues with playback*.

For the above: *request latency* can be treated as SLI and *error rates* is the ratio of (error or success)/(total request) or also (error or success)/(throughput).

Latency can be measured as "time to first byte to application server" or "time to play back as seen by the client". There are some tradeoffs.

## Reliability improvement

- deploy small changes.
- add redundant infrastructure (by this we avoid single amount of failure)

## Calculate expected failure and how to improve

How to improve is already discussed above, but discussing it here with corelation of failure.

**E(expected failure): (TTD(time to detect) + TTR(time to resolution)) * % impact / TTF(time to failure)**.

TTF: expresses how frequently you expect this particular failure to occur.

we must try to decrease the value of TTD, TTR and impact% and to increase TTF to reduce impact of failure.

to reduce TTD we can implement monitoring tool along with debugging tools and add automated alerting system. For TTR we can take help of toil and automation and by creating a playbook of outage scenarios. For percentage of impact we can take help of canary deployments or run you service in a degraded mode(like allowing read only operation but writes). Lastly to increase the TTF: using health checks, avoid single point of failure.

Operation approach to increase reliability. Here we discuss other factors apart from TTD, TTR, TTF and impact% which can be tuned to improve reliability.

- Report on worst customers, worst region or other category to find cases where error budget is NOT evenly distributed. Extra attention is required there.
- Providing inputs on achieving targets. Engaging product team where possible to discuss on achieving target.
- Standardizing infrastructure helps in easy repeatable deployments without breaking the deployments.
- Consult system design with SRE to better understand the processes and infrastructure before developing the application. It help to catch reliability issues early.
- Bad pushes are inevitable. Hence write code that are easily deployable and rollback. Postmortem are important.
- Canarying - phase rollout.

## Strategies of defining meaningful SLI

Main **complexity of SLI** depends on the **complexity of the service**. There may be 100s of micro services supporting the services however defining 100s of SLI lead to operational paralysis and important of essence is lost in the see of noise and data.

*NOTE: Deterioration of SLI indicate something is wrong, and we can use monitoring and observability system to deep dive on the issue*.

- **Choose right metric**
  - *properties of good SLI matrices*:
    - close approximation or liner relationship with user experience(happiness of user).
    - it shows long term trend clearly. Can be aggregated over long time period.
    - expressed as good events/valid events (why?? as this gives opportunity to define pass and failure rate correlating with user happiness, also they are always represented in percentage which make us easy to understand)
      - valid events: we only consider valid events, and need to discard invalid events while calculating error budget.
    - they are NOT common system matrices like (CPU utilization, load average, memory usage or bandwidth etc) as they are not directly related to user.
    - they are NOT common internal state like (queue length, thread pool) for the same reason.
  - *Common SLI*: any number of root cause collapses to few observable symptoms.
    - *User is responding to request and response*: how fast (latency), unsuccessful request (quality/error) and availability.
      - **availability**: proportion of **valid request** served **successfully**.
        - to change this above definition into implementation we need to answer two questions
          - Which of the request are VALID for SLI?
          - and what make response SUCCESSFUL? - it may be simple or complex depend on the system. We may write a logic which return a boolean and attach it to the SLI monitoring system.
        - formula will be: [request with successful response / valid request]
        - other uses: availability matrics can be used to check VMs like bootable time and able to ssh to the VM.
      - **Latency**: proportion of **valid requests** served **faster** than a **threshold**.
        - to change this above definition into implementation we need to answer three questions
          - Which of the request are VALID for SLI? NOTE: Valid request for availability may NOT be same as latency.
          - When the TIMER for latency starts and stops?
          - and what is the SLO threshold value? setting a threshold fast enough depends on how accurately latency translates to user experience and closely related to SLO target. Most system have techniques like pre-fetching and caching. In this scenario, request may be made by the application in the background and user may not wait for the request.
        - its common to set the target to 95% or 99% when we have single latency threshold. *Means 95 - 99% of the request will be served faster than the single value threshold*. SLO would be something like this "Most requests must be responded to faster than this for our users to be happy." However note that its likely if that user are happier if SLO covered more that one point in the latency distribution this is because relationship between latency and happiness tends to be a **S** curve rather than a linear.*Put happiness in Y axis and latency in X axis, and measure happiness of 75 - 90% of request. The outcome is a S curve*. Hence apart from threshold for 99% request, there should be another threshold for 75 - 90% of the request. But setting threshold for less than 75% of the request, weakens the promise to the customer. *For example we can say 99% of request will be served between 3 seconds and 75-90% request will be served between 1.8 seconds*.
        - formula will be: [request that responded with in threshold/valid request]
        - other uses:
          - async batch processing/work queue task/data processing: Generally latency of long running job are not much cared by user. User care more about time time it take to complete the job, but if the job failed its useful to calculate.
      - **quality**: the proportion of **valid requests** served with **degraded quality**.
        - to change this above definition into implementation we need to answer two questions
          - what are valid request for quality
          - what are degraded quality mean? psychologically degradation of quality is not generally identified until and unless they are severe. However, user may treat "less relevant ads user reducing click through rate". quality of a service can be tracked from the response. Bad response means bad quality and it can be used to track the SLI.
          - SLO threshold allowed? similar to latency, quality SLI can have multiple threshold. *For example: 10 optional backend is each having 99.9% of availability target, with a ability to redirect when overloaded. Hence we can choose 99% of request must be served, 99.9% of the request with no more than one backend*.
        - formula will be: [valid request - request with degraded response / valid request] NOTE: *we are subtracting valid request with degraded request to fetch good request. This is done as its easy to calculate bad request instead of good request*.
        - example quality SLI: *returning results after searching subset of data saved in CPU cycle when overloaded*, *serving stale data from cache because the database is overloaded*.
    - *User is processing data*: Coverage of the data, correctness, freshness of the processed data and throughput of the data in the pipeline.
      - **Freshness**
      - **Correctness**
      - **coverage**
      - **throughput**
       ========================= READ LATER ========================
       A freshness SLI measures the system's performance against those expectations, and can perform those engineering decisions. The suggested specification for data processing freshness SLI is, the proportion of valid data updated more recently than a threshold. Turning this specification into an implementation requires making two choices, which of the data this system processes are valid for the SLI, and, when the timer for measuring the freshness of the data starts and stops. For a batch processing system, freshness can be approximated as the time since the completion of the last successful processing run. More accurate freshness measurements for batch systems usually require augmenting processing systems to track generation and or source age timestamps. Freshness for incremental streaming processing systems can also be measured with a watermark that tracks the age of the most recent record that has been fully processed. Stale serving data is a common way for response quality to be degraded without system making an active choice to do so. Measuring stale data as degraded response quality is a useful strategy. If no user accesses the stale data, no expectations around the freshness of the data can have been missed. For this to be feasible, the parts of the system responsible for generating the serving data must also produce a generation timestamp that the serving infrastructure can check against the freshness threshold when it reads the data. In some cases, it can be important to measure not just that a system processes all the data it should have, but that it produces the correct outputs while doing so. Correctness is something best insured proactively via good software engineering and testing practice, rather than detective reactively in absentia. However, users have strong expectations that data that they have been accessing has been generated correctly, and have ways of independently validating that correctness. Having an SLI to measure correctness on an ongoing basis can be valuable. A suggested specification for data processing correctness SLI is, the proportion of valid data producing correct output. Turning this specification into an implementation requires making two choices. Which of the data this system processes are valid for the SLI, and, how to determine the correctness of output records. For correctness SLI to be useful, a method of determining correctness needs to be independent of the methods used to generate the output of the data. Otherwise, it is probable that any correctness bugs that exists during the generation will also exist during validation preventing the detection of the resulting incorrectness by the SLI. A common strategy is to have golden input data that produces known good outputs when processed. If this input data is sufficiently representative of real user data and is designed to exercise most of the processing systems code paths, then this can be sufficient to estimate overall correctness. A coverage SLI functions similarly to an availability SLI when processing data in a system. When users have expectations that data will be processed and the outputs made available to them, you should consider using a coverage SLI. The suggested specification for a data processing coverage SLI is, the proportion of valid data processed successfully. Turning the specification into an implementation requires making two choices. Which of the data the system processes are valid for the SLI, and how to determine whether the processing of a particular piece of data was successful. For the most part, the system during the processing of the data ought to be able to determine whether a record that it began processing was processed successfully and output counts of success and failure. The challenge comes from identifying those records that should have been processed but were skipped for some reason. This usually requires some way of determining the number of valid records that resides outside of the data processing system itself, perhaps by running equivalent of count star on the data source. Data processing systems may be designed to operate continuously on streams or small batches of data to lower the processing latency observed by users. A latency SLI usually is the best way to quantify this. But the overall throughput of the system may be a better measure when you have promised to provide your users with a given level of throughput or, if their expectations of processing latency are not a constant for example, when the quantity of data processed prevents varies dramatically. The suggested specification for a data processing throughput SLI is, the proportion of time where the data processing rate is faster than a threshold. The structure of this specification is somehow different to a latency SLI because the throughput is a rate of events over time. We fit this into the SLI equation by defining an event as the passage of a unit of time like a second or a minute and a good event to be a unit of time where the rate of processing was fast enough. Turning this specification into an implementation requires making a single choice. The units of measurement for your data processing rate. We generally find that the most common measure of throughput is bytes per second since we can measure the size of each unit of data to be processed in bytes, and the amount of work to do processing each unit of data is often proportional to its size. Any metric scales roughly linearly with respect to the cost of processing should work. The system processing the data ought to be able to record metrics that quantify the rate at which it is processing the data. As with latency and quality, throughput rates are a spectrum where multiple thresholds may be appropriate. You may be able to tolerate operating with a reduced overall throughput for hours or even days if your system is designed with quality of service levels to ensure important data still makes it through quickly while low priority stuff queues up. But if throughput falls dramatically, you're almost certainly going to end up violating someone's expectations.
       ============================================
    - *User is give something to Store, and retrieve later*: then good way to measure the durability of the storage layer.
- **Measure your SLI**
  - Broadly there are five ways to measure a SLI. (each is in increasing order of proximity to customer).
  - We mostly tend to choose more than one(as complementary) for measuring SLI, one for short term(for operational response) and another for long term(for decision making)
    - *Processing server side request logs or data*. This is a good way to track complex user journeys, with many request/response on a single long running session. convoluted logic can be developed(this logic can be written in code of your logs or processing jobs) to process the log data to derive SLI. Then export it to count good event counter.
      - problems:
        - with this approach is that the data is ingested, processed and analysis require bit of engineering work.
        - accurately construct user session
        - add significant latency between event occurring and observed.
        - request that do not make till your server are not at all tracked.
      - hence log based matrices are *NOT good fit for* triggering emergency response.
    - *Processing application matrices* The also suffers same problem as request logs from the server.
    - *Processing front-end LB matrices*: this is the closest point to the user which is under control.
      - Problems:
        - They are also in the cloud infra, hence few request can go unmeasured.
        - LB are stateless, hence there is not way to track user sessions and don't give insight of response data. Only we can check the metadata of the response to determine the response are good or bad. Sometime LB data do not guarantee response are really good or bad as metadata is very high level to determine the response data.
      - Benefits:
        - cloud provider already have mechanism to capture the logs and historical data of LB, hence low or no engineering work is required.
        - its more closer to user than application server or server logs.
    - *Processing synthetic clients*: they are bots, which emulate successful user interaction outside the nearest interaction. And verifies that the responses received are good.
      - Problem:
        - they are bots and they never emulate correct user interaction.
        - additional effort and huge engineering task to design, run and maintain the emulation in realtime.
    - *Client-side instrumentation*: get the data from client side matrices to measure SLI.
      - Problem:
        - telemetric data have huge latency. Because of this triggering short term operational response is not possible just like log processing.
        - they are against user trust
        - and for mobile user this is against battery life.
      - Benefits:
        - we can include reliability of the third party systems like CDN or payment systems.
- **then select the target for the SLI**
  - Once we have SLI matrices and we know how to measure them to get good co-relation with user activity, we need to select a target for the SLI.
  - Also known as *reliability target* or *SLI target* or *SLO targets*.
  - *Its not feasible to measure user happiness directly. We have to derive it from social media, noise around the third party or by feedback loop, or from Past performance metric or logs. In google the maxim is "User expectation are strongly tied with past performance"*. **NOTE**: historical data is important to take data-driven decision while choosing the target. If historical data is NOT there start collecting the data. Its not mandatory to have SLI target defined as soon as you have SLI defined. We can collect the data and make a conscious and data-driven decision later. Then we iterate and refine the target continuously. **This way of setting SLI target is known as ACHIEVABLE SLO**. This is the best way to get started. However, **downside** of this approach is that we are only assuming that user are happy with the current status. And more over we cant validate this from anywhere.
  - **What if you want to have you SLA from day-1**? OR **What if you know your past performance is not good enough**? OR **What if you know users are sticking with you as other competitor are worse**? OR **what if you know that your service can be far better than customer happiness**? All these scenario are based on business needs and not on past data. In this case we need to set SLO known **as ASPIRATIONAL SLO**. These SLO are not intended to meet at first but to improve iteratively.
  - In both ASPIRATIONAL SLO and ACHIEVABLE SLO, target is the not the main intension, target is to make our service better as possible keeping our user happy.
- **refine an SLI implementation**
  - Technically both aspirational and achievable SLO should be same, but they diverge.
  - Once we set the SLO target for the first time, we can then collect data from social media, user forum and support team to gather more matrices and draw the pine correctly.
  - Initially revisit the SLO more frequently than once you have confidence you can lower the pace(google recommends at least once a year) of revisiting the pace.
- **reduce SLI complexity**
  - **Best practice:** choose only 1-3 SLIs max per user journeys. This is because each SLI increases the chance of conflicting signals and adds a cognitive load on ops team and resolution time.
  - **How to maintain the above best practice if our system is too complex**:
    - Prioritize the important user journeys. *this is very common, there are long list of SLI after considering only important one*.
    - Second, aggregate SLI: many user interactions are common but they are considered as separate journeys. *Refer example in the aggregating section below*. **NOTE the disadvantage of aggregation**: simple aggregation works well, but when request rate differs heavily there is a risk that small but significant journey get lost in the noise. Grouping journeys based on request rate and priority can eliminate the aggregation disadvantage to some level.
    - bucketing: this can be applied when we have different thresholds for Latency, freshness, throughput SLI for certain label(category of request), then we can also apply different threshold in the distribution. *For example: human read transaction - 400ms(annoying) & 1s(painful) | human write - 1500ms(annoying) & 2s(painful) | background transaction - 5s. NOTE: annoying is small number of request generally 50-75% and painful is 99% of the request*.
      - last bucket you need to consider is third party(where we don't have control over) like payment gateway, identity providers etc. Most of the time user understand and probably don't hold us responsible for delay of these service. We can set a reasonable target from the past transaction. Or sometime External API comes with SLA as well so that we easily build on top of the SLI.
- Set SLI target to form SLO.

## Implementing SLO and SLI for a user journey (HANDS On)

**Example Game**: *The rise of the vampires has taken a devastating toll on humanity, forcing those who survived to cluster together in the few remaining habitable regions, far from previous centers of civilization. As the leader of the tribe of survivors, you must recruit people to your cause, secure, and upgrade your settlement, raid vampire-occupied cities, and battle other tribes for control of resources*. Sounds like fun. *The game world is setup into a number of areas and varying rewards and challenges*. *Access to areas with better rewards is gated by overall playtime, settlement size, and in-game currency expenditure*. *Each area has its own leader board ranking the top tribes*. We have around 50 million 30-day active users playing, with between one million and 10 million players online at any given time. We add new world areas once a month, which drives a spike in both traffic and revenues. **The primary revenue stream stems from the exchange of real-world money for an in-game currency via in-app purchases. Players can earn currency without paying for it, by winning player-versus-player battles, playing mini-games, or over time via control of in-game resource production**. *Players can spend in-game currency on settlement upgrades, defensive emplacements for battles, and by playing a recruitment mini-game that gives them a chance of recruiting highly skilled people to their tribe*. *Our game also allows players to log in to their account via web browser and keep track of their settlement while they aren't actively playing on their device. One of the things players can do while logged in, is visiting the profile page for their in-game tribe*. The game has both a mobile client and a web UI. The mobile client makes requests for our serving infrastructure via JSON-RPC messages, transmitted over RESTful HTTP. It also maintains a web socket connection to receive game state updates. Browsers talk to the web servers via HTTPS. Leader boards are updated every five minutes. In the next video, we'll delve into a simple user journey served by this infrastructure.


This is a **four step** process

### Choose an SLI specification

High level SLI specification by referring SLI menu.

### Choose SLI implementation

Events you want to measure and what defines good and valid events.
Mention where and how SLI will be measured.

### Walk through the user journey and look through the coverage gaps

### Set aspirational SLo target based on business need

## Example of aggregating SLI

Google Play store

- Below four are different user journey:
  - Visiting google store home page by launching the app.
  - Launching the app and search for store
  - Launching the app and search by the category
  - Launching the app and search by genre

All the above journeys are similar from user perspective and can be combined to a "browse store" meta journey. Since play store is a request/response service we use availability and latency as our SLI.

|journey    | good (availability) | fast (latency)  | valid |
|   ---     |     ---             |     ---         |   --- |
|home       |     9994            |     9866        | 10000 |
|search     |     9989            |     9729        | 10000 |
|category   |     9997            |     9913        | 10000 |
|details    |     10000           |     9848        | 10000 |
|   ---     |     ---             |     ---         |   --- |
| total     |     39980           |     39356       | 40000 |
|   ---     |     ---             |     ---         |   --- |
|browse     |     99.95%          |     98.39%      |       |

## Google Free SRE books

https://sre.google/books/