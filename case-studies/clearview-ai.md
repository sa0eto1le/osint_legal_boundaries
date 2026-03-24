# Clearview AI - CNIL, 2022 / EDPB coordination
 
> **FR** - Analyse de l'affaire Clearview AI : la décision de référence en matière de scraping massif de données biométriques et son impact sur la pratique de l'OSINT.  
> **EN** - Analysis of the Clearview AI case: the landmark decision on mass scraping of biometric data and its impact on OSINT practice.
 
---
 
##  Références / References
 
- **CNIL**, Mise en demeure puis sanction, 2021-2022
- **Montant de la sanction CNIL** : 20 000 000 €
- **Date de la sanction CNIL** : octobre 2022
- **Coordination EDPB** : décisions similaires dans plusieurs États membres (Italie, Grèce, Royaume-Uni)
- **Source EDPB** : *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022
- **Source CEPD** : *Annual Report 2023*, avr. 2024, p. 37
 
---
 
##  Qui est Clearview AI / Who is Clearview AI
 
**FR** - Clearview AI est une société américaine qui a développé un moteur de recherche par reconnaissance faciale. Son fonctionnement repose sur une base de données constituée par scraping massif et automatisé de photographies publiées sur internet - réseaux sociaux, sites web, plateformes diverses. À chaque photo, un vecteur biométrique (embedding facial) est extrait et stocké. La base ainsi constituée permettait, à partir d'une photo d'un inconnu, de retrouver ses apparitions sur internet et d'identifier la personne.
 
**EN** - Clearview AI is an American company that developed a facial recognition search engine. Its operation relies on a database built through massive automated scraping of photographs published on the internet - social networks, websites, various platforms. For each photo, a biometric vector (facial embedding) is extracted and stored. The resulting database allowed, from a photo of an unknown person, to find their appearances on the internet and identify the person.
 
---
 
##  Les faits / Facts
 
### La mécanique de constitution de la base
 
**FR** - Le processus de Clearview AI suit une logique d'aggravation progressive, chaque étape amplifiant l'atteinte :
 
**EN** - Clearview AI's process follows a logic of progressive aggravation, each step amplifying the violation:
 
```
ÉTAPE 1 - Scraping massif et non ciblé
└── Collecte automatisée de milliards de photos depuis internet
└── Sans consentement des personnes photographiées
└── Sans base légale identifiée
 
ÉTAPE 2 - Traitement biométrique
└── Extraction d'un embedding facial pour chaque photo
└── Transformation de l'image en vecteur numérique identifiant
└── Entrée dans le champ de l'art. 9 RGPD (données biométriques)
 
ÉTAPE 3 - Constitution d'une base de données massive
└── Milliards d'empreintes faciales stockées
└── Associées aux URLs sources et métadonnées
└── Permettant l'identification de personnes à partir d'une photo
 
ÉTAPE 4 - Commercialisation
└── Service vendu à des forces de l'ordre, agences privées, entreprises
└── Sans information des personnes figurant dans la base
└── Sans mécanisme d'opposition effectif
```
 
---
 
### Les manquements retenus par la CNIL
 
**FR** - La CNIL a retenu plusieurs manquements au RGPD :
 
**EN** - The CNIL identified several GDPR violations:
 
```
1. ABSENCE DE BASE LÉGALE (art. 6 RGPD)
   └── Aucune des bases légales de l'art. 6 ne justifiait le traitement
   └── Le consentement n'avait pas été recueilli
   └── L'intérêt légitime invoqué ne résistait pas à la mise en balance
 
2. TRAITEMENT ILLICITE DE DONNÉES BIOMÉTRIQUES (art. 9 RGPD)
   └── Les embeddings faciaux sont des données biométriques au sens de l'art. 9
   └── Aucune exception de l'art. 9 §2 n'était applicable
   └── Interdiction de principe violée
 
3. NON-RESPECT DU DROIT D'ACCÈS (art. 15 RGPD)
   └── Les demandes d'accès des personnes n'étaient pas traitées correctement
 
4. NON-RESPECT DU DROIT D'OPPOSITION (art. 21 RGPD)
   └── Absence de mécanisme effectif permettant aux personnes de s'opposer
   └── Ou mécanisme inefficace dans les faits
 
5. NON-RESPECT DU DROIT À L'EFFACEMENT (art. 17 RGPD)
   └── Les demandes d'effacement n'étaient pas honorées effectivement
```
 
---
 
### La non-conformité persistante
 
**FR** - Clearview AI n'a pas mis fin aux manquements après les premières injonctions. Le CEPD mentionne dans son bilan 2023 une procédure de sanction supplémentaire pour défaut de conformité, illustrant la dimension coercitive et persistante de ce type de procédure.
 
**EN** - Clearview AI did not end the violations after initial injunctions. The EDPB mentions in its 2023 annual report additional sanction proceedings for non-compliance, illustrating the coercive and persistent dimension of this type of procedure.
 
> Source : CEPD, *Annual Report 2023*, avr. 2024, p. 37.  
 
---
 
##  Les principes juridiques dégagés / Legal Principles Established
 
### 1. La publicité d'une image ≠ autorisation de traitement biométrique
 
**FR** - C'est l'enseignement central de l'affaire Clearview AI, directement transposable à l'OSINT. Le fait qu'une photographie soit publiée librement sur internet - sur un réseau social, un site personnel, une page professionnelle - ne vaut pas autorisation pour un tiers de l'utiliser à des fins d'identification biométrique.
 
La personne qui publie une photo en ligne manifeste une attente raisonnable : être vue par les visiteurs du site ou ses contacts. Elle n'exprime pas le consentement à ce que son visage soit vectorisé, stocké dans une base biométrique et utilisé pour l'identifier à partir de n'importe quelle autre photo.
 
**EN** - This is the central lesson of the Clearview AI case, directly applicable to OSINT. The fact that a photograph is freely published on the internet - on a social network, personal site, professional page - does not constitute authorization for a third party to use it for biometric identification purposes.
 
The person who publishes a photo online expresses a reasonable expectation: to be seen by site visitors or their contacts. They do not express consent for their face to be vectorized, stored in a biometric database, and used to identify them from any other photo.
 
---
 
### 2. La logique d'aggravation progressive
 
**FR** - La CNIL n'a pas sanctionné Clearview AI pour avoir regardé des photos publiques. Elle a sanctionné la **chaîne complète de traitement** : scraping → vectorisation → stockage → commercialisation. Chaque étape aggrave l'atteinte. Cette logique s'applique à toute démarche OSINT impliquant des données biométriques.
 
**EN** - The CNIL did not sanction Clearview AI for looking at public photos. It sanctioned the **complete processing chain**: scraping → vectorization → storage → commercialization. Each step aggravates the violation. This logic applies to any OSINT approach involving biometric data.
 
```
OBSERVER une photo en ligne          → Pas de traitement biométrique
EXTRAIRE un embedding facial         → Art. 9 RGPD applicable
STOCKER l'embedding                  → Traitement sans base légale
CROISER avec d'autres embeddings     → Identification = atteinte aggravée
COMMERCIALISER ou diffuser           → Aggravation maximale
```
 
---
 
### 3. L'absence de présence dans l'UE n'exclut pas la compétence CNIL
 
**FR** - Clearview AI est une société américaine sans établissement dans l'Union européenne. La CNIL s'est néanmoins déclarée compétente sur le fondement du critère de ciblage (art. 3 §2 RGPD) : le traitement portait sur des personnes situées sur le territoire de l'Union. Ce principe est important pour l'OSINT : un outil étranger traitant des données de personnes européennes reste soumis au RGPD.
 
**EN** - Clearview AI is an American company without an establishment in the European Union. The CNIL nevertheless declared itself competent on the basis of the targeting criterion (art. 3 §2 GDPR): the processing concerned persons located on EU territory. This principle matters for OSINT: a foreign tool processing data of European persons remains subject to the GDPR.
 
> Source : Règlement (UE) 2016/679 - RGPD, art. 3 §2 (critère de ciblage).
 
---
 
##  Impact sur l'OSINT / Impact on OSINT
 
### Ce que Clearview AI interdit de reproduire
 
```
 Constituer une base d'embeddings faciaux par scraping de photos publiques
   → Interdit RGPD art. 9 + AI Act art. 5 §1 e) depuis le 2 février 2025
 
 Utiliser un outil tiers alimenté par ce type de base
   → L'utilisateur d'un service construit sur scraping massif
     partage une responsabilité dans le traitement
 
 Croiser des photos OSINT avec une base de reconnaissance faciale
   non autorisée
   → Même à des fins non commerciales, même en contexte privé
```
 
---
 
### La ligne de bascule technique en OSINT
 
```
OSINT VISUEL LICITE                     OSINT BIOMÉTRIQUE ILLICITE
│                                       │
├── Regarder une photo publiée          ├── Extraire un embedding facial
├── Décrire l'apparence d'une           ├── Comparer algorithmiquement
│   personne                            │   deux visages
├── Identifier manuellement             ├── Rechercher par similarité
│   une photo déjà connue               │   dans une base
└── Recherche d'image inversée          └── Constituer une base
    (Google Images, TinEye)                 d'empreintes faciales
    → pas d'extraction d'embedding
```
 
>  **Google Images / TinEye** : ces outils de recherche d'image inversée ne constituent pas un traitement biométrique au sens de l'art. 9 RGPD dans leur usage standard - ils cherchent par similarité visuelle globale sans extraire ni stocker d'embedding facial identifiant. La qualification dépend cependant de l'implémentation exacte de l'outil utilisé.
 
---
 
##  Sanctions coordonnées au niveau européen / Coordinated European Sanctions
 
| Autorité | Montant | Année |
|---|---|---|
| CNIL (France) | 20 000 000 € | 2022 |
| Garante (Italie) | 20 000 000 € | 2022 |
| ICO (Royaume-Uni) | 7 500 000 £ | 2022 |
| HDPA (Grèce) | 20 000 000 € | 2022 |
 
> Source : EDPB, *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022.  
 
>  **Note** : les montants exacts des sanctions des autorités italienne et grecque sont repris des communications EDPB. Pour les détails exacts des décisions nationales, se référer directement aux autorités concernées (Garante, HDPA).
 
---
 
##  Liens avec d'autres textes et décisions / Links to Other Texts and Decisions
 
| Texte / Décision | Lien avec Clearview AI |
|---|---|
| RGPD art. 9 | Fondement principal - données biométriques |
| RGPD art. 3 §2 | Compétence territoriale - critère de ciblage |
| AI Act art. 5 §1 e) | Interdit depuis fév. 2025 ce que Clearview AI faisait |
| KASPR (2024) | Même logique : visibilité partielle ≠ libre réutilisation |
| Bluetouff (2015) | Complémentaire : accessibilité technique ≠ autorisation |
 
---
 
##  Références / References
 
- EDPB, *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022
- CEPD, *Annual Report 2023*, avr. 2024, p. 37
- Règlement (UE) 2016/679 - RGPD, art. 3 §2, 6, 9, 15, 17, 21
- Règlement (UE) 2024/1689 - AI Act, art. 5 §1 e)
 
---
