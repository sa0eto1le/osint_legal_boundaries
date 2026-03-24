# Bluetouff - Cass. crim., 20 mai 2015, n° 14-81.336
 
> **FR** - Analyse de l'affaire Bluetouff : l'arrêt de référence en matière de maintien frauduleux dans un STAD sans effraction technique, et son impact direct sur la pratique de l'OSINT.  
> **EN** - Analysis of the Bluetouff case: the landmark ruling on unauthorized persistence in a computer system without technical intrusion, and its direct impact on OSINT practice.
 
---
 
##  Référence / Reference
 
- **Juridiction** : Cour de cassation, Chambre criminelle
- **Date** : 20 mai 2015
- **Numéro** : n° 14-81.336
- **Publication** : Bulletin criminel 2015, n° 113
- **Légifrance** 
 
---
 
##  Les faits / Facts
 
**FR** - Un individu, connu sous le pseudonyme Bluetouff, effectue des recherches sur un moteur de recherche standard. Parmi les résultats, apparaît un lien donnant accès à des documents internes d'une organisation - l'Agence nationale de sécurité sanitaire de l'alimentation, de l'environnement et du travail (ANSES). Ces documents avaient été indexés par inadvertance et étaient accessibles via une URL directe sans authentification requise.
 
L'individu n'a utilisé aucun outil de piratage, aucune technique d'effraction, aucun contournement de système de protection actif. Il a simplement suivi un lien apparu dans les résultats d'un moteur de recherche, navigué dans les répertoires accessibles, puis téléchargé plusieurs fichiers dont il a reconnu le caractère confidentiel.
 
**EN** - An individual, known by the pseudonym Bluetouff, conducts searches on a standard search engine. Among the results, a link appears giving access to internal documents of an organization - the French Agency for Food, Environmental and Occupational Health & Safety (ANSES). These documents had been inadvertently indexed and were accessible via a direct URL without required authentication.
 
The individual used no hacking tools, no intrusion technique, no bypass of any active protection system. He simply followed a link appearing in search results, navigated accessible directories, then downloaded several files whose confidential nature he acknowledged.
 
---
 
##  La procédure / Procedure
 
**FR** - L'individu a été poursuivi puis condamné en première instance et en appel pour :
- Maintien frauduleux dans un système de traitement automatisé de données (art. 323-1 C. pén.)
- Vol de fichiers informatiques
 
Il s'est pourvu en cassation, contestant notamment que l'absence de protection technique active ne pouvait caractériser un accès ou maintien frauduleux.
 
**EN** - The individual was prosecuted and convicted at first instance and on appeal for:
- Unauthorized persistence in an automated data processing system (art. 323-1 French Penal Code)
- Theft of computer files
 
He appealed to the Court of Cassation, contesting notably that the absence of active technical protection could not characterize unauthorized access or persistence.
 
---
 
##  La décision / The Ruling
 
**FR** - La Chambre criminelle de la Cour de cassation a **rejeté le pourvoi** et confirmé la condamnation. Le raisonnement de la Cour repose sur deux points fondamentaux.
 
**EN** - The Criminal Chamber of the Court of Cassation **rejected the appeal** and confirmed the conviction. The Court's reasoning rests on two fundamental points.
 
### Point 1 - La protection technique n'est pas le critère
 
**FR** - La Cour confirme que la qualification de maintien frauduleux dans un STAD ne dépend **pas** de l'existence d'une protection technique active. Ce qui importe, c'est l'intention du maître du système de restreindre l'accès - et non la robustesse des moyens techniques mis en œuvre pour y parvenir.
 
Un système mal protégé, voire exposé par inadvertance, reste un STAD juridiquement protégé par l'article 323-1 si son propriétaire n'a pas entendu le rendre librement accessible.
 
**EN** - The Court confirms that the unauthorized persistence qualification does **not** depend on the existence of active technical protection. What matters is the system owner's intent to restrict access - not the robustness of technical means implemented to achieve it.
 
A poorly protected or even inadvertently exposed system remains a legally protected STAD under article 323-1 if its owner did not intend to make it freely accessible.
 
---
 
### Point 2 - La conscience de franchir une limite
 
**FR** - L'élément moral décisif est la **conscience**, chez l'auteur, d'avoir perçu que le système ou les données n'étaient pas destinés au public, et d'avoir néanmoins choisi de poursuivre sa navigation et de télécharger des fichiers.
 
En l'espèce, la Cour retient que l'individu avait clairement conscience du caractère confidentiel des documents - leur nature même (documents internes d'une agence sanitaire) le démontrait. Malgré cette conscience, il a continué à naviguer et à télécharger. C'est ce maintien conscient qui fonde la qualification pénale.
 
**EN** - The decisive mental element is the **awareness**, on the part of the perpetrator, of having perceived that the system or data were not intended for the public, and having nevertheless chosen to continue navigating and downloading files.
 
In this case, the Court found that the individual was clearly aware of the confidential nature of the documents - their very nature (internal documents of a health agency) demonstrated this. Despite this awareness, he continued to navigate and download. It is this conscious persistence that establishes the criminal qualification.
 
---
 
##  L'enseignement central / The Core Lesson
 
> **FR** - Ce n'est pas l'effraction qui fonde la qualification pénale. C'est la **conscience de franchir une limite** et la décision de **poursuivre malgré tout**.
>
> **EN** - It is not the intrusion that establishes the criminal qualification. It is the **awareness of crossing a boundary** and the decision to **continue regardless**.
 
---
 
##  Chronologie de la bascule / Tipping Point Timeline
 
```
AVANT LA BASCULE                          APRÈS LA BASCULE
(zone neutre)                             (zone de risque pénal)
│                                         │
├── Recherche sur moteur de recherche     ├── Perception du caractère
├── Apparition d'un lien dans             │   confidentiel des documents
│   les résultats                         ├── Décision de poursuivre
└── Clic sur le lien                      │   malgré cette perception
                                          ├── Navigation dans les répertoires
                                          └── Téléchargement des fichiers
                                          
                  ↑
         POINT DE BASCULE :
    perception du signal de restriction
```
 
---
 
##  Impact direct sur l'OSINT / Direct Impact on OSINT
 
### Ce que l'arrêt change concrètement
 
**FR** - Avant Bluetouff, il était possible d'argumenter qu'un système accessible sans protection active était "ouvert" et donc librement consultable. Bluetouff ferme définitivement cet argument. La ligne de démarcation n'est pas technique - elle est cognitive : **à partir du moment où l'enquêteur perçoit que le contenu n'était pas destiné au public, poursuivre devient risqué.**
 
**EN** - Before Bluetouff, it was possible to argue that a system accessible without active protection was "open" and therefore freely consultable. Bluetouff definitively closes this argument. The dividing line is not technical - it is cognitive: **from the moment the investigator perceives that the content was not intended for the public, continuing becomes risky.**
 
---
 
### Application pratique par type de technique
 
| Technique OSINT | Signal de restriction possible | Risque après Bluetouff |
|---|---|---|
| Dorking - répertoires exposés | robots.txt, structure interne, nature des fichiers |  Élevé si poursuite consciente |
| Dorking - fichiers de config | Contenu manifestement interne (.env, credentials) |  Très élevé |
| Consultation via URL directe | Nature confidentielle du document |  Élevé si téléchargement |
| Accès à une interface admin exposée | Interface clairement restreinte |  Très élevé |
| Navigation dans un répertoire listé | Absence de page d'accueil, structure interne |  Dépend du contenu |
 
---
 
### Les signaux de restriction post-Bluetouff
 
**FR** - L'arrêt n'établit pas une liste exhaustive des signaux de restriction. Il pose un principe : tout indice permettant à l'enquêteur de comprendre que le contenu n'est pas destiné au public peut constituer ce signal. En pratique :
 
**EN** - The ruling does not establish an exhaustive list of restriction signals. It establishes a principle: any indication allowing the investigator to understand that the content is not intended for the public can constitute such a signal. In practice:
 
```
Signaux reconnus comme pertinents post-Bluetouff :
 
TECHNIQUES
├── robots.txt excluant la ressource
├── Absence de lien depuis les pages publiques du site
├── Structure d'URL suggérant un usage interne (/admin/, /backup/, /internal/)
└── Mesures anti-bot (même contournables)
 
CONTEXTUELS
├── Nature des documents (RH, finances, configuration, données médicales)
├── Mentions de confidentialité dans les fichiers
├── Structure manifestement interne (organigrammes, notes internes)
└── Données d'accès ou credentials présents dans les fichiers
```
 
---
 
##  Lien avec d'autres textes et décisions / Links to Other Texts and Decisions
 
| Texte / Décision | Lien avec Bluetouff |
|---|---|
| Art. 323-1 C. pén. | Fondement de la condamnation - maintien frauduleux |
| Loi Godfrain (1988) | Origine historique de l'art. 323-1 |
| IDOR (failles d'accès) | Même raisonnement : conscience de franchir une limite |
| Dorking sur contenu restreint | Application directe du raisonnement Bluetouff |
| Cass. ass. plén., 22 déc. 2023 | Complète Bluetouff sur la recevabilité de la preuve obtenue |
 
---
 
##  Doctrine / Doctrine
 
**FR** - L'arrêt Bluetouff est régulièrement cité dans la doctrine pénaliste française spécialisée en cybercriminalité pour illustrer que le critère de la fraude informatique est **subjectif** - il repose sur l'état de connaissance de l'auteur, pas sur la sophistication de ses moyens techniques. Romain Ollard souligne à ce propos que le critère décisif est l'intention manifeste du maître du système de restreindre l'accès, et non l'existence d'une protection technique effective.
 
**EN** - The Bluetouff ruling is regularly cited in French criminal doctrine specializing in cybercrime to illustrate that the criterion for computer fraud is **subjective** - it rests on the perpetrator's state of knowledge, not on the sophistication of their technical means.
 
> Source : Ollard R., *Ordre et désordres du droit pénal (spécial) de la cybercriminalité*, Lexbase, La Lettre juridique, n° 946, 5 oct. 2023.  
 
---
 
##  Références / References
 
- Cass. crim., 20 mai 2015, n° 14-81.336, Bull. crim. 2015, n° 113
- C. pén., art. 323-1
- Loi n° 88-19 du 5 janv. 1988 (loi Godfrain)
- Ollard R., *Ordre et désordres du droit pénal (spécial) de la cybercriminalité*,
  Lexbase, n° 946, 5 oct. 2023
 
---
