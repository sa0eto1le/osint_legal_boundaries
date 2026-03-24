# AI Act & Biométrie - Règlement (UE) 2024/1689 appliqué à l'OSINT
 
> **FR** - Fiche juridique : encadrement de la biométrie par le règlement européen sur l'intelligence artificielle et impact sur les pratiques OSINT.  
> **EN** - Legal fact sheet: regulation of biometrics under the EU AI Act and its impact on OSINT practices.
 
---
 
##  Texte de référence / Reference Text
 
**Règlement (UE) 2024/1689 du Parlement européen et du Conseil du 13 juin 2024** établissant des règles harmonisées concernant l'intelligence artificielle (AI Act).  
Publié au JOUE L du 12 juillet 2024.
 
### Calendrier d'application / Application Timeline
 
```
1er août 2024       → Entrée en vigueur
2 février 2025      → Art. 5 (pratiques interdites) APPLICABLE
2 août 2025         → Dispositions sur les autorités notifiantes
2 août 2026         → Majorité des dispositions applicables
```
 
>  **Les interdictions de l'article 5 - dont celles relatives à la biométrie - sont applicables depuis le 2 février 2025.**
 
---
 
##  Définitions clés - Art. 3 / Key Definitions
 
### Données biométriques
> *"Données à caractère personnel résultant d'un traitement technique spécifique, relatives aux caractéristiques physiques, physiologiques ou comportementales d'une personne physique, qui permettent ou confirment l'identification unique de cette personne physique, telles que des images faciales ou des données dactyloscopiques."*  
> - AI Act, art. 3 §34
 
### Système d'identification biométrique à distance
> Système d'IA permettant d'identifier des personnes physiques à distance par comparaison de leurs données biométriques avec celles contenues dans une base de référence.  
> - AI Act, art. 3 §40
 
### En temps réel vs en différé
- **En temps réel** : capture, comparaison et identification sans délai significatif
- **En différé** : traitement de données biométriques déjà capturées
 
---
 
##  Pratiques interdites - Art. 5 (applicable depuis le 2 février 2025)
 
### Art. 5 §1 e) - Interdiction du scraping facial
 
**FR** - Est interdit :
 
> *"La mise sur le marché, la mise en service ou l'utilisation de systèmes d'IA qui créent ou étendent des bases de données de reconnaissance faciale par le moissonnage non ciblé d'images faciales à partir d'internet ou de systèmes de vidéosurveillance."*
 
**EN** - Prohibited:
 
> *"The placing on the market, putting into service or use of AI systems that create or expand facial recognition databases through the untargeted scraping of facial images from the internet or CCTV footage."*
 
>  **Impact OSINT direct** : constituer une base d'embeddings faciaux à partir de photos publiques scrappées - même dans un cadre privé, même à des fins non commerciales - est **catégoriquement interdit** depuis le 2 février 2025. Il n'existe aucune exception pour les acteurs privés non habilités.
 
---
 
### Art. 5 §1 h) - Identification biométrique à distance en temps réel dans les espaces publics
 
**FR** - Est interdit l'usage de systèmes d'identification biométrique à distance **en temps réel** dans des espaces accessibles au public **à des fins répressives**, sauf exceptions strictes réservées aux autorités publiques (art. 5 §2 à §5).
 
**Exceptions réservées aux autorités publiques (art. 5 §2) :**
```
1. Recherche ciblée de victimes spécifiques (enlèvement, traite, exploitation sexuelle)
2. Prévention d'une menace terroriste spécifique, réelle et imminente
3. Identification de suspects dans le cadre d'infractions pénales graves
   listées à l'art. 5 §2 point c)
```
 
**Conditions supplémentaires cumulatives :**
```
├── Autorisation judiciaire ou administrative indépendante préalable
│   (sauf urgence absolue - art. 5 §4)
├── Supervision indépendante effective
├── Durée d'utilisation strictement limitée
└── Notification aux autorités de surveillance du marché
```
 
>  **Ces exceptions sont réservées aux autorités publiques habilitées. Elles ne s'appliquent pas aux acteurs privés.**
 
---
 
### Art. 5 §1 g) - Catégorisation biométrique sensible
 
**FR** - Est interdit tout système d'IA qui catégorise des personnes physiques à partir de leurs données biométriques pour en **déduire** leur race, opinions politiques, appartenance syndicale, convictions religieuses ou philosophiques, vie sexuelle ou orientation sexuelle.
 
>  Cela vise notamment les outils OSINT qui croiseraient des données biométriques avec d'autres signaux pour inférer des caractéristiques sensibles.
 
---
 
##  Systèmes à haut risque - Annexe III
 
**FR** - Les systèmes d'identification biométrique et de catégorisation des personnes physiques figurent à l'**Annexe III, point 1** de l'AI Act comme systèmes à haut risque. Ils sont soumis à des obligations renforcées (évaluation de conformité, documentation technique, enregistrement, transparence).
 
**EN** - Biometric identification and categorisation of natural persons are listed in **Annex III, point 1** of the AI Act as high-risk AI systems, subject to enhanced obligations.
 
---
 
##  Articulation avec le RGPD / Interaction with GDPR
 
**FR** - L'AI Act ne remplace pas le RGPD. Les deux textes s'appliquent **cumulativement** :
 
| Question | Texte applicable |
|---|---|
| Le traitement de données biométriques est-il licite ? | RGPD art. 9 |
| Le système d'IA utilisé est-il interdit ? | AI Act art. 5 |
| Le système d'IA est-il à haut risque ? | AI Act Annexe III |
| Les droits des personnes sont-ils respectés ? | RGPD art. 12 à 23 |
 
> Un traitement peut être conforme au RGPD (base légale art. 9 présente) et **quand même être interdit** par l'AI Act si le système utilisé entre dans les pratiques prohibées de l'art. 5.
 
---
 
##  Application à l'OSINT / Application to OSINT
 
### Ce qui est interdit depuis le 2 février 2025
 
```
 Scraper des photos publiques pour constituer une base de reconnaissance faciale
 Utiliser un outil d'identification faciale alimenté par du scraping massif (ex : Clearview AI)
 Extraire des embeddings faciaux à partir de photos en ligne sans base légale art. 9 RGPD
 Catégoriser des personnes à partir de données biométriques pour inférer des caractéristiques
   sensibles (religion, orientation sexuelle, opinions politiques)
```
 
### Ce qui reste possible sous conditions
 
```
  Regarder une photo publiée en ligne → pas de traitement biométrique
  Identifier manuellement une personne à partir d'une photo → dépend du contexte
    et de la base légale RGPD
  Utiliser des outils d'identification biométrique avec base légale explicite art. 9 RGPD
    et en dehors des pratiques interdites art. 5 AI Act
```
 
### La ligne de bascule technique
 
```
OBSERVATION (pas de traitement biométrique)
    └── Regarder une photo publiée sur un réseau social
    └── Décrire l'apparence d'une personne
    └── Identifier manuellement une photo déjà connue
 
    ↓  BASCULE : extraction d'un vecteur biométrique (embedding)
 
TRAITEMENT BIOMÉTRIQUE (RGPD art. 9 + AI Act art. 5 applicables)
    └── Extraction d'un embedding facial à des fins d'identification
    └── Comparaison algorithmique entre deux visages
    └── Recherche par similarité faciale dans une base
    └── Constitution d'une base d'empreintes faciales
```
 
---
 
##  Décision de référence / Reference Decision
 
### Clearview AI - CNIL, octobre 2022
 
**FR** - La CNIL a sanctionné Clearview AI à hauteur de **20 millions d'euros** pour collecte massive de photos publiques sans base légale, violation de l'art. 9 RGPD et non-respect des droits des personnes. L'EDPB a coordonné des décisions similaires dans plusieurs États membres.
 
Ce qui rend cette décision structurante pour l'OSINT : la logique d'aggravation progressive retenue par la CNIL - chaque étape amplifie l'atteinte (collecte → vectorisation → base → commercialisation) - s'applique à toute démarche similaire, même privée et non commerciale.
 
**EN** - The CNIL fined Clearview AI **€20 million** for mass collection of public photos without legal basis, violation of GDPR art. 9, and failure to respect data subjects' rights. The EDPB coordinated similar decisions across several member states.
 
> Source : EDPB, *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022.  
> Source : CEPD, *Annual Report 2023*, avr. 2024, p. 37.
 
---
 
##  Références / References
 
- Règlement (UE) 2024/1689 - AI Act, art. 3, 5, Annexe III
- Règlement (UE) 2016/679 - RGPD, art. 9
- EDPB, *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022
- CEPD, *Annual Report 2023*, avr. 2024, p. 37
 
---
