# L'Épopée du scoutisme

Page de pré-commande du concert-spectacle **L'Épopée du scoutisme** — pilote envisagé au printemps 2027.

Version statique, sans dépendance ni build : un seul fichier [`index.html`](index.html) qui embarque son CSS et son JavaScript.

## Contenu de la page

| Section | Rôle |
|---|---|
| Héros | Titre, promesse, deux appels à l'action, mention du financement par les pré-ventes |
| Le projet | Le récit depuis Brownsea 1907, puis trois volets : le spectacle, le calendrier, le financement |
| Pré-ventes | Quatre formules (Éclaireur, Bâtisseur, Pionnier, Grand camp) et le formulaire de réservation |
| Newsletter | Formulaire d'inscription aux nouvelles du projet |
| Pied de page | Rappel du statut « projet en construction » |

## ⚠️ À faire avant la mise en ligne

**Les formulaires ne sont pas raccordés.** En haut du `<script>` de `index.html` :

```js
var ENDPOINT = '';
```

Tant que cette valeur est vide, les deux formulaires valident les champs mais **n'envoient rien**, et le disent au visiteur. Renseignez une URL acceptant un `POST` (Formspree, Basin, Netlify Forms, Google Apps Script…) et tout devient opérationnel, sans autre modification.

**L'image du héros est encore distante** : elle pointe vers l'application Lovable d'origine. Pour que le dépôt soit autonome, télécharger le fichier dans `assets/` et remplacer l'URL par un chemin relatif.

## Choix techniques

- **Typographie** — Cormorant Garamond (titres), Karla (texte), Caveat (la note manuscrite), chargées depuis Google Fonts avec repli sur des polices système.
- **Couleurs** — palette déclarée en variables CSS, chaque teinte donnée d'abord en hexadécimal puis en `oklch()` : les navigateurs récents prennent la seconde, les anciens gardent la première.
- **Accessibilité** — lien d'évitement, libellés reliés à leurs champs, états de focus visibles, `prefers-reduced-motion` respecté, retours de formulaire annoncés via `role="status"`.
- **Écarts assumés avec la version Lovable** — les repères décoratifs `01 / 02 / 03` sont remplacés par des libellés qui portent une information (*Le spectacle*, *Le calendrier*, *Le financement*), et les formulaires signalent explicitement leur état plutôt que de simuler un envoi.

## Utilisation

Ouvrir `index.html` dans un navigateur — aucune installation nécessaire.

## Publication

Le fichier étant nommé `index.html` à la racine, le dépôt peut être servi tel quel par GitHub Pages : *Settings → Pages → Deploy from a branch → `main` / `root`*.
