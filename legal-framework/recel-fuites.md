# Recel & Fuites de données - Art. 321-1 C. pén. appliqué à l'OSINT
 
> **FR** - Fiche juridique : qualification de recel appliquée à l'exploitation de données issues de fuites, et tensions avec la liberté d'expression en contexte OSINT.  
> **EN** - Legal fact sheet: handling stolen goods qualification applied to leaked data exploitation, and tensions with freedom of expression in OSINT contexts.
 
---
 
##  Texte de loi / Statutory Text
 
```
Article 321-1 du Code pénal
 
Le recel est le fait de dissimuler, de détenir ou de transmettre une chose, ou de faire 
office d'intermédiaire afin de la transmettre, en sachant que cette chose provient d'un 
crime ou d'un délit.
 
Constitue également un recel le fait, en connaissance de cause, de bénéficier, par tout 
moyen, du produit d'un crime ou d'un délit.
 
Le recel est puni de cinq ans d'emprisonnement et de 375 000 euros d'amende.
```
 
```
Article 321-2 du Code pénal (recel aggravé)
 
Le recel est puni de dix ans d'emprisonnement et de 750 000 euros d'amende :
1° Lorsqu'il est commis de façon habituelle ou en utilisant les facilités que procure 
   l'exercice d'une activité professionnelle ;
2° Lorsqu'il est commis en bande organisée.
```
 
---
 
##  Éléments constitutifs / Elements of the Offense
 
### 1. L'infraction préalable
 
**FR** - Le recel est une **infraction de conséquence** : il suppose l'existence d'un crime ou d'un délit préalable dont provient la chose recelée. En matière de fuites de données, l'infraction préalable est généralement :
 
**EN** - Handling stolen goods is a **consequential offense**: it requires a prior crime or offense from which the thing originates. In data leak contexts, the prior offense is typically:
 
```
Infractions préalables fréquentes en contexte de fuite de données :
├── Accès frauduleux à un STAD (art. 323-1 C. pén.)
├── Extraction frauduleuse de données (art. 323-3 C. pén.)
├── Vol de données (débat doctrinal persistant sur la qualification)
└── Atteinte au secret des correspondances (art. 226-15 C. pén.)
```
 
---
 
### 2. La connaissance de l'origine illicite
 
**FR** - L'élément moral du recel est **la connaissance** de l'origine illicite de la chose. Il n'est pas nécessaire de connaître précisément l'infraction préalable - il suffit d'avoir conscience que la chose provient d'un crime ou d'un délit.
 
En pratique OSINT, cette connaissance peut résulter de :
 
**EN** - The mental element of handling stolen goods is **knowledge** of the illicit origin. It is not necessary to know the exact prior offense - awareness that the thing originates from a crime or offense suffices.
 
In OSINT practice, this knowledge may result from:
 
```
Indices de connaissance de l'origine illicite :
├── La donnée est publiée sur un forum spécialisé dans les fuites (BreachForums, etc.)
├── Le volume et la nature des données sont incompatibles avec une divulgation légale
├── La fuite est médiatisée et son origine illicite est publiquement connue
├── Les données contiennent des informations manifestement confidentielles
│   (credentials, données bancaires, dossiers médicaux, etc.)
└── Le fichier est explicitement présenté comme issu d'un accès non autorisé
```
 
---
 
### 3. L'acte de recel
 
**FR** - Deux formes distinctes sont incriminées :
 
**EN** - Two distinct forms are criminalized:
 
```
RECEL-DÉTENTION                          RECEL-PROFIT
├── Dissimuler                           ├── Bénéficier du produit
├── Détenir                              └── En connaissance de cause
└── Transmettre / servir d'intermédiaire
```
 
>  **Le simple fait de consulter, télécharger ou stocker des données issues d'une fuite connue peut constituer un acte de recel-détention**, même en l'absence d'intention de nuire ou de profit.
 
---
 
##  Application à l'OSINT / Application to OSINT
 
### Scénarios concrets / Concrete Scenarios
 
| Situation | Qualification potentielle |
|---|---|
| Consulter une fuite publiée sur BreachForums pour vérifier une information |  Recel-détention si téléchargement |
| Télécharger une base de données fuité pour analyser son contenu |  Recel-détention probable |
| Croiser des données d'une fuite avec des sources publiques |  Recel + traitement sans base légale RGPD |
| Publier des informations issues d'une fuite sans les télécharger |  Recel-profit si bénéfice indirect (audience, notoriété) |
| Signaler l'existence d'une fuite sans accéder aux données |  Pas de recel a priori |
| Vérifier si une adresse email figure dans une fuite via HaveIBeenPwned |  Service tiers - pas d'accès direct aux données brutes |
 
---
 
### Le problème structurel pour l'OSINT
 
**FR** - L'infraction de recel présente une caractéristique qui la rend particulièrement contraignante en OSINT : elle est **aveugle à l'intention morale**. Que l'analyste cherche à nuire, à s'enrichir, ou au contraire à alerter sur une vulnérabilité, à documenter une fuite pour protéger des victimes, ou à produire un reportage d'intérêt public - si la connaissance de l'origine illicite est établie et que l'acte de détention ou d'exploitation est caractérisé, l'infraction est constituée.
 
**EN** - The handling offense has a characteristic that makes it particularly constraining in OSINT: it is **blind to moral intent**. Whether the analyst seeks to harm, profit, or conversely to alert about a vulnerability, document a leak to protect victims, or produce public interest journalism - if knowledge of illicit origin is established and the act of possession or exploitation is characterized, the offense is established.
 
---
 
##  Tension avec la liberté d'expression / Tension with Freedom of Expression
 
### CEDH, Guja c. Moldova, 12 février 2008 (req. n° 14277/04)
 
**FR** - La Cour européenne des droits de l'homme a précisé dans cet arrêt que la divulgation d'informations confidentielles peut relever de la **liberté d'expression protégée par l'article 10 de la Convention** lorsqu'elle répond à certaines conditions. La Cour a dégagé une grille d'évaluation reposant notamment sur :
 
**EN** - The European Court of Human Rights clarified in this ruling that disclosure of confidential information may fall under **freedom of expression protected by Article 10 of the Convention** when certain conditions are met. The Court established an evaluation framework based notably on:
 
```
Critères dégagés par la Cour (Guja c. Moldova) :
│
├── 1. Existence d'un intérêt public réel dans l'information divulguée
│
├── 2. Authenticité de l'information (pas de fabrication ou falsification)
│
├── 3. Bonne foi de l'auteur de la divulgation
│
├── 4. Absence d'autre voie pour porter l'information à la connaissance du public
│
├── 5. Préjudice causé à l'autorité concernée vs intérêt du public à être informé
│       → Mise en balance proportionnalité
│
└── 6. Sévérité de la sanction infligée à l'auteur de la divulgation
```
 
>  **Important** : cet arrêt concernait un fonctionnaire divulguant des documents internes à la presse. Il ne constitue **pas une immunité générale** pour les analystes OSINT exploitant des données issues de fuites. Il dessine une grille d'évaluation que le juge peut prendre en compte - pas une exonération automatique.
 
---
 
### Cass. ass. plén., 22 décembre 2023 (n° 20-20.648 et n° 21-11.330)
 
**FR** - L'assemblée plénière de la Cour de cassation a opéré un **revirement de jurisprudence** en matière civile sur la recevabilité des preuves obtenues de manière déloyale. La Cour rejette désormais l'exclusion automatique et impose au juge de mettre en balance :
 
**EN** - The plenary assembly of the Court of Cassation operated a **reversal of case law** in civil matters regarding the admissibility of disloyally obtained evidence. The Court now rejects automatic exclusion and requires the judge to balance:
 
```
Critères de mise en balance (Cass. ass. plén., 22 déc. 2023) :
├── Le droit à la preuve
├── Les droits antinomiques en présence (vie privée, confidentialité, etc.)
├── La preuve doit être indispensable à l'exercice de ce droit
└── L'atteinte doit être strictement proportionnée au but poursuivi
```
 
>  **Impact OSINT** : ce revirement ne concerne que la matière civile. En matière pénale, l'art. 427 CPP n'a jamais consacré d'irrecevabilité automatique. Mais la logique de proportionnalité in concreto se rapproche des deux ordres. Une preuve issue d'une fuite utilisée dans un contexte OSINT sera évaluée au regard de sa nécessité et de la proportionnalité de l'atteinte - pas automatiquement écartée, mais pas automatiquement admise.
 
---
 
##  Bonnes pratiques pour limiter le risque / Best Practices to Limit Risk
 
```markdown
AVANT D'ACCÉDER À DES DONNÉES POTENTIELLEMENT ISSUES D'UNE FUITE
[ ] Ne pas télécharger les données brutes - consulter uniquement via des services
    tiers agréés si possible (ex : HaveIBeenPwned pour les emails)
[ ] Documenter la finalité légitime de la consultation
[ ] Évaluer si l'origine illicite est connue ou manifeste
 
SI L'ACCÈS EST NÉCESSAIRE
[ ] Limiter strictement au minimum indispensable à la finalité
[ ] Ne pas stocker les données au-delà du strict nécessaire
[ ] Ne pas croiser avec d'autres sources sans base légale RGPD
[ ] Documenter chaque étape (date, source, méthode, finalité)
 
PUBLICATION / DIFFUSION
[ ] Évaluer l'intérêt public réel de l'information
[ ] Ne publier que ce qui est strictement nécessaire à cet intérêt
[ ] Anonymiser ou pseudonymiser autant que possible
[ ] Conserver la traçabilité complète de la démarche
```
 
---
 
##  Échelle des peines / Sentencing Scale
 
| Infraction | Peine maximale |
|---|---|
| Recel simple (art. 321-1) | 5 ans · 375 000 € |
| Recel habituel ou professionnel (art. 321-2 1°) | 10 ans · 750 000 € |
| Recel en bande organisée (art. 321-2 2°) | 10 ans · 750 000 € |
 
---
 
##  Références / References
 
- C. pén., art. 321-1 et 321-2
- C. pén., art. 323-1, 323-3
- CEDH, 12 févr. 2008, Guja c. Moldova, req. n° 14277/04
- Cass. ass. plén., 22 déc. 2023, n° 20-20.648 et n° 21-11.330
- Conv. EDH, art. 10 (liberté d'expression)
- C. pr. pén., art. 427 (liberté de la preuve en matière pénale)
 
---
