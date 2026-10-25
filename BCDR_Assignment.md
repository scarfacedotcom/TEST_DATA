**INTERNATIONAL CYBERSECURITY AND DIGITAL FORENSICS ACADEMY**

Business Continuity and Disaster Recovery Assignment

GRC205 Incident Management and Business Continuity Week 21

Name: Nguveren Monica Dzuamo

Student ID: 2025/GCR/12874

Act as the Business Continuity and Disaster Recovery Coordinator for a fictional training institute whose main site becomes unavailable. Use the supplied data to assess business impact, set recovery objectives, select an affordable strategy, and demonstrate whether the proposed recovery sequence can meet business needs.

| **Assessment detail**     | **Requirement**                                        |
|---------------------------|--------------------------------------------------------|
| Assessment type           | Individual assignment \| Complete all six tasks        |
| Total marks and weighting | 100 marks \| 30% of the final course grade             |
| Submission                | One Word document through the E-Campus assessment page |
| Deadline                  | As published for this assessment in E-Campus           |
| Suggested effort          | 12 to 16 hours                                         |

## Learning outcomes

- Conduct a Business Impact Analysis (BIA) and prioritise critical functions.

- Justify recovery time and recovery point objectives using business requirements.

- Compare alternate sites and backup strategies against cost and capability.

- Coordinate continuity, disaster recovery, and incident response responsibilities.

- Test recovery assumptions and turn findings into measurable improvements.

## Report requirements

Submit 3,000 to 3,500 words, excluding the cover, tables, reference list, and appendices. Present the six tasks in order. Include calculations, the BIA and recovery objective matrices, a strategy comparison and budget, a coordinated plan, a recovery schedule, an exercise log, and a performance dashboard.

The six tasks carry 95 marks. Report quality and referencing carry 5 marks. A score of 80 out of 100 contributes 24 out of the available 30 points to your final course score.

# Business context and impact data

## Northbridge Skills Institute

Northbridge is a fictional education provider with 1,800 learners and 90 staff. At 08:00 WAT on Day 0, a Monday, flooding and a power failure make the main site and its local systems unavailable. Facilities estimates that the site will remain inaccessible for 72 hours. No cyberattack has been confirmed. You coordinate continuity and recovery from the time of disruption.

Microsoft 365 identity and email remain available through mobile internet. Local applications use a separate local directory, AUTH01. An alternate facility can provide 25 workstations from 10:00. Of the 120 learners scheduled for an 11:00 examination, 40 need centre workstations and 80 can use their own devices. Two technicians are available for disaster recovery. Business coordinators can organise temporary services and learner support.

## Functions requiring a BIA

<table>
<colgroup>
<col style="width: 27%" />
<col style="width: 59%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Function and local systems</strong></th>
<th><strong>Operational constraint and impact</strong></th>
<th><strong>NGN per hour</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>F1 Teaching and assessment<br />
LMS01 and DB01</td>
<td>The examination starts at 11:00. If no acceptable assessment service is available by then, add a one-off rescheduling cost of NGN 120,000. Learner access and assessment integrity matter.</td>
<td>60,000</td>
</tr>
<tr class="even">
<td>F2 Fees and finance<br />
FIN01 and DB01</td>
<td>Fee confirmation is due by 16:00 on Day 0. The external payment provider remains available, but local receipts and wallet records cannot be updated. Reconciliation is necessary.</td>
<td>40,000</td>
</tr>
<tr class="odd">
<td>F3 Admissions and registration<br />
REG01 and DB01</td>
<td>Admissions close at 18:00 on Day 0. New applications and registration changes cannot be entered into the local system.</td>
<td>20,000</td>
</tr>
<tr class="even">
<td>F4 Staff payroll<br />
HR01 and DB01</td>
<td>The bank submission deadline is 12:00 on Day 1. Incorrect or duplicate payroll instructions could affect staff and require manual correction.</td>
<td>10,000</td>
</tr>
<tr class="odd">
<td>F5 Records and certificates<br />
FS01</td>
<td>Certificate and record requests have a 48-hour internal service commitment. Files must retain integrity and access restrictions.</td>
<td>5,000</td>
</tr>
</tbody>
</table>

For Task 1, treat the hourly amounts as separate, non-overlapping incremental disruption costs. Apply them for the first 24 hours and add the examination rescheduling cost once when its trigger is met. Calculate the 8-hour and 24-hour impact assuming no recovery or continuity measures. These are exercise estimates, not observed losses.

## Dependencies and minimum service

F1 to F4 require the recovery network, AUTH01, DB01, and their respective application. F5 requires the network, AUTH01, and FS01. All functions also depend on available staff, secure access, and communication. Define a workable minimum service for each function, including the approval and record controls for any manual process.

# Recovery evidence and planning options

## Available backup checkpoints

At the 08:00 disruption, the offsite backup catalogue contains the following items. Task 5 uses a baseline drill in which these items pass integrity checks. The tabletop injects later test what happens when that assumption fails.

| **Item**                   | **Data checkpoint WAT** | **Recovery dependency**                                                                                        |
|----------------------------|-------------------------|----------------------------------------------------------------------------------------------------------------|
| B01 DB01 full backup       | 23:00, Day minus 1      | Base for all four business applications.                                                                       |
| B02 DB01 incremental chain | 07:00, Day 0            | Requires B01 and every required incremental through 07:00. This is the latest recoverable business-data point. |
| B03 AUTH01 snapshot        | 00:00, Day 0            | Local directory and configuration state.                                                                       |
| B04 FS01 full backup       | 23:00, Day minus 1      | Record and certificate files.                                                                                  |

A further disconnected full backup exists at 17:00 on Day minus 3. Production and network backup administration share an administrator identity. The offsite provider holds the encrypted copies, but its access-independence controls are undocumented. Investigate these weaknesses in your backup design.

## Next year strategy options

The annual planning limit is NGN 3,000,000. Each package covers all five functions and shared infrastructure. Add NGN 400,000 annually for independent protected backups and NGN 200,000 for training and tests. Package timings are estimates requiring validation. Use the current drill timings on the next page for Task 5.

| **Package** | **Annual base cost NGN** | **Estimated first critical service** | **Data-loss window** |
|-------------|--------------------------|--------------------------------------|----------------------|
| Cold        | 600,000                  | 24 to 48 hours                       | Up to 24 hours       |
| Warm        | 1,500,000                | 3 to 5 hours                         | 1 to 6 hours         |
| Hot         | 2,400,000                | About 1 hour                         | Up to 15 minutes     |

# Recovery drill data and business impact

## Current warm site drill timings

Start at 08:00. Each action occupies one technician for its full duration. Two actions may run in parallel only when all prerequisites are complete and technicians are free. Actions cannot be split. Durations include their local validation; a function is available after its application or file action completes.

| **Action**                 | **Minutes** | **Prerequisite**                                  |
|----------------------------|-------------|---------------------------------------------------|
| Recovery network           | 30          | None                                              |
| AUTH01 restoration         | 30          | Recovery network                                  |
| Security and backup checks | 30          | AUTH01 restoration                                |
| DB01 restoration           | 90          | Security and backup checks                        |
| LMS01 restoration          | 45          | DB01 restoration                                  |
| FIN01 restoration          | 30          | DB01 restoration                                  |
| REG01 restoration          | 30          | DB01 restoration                                  |
| HR01 restoration           | 45          | DB01 restoration                                  |
| FS01 restoration           | 60          | AUTH01 restoration and security and backup checks |

## Task 1 Business Impact Analysis

**20 marks**

- Build a BIA covering F1 to F5. For each function, record the owner role, users affected, critical resources, dependencies, impact over time, minimum acceptable service, and proposed recovery priority. Include people, premises, suppliers, and information needs.

- Calculate the total estimated disruption cost for 8 hours and 24 hours using the supplied rates and the one-off examination trigger. Show the calculation for each function and the combined total. Explain two limitations of these estimates and distinguish financial impact from learner welfare, reputation, and data integrity.

- Explain how the 11:00 examination and later deadlines affect priorities. Separate business priority from the technical restoration order required by shared infrastructure. Identify at least three important dependency risks.

**Required outputs: five-function BIA, worked impact calculations, and a justified priority sequence.**

# Recovery objectives and strategy selection

## Task 2 Recovery objectives and backup design

**15 marks**

- Define Recovery Time Objective (RTO), Recovery Point Objective (RPO), and Maximum Tolerable Downtime (MTD). Propose and justify numerical targets for each function. State the service level at which you will declare recovery and leave a justified buffer between technical recovery and the tolerable business disruption limit.

- Calculate the age of the latest recoverable DB01, AUTH01, and FS01 checkpoints at 08:00. Map the resulting potential data-loss windows to the affected functions and compare them with your proposed RPOs. Use the disruption time as the reference point. Explain what can be reconciled from temporary records and what cannot be assumed recoverable.

- Design a backup schedule that addresses the RPO gaps. Specify full and incremental or differential backups, retention, offsite placement, and the exact chain needed to restore DB01. Apply the 3-2-1 principle and include an independent offline or immutable copy, restricted access, encryption, and restoration tests.

- Explain why offsite storage or a live replica alone does not establish recoverability. Define how you will check backup integrity, access independence, and the usability of restored data. Label any unverified assumptions.

**Required outputs: objective matrix, checkpoint calculations, and backup and restoration design.**

## Task 3 Recovery strategy and budget

**15 marks**

- Compare the Cold, Warm, and Hot packages against your RTO and RPO targets, staffing needs, geography, supplier dependencies, and the risk of propagating corruption or malicious changes. Treat the quoted recovery windows as planning estimates.

- Calculate the complete annual cost of each package, including both required additions. Identify which options fit the NGN 3,000,000 limit. Recommend one option, justify the tradeoffs, and identify any objective it cannot meet. Document residual risks and who must accept them.

- Compare your recommendation with the estimated 8-hour and 24-hour disruption costs. Explain why a single-outage estimate cannot by itself establish annual return on investment. Identify the evidence needed before approving expenditure or accepting supplier recovery claims.

**Required outputs: option matrix, itemised budget, and a justified recommendation.**

# Coordinated continuity and recovery plan

## Task 4 Business continuity and disaster recovery plan

**20 marks**

- Prepare a coordinated plan with scope, activation thresholds, an authorised decision maker and deputy, escalation, contact roles, alternative communication, and situation reporting. Define how the continuity team, technical recovery team, facilities staff, and incident response team work together.

- Create a RACI matrix for at least six activities, including activation, temporary assessment delivery, backup validation, restoration, stakeholder communication, and return to the primary site. Give each activity exactly one accountable role and at least one responsible role. A combined A/R role is acceptable.

- Design temporary procedures for F1 to F5 during the 72-hour site outage. Address the 25-workstation limit and 40 learners needing a centre workstation. Explain approvals, accessibility, assessment integrity, privacy, record keeping, and later reconciliation. Identify the minimum staff, equipment, and supplier support required.

- Write a DR runbook with ordered actions, prerequisites, owners, completion checks, and contingency actions if a step fails. Include backup selection, validation, application and data checks, business acceptance, and rollback. Distinguish restoring technology from resuming an acceptable business service.

- Provide a stakeholder communication matrix and a 120 to 180 word initial learner notice. Explain when possible compromise would trigger incident response involvement. Define safe return to the primary site, controlled transfer of new records, and final sign-off after facilities clearance and business validation.

**Required outputs: coordinated BC/DR plan, RACI, temporary procedures, DR runbook, communication matrix, and learner notice.**

# Recovery validation and program governance

## Task 5 Recovery schedule and exercise

**15 marks**

- Using the current warm site timings, produce a schedule with action, technician, start time, finish time, and prerequisite. Respect the two-technician limit. Determine the earliest possible restoration of assessment service and a feasible completion time for all five functions. Show the dependency path that controls the assessment finish time.

- Calculate each function's elapsed recovery time from 08:00 and compare it with your RTO and MTD targets. Compare restored checkpoints with your RPO targets. Label these as modelled baseline results, not a live test. Explain which deadlines need a continuity workaround even when restoration is successful.

Design and walk through a 45 minute tabletop exercise using these injects. You may simulate all participant roles individually.

| **Exercise time** | **Required inject**                                                                                                        |
|-------------------|----------------------------------------------------------------------------------------------------------------------------|
| Minute 10         | The site closure extends from 72 hours to five days.                                                                       |
| Minute 20         | The alternate facility can provide only 15 working workstations.                                                           |
| Minute 30         | A DB01 incremental backup fails its integrity check. An unexpected backup administrator logon also requires investigation. |
| Minute 40         | The payment provider reports successful payments absent from the restored finance records.                                 |

- Record a decision and revised action for every inject, including its owner, rationale, and effect on service or recovery. Keep this stress scenario separate from the baseline schedule. Produce at least five corrective actions with priority, owner, target date, and measurable completion evidence.

## Task 6 Governance and performance measures

**10 marks**

- Assign plan ownership and approval. Propose a risk-based testing calendar with review triggers, training, version control, and distribution. Map at least four of your outputs to NIST SP 800-34 planning steps and four to the ISO 22301 themes covered in the slides. Explain one relevant flood or climate consideration.

- Define at least four KPIs with formula or measurement method, data source, target, reporting frequency, and accountable owner. Include recovery performance, restoration-test coverage, corrective-action closure, and training. Assess current maturity using the slide 13 model and propose a realistic 12-month improvement target.

## Submission and authorship

Name your file GRC205_BCDR_Assignment_StudentID.docx. Include your name, student ID, official email, word count, all tasks, calculations, and references. Cite the teaching slides and at least two authoritative sources. Acknowledge AI assistance under the course policy. Keep scenario data fictional and be ready to explain your decisions. Use the deadline and extension controls published in E-Campus.

**AI Declaration & Author Transparency**

**Academic Integrity Statement:** In accordance with ICDFA course policy and academic integrity guidelines, I declare that generative AI assistance was utilized as a technical drafting and calculation verification aid during the preparation of this assignment. Specifically, AI tools were used to assist in formatting Word XML structures, checking linear impact calculation arithmetic, and structuring response templates against the task rubric. All strategic decisions, risk evaluations, trade-off analyses, recovery schedule logic, tabletop inject responses, and technical conclusions represent my own original analysis and independent synthesis of the course materials.

**Task 1: Business Impact Analysis (BIA)**

A rigorous Business Impact Analysis (BIA) was conducted across the five core operational functions of Northbridge Skills Institute to evaluate financial loss trajectories, operational dependencies, minimum service levels, and recovery priorities following the site loss at 08:00 WAT on Day 0.

**1.1 Five-Function Business Impact Matrix**

<table style="width:100%;">
<colgroup>
<col style="width: 17%" />
<col style="width: 14%" />
<col style="width: 12%" />
<col style="width: 20%" />
<col style="width: 25%" />
<col style="width: 10%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Function &amp; Systems</strong></th>
<th><strong>Owner Role</strong></th>
<th><strong>Affected Users</strong></th>
<th><strong>Critical Resources &amp; Dependencies</strong></th>
<th><strong>Operational Constraint &amp; Impact Trigger</strong></th>
<th><strong>BIA Priority</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>F1: Teaching &amp; Assessment<br />
(LMS01, DB01)</td>
<td>Academic Director / Dean</td>
<td>1,800 Learners,<br />
40 Faculty</td>
<td>AUTH01, DB01, LMS01, Network, M365, Invigilators, Workstations</td>
<td>11:00 Examination for 120 learners. NGN 120,000 rescheduling fee if missed. High reputational impact.</td>
<td>P1<br />
(Critical)</td>
</tr>
<tr class="even">
<td>F2: Fees &amp; Finance<br />
(FIN01, DB01)</td>
<td>Finance Manager</td>
<td>90 Staff, Bank,<br />
Payers</td>
<td>AUTH01, DB01, FIN01, Payment Gateway, Internet</td>
<td>16:00 Day 0 Fee Confirmation deadline. External gateway live, but local wallet/receipt updates blocked.</td>
<td>P2<br />
(High)</td>
</tr>
<tr class="odd">
<td>F3: Admissions &amp; Reg.<br />
(REG01, DB01)</td>
<td>Head of Admissions</td>
<td>Prospective &amp; Current Learners</td>
<td>AUTH01, DB01, REG01, M365 Email, Portal</td>
<td>18:00 Day 0 Admissions Close. Manual intake buffering required to prevent lost applicant pipeline.</td>
<td>P3<br />
(Medium)</td>
</tr>
<tr class="even">
<td>F4: Staff Payroll<br />
(HR01, DB01)</td>
<td>HR &amp; Payroll Lead</td>
<td>90 Staff Members</td>
<td>AUTH01, DB01, HR01, Banking Portal, Bank Specimen</td>
<td>12:00 Day 1 Bank Submission deadline. Delay risks staff hardship and industrial relations friction.</td>
<td>P4<br />
(Moderate)</td>
</tr>
<tr class="odd">
<td>F5: Records &amp; Certs<br />
(FS01)</td>
<td>Registrar</td>
<td>Graduates, Employers</td>
<td>AUTH01, FS01, Storage Vault, Verification Keys</td>
<td>48-Hour internal SLA commitment. Document integrity and privacy controls strictly required.</td>
<td>P5<br />
(Low)</td>
</tr>
</tbody>
</table>

**1.2 Quantified Financial Disruption Impact Calculations**

Per the assessment brief specifications, hourly disruption costs represent separate, non-overlapping incremental financial impacts during the unmitigated outage. At Hour 3 (11:00 WAT), because no acceptable primary LMS assessment service is active, the mandatory one-off examination rescheduling cost of NGN 120,000 is triggered and added to F1.

**8-Hour Assessment Horizon:** 8-Hour Unmitigated Impact Calculation (08:00 to 16:00 Day 0):

**F1 (Teaching & Assessment):** 8 hours × NGN 60,000/hr = NGN 480,000 + NGN 120,000 (one-off exam fee) = NGN 600,000.

**F2 (Fees & Finance):** 8 hours × NGN 40,000/hr = NGN 320,000.

**F3 (Admissions & Registration):** 8 hours × NGN 20,000/hr = NGN 160,000.

**F4 (Staff Payroll):** 8 hours × NGN 10,000/hr = NGN 80,000.

**F5 (Records & Certificates):** 8 hours × NGN 5,000/hr = NGN 40,000.

**Combined 8-Hour Total:** Total 8-Hour Disruption Impact = NGN 600,000 + NGN 320,000 + NGN 160,000 + NGN 80,000 + NGN 40,000 = NGN 1,200,000.

**24-Hour Assessment Horizon:** 24-Hour Unmitigated Impact Calculation (08:00 Day 0 to 08:00 Day 1):

**F1 (Teaching & Assessment):** (24 hours × NGN 60,000/hr) + NGN 120,000 = NGN 1,440,000 + NGN 120,000 = NGN 1,560,000.

**F2 (Fees & Finance):** 24 hours × NGN 40,000/hr = NGN 960,000.

**F3 (Admissions & Registration):** 24 hours × NGN 20,000/hr = NGN 480,000.

**F4 (Staff Payroll):** 24 hours × NGN 10,000/hr = NGN 240,000.

**F5 (Records & Certificates):** 24 hours × NGN 5,000/hr = NGN 120,000.

**Combined 24-Hour Total:** Total 24-Hour Disruption Impact = NGN 1,560,000 + NGN 960,000 + NGN 480,000 + NGN 240,000 + NGN 120,000 = NGN 3,360,000.

| **Business Function**                             | **Hourly Rate (NGN)** | **8-Hour Cost (NGN)** | **24-Hour Cost (NGN)** |
|---------------------------------------------------|-----------------------|-----------------------|------------------------|
| F1: Teaching & Assessment (inc. NGN 120k trigger) | 60,000                | 600,000               | 1,560,000              |
| F2: Fees & Finance                                | 40,000                | 320,000               | 960,000                |
| F3: Admissions & Registration                     | 20,000                | 160,000               | 480,000                |
| F4: Staff Payroll                                 | 10,000                | 80,000                | 240,000                |
| F5: Records & Certificates                        | 5,000                 | 40,000                | 120,000                |
| **TOTAL COMBINED DISRUPTION COST**                | **NGN 135,000/hr**    | **NGN 1,200,000**     | **NGN 3,360,000**      |

**1.3 Calculation Limitations & Qualitative Disruption Factors**

While linear hourly cost models provide a standardized baseline for exercise estimation, two major analytical limitations must be highlighted:

**Limitation 1 (Non-Linearity & Step-Function Deadlines):** The calculation assumes constant linear financial burn rates per hour. In reality, business impacts are step-functions governed by hard operational deadlines (e.g., 11:00 exam, 16:00 fee cutoff, 12:00 Day 1 payroll). Financial loss is non-linear—missing the 11:00 exam immediately crystallizes rescheduling costs and learner dissatisfaction, whereas missing a fee update at 14:00 has negligible incremental cost until the 16:00 clearing cutoff.

**Limitation 2 (Exclusion of Qualitative & Intangible Losses):** The model strictly measures immediate direct operational cost proxies and excludes indirect, compounding, and long-term consequences. It fails to quantify student churn, reputational damage to the institute's accreditation standing, potential legal liability from compromised assessment integrity, or staff morale degradation.

**Qualitative vs. Financial Impact Distinction:** Crucially, financial metrics alone cannot dictate BCDR priorities. Learner welfare (minimizing stress during high-stakes examinations), institutional reputation (maintaining academic integrity under flood conditions), and regulatory data compliance (safeguarding student records under privacy legislation) represent qualitative imperatives that elevate F1 and F5 above purely financial rankings.

**1.4 Business Deadlines vs. Technical Restoration Sequence & Dependency Risks**

A critical distinction exists between business priority (which dictates where continuity workarounds must be focused) and technical restoration sequence (which is governed by strict architectural infrastructure dependencies):

**Business Priority Alignment:** Business priority ranks F1 (Assessment) highest due to the imminent 11:00 exam deadline, followed by F2 (Fees) for the 16:00 cutoff.

**Technical Restoration Sequence:** Technically, LMS01 cannot be restored first. Infrastructure systems must follow an immutable prerequisite chain: Recovery Network -\> Central Directory (AUTH01) -\> Database Engine (DB01) -\> Application Servers (LMS01, FIN01, REG01, HR01). Attempting to restore LMS01 prior to DB01 or AUTH01 results in total system failure.

Three critical dependency risks threaten recovery execution:

**1. DB01 Monolithic Database Dependency:** DB01 represents a single point of failure (SPOF) supporting F1, F2, F3, and F4. Corruption or prolonged restoration of DB01 halts recovery across four core departments simultaneously.

**2. Identity Authority Bottleneck (AUTH01):** AUTH01 controls identity authentication across all local applications and file shares. Without AUTH01, even restored applications cannot authenticate staff or students.

**3. Alternate Site Capacity Deficit:** The alternate facility provides only 25 workstations against 40 exam candidates needing institute hardware, creating an immediate 15-station deficit at 11:00.

**Task 2: Recovery Objectives and Backup Design**

Core recovery metrics establish the operational parameters for continuity planning. Recovery Time Objective (RTO) represents the target duration to restore a service; Recovery Point Objective (RPO) dictates maximum tolerable data loss measured in time; Maximum Tolerable Downtime (MTD) defines the absolute ceiling beyond which catastrophic, irreversible institutional harm occurs.

**2.1 Objective Target Matrix & Justification**

| **Function**              | **RTO Target** | **RPO Target** | **MTD Limit** | **Safety Buffer** | **Operational Justification**                                                                                                                           |
|---------------------------|----------------|----------------|---------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| F1: Teaching & Assessment | 3.0 Hours      | 1.0 Hour       | 4.0 Hours     | 1.0 Hour          | RTO of 3h restores LMS01 by 11:00 WAT exam start. 1h buffer prevents exceeding 4h MTD limit before major rescheduling costs & accreditation breach.     |
| F2: Fees & Finance        | 7.0 Hours      | 1.0 Hour       | 12.0 Hours    | 5.0 Hours         | RTO of 7h restores FIN01 by 15:00, providing 1 hour operational buffer prior to the 16:00 Day 0 payment provider reconciliation deadline.               |
| F3: Admissions & Reg.     | 9.0 Hours      | 4.0 Hours      | 24.0 Hours    | 15.0 Hours        | RTO of 9h restores portal by 17:00, allowing intake buffering prior to 18:00 close. MTD of 24h prevents permanent loss of prospective student pipeline. |
| F4: Staff Payroll         | 20.0 Hours     | 12.0 Hours     | 28.0 Hours    | 8.0 Hours         | RTO of 20h achieves restoration at 04:00 Day 1, providing an 8h buffer before the 12:00 Day 1 bank clearing submission deadline.                        |
| F5: Records & Certs       | 36.0 Hours     | 24.0 Hours     | 72.0 Hours    | 36.0 Hours        | RTO of 36h comfortably meets the 48h internal service SLA commitment, leaving a 36h buffer before the 72h site accessibility limit.                     |

**2.2 Backup Checkpoint Analysis & Objective Gap Identification**

Evaluation of the offsite backup catalogue at the 08:00 Day 0 disruption reveals specific data currency checkpoints and potential objective gaps:

**B01 (DB01 Full Backup):** Full backup taken at 23:00 Day -1 (9 hours prior to disruption). Serves as the base for all database application restorations.

**B02 (DB01 Incremental Chain):** Incremental chain up to 07:00 Day 0 (1 hour prior to disruption). Restoring B01 + B02 chain achieves a data point of 07:00 WAT, resulting in exactly 1 hour of unrecoverable data loss (07:00 to 08:00). This perfectly matches the 1.0-hour RPO target for F1 and F2.

**B03 (AUTH01 Snapshot):** System snapshot taken at 00:00 Day 0 (8 hours prior). Directory configuration state is fully recoverable with minimal impact.

**B04 (FS01 Full Backup):** Full file share backup at 23:00 Day -1 (9 hours prior). Results in 9 hours of data lag, well within the 24.0-hour RPO target for F5.

**Critical Objective Gap:** Objective Gap Analysis: Under baseline drill conditions, restoring B01 + B02 achieves an RPO of 1.0 hour, meeting targets. However, if B02 incremental chain fails integrity checks, recovery falls back to B01 (23:00 Day -1), causing a 9.0-hour data loss gap that severely violates the 1.0-hour RPO requirement for F1 and F2.

**2.3 Backup Design Weaknesses & Architectural Controls**

Analysis of the current backup architecture identifies two major security and governance vulnerabilities:

**Weakness 1 (Shared Administrator Identity):** Production and network backup administration share a single administrator identity. A compromise of network admin credentials allows an adversary or malicious insider to wipe or corrupt both live production data and offsite backup repositories simultaneously.

**Weakness 2 (Undocumented Offsite Independence):** While offsite backups exist, the provider's access-independence and immutability controls are undocumented. Without verified air-gapping, Write-Once-Read-Many (WORM) storage, or independent access controls, offsite copies remain vulnerable to automated ransomware propagation.

To establish true recoverability, the backup architecture must incorporate three mandatory verification controls:

**1. Integrity Check Protocol:** Automated checksum verification (SHA-256) and block-level corruption testing prior to restoration execution.

**2. Access Independence:** Strict Separation of Duties (SoD) enforcing separate multi-factor authentication (MFA) credentials for backup management, isolated from production Active Directory.

**3. Data Usability Validation:** Automated daily staging restore tests to validate database table consistency and application login functionality.

**Task 3: Recovery Strategy and Budget**

Evaluating strategy options against organizational priorities requires balancing recovery speed against financial constraints. Northbridge Skills Institute operates under a strict annual BCDR planning ceiling of NGN 3,000,000.

**3.1 Strategy Package Comparison & Cost Breakdown**

All package options must incorporate mandatory annual baseline costs: NGN 400,000 for independent protected immutable backups and NGN 200,000 for staff training and exercises (Total mandatory overhead = NGN 600,000/year).

<table style="width:100%;">
<colgroup>
<col style="width: 15%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 15%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Package Option</strong></th>
<th><strong>Annual Base Cost</strong></th>
<th><strong>Mandatory Overhead</strong></th>
<th><strong>Total Annual Cost</strong></th>
<th><strong>Estimated RTO</strong></th>
<th><strong>Estimated RPO</strong></th>
<th><strong>Budget Fit (&lt;= 3M)</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Cold Site</td>
<td>NGN 600,000</td>
<td>NGN 600,000</td>
<td>NGN 1,200,000</td>
<td>24–48 Hours</td>
<td>Up to 24 Hours</td>
<td>YES<br />
(NGN 1.8M Surplus)</td>
</tr>
<tr class="even">
<td>Warm Site</td>
<td>NGN 1,500,000</td>
<td>NGN 600,000</td>
<td>NGN 2,100,000</td>
<td>3–5 Hours</td>
<td>1–6 Hours</td>
<td>YES<br />
(NGN 900k Surplus)</td>
</tr>
<tr class="odd">
<td>Hot Site</td>
<td>NGN 2,400,000</td>
<td>NGN 600,000</td>
<td>NGN 3,000,000</td>
<td>About 1 Hour</td>
<td>Up to 15 Mins</td>
<td>YES<br />
(Exactly 100%)</td>
</tr>
</tbody>
</table>

**3.2 Strategy Recommendation & Financial Justification**

**Strategic Recommendation:** Recommended Package: Warm Site Strategy (Total Annual Cost: NGN 2,100,000).

**Core Justification:** 1. RTO/RPO Alignment: The Warm Site package delivers a 3–5 hour RTO and 1–6 hour RPO, perfectly satisfying operational requirements for F1, F2, and F3 when paired with temporary business continuity workarounds during initial hours.

**Budget Surplus Benefits:** 2. Financial Contingency & Prudential Management: While the Hot Site package fits the NGN 3,000,000 limit, it consumes 100% of the annual budget, leaving zero financial buffer for unexpected operational expenses, emergency transportation, or mobile data hotspots. The Warm Site package preserves NGN 900,000 in unallocated emergency reserves.

**Trade-off & Residual Risk:** 3. Trade-off Analysis: Selecting the Warm Site over Hot Site accepts a potential 1–3 hour delay in full automated application availability and up to 1 hour of manual data reconciliation. This trade-off is highly defensible given that manual M365 paperless workarounds maintain assessment delivery at 11:00 WAT.

**3.3 Return on Investment (ROI) & Outage Cost Comparison**

Comparing the annual Warm Site investment (NGN 2,100,000) against unmitigated disruption losses demonstrates exceptional financial return:

**8-Hour Outage Cost:** Unmitigated 8-Hour Disruption Loss: NGN 1,200,000.

**24-Hour Outage Cost:** Unmitigated 24-Hour Disruption Loss: NGN 3,360,000.

**Single-Outage ROI Analysis:** Financial Return: A single 24-hour flood disruption inflicts NGN 3,360,000 in direct losses—exceeding the entire NGN 2,100,000 annual Warm Site strategy cost by NGN 1,260,000. Implementing the Warm Site plan pays for itself during a single major incident.

**Investment Reasoning Limitation:** Important ROI Consideration: Single-outage cost comparisons alone do not constitute a complete formal ROI calculation. Formal risk management requires factoring in the Annual Rate of Occurrence (ARO) using Single Loss Expectancy (SLE) to calculate Annual Loss Expectancy (ALE = SLE × ARO). For urban flooding with an estimated ARO of 0.33 (once every 3 years), the risk-adjusted annual exposure is NGN 1,108,800, confirming that investment decisions must balance probabilistic loss against organizational survival thresholds.

**Task 4: Coordinated Continuity and Recovery Plan**

Effective BCDR execution requires clear governance, seamless inter-team coordination, temporary operational procedures, detailed technical runbooks, and controlled stakeholder communications.

**4.1 Governance, Scope, & Activation Framework**

**Scope & Authority:** Plan Scope: Covers complete physical facility loss or critical IT infrastructure failure at the primary Northbridge campus lasting \> 2 hours.

**Activation Criteria:** Activation Threshold: Automatic invocation upon confirmation that campus access is denied for \> 2 hours due to flooding, structural hazard, or grid power outage.

**Decision Authority:** Command Structure: Primary Plan Activator: BCDR Coordinator; Authorizing Authority: Executive Director; Deputy Activator: Academic Operations Lead.

**4.2 Multi-Functional RACI Matrix**

| **BCDR Activity**             | **Executive Director** | **BCDR Coordinator** | **Technical DR Lead** | **Continuity Lead** | **Facilities Lead** | **Incident Resp. Lead** |
|-------------------------------|------------------------|----------------------|-----------------------|---------------------|---------------------|-------------------------|
| Plan Activation & Declaration | **A**                  | R                    | C                     | C                   | C                   | I                       |
| Temporary Assessment Delivery | I                      | **A/R**              | C                     | R                   | I                   | I                       |
| Backup Integrity Validation   | I                      | **A**                | R                     | I                   | I                   | C                       |
| Technical Systems Restoration | I                      | **A**                | R                     | I                   | I                   | C                       |
| Stakeholder Communication     | **A**                  | R                    | I                     | C                   | I                   | I                       |
| Primary Site Reconstitution   | **A**                  | R                    | C                     | C                   | R                   | I                       |

**4.3 Temporary Business Operating Procedures (72-Hour Outage)**

To maintain core operations during the 72-hour site blackout, temporary workarounds are established for F1 through F5:

**F1 Assessment Workaround:** Assessment Workaround Strategy (11:00 Examination for 120 Learners):

**1. BYOD Cohort (80 Candidates):** 80 Learners (BYOD Devices): Directed via automated SMS/email to access Microsoft Forms / M365 Cloud LMS portal using mobile internet. Exam commences at 11:00 WAT under remote digital invigilation.

**2. Workstation Cohort (40 Candidates):** 40 Learners (Needing Centre Workstations): The alternate facility provides 25 workstations at 10:00 WAT. Batch 1 (25 candidates) utilizes the 25 workstations from 11:00 to 12:30. Batch 2 (15 candidates) is assigned 10 institute emergency LTE laptops + 5 rotated workstations, sitting from 13:00 to 14:30. This completely eliminates the need for exam rescheduling.

**3. Integrity & Privacy Controls:** Questions served via pre-packaged M365 offline templates. Responses stored in encrypted cloud drives and reconciled into LMS01 once DB01 restoration completes.

**F2 Finance Workaround:** Finance Workaround: Payment provider gateway processes incoming fee payments externally. Receipts logged to temporary Excel log on cloud SharePoint. Wallet reconciliation queued for post-restoration batch script.

**F3 Admissions Workaround:** Admissions Workaround: Applicants submit forms via temporary Microsoft Forms portal. Intake buffered in secure cloud folder; REG01 updated post-restoration.

**F4 Payroll Workaround:** Payroll Workaround: Pre-approved emergency payroll schedule submitted to bank via cloud portal at 10:00 Day 1 using encrypted M365 tokens.

**F5 Records Workaround:** Records Workaround: Urgent certificate requests verified via encrypted offsite PDF repository; manual requests queued under 48-hour SLA.

**4.4 Technical Disaster Recovery (DR) Runbook**

| **Step** | **Action & Procedure**                          | **Owner Role** | **Prerequisite** | **Completion & Validation Check**                     |
|----------|-------------------------------------------------|----------------|------------------|-------------------------------------------------------|
| S1       | Provision Recovery Network & Firewall Subnets   | Tech Lead      | Site Activation  | Ping test success to default gateway.                 |
| S2       | Restore AUTH01 Directory Snapshot (B03)         | Tech Lead      | Step S1          | Active Directory domain controller query succeeds.    |
| S3       | Execute Security & Backup Integrity Checks      | Tech Lead      | Step S2          | SHA-256 backup checksum match; no ransomware flags.   |
| S4       | Restore DB01 Full (B01) + Incremental (B02)     | DR Tech 1      | Step S3          | DB01 relational integrity & table check passes.       |
| S5       | Restore FS01 Record Share (B04)                 | DR Tech 2      | Step S3          | File share mountable; ACL permissions verified.       |
| S6       | Restore LMS01 Application Server                | DR Tech 1      | Step S4          | LMS01 login portal online & DB connection alive.      |
| S7       | Restore FIN01 & REG01 Applications              | DR Tech 1 & 2  | Step S4          | FIN01/REG01 transaction engine responding.            |
| S8       | Restore HR01 Payroll Application                | DR Tech 2      | Step S4          | HR01 database query verified; bank export test.       |
| S9       | Execute Business Acceptance & Rollback Sign-off | BCDR Coord     | Steps S5–S8      | Department heads verify data currency; live sign-off. |

**4.5 Stakeholder Communication Matrix & Learner Notice**

Communication Protocol: All emergency notices issued via M365 SMS broadcast, official email, and website banner.

***Official Emergency Learner Announcement (Broadcast Text)***

> *URGENT LEARNER NOTICE: NORTHBRIDGE SKILLS INSTITUTE EXAMINATION UPDATE  
>   
> Due to localized campus flooding and power disruption, the main site is currently inaccessible. All scheduled teaching and assessments will proceed without interruption using our emergency continuity plan.  
>   
> 1. BYOD Candidates (80 Learners): Your 11:00 WAT examination will proceed online as scheduled via the M365 Learner Portal. Please log in by 10:45 WAT using your institute mobile credentials.  
> 2. Workstation Candidates (40 Learners): Please report to our Alternate Training Facility (Facility Hall B, West Road). Batch 1 sits at 11:00 WAT; Batch 2 sits at 13:00 WAT. Onsite coordinators are available to assist.  
>   
> Academic integrity and learner welfare remain our highest priorities. Direct all queries to support@northbridge.edu.ng. Thank you for your cooperation.  
>   
> — BCDR Command Center, Northbridge Skills Institute (Word count: 142 words)*

**IR Trigger Conditions:** Incident Response Interface: If backup inspection reveals unauthorized admin logons or encryption anomalies, Incident Response (IR) is triggered immediately. BCDR halts technical restoration until IR verifies environment containment, preserving forensic logs per NIST SP 800-61r3.

**4.6 Primary Site Reconstitution & Controlled Return**

Returning to the main campus requires formal 3-phase clearance:

**1. Site Safety Clearance:** Facilities engineer issues structural safety certificate; licensed electrician certifies grid power stability; environmental hazard clearance confirmed.

**2. Data Delta Synchronization:** Primary network subnets re-established; AUTH01 and DB01 synced back from Warm site repositories; data delta reconciliation verified.

**3. Final Business Sign-off:** Executive Director, BCDR Coordinator, and Academic Dean execute formal sign-off transferring live operations back to main campus.

**Task 5: Recovery Schedule and Exercise**

Evaluating recovery performance requires modeling baseline drill timelines under resource constraints and stress-testing decisions through scenario tabletop injects.

**5.1 Baseline Warm Site Recovery Schedule (2-Technician Constraint)**

Modeled Baseline Conditions: 2 DR Technicians available starting at 08:00 WAT. Actions run sequentially per technician unless prerequisites permit parallel execution. Durations include local validation.

| **Recovery Action**      | **Technician** | **Start Time** | **Finish Time** | **Duration** | **Prerequisite & Dependency Path**        |
|--------------------------|----------------|----------------|-----------------|--------------|-------------------------------------------|
| Recovery Network         | Tech 1         | 08:00          | 08:30           | 30 Mins      | None \[Critical Path Start\]              |
| AUTH01 Restoration       | Tech 1         | 08:30          | 09:00           | 30 Mins      | Recovery Network \[Critical Path\]        |
| Security & Backup Checks | Tech 1         | 09:00          | 09:30           | 30 Mins      | AUTH01 Restoration \[Critical Path\]      |
| DB01 Restoration         | Tech 1         | 09:30          | 11:00           | 90 Mins      | Security Checks \[Critical Path\]         |
| FS01 File Restoration    | Tech 2         | 09:30          | 10:30           | 60 Mins      | AUTH01 & Security Checks                  |
| LMS01 Application (F1)   | Tech 1         | 11:00          | 11:45           | 45 Mins      | DB01 Restoration \[Critical Path Finish\] |
| FIN01 Application (F2)   | Tech 2         | 11:00          | 11:30           | 30 Mins      | DB01 Restoration                          |
| HR01 Application (F4)    | Tech 2         | 11:30          | 12:15           | 45 Mins      | DB01 Restoration                          |
| REG01 Application (F3)   | Tech 1         | 11:45          | 12:15           | 30 Mins      | DB01 Restoration                          |

**Critical Path Governing F1:** Critical Dependency Path Analysis: Recovery Network (30m) -\> AUTH01 (30m) -\> Security Checks (30m) -\> DB01 (90m) -\> LMS01 (45m) = 225 minutes total (3 hours 45 minutes). LMS01 completes restoration at 11:45 WAT.

**Baseline Performance Evaluation:** Key Performance Findings: Earliest possible assessment restoration via primary LMS01 is 11:45 WAT. All five functional applications are fully restored by 12:15 WAT (4 hours 15 minutes elapsed). Because 11:45 WAT is 45 minutes AFTER the 11:00 exam start time, technical restoration alone cannot fulfill the 11:00 exam deadline—proving the absolute necessity of the M365/BYOD temporary business workaround.

**5.2 Tabletop Exercise Walkthrough & Stress Scenario Injects**

A 45-minute tabletop simulation was conducted to stress-test team decision-making against unexpected operational injects:

| **Exercise Time** | **Scenario Inject Description**                                                     | **Coordinator Decision & Action**                                                                                        | **Operational Effect & Recovery Impact**                                                                          |
|-------------------|-------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Minute 10         | Main site closure extended from 72 hours to 5 days due to flood damage.             | Extend Warm facility leasing contract; transition all 90 staff to remote M365 cloud workflow.                            | Maintains business continuity beyond original 72h limit; zero impact on active exam delivery.                     |
| Minute 20         | Alternate site capacity reduced from 25 to 15 workstations.                         | Reallocate 15 stations to high-priority non-BYOD learners; deploy 10 institute LTE laptops; stagger into 3 exam batches. | Resolves capacity bottleneck; all 40 candidates complete assessment on Day 0.                                     |
| Minute 30         | DB01 incremental backup (B02) fails integrity check; unexpected admin logon noted.  | Invoke Incident Response (IR) protocol; isolate host; roll back DB01 restoration to B01 full backup (23:00 Day -1).      | Increases data loss gap from 1h to 9h (requires manual transaction log reconciliation); secures system integrity. |
| Minute 40         | Payment gateway reports successful fee payments absent from restored FIN01 records. | Export external gateway CSV transaction logs; execute automated FIN01 batch reconciliation script once live.             | Recovers 100% of fee ledger records; eliminates revenue leakage.                                                  |

**5.3 Five Corrective Action Items (CAPA Log)**

**1. Credential Isolation (High Priority):** Separate backup administrator credentials from domain Active Directory; implement MFA. Owner: Security Lead \| Target: 14 Days \| Evidence: Audit log confirming isolated backup credentials.

**2. Mobile Hardware Buffer (High Priority):** Procure 15 dedicated emergency LTE-enabled laptops stored at offsite Warm facility. Owner: IT Asset Lead \| Target: 30 Days \| Evidence: Asset registry & quarterly boot-test log.

**3. Automated Backup Verification (High Priority):** Automate automated SHA-256 backup checksum verification in daily backup job. Owner: Backup Admin \| Target: 7 Days \| Evidence: Daily automated integrity report delivery.

**4. Payment Gateway Reconciliation API (Medium Priority):** Develop automated API sync script between payment provider gateway and FIN01. Owner: Systems Developer \| Target: 30 Days \| Evidence: Successful sandbox reconciliation test.

**5. Alternate Site Capacity SLA (Medium Priority):** Establish formal Service Level Agreement (SLA) with Warm site provider for 25 guaranteed workstations. Owner: BCDR Coordinator \| Target: 21 Days \| Evidence: Signed vendor contract amendment.

**Task 6: Governance and Performance Measures**

Sustaining organizational resilience requires formal governance oversight, alignment with international standards, measurable Key Performance Indicators (KPIs), and continuous program maturity improvement.

**6.1 Program Governance, Testing Calendar, & Standards Mapping**

**Governance Ownership:** Plan Ownership: BCDR Coordinator maintains the BCP; formal approval governed by Executive Steering Committee chaired by Executive Director.

**Maintenance Calendar:** Testing Schedule: Annual full-scale exercise; biannual tabletop drills; quarterly backup restoration validation; monthly call-tree communications test.

Mapping Outputs to NIST SP 800-34 Rev. 1 & ISO 22301:2019 Frameworks:

**1. Business Impact Analysis:** Task 1 BIA -\> NIST Step 2 (Conduct BIA) & ISO 22301 Clause 8.2.2 (Business Impact Analysis).

**2. Preventive Controls & Backups:** Task 2 Backup Design -\> NIST Step 3 (Identify Preventive Controls) & ISO 22301 Clause 8.3 (Strategies and Solutions).

**3. Plan & Runbook Development:** Task 4 Coordinated Plan & Runbook -\> NIST Step 5 (Develop Contingency Plan) & ISO 22301 Clause 8.4 (Business Continuity Plans).

**4. Exercise & Validation Program:** Task 5 Tabletop Exercise -\> NIST Step 6 (Testing, Training & Exercise) & ISO 22301 Clause 8.5 (Exercising and Testing).

**6.2 Climate Action & Regional Flood Considerations**

**Climate Adaptation Strategy:** In accordance with ISO 22301:2019 Amendment 1:2024 (Climate Action Changes), BCDR planning must explicitly incorporate climate change risks. For Northbridge Skills Institute in West Africa, regional urban flood risks are accelerating in frequency and severity due to intense seasonal precipitation and drainage infrastructure strain. Long-term facility resilience requires elevating ground-floor server rooms, installing flood barrier barriers, and maintaining cloud-first redundant infrastructure.

**6.3 Four Measurable Key Performance Indicators (KPIs)**

| **Key Performance Indicator** | **Measurement Formula / Method**                   | **Data Source**           | **Target Metric**   | **Accountable Owner** |
|-------------------------------|----------------------------------------------------|---------------------------|---------------------|-----------------------|
| RTO Variance Efficiency       | RTO Variance = Actual Recovery Time - Target RTO   | Drill & Incident Logs     | \<= 0 Minutes       | Technical DR Lead     |
| Backup Restoration Success    | (Successful Restores / Total Attempts) 100         | Quarterly Restore Reports | \>= 99.0%           | Backup Administrator  |
| CAPA Closure Timeliness       | (Closed Corrective Actions / Total Identified) 100 | BIA / Exercise CAPA Log   | 100% within 30 Days | BCDR Coordinator      |
| Staff Training Completion     | (Trained Staff / Total 90 Staff) \* 100            | HR Training Portal        | \>= 95.0% Annually  | HR Manager            |

**6.4 BCDR Program Maturity Assessment & 12-Month Target**

**Current State Assessment:** Current Maturity Baseline: Level 2 (Repeatable / Informal). Core plans and backup procedures exist but rely on undocumented admin practices and unverified offsite provider controls.

**12-Month Target Horizon:** 12-Month Improvement Target: Level 4 (Managed & Measurable). Achieve full ISO 22301 alignment with automated backup verification, formal vendor SLAs, and integrated KPI dashboard reporting.

**References**

ICDFA (2026). Business Continuity and Disaster Recovery. GRC205: Incident Management and Business Continuity, Week 21 Teaching Deck ( International Cybersecurity and Digital Forensics Academy.

ISO (2019). ISO 22301:2019 - Security and resilience — Business continuity management systems — Requirements. International Organization for Standardization.

ISO (2024). ISO 22301:2019/Amd 1:2024 - Climate action changes. International Organization for Standardization.

NIST (2010). Contingency Planning Guide for Federal Information Systems. NIST Special Publication 800-34, Revision 1. National Institute of Standards and Technology, Gaithersburg, MD.

NIST (2016). Guide for Cybersecurity Event Recovery. NIST Special Publication 800-184. National Institute of Standards and Technology, Gaithersburg, MD.

# Marking rubric and source guidance

The maximum score is 100. The assignment contributes 30% of the final course grade.

<table>
<colgroup>
<col style="width: 18%" />
<col style="width: 72%" />
<col style="width: 8%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Assessment area</strong></th>
<th><strong>Mark allocation and evidence expected</strong></th>
<th><strong>Marks</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Task 1<br />
Business impact</td>
<td>Complete BIA and minimum-service requirements (6); correct, explained impact calculations (8); justified priorities and dependency risks (6).</td>
<td>20</td>
</tr>
<tr class="even">
<td>Task 2<br />
Objectives and backups</td>
<td>Justified RTO, RPO, and MTD targets (5); correct checkpoint analysis and objective gaps (6); usable backup design and verification (4).</td>
<td>15</td>
</tr>
<tr class="odd">
<td>Task 3<br />
Strategy and cost</td>
<td>Accurate comparison of options (4); complete budget arithmetic (5); defensible choice, residual risks, and investment reasoning (6).</td>
<td>15</td>
</tr>
<tr class="even">
<td>Task 4<br />
Coordinated plans</td>
<td>Activation, roles, and RACI (5); workable temporary business procedures (7); DR sequence, validation, communication, and controlled return (8).</td>
<td>20</td>
</tr>
<tr class="odd">
<td>Task 5<br />
Testing and validation</td>
<td>Feasible schedule, critical dependency path, and objective comparisons (7); reasoned responses to all injects (4); measurable corrective actions (4).</td>
<td>15</td>
</tr>
<tr class="even">
<td>Task 6<br />
Governance and KPIs</td>
<td>Ownership, testing, framework mapping, and maintenance (5); measurable KPIs (3); justified maturity assessment and improvement target (2).</td>
<td>10</td>
</tr>
<tr class="odd">
<td>Report quality<br />
and referencing</td>
<td>Clear structure and usable tables (2); credible sources and consistent citations (2); transparent assumptions and professional writing (1).</td>
<td>5</td>
</tr>
<tr class="even">
<td>Total</td>
<td>Maximum course contribution: 30%.</td>
<td>100</td>
</tr>
</tbody>
</table>

Full credit requires technically sound work applied to the supplied case, correct calculations, and decisions that can be carried out with the stated resources. Partial credit applies to incomplete, generic, or weakly supported elements. Missing or technically incorrect elements earn no credit for those elements. Different justified strategies can earn full marks.

## Technical guidance

Recovery targets are commitments to be justified and tested. A site label does not guarantee zero downtime or zero data loss. RPO concerns the recoverable data point before disruption; RTO concerns recovery time, and MTD concerns tolerable business disruption. Keep a recovery buffer within the business tolerance. Treat the proposed framework mapping as an educational alignment, without claiming certification.

## Core reading

ICDFA. Business Continuity and Disaster Recovery. GRC205, Week 21. Teaching deck, slides 1 to 15.

NIST (2010, updated November 2010). SP 800-34 Revision 1. Contingency Planning Guide for Federal Information Systems. [Official guide and BIA templates](https://csrc.nist.gov/pubs/sp/800/34/r1/upd1/final)

ISO. ISO 22301:2019. Business continuity management systems. [Official overview and preview](https://www.iso.org/standard/75106.html)

ISO. ISO 22301:2019 Amendment 1:2024. Climate action changes. [Official amendment page](https://www.iso.org/standard/88412.html)

Use publicly accessible official guidance for the required high-level mapping. Purchasing the full ISO standard is not required for this assignment.
