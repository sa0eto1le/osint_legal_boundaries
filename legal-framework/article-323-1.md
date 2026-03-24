# Art. 323-1 C. pén. - Accès et maintien frauduleux dans un STAD
 
> **FR** - Fiche juridique : l'infraction d'accès et de maintien frauduleux dans un système de traitement automatisé de données, et son application aux pratiques OSINT.  
> **EN** - Legal fact sheet: the offense of unauthorized access and persistence in an automated data processing system, and its application to OSINT practices.
 
---
 
##  Texte de loi / Statutory Text
 
```
Article 323-1 du Code pénal (version en vigueur)
 
Le fait d'accéder ou de se maintenir, frauduleusement, dans tout ou partie d'un système 
de traitement automatisé de données est puni de trois ans d'emprisonnement et de 
100 000 euros d'amende.
 
Lorsqu'il en est résulté soit la suppression ou la modification de données contenues 
dans le système, soit une altération du fonctionnement de ce système, la peine est de 
cinq ans d'emprisonnement et de 150 000 euros d'amende.
 
Lorsque les infractions prévues aux deux premiers alinéas ont été commises à l'encontre 
d'un système de traitement automatisé de données à caractère personnel mis en œuvre 
par l'État, la peine est portée à sept ans d'emprisonnement et à 300 000 euros d'amende.
```
 
> Fondement historique : **loi n° 88-19 du 5 janvier 1988** relative à la fraude informatique, dite loi **Godfrain**.
 
---
 
##  Éléments constitutifs / Elements of the Offense
 
### 1. Le STAD - Système de Traitement Automatisé de Données
 
**FR** - La loi ne définit pas le STAD. Ce silence est volontaire : le législateur a choisi une formulation large pour absorber les évolutions technologiques. En pratique, tout système informatique connecté ou non, dès lors qu'il traite des données de manière automatisée, peut être qualifié de STAD : serveur web, base de données, API, application mobile, etc.
 
**EN** - The law does not define STAD (automated data processing system). This silence is deliberate: the legislator chose broad wording to absorb technological evolution. In practice, any computer system - connected or not - that processes data automatically qualifies: web server, database, API, mobile application, etc.
 
>  **Ce qui compte n'est pas la sophistication du système, mais l'intention de son propriétaire d'en restreindre l'accès.**
 
---
 
### 2. Le critère décisif : la restriction d'accès
 
**FR** - Contrairement à une idée reçue, l'infraction ne requiert **pas** l'existence d'une protection technique active (mot de passe, chiffrement, pare-feu). La jurisprudence et la doctrine ont établi que le critère déterminant est **l'intention manifeste du maître du système de restreindre l'accès**.
 
Autrement dit : un système mal protégé, voire non protégé, reste un STAD protégé par l'article 323-1 si son propriétaire n'a pas souhaité le rendre public.
 
**EN** - Contrary to popular belief, the offense does **not** require an active technical protection (password, encryption, firewall). Case law and doctrine have established that the determining criterion is **the system owner's manifest intent to restrict access**.
 
In other words: a poorly protected or even unprotected system remains a protected STAD under art. 323-1 if its owner did not intend to make it public.
 
---
 
### 3. L'élément moral : la fraude
 
**FR** - La fraude n'est pas définie par la loi. Elle couvre toute intrusion **consciente** au-delà d'une frontière que l'auteur sait ou devrait savoir protégée. L'accès obtenu "sans forcer" n'exclut pas l'illicéité si l'auteur avait conscience du caractère restreint du système.
 
Deux comportements distincts sont incriminés **de manière autonome** :
- **L'accès frauduleux** - pénétrer dans le système sans droit
- **Le maintien frauduleux** - rester dans le système après avoir réalisé que l'accès n'était pas autorisé
 
**EN** - Fraud is not defined by law. It covers any **conscious** intrusion beyond a boundary that the perpetrator knows or should know is protected. Access obtained "without force" does not exclude illegality if the perpetrator was aware of the restricted nature of the system.
 
Two distinct behaviors are separately criminalized:
- **Unauthorized access** - entering the system without right
- **Unauthorized persistence** - remaining in the system after realizing access was not authorized
 
---
 
##  Jurisprudence clé / Key Case Law
 
###  Bluetouff - Cass. crim., 20 mai 2015 (n° 14-81.336)
 
**Les faits / Facts**
 
Un individu accède via Google à des documents internes d'une organisation. Ces documents étaient indexés par inadvertance et accessibles via une simple URL. Sans outil de piratage, l'individu navigue, explore et télécharge plusieurs fichiers. Il ne s'est pas introduit dans le système par effraction technique.
 
**La décision / Ruling**
 
La Chambre criminelle retient le **maintien frauduleux dans un STAD**. Le raisonnement de la Cour repose sur deux points :
1. L'individu a perçu des signaux indiquant que le contenu n'était pas destiné au public (nature des documents, structure du système).
2. Malgré cette prise de conscience, il a choisi de poursuivre sa navigation et de télécharger des fichiers.
 
**L'enseignement / Key takeaway**
 
> Ce n'est pas l'effraction qui fonde la qualification pénale. C'est la **conscience de franchir une limite** et la décision de **poursuivre malgré tout**.
 
**Impact direct sur l'OSINT**
 
| Situation | Qualification |
|---|---|
| Trouver un document via Google sans signe de restriction |  Zone neutre |
| Percevoir un signal de restriction (robots.txt, structure interne, CGU) et s'arrêter |  Pas d'infraction |
| Percevoir un signal de restriction et poursuivre |  Maintien frauduleux potentiel |
| Télécharger / exporter des données après ce signal |  Risque pénal élevé |
 
---
 
##  Application à l'OSINT / Application to OSINT
 
### Ce qui ne constitue PAS une infraction
 
```
 Consulter des pages web publiques indexées par les moteurs de recherche
 Utiliser des opérateurs de recherche avancée (dorking) sur des contenus publics
 Accéder à des données disponibles via une API publique dans le respect des CGU
 Consulter des profils publics sur des réseaux sociaux
 Utiliser Shodan pour une reconnaissance passive (données déjà indexées)
```
 
### Zones de risque / Risk zones
 
```
  Poursuivre la navigation après avoir perçu un signal de restriction
  Accéder à un répertoire exposé par inadvertance (robots.txt indique une restriction)
  Modifier des paramètres d'URL pour accéder à des ressources non autorisées (IDOR)
  Utiliser un compte fictif pour accéder à un espace techniquement restreint
  Réitérer ou automatiser l'accès à des ressources dont le caractère restreint est connu
```
 
### Ce qui constitue clairement une infraction
 
```
 Contourner une authentification (même faible)
 Exploiter une faille pour accéder à des données non destinées au public
 Télécharger des données après avoir perçu un signal de restriction
 Scanner activement un système tiers sans autorisation
```
 
---
 
##  Les signaux de restriction à reconnaître / Restriction Signals
 
**FR** - Dans la pratique OSINT, identifier ces signaux est crucial. Les percevoir et poursuivre, c'est basculer dans la zone de risque pénal.
 
**EN** - In OSINT practice, identifying these signals is critical. Perceiving them and continuing means entering the criminal risk zone.
 
```
SIGNAUX TECHNIQUES / TECHNICAL SIGNALS
├── robots.txt indiquant des zones exclues
├── CAPTCHA ou mécanisme anti-bot
├── Authentification requise (même contournable)
├── Rate limiting ou blocage d'IP
└── Tokens ou headers de session dans les requêtes
 
SIGNAUX CONTEXTUELS / CONTEXTUAL SIGNALS
├── Documents à caractère manifestement interne (RH, finances, config)
├── Répertoire listé sans page d'accueil (index of /)
├── Fichiers de configuration ou credentials exposés
├── Mentions légales ou CGU restreignant l'accès automatisé
└── URL structurée pour un usage interne (admin/, backoffice/, etc.)
```
 
---
 
##  Échelle des peines / Sentencing Scale
 
| Infraction | Peine maximale |
|---|---|
| Accès / maintien frauduleux simple | 3 ans · 100 000 € |
| Avec suppression ou modification de données | 5 ans · 150 000 € |
| Sur un STAD de l'État | 7 ans · 300 000 € |
| En bande organisée | 10 ans · 300 000 € |
 
---
 
##  Infractions connexes / Related Offenses
 
| Article | Infraction | Lien avec l'OSINT |
|---|---|---|
| Art. 226-4-1 C. pén. | Usurpation d'identité numérique | Sockpuppet / faux profil sur une personne réelle |
| Art. 321-1 C. pén. | Recel | Exploitation de données issues d'une fuite |
| Art. 226-1 C. pén. | Atteinte à la vie privée | Collecte de données dans un lieu privé |
| Art. 323-2 C. pén. | Entrave au fonctionnement d'un STAD | Scraping intensif perturbant un service |
| Art. 323-3 C. pén. | Extraction frauduleuse de données | Export non autorisé de bases de données |
 
---
 
##  Références / References
 
- C. pén., art. 323-1 à 323-8
- Loi n° 88-19 du 5 janv. 1988, dite loi Godfrain
- Cass. crim., 20 mai 2015, n° 14-81.336 (Bluetouff)
- ANSSI, CyberDico - entrée « STAD »
- Ollard R., *Ordre et désordres du droit pénal de la cybercriminalité*, Lexbase, n° 946, 2023
 
---
