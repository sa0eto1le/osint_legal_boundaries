# Port Scanning - Reconnaissance réseau : techniques et limites juridiques
 
> **FR** - Fiche technique et juridique : reconnaissance réseau en OSINT, distinction passive/active, exemples complets avec outputs, et qualification pénale associée.  
> **EN** - Technical and legal fact sheet: network reconnaissance in OSINT, passive/active distinction, full examples with outputs, and associated criminal qualification.
 
---
 
##  Définition / Definition
 
**FR** - Le balayage de ports (port scanning) consiste à envoyer des paquets vers les ports d'une machine cible afin d'analyser les réponses et déterminer l'état de ces ports : ouvert, fermé ou filtré. Chaque port correspond à un service réseau spécifique. Identifier les ports ouverts permet de cartographier les services exposés sur un système.
 
**EN** - Port scanning consists of sending packets to a target machine's ports to analyze responses and determine port states: open, closed, or filtered. Each port corresponds to a specific network service. Identifying open ports maps the services exposed on a system.
 
> Source : ANSSI, CyberDico, entrée « Balayage de ports / Port scanning ».  
 
---
 
##  Distinction fondamentale : reconnaissance passive vs active
 
**FR** - Cette distinction est **juridiquement déterminante**. Elle conditionne la qualification applicable sous l'art. 323-1 C. pén.
 
**EN** - This distinction is **legally decisive**. It conditions the applicable qualification under art. 323-1 French Penal Code.
 
```
RECONNAISSANCE PASSIVE                    RECONNAISSANCE ACTIVE
│                                         │
├── Consultation de données déjà          ├── Envoi de paquets vers la cible
│   indexées par un tiers                 ├── Contact direct avec le système
├── Aucun paquet envoyé vers la cible     ├── La cible reçoit et répond aux requêtes
├── Exemples : Shodan, Censys,            ├── Exemples : Nmap, Masscan,
│   FOFA, GreyNoise                       │   Zmap, Netcat
│                                         │
→ Comparable à la lecture d'un           → Contact direct avec le système
  annuaire public                          cible - qualification pénale
                                           potentielle sans autorisation
```
 
---
 
##  Reconnaissance passive - Shodan
 
**FR** - Shodan est un moteur de recherche qui indexe les services et bannières exposés sur internet. L'utilisateur interroge la base de données de Shodan - il n'envoie aucun paquet vers la cible.
 
**EN** - Shodan is a search engine that indexes services and banners exposed on the internet. The user queries Shodan's database - no packets are sent to the target.
 
> Source : Shodan, *What is Shodan?*  
 
### Requêtes Shodan / Shodan Queries
 
```bash
# Recherche par IP
shodan host 93.184.216.34
 
# Recherche par organisation
shodan search org:"exemple"
 
# Recherche par service spécifique
shodan search product:nginx version:1.18.0
 
# Recherche de services vulnérables (via CLI)
shodan search vuln:CVE-2021-44228      # Log4Shell
 
# Recherche de bannières spécifiques
shodan search "MongoDB Server Information" port:27017
 
# Via l'interface web - filtres utiles
port:22 country:FR                     # SSH exposés en France
port:3389 os:"Windows"                 # RDP Windows exposés
port:27017 -authentication             # MongoDB sans authentification
```
 
**Output typique `shodan host` :**
```
93.184.216.34
City:                    Norwell
Country:                 United States
Organisation:            EDGECAST
 
Open ports: 80, 443
 
Port 80/tcp
└── HTTP/1.1 200 OK
    Server: ECS (dcb/7F37)
    Content-Type: text/html; charset=UTF-8
 
Port 443/tcp
└── HTTP/1.1 200 OK
    Server: ECS (dcb/7F84)
    SSL Certificate:
        Subject: CN=www.example.com
        Issuer: DigiCert TLS RSA SHA256 2020 CA1
        Expires: 2024-03-01
```
 
**Output typique MongoDB sans auth :**
```
Port 27017/tcp - MongoDB
{
  "version": "4.4.6",
  "databases": ["users", "orders", "analytics"],   ← bases accessibles
  "authentication": false                           ← pas d'authentification
}
```
 
---
 
##  Reconnaissance active - Nmap
 
**FR** - Nmap (Network Mapper) est un outil open source de découverte réseau et d'audit de sécurité. Il envoie des paquets vers la cible et analyse les réponses pour identifier les ports ouverts, les services actifs et leurs versions.
 
**EN** - Nmap is an open source network discovery and security auditing tool. It sends packets to the target and analyzes responses to identify open ports, active services, and their versions.
 
> Source : Lyon G. F., *Nmap Network Scanning*, Insecure.Com LLC, 2009.  
 
### Commandes Nmap / Nmap Commands
 
```bash
# Scan basique des ports les plus courants
nmap -sV -p 22,80,443,8080,3306,5432 cible.exemple.com
 
# Scan des 1000 ports les plus courants avec détection de version
nmap -sV cible.exemple.com
 
# Scan complet avec détection OS et scripts par défaut
nmap -A -T4 cible.exemple.com
 
# Scan silencieux (SYN scan - moins visible dans les logs)
nmap -sS cible.exemple.com
 
# Scan UDP
nmap -sU --top-ports 100 cible.exemple.com
 
# Scan d'un réseau entier (CIDR)
nmap -sV 192.168.1.0/24
 
# Détection de vulnérabilités via scripts NSE
nmap --script vuln cible.exemple.com
nmap --script http-shellshock cible.exemple.com
```
 
**Output typique `nmap -sV -A` :**
```
Starting Nmap 7.94 ( https://nmap.org )
Nmap scan report for cible.exemple.com (203.0.113.42)
Host is up (0.023s latency).
 
PORT     STATE  SERVICE    VERSION
22/tcp   open   ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.5
| ssh-hostkey:
|   3072 xx:xx:xx:xx (RSA)
|_  256 xx:xx:xx:xx (ED25519)
80/tcp   open   http       nginx 1.18.0 (Ubuntu)
|_http-title: Exemple Corp - Accueil
|_http-server-header: nginx/1.18.0 (Ubuntu)
443/tcp  open   ssl/https  nginx 1.18.0
| ssl-cert:
|   Subject: CN=exemple.com
|   Not valid after:  2024-06-15          ← certificat expirant bientôt
3306/tcp open   mysql      MySQL 5.7.39
| mysql-info:
|   Protocol: 10
|   Version: 5.7.39-log
|_  Status: Autocommit
8080/tcp open   http       Apache Tomcat 9.0.58
|_http-title: Apache Tomcat/9.0.58        ← interface par défaut non configurée
 
OS details: Linux 4.15 - 5.6
 
Service detection performed.
```
 
**Output typique `--script vuln` :**
```
PORT   STATE SERVICE
80/tcp open  http
| http-vuln-cve2017-5638:
|   VULNERABLE:
|   Apache Struts Remote Code Execution (CVE-2017-5638)
|     State: VULNERABLE
|     Risk factor: HIGH
|_    Description: Remote code execution via Content-Type header
```
 
---
 
##  Cadre juridique / Legal Framework
 
### L'absence de frontière claire en droit positif français
 
**FR** - L'article 323-1 C. pén. ne mentionne pas explicitement le port scanning. La qualification dépend de l'analyse cas par cas des éléments suivants :
 
**EN** - Article 323-1 French Penal Code does not explicitly mention port scanning. Qualification depends on case-by-case analysis of the following elements:
 
```
Facteurs d'analyse :
│
├── 1. AUTORISATION
│   └── Scan réalisé avec autorisation écrite du propriétaire du système ?
│        Oui → Activité légitime (pentest, audit, bug bounty)
│        Non → Risque pénal art. 323-1
│
├── 2. TYPE DE RECONNAISSANCE
│   └── Passive (Shodan) → risque moindre, données déjà publiques
│   └── Active (Nmap) → contact direct avec la cible → risque plus élevé
│
├── 3. INTENTION MANIFESTE DE RESTRICTION
│   └── Le système présente-t-il des signaux de restriction ?
│       (firewall, IDS, bannière interdisant les scans, CGU)
│       → Percevoir ces signaux et poursuivre = maintien frauduleux potentiel
│
└── 4. USAGE DES RÉSULTATS
    └── Documenter pour signalement responsable → contexte atténuant
    └── Exploiter les vulnérabilités identifiées → aggravation certaine
```
 
---
 
### Tableau de qualification / Qualification Table
 
| Situation | Qualification |
|---|---|
| Shodan - consultation passive sans contact cible |  Pas d'infraction a priori |
| Nmap sur son propre système ou réseau |  Légitime |
| Nmap dans le cadre d'un pentest avec mandat écrit |  Légitime - documenter le mandat |
| Nmap sur un système tiers sans autorisation |  Art. 323-1 C. pén. potentiel |
| Nmap + exploitation des vulnérabilités identifiées |  Art. 323-1 + 323-3 C. pén. |
| Scan automatisé massif perturbant le service |  Art. 323-2 C. pén. (entrave) |
 
---
 
### Le cadre PASSI - référence de bonne pratique
 
**FR** - L'ANSSI a mis en place le dispositif PASSI (Prestataires d'Audit de la Sécurité des Systèmes d'Information) qui définit les exigences applicables aux prestataires réalisant des audits de sécurité. Ce référentiel impose notamment une méthodologie documentée, la qualification du personnel et la traçabilité des interventions.
 
Bien que la qualification PASSI ne confère pas d'immunité pénale automatique, elle constitue un indicateur fort de bonne foi et d'absence d'intention frauduleuse - deux éléments déterminants dans l'appréciation judiciaire de l'art. 323-1.
 
**EN** - The ANSSI established the PASSI framework (Security Audit Service Providers) defining requirements for providers conducting security audits. While PASSI qualification does not confer automatic criminal immunity, it constitutes a strong indicator of good faith and absence of fraudulent intent.
 
> Source : ANSSI, Référentiel PASSI.  
 
---
 
### Droit comparé / Comparative Law
 
```
FRANCE - Art. 323-1 C. pén.
└── Pas de seuil technique défini
└── Critère : intention de restriction du maître du système
└── Zone grise persistante pour le scan sans exploitation
 
ÉTATS-UNIS - CFAA (18 U.S.C. § 1030)
└── "Unauthorized access" ou "exceeds authorized access"
└── Débat doctrinal sur la définition de "non autorisé"
└── Van Buren v. United States (2021) : la SCOTUS a restreint
    la portée du "exceeds authorized access"
    → Source : Van Buren v. United States, 593 U.S. 374 (2021)
 
ROYAUME-UNI - Computer Misuse Act 1990
└── Incrimination comparable
└── Les tribunaux ont progressivement admis certaines activités
    de recherche en cybersécurité sous "motif raisonnable"
```
 
---
 
##  Ports de référence / Reference Ports
 
**FR** - Connaître les ports standards permet d'interpréter rapidement un output de scan.  
**EN** - Knowing standard ports allows quick interpretation of scan output.
 
> Source : IANA, Service Name and Transport Protocol Port Number Registry.  
 
```
PORT    PROTOCOLE    SERVICE
21      TCP          FTP - transfert de fichiers (non chiffré)
22      TCP          SSH - accès distant sécurisé
23      TCP          Telnet - accès distant non chiffré (obsolète)
25      TCP          SMTP - envoi de mail
53      TCP/UDP      DNS - résolution de noms
80      TCP          HTTP - web non chiffré
110     TCP          POP3 - récupération mail
143     TCP          IMAP - récupération mail
443     TCP          HTTPS - web chiffré
445     TCP          SMB - partage de fichiers Windows
3306    TCP          MySQL - base de données
3389    TCP          RDP - bureau distant Windows
5432    TCP          PostgreSQL - base de données
5900    TCP          VNC - bureau distant
6379    TCP          Redis - base de données en mémoire
8080    TCP          HTTP alternatif / interfaces d'admin
8443    TCP          HTTPS alternatif
27017   TCP          MongoDB - base de données NoSQL
```
 
---
 
##  Bonnes pratiques / Best Practices
 
```markdown
AVANT TOUT SCAN ACTIF
[ ] Autorisation écrite du propriétaire du système obtenue
[ ] Périmètre du scan défini et documenté
[ ] Objectif de l'audit documenté (finalité légitime)
 
PENDANT LE SCAN
[ ] Limiter l'intensité pour ne pas perturber le service (éviter art. 323-2)
[ ] Horodater chaque opération
[ ] Conserver les outputs bruts pour traçabilité
 
APRÈS LE SCAN
[ ] Ne pas exploiter les vulnérabilités identifiées sans autorisation
[ ] Signalement responsable si vulnérabilité critique découverte
[ ] Rapport documenté conservé
[ ] Données supprimées si périmètre personnel non concerné
```
 
---
 
##  Références / References
 
- ANSSI, CyberDico, entrée « Balayage de ports / Port scanning »
- ANSSI, Référentiel PASSI
- IANA, Service Name and Transport Protocol Port Number Registry
- Lyon G. F., *Nmap Network Scanning*, Insecure.Com LLC, 2009
- Shodan, *What is Shodan?*
- C. pén., art. 323-1, 323-2, 323-3
- Computer Fraud and Abuse Act (CFAA), 18 U.S.C. § 1030
- Van Buren v. United States, 593 U.S. 374 (2021)
 
---
