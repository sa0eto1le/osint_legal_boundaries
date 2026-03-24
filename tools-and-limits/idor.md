
# IDOR - Insecure Direct Object Reference : techniques et limites juridiques
 
> **FR** - Fiche technique et juridique : détection des failles IDOR en OSINT, exemples complets avec outputs, et qualification pénale associée.  
> **EN** - Technical and legal fact sheet: IDOR vulnerability detection in OSINT, full examples with outputs, and associated criminal qualification.
 
---
 
##  Définition / Definition
 
**FR** - Une faille IDOR (Insecure Direct Object Reference) survient lorsqu'une application expose une référence directe à un objet interne - identifiant de base de données, nom de fichier, clé - sans vérifier si l'utilisateur est autorisé à y accéder. En manipulant ces références dans une requête, il est possible d'accéder à des ressources appartenant à d'autres utilisateurs.
 
**EN** - An IDOR (Insecure Direct Object Reference) vulnerability occurs when an application exposes a direct reference to an internal object - database ID, filename, key - without verifying whether the user is authorized to access it. By manipulating these references in a request, it is possible to access resources belonging to other users.
 
> Source : OWASP Foundation, *Insecure Direct Object Reference Prevention Cheat Sheet*.  
 
> Source : OWASP Top 10, *A01:2021 - Broken Access Control*.  
 
---
 
##  Fonctionnement technique / Technical Mechanism
 
**FR** - Le principe repose sur l'absence ou l'insuffisance de contrôle d'accès côté serveur. L'application fait confiance à l'identifiant fourni par l'utilisateur sans vérifier si cet utilisateur a le droit d'accéder à la ressource correspondante.
 
**EN** - The principle rests on the absence or insufficiency of server-side access control. The application trusts the identifier provided by the user without verifying whether that user has the right to access the corresponding resource.
 
```
FLUX NORMAL (avec contrôle d'accès)          FLUX IDOR (sans contrôle d'accès)
│                                             │
├── Utilisateur → GET /facture?id=1234        ├── Utilisateur → GET /facture?id=1235
├── Serveur vérifie :                         ├── Serveur NE vérifie PAS :
│   "cet utilisateur possède-t-il            │   "cet utilisateur possède-t-il
│    la facture 1234 ?"                       │    la facture 1235 ?"
├── Oui → retourne la facture                 ├── Retourne directement la facture
└── Non → 403 Forbidden                       └── d'un autre utilisateur ← IDOR
```
 
---
 
##  Exemples complets avec outputs / Full Examples with Outputs
 
### 1. IDOR dans les paramètres d'URL
 
**FR** - Le vecteur le plus courant : l'identifiant est passé directement dans l'URL en paramètre GET.  
**EN** - The most common vector: the identifier is passed directly in the URL as a GET parameter.
 
```
# Accès légitime
GET https://exemple.com/facture?id=1234
→ Retourne la facture de l'utilisateur connecté
 
# Manipulation IDOR
GET https://exemple.com/facture?id=1235
GET https://exemple.com/facture?id=1236
GET https://exemple.com/facture?id=1237
```
 
**Output typique / Typical output :**
```json
{
  "id": 1235,
  "client": "Dupont SA",
  "date": "2024-01-15",
  "montant": 4800.00,
  "iban": "FR76 3000 6000 0112 3456 7890 189",
  "contact": "jean.dupont@dupont-sa.fr",
  "adresse": "12 rue de la Paix, 75001 Paris"
}
```
 
---
 
### 2. IDOR dans le chemin d'URL (Path Traversal IDOR)
 
```
# Accès légitime
GET https://exemple.com/api/users/42/profil
 
# Manipulation IDOR
GET https://exemple.com/api/users/43/profil
GET https://exemple.com/api/users/1/profil    ← profil administrateur
```
 
**Output typique profil admin :**
```json
{
  "id": 1,
  "username": "admin",
  "email": "admin@exemple.com",
  "role": "superadmin",
  "created_at": "2019-03-01",
  "last_login": "2024-01-20T09:34:12Z",
  "api_key": "sk_prod_xxxxxxxxxxxxxxxxxxxx"    ← clé API administrative
}
```
 
---
 
### 3. IDOR dans les requêtes POST / corps de requête
 
**FR** - L'identifiant n'est pas toujours visible dans l'URL - il peut être dans le corps d'une requête POST, interceptable via un proxy comme Burp Suite.
 
**EN** - The identifier is not always visible in the URL - it may be in the body of a POST request, interceptable via a proxy like Burp Suite.
 
```http
# Requête originale
POST /api/download-document HTTP/1.1
Host: exemple.com
Content-Type: application/json
Cookie: session=eyJhbGc...
 
{
  "document_id": "DOC-2024-0042",
  "user_id": "789"
}
 
# Manipulation IDOR - modification du document_id et user_id
{
  "document_id": "DOC-2024-0001",    ← document d'un autre utilisateur
  "user_id": "1"                     ← identifiant administrateur
}
```
 
---
 
### 4. IDOR dans les références de fichiers
 
```
# Accès à son propre document
GET https://exemple.com/documents/contrat_dupont_2024.pdf
 
# Manipulation IDOR - énumération de fichiers prévisibles
GET https://exemple.com/documents/contrat_martin_2024.pdf
GET https://exemple.com/documents/contrat_durand_2024.pdf
GET https://exemple.com/documents/contrat_admin_2024.pdf
 
# Ou avec identifiants numériques
GET https://exemple.com/export/rapport_2024_001.csv
GET https://exemple.com/export/rapport_2024_002.csv
```
 
---
 
### 5. IDOR dans les APIs (cas fréquent en OSINT)
 
```http
# Endpoint légitime - récupère ses propres données
GET /api/v1/users/me/orders HTTP/1.1
Authorization: Bearer eyJhbGc...
 
# Manipulation IDOR - accès aux commandes d'autres utilisateurs
GET /api/v1/users/100/orders HTTP/1.1
GET /api/v1/users/101/orders HTTP/1.1
 
# IDOR sur endpoint d'export - cas particulièrement sensible
GET /api/v1/export?user_id=100&format=csv
```
 
**Output typique export CSV :**
```csv
user_id,nom,prenom,email,telephone,adresse,date_naissance
100,Martin,Sophie,s.martin@mail.com,+33612345678,"5 rue Victor Hugo, 69001 Lyon",1985-04-12
```
 
---
 
### 6. Détection automatisée - Intruder (Burp Suite)
 
**FR** - Dans un contexte de pentest autorisé, l'outil Intruder de Burp Suite permet d'automatiser l'énumération d'identifiants pour détecter les failles IDOR à grande échelle.
 
**EN** - In an authorized pentest context, Burp Suite's Intruder tool allows automated enumeration of identifiers to detect IDOR vulnerabilities at scale.
 
```
Configuration Intruder :
├── Position : paramètre id= marqué comme payload position
├── Payload : liste numérique (1 → 10000)
├── Grep - Match : codes HTTP 200 (accès réussi)
└── Grep - Extract : longueur de réponse (variations = données différentes)
 
Résultat :
ID 1234 → 200 OK, 842 bytes  ← propre ressource
ID 1235 → 200 OK, 756 bytes  ← ressource d'un autre utilisateur = IDOR confirmé
ID 1236 → 403 Forbidden      ← accès refusé = contrôle d'accès présent
ID 1237 → 200 OK, 901 bytes  ← IDOR confirmé
```
 
>  **L'automatisation de cette technique sans autorisation constitue une circonstance aggravante** au regard de l'art. 323-1 C. pén. - la répétition caractérise l'intentionnalité.
 
---
 
##  Cadre juridique / Legal Framework
 
### Qualification pénale - Art. 323-1 C. pén.
 
**FR** - La faille IDOR soulève une question juridique centrale : accéder à `id=1235` en changeant manuellement un paramètre constitue-t-il un accès frauduleux à un STAD ?
 
La réponse dépend de plusieurs facteurs, mais le raisonnement de l'arrêt Bluetouff (*Cass. crim., 20 mai 2015, n° 14-81.336*) s'applique directement : **ce n'est pas la sophistication de la méthode qui fonde la qualification, c'est la conscience d'avoir franchi une limite.**
 
**EN** - The IDOR vulnerability raises a central legal question: does accessing `id=1235` by manually changing a parameter constitute unauthorized access to a computer system?
 
The answer depends on several factors, but the Bluetouff reasoning applies directly: **it is not the sophistication of the method that establishes the qualification, it is the awareness of having crossed a boundary.**
 
---
 
### L'IDOR dans la classification OWASP
 
**FR** - L'OWASP (Open Worldwide Application Security Project) classe les failles de contrôle d'accès - dont l'IDOR - en **première position** du Top 10 des vulnérabilités web les plus critiques (A01:2021 - Broken Access Control). Cette classification est reconnue internationalement par la communauté de la cybersécurité et constitue une référence dans les audits de sécurité.
 
**EN** - OWASP classifies access control flaws - including IDOR - in **first position** in the Top 10 most critical web vulnerabilities (A01:2021 - Broken Access Control). This classification is internationally recognized by the cybersecurity community and constitutes a reference in security audits.
 
> Source : OWASP Top 10, *A01:2021 - Broken Access Control*.  
 
---
 
### Tableau de qualification / Qualification Table
 
| Situation | Qualification |
|---|---|
| Découverte fortuite d'un IDOR sans exploitation |  Zone grise - contexte décisif |
| Accès à une ressource via IDOR - première occurrence |  Art. 323-1 C. pén. potentiel |
| Répétition manuelle ou itération automatisée |  Intentionnalité caractérisée |
| Téléchargement ou export de données via IDOR |  Art. 323-1 + 323-3 C. pén. |
| IDOR dans le cadre d'un pentest avec mandat écrit |  Légitime - documenter le mandat |
| Signalement responsable sans exploitation des données |  Démarche défensive - documenter |
 
---
 
### IDOR et RGPD
 
**FR** - Lorsqu'une faille IDOR expose des données à caractère personnel, son exploitation - même involontaire - constitue potentiellement un traitement sans base légale au sens du RGPD (art. 6). Si les données exposées sont sensibles (art. 9), l'infraction est aggravée.
 
Par ailleurs, l'organisation dont le système présente la faille IDOR peut elle-même être en violation du RGPD pour défaut de mesures de sécurité appropriées (art. 32 - sécurité du traitement).
 
**EN** - When an IDOR vulnerability exposes personal data, its exploitation - even unintentional - potentially constitutes processing without a legal basis under GDPR (art. 6). If the exposed data is sensitive (art. 9), the violation is aggravated.
 
---
 
##  Signalement responsable / Responsible Disclosure
 
**FR** - La découverte d'une faille IDOR sur un système tiers sans autorisation place l'analyste dans une situation délicate. La démarche la plus défensive juridiquement est le **signalement responsable** (responsible disclosure) :
 
**EN** - Discovering an IDOR vulnerability on a third-party system without authorization places the analyst in a delicate situation. The most legally defensive approach is **responsible disclosure**:
 
```markdown
PROTOCOLE DE SIGNALEMENT RESPONSABLE
 
[ ] Ne pas exploiter la faille au-delà de la confirmation de son existence
[ ] Ne pas télécharger, copier ou stocker les données exposées
[ ] Documenter la découverte (URL, date, nature de la faille)
    sans conserver les données d'autrui
[ ] Identifier le contact sécurité de l'organisation
    (security.txt, hall of fame, programme bug bounty)
[ ] Notifier l'organisation avec les détails techniques suffisants
    pour reproduire et corriger
[ ] Définir un délai raisonnable avant divulgation publique
    (pratique courante : 90 jours)
[ ] Conserver la trace du signalement et des échanges
```
 
>  En France, la directive NIS2 (art. 12, Directive (UE) 2022/2555) impose aux États membres de mettre en place un dispositif de **divulgation coordonnée des vulnérabilités**. Ce cadre reconnaît implicitement l'utilité des découvertes de failles par des acteurs externes, sans pour autant leur conférer une immunité pénale automatique.
 
---
 
##  Bonnes pratiques / Best Practices
 
```markdown
DANS UN CONTEXTE OSINT
[ ] Ne pas itérer sur les identifiants sans autorisation
[ ] En cas de découverte fortuite : ne pas exploiter, envisager le signalement
[ ] Documenter la méthode de découverte (pour démontrer l'absence d'intention)
 
DANS UN CONTEXTE DE PENTEST AUTORISÉ
[ ] Mandat écrit définissant le périmètre obtenu avant tout test
[ ] Conserver les outputs bruts horodatés
[ ] Rapport de vulnérabilité documenté et transmis au client
[ ] Ne pas exploiter les données personnelles exposées
```
 
---
 
## 📖 Références / References
 
- OWASP Foundation, *Insecure Direct Object Reference Prevention Cheat Sheet*
- OWASP Top 10, *A01:2021 - Broken Access Control*
- Cass. crim., 20 mai 2015, n° 14-81.336 (Bluetouff)
- Directive (UE) 2022/2555 (NIS2), art. 12
- C. pén., art. 323-1, 323-3
- Règlement (UE) 2016/679 - RGPD, art. 6, 9, 32
 
---
