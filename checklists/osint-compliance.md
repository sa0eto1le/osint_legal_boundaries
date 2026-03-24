# Checklist OSINT-Compliant - Avant, pendant et après une enquête
 
> **FR** - Checklist terrain à utiliser avant toute opération de collecte OSINT. Couvre les exigences RGPD, les signaux de restriction, la traçabilité et la gestion post-enquête.  
> **EN** - Field checklist to use before any OSINT collection operation. Covers GDPR requirements, restriction signals, traceability, and post-investigation management.
 
---
 
##  Rappel préliminaire / Preliminary Reminder
 
**FR** - Cette checklist ne constitue pas un avis juridique. Elle synthétise les bonnes pratiques issues des textes en vigueur (RGPD, AI Act, C. pén.) et des recommandations de la CNIL. Elle ne dispense pas d'une analyse au cas par cas selon le contexte de l'enquête.
 
**EN** - This checklist does not constitute legal advice. It synthesizes best practices from current texts (GDPR, AI Act, French Penal Code) and CNIL recommendations. It does not replace case-by-case analysis depending on the investigation context.
 
> Sources principales : CNIL (LINC), *Le renseignement en sources ouvertes*, 5 févr. 2024 ; CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025.
 
---
 
##  PHASE 1 - Avant la collecte / Before Collection
 
### 1.1 Définition de la mission
 
```markdown
[ ] La finalité de l'enquête est définie avec précision avant tout début de collecte
    → "Vérifier l'identité de X" ≠ "Collecter tout ce qui existe sur X"
 
[ ] La finalité est légitime et documentée par écrit
    → Qui mandate l'enquête ? Dans quel cadre ? Pour quel usage final ?
 
[ ] Le périmètre de collecte est limité aux données strictement nécessaires
    → Principe de minimisation - art. 5 §1 c) RGPD
 
[ ] Les types de données susceptibles d'être rencontrés sont anticipés
    → Données sensibles (art. 9 RGPD) identifiées et traitées en conséquence
```
 
---
 
### 1.2 Base légale RGPD
 
```markdown
[ ] Une base légale a été identifiée pour le traitement envisagé (art. 6 RGPD)
 
    Bases légales applicables en OSINT :
    [ ] Intérêt légitime (art. 6 §1 f) - mise en balance documentée obligatoire
    [ ] Mission d'intérêt public (art. 6 §1 e) - réservé aux acteurs habilités
    [ ] Obligation légale (art. 6 §1 c) - texte légal imposant le traitement
    [ ] Consentement (art. 6 §1 a) - rarement applicable en OSINT
 
[ ] Si base = intérêt légitime :
    [ ] L'intérêt poursuivi est réel et documenté
    [ ] La mise en balance avec les droits des personnes concernées est réalisée
    [ ] La mise en balance est tracée par écrit
    [ ] L'impact sur les attentes raisonnables des personnes est évalué
 
[ ] Si données sensibles (art. 9 RGPD) susceptibles d'être traitées :
    [ ] Une exception de l'art. 9 §2 est applicable et documentée
    → En l'absence d'exception : ne pas collecter ces données
```
 
---
 
### 1.3 Vérification des signaux de restriction
 
```markdown
SIGNAUX TECHNIQUES
[ ] robots.txt des domaines ciblés vérifié
    → Zones exclues identifiées et respectées
    → Source : IETF, RFC 9309
 
[ ] Présence de mesures anti-bot identifiée
    (CAPTCHA, rate limiting, tokens, vérification JS)
    → Ne pas contourner ces mesures
 
[ ] Nécessité d'authentification évaluée
    → Accès nécessitant un compte : vérifier la licéité de l'accès
 
[ ] CGU des plateformes ciblées lues
    → Restrictions sur le scraping automatisé identifiées
 
SIGNAUX CONTEXTUELS
[ ] Le contenu ciblé est-il manifestement destiné au public ?
    → Documents internes, fichiers de configuration, données RH :
      signaux de restriction implicites
 
[ ] La structure des URLs suggère-t-elle un accès restreint ?
    → /admin/, /backoffice/, /private/, /internal/ : zones à risque
```
 
---
 
### 1.4 Outils et méthodes
 
```markdown
[ ] Les outils utilisés sont identifiés et documentés
 
[ ] L'environnement de travail est isolé si données sensibles attendues
    (VM dédiée, navigateur isolé, aucune synchronisation cloud)
 
[ ] Un système d'horodatage et d'archivage des sources est en place
    → Archive.org ou archive local pour les URLs consultées
 
[ ] Un journal de l'enquête (investigation log) est ouvert
    → Date, heure, source, méthode, résultat pour chaque étape
```
 
---
 
##  PHASE 2 - Pendant la collecte / During Collection
 
### 2.1 Respect des limites en temps réel
 
```markdown
[ ] Arrêt immédiat si un signal de restriction est identifié en cours d'enquête
    → robots.txt restrictif découvert en cours de route
    → Contenu manifestement interne ou confidentiel
    → Accès nécessitant une authentification non prévue
    → Message d'erreur 403 ou redirect vers login
 
[ ] Aucun contournement de mesure de sécurité technique
    → Pas de bypass d'authentification
    → Pas de contournement de CAPTCHA
    → Pas de rotation d'IP pour contourner un blocage
 
[ ] Aucune modification de paramètres pour accéder à des ressources non ciblées
    → Pas d'itération sur des identifiants sans autorisation (cf. IDOR)
    → Pas de manipulation d'URL pour accéder à des espaces restreints
```
 
---
 
### 2.2 Traçabilité en temps réel
 
```markdown
[ ] Chaque source consultée est horodatée et archivée
    Format recommandé :
    [DATE ISO 8601] | [URL] | [MÉTHODE] | [RÉSULTAT SYNTHÉTIQUE]
    Ex : 2024-01-15T14:32:00Z | https://exemple.com/page | manuel | profil public
 
[ ] Les captures d'écran sont conservées avec métadonnées intactes
    → Ne pas recadrer ou modifier les captures (valeur probatoire)
 
[ ] Les téléchargements sont horodatés et leur source documentée
    → Hash SHA-256 des fichiers téléchargés si usage probatoire envisagé
 
[ ] La méthode de collecte est notée pour chaque donnée
    (manuelle / automatisée / outil utilisé / requête exacte)
```
 
---
 
### 2.3 Données sensibles
 
```markdown
[ ] Si une donnée relevant de l'art. 9 RGPD est rencontrée de manière fortuite :
    [ ] Ne pas collecter si aucune base légale spécifique n'est disponible
    [ ] Documenter la rencontre sans conserver la donnée
    [ ] Évaluer si la poursuite de l'enquête reste dans le périmètre défini
 
[ ] Si des données biométriques sont rencontrées (photos, vidéos) :
    [ ] Ne pas extraire d'embeddings faciaux
        → Interdit par AI Act art. 5 §1 e) depuis le 2 février 2025
    [ ] Ne pas constituer de base d'identification faciale
 
[ ] Si des credentials ou données d'accès sont découverts par inadvertance :
    [ ] Ne pas les utiliser
    [ ] Envisager un signalement responsable à l'organisation concernée
    [ ] Documenter la découverte sans conserver les données
```
 
---
 
##  PHASE 3 - Après la collecte / After Collection
 
### 3.1 Tri et minimisation
 
```markdown
[ ] Toutes les données collectées sont passées en revue
 
[ ] Les données non nécessaires à la finalité définie sont supprimées
    → Principe de minimisation - art. 5 §1 c) RGPD
    → Ne conserver que ce qui est strictement utile
 
[ ] Les données sensibles (art. 9) sans base légale identifiée sont supprimées
 
[ ] La durée de conservation est définie et documentée
    → Pas de conservation indéfinie "au cas où"
```
 
---
 
### 3.2 Documentation finale
 
```markdown
[ ] Le journal de l'enquête est complet et cohérent
    → Chaque étape documentée, chaque source tracée
 
[ ] La mise en balance (si base = intérêt légitime) est finalisée et conservée
 
[ ] Les méthodes utilisées sont documentées de manière à démontrer :
    [ ] L'absence d'intention frauduleuse
    [ ] Le respect des signaux de restriction identifiés
    [ ] La proportionnalité de la démarche à la finalité poursuivie
 
[ ] Si une vulnérabilité ou une fuite a été découverte en cours d'enquête :
    [ ] Le signalement responsable est envisagé et documenté
    [ ] Les données exposées ne sont pas conservées au-delà du strict nécessaire
```
 
---
 
### 3.3 Sécurité des données collectées
 
```markdown
[ ] Les données collectées sont stockées de manière sécurisée
    → Chiffrement si données personnelles ou sensibles
    → Accès limité aux seules personnes nécessaires
 
[ ] Les données ne sont pas partagées sans évaluation préalable
    → Destinataires identifiés, finalité du partage cohérente avec la collecte
    → Pas de diffusion publique sans évaluation de l'impact vie privée
 
[ ] En cas de diffusion publique d'informations issues de l'enquête :
    [ ] Intérêt public réel de l'information évalué
    [ ] Données minimisées (anonymisation si possible)
    [ ] Proportionnalité de la diffusion à l'objectif poursuivi vérifiée
```
 
---
 
##  Situations d'arrêt immédiat / Immediate Stop Situations
 
**FR** - Ces situations imposent un arrêt immédiat de la collecte et une réévaluation avant de poursuivre.  
**EN** - These situations require an immediate stop and reassessment before continuing.
 
```
 ARRÊT IMMÉDIAT si :
 
├── Découverte de credentials, clés API ou tokens en clair
├── Accès à un espace manifestement non destiné au public
│   (structure interne, données RH, fichiers de configuration)
├── Signal de restriction explicite non anticipé
│   (robots.txt restrictif, 403 contournable, CGU prohibant l'accès)
├── Données biométriques exploitables rencontrées
├── Données de mineurs identifiées
├── Données de santé ou données sensibles art. 9 rencontrées
│   sans base légale préalablement identifiée
└── Données issues d'une fuite connue identifiées
```
 
---
 
##  Récapitulatif des risques par type d'action / Risk Summary by Action Type
 
| Action | Risque RGPD | Risque pénal | Risque civil |
|---|---|---|---|
| Consultation de pages publiques indexées | Faible | Faible | Faible |
| Scraping avec robots.txt respecté + base légale | Moyen | Faible | Faible |
| Scraping avec contournement anti-bot | Élevé | Moyen | Moyen |
| Dorking sur contenu manifestement interne | Moyen | Élevé (Bluetouff) | Moyen |
| Faux profil / sockpuppet | Moyen | Élevé (323-1, 226-4-1) | Élevé |
| Exploitation de faille IDOR | Élevé | Élevé (323-1, 323-3) | Élevé |
| Scraping facial massif | Critique (AI Act) | Élevé | Élevé |
| Exploitation de données issues d'une fuite | Élevé | Élevé (321-1) | Moyen |
 
---
 
##  Références / References
 
- Règlement (UE) 2016/679 - RGPD, art. 5, 6, 9, 14, 32
- Règlement (UE) 2024/1689 - AI Act, art. 5 §1 e)
- C. pén., art. 321-1, 323-1, 323-3, 226-4-1
- CNIL (LINC), *Le renseignement en sources ouvertes*, 5 févr. 2024
- CNIL, *Fiche focus - Intérêt légitime et web scraping*, 19 juin 2025
- IETF, RFC 9309 – Robots Exclusion Protocol
- Cass. crim., 20 mai 2015, n° 14-81.336 (Bluetouff)
 
---
