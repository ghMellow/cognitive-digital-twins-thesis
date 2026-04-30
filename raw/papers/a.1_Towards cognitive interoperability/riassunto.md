Ecco il riassunto strutturato della tesi, pensato come scheda di consultazione rapida.

---

# 📋 Scheda di Riferimento — Tesi CDT & Cognitive Interoperability

**Titolo completo:** _Towards Cognitive Interoperability: Cognitive Digital Twin and Cognitive Architecture for Human-CPS Collaboration_  
**Progetto:** AI4C2PS (ANR/FNR — Francia/Lussemburgo, University of Lorraine + LIST)

---

## Il Problema Centrale

La **semantic interoperability** (ontologie OWL, vocabolari condivisi) non è sufficiente quando umani e sistemi cyber-fisici devono _collaborare davvero_. Un operatore e un cobot possono parlare la stessa ontologia ma interpretare la stessa situazione in modo radicalmente diverso. Serve un livello superiore: la **cognitive interoperability**.

**Definizione ufficiale della tesi:**

> _"Cognitive Interoperability = la capacità di agenti diversi (umani o artificiali) di allineare pensieri e percezioni, costruire modelli mentali condivisi, e raggiungere mutua comprensione e intenzioni condivise per il decision-making congiunto."_

---

## I 4 Contributi Principali (C1–C4)

|ID|Contributo|Cosa risolve|
|---|---|---|
|**C1**|Formalizzazione di CCPS e CDT come entità cognitive|Definizione teorica rigorosa di cosa è un "sistema cognitivo" industriale |
|**C2**|Definizione formale di Cognitive Interoperability|Distingue semantic da cognitive interoperability, con criteri misurabili |
|**C3**|Modello di Maturità MMCI (5 livelli)|Strumento di assessment per misurare il grado di allineamento cognitivo |
|**C4**|Ontologia CDTO|Knowledge base strutturata per task, ruoli, vincoli, capabilities, affordances |

---

## Il Modello di Maturità MMCI

Scala progressiva da semantica a cognizione vera:

- **Level 0 — Semantic Interoperability**: ontologie condivise, mapping, significato consistente degli scambi
    
- **Level 1 — Shared Situation Awareness**: accordo su _cosa sta succedendo ora_ e previsione a breve termine
    
- **Level 2 — Shared Mental Models**: struttura del task condivisa (step, ruoli, vincoli causa-effetto)
    
- **Level 3 — Intent & Reasoning Alignment**: goal condivisi, spiegazioni delle decisioni, adattamento coerente
    
- **Level 4 — Joint Decision-Making + Metacognition**: decisioni congiunte con gestione esplicita di incertezza, confidence e delegazione adattiva
    

---

## L'Architettura CDT

Ogni **Cognitive Digital Twin** ha tre funzioni core:

```
Physical Entity (CPS/Human)
          │ sensor data (obs, cmd, state)
          ▼
┌─────────────────────────────────────┐
│           CDT                       │
│  ┌─────────────┐                    │
│  │  EMULATION  │ → stima stato      │
│  │             │   e azione corrente│
│  ├─────────────┤                    │
│  │  COGNITION  │ → CLARION          │
│  │             │   (reasoning + RL) │
│  ├─────────────┤                    │
│  │ SIMULATION  │ → Q-learning su    │
│  │             │   scenari futuri   │
│  └─────────────┘                    │
└─────────────────────────────────────┘
```

**Due modalità di coupling col fisico:**

- **Strong coupling**: il CDT controlla direttamente il CPS (lo trasforma in CCPS)
    
- **Weak coupling**: il CDT ragiona internamente e produce raccomandazioni/predizioni
    

---

## L'Architettura Cognitiva: CLARION

Scelta rispetto a SOAR, ACT-R, LIDA per il miglior bilanciamento tra explainability e adattamento. È ibrida neuro-simbolica con 4 subsystem:

|Subsystem|Ruolo nel CDT|Meccanismo chiave|
|---|---|---|
|**ACS** (Action-Centred)|Selezione azione real-time|Q-learning (IDN implicito) + regole simboliche (ARS esplicito) |
|**NACS** (Non-Action-Centred)|Ragionamento e memoria concettuale|Rule-based + similarity-based inference su GKS |
|**MS** (Motivational)|Goal management e reward signal|Drive primari/derivati → goal espliciti per ACS |
|**MCS** (Meta-Cognitive)|Supervisione dell'intero loop cognitivo|Regola learning rate, exploration/exploitation, filtra input |

**Dual-level learning** in ACS:

- _Bottom-up_: se un'azione ha successo → estrazione di regola esplicita (RER)
    
- _Top-down_: regole esplicite guidano il Q-learning implicito
    

---

## L'Ontologia CDTO

Stack modulare OWL:

`DUL (upper-level: oggetti, eventi, ruoli, contesto)
  └── SOMA (robotica: capabilities, task, tools, CPS)
       └── SSN/SOSA (sensori, osservazioni, attuatori)
            └── HUMO (human layer: cognitivo, fisico, stato)
            `

**Modello CAA (Capabilities, Abilities, Affordances):** cosa un agente _può fare_, _come lo fa_, e _in quale contesto è possibile_.

**Regole SWRL** per inferenza runtime: es. "se il robot ha la capability X e le precondizioni Y sono soddisfatte, allora può eseguire step Z".

**Statistiche SOMA module:** 675 classi, 266 object properties, 38 data properties, 357 OWL restrictions, 70 disjointness axioms.

---

## Use Case di Validazione

**Scenario:** Human-Robot Collaboration (HRC) su assemblaggio con cobot UR5e — operazione di avvitatura.

**Pipeline implementata:**

1. Stato del mondo ingerito via **NGSI-LD** nell'ontologia
    
2. Reasoner (HermiT) applica regole SWRL → inferisce feasibility delle azioni
    
3. **PyClarion** riceve features dall'ontologia, seleziona azione, aggiorna chunks/regole
    
4. Q-learning addestrato _separatamente in simulazione_ per la skill procedurale (avvitatura), poi policy riusata in execution
    

**Risultato:** il sistema con cognitive layer (CLARION + CDTO) raggiunge livelli MMCI più alti rispetto al baseline puramente semantico, in particolare su adattamento, anticipazione e joint decision-making.

---

## Limiti Dichiarati dall'Autore

- **Emulation function non implementata** — rimane come sviluppo futuro
    
- **Human Digital Twin (HDT) assente** — il lato umano non è un CDT a tutti gli effetti
    
- **Learning loop CLARION non pienamente integrato** — Q-learning validato solo in simulazione separata, non in loop chiuso con CDTO
    
- **MMCI non ancora validato empiricamente** con metriche quantitative definite per ogni livello
    
- **Use case singolo** (HRC assemblaggio) — generalizzazione richiede ri-design dell'ontologia
    

---

## Stack Tecnologico

|Layer|Tecnologia|
|---|---|
|Context broker|NGSI-LD (FIWARE standard) |
|Ontology dev|Protégé + HermiT reasoner |
|Reasoning rules|SWRL + SPARQL |
|Cognitive engine|PyClarion (Python) |
|Learning|Q-learning (Watkins & Dayan, 1992) |
|Robot|UR5e (Universal Robots) |
|Reference ontologies|DUL, SOMA, SSN/SOSA, HUMO |