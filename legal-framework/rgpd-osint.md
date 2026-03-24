# RGPD & OSINT - Le règlement général sur la protection des données appliqué aux sources ouvertes
 
> **FR** - Fiche juridique : application du RGPD aux pratiques de collecte et de traitement de données dans le cadre de l'OSINT.  
> **EN** - Legal fact sheet: application of the GDPR to data collection and processing practices in the context of OSINT.
 
---
 
##  Principe fondamental / Core Principle
 
**FR** - Le RGPD ne raisonne pas en termes de visibilité. Il raisonne en termes de **traitement**. Dès lors qu'une donnée concerne une personne identifiée ou identifiable et qu'elle fait l'objet d'une collecte, d'un croisement, d'un stockage ou d'une diffusion - les règles s'appliquent. Peu importe que la donnée soit publique, accessible librement ou indexée par un moteur de recherche.
 
**EN** - The GDPR does not reason in terms of visibility. It reasons in terms of **processing**. As soon as data relates to an identified or identifiable person and is collected, cross-referenced, stored, or shared - the rules apply. It does not matter whether the data is public, freely accessible, or indexed by a search engine.
 
>  **Accessibilité technique ≠ autorisation juridique de traitement.**
 
---
 
##  Les 5 principes clés pour l'OSINT / The 5 Key Principles for OSINT
 
### 1. Finalité - Art. 5 §1 b)
 
**FR** - Les données doivent être collectées pour des **finalités déterminées, explicites et légitimes**. Elles ne peuvent pas être réutilisées de manière incompatible avec ces finalités.
 
En OSINT, ce principe est structurellement difficile à respecter : on collecte souvent "au cas où", sans finalité précise définie en amont. C'est exactement là que le risque commence.
 
**EN** - Data must be collected for **specified, explicit and legitimate purposes**. It cannot be reused in a way incompatible with those purposes.
 
In OSINT, this principle is structurally difficult to comply with: collection often happens "just in case", without a precise purpose defined upfront. That is exactly where the risk begins.
 
```
 Collecter toutes les données disponibles sur une personne sans objectif défini
 Définir la finalité avant de commencer la collecte et s'y tenir strictement
```
 
---
 
### 2. Minimisation - Art. 5 §1 c)
 
**FR** - Les données collectées doivent être **adéquates, pertinentes et limitées** à ce qui est nécessaire au regard de la finalité. L'automatisation pousse à tout collecter - le RGPD impose de ne prendre que ce qui est strictement utile.
 
**EN** - Collected data must be **adequate, relevant and limited** to what is necessary for the purpose. Automation pushes toward collecting everything - the GDPR requires taking only what is strictly useful.
 
```
 Scraper l'intégralité du profil d'une personne alors que seul son poste est pertinent
 Limiter la collecte aux données directement nécessaires à la mission définie
```
 
---
 
### 3. Licéité - Art. 6
 
**FR** - Tout traitement doit reposer sur une **base légale**. En OSINT, les bases légales les plus couramment invoquées sont :
 
| Base légale | Conditions | Usage OSINT typique |
|---|---|---|
| **Intérêt légitime** (art. 6 §1 f) | Mise en balance avec les droits de la personne | Veille concurrentielle, due diligence |
| **Mission d'intérêt public** (art. 6 §1 e) | Réservé aux autorités publiques ou missions déléguées | OSINT régalien, recherche académique |
| **Obligation légale** (art. 6 §1 c) | Texte légal imposant le traitement | Conformité réglementaire |
| **Consentement** (art. 6 §1 a) | Libre, éclairé, spécifique, révocable | Rarement applicable en OSINT |
 
**EN** - Every processing operation must rest on a **legal basis**. In OSINT, the most commonly invoked bases are shown in the table above.
 
>  **L'intérêt légitime n'est pas une clause blanche.** Il impose une mise en balance documentée entre l'intérêt poursuivi et les droits de la personne concernée. La CNIL a précisé en juin 2025 que cette mise en balance doit être explicite et traçable, y compris pour le scraping.
 
---
 
### 4. Transparence - Art. 14
 
**FR** - Lorsque les données n'ont pas été collectées directement auprès de la personne concernée (ce qui est toujours le cas en OSINT), une **obligation d'information** s'applique en principe. La personne doit être informée de l'existence du traitement, de sa finalité, de sa durée de conservation et de ses droits.
 
Cette obligation n'est pas absolue : des exceptions existent, mais elles sont **strictement encadrées** et doivent être justifiées au cas par cas.
 
**EN** - When data was not collected directly from the data subject (which is always the case in OSINT), an **information obligation** applies in principle. The person must be informed of the processing, its purpose, retention period, and their rights.
 
This obligation is not absolute: exceptions exist, but they are **strictly framed** and must be justified on a case-by-case basis.
 
```
Exceptions applicables (art. 14 §5 RGPD) :
├── Information impossible ou effort disproportionné
├── Obligation légale de confidentialité
└── Finalité de recherche, statistique ou archivage d'intérêt public
        → Conditions cumulatives + garanties appropriées requises
```
 
---
 
### 5. Durée de conservation - Art. 5 §1 e)
 
**FR** - Les données ne peuvent être conservées que le temps **strictement nécessaire** à la finalité pour laquelle elles ont été collectées. Conserver indéfiniment des données collectées en OSINT, même légitimement, constitue une violation du RGPD.
 
**EN** - Data may only be retained for as long as **strictly necessary** for the purpose for which it was collected. Retaining OSINT-collected data indefinitely, even legitimately, constitutes a GDPR violation.
 
---
 
##  Données sensibles - Art. 9
 
**FR** - Certaines catégories de données bénéficient d'une protection renforcée. Leur traitement est **interdit par principe**, sauf exceptions limitativement prévues.
 
**EN** - Certain categories of data benefit from enhanced protection. Their processing is **prohibited in principle**, except for strictly limited exceptions.
 
| Catégorie | Exemples OSINT | Risque |
|---|---|---|
| Opinions politiques | Posts militants, associations |  Interdit sans base légale spécifique |
| Convictions religieuses | Profils, lieux de culte fréquentés |  Interdit sans base légale spécifique |
| Données biométriques | Reconnaissance faciale, embeddings |  Interdit - voir [ai-act-biometrie.md](ai-act-biometrie.md) |
| Données de santé | Mentions de pathologies en ligne |  Interdit sans base légale spécifique |
| Orientation sexuelle | Profils, publications |  Interdit sans base légale spécifique |
 
>  **Une donnée sensible reste sensible même si elle est publiquement accessible.** Le fait qu'une personne ait mentionné sa religion sur un réseau social ne constitue pas une autorisation de traitement.
 
---
 
##  Décisions CNIL illustratives / Illustrative CNIL Decisions
 
### Clearview AI - 2022
 
**FR** - Clearview AI scrape massivement des photos publiques pour constituer une base de reconnaissance faciale. Sanction : **20M€**. La CNIL retient l'absence de base légale, la violation de l'art. 9 et le non-respect des droits des personnes. La publicité des photos ne vaut pas autorisation de traitement biométrique.
 
**EN** - Clearview AI massively scraped public photos to build a facial recognition database. Fine: **€20M**. The CNIL found no legal basis, violation of art. 9, and failure to respect data subjects' rights. The public nature of photos does not authorize biometric processing.
 
---
 
### KASPR - 5 décembre 2024
 
**FR** - Kaspr collecte via LinkedIn des coordonnées dont les utilisateurs avaient restreint la visibilité à leurs connexions. Sanction : **240 000€**. La CNIL rappelle que les attentes raisonnables de confidentialité des personnes concernées s'imposent, même pour des données techniquement accessibles à certains cercles.
 
**EN** - Kaspr collected contact details from LinkedIn where users had restricted visibility to their connections. Fine: **€240,000**. The CNIL emphasized that the reasonable confidentiality expectations of data subjects apply, even for data technically accessible to certain circles.
 
---
 
##  Intérêt légitime et scraping - CNIL, juin 2025
 
**FR** - La CNIL a publié en juin 2025 une fiche focus sur le scraping et la base légale de l'intérêt légitime. Les conditions cumulatives pour qu'un scraping soit conforme :
 
**EN** - The CNIL published in June 2025 a focus note on scraping and the legitimate interest legal basis. Cumulative conditions for compliant scraping:
 
```
CONDITIONS CUMULATIVES / CUMULATIVE CONDITIONS
 
1. FINALITÉ LÉGITIME
   └── Objectif réel, documenté, non contraire à la loi
 
2. NÉCESSITÉ
   └── Le scraping est le seul moyen d'atteindre cet objectif
 
3. MISE EN BALANCE
   └── L'intérêt poursuivi l'emporte sur les droits des personnes
   └── Mise en balance documentée et traçable
 
4. RESPECT DES SIGNAUX D'OPPOSITION
   └── robots.txt pris en compte
   └── Mesures anti-bot respectées
   └── Mécanismes d'opposition des personnes honorés
 
5. GARANTIES
   └── Filtrage en amont avant conservation
   └── Durée de conservation limitée
   └── Sécurité des données collectées assurée
```
 
---
 
##  Checklist RGPD pour une collecte OSINT / GDPR Checklist for OSINT Collection
 
```markdown
AVANT LA COLLECTE / BEFORE COLLECTION
[ ] Finalité définie, documentée, légitime
[ ] Base légale identifiée et justifiée
[ ] Données sensibles (art. 9) identifiées et exclues si pas de base légale
[ ] Périmètre de collecte limité au strict nécessaire
 
PENDANT LA COLLECTE / DURING COLLECTION
[ ] robots.txt vérifié sur les domaines concernés
[ ] Mesures anti-bot respectées (pas de contournement)
[ ] CGU des plateformes vérifiées
[ ] Traçabilité des sources maintenue
 
APRÈS LA COLLECTE / AFTER COLLECTION
[ ] Données inutiles supprimées immédiatement
[ ] Durée de conservation définie et respectée
[ ] Obligation d'information art. 14 évaluée
[ ] Mise en balance documentée si base = intérêt légitime
[ ] Sécurité des données stockées assurée
```
 
---
 
##  Références / References
 
- Règlement (UE) 2016/679 - RGPD, art. 5, 6, 9, 14
- CNIL (LINC), *Le renseignement en sources ouvertes*, 5 févr. 2024
- CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025
- CNIL, délibération KASPR, 5 déc. 2024
- EDPB, *Report of the work undertaken by the ChatGPT Taskforce*, 23 mai 2024
- EDPB, *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022
 
---
