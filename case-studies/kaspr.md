# KASPR - CNIL, délibération du 5 décembre 2024
 
> **FR** - Analyse de la décision CNIL contre KASPR : la décision de référence sur la collecte de données via scraping de réseaux sociaux professionnels et les attentes raisonnables de confidentialité.  
> **EN** - Analysis of the CNIL decision against KASPR: the landmark decision on data collection via scraping of professional social networks and reasonable confidentiality expectations.
 
---
 
##  Références / References
 
- **Autorité** : Commission nationale de l'informatique et des libertés (CNIL)
- **Date** : 5 décembre 2024
- **Montant de la sanction** : 240 000 €
- **Source CNIL** : *Data scraping : KASPR sanctionnée à hauteur de 240 000 euros*
 
---
 
##  Qui est KASPR / Who is KASPR
 
**FR** - KASPR est une société proposant un outil de prospection commerciale permettant d'obtenir les coordonnées professionnelles de personnes à partir de leurs profils LinkedIn. L'outil se présente comme une extension de navigateur qui, lorsqu'un utilisateur visite un profil LinkedIn, extrait et fournit les coordonnées de contact associées - numéros de téléphone et adresses email notamment - en interrogeant des endpoints de la plateforme.
 
**EN** - KASPR is a company offering a commercial prospecting tool that allows obtaining professional contact details of individuals from their LinkedIn profiles. The tool presents itself as a browser extension that, when a user visits a LinkedIn profile, extracts and provides associated contact details - phone numbers and email addresses notably - by querying platform endpoints.
 
---
 
##  Les faits / Facts
 
### Le mécanisme de collecte
 
**FR** - KASPR collectait des données de contact depuis LinkedIn en interrogeant des endpoints de la plateforme. La particularité de cette affaire tient au paramètre de visibilité des données collectées : les utilisateurs LinkedIn avaient, pour certaines de ces données, **restreint la visibilité à leurs connexions directes** - et non au public général.
 
KASPR accédait néanmoins à ces données en exploitant les accès de ses propres utilisateurs (qui étaient connectés à LinkedIn) pour récupérer des informations que les personnes ciblées n'avaient pas rendu visibles à tous.
 
**EN** - KASPR collected contact data from LinkedIn by querying platform endpoints. The particularity of this case concerns the visibility parameter of the collected data: LinkedIn users had, for some of this data, **restricted visibility to their direct connections** - not to the general public.
 
KASPR nevertheless accessed this data by exploiting its own users' access (who were logged into LinkedIn) to retrieve information that the targeted persons had not made visible to everyone.
 
---
 
### Les manquements retenus par la CNIL
 
```
1. ABSENCE DE BASE LÉGALE (art. 6 RGPD)
   └── La collecte ne reposait sur aucune base légale valide
   └── L'intérêt légitime invoqué ne résistait pas à la mise en balance
       avec les attentes raisonnables des personnes concernées
 
2. VIOLATION DES ATTENTES RAISONNABLES DE CONFIDENTIALITÉ
   └── Les personnes avaient activement restreint la visibilité
       de leurs coordonnées à leurs connexions directes
   └── Cette restriction exprime une attente légitime de confidentialité
   └── La collecte par un tiers via un mécanisme détourné viole
       cette attente même si les données étaient techniquement accessibles
       via un compte connecté
 
3. MANQUEMENT À L'OBLIGATION D'INFORMATION (art. 14 RGPD)
   └── Les personnes dont les données étaient collectées
       n'en étaient pas informées
 
4. MANQUEMENT AUX DROITS DES PERSONNES
   └── Absence de mécanisme effectif d'exercice des droits
       (accès, opposition, effacement)
```
 
---
 
##  Les principes juridiques dégagés / Legal Principles Established
 
### 1. Visibilité partielle ≠ consentement à la collecte par des tiers
 
**FR** - C'est l'enseignement central de la décision KASPR. La CNIL affirme avec clarté qu'un utilisateur qui restreint la visibilité de ses coordonnées à ses connexions directes n'exprime **pas** le consentement à ce qu'un tiers les collecte, les stocke et les commercialise. Le choix d'une visibilité restreinte est au contraire un signal explicite de volonté de limiter la diffusion.
 
**EN** - This is the central lesson of the KASPR decision. The CNIL clearly states that a user who restricts the visibility of their contact details to their direct connections does **not** express consent for a third party to collect, store, and commercialize them. The choice of restricted visibility is on the contrary an explicit signal of intent to limit dissemination.
 
>  **Formulation clé** : la CNIL considère que le choix d'une visibilité restreinte à certains cercles relationnels ne revient pas à autoriser un tiers à aspirer ces données pour les intégrer à une base destinée à des usages commerciaux.
 
---
 
### 2. Les attentes raisonnables de confidentialité s'imposent
 
**FR** - La décision KASPR ancre dans la pratique CNIL le concept d'**attentes raisonnables de confidentialité** des personnes concernées. Ce concept, développé notamment par la jurisprudence de la Cour européenne des droits de l'homme dans l'interprétation de l'article 8 de la Convention, signifie que la légitimité d'un traitement s'évalue aussi au regard de ce que la personne pouvait raisonnablement anticiper quant à l'usage de ses données.
 
Une personne qui publie ses coordonnées sur LinkedIn avec une restriction de visibilité anticipe raisonnablement qu'elles seront vues par ses connexions - pas qu'elles seront extraites et revendues à des tiers à des fins commerciales.
 
**EN** - The KASPR decision anchors in CNIL practice the concept of **reasonable confidentiality expectations** of data subjects. This concept, developed notably by the European Court of Human Rights in interpreting Article 8 of the Convention, means that the legitimacy of processing is also assessed against what the person could reasonably anticipate regarding the use of their data.
 
A person who publishes their contact details on LinkedIn with a visibility restriction reasonably anticipates they will be seen by their connections - not that they will be extracted and resold to third parties for commercial purposes.
 
---
 
### 3. L'accessibilité technique via un compte connecté ne suffit pas
 
**FR** - KASPR n'accédait pas à des données totalement publiques - elle exploitait l'accès de ses utilisateurs connectés pour atteindre des données dont la visibilité était restreinte. La CNIL retient que cette accessibilité technique conditionnelle (visible uniquement pour les connexions) ne constitue pas une autorisation de collecte par un tiers commercial.
 
Ce principe complète le raisonnement Clearview AI : même une accessibilité technique réelle, sous conditions, ne vaut pas autorisation juridique de traitement.
 
**EN** - KASPR was not accessing fully public data - it exploited its logged-in users' access to reach data whose visibility was restricted. The CNIL finds that this conditional technical accessibility (visible only to connections) does not constitute authorization for collection by a commercial third party.
 
This principle complements the Clearview AI reasoning: even real technical accessibility, under conditions, does not constitute legal authorization for processing.
 
---
 
##  Impact sur l'OSINT / Impact on OSINT
 
### Ce que KASPR interdit de reproduire en OSINT
 
```
 Collecter des données dont la visibilité a été restreinte par la personne
   → Même si techniquement accessibles via un compte connecté
 
 Exploiter les accès d'un compte tiers pour atteindre des données
   restreintes à certains cercles relationnels
 
 Constituer une base de données de coordonnées professionnelles
   sans base légale et sans information des personnes
 
 Ignorer les paramétrages de confidentialité des plateformes
   comme signaux des attentes des personnes
```
 
---
 
### La grille de lecture post-KASPR pour l'OSINT sur réseaux sociaux
 
```
DONNÉE PUBLIQUE (visible par tous, sans compte)
└── Accessibilité technique élevée
└── Base légale toujours requise (RGPD art. 6)
└── Attentes de confidentialité : faibles mais présentes
 
DONNÉE SEMI-PUBLIQUE (visible pour les connexions/abonnés)
└── Accessibilité technique conditionnelle
└── Base légale requise (RGPD art. 6)
└── Attentes de confidentialité : moyennes à élevées
└── KASPR : collecte par tiers commercial = illicite
 
DONNÉE PRIVÉE (visible uniquement pour l'utilisateur)
└── Accessibilité technique inexistante sans violation
└── Toute collecte = accès frauduleux (art. 323-1 C. pén.)
└── Attentes de confidentialité : maximales
```
 
---
 
### Application pratique par type de plateforme
 
| Plateforme | Type de donnée | Paramètre visibilité | Risque OSINT |
|---|---|---|---|
| LinkedIn - coordonnées restreintes | Semi-publique | Connexions uniquement |  KASPR - illicite |
| LinkedIn - profil public | Publique | Tous |  Base légale requise |
| Twitter/X - compte public | Publique | Tous |  Base légale requise |
| Twitter/X - compte privé | Privée | Abonnés approuvés |  Accès frauduleux |
| Instagram - compte privé | Privée | Abonnés approuvés |  Accès frauduleux |
| Facebook - groupe fermé | Semi-publique | Membres du groupe |  Zone grise - contexte décisif |
 
---
 
##  Liens avec d'autres textes et décisions / Links to Other Texts and Decisions
 
| Texte / Décision | Lien avec KASPR |
|---|---|
| RGPD art. 6 | Fondement principal - absence de base légale |
| RGPD art. 14 | Obligation d'information non respectée |
| Conv. EDH art. 8 | Attentes raisonnables de confidentialité |
| Clearview AI (2022) | Même logique : publicité ≠ libre réutilisation |
| Bluetouff (2015) | Complémentaire : conscience de la restriction |
| CNIL scraping (2025) | Cadre général de conformité du scraping |
 
---
 
##  Ce que la décision apporte de nouveau / What the Decision Adds
 
**FR** - Par rapport aux décisions antérieures, KASPR apporte deux précisions importantes pour la pratique OSINT :
 
1. **La granularité des paramètres de confidentialité est juridiquement pertinente.** Ce n'est pas seulement la distinction public/privé qui compte, mais le paramètre de visibilité précis choisi par la personne. Restreindre à ses connexions est un acte juridiquement significatif.
 
2. **L'exploitation de l'accès d'un tiers pour contourner une restriction est assimilée à une collecte non autorisée.** KASPR utilisait les sessions de ses propres utilisateurs - eux légitimement connectés - pour atteindre des données que les cibles n'avaient pas rendues accessibles à tous. Ce mécanisme indirect ne neutralise pas l'illicéité.
 
**EN** - Compared to previous decisions, KASPR brings two important clarifications for OSINT practice:
 
1. **The granularity of privacy settings is legally relevant.** It's not just the public/private distinction that matters, but the precise visibility parameter chosen by the person.
 
2. **Exploiting a third party's access to bypass a restriction is treated as unauthorized collection.** KASPR used its own users' sessions - legitimately logged in - to reach data that targets had not made accessible to everyone. This indirect mechanism does not neutralize the illegality.
 
---
 
##  Références / References
 
- CNIL, *Data scraping : KASPR sanctionnée à hauteur de 240 000 euros*,
  délibération du 5 déc. 2024
- Règlement (UE) 2016/679 - RGPD, art. 6, 14, 17, 21
- Conv. EDH, art. 8 (droit au respect de la vie privée)
- CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025
 
---
