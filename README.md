# AI Governance Proposal: Clinical Risk-Prediction Algorithm

A practical, end-to-end governance proposal for an AI system that is already in real-world use: a commercial clinical risk-prediction algorithm that large US health systems rely on to decide which patients receive intensive care management. It was built as a group project by a five-person team.

This repository gives an overview of the project. The full report and presentation deck are not published here — see [Deliverables](#deliverables).

## The case

The proposal follows one deployment: a large hospital rolls the algorithm out across its outpatient population. Each patient receives an annual risk score, computed from insurance claims and electronic health records. Patients with the highest scores are enrolled automatically in a programme that adds extra nursing support, priority appointments and coordinated care for chronic conditions; everyone else stays in routine care.

The algorithm estimates medical need from how much a patient is likely to **cost**. Because less is spent on Black patients than on equally sick White patients, the score systematically underestimates how sick they are. In the published study of this algorithm, Black patients at a given risk score had 26.3% more chronic conditions than White patients, and correcting the label would raise the share of Black patients receiving additional care from 17.7% to 46.5% ([Obermeyer et al., 2019](https://doi.org/10.1126/science.aax2342)).

This makes it a useful governance case. The harm does not come from a malfunction. It comes from a choice that looks technical — the prediction target — but is really a decision about who gets care.

## The proposal at a glance

### Stakeholders

| Stakeholder | Role in governance |
|---|---|
| Patients, including groups that are heavily affected | Must be told that a score is used, and must be able to appeal |
| Clinicians and hospital staff | Hold a real veto over the score, and report problems |
| Hospital management and procurement | Carry the legal exposure; set contract terms and commission audits |
| Algorithm vendor | Holds the label, data and model; must document the system and accept audits |
| Regulators | Investigate complaints and set duties for high-risk AI |
| Internal AI governance and ethics committee | Runs the AI register, monitors performance and coordinates appeals |

### Key risks

Seven risk areas were identified and analysed:

| # | Risk area | What it is |
|---|---|---|
| R1 | Fairness and discrimination | Spending is used as a stand-in for health need, and past spending is unequal |
| R2 | Accountability | No named owner, undisclosed labels and scores that cannot be contested |
| R3 | Safety and reliability | Silent false negatives, and vendor updates that change outputs |
| R4 | Privacy | Large-scale claims data, and audits that need sensitive race data |
| R5 | Model drift and feedback loop | Patients who are left out cost less, which widens the gap in the next round |
| R6 | Third-party dependency | The label, data and model are all owned by the vendor |
| R7 | Transparency and explainability | Scores without reasons, and explanations that can be manipulated |

### Governance suggestions

Each of the six measures is mapped to the risks it addresses, and a coverage check confirms that every risk has a primary control:

| # | Measure | What it does | Risks addressed | Lifecycle stage |
|---|---|---|---|---|
| S1 | Label governance | Moves the prediction target from future cost to health need (for example, the number of active chronic conditions), reviewed by a clinical panel | R1 | Problem definition |
| S2 | Named accountability | One named person in the hospital signs off; the system is entered in an AI register; the vendor supplies model documentation | R2, R6 | Whole lifecycle |
| S3 | Mandatory independent bias audit | An independent bias audit before rollout, every year and on every version change, with thresholds that block launch if missed | R1, R3, R5 | Validation and monitoring |
| S4 | Human control and contestability | Patients are told when the algorithm is used and get an appeal channel; clinicians keep a real veto, backed by training | R2, R7 | Rollout |
| S5 | Privacy-protective audit data governance | A data protection impact assessment before rollout; audit data are purpose-limited, access-restricted and de-identified before release | R4 | Data collection |
| S6 | Compliance assessment on two tracks | Assessed against recognised governance practices and against the EU AI Act's obligations for high-risk systems | R2, R6 | Whole lifecycle |

### Fairness, privacy and explainability

- **Fairness:** who may be treated unfairly, which fairness measures and thresholds apply, and how they are tested before launch and after every change.
- **Privacy:** the audit itself needs race data, so sensitive data are governed through a data protection impact assessment, purpose limitation and de-identification.
- **Explainability:** three audiences need different explanations: patients (plain notice of the score, the outcome and how to appeal), clinicians (the main factors and a counterfactual) and inspectors (group-level performance, the label definition, version history and a model card).

### Implementation plan

Actions are organised into three tables — before deployment, while the system is running, and audit and review. Every action names an owner role, a timeline or trigger, and a KPI together with the consequence if it is missed (for example: no signed label record, no model training; a fairness breach suspends automatic enrolment).

## How the team worked

- **Five members, one document.** Each member owned specific chapters and drafted against a shared writing guide (word budgets, citation rules, one agreed set of terms and figures). The lead then integrated and edited the drafts into a single report.
- **Evidence traced to its source.** Statistics and legal claims were checked against the original paper, regulation or standard rather than secondary summaries, and the report and slides used the same figures.
- **Controls tied to risks.** No measure was proposed without saying which risk it reduces, and no identified risk was left without a control.
- **Plans made operational.** Recommendations were turned into actions with owners, timelines and measurable consequences, rather than left as principles.
- **Tooling.** Python scripts (`python-docx`, `python-pptx`) assembled the formatted report from the chapter drafts and generated draft versions of the deck, with checks on layout, speaker notes and figures. The scripts are part of the private archive.

## Deliverables

Two deliverables were produced. They were assessed coursework, so they are **not published in this repository** and are kept in a private archive:

- a written governance proposal: six sections, seven tables and 13 references in APA 7 style;
- a 14-slide presentation, delivered by all five members in a 15-minute talk.

## Selected references

- Amann, J., Blasimme, A., Vayena, E., Frey, D., Madai, V. I., & Precise4Q consortium. (2020). Explainability for artificial intelligence in healthcare: A multidisciplinary perspective. *BMC Medical Informatics and Decision Making, 20*, Article 310. https://doi.org/10.1186/s12911-020-01332-6
- European Parliament & Council of the European Union. (2024). Regulation (EU) 2024/1689 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). *Official Journal of the European Union*, L 2024/1689. https://eur-lex.europa.eu/eli/reg/2024/1689/oj
- Kleinberg, J., Mullainathan, S., & Raghavan, M. (2017). Inherent trade-offs in the fair determination of risk scores. *Proceedings of the 8th Innovations in Theoretical Computer Science Conference (ITCS 2017)*. https://doi.org/10.4230/LIPIcs.ITCS.2017.43
- Mitchell, M., Wu, S., Zaldivar, A., Barnes, P., Vasserman, L., Hutchinson, B., Spitzer, E., Raji, I. D., & Gebru, T. (2019). Model cards for model reporting. *Proceedings of the Conference on Fairness, Accountability, and Transparency (FAT\* '19)*, 220–229. https://doi.org/10.1145/3287560.3287596
- National Institute of Standards and Technology. (2023). *Artificial intelligence risk management framework (AI RMF 1.0)* (NIST AI 100-1). https://doi.org/10.6028/NIST.AI.100-1
- Nissenbaum, H. (2004). Privacy as contextual integrity. *Washington Law Review, 79*(1), 119–157.
- Obermeyer, Z., Powers, B., Vogeli, C., & Mullainathan, S. (2019). Dissecting racial bias in an algorithm used to manage the health of populations. *Science, 366*(6464), 447–453. https://doi.org/10.1126/science.aax2342
- Regulation (EU) 2016/679 of the European Parliament and of the Council (General Data Protection Regulation). (2016). *Official Journal of the European Union*, L 119, 1–88. https://eur-lex.europa.eu/eli/reg/2016/679/oj
- Sweeney, L. (2002). k-anonymity: A model for protecting privacy. *International Journal of Uncertainty, Fuzziness and Knowledge-Based Systems, 10*(5), 557–570. https://doi.org/10.1142/S0218488502001648

## Contributors

- Jie Cheng
- Dekang Lu
- Shiyu Zhong
- Yixuan Liu
- Zhanjian Li

## License

Released under the [MIT License](LICENSE).
