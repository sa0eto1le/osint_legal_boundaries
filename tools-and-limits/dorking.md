# Google Dorking - Recherche avancée : techniques et limites juridiques
 
> **FR** - Fiche technique et juridique : utilisation des opérateurs de recherche avancée en OSINT, exemples complets avec outputs, et qualification pénale associée.  
> **EN** - Technical and legal fact sheet: use of advanced search operators in OSINT, full examples with outputs, and associated criminal qualification.
 
---
 
##  Définition / Definition
 
**FR** - Le dorking (aussi appelé Google Hacking) désigne l'utilisation d'opérateurs de recherche avancée pour affiner les résultats d'un moteur de recherche et faire remonter des contenus spécifiques, parfois exposés par inadvertance. La technique repose sur l'index constitué par le moteur - l'utilisateur n'accède à aucun système directement, il interroge une base de données tierce.
 
**EN** - Dorking (also called Google Hacking) refers to the use of advanced search operators to refine search engine results and surface specific content, sometimes inadvertently exposed. The technique relies on the index built by the search engine - the user does not access any system directly, they query a third-party database.
 
> Source technique : Google, *Search operators*, Google Search Central Documentation.  
 
---
 
##  Opérateurs fondamentaux / Core Operators
 
| Opérateur | Fonction | Exemple |
|---|---|---|
| `site:` | Limite la recherche à un domaine | `site:exemple.com` |
| `filetype:` | Filtre par extension de fichier | `filetype:pdf` |
| `intitle:` | Cherche dans le titre de la page | `intitle:"index of"` |
| `inurl:` | Cherche dans l'URL | `inurl:admin` |
| `intext:` | Cherche dans le corps du texte | `intext:"mot de passe"` |
| `cache:` | Affiche la version en cache | `cache:exemple.com` |
| `"..."` | Recherche de l'expression exacte | `"confidentiel"` |
| `-` | Exclut un terme | `site:exemple.com -www` |
 
---
 
##  Exemples complets avec outputs / Full Examples with Outputs
 
### 1. Répertoires exposés (Directory Listing)
 
**FR** - Certains serveurs web exposent le contenu de leurs répertoires lorsque la configuration ne prévoit pas de page d'accueil. Ces répertoires listés sont indexés par les moteurs de recherche et accessibles via une simple requête.
 
**EN** - Some web servers expose their directory contents when no index page is configured. These listed directories are indexed by search engines and accessible via a simple query.
 
```bash
intitle:"index of" site:exemple.com
intitle:"index of /" "parent directory"
intitle:"index of" "backup"
intitle:"index of" ".env"
```
 
**Output typique / Typical output :**
```
Index of /backup/
[DIR]  archives/          15-Jan-2024
[   ]  config_old.zip     08-Mar-2023   4.2M
[   ]  database_dump.sql  22-Nov-2023   18M    ← dump de base de données
[   ]  .env.bak           01-Dec-2023   2K     ← variables d'environnement
```
 
---
 
### 2. Fichiers de configuration et credentials
 
```bash
# Fichiers .env exposés (variables d'environnement, souvent avec credentials)
filetype:env "DB_PASSWORD"
filetype:env "SECRET_KEY"
 
# Fichiers de configuration exposés
filetype:xml "connectionString"
filetype:cfg "password"
filetype:ini "password" site:exemple.com
 
# Fichiers de log exposés
filetype:log "username" "password"
filetype:log site:exemple.com
```
 
**Output typique / Typical output `.env` :**
```
DB_HOST=localhost
DB_NAME=production_db
DB_USER=admin
DB_PASSWORD=P@ssw0rd2023        ← credentials en clair
SECRET_KEY=sk_live_xxxxxxxxxxxx ← clé API de production
SMTP_PASSWORD=mailpass123
```
 
---
 
### 3. Documents internes et sensibles
 
```bash
# Fichiers Excel avec données sensibles
filetype:xls site:exemple.com "confidentiel"
filetype:xlsx "password" site:exemple.com
filetype:xls intext:"salaire" site:exemple.com
 
# Documents Word internes
filetype:doc "usage interne" site:exemple.com
filetype:docx "ne pas diffuser" site:exemple.com
 
# Présentations internes
filetype:ppt "confidentiel" site:exemple.com
filetype:pptx "internal use only" site:exemple.com
```
 
**Output typique / Typical output :**
```
[XLSX] RH_salaires_2023.xlsx - exemple.com/rh/documents/
[DOC]  compte_rendu_CODIR_mars2024.doc - exemple.com/direction/
[PPT]  strategie_commerciale_2024_CONFIDENTIEL.pptx - exemple.com/sales/
```
 
---
 
### 4. Interfaces d'administration exposées
 
```bash
# Interfaces d'administration web
inurl:admin site:exemple.com
inurl:"/admin/login" site:exemple.com
inurl:"/wp-admin" site:exemple.com
intitle:"phpMyAdmin" site:exemple.com
 
# Interfaces de gestion de bases de données
intitle:"phpMyAdmin" "Welcome to phpMyAdmin"
intitle:"Adminer" inurl:adminer.php
 
# Interfaces de monitoring exposées
intitle:"Grafana" inurl:"/login"
intitle:"Kibana" inurl:":5601"
```
 
**Output typique / Typical output :**
```
exemple.com/admin/login.php        ← interface admin accessible sans auth
exemple.com/phpmyadmin/            ← gestion BDD directement accessible
exemple.com:3000/                  ← Grafana sans authentification
```
 
---
 
### 5. Appareils connectés et services exposés (combinaison Shodan/Dorking)
 
```bash
# Caméras et systèmes de surveillance
intitle:"webcamXP 5" inurl:8080
intitle:"Live View / - AXIS" inurl:view/view.shtml
intitle:"Network Camera" inurl:/view/index.shtml
 
# Imprimantes et équipements réseau
intitle:"HP LaserJet" inurl:SSI/Auth/setpassword.htm
intitle:"RouterOS" inurl:winbox
 
# Panneaux de contrôle industriels (SCADA)
intitle:"SCADA" inurl:login
```
 
>  **Ces requêtes remontent des équipements réels exposés sur internet.** Leur consultation via un moteur de recherche est techniquement passive - mais accéder aux interfaces, même sans authentification, peut constituer un accès frauduleux à un STAD (art. 323-1 C. pén.).
 
---
 
### 6. Fuites de données et fichiers sensibles
 
```bash
# Fichiers SQL exposés
filetype:sql "INSERT INTO" site:exemple.com
filetype:sql "CREATE TABLE" "password"
 
# Fichiers de sauvegarde exposés
filetype:bak site:exemple.com
filetype:backup inurl:backup
ext:bak inurl:"htaccess|passwd|shadow|htusers"
 
# Clés privées et certificats
filetype:pem "PRIVATE KEY"
filetype:key "PRIVATE KEY"
```
 
**Output typique / Typical output SQL :**
```sql
INSERT INTO users (id, username, password, email) VALUES
(1, 'admin', '$2y$10$xxxxxxxxxxxxxxxxxxxx', 'admin@exemple.com'),
(2, 'jdupont', '$2y$10$xxxxxxxxxxxxxxxxxxxx', 'j.dupont@exemple.com');
```
 
---
 
##  Cadre juridique / Legal Framework
 
### La ligne de bascule - Arrêt Bluetouff (Cass. crim., 20 mai 2015)
 
**FR** - La technique du dorking n'implique aucune intrusion technique : l'utilisateur interroge l'index d'un moteur de recherche, pas le système cible. Cette neutralité technique ne dispense cependant pas d'une analyse juridique au cas par cas.
 
L'arrêt Bluetouff (*Cass. crim., 20 mai 2015, n° 14-81.336*) a posé le critère décisif : **c'est la conscience de franchir une limite, et non l'effraction technique, qui fonde la qualification de maintien frauduleux** au sens de l'art. 323-1 C. pén.
 
**EN** - Dorking involves no technical intrusion: the user queries a search engine index, not the target system. This technical neutrality does not exempt from case-by-case legal analysis.
 
The Bluetouff ruling established the decisive criterion: **it is awareness of crossing a boundary, not technical intrusion, that establishes unauthorized persistence** under art. 323-1 French Penal Code.
 
---
 
### Tableau de qualification / Qualification Table
 
| Situation | Signal de restriction | Qualification |
|---|---|---|
| Accéder à une page publique indexée | Aucun |  Pas d'infraction |
| Trouver un répertoire listé via dorking | Aucun signal visible |  Zone grise - contexte décisif |
| Trouver un répertoire listé + robots.txt restrictif | robots.txt exclut ce répertoire |  Maintien frauduleux potentiel si poursuite |
| Trouver des credentials en clair et les utiliser | Contenu manifestement interne |  Accès frauduleux probable |
| Télécharger un dump SQL exposé | Contenu manifestement restreint |  Maintien frauduleux + recel potentiel |
| Accéder à une interface admin sans authentification | Interface clairement restreinte |  Accès frauduleux |
 
---
 
### Le robots.txt - signal juridiquement significatif
 
**FR** - Le fichier robots.txt est défini par l'IETF dans la RFC 9309 (septembre 2022) comme un mécanisme permettant aux administrateurs de sites d'indiquer aux robots d'exploration les ressources qu'ils peuvent consulter. Ce fichier n'est **pas juridiquement contraignant** en lui-même - il ne crée pas d'obligation légale pour les tiers.
 
Cependant, sa présence constitue un **signal d'intention** de restriction de l'accès. Dans le raisonnement Bluetouff, percevoir ce signal et poursuivre la consultation bascule l'acte vers le maintien frauduleux.
 
**EN** - The robots.txt file is defined by the IETF in RFC 9309 (September 2022) as a mechanism allowing site administrators to indicate to crawlers which resources they may access. This file is **not legally binding** in itself. However, its presence constitutes a **restriction intent signal**. In the Bluetouff reasoning, perceiving this signal and continuing consultation shifts the act toward unauthorized persistence.
 
> Source : IETF, RFC 9309 – Robots Exclusion Protocol, sept. 2022.  
 
```
# Exemple de robots.txt
User-agent: *
Disallow: /admin/
Disallow: /backup/
Disallow: /private/
Disallow: /config/
 
→ Accéder à exemple.com/backup/ après avoir consulté ce fichier
  = signal de restriction perçu = risque pénal art. 323-1
```
 
---
 
### RGPD et dorking
 
**FR** - Lorsque le dorking permet de récupérer des données à caractère personnel (noms, emails, numéros de téléphone, etc.), les obligations du RGPD s'appliquent indépendamment de la méthode de collecte. La CNIL a rappelé dans sa fiche de juin 2025 sur le scraping que l'accessibilité technique d'une donnée ne neutralise pas les exigences de finalité, de minimisation et de base légale.
 
**EN** - When dorking retrieves personal data (names, emails, phone numbers, etc.), GDPR obligations apply regardless of the collection method. The CNIL recalled in its June 2025 note on scraping that the technical accessibility of data does not neutralize requirements of purpose, minimization, and legal basis.
 
> Source : CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025.  
 
---
 
##  Bonnes pratiques / Best Practices
 
```markdown
AVANT UNE SESSION DE DORKING
[ ] Finalité définie et documentée
[ ] Périmètre limité aux informations strictement nécessaires
[ ] Vérification du robots.txt des domaines ciblés
 
PENDANT LA SESSION
[ ] Arrêt immédiat si signal de restriction identifié
[ ] Ne pas télécharger de contenu manifestement interne ou restreint
[ ] Ne pas utiliser les credentials ou données d'accès trouvés
[ ] Horodater et archiver les URLs consultées
 
EN CAS DE DÉCOUVERTE SENSIBLE
[ ] Ne pas télécharger, copier ou diffuser
[ ] Envisager un signalement responsable à l'organisation concernée
[ ] Documenter la découverte sans exploiter les données
```
 
---
 
##  Références / References
 
- Google, *Search operators*, Google Search Central Documentation
- Google, *Introduction to robots.txt*, Google Search Central Documentation
- IETF, RFC 9309 – Robots Exclusion Protocol, sept. 2022
- Cass. crim., 20 mai 2015, n° 14-81.336 (Bluetouff)
- CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025
- C. pén., art. 323-1
 
---
