# Asymétrie institutionnelle - Acteur public vs acteur privé en OSINT
 
> **FR** - Fiche juridique : pourquoi une même pratique OSINT est licite pour un acteur public mandaté et risquée pour un acteur privé. Analyse des fondements légaux asymétriques.  
> **EN** - Legal fact sheet: why the same OSINT practice is lawful for a mandated public actor and risky for a private actor. Analysis of asymmetric legal foundations.
 
---
 
##  Principe / Core Principle
 
**FR** - La licéité d'une pratique OSINT ne dépend pas uniquement de la technique employée. Elle dépend également - et parfois principalement - du **statut de celui qui l'emploie**. Un même outil, une même méthode, un même objectif peuvent produire des qualifications juridiques radicalement différentes selon que l'acteur dispose ou non d'une base légale formelle, d'une supervision institutionnelle et d'une traçabilité encadrée.
 
**EN** - The legality of an OSINT practice does not depend solely on the technique used. It also depends - and sometimes primarily - on the **status of the actor using it**. The same tool, method, and objective can produce radically different legal qualifications depending on whether the actor has a formal legal basis, institutional supervision, and framed traceability.
 
---
 
##  Le cadre habilitant de l'acteur public / The Enabling Framework of Public Actors
 
### 1. L'enquête sous pseudonyme - Art. 230-46 CPP
 
**FR** - L'article 230-46 du Code de procédure pénale autorise les officiers ou agents de police judiciaire, ainsi que les agents des douanes habilités, à participer sous une identité d'emprunt à des échanges électroniques dans le cadre d'enquêtes portant sur des infractions commises par voie électronique ou dont la commission est facilitée par l'utilisation d'internet.
 
Les actes ainsi réalisés ne peuvent constituer une incitation à commettre des infractions.
 
**EN** - Article 230-46 of the Code of Criminal Procedure authorizes judicial police officers and agents, as well as authorized customs agents, to participate under a fictitious identity in electronic exchanges as part of investigations into offenses committed electronically or facilitated by internet use.
 
Acts performed in this manner cannot constitute incitement to commit offenses.
 
```
Conditions d'application :
├── Qualité d'OPJ/APJ ou agent habilité
├── Cadre d'une enquête préliminaire, de flagrance ou d'instruction
├── Infractions visées : celles commises par voie électronique
│   ou dont la commission est facilitée par l'utilisation d'internet
├── Pas d'incitation à commettre une infraction (interdiction de provocation)
└── Traçabilité et supervision judiciaire
```
 
>  **Ce que l'art. 230-46 permet à l'acteur public** - et que l'acteur privé ne peut pas faire sans risque pénal : créer un faux profil, infiltrer un espace numérique restreint, interagir sous une identité d'emprunt.
 
---
 
### 2. La LOPMI - Loi n° 2023-22 du 24 janvier 2023
 
**FR** - La loi d'orientation et de programmation du ministère de l'Intérieur du 24 janvier 2023 (LOPMI) a notamment renforcé les capacités numériques d'investigation des forces de l'ordre, en adaptant certains cadres procéduraux aux réalités des enquêtes en environnement numérique.
 
> Source : Loi n° 2023-22 du 24 janv. 2023, JORF n° 0021 du 25 janv. 2023.
 
---
 
### 3. Le contrôle du renseignement - CNCTR
 
**FR** - La Commission nationale de contrôle des techniques de renseignement (CNCTR) est l'autorité administrative indépendante chargée de s'assurer que les techniques de renseignement sont mises en œuvre dans le respect de la loi. Elle émet des avis préalables sur les demandes d'autorisation et contrôle a posteriori les conditions d'emploi des techniques autorisées.
 
Son rapport d'activité 2024 documente les observations formulées lors de ses contrôles et les recommandations adressées aux services.
 
> Source : CNCTR, Rapport d'activité 2024, 2025.  
 
---
 
### 4. La jurisprudence européenne sur les limites de l'OSINT régalien
 
#### CEDH, gde ch., Big Brother Watch et autres c. Royaume-Uni, 25 mai 2021
(req. n° 58170/13, 62322/14 et 24960/15)
 
**FR** - La Grande Chambre de la CEDH a jugé que le régime britannique de surveillance de masse présentait des insuffisances au regard de l'article 8 (droit au respect de la vie privée) et de l'article 10 (liberté d'expression) de la Convention. La Cour n'a pas interdit la surveillance numérique étatique en tant que telle, mais a posé des exigences précises :
 
**EN** - The ECHR Grand Chamber found that the UK's bulk interception regime presented deficiencies under Article 8 (right to private life) and Article 10 (freedom of expression) of the Convention. The Court did not prohibit state digital surveillance as such, but set precise requirements:
 
```
Exigences dégagées par la Cour (Big Brother Watch) :
│
├── Base légale accessible et prévisible
├── Supervision indépendante effective (avant et après l'opération)
├── Mécanisme de recours accessible aux personnes concernées
├── Critères objectifs de sélection des cibles
└── Pour les journalistes : autorisation judiciaire préalable spécifique
    lorsque la surveillance risque de compromettre la confidentialité des sources
```
 
>  **Ce que cet arrêt signifie pour l'OSINT** : même l'acteur public n'a pas carte blanche. La licéité de l'OSINT régalien dépend de l'existence effective de ces garanties - pas seulement de la qualité de l'agent.
 
---
 
#### CE, ass., French Data Network et autres, 21 avril 2021
(n° 393099, 394922, 397844, 397851)
 
**FR** - L'Assemblée du Conseil d'État a jugé que la conservation généralisée et indifférenciée des données de connexion par les fournisseurs d'accès, imposée par le droit français, était en principe incompatible avec le droit de l'Union européenne. Elle a toutefois admis des exceptions pour les besoins de la sécurité nationale, sous réserve d'un contrôle préalable par une autorité indépendante.
 
**EN** - The Council of State Assembly ruled that the general and indiscriminate retention of connection data by access providers, required by French law, was in principle incompatible with EU law. It nevertheless admitted exceptions for national security needs, subject to prior review by an independent authority.
 
> Source : CE, ass., 21 avr. 2021, French Data Network e.a., n° 393099.  
 
---
 
##  Le cadre (absent) de l'acteur privé / The (Absent) Framework of Private Actors
 
### Ce dont dispose l'acteur public - et pas l'acteur privé
 
| Élément | Acteur public mandaté | Acteur privé |
|---|---|---|
| Base légale formelle pour les faux profils |  Art. 230-46 CPP |  Absent |
| Supervision judiciaire ou indépendante |  Juge, CNCTR |  Absent |
| Traçabilité institutionnelle encadrée |  Procédure pénale |  Volontaire uniquement |
| Exceptions biométrie AI Act |  Art. 5 §2 à §5 |  Absent |
| Protection contre les poursuites pour recel |  Cadre de l'enquête |  Absent |
| Accès données plateformes (DSA art. 40) |  Partiel |  Chercheurs agréés uniquement |
 
---
 
### Les risques cumulatifs de l'acteur privé
 
**FR** - L'acteur privé pratiquant l'OSINT sans cadre institutionnel s'expose simultanément à trois types de risques que le droit commun ne lui permet pas d'écarter :
 
**EN** - The private actor practicing OSINT without an institutional framework is simultaneously exposed to three types of risks that common law does not allow to be avoided:
 
```
RISQUE PÉNAL
├── Art. 323-1 C. pén. - accès/maintien frauduleux (faux profil + espace restreint)
├── Art. 226-4-1 C. pén. - usurpation d'identité (si personne réelle imitée)
├── Art. 321-1 C. pén. - recel (exploitation de données issues d'une fuite)
└── Art. 226-1 C. pén. - atteinte à la vie privée
 
RISQUE CIVIL
├── Art. 9 C. civ. - atteinte à la vie privée
├── Art. 1240 C. civ. - responsabilité délictuelle
└── Violation des CGU → responsabilité contractuelle
 
RISQUE ADMINISTRATIF
├── RGPD - amende CNIL jusqu'à 20M€ ou 4% CA mondial
└── AI Act - sanctions pour pratiques interdites (art. 5)
```
 
---
 
### Le cas du sockpuppet - illustration de l'asymétrie
 
**FR** - Le sockpuppet (compte fictif utilisé pour accéder à des espaces ou interagir anonymement) illustre parfaitement l'asymétrie :
 
**EN** - The sockpuppet (fictitious account used to access spaces or interact anonymously) perfectly illustrates the asymmetry:
 
```
ACTEUR PUBLIC (OPJ sous art. 230-46 CPP)
└── Crée un faux profil
└── Infiltre un forum restreint
└── Interagit sous identité d'emprunt
→ Acte légal, encadré, traçable, supervisé
 
ACTEUR PRIVÉ (analyste OSINT indépendant)
└── Crée un faux profil → violation CGU → responsabilité civile
└── Infiltre un forum restreint → art. 323-1 C. pén. potentiel (Bluetouff)
└── Imite une personne réelle → art. 226-4-1 C. pén.
→ Cumul de risques sans base légale protectrice
```
 
---
 
##  Les dispositifs partiels existants / Existing Partial Frameworks
 
### Enquêteur privé - Art. L. 621-1 CSI
 
**FR** - Les activités privées de recherche et d'investigation sont encadrées par le Code de la sécurité intérieure (art. L. 621-1 et suivants) et soumises au contrôle du CNAPS (Conseil national des activités privées de sécurité). Ce cadre ne couvre cependant pas les journalistes, les chercheurs en cybersécurité ou les citoyens engagés dans une démarche d'investigation numérique.
 
> Source : C. sécurité intérieure, art. L. 621-1 et s.
 
---
 
### Lanceur d'alerte - Art. 122-9 C. pén. / Loi Waserman
 
**FR** - La loi n° 2022-401 du 21 mars 2022 (loi Waserman) a renforcé la protection des lanceurs d'alerte. L'article 122-9 du Code pénal exclut la responsabilité pénale du lanceur d'alerte qui divulgue des informations couvertes par un secret légal, à trois conditions cumulatives : nécessité, proportionnalité, respect des procédures définies.
 
Ce dispositif ne s'applique qu'aux personnes ayant eu connaissance des informations dans le cadre de leurs activités professionnelles. Il ne couvre pas l'analyste OSINT exploitant des sources ouvertes sans lien avec une organisation.
 
> Source : Loi n° 2022-401 du 21 mars 2022, JORF du 22 mars 2022.  
> Source : C. pén., art. 122-9.
 
---
 
### Accès chercheurs - DSA Art. 40
 
**FR** - L'article 40 du règlement (UE) 2022/2065 (DSA) prévoit un mécanisme d'accès aux données des très grandes plateformes pour les chercheurs agréés. Cet accès est conditionné à une demande motivée adressée au coordinateur des services numériques de l'État membre, qui vérifie la légitimité de la finalité de recherche.
 
Ce dispositif reste très sélectif et ne couvre pas la pratique OSINT générale.
 
> Source : Règlement (UE) 2022/2065, art. 40.
 
---
 
##  Références / References
 
- C. pr. pén., art. 230-46
- C. pén., art. 122-9, 226-4-1, 321-1, 323-1
- C. sécurité intérieure, art. L. 621-1 et s.
- Conv. EDH, art. 8 et 10
- Loi n° 2023-22 du 24 janv. 2023 (LOPMI), JORF du 25 janv. 2023
- Loi n° 2022-401 du 21 mars 2022 (Waserman), JORF du 22 mars 2022
- Règlement (UE) 2022/2065 (DSA), art. 40
- Règlement (UE) 2024/1689 (AI Act), art. 5 §2 à §5
- CEDH, gde ch., 25 mai 2021, Big Brother Watch, req. n° 58170/13, 62322/14 et 24960/15
- CE, ass., 21 avr. 2021, French Data Network, n° 393099
- CNCTR, Rapport d'activité 2024
 
---
