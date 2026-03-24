# Checklist - Recueil de la preuve numérique en contexte OSINT
 
> **FR** - Checklist terrain pour la collecte, la conservation et la présentation de preuves numériques issues d'une enquête OSINT, dans un cadre civil ou pénal.  
> **EN** - Field checklist for the collection, preservation, and presentation of digital evidence from an OSINT investigation, in civil or criminal contexts.
 
---
 
##  Rappel préliminaire / Preliminary Reminder
 
**FR** - La valeur probatoire d'une preuve numérique dépend directement de la rigueur de sa collecte. Une preuve mal documentée, modifiée ou obtenue de manière déloyale peut être écartée par le juge ou voir sa valeur probante réduite. Depuis l'arrêt de l'assemblée plénière du 22 décembre 2023, le juge civil doit procéder à une mise en balance entre le droit à la preuve et les droits antinomiques en présence - la loyauté de la démarche est déterminante.
 
**EN** - The probative value of digital evidence directly depends on the rigor of its collection. Poorly documented, modified, or disloyally obtained evidence may be set aside by the court or have its probative value reduced. Since the plenary assembly ruling of 22 December 2023, the civil judge must balance the right to evidence against conflicting rights - the loyalty of the approach is decisive.
 
> Source : Cass. ass. plén., 22 déc. 2023, n° 20-20.648 et n° 21-11.330.  
 
---
 
##  PHASE 1 - Avant la collecte / Before Collection
 
### 1.1 Définir le cadre probatoire
 
```markdown
[ ] L'usage probatoire envisagé est identifié en amont
    → Procédure civile ? Pénale ? Administrative ? Usage interne ?
    → Le cadre conditionne les exigences de forme
 
[ ] La loyauté de la méthode de collecte est évaluée
    → La preuve peut-elle être obtenue sans violation de droits tiers ?
    → Si non : évaluer la proportionnalité (Cass. ass. plén., 22 déc. 2023)
 
[ ] Les exigences techniques minimales sont en place
    → Horodatage fiable (NTP synchronisé ou service tiers)
    → Système de hachage disponible (SHA-256 minimum)
    → Stockage sécurisé et non modifiable prévu
 
[ ] Un journal de collecte dédié est ouvert
    → Distinct du journal d'enquête général
    → Format : date ISO 8601, action, résultat, hash
```
 
---
 
### 1.2 Environnement de collecte
 
```markdown
[ ] L'environnement de travail est documenté avant toute collecte
    → Système d'exploitation, version du navigateur, date et heure système
    → Synchronisation NTP vérifiée
 
[ ] L'environnement est isolé si nécessaire
    → VM dédiée sans synchronisation cloud
    → Aucune extension de navigateur susceptible de modifier le contenu
 
[ ] L'heure système est vérifiée et documentée
    → Capture d'écran de l'horloge système en début de session
    → Référence à une source de temps fiable (time.is ou équivalent)
```
 
---
 
##  PHASE 2 - Collecte et préservation / Collection and Preservation
 
### 2.1 Captures d'écran
 
```markdown
[ ] La capture inclut l'URL complète visible dans la barre d'adresse
 
[ ] La capture inclut la date et l'heure système visibles
    → Ou horodatage noté immédiatement dans le journal
 
[ ] La capture est réalisée en pleine page si possible
    (outil : extension navigateur dédiée ou outil natif OS)
 
[ ] La capture n'est pas recadrée, retouchée ou modifiée après coup
    → Toute modification ultérieure doit être documentée et justifiée
 
[ ] Le fichier image est conservé dans son format original
    → Ne pas recompresser ou convertir sans documenter
 
[ ] Le hash SHA-256 du fichier est calculé et consigné immédiatement
    après la capture
```
 
**Commande de hachage / Hash command :**
```bash
# Linux / macOS
sha256sum capture_2024-01-15.png
 
# Windows (PowerShell)
Get-FileHash capture_2024-01-15.png -Algorithm SHA256
 
# Output attendu / Expected output :
# a3f8c2d1e4b5... capture_2024-01-15.png
```
 
---
 
### 2.2 Archivage des URLs
 
```markdown
[ ] Chaque URL pertinente est archivée via un service tiers
    → archive.org (Wayback Machine) : https://web.archive.org/save/
    → archive.ph : https://archive.ph
 
[ ] L'URL de l'archive est conservée dans le journal
    Format : [URL originale] → [URL archive] [date d'archivage]
 
[ ] En cas d'indisponibilité des services d'archivage :
    [ ] Archive locale réalisée (HTTrack ou équivalent)
    [ ] Date et heure de l'archive locale documentées
    [ ] Hash de l'archive calculé et consigné
 
[ ] Pour les contenus susceptibles de disparaître rapidement :
    [ ] Archivage en priorité avant toute autre action
    [ ] Plusieurs formats de conservation (capture + archive + téléchargement)
```
 
---
 
### 2.3 Téléchargement de fichiers
 
```markdown
[ ] Le fichier est téléchargé sans modification
    → Ne pas ouvrir et réenregistrer - conserver le fichier original
 
[ ] Les métadonnées du fichier sont préservées
    → Ne pas modifier la date de modification système
 
[ ] Le hash SHA-256 est calculé immédiatement après téléchargement
    et consigné dans le journal
 
[ ] La source du fichier (URL exacte) est documentée
 
[ ] Les métadonnées internes du fichier sont extraites et documentées
    si pertinentes (EXIF pour les images, propriétés pour les documents)
```
 
**Extraction de métadonnées EXIF / EXIF metadata extraction :**
```bash
# Via ExifTool (outil open source)
exiftool image.jpg
 
# Output typique / Typical output :
# File Name        : image.jpg
# File Size        : 2.1 MB
# Create Date      : 2024:01:15 14:32:00
# GPS Latitude     : 48.8566° N      ← géolocalisation potentielle
# GPS Longitude    : 2.3522° E
# Camera Model     : iPhone 14 Pro
# Software         : Adobe Photoshop  ← indice de modification
```
 
---
 
### 2.4 Contenus dynamiques et réseaux sociaux
 
```markdown
[ ] Pour les publications sur réseaux sociaux :
    [ ] Capture de la publication complète avec nom d'utilisateur visible,
        date de publication et URL du profil
    [ ] Archive via archive.ph ou archive.org
    [ ] Hash de la capture calculé et consigné
    [ ] Identifiant unique de la publication noté
        (ID dans l'URL, numéro de tweet/post)
 
[ ] Pour les vidéos :
    [ ] URL de la vidéo archivée
    [ ] Capture de la miniature avec métadonnées visibles
    [ ] Téléchargement si usage probatoire - hash calculé
 
[ ] Pour les contenus susceptibles de modification
    (pages web, profils) :
    [ ] Archivages successifs horodatés pour tracer les modifications
```
 
---
 
### 2.5 Format du journal de collecte
 
```markdown
Chaque entrée du journal doit contenir :
 
[ ] Date et heure (format ISO 8601 : AAAA-MM-JJTHH:MM:SSZ)
[ ] Type d'action (capture / téléchargement / archivage / consultation)
[ ] URL ou source exacte
[ ] Méthode utilisée (manuel / outil - préciser lequel)
[ ] Résultat synthétique
[ ] Nom du fichier conservé
[ ] Hash SHA-256 du fichier conservé
[ ] Observations particulières (signal de restriction, anomalie, etc.)
 
Exemple d'entrée :
2024-01-15T14:32:00Z | capture | https://exemple.com/profil/123 |
manuel Firefox 121.0 | profil public visible | profil_123_20240115.png |
SHA256: a3f8c2d1... | RAS
```
 
---
 
##  PHASE 3 - Conservation et intégrité / Storage and Integrity
 
### 3.1 Organisation des fichiers
 
```markdown
[ ] Structure de dossiers cohérente et documentée
    Exemple :
    enquete_AAAA-MM/
    ├── journal_collecte.csv
    ├── captures/
    │   ├── capture_001_20240115.png
    │   └── capture_002_20240115.png
    ├── archives/
    │   └── urls_archivees.txt
    ├── fichiers/
    │   └── document_001.pdf
    └── hashes.sha256         ← fichier récapitulatif de tous les hashs
 
[ ] Le fichier de hashs récapitulatif est généré et conservé
 
[ ] Les fichiers sont stockés sur un support non modifiable si possible
    (disque dédié, stockage en lecture seule après collecte)
```
 
**Génération du fichier de hashs récapitulatif :**
```bash
# Linux / macOS - génère un fichier avec les hashs de tous les fichiers
find ./enquete_2024-01/ -type f -exec sha256sum {} \; > hashes.sha256
 
# Vérification ultérieure de l'intégrité
sha256sum -c hashes.sha256
```
 
---
 
### 3.2 Sécurité du stockage
 
```markdown
[ ] Les données sont chiffrées si elles contiennent des informations
    personnelles ou sensibles
 
[ ] L'accès aux données est limité aux seules personnes nécessaires
 
[ ] Une copie de sauvegarde est réalisée sur un support distinct
 
[ ] La durée de conservation est définie et documentée
    → En lien avec la finalité de l'enquête et les exigences RGPD
```
 
---
 
##  PHASE 4 - Présentation de la preuve / Presenting Evidence
 
### 4.1 En procédure civile
 
```markdown
[ ] La loyauté de la méthode de collecte est documentée
    → Démontrer l'absence de violation de droits tiers disproportionnée
    → Référence : Cass. ass. plén., 22 déc. 2023
 
[ ] La proportionnalité de la preuve à l'objectif est démontrée
    → La preuve est indispensable à l'exercice du droit concerné
    → L'atteinte aux droits tiers est strictement proportionnée au but
 
[ ] Le journal de collecte est disponible et complet
    → Reconstitution possible de chaque étape
 
[ ] Les hashs permettent de démontrer l'intégrité des fichiers
    → Aucune modification depuis la collecte
```
 
---
 
### 4.2 En procédure pénale
 
```markdown
[ ] La preuve a été obtenue sans violation des règles applicables
    → Art. 427 CPP : liberté de la preuve en matière pénale
    → Mais loyauté de la preuve exigée
 
[ ] Si la preuve provient d'une source potentiellement illicite :
    [ ] La nécessité de la preuve est documentée
    [ ] L'absence d'alternative loyale est démontrée
    [ ] L'impact sur les droits des tiers est évalué
 
[ ] La chaîne de custody (chaîne de traçabilité) est complète
    → Qui a collecté, quand, comment, où la preuve a été stockée
    → Aucune rupture dans la traçabilité
```
 
---
 
##  Références / References
 
- Cass. ass. plén., 22 déc. 2023, n° 20-20.648 et n° 21-11.330
- C. pr. pén., art. 427 (liberté de la preuve en matière pénale)
- Règlement (UE) 2016/679 - RGPD, art. 5 §1 e) (conservation limitée)
- NIST, Guttman B., White D. R., Walraven T., *Digital Evidence Preservation:
  Considerations for Evidence Handlers*, NIST IR 8387, 2022
- ExifTool - outil open source d'extraction de métadonnées
- Wayback Machine - Internet Archive
 
---
