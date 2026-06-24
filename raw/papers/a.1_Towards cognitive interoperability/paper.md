# Towards Cognitive Interoperability: Cognitive Digital Twin and Cognitive Architecture for Human-CPS Collaboration

**Author:** Jana AL HAJ ALI
**Institution:** Université de Lorraine — École doctorale IAEM Lorraine
**Lab:** CRAN, CNRS — UMR 7039
**Thesis Directors:** Hervé Panetto (Professor, Université de Lorraine), Yannick Naudet (Lead Scientist ADR, Luxembourg Institute of Science and Technology)
**Type:** PhD Thesis (Doctorat de l'Université de Lorraine)
**Mention:** Automatique, Traitement du signal et des images, Génie informatique

---

## Abstract

Industry 5.0 promotes human-centric production systems where humans and Cyber-Physical Systems (CPS) collaborate as partners rather than operating in isolated roles. In such contexts, semantic interoperability alone is insufficient, since successful collaboration requires not only a common interpretation of data, but also the alignment of situation awareness, mental models, intentions, and decision-making processes.

This thesis investigates the transition towards **cognitive interoperability** in Cyber-Physical Enterprises (CPEs) by proposing a framework based on a **Cognitive Digital Twin (CDT)** and a **Cognitive Architecture** to support collaboration between humans and CPS.

The thesis:
1. Establishes a formal conceptualisation of cognitive systems and introduces a definition of cognitive interoperability that extends beyond semantic alignment.
2. Based on cognitive psychology and team cognition theories, proposes a **Maturity Model of Cognitive Interoperability (MMCI)** characterising progressive levels of cognitive alignment — from shared situation awareness to joint decision-making with metacognitive regulation.
3. Defines the CDT as a DT enriched with cognitive capabilities and analyses architectural requirements.
4. Designs an ontology-based semantic foundation (CDTO) to represent tasks, agents, capabilities, abilities, and contextual constraints within a unified knowledge model.
5. Integrates the **CLARION** cognitive architecture as the decision-making core of the CDT, enabling hybrid neuro-symbolic operation.

Validated through an industrial human-robot collaborative assembly use case involving a **UR5e cobot**.

**Keywords:** Cognitive Interoperability, Cognitive Digital Twin, Cyber-Physical Systems, Human-Robot Collaboration, Ontologies, Cognitive Architectures, Neuro-symbolic AI, Industry 5.0.

---

## List of Publications

### Journal Publications
- Al Haj Ali, J. et al. (2025). Enabling human-CPS cognitive interoperability: Cognitive architectures as technologies for human-like cognitive digital twins. *Journal of Industrial Information Integration*, 48, 100969.
- Gaffinet, B., Al Haj Ali, J. et al. (2025). Human Digital Twins: A systematic literature review and concept disambiguation for industry 5.0. *Computers in Industry*, 166, 104230.
- Al Haj Ali, J. et al. (2024). Cognitive systems and interoperability in the enterprise: A systematic literature review. *Annual Reviews in Control*, 57, 100954.

### International Conferences
- Al Haj Ali, J. et al. (2025). From Semantic Interoperability to Cognitive Interoperability: Enabling Human-CPS Collaboration in Industry 5.0. IN4PL 2025, Marbella, Spain.
- Naudet, Y., Zehnder, E., Gaffinet, B., Al Haj Ali, J. et al. (2025). A Human Ontology with Cognition and Ability Models for Human and Cognitive Digital Twins. IN4PL 2025, Marbella, Spain.
- Gaffinet, B., Al Haj Ali, J. et al. (2025). Towards Cognitive Interoperability with Cognitive Human Digital Twins. EI2N 2025, Marbella, Spain.
- Bhattacharya, S., Al Haj Ali, J. et al. (2025). Ontology-Guided Deep Reinforcement Learning for Robotic Task Execution. IFAC-PapersOnLine, 59(26), 311-316.
- Naudet, Y., Al Haj Ali, J. et al. (2024). Cognition in digital twins for cyber-physical systems and humans: Where and why? IN4PL 2024.
- Al Haj Ali, J. et al. (2024). Cognitive architecture for cognitive cyber-physical systems. *IFAC-PapersOnLine*, 58(19), 1180-1185.
- Gaffinet, B., Al Haj Ali, J. et al. (2023). Human-centric digital twins: Advancing safety and ergonomics in human-robot collaboration. IN4PL 2023.

### Submitted / Under Review
- Al Haj Ali, J. et al. (2026). Ontology-Guided Cognitive Digital Twin with Cognitive Architecture for Autonomous Ability Learning in HRC. 23rd IFAC World Congress, Busan, South Korea.
- Al Haj Ali, J. et al. (2026). Evolving from Semantic to Cognitive Digital Twins: A Comparative Framework for Resilience in Industry 5.0. 23rd IFAC World Congress, Busan, South Korea.

---

## Acronyms

| Acronym | Meaning |
|---------|---------|
| ACS | Action-Centred Subsystem |
| AI | Artificial Intelligence |
| AI4C2PS | Artificial Intelligence for Cognitive Cyber-Physical Systems Interoperability |
| AMNs | Associative Memory Networks |
| ARS | Action Rule Store |
| CCPS | Cognitive Cyber-Physical Systems |
| CDT | Cognitive Digital Twin |
| CPE | Cyber-Physical Enterprise |
| CPHS | Cyber-Physical-Human Systems |
| CPSs | Cyber-Physical Systems |
| CPSSs | Cyber-Physical-Social Systems |
| DT | Digital Twin |
| EIF | European Interoperability Framework |
| GKS | General Knowledge Store |
| HCC | Human-CCPS Collaboration |
| HDT | Human Digital Twin |
| HRC | Human-Robot Collaboration |
| IDNs | Implicit Decision Networks |
| KGs | Knowledge Graphs |
| KRR | Knowledge Representation and Reasoning |
| LTM | Long-Term Memory |
| MCS | Meta-Cognitive Subsystem |
| MS | Motivational Subsystem |
| NACS | Non-Action-Centred Subsystem |
| OWL | Web Ontology Language |
| RDF | Resource Description Framework |
| RDFS | RDF Schema |
| SLR | Systematic Literature Review |
| SWRL | Semantic Web Rule Language |
| URN | Uniform Resource Name |
| WM | Working Memory |

---

## Introduction

### 0.1 Context and Motivation

Industrial production systems are currently going through a profound transformation associated with Industry 4.0, driven by sensors, connectivity, and close integration of computing into physical processes. Within this vision, **Cyber-Physical Systems (CPSs)** are recognised as a central technological building block coupling physical entities with cyber components for monitoring, control, and decision support.

However, as industrial environments become increasingly interactive and adaptive, it is no longer sufficient to consider only the cyber-physical coupling. Operators continuously interpret context, manage trade-offs, handle uncertainty, and adapt actions when conditions deviate from nominal expectations. This motivates the paradigm of **Cyber-Physical-Human Systems (CPHS)**, which consider humans as integral elements of the global system.

**Industry 5.0** grounds this evolution in human-centricity: the aim is no longer to fully automate tasks, but to facilitate cooperation between people and machines, leveraging human skills such as creativity, problem-solving, and adaptation.

Despite this objective, a key gap remains: many CPSs are primarily designed as autonomous technical entities, with a limited human role in supervision. The *human-in-the-loop* remains confined to interfaces and control actions; humans are not truly integrated as collaborative partners in the system's reasoning and adaptation mechanisms.

### 0.2 Trends and Industrial Transformation

#### 0.2.1 From Challenges in Human-CPS Collaboration

The effectiveness of a CPE depends on interoperability — the ability to exchange information and make use of it in a consistent manner (European Commission, 2017). **Semantic interoperability** ensures that exchanged information is interpreted with the same meaning by all parties, typically achieved through shared vocabularies and formal knowledge models (ontologies).

However, when collaboration involves humans (e.g., HCC, HRC), semantic interoperability remains a necessary but insufficient foundation. Collaboration is not only a matter of accessing the same information; it also relies on how agents interpret situations, form expectations, coordinate roles, and adapt to evolving context during joint activity. Semantic alignment of information must be complemented by mechanisms enabling systems to represent and reason about intentions, roles, commitments, and context — motivating the transition to **cognitive interoperability**.

**Cognitive interoperability** is understood as the ability of interacting entities to align not only the meaning of exchanged information, but also the cognitive structures that support interpretation and joint action (e.g., intentions, perspectives, roles, and context).

#### 0.2.2 Towards Cognitive Interoperability Between Humans and CCPSs

Human cooperation is supported by cognitive capabilities that go beyond decoding information: humans coordinate by forming shared goals, anticipating each other's intentions, managing commitments, and adapting behaviour as situations evolve. In collaborative work, cognition can be understood as the set of processes by which sensory information is transformed, reduced, processed, stored, retrieved and used to guide decision and action (Neisser, 1967). These processes include perception, attention, memory, learning, reasoning, problem solving, and situational awareness.

Operationalizing cognitive interoperability requires computational supports that can: (i) represent the state of the system and the collaboration context, (ii) reason about tasks and goals, and (iii) adapt behavior and explanations to human needs. **Digital Twins (DTs)** provide a natural infrastructure, which can be extended to host reasoning and decision mechanisms.

This leads to the notion of a **Cognitive Digital Twin (CDT)** — a DT enriched with cognitive capabilities. When the twinned entity is technical, the CDT supports interpretation and adaptive control beyond physical monitoring. When the twinned entity is human, the CDT takes the form of a **Human Digital Twin (HDT)**, intended to represent human state and dynamics.

### 0.3 Project Context: AI4C2PS

This thesis is conducted in the context of the **AI4C2PS** project (*Artificial Intelligence for Cognitive Cyber-Physical Systems Interoperability*), a bilateral initiative funded by the French National Research Agency (ANR) and the Luxembourg National Research Fund (FNR). The consortium includes the University of Lorraine, the Research Centre for Automatic COntrol (CRAN CNRS UMR 7039), the Luxembourg Institute of Science and Technology (LIST), and the enterprise Orisun (ORSN).

AI4C2PS proposes extending interoperability from the semantic to the cognitive level by integrating models that represent concepts, cognitive processes and collaborative dynamics, with a human-centric orientation aligned with trustworthy AI.

### 0.4 Research Questions and Objectives

**Overall objective:** Establish the conceptual, methodological and computational principles that enable cognitive interoperability between humans and CPSs.

**RQ1:** *How can cognitive interoperability within a CPE be formally defined and characterised, and how can a maturity model capture the transition from semantic to cognitive interoperability?*

**RQ2:** *What constitutes a cognitive layer? How can a CCPS and a CDT be defined, and more generally, what is a cognitive system?*

**RQ3:** *Which representation principles and knowledge structures are required to support cognitive interoperability in CDTs?*

**RQ4:** *Which cognitive-architecture requirements enable a CDT to perform cognitive functions needed for collaboration (reasoning, adaptation, and explainability), and how can these architectures be integrated with the chosen knowledge representations?*

### 0.5 Contributions and Structure

**C1: Formal characterisation of cognitive entities** — formal characterisation of cognitive systems, CCPS and CDT. *(Addresses RQ2)*

**C2: Formal definition of cognitive interoperability** — definition that distinguishes it from semantic interoperability by focusing on cognitive alignment mechanisms (intentions, roles, context and adaptive coordination). *(Addresses RQ1)*

**C3: Cognitive interoperability maturity model** — multi-level maturity model (MMCI) assessing the progression from semantic to cognitive interoperability in HCC. *(Addresses RQ1)*

**C4: Ontology supporting cognitive interoperability in collaborative tasks** (CDTO) — structures the knowledge required for collaboration (task context, roles, goals, constraints, interaction state). *(Addresses RQ3; supports RQ4)*

**Thesis structure:**
- **Chapter 1** — State of the Art (foundations for all RQs)
- **Chapter 2** — Conceptualisation: cognitive systems, cognitive interoperability, MMCI (RQ1, RQ2)
- **Chapter 3** — Architecture for CDT with CLARION (RQ4)
- **Chapter 4** — CDTO Ontology for CDTs (RQ3)
- **Chapter 5** — Use Case: HRC implementation and evaluation (RQ3, RQ4)
- **Chapter 6** — General Conclusion

---

## Chapter 1 — State of the Art

Three complementary literature reviews structured around the three main research questions:

- **Review I:** Cognitive Interoperability Concept → RQ1
- **Review II:** Cognitive Systems → RQ2
- **Review III:** Technologies Enabling Cognition → RQ3

### 1.1 Review on the Cognitive Interoperability Concept

The European Interoperability Framework (EIF) proposes a layered interoperability model with four layers:
- **Legal Interoperability** — organisations under different legal frameworks
- **Organisational Interoperability** — alignment of business processes and responsibilities
- **Semantic Interoperability** — preservation of precise format and meaning of exchanged data
- **Technical Interoperability** — applications and infrastructures linking systems

When humans collaborate with machines, the limitations of semantic interoperability become apparent: simply having semantic interoperability *"is not always sufficient to ensure that CPSs and human agents understand each other well enough to cooperate or collaborate effectively"* (Naudet et al., 2023a).

#### 1.1.1 Review of Existing Definitions

| Reference | Definition |
|-----------|------------|
| Goldkuhl (2008) | *Cognitive Interoperability is a part of organisational interoperability related to the congruence in thought and perceptions or the human actors' way of thinking: aligning the way they conceptualise and understand information.* |
| Berthier (2006) | Semiotico-cognitive interoperability: an artificial agent *appears to behave in the same way as a human agent would in the same situation*, some meanings seem to be shared using standardised languages and normalised means to translate between different knowledge representations, including ontologies. |
| Vogt (2023) | *A critical characteristic of data structures and information technology systems that plays an essential role in facilitating efficient communication of data and metadata with human users.* Encompasses how humans prefer to interact with technology (HCI) and how they interact with information (human information interaction), considering their general cognitive conditions. |
| Blad & Potts (2003) | A unity of mindsets, confidence/trust and mutual understanding based on shared education and values. |
| Kwon et al. (2011) | *Socio-Cognitive Interoperability* is the ability of systems and users to share and understand information coherently by incorporating socio-cognitive aspects, enabling effective communication, shared understanding, and joint decision-making, particularly in complex situations. |
| Raubal (2005) | *Cognitive semantic interoperability* consists of aligning the data representation of systems with human conceptual structures. Mental models of both sender and receiver have to be mapped for complete understanding. |
| Bytniewski et al. (2015) | Ability of different systems or agents to work together, exchanging and understanding knowledge in a way that promotes collaborative decision-making and adaptive behavior, drawing on cognitive processes. |
| Myneni et al. (2016) | The ability of a system to align itself with the cognitive processes of users, making it easier for them to interact with the system in accordance with their habitual thought patterns. |
| Krinkin et al. (2023) | The ability of human and artificial intelligence to work together by synchronizing their knowledge and sharing a common understanding, even when they have different ontological models. |

**Key dimensions emerging from the literature:**
1. Recurring theme of aligning mental models — shared understanding, mutual perception and trust
2. Integration of cognitive processes (intentionality, reasoning, adaptation) into systems
3. Importance of contextualisation and user-centred interaction

#### 1.1.2 Application Domains

Cognitive interoperability has applications across multiple fields, all involving situations where **agents with different cognitive models must achieve mutual understanding in order to act coherently together**:
- Military domain — unity of mind and mutual understanding through joint training
- Crisis management — real-time communication, joint decision-making under uncertainty
- E-government — convergence of thought among public institutions
- Geographic information systems — adapts data representations to mental models of users
- Enterprise systems and HMI — semiotic-cognitive interoperability, human-like reasoning alignment
- Human-machine collaboration — continuously adapts and aligns human and AI agents
- Integrated management systems — enables subsystems to share knowledge via adaptive behaviour
- Biomedical laboratories — usability improvement by aligning system interfaces with thought patterns
- Information systems — knowledge graphs with interactive exploration strategies

**Common theme:** heterogeneous agents, dynamic decision-making in uncertain contexts, variable user expertise, and the need for collaborative reasoning.

### 1.2 Review on Cognitive Systems

Systematic Literature Review (SLR) following Kitchenham guidelines. **Search query:**

> *"Cognition" **AND** ("Interoperability" OR "Digital Twin" OR "Cyber-Physical Systems")*

**Databases:** Web of Science (503 → 314), ACM (64), IEEE Xplore (175), Scopus (503), PubMed (23) → **Total: 1079 papers → 90 selected** after full filtering.

**SLR Sub-Research Questions (SRQs):**
- **SRQ1:** How is cognition characterised and defined in cognitive psychology?
- **SRQ2:** Which cognitive functions are integrated into CPS and DT?
- **SRQ3:** What methods/strategies are used to implement cognition in CPS and DT?
- **SRQ4:** What are the theoretical foundations of cognition used in CPS and DT?
- **SRQ5:** How are cognitive CPS and DT conceptualised within Industry 4.0/5.0?
- **SRQ6:** How can interoperability be enhanced by cognition?
- **SRQ7:** What types of KRR approaches are commonly used?

**Temporal trend:** Low activity 1995–2007; gradual increase from 2011; significant peak in 2022.

**Application areas:** Manufacturing (46%), Industry 4.0 (29%), Infrastructure/Smart Cities (9%), Security & Defense (4%), Maintenance (4%), Others (8%).

#### 1.2.3 Theoretical Foundations for Systems Cognition

##### 1.2.3.1 Cognition

Cognition refers to the set of mental processes that enable humans and other agents to interact effectively with their environment. Key definitions from the literature:

| Theme | Definition |
|-------|------------|
| Awareness | Integrative capability to perceive and interpret the environment and its context, to learn from past actions, and to use this knowledge to reason, anticipate, and guide decisions toward specific goals. Involves real-time situation awareness. |
| Knowledge acquisition | Mental processes through which knowledge is acquired, structured, and understood by combining experience, perception, and reasoning. |
| Information processing | Processes that enable an agent to transform, organise, store, retrieve, and use information obtained from the environment. Includes perception, data interpretation, memory management, and reasoning. |

Cognition involves both **procedural knowledge** (how to perform actions) and **declarative knowledge** (facts and concepts). It is not a static capability but a continuous process of exploration and adaptation.

**In industrial research:** Cognition in CCPS is mainly associated with perception, continuous interaction, and decision-making based on real-time data. CDTs focus more on knowledge acquisition, organisation, and exploitation to support prediction and reasoning.

##### 1.2.3.2 Cognitive Functions

Main cognitive functions in CDTs (Faruque et al., 2021):
- **Perception:** transforms data representations into useful information
- **Attention:** selectively focuses on relevant tasks/data, filtering distracting elements
- **Reasoning:** draws conclusions from a starting point, often relying on existing memory or assertions
- **Learning:** converts experience into reusable knowledge, enabling adaptation and evolution
- **Problem-solving and decision-making:** work together to find solutions and reach goals
- **Memory:** stores and recalls information, from specific events to general knowledge about the environment

**CCPS vs CDT distinction:**
- CCPS: situated cognition and immediate action (real-time perception, situational awareness)
- CDT: model-based understanding, anticipation, and explicit reasoning (simulation, prediction)

This epistemic orientation makes CDTs particularly suitable as hosts for higher-level cognitive functions and interoperability mechanisms.

##### 1.2.3.3 Technologies Enabling Cognition in CCPS and CDT

**AI-based technologies (SRQ3):**
- Data-driven approaches (ML, DL) — pattern extraction, prediction, classification
- Language technologies (NLP, LLM-based) — text understanding, knowledge extraction, NL interaction
- Vision-based approaches (computer vision) — visual signal interpretation

**Knowledge Representation and Reasoning (KRR) (SRQ7):**
- **Ontologies:** shared vocabularies and formal conceptualisations, rule-based reasoning, explicit assumptions
- **Knowledge Graphs (KGs):** entities and relations in a graph structure, contextual linking, querying, inference

Two dominant KRR approaches in CCPS and CDT literature: ontologies (semantic consistency, rule-based reasoning) and KGs (contextual linking, extensible knowledge base).

#### 1.2.4 Cognitive Systems in CPE

##### 1.2.4.1 Cognitive Cyber-Physical Systems (CCPS)

Key characteristics:
- **Adaptability** — modifies and optimises behaviour in response to changing environments
- **Autonomy** — self-monitors and solves problems
- **Awareness** — perceives its environment and its own state

##### 1.2.4.2 Cognitive Digital Twin (CDT)

CDTs enrich classical DTs with cognitive capabilities for interpretation, adaptive control, and reasoning about environment and objectives. Key distinction: CDTs emphasise model-based understanding and explicit reasoning (simulation, prediction), making them suitable hosts for higher-level cognitive functions.

### 1.3 Technologies Enabling Cognitive Digital Twin

#### 1.3.1 Technologies for Emulation Function
Technologies enabling a DT to faithfully replicate the behaviour and state of the physical entity: digital representations, data synchronisation, real-time monitoring.

#### 1.3.2 Technologies for Cognition Function
AI-based and KRR technologies (ML, DL, NLP, ontologies, KGs) enabling perception, reasoning, learning, and decision-making within CDTs.

#### 1.3.3 Technologies for Simulation Function
Technologies enabling CDTs to simulate future states, predict behaviour, and test scenarios: simulation engines, predictive models.

#### 1.3.4 Cognitive Architectures

Cognitive architectures provide unified computational frameworks inspired by theories of cognition — reusable building blocks and control structures to combine multiple cognitive functions coherently.

**Cognitive Architectures in Biological Systems:**
- Common Model of Cognition (Rosenbloom et al., 2024) — integrative reference model

**Cognitive Architectures in Artificial Intelligence:**
- **ACT-R** (Anderson) — modular architecture mapping on brain regions
- **SOAR** (Laird et al., 2017) — production rule-based cognitive architecture
- **Spaun** (Stewart et al., 2012) — neural simulation-based architecture
- **CLARION** (Sun, 2006/2007) — hybrid neuro-symbolic architecture with four subsystems: ACS, NACS, MS, MCS

**Selection of CLARION for CDT:**
Justified by: (i) hybrid explicit/implicit (neuro-symbolic) organisation, (ii) dedicated subsystems for action, knowledge, motivation and metacognition, (iii) mechanisms enabling both explainable decision and learning-based adaptation.

---

## Chapter 2 — Conceptualisation of Cognitive Systems, Cognitive Interoperability, and Its Maturity Model

### 2.1 Cognitive Systems in Industry

#### 2.1.1 Defining a Cognitive System
A system equipped with mechanisms that support perception, reasoning, learning, and decision making — aiming to support human-like reasoning and learning capabilities.

#### 2.1.2 Defining a Cognitive Cyber-Physical System (CCPS)
CPS enriched with cognitive capabilities (e.g., interpretation, reasoning, adaptation, explainability) during interaction. Characteristics: autonomy, adaptability, and awareness.

#### 2.1.3 Defining a Cognitive Digital Twin (CDT)
A DT enriched with cognitive capabilities. Defined as a computational entity resting on three main functions: **emulation, simulation**, and **cognition**. The cognition function is the focus — it supports interpretation and adaptive decision-making.

Two implementation strategies:
1. **Externalised cognition** strongly coupled to the physical system
2. **Internalised cognition** within the CDT — more modular, serving primarily decision-making and reasoning

#### 2.1.4 The Cognitive Functions
Hierarchical meta-model of the different components of a cognitive system and their relations to cognitive functions and abilities (adapted from Naudet et al., 2025):
- Perception, Attention, Reasoning, Memory, Learning, Problem-solving, Decision-making, Situational Awareness

### 2.2 Cognitive Interoperability: Concept and Vision

#### 2.2.1 Why Semantic Interoperability is Not Sufficient

Semantic interoperability ensures common interpretation of data. But effective collaboration requires not only semantic alignment but also:
- Alignment of situation awareness
- Shared mental models
- Aligned intentions and reasoning strategies
- Joint decision-making with metacognitive regulation

**Definition proposed:**
> *Cognitive interoperability is the capacity of human and/or artificial agents to align their thoughts and their perception of information in order to achieve mutual understanding and shared intentions, through the construction of common mental models and a common way of using, interpreting, and reasoning about knowledge.*

#### 2.2.2 Terminological Landscape: A Bag-of-Words Analysis

Key semantic groups contributing to cognitive interoperability:
1. **Understanding** — mutual comprehension, shared meaning
2. **Thoughts** — mental processes, reasoning, intentions
3. **Perception** — situational awareness, contextual interpretation
4. **Decision-Making** — joint action, adaptive coordination
5. **Mental Models** — shared representations of tasks, agents, context

### 2.3 Architecture for Cognitive Interoperability

Functional Architecture for Achieving Cognitive Interoperability between Human and CPS Agents — defines the computational components required to support each level of cognitive alignment.

### 2.4 Maturity Model of Cognitive Interoperability (MMCI)

The MMCI structures cognitive interoperability into progressive levels, grounded in:
- Cognitive skill hierarchies (e.g., Bloom's taxonomy)
- Neuropsychological domains (executive functions, metacognition)
- Team cognition and joint action theories

**Levels:**

| Level | Name | Description |
|-------|------|-------------|
| 0 | Semantic Interoperability | Maximum achievable via semantic interoperability only; common data interpretation |
| 1 | Shared Situation Awareness | Shared perception of the current state; agents understand what is happening |
| 2 | Shared Mental Models | Agents share representations of tasks, roles, constraints, and expectations |
| 3 | Intent and Reasoning Alignment | Mutual alignment of intentions and reasoning strategies |
| 4 | Joint Decision-Making with Metacognitive Regulation | Fully collaborative decision-making with self-monitoring and adaptive regulation |

---

## Chapter 3 — Architecture for the Cognitive Digital Twin

### 3.1 Cognitive Digital Twin Framework

Three CDT functions:
- **Emulation:** faithful replication of physical entity behaviour and state
- **Cognition:** interpretation, reasoning, decision-making, adaptation — the focus of this chapter
- **Simulation:** anticipation, prediction, scenario testing

Two implementation strategies (Figure 3.2):
1. Cognition externalised to support a CCPS via strong coupling
2. Cognition internal to the CDT, supports only its own functions, with weak coupling to the physical system

### 3.2 Cognitive Architectures for Cognitive Digital Twins

#### 3.2.2 Comparison of Cognitive Architectures and Selection of CLARION

Comparison criteria for CDT selection:
- Hybrid/neuro-symbolic operation
- Multi-modal perception capabilities
- Action selection mechanisms
- Memory subsystems (procedural + declarative)
- Goal/motivation management
- Metacognitive monitoring
- Explainability of decisions
- Integration with ontologies/KRR

**CLARION selected** as the most suitable architecture for CDTs because it satisfies all selection criteria with its four subsystems.

### 3.3 CLARION Architecture for CDTs

CLARION (Connectionist Learning with Adaptive Rule Induction ON-line — Sun, 2006/2007):

#### 3.3.1.1 Action-Centred Subsystem (ACS)
- Procedural knowledge — action selection, execution
- Top level: explicit rules (symbolic reasoning)
- Bottom level: implicit routines (neural networks, reinforcement learning)
- Compact logigram for bottom-up rule extraction and refinement

#### 3.3.1.2 Non Action-Centred Subsystem (NACS)
- Declarative knowledge — facts, beliefs, world model
- General Knowledge Store (GKS)
- Associative Memory Networks (AMNs)

#### 3.3.1.3 Motivational Subsystem (MS)
- Goal and priority management
- Drives and motivations guiding action selection

#### 3.3.1.4 Meta-Cognitive Subsystem (MCS)
- Monitors and regulates the other subsystems
- Triggers learning, monitors errors, arbitrates between rules and learning
- Supervises adaptive regulation

#### 3.3.2 Integration of CLARION into the CDT Environment

Mapping of CDT cognitive functions to CLARION mechanisms:

| CDT Cognitive Function | CLARION Mechanism |
|----------------------|-------------------|
| Perception | ACS bottom-level perception pipeline |
| Attention | ACS action selection filtering |
| Reasoning | NACS + ACS top-level symbolic rules |
| Memory | NACS (declarative) + ACS (procedural) |
| Learning | ACS bottom-up rule extraction, RL |
| Decision-making | ACS action selection + MCS monitoring |
| Goal management | MS |
| Metacognitive regulation | MCS |

**Operational coupling between CDT and CLARION:** Ontology reasoning results are fed as perception variables into CLARION subsystems; CLARION action outputs drive CDT effectors.

---

## Chapter 4 — CDTO Ontology for Cognitive Digital Twins

### 4.1 Motivation and Role of Ontologies in Cognitive Systems

To make human-CCPS collaboration coherent and explainable, a shared model is needed describing:
- Tasks and their structure (workflow)
- Agents (human, robot, systems)
- Capabilities and abilities (capabilities/abilities)
- Objects, resources, constraints, and contextual conditions

The ontology plays a dual role: (i) formally structure knowledge and (ii) enable **reasoning** to derive information useful for decision-making.

#### 4.1.3 Why an Ontology in Addition to a Cognitive Architecture
The ontology constitutes the declarative memory and reasoning base of the CDT:
- Formalises execution rules, feasibility, and temporal dependencies
- Supports explainable decision mechanisms (via symbolic deduction)
- Prepares integration of ontological reasoning into a hybrid cognitive architecture

#### 4.1.4 CLARION-Ontology Integration
Ontological reasoning results are transformed into perception variables and injected into CLARION architecture subsystems.

### 4.2 Ontology Concepts, Languages, and Inference

Technology stack:
- **RDF** — knowledge representation as triples (Subject-Predicate-Object)
- **RDFS** — schema-level semantics and constraints
- **OWL** — expressive ontology language with logical semantics
- **SPARQL** — queries for knowledge retrieval
- **SWRL** — rules for semantic reasoning and inference

### 4.3 Overview and Conceptual Model of the CDTO Ontology

CDTO is organised in modules and reuses external ontologies (SOMA, HUMO) to favour alignment with existing standards. Validated in Protégé; logical consistency verified by HermiT reasoner.

### 4.4 Ontology Classes, Properties, and Constraints

#### 4.4.1 Classes of the CDTO Ontology
Main classes: Tasks, Agents, Capabilities, Abilities, Objects, Resources, Constraints, Context.

#### 4.4.2 Class Hierarchy and Taxonomy
Hierarchical structure enabling inheritance and specialisation of concepts.

#### 4.4.3 Constraints and Consistency Rules
OWL axioms ensuring consistency and logical completeness.

### 4.5 HUMO: Human and Cognition Layer in CDTO

#### 4.5.1 Human-System-Cognition Structure and Integration with SOMA
Integrated with SOMA (Socially-Situated Everyday Activities) ontology. Models human agents with their cognitive capabilities.

#### 4.5.2 Cognition Model and Link to Mental Tasks
Cognitive functions linked to mental tasks of SOMA in HUMO — formalises the relationship between human cognitive capabilities and task execution requirements.

### 4.6 Capabilities, Abilities, and Affordances (CAA) Model in HUMO

Formalises the relationship between agent capabilities, situational abilities (what an agent can do in a given context), and affordances (what the environment enables).

Formalisation with SOMA Affordances.

### 4.7 SWRL Rules for Reasoning and Inference Mechanisms

SWRL rules enabling:
- Inferring task feasibility from agent capabilities
- Detecting missing capabilities and triggering learning
- Deriving high-level workflow progression
- Identifying role assignment constraints

---

## Chapter 5 — Use Case Implementation and Evaluation of Cognitive Interoperability

### 5.1 Use Case Description: Human-Robot Collaborative Assembly

#### 5.1.1 Workstation Overview
Industrial human-robot collaborative assembly workstation:
- Physical setup: stock zone (red) and assembly zone (green)
- Equipment: **UR5e cobot** with screwdriver tool + human operator
- Task: motor assembly with screwing operations

#### 5.1.2 Assembly Description and Sequence of Operations
Collaborative motor assembly process decomposed into hierarchical steps. Task-agent matching for the collaborative motor assembly process.

#### 5.1.3 Human and Robot Roles in the HRC Scenario
- Human operator: handles tasks requiring dexterity, contextual judgment, and adaptation
- UR5e cobot: handles structured, repeatable tasks (screwing)
- CDT: cognitive intermediary supporting monitoring, reasoning, and adaptation

#### 5.1.4 Motivation and Problem Statement
Goal: demonstrate how the CDT, enriched by ontology and cognitive architecture, enables more adaptive collaboration than a strictly semantic approach. Specifically: handle unforeseen situations, redistribute tasks if necessary, allow the robot to compensate for certain capability limitations.

### 5.2 Cognitive Digital Twin for the HRC Use Case

Architecture of the CDT where cognition exploits CDTO ontology and is driven by CLARION. Conceptual Architecture for Human-CPS Collaboration integrating CDT and HDT.

### 5.3 Ontology Instantiation and Reasoning

#### 5.3.1 Creation of the NGSI-LD Input File
NGSI-LD (Next Generation Service Interface - Linked Data) used for context data representation and ingestion into the ontology.

**Structure of the NGSI-LD file:** encodes agents, tasks, objects, constraints as linked data entities.

**Modelling the steps of the screwing scenario:** each step is represented as an ontology individual with properties (agent, tool, object, constraints, pre/post-conditions).

#### 5.3.2 Automatic Ontology Instantiation and Inference
Workflow from environment data → CDTO instantiation → inferred knowledge. Automatic instantiation from NGSI-LD input.

#### 5.3.3 Inferences
SWRL/OWL inference results include:
- Workflow progression
- Action feasibility
- Capability prerequisites
- Missing tasks or agents

### 5.4 CLARION Cognitive Architecture for the Use Case

#### 5.4.1 Integration of Ontology Reasoning with CLARION
Ontology reasoning results → perception variables → injected into CLARION subsystems:
- **ACS:** action filtering and execution via rules and routines
- **NACS:** storage of declarative knowledge (workflow, relations, context)
- **MS:** management of collaboration goals and priorities
- **MCS:** supervision, learning trigger, adaptive regulation

#### 5.4.2 CLARION Configuration

**CLARION information flow:** Environment → perception pipeline → ACS/NACS processing → action selection → effectors.

**Feature and chunk modelling:** environmental state features encoded as perceptual inputs; CLARION chunks represent working memory elements.

#### 5.4.3 Learning Mechanisms and Training

#### 5.4.4 Reinforcement Learning for the Screwing Skill

PPO (Proximal Policy Optimization) RL module for acquiring the screwing procedural skill:

**Environment modelling:** screwing tool-screw interaction dynamics — vertical position, rotation progress, force/torque signals.

**Training procedure:** RL traces showing tool-screw interaction over time.

**Integration with CLARION decision-making:** RL-learned skill is a skill execution module within CLARION; high-level decisions remain managed by CLARION, ensuring workflow coherence and explainability.

### 5.5 Evaluation Framework and Metrics

MMCI indicators evaluated in the use case. The evaluation targets cognitive interoperability between:
- `<CPS, CDT>` — evidence from CDT internal reasoning
- `<Human, HDT>` — evidence from human-CDT interaction

Comparison vs. semantic-only baseline (CDT without cognitive architecture).

**Results show the cognitive CDT improves:**
- **Adaptability** — handling deviations and missing tasks
- **Decision quality** — taking constraints, objectives and context into account
- **Robustness** — overall interaction robustness in dynamic collaborative scenarios

---

## Chapter 6 — General Conclusion

### 6.1 Summary of the Thesis

This thesis proposes a complete framework to support the transition from semantic to cognitive interoperability in CPEs, combining:

1. A **formal definition** of cognitive interoperability
2. A **maturity model** (MMCI) structuring its levels
3. A **cognitive CDT architecture** based on CLARION
4. An **ontology** (CDTO) for representation and reasoning
5. **Experimental validation** in human-robot collaboration with simulation integration and procedural learning

### 6.2 Perspectives and Future Directions

- Extension of the MMCI with more measurable indicators
- Richer HDT models for dynamic human state representation
- Scaling to multi-agent scenarios (multiple humans and robots)
- Deeper integration of LLM-based components for natural language interaction
- Transfer learning for cognitive ability acquisition across different contexts

---

## Appendix A — Implementation Listings (NGSI-LD and Ontology Processing)

- A.1 NGSI-LD input format
- A.2 Ontology loading and merging (Owlready2)
- A.3 Automatic ontology instantiation from NGSI-LD
- A.4 Inference illustration (before vs. after)

## Appendix B — Additional CLARION Functional Pathways

- B.1 PyClarion Long-Term Memory pipeline
- B.2 PyClarion Short-Term Memory pipeline
- B.3 PyClarion Action Selection pipeline
