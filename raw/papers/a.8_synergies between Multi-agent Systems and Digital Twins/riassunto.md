Ecco il tuo **cheat sheet da tenere in archivio** su questo paper.

---

# 📋 Scheda di Riferimento — Pretel et al., 2024

**Titolo:** _Analysing the Synergies between Multi-Agent Systems and Digital Twins — A Systematic Literature Review_  
**Pubblicato su:** _Information and Software Technology_, Vol. 174, 2024  
**Autori:** Elena Pretel, Alejandro Moya, Elena Navarro, Víctor López-Jaquero, Pascual González — Università di Castilla-La Mancha, Spagna

---

## 📌 Di cosa parla

È una **Systematic Literature Review (SLR)**: niente nuovo modello, niente codice. Analizza **64 paper** (filtrati da 220) per mappare lo stato dell'arte sull'integrazione tra **Digital Twins (DT)** e **Multi-Agent Systems (MAS)**. La tesi centrale è che DT e agenti MAS sono concettualmente equivalenti — entrambi rappresentano entità fisiche nel digitale, reagiscono all'ambiente e prendono decisioni — e quindi le proprietà dei MAS possono essere usate per costruire DT migliori.

---

## 🧱 Concetti chiave da ricordare

## Tre livelli di "Digital Twin"

|Tipo|Flusso dati|Bidirezionale?|
|---|---|---|
|Digital Model|Manuale|❌|
|Digital Shadow|PO → LO automatico|⚠️ Solo lettura|
|**True Digital Twin**|Automatico bidirezionale|✅ LO agisce sul PO|

La **maggior parte dei paper analizzati costruisce Digital Shadows, non veri DT**.

## Le 12 proprietà di un DT (Minerva et al.)

- **Essenziali (DT1–DT3):** Representativeness, Reflection, Entanglement — coperte da quasi tutti
    
- **Valore aggiunto (DT4–DT12):** Replication, Persistency, Memorization, Composability, Accountability, Augmentation, Ownership, Servitization, Predictability — pochissime coperte
    
- **DT6.Memorization** e **DT12.Predictability** sono le più comuni tra le value-adding
    
- **DT11.Servitization** non è supportata da nessun paper
    

## Le 4+8 proprietà degli Agenti/MAS

- **Agent-level:** Autonomy, Sociability, Reactivity, Proactivity
    
- **MAS-level:** Leadership, Decision Function, Heterogeneity, Agreement Parameters, Delay Consideration, Topology, Data Transmission Frequency, Mobility
    
- **Risultato:** Il 91.7% delle proprietà DT può essere coperto usando le proprietà MAS
    

---

## 🔢 Numeri utili

- Paper analizzati: **64** su 220 iniziali
    
- Dominio principale: **Manufacturing (39.1%)**, poi Precision Agriculture (12.5%), Energy (10.9%), Smart City (9.4%)
    
- Solo il **26.8%** dei paper dichiara il framework usato
    
- Solo il **37.5%** descrive come gestisce la conoscenza
    
- Tra chi la gestisce, il **26.6% usa ontologie**
    
- Framework citati: JADE, PADE, JADEX, JaCaMo, Python, Java
    

---

## 🔑 Trovate principali (Research Questions)

- **RQ1:** La maggior parte dei paper soddisfa solo le 3 proprietà essenziali DT1–DT3. Quasi nessuno implementa un vero DT bidirezionale — si fermano al Digital Shadow
    
- **RQ2:** Due pattern di integrazione: **MAS with DT** (l'agente usa il DT come sensore/knowledge base, 43 paper) e **MAS for DT** (il MAS costruisce l'architettura del DT, 21 paper)
    
- **RQ3:** La knowledge representation si basa quasi esclusivamente su **ontologie**. Nessun paper usa ontologie con modelli ML — gap enorme ancora aperto
    

---

## 🚀 Research Agenda (future work del settore)

1. Framework teorici per costruire DT con MAS
    
2. Sviluppare **veri DT bidirezionali**, non solo shadows
    
3. Sfruttare le proprietà MAS avanzate (Leadership, Agreement, Topology) ancora inesplorate
    
4. **Ontologie + ML** per DT — nessuno lo ha fatto ancora
    
5. Human Digital Twin (HDT) per healthcare e smart cities
    
6. Logistica globale e supply chain con DT+MAS
    

---

## ⚠️ Limiti da tenere a mente

- Ricerca corpus: solo fino a **febbraio 2023**
    
- Forte bias verso il **manufacturing**
    
- Nessuno standard di sviluppo emerso
    
- Nessun benchmark di performance tra le soluzioni