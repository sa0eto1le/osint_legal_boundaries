> **FR** — Cadre juridique et technique pour une pratique OSINT conforme au droit français et européen  
> **EN** — Legal and technical framework for OSINT practices compliant with French and European law

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![RGPD Compliant](https://img.shields.io/badge/RGPD-Aware-blue)](legal-framework/rgpd-osint.md)
[![Lang: FR/EN](https://img.shields.io/badge/Lang-FR%2FEN-lightgrey)]()

---

##  Disclaimer / Avertissement

> **FR** — Ce repository est un outil pédagogique et de recherche. Les exemples techniques sont fournis à des fins d'illustration uniquement. L'auteur ne saurait être tenu responsable d'un usage non conforme au droit applicable.  
> **EN** — This repository is an educational and research tool. Technical examples are provided for illustration purposes only. The author cannot be held responsible for any use that does not comply with applicable law.

---

##  À propos / About

**FR**  
En pratiquant l'OSINT, on se heurte vite à une question inconfortable : jusqu'où peut-on aller légalement ? La réponse évidente — "si c'est public, c'est utilisable" — est fausse. Ce projet est né de cette tension entre ce que la technique permet et ce que le droit autorise.

**La thèse centrale : accessibilité technique ≠ disponibilité juridique.** Une information visible en ligne n'est pas nécessairement libre d'usage. Les conditions de collecte, la nature du traitement et le statut de l'acteur changent tout.

Ce repo compile des ressources concrètes pour naviguer dans cette zone grise : fiches juridiques, exemples techniques commentés, checklists terrain et analyses de cas réels.

**EN**  
When practicing OSINT, you quickly run into an uncomfortable question: how far can you legally go? The obvious answer — "if it's public, it's usable" — is wrong. This project was born from the tension between what technology enables and what the law allows.

**The central argument: technical accessibility ≠ legal availability.** Information visible online is not necessarily free to use. Collection conditions, processing nature, and the actor's status change everything.

This repo compiles concrete resources to navigate this grey area: legal fact sheets, commented technical examples, field checklists, and real case analyses.

---

##  Structure

```
osint_legal_boundaries/
│
├── README.md
│
├── legal-framework/           # Fiches juridiques / Legal fact sheets
│   ├── rgpd-osint.md          # RGPD appliqué à l'OSINT
│   ├── article-323-1.md       # Accès et maintien frauduleux (STAD)
│   ├── ai-act-biometrie.md    # AI Act & reconnaissance faciale
│   ├── recel-fuites.md        # Recel et analyse de fuites de données
│   └── asymetrie-acteurs.md   # Acteur public vs acteur privé
│
├── tools-and-limits/          # Outils + cadre légal associé
│   ├── dorking.md             # Google Dorking — exemples & limites
│   ├── port-scanning.md       # Nmap, Shodan — technique & risques
│   ├── idor.md                # Failles IDOR — détection & qualification
│   └── scraping.md            # Web scraping — conformité RGPD
│
├── checklists/                # Outils terrain / Field tools
│   ├── osint-compliance.md    # Checklist OSINT avant enquête
│   └── preuve-numerique.md    # Checklist recueil de preuve numérique
│
└── case-studies/              # Analyses de cas / Case analyses
    ├── bluetouff.md           # Cass. crim. 20 mai 2015
    ├── clearview-ai.md        # CNIL / EDPB — 2022
    └── kaspr.md               # CNIL — déc. 2024
```

---

##  Cadre juridique clé / Key Legal Framework

| Texte / Text | Portée / Scope | Impact OSINT |
|---|---|---|
| RGPD (2016/679) | Tout traitement de données personnelles | Finalité, minimisation, base légale obligatoires |
| Art. 323-1 C. pén. | Accès/maintien frauduleux dans un STAD | S'applique même sans effraction technique |
| AI Act (2024/1689) | IA à haut risque, biométrie | Interdit le scraping facial massif aux acteurs privés |
| DSA (2022/2065) | Grandes plateformes | Accès chercheurs agréés uniquement (art. 40) |
| Loi Godfrain (1988) | Fraude informatique | Fondement historique de l'art. 323-1 |

---

##  Tools & Limits — Exemples complets

### 1. Google Dorking

**FR** — Le dorking utilise des opérateurs de recherche avancée pour révéler des contenus non destinés à l'exposition publique.  
**EN** — Dorking uses advanced search operators to surface content not intended for public exposure.

```bash
# Trouver des fichiers Excel contenant des mots de passe sur un domaine
filetype:xls site:exemple.com "password"

# Trouver des répertoires exposés
intitle:"index of" site:exemple.com

# Trouver des fichiers de configuration exposés
filetype:env "DB_PASSWORD" site:exemple.com
```

**Output typique / Typical output :**
```
exemple.com/backup/config.xls        ← fichier exposé par inadvertance
exemple.com/admin/                   ← répertoire listé sans protection
exemple.com/.env                     ← credentials en clair
```

>  **Qualification juridique FR** — Le dorking n'implique aucune intrusion technique. Cependant, dès que l'enquêteur perçoit un signal de restriction (robots.txt, accès normalement protégé, contenu manifestement interne) et poursuit sa consultation, il entre dans le champ du **maintien frauduleux** au sens de l'art. 323-1 C. pén. (*Cass. crim., 20 mai 2015, Bluetouff*).

>  **Legal qualification EN** — Dorking involves no technical intrusion. However, once the investigator perceives a restriction signal and continues, this may constitute **unauthorized persistence** within a computer system under art. 323-1 French Penal Code (*Bluetouff, 2015*).

---

### 2. Port Scanning (Nmap / Shodan)

**FR** — Le balayage de ports permet d'identifier les services exposés sur un système.  
**EN** — Port scanning identifies services exposed on a target system.

```bash
# Scan basique des ports les plus courants
nmap -sV -p 22,80,443,8080 cible.exemple.com

# Scan avec détection d'OS et de version
nmap -A -T4 cible.exemple.com

# Reconnaissance passive via Shodan (sans contact direct avec la cible)
shodan host <IP_ADDRESS>
```

**Output typique / Typical output :**
```
PORT     STATE  SERVICE    VERSION
22/tcp   open   ssh        OpenSSH 8.2p1
80/tcp   open   http       nginx 1.18.0
443/tcp  open   https      nginx 1.18.0
3306/tcp open   mysql      MySQL 5.7.32    ← base de données exposée
8080/tcp open   http       Apache Tomcat   ← interface d'admin accessible
```

>  **Qualification juridique FR** — La distinction reconnaissance **passive** (Shodan, données déjà indexées) / reconnaissance **active** (Nmap, paquets envoyés vers la cible) est juridiquement déterminante. Un scan actif sans mandat sur un système tiers peut être qualifié d'accès frauduleux. L'absence de protection technique ne neutralise pas l'infraction si l'intention de restriction du maître du système est manifeste.

>  **Legal qualification EN** — The **passive** (Shodan) vs **active** (Nmap) distinction is legally critical. Active scanning without authorization may constitute unauthorized access. The absence of technical protection does not neutralize the offense if the system owner's intent to restrict access is evident.

---

### 3. Faille IDOR (Insecure Direct Object Reference)

**FR** — Une faille IDOR permet d'accéder à des ressources en manipulant des identifiants dans une requête, sans exploitation technique complexe.  
**EN** — An IDOR vulnerability allows access to resources by manipulating identifiers in a request, without complex technical exploitation.

```
# URL originale (accès légitime)
GET https://exemple.com/facture?id=1234

# Manipulation IDOR
GET https://exemple.com/facture?id=1235    ← facture d'un autre utilisateur
GET https://exemple.com/facture?id=1236    ← itération = aggravation potentielle
```

**Output typique / Typical output :**
```json
{
  "id": 1235,
  "client": "Dupont SA",
  "montant": 4800,
  "iban": "FR76 XXXX XXXX XXXX"    ← données personnelles et financières
}
```

>  **Qualification juridique FR** — Accéder à `id=1235` constitue potentiellement un accès non autorisé à un STAD dès la première occurrence, a fortiori si l'accès est répété ou automatisé. La qualification pénale ne dépend pas de la sophistication de la méthode mais de la conscience d'avoir franchi une limite (art. 323-1 C. pén.).

>  **Legal qualification EN** — Accessing `id=1235` potentially constitutes unauthorized access from the first instance, especially if repeated or automated. Criminal qualification does not depend on technical sophistication but on awareness of crossing a boundary (art. 323-1 French Penal Code).

---

##  Checklist OSINT — Avant toute enquête / Before any investigation

```markdown
###  Checklist OSINT-Compliant

DÉFINITION DE LA MISSION / MISSION DEFINITION
[ ] Finalité définie et documentée avant le début de la collecte
[ ] Périmètre limité aux données strictement nécessaires (minimisation)
[ ] Base légale identifiée (intérêt légitime / mission légale / consentement)

SIGNAUX DE RESTRICTION / RESTRICTION SIGNALS
[ ] Vérification du fichier robots.txt sur les domaines concernés
[ ] Identification des mesures anti-bot (CAPTCHA, rate limiting, tokens)
[ ] Vérification des CGU des plateformes ciblées
[ ] Aucune zone manifestement restreinte ou protégée accédée

TRAÇABILITÉ / TRACEABILITY
[ ] Date et heure d'accès horodatées pour chaque source
[ ] URL d'origine archivée (ex : archive.org ou archive local)
[ ] Méthode de collecte documentée (manuelle / automatisée / outil utilisé)
[ ] Captures d'écran conservées avec métadonnées intactes

DONNÉES SENSIBLES / SENSITIVE DATA
[ ] Aucune donnée biométrique traitée sans base légale art. 9 RGPD
[ ] Aucun profil de personne physique constitué sans nécessité démontrée
[ ] Évaluation de l'impact vie privée si données agrégées

APRÈS ENQUÊTE / POST-INVESTIGATION
[ ] Données inutiles supprimées (principe de minimisation)
[ ] Rapport de traçabilité conservé
[ ] Vulnérabilité détectée → signalement responsable envisagé
```

---

##  Asymétrie institutionnelle / Institutional Asymmetry

**FR** — Un même outil, des régimes juridiques radicalement différents selon l'acteur.  
**EN** — Same tool, radically different legal regimes depending on the actor.

| Pratique | Acteur public mandaté | Acteur privé |
|---|---|---|
| Faux profil / sockpuppet | ✅ Art. 230-46 CPP | ⚠️ Art. 226-4-1 / 323-1 C. pén. |
| Scraping de données semi-publiques | ✅ Cadre réglementaire spécifique | ⚠️ RGPD + CGU + responsabilité civile |
| Reconnaissance faciale biométrique | ✅ Exceptions AI Act (art. 5 §2-5) | ❌ Interdit pour acteurs privés non habilités |
| Analyse de fuites de données | ✅ Dans le cadre de l'enquête | ⚠️ Risque de recel (art. 321-1 C. pén.) |
| Port scanning actif | ✅ Avec mandat / qualification PASSI | ⚠️ Zone grise — art. 323-1 potentiel |

---

##  Case Studies

###  Bluetouff — Cass. crim., 20 mai 2015

**FR** — Un individu accède via Google à des documents internes exposés par inadvertance. Sans outil de piratage, il navigue et télécharge des fichiers. La Cour retient le **maintien frauduleux dans un STAD** : c'est la conscience de la restriction, et non l'effraction technique, qui fonde la qualification.

**EN** — An individual accessed internal documents via Google that were inadvertently exposed. Without hacking tools, he browsed and downloaded files. The Court upheld **unauthorized persistence in a computer system**: awareness of the restriction — not technical intrusion — establishes the offense.

>  Repérer un signal de restriction = point de bascule. Poursuivre = risque pénal réel.

---

###  Clearview AI — CNIL/EDPB, 2022

**FR** — Clearview AI constitue une base de milliards d'empreintes faciales par scraping massif de photos publiques. Sanction CNIL : 20M€. Motifs : absence de base légale, violation de l'art. 9 RGPD, non-respect des droits des personnes.

**EN** — Clearview AI built a database of billions of facial embeddings by massively scraping public photos. CNIL fine: €20M. Grounds: no legal basis, GDPR art. 9 violation, failure to respect data subjects' rights.

>  La publicité d'une image ne vaut pas autorisation de traitement biométrique.

---

###  KASPR — CNIL, 5 déc. 2024

**FR** — Kaspr collecte via LinkedIn des coordonnées dont la visibilité avait été restreinte par les utilisateurs. Amende : 240 000€. La visibilité partielle n'équivaut pas à un consentement de collecte par des tiers.

**EN** — Kaspr collected contact details from LinkedIn where users had restricted visibility. Fine: €240,000. Partial visibility does not equate to consent for third-party collection.

>  Les attentes raisonnables de la personne concernée comptent, même pour des données techniquement accessibles.

---

##  Références / References

- CNIL (LINC), *Le renseignement en sources ouvertes*, 5 févr. 2024
- CNIL, *Fiche focus — Intérêt légitime et web scraping*, 19 juin 2025
- ANSSI, CyberDico — entrées STAD, port scanning, deep web
- OWASP Top 10 — A01:2021 Broken Access Control
- IETF, RFC 9309 — Robots Exclusion Protocol
- Règlement (UE) 2016/679 — RGPD
- Règlement (UE) 2024/1689 — AI Act
- Règlement (UE) 2022/2065 — DSA

---

##  Auteur / Author

**sa0**  
Cybersécurité offensive · OSINT · Droit du numérique

---

*Ce repository est un projet personnel à vocation pédagogique. Il ne constitue pas un conseil juridique.*  
*This repository is a personal educational project. It does not constitute legal advice.*
