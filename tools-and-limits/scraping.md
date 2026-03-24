# Web Scraping - Moissonnage automatisé : techniques et limites juridiques
 
> **FR** - Fiche technique et juridique : scraping en OSINT, exemples complets avec outputs, conformité RGPD et qualification pénale associée.  
> **EN** - Technical and legal fact sheet: scraping in OSINT, full examples with outputs, GDPR compliance, and associated criminal qualification.
 
---
 
##  Définition / Definition
 
**FR** - Le web scraping (ou moissonnage) consiste à extraire automatiquement des données depuis des sites web en imitant le comportement d'un navigateur ou en interrogeant directement les ressources d'un serveur. Contrairement à une API qui fournit des données dans un format structuré prévu à cet effet, le scraping récupère des contenus depuis des pages HTML ou des endpoints non documentés.
 
**EN** - Web scraping consists of automatically extracting data from websites by mimicking browser behavior or directly querying server resources. Unlike an API that provides data in a structured format intended for this purpose, scraping retrieves content from HTML pages or undocumented endpoints.
 
> Source : CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025.  
 
---
 
##  Distinction fondamentale : API vs Scraping
 
**FR** - Cette distinction est importante juridiquement : une API est un canal **prévu et autorisé** par l'éditeur pour accéder à ses données. Le scraping contourne ce canal ou opère là où aucun canal officiel n'existe.
 
**EN** - This distinction matters legally: an API is a channel **intended and authorized** by the publisher to access its data. Scraping bypasses this channel or operates where no official channel exists.
 
```
API (canal autorisé)                     SCRAPING (canal non prévu)
│                                        │
├── Endpoint documenté                   ├── Parsing HTML ou endpoints
├── Conditions d'utilisation             │   non documentés
│   définies par l'éditeur               ├── Imitation d'un navigateur
├── Format structuré (JSON, XML)         ├── Contournement possible
├── Rate limiting prévu                  │   des mesures anti-bot
└── Clé API = authentification           └── Pas d'autorisation explicite
    et traçabilité                           de l'éditeur
```
 
---
 
##  Exemples complets avec outputs / Full Examples with Outputs
 
### 1. Scraping HTML basique - Python / BeautifulSoup
 
```python
import requests
from bs4 import BeautifulSoup
import time
 
url = "https://exemple.com/annuaire"
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36"
}
 
response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")
 
# Extraction des contacts
contacts = []
for card in soup.find_all("div", class_="contact-card"):
    nom = card.find("h2", class_="nom").text.strip()
    email = card.find("a", class_="email").text.strip()
    telephone = card.find("span", class_="tel").text.strip()
    contacts.append({"nom": nom, "email": email, "telephone": telephone})
 
print(contacts)
```
 
**Output typique / Typical output :**
```json
[
  {"nom": "Marie Dupont", "email": "m.dupont@exemple.com", "telephone": "+33 6 12 34 56 78"},
  {"nom": "Jean Martin", "email": "j.martin@exemple.com", "telephone": "+33 6 98 76 54 32"},
  {"nom": "Sophie Bernard", "email": "s.bernard@exemple.com", "telephone": "+33 7 11 22 33 44"}
]
```
 
>  **Dès que ce résultat contient des données à caractère personnel, le RGPD s'applique** - indépendamment du fait que ces données soient publiques sur le site.
 
---
 
### 2. Scraping avec contournement de mesures anti-bot
 
```python
import requests
from bs4 import BeautifulSoup
import time
import random
 
# Rotation de User-Agents pour imiter différents navigateurs
user_agents = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36",
    "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36",
    "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36"
]
 
# Délai aléatoire entre les requêtes pour imiter un comportement humain
def scrape_with_delay(urls):
    results = []
    for url in urls:
        headers = {"User-Agent": random.choice(user_agents)}
        response = requests.get(url, headers=headers)
        # Traitement...
        time.sleep(random.uniform(1.5, 4.0))    # délai aléatoire
    return results
```
 
>  **Ce type de code contourne délibérément les mesures anti-bot.** La CNIL précise dans sa fiche de juin 2025 que le respect des mécanismes d'opposition - dont les mesures anti-bot - est une condition de conformité au RGPD. Contourner ces mesures fragilise la base légale et peut caractériser une intention d'accès non autorisé au regard de l'art. 323-1 C. pén.
 
---
 
### 3. Scraping de réseaux sociaux - LinkedIn (cas KASPR)
 
```python
import requests
 
# Endpoint non documenté LinkedIn (exemple illustratif)
headers = {
    "Authorization": "Bearer TOKEN_SESSION",
    "User-Agent": "LinkedIn/...",
    "Csrf-Token": "ajax:XXXX"
}
 
# Récupération des coordonnées d'un profil
response = requests.get(
    "https://www.linkedin.com/voyager/api/identity/profiles/jdupont/profileContactInfo",
    headers=headers
)
 
data = response.json()
```
 
**Output typique / Typical output :**
```json
{
  "emailAddress": "jean.dupont@entreprise.com",
  "phoneNumbers": [{"number": "+33612345678", "type": "MOBILE"}],
  "twitterHandles": [{"name": "jdupont_pro"}],
  "websites": [{"url": "https://jdupont.com"}]
}
```
 
>  **C'est exactement ce que faisait KASPR.** La CNIL a sanctionné cette pratique à hauteur de **240 000€** (délibération du 5 déc. 2024) : les utilisateurs avaient restreint la visibilité de ces données à leurs connexions. La collecte via un endpoint non autorisé, même techniquement accessible, viole le RGPD et les CGU de la plateforme.  
> Source : CNIL, délibération KASPR, 5 déc. 2024.  
 
---
 
### 4. Scraping massif d'images - cas Clearview AI
 
```python
# Architecture simplifiée du scraping massif de Clearview AI (illustratif)
 
import requests
from urllib.parse import urljoin
import face_recognition    # extraction d'embeddings faciaux
 
def scrape_and_embed(image_url):
    response = requests.get(image_url)
    image = face_recognition.load_image_file(image_url)
    
    # Extraction de l'embedding facial
    embeddings = face_recognition.face_encodings(image)
    
    if embeddings:
        return {
            "source_url": image_url,
            "embedding": embeddings[0].tolist()    # vecteur biométrique
        }
```
 
>  **Cette architecture est catégoriquement interdite depuis le 2 février 2025** par l'art. 5 §1 e) de l'AI Act, indépendamment du RGPD. La CNIL avait déjà sanctionné Clearview AI à hauteur de **20M€** en 2022 sur le fondement du RGPD seul.  
> Voir [ai-act-biometrie.md](ai-act-biometrie.md) pour l'analyse complète.
 
---
 
### 5. Scraping via robots.txt - vérification préalable
 
```python
import urllib.robotparser
 
def check_robots(url, user_agent="*"):
    """
    Vérifie si le scraping d'une URL est autorisé par le robots.txt
    """
    rp = urllib.robotparser.RobotFileParser()
    
    # Construire l'URL du robots.txt
    from urllib.parse import urlparse
    parsed = urlparse(url)
    robots_url = f"{parsed.scheme}://{parsed.netloc}/robots.txt"
    
    rp.set_url(robots_url)
    rp.read()
    
    allowed = rp.can_fetch(user_agent, url)
    crawl_delay = rp.crawl_delay(user_agent)
    
    return {
        "url": url,
        "robots_url": robots_url,
        "allowed": allowed,
        "crawl_delay": crawl_delay
    }
 
# Exemple d'utilisation
result = check_robots("https://exemple.com/annuaire/")
print(result)
```
 
**Output typique / Typical output :**
```json
{
  "url": "https://exemple.com/annuaire/",
  "robots_url": "https://exemple.com/robots.txt",
  "allowed": false,         ← scraping non autorisé par le robots.txt
  "crawl_delay": 10
}
```
 
>  **Bonne pratique** : intégrer cette vérification systématiquement avant tout scraping. Un résultat `allowed: false` est un signal de restriction explicite - poursuivre fragilise la base légale et expose au risque pénal.
 
---
 
##  Cadre juridique / Legal Framework
 
### RGPD - Les conditions de la CNIL (juin 2025)
 
**FR** - La CNIL a publié en juin 2025 une fiche focus sur la base légale de l'intérêt légitime appliquée au scraping. Elle précise que le scraping n'est pas illégal par principe, mais qu'il exige le respect de conditions cumulatives.
 
**EN** - The CNIL published in June 2025 a focus note on the legitimate interest legal basis applied to scraping. It clarifies that scraping is not illegal in principle, but requires compliance with cumulative conditions.
 
> Source : CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025.  
 
```
CONDITIONS CUMULATIVES CNIL (juin 2025) :
 
1. Finalité légitime documentée avant la collecte
2. Nécessité démontrée du scraping pour atteindre cette finalité
3. Mise en balance documentée (intérêt poursuivi vs droits des personnes)
4. Respect des signaux d'opposition :
   └── robots.txt
   └── Mesures anti-bot
   └── Mécanismes d'opposition des personnes
5. Filtrage en amont avant toute conservation
6. Durée de conservation limitée et justifiée
7. Sécurité des données collectées assurée
```
 
---
 
### Tableau de qualification / Qualification Table
 
| Situation | Qualification |
|---|---|
| Scraping de données publiques avec finalité définie + robots.txt respecté |  Possible si conditions CNIL respectées |
| Scraping avec contournement délibéré des mesures anti-bot |  Fragilise base légale RGPD + risque art. 323-1 |
| Scraping d'un espace nécessitant une authentification |  Art. 323-1 C. pén. |
| Scraping de données biométriques (photos → embeddings) |  AI Act art. 5 §1 e) + RGPD art. 9 |
| Scraping de données dont la visibilité est restreinte (cas KASPR) |  RGPD + CGU - sanctions CNIL |
| Scraping dans le cadre d'une API publique respectant les CGU |  Légitime si CGU respectées |
 
---
 
### CGU et responsabilité contractuelle
 
**FR** - Les conditions générales d'utilisation (CGU) des plateformes interdisent généralement le scraping automatisé. Leur violation ne constitue pas en elle-même une infraction pénale, mais engage la **responsabilité civile contractuelle** de l'auteur (art. 1240 C. civ.). Elle peut également constituer un indice d'intention dans l'appréciation de l'art. 323-1 C. pén.
 
**EN** - Terms of Service (ToS) of platforms generally prohibit automated scraping. Their violation does not in itself constitute a criminal offense, but engages the **contractual civil liability** of the author (art. 1240 French Civil Code). It may also constitute an intent indicator in the assessment of art. 323-1 French Penal Code.
 
---
 
### Droit sui generis des bases de données - Directive 96/9/CE
 
**FR** - La directive européenne 96/9/CE du 11 mars 1996 sur la protection juridique des bases de données instaure un **droit sui generis** pour le producteur d'une base de données ayant réalisé un investissement substantiel. Ce droit interdit l'extraction ou la réutilisation d'une partie substantielle du contenu de la base sans autorisation, indépendamment du droit d'auteur.
 
En OSINT, scraper une base de données structurée - même si son contenu est accessible publiquement - peut violer ce droit sui generis si l'extraction porte sur une partie substantielle.
 
**EN** - EU Directive 96/9/EC of 11 March 1996 on the legal protection of databases establishes a **sui generis right** for the database producer who made a substantial investment. This right prohibits extraction or re-utilization of a substantial part of the database content without authorization, independently of copyright.
 
> Source : Directive 96/9/CE du Parlement européen et du Conseil du 11 mars 1996 concernant la protection juridique des bases de données, JOCE L 77 du 27 mars 1996.
 
---
 
##  Bonnes pratiques / Best Practices
 
```markdown
AVANT TOUT SCRAPING
[ ] Vérifier l'existence d'une API officielle - la privilégier si disponible
[ ] Lire et respecter les CGU de la plateforme ciblée
[ ] Vérifier le robots.txt et respecter les directives
[ ] Définir et documenter la finalité avant de commencer
[ ] Identifier la base légale RGPD applicable
 
PENDANT LE SCRAPING
[ ] Respecter les délais indiqués dans robots.txt (Crawl-delay)
[ ] Ne pas contourner les mesures anti-bot (CAPTCHA, rate limiting)
[ ] Limiter strictement aux données nécessaires à la finalité
[ ] Horodater et tracer chaque session
 
APRÈS LE SCRAPING
[ ] Filtrer et supprimer les données non nécessaires immédiatement
[ ] Documenter la mise en balance (intérêt légitime vs droits des personnes)
[ ] Respecter la durée de conservation définie
[ ] Évaluer l'obligation d'information art. 14 RGPD
```
 
---
 
##  Références / References
 
- CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025
- CNIL, délibération KASPR, 5 déc. 2024
- EDPB, *The French SA fines Clearview AI EUR 20 million*, 20 oct. 2022
- Directive 96/9/CE du 11 mars 1996 - protection juridique des bases de données
- Règlement (UE) 2016/679 - RGPD, art. 5, 6, 9, 14, 32
- Règlement (UE) 2024/1689 - AI Act, art. 5 §1 e)
- IETF, RFC 9309 – Robots Exclusion Protocol
- C. pén., art. 323-1
- C. civ., art. 1240
 
---
