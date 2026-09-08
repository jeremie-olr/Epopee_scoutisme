# L'Épopée du scoutisme

Page de pré-commande du concert-spectacle **L'Épopée du scoutisme** — pilote envisagé au printemps 2027.

Version statique, sans dépendance ni build : un seul fichier [`index.html`](index.html) qui embarque son CSS et son JavaScript.

## Contenu de la page

| Section | Rôle |
|---|---|
| Héros | Titre, promesse, deux appels à l'action, mention du financement par les pré-ventes |
| Le projet | Le récit depuis Brownsea 1907, puis trois volets : le spectacle, le calendrier, le financement |
| Pré-ventes | Trois formules cliquables (Éclaireur 60 €, Pionnier 110 €, Grand camp 250 € et +) et le formulaire de soutien |
| Newsletter | Formulaire d'inscription aux nouvelles du projet |
| Pied de page | Rappel du statut « projet en construction » |

## ⚠️ À faire avant la mise en ligne

**La photo du premier camp manque.** La section « Le projet » attend un fichier `assets/premier-camp.jpg` (cadrage 4/3 conseillé). Tant qu'il est absent, un cartouche typographique prend sa place automatiquement — aucune image cassée, mais pas de photo. Déposez le fichier à ce chemin et il s'affiche sans autre changement.

**Le crédit photo est à renseigner** en même temps, dans la légende de la figure :

```html
<span class="credit"></span>
```

Écrire entre les balises le fonds d'archives et les conditions de réutilisation, par exemple `Photo : The Scout Association Heritage Service — reproduite avec autorisation.` Laissée vide, la ligne est masquée (`:empty`), donc rien d'inesthétique ne s'affiche avant qu'elle soit remplie.

> Ne réutilisez pas une image trouvée sur un réseau social : une republication ne confère aucun droit. Les photographies du camp de Brownsea (août 1907) disponibles sur Wikimedia Commons sont de très faible résolution et signalées comme domaine public *aux États-Unis seulement* — insuffisant pour un site français. Passez par le détenteur du fonds.

**Les formulaires attendent un déploiement Netlify.** Ils sont câblés pour **Netlify Forms** : chaque formulaire porte un `name`, l'attribut `data-netlify="true"`, un champ caché `form-name` et un leurre anti-spam `bot-field`. Le JavaScript poste vers la racine du site (`ENDPOINT = '/'`), ce que Netlify intercepte pour déposer la soumission dans *Site configuration → Forms*. Aucun serveur à écrire.

> ⚠️ **En local, le test est trompeur** : un simple serveur de fichiers répond `200` à un `POST` sur `/`, et le formulaire paraîtra fonctionner alors que rien n'est enregistré. Seul un déploiement Netlify permet de vérifier réellement.

Pour héberger ailleurs, remplacer `'/'` par l'URL d'un service acceptant un `POST` (Formspree, Basin, Google Apps Script…). Valeur vide : rien n'est envoyé et le formulaire l'annonce au visiteur.

## Choix techniques

- **Autonomie** — l'illustration du héros vit dans `assets/hero-feu.jpg` : le dépôt ne dépend d'aucune ressource externe hormis Google Fonts.

- **Typographie** — Cormorant Garamond (titres), Karla (texte), Caveat (la note manuscrite), chargées depuis Google Fonts avec repli sur des polices système.
- **Couleurs** — palette déclarée en variables CSS, chaque teinte donnée d'abord en hexadécimal puis en `oklch()` : les navigateurs récents prennent la seconde, les anciens gardent la première.
- **Accessibilité** — lien d'évitement, libellés reliés à leurs champs, états de focus visibles, `prefers-reduced-motion` respecté, retours de formulaire annoncés via `role="status"`.
- **Écarts assumés avec la version Lovable** — les repères décoratifs `01 / 02 / 03` sont remplacés par des libellés qui portent une information (*Le spectacle*, *Le calendrier*, *Le financement*), et les formulaires signalent explicitement leur état plutôt que de simuler un envoi.

## Utilisation

Ouvrir `index.html` dans un navigateur — aucune installation nécessaire.

## Publication

### Netlify Drop (dépôt privé accepté)

Le dossier `deploy/`, exclu du versionnement, contient les seuls fichiers à mettre en ligne — `index.html` et `assets/`, sans `.git`. Le régénérer après chaque modification :

```powershell
Remove-Item deploy -Recurse -Force
New-Item -ItemType Directory -Force deploy\assets
Copy-Item index.html deploy\index.html
Copy-Item assets\* deploy\assets\
```

Puis déposer le dossier `deploy` sur https://app.netlify.com/drop. Ne jamais déposer la racine du dépôt : `.git`, donc tout l'historique, se retrouverait publiquement accessible.

Renommer l'URL attribuée dans *Site configuration → Site details → Change site name*.

### GitHub Pages

Le fichier étant nommé `index.html` à la racine, le dépôt peut aussi être servi tel quel : *Settings → Pages → Deploy from a branch → `main` / `root`*. **Le dépôt doit être public** — sur un compte gratuit, Pages ne publie pas un dépôt privé et l'URL renvoie « Site not found ».
