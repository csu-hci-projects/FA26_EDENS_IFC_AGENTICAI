# FA26_EDENS_IFC_AGENTICAI

### Checkpoints and Overleaf Links
| Topic | Link |
| --- | --- |  
| Link To Paper Done in Overleaf| [RE_Overleaf.pdf](https://github.com/BusterShrugz/IFC_AGENTIC_VULNERABILITY_ANALYSIS/blob/main/docs/Overleaf/CHI2026_ReeseE.pdf) |
| Link To Overleaf Project | [Overleaf Project](https://www.overleaf.com/project/6abdee9ebad58b38dfeb47ab)  |
| Link To YouTube, Checkpoint 2 |  [Checkpoint 2]() |
| Link To YouTube, Prototype in action | [Prototype]() |

---

# Human-Centered Agentic Vulnerability Analysis

This research project investigates how an AI agent that actively
investigates IFC related vulnerabilities in source code affects human
vulnerability-response decisions and reliance on automated security
analysis.

The study compares two conditions:

1. CVE-text-only analysis
2. Agentic code investigation with a visible resource trail

Both conditions present the same IFC-oriented finding structure:
security property, information source, sink, flow mechanism, and
vulnerability class.

The primary research question is whether visible agentic investigation evidence
improves decision accuracy and helps users appropriately reject incorrect AI
recommendations. The current prototype evaluates prepared agent assisted documentation trails
rather than live agent execution.

An existing set of 120 manually annotated CVEs is used as
an engineering benchmark for validating the structured vulnerability
representation and supporting pipeline.

---

## CVE Benchmark and Reference Annotations
Using a previously constructed benchmark of 120 CVEs selected from a larger dataset (~45000) that has been collected through the National Vulnerability Database (NVD) API, from January 2025 - current. The candidate CVEs were identified using a broad rule-based filtering pipeline designed to capture potential information-flow-control (IFC) relevance, followed by clustering, audit sampling, and manual review of candidate and potentially missed cases.  

After the first review, we classified edge cases in each cluster, deciding true IFC relevance or not. The CVEs were annotated using a structured codebook covering security violation, flow mechanism, side-channel type, information source, information sink, vulnerability class, implementation language, and application domain.  

Two annotators—a PhD researcher and the primary student researcher—independently annotated the CVEs using the shared codebook and annotation rules.    

Project corrected is the finalized classification ground truth. The researcher view compares Reese's ratings with this reference using eight separate nominal Cohen's kappa scores on the 120 paired main Cases CVEs. This is agreement with a finalized reference, rather than independent inter-annotator reliability; the original Reese–PI comparison is retained separately. The twelve selected prototype cases use the same finalized classifications in both conditions. Scenario-specific response answers remain separate from CVE classification ground truth.

---
## Primary Research Question

**RQ:** How does an AI agent that investigates a vulnerability within a
developer's code affect vulnerability-response decisions and appropriate
reliance compared with an AI system that reasons only from the CVE
description?

**RQ1a** Does access to an agent assisted documentation trail affect the accuracy 
of vulnerability-response decisions? 

**RQ1b**  Does access to the agent assisted documentation trail affect users' 
ability to identify incorrect AI vulnerability assessments?

**RQ1c** How does inspection of the agent's assisted documentationtrail relate to decision confidence, 
completion time, and perceived workload?

## Hypotheses

**H1 — Decision accuracy**  
Participants will make more accurate vulnerability-response decisions 
when using the investigating-agent condition than when using the CVE-text-only condition.

**H2 — Appropriate reliance**  
Participants will reject a greater proportion of incorrect AI 
assessments in the investigating-agent condition than in the CVE-text-only condition.

**H3 — Trail inspection**  
Within the investigating-agent condition, participants who inspect the agent assisted documentation trail will be more likely to identify seeded 
incorrect assessments than participants who do not inspect the trail.

---
## Engineering Validation

The manually annotated CVE benchmark is used to evaluate whether the
supporting analysis system can reproduce the structured IFC-oriented
vulnerability fields used in the human study.

This engineering evaluation is separate from the primary human-centered
experiment.

The system will be evaluated on fields including:

- security violation
- information source
- information sink
- flow mechanism
- side-channel type
- vulnerability class
- implementation language
- application domain

Engineering metrics may include precision, recall, F1-score, and
attribute-level agreement with the manually coded benchmark.

---

## Vulnerability Representation

The project uses a structured representation of vulnerability
characteristics relevant to Information Flow Control.

Current fields include:

- `security_violation`: Confidentiality, Integrity, Both, or Unclear
- `flow_type`: Explicit flow; Implicit flow, timing; Implicit flow, termination; Implicit flow, resource; Implicit flow, response discrepancy or enumeration; Implicit flow, type unclear; Mixed; or Unclear
- information source
- information sink
- vulnerability class
- implementation language
- application domain
- `ifc_relevant`: IFC or NOT IFC
- supporting notes and evidence

The schema uses the exact shared workbook Codebook labels and column names, including
`URL Parameter`. Definitions are retained in `backend/src/models/codebook.json`.  
Code only the direct source, receiving sink, and violation supported by the
description or references. Implementation language requires evidence for the
vulnerable component; CVSS and pipeline metadata do not establish a code.
IFC requires an identifiable source, missing or failed check, and resulting sink.
Secondary sources and sinks belong in notes with the codebook's named labels.

---

Methodology

The current study is an exploratory, between-subjects comparison of two
vulnerability-response interfaces. It examines decision accuracy and appropriate
reliance when participants receive CVE-based findings with or without a visible
agent assisted documentation trail. Each participant selects one condition and completes six
cases in that condition.

The prototype uses real CVEs and finalized IFC classifications, together with
authored deployment scenarios, recommendations, and agent assisted documentation trails.
The trails are prepared study materials; the prototype does not run a live
agent against a participant's codebase. The current evaluation therefore
examines decision support from visible investigation evidence, rather than
live agent performance.

### Participants

Recruitment targets 24 participants: 12 in T1 (CVE-text-only analysis) and 12
in T2 (prepared agent assisted documentation). Each condition has four versions, with
three completed participants per version. Participants are undergraduate,
graduate, or PhD students who are
currently enrolled at CSU or have taken courses there. Intended participants
have completed at least one security-focused programming course and have
introductory familiarity with software and security concepts. The study focuses
on technically literate, non-expert developers. The interface records programming
experience and prior security coursework.

### Study Conditions

Both conditions present an application context, a CVE description, a structured
IFC-oriented finding, and a prepared vulnerability-response recommendation.
The finding uses the same representation in both interfaces, including security
property, information source, sink, flow mechanism, and vulnerability class.

- **T1 — CVE-text-only analysis:** Participants review the case information,
  structured finding, and recommendation without an agent assisted documentation trail.
- **T2 — Prepared agent assisted documentation trail:** Participants receive the same types of
  case information and can expand an authored trail containing investigation
  steps, supporting evidence, and references. Where available, steps also offer
  expandable plain-language evidence summaries.

The response options and finding terminology are consistent across conditions.
Both conditions use the same twelve-CVE pool and version assignments described below.

### Case Selection and Recommendation Versions

Both T1 and T2 use the same twelve selected CVEs. A reproducible pseudorandom
shuffle (release seed `56720261018`) maps the cases to positions A–L. Four fixed
versions select six cases each, using the same assignment table in both
conditions. Participants see each assigned CVE once, in independently shuffled
presentation order.

| Version | Cases presented | Correct recommendation | Incorrect recommendation |
| --- | --- | --- | --- |
| V1 | A–F | A, B, C | D, E, F |
| V2 | G–L | G, H, I | J, K, L |
| V3 | A–F | D, E, F | A, B, C |
| V4 | G–L | J, K, L | G, H, I |

Every version contains three correct and three intentionally incorrect final
recommendations (50%). Each CVE appears in two versions per condition: once
with a correct recommendation and once with an incorrect recommendation.
Incorrect recommendations are existing authored alternatives to scenario-specific
reference responses; classifications and supporting evidence remain unchanged.
See the [protocol's CVE assignment table](docs/six-case-study.md#cve-assignment-table)
for the mapping of A–L to the selected CVEs.

The system randomly assigns a version among the least-used versions within the
selected condition and design release. Assignment balancing counts all session
starts, so completed-session balance must also be checked during recruitment.
The shared pool, version, presentation order, recommendations, and materials are saved
with each session and remain fixed on refresh or resume.

### Participant allocation

| Condition | V1 | V2 | V3 | V4 | Total |
| --- | --- | --- | --- | --- | --- |
| T1 — CVE-text-only | 3 | 3 | 3 | 3 | 12 |
| T2 — Agent assisted documentation trail | 3 | 3 | 3 | 3 | 12 |
| Total | 6 | 6 | 6 | 6 | 24 |

These are completed-participant targets. The app balances version assignments
by session starts; the researcher monitors completions using the protected
recruitment view. It does not enforce recruitment quotas or replace withdrawals
automatically. Each participant completes only one condition and one version.

### Procedure

1. The researcher provides the consent procedure. The interface additionally
   collects a voluntary-participation acknowledgment, participant code,
   programming background, prior security coursework, and condition selection.
2. Participants complete one standardized fictional practice case in their
   selected interface. Practice responses are excluded from study outcomes.
3. Participants complete six vulnerability-response cases. For each case, they
   decide whether the developer should **update / remediate**, **ignore**, or
   **investigate further**. T2 participants may inspect the trail before deciding.
4. After each decision, participants review the original case and their locked
   response, then report confidence (1–7), their main reason, the information
   they used, and the recommendation's influence on their decision (1–7).
   T2 trails remain available during this review. Correctness feedback is
   withheld throughout the trials.
5. After all six cases, participants complete an adapted six-dimension NASA-TLX
   workload questionnaire and may provide final feedback. A debrief explains
   the three intentionally incorrect recommendations and the use of prepared
   study materials.

### Measures and Scoring

The primary outcomes are:

- **Decision accuracy:** Whether the selected action matches the scenario-specific
  reference response. These response answers are separate from the CVE
  classification ground truth.
- **Acceptance of correct recommendations:** The proportion of correct
  recommendations for which the participant selects the recommended action.
- **Rejection of incorrect recommendations:** The proportion of seeded incorrect
  recommendations for which the participant selects a different action.

Acceptance means choosing the recommended action; rejection means choosing
another action. With three response options, rejecting an incorrect
recommendation does not necessarily mean selecting the correct response.
Decision accuracy and recommendation acceptance are therefore scored separately.

| Recommendation | Participant response | Reliance interpretation |
| --- | --- | --- |
| Correct | Accepts | Appropriate reliance |
| Correct | Rejects | Under-reliance |
| Incorrect | Accepts | Over-reliance |
| Incorrect | Rejects | Appropriate skepticism; decision may still be incorrect |

Secondary and exploratory measures include trail opening and closing, evidence
summary interactions, case completion time, confidence, decision reasons,
self-reported information use, recommendation influence, and perceived workload.
Trail interactions during post-case review are logged separately from inspection
before the decision; opening a trail is an interaction measure, not proof that
its contents were read or understood.

Case timing begins when a case is displayed and ends when the decision is
submitted. Server timestamps determine saved durations. Time away from an
unfinished case is included; reopening the case does not reset its timer.
Practice and post-case questionnaire time are excluded from cumulative case
time, and questionnaire duration is recorded separately. Participants see no
timers or timing summaries.

Workload is collected once after the six cases using adapted NASA-TLX items
covering mental demand, physical demand, temporal demand, performance, effort,
and frustration. Ratings range from 0 to 100 in steps of five and are combined
using an unweighted mean (Raw TLX).

### Analysis and Interpretation

The comparison addresses differences in decision accuracy, acceptance of correct
recommendations, and rejection of incorrect recommendations between T1 and T2.
Within T2, exploratory analysis examines how trail inspection relates to error
rejection, confidence, completion time, and workload. Inspection is voluntary,
so these relationships do not establish that inspection causes better decisions.

Participants self-select their condition, so participant differences can explain
observed condition differences. Sharing CVEs and version assignments across
conditions reduces systematic case differences, but uneven version completion
can still produce case imbalance. Recruitment should monitor completed sessions
across all eight condition/version combinations. With a target sample of 24 participants (12 per condition), findings
will be interpreted as exploratory. The six responses from one participant are
repeated observations, not six independent participants; V1–V4 balance
recommendation correctness and are not separate study arms.

The 120-CVE engineering benchmark remains a separate evaluation of the structured
vulnerability representation and supporting pipeline. It does not establish the
effectiveness of the participant interface or the accuracy of a live agent.
See the [current six-case protocol](docs/six-case-study.md) for implementation
and data-recording details.

---

## Project Status

### Research Design and Study Preparation

- [x] Initial research questions
- [x] Initial IFC-relevant vulnerability taxonomy
- [x] 120+ manually analyzed CVEs
- [x] Revised primary human-centered research question
- [x] Final hypotheses for human study
- [x] Human-study design and participant plan
- [x] Benchmark provenance and annotation procedure documented
- [x] Formal benchmark schema
- [x] Development/evaluation split for benchmark validation
- [x] Selection of study CVEs
- [x] Text-only baseline condition
- [x] Investigating-agent condition
- [x] Pre-recorded agent agent assisted documentation trails
- [x] Seeded incorrect verdicts for reliance evaluation
- [x] Study interface and interaction logging
- [x] Engineering validation against annotated CVE benchmark
- [ ] Human-centered evaluation
- [ ] Final analysis and research report

---

## Technology 

### Backend
**Planned technologies include:**

- Python
- FastAPI
- Pydantic
- LLM API (GPT, Codex)
- vulnerability-document retrieval
- structured agent traces

**Interface**  
The study interface will present:
- application context
- CVE information
- structured IFC findings
- AI recommendation
- Agent assisted documentation trail in the agent condition
- participant decision controls
- confidence input
- interaction logging  

_**The exact model and retrieval stack will be documented once finalized.**_


## Research Data

Research datasets and annotations may have different distribution requirements from the source code.

The presence of the Apache 2.0 software license in this repository should not be interpreted as automatically licensing third-party CVE data, research annotations, external documents, or other datasets unless explicitly stated.

---

**Research datasets and third-party materials may be subject to separate terms.**


Local prototype for studying vulnerability-response decisions using twelve selected CVEs and existing verified IFC coding. Participants select T1 (text) or T2 (trail), complete one fictional practice task, then six CVE trials in that condition. Both conditions share the same twelve-CVE pool and four version assignments, with three participants per version per condition (24 total). Three of each participant’s six recommendations contain seeded errors.

## Run

For the hosted PI/mentor demo using Render, Neon, and a subdomain of
`reeseedens.dev`, see [deployment setup](docs/deployment.md). The hosted WSGI
entry point is separate from the local-only server described below.

Python 3.10+; the app uses the standard library and needs no package installation.

```sh
python3 run.py
```

Open http://127.0.0.1:8000/. Keep the process running; stop it with Ctrl+C. In **PyCharm**, open `run.py` and select **Run**. Stop an existing instance before starting another on the same port. Reload the browser after frontend edits; restart the server after Python or material changes.

`run.py` explicitly loads your private selected set and enables key-protected researcher access. It fails if that set is missing, rather than silently switching to synthetic trials. On a fresh clone without private data, use `python3 -m backend.server --materials demo` for the synthetic demonstration.

## Prototype modes

The opening screen offers **Demo mode** and **Experiment mode**.
Demo mode explores all twelve cases and both interfaces without creating a
session, recording decisions, timing, or affecting version allocation.
Experiment mode runs the participant procedure and saves responses and events.
At completion or withdrawal, the researcher can unlock **Show session log**
or download the JSON export using the existing researcher key. The opening
screen also provides protected recruitment counts for all eight condition/version
combinations. See the [two-mode demonstration walkthrough](docs/prototype-modes.md).

## Where to work

| Task | Location |
| --- | --- |
| Participant screens and interaction | `frontend/app.js`, `frontend/index.html` |
| Styling | `frontend/style.css` |
| Researcher annotation view | `frontend/research.js`, `frontend/research.html` |
| Trial flow, scoring, saved sessions | `backend/study.py` |
| Local server and API | `backend/server.py` |
| Annotation comparison | `backend/annotations.py` |
| 12 scenario records | `data/private/selected_cases.json` |
| Readable scenarios and answer rubrics | `data/private/participant-scenarios.md` |
| Original imported coding | `data/annotations/library.json` |
| Saved responses | `results/prototype.sqlite3` |
| Tests | `backend/tests/` |

The synthetic fixtures in `data/study/` are still required for practice, demo mode, tests, and legacy session compatibility. `backend/src/models/vulnerability_schema.py` is the shared codebook benchmark schema version 2.0; the current app does not import it. It replaces legacy snake-case category values and the separate flow mechanism and side-channel fields with the workbook's `flow_type`, and includes `ifc_relevant`. Existing serialized schema 1.0 records require explicit migration before validation.

## Test

```sh
python3 -m unittest discover -s backend/tests -v
```

## Documentation and maintenance

- [Selected scenarios, PyCharm configuration, and exports](docs/selected-scenarios.md)
- [Private data and researcher access](docs/private-data.md)
- [Maintenance scripts](scripts/README.md)
- [Paper and Overleaf notes](docs/Overleaf/)
- [Research references](docs/papers_and_references.md)
- [Historical plans and earlier implementation notes](docs/archive/)

Software is licensed under [Apache 2.0](LICENSE). Research datasets, annotations, and third-party materials may have separate terms.
