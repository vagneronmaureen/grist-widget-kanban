# grist-kanban-dsfr

Widget personnalisé Grist qui affiche une table sous forme de **kanban**, dans l'esprit des interfaces Airtable, avec le **Système de design de l'État (DSFR)**.

Un seul fichier (`index.html`), sans build ni dépendance à installer.

## Fonctionnalités

- **Colonnes du kanban** : alimentées par une colonne de type *Choice*, *ChoiceList*, *Ref* ou *RefList*.
- **Glisser-déposer** des cartes d'une colonne à l'autre : la valeur est mise à jour dans Grist.
  - Pour une *RefList* ou une *ChoiceList*, la carte quitte la colonne d'origine et rejoint la nouvelle, les autres valeurs sont conservées.
- **Couleurs des colonnes modifiables** : pastille dans l'en-tête de chaque colonne, palette de 12 couleurs DSFR. Pour une liste de choix colorée dans Grist, la couleur du choix est reprise par défaut.
- **Cartes configurables** :
  - le titre est choisi parmi les champs de la table ;
  - des champs complémentaires s'affichent sous le titre, sous trois formes : *texte*, *date* (avec icône) ou *pastille* colorée ;
  - ajout, retrait et réordonnancement des champs.
- **Fenêtre de détail** au clic sur une carte :
  - affiche des champs supplémentaires par rapport à la carte, au choix ;
  - tous les champs sont modifiables (sauf les colonnes formules).
- **Ajout de carte** depuis une colonne (la nouvelle carte est créée avec la valeur de la colonne).
- **Recherche** dans les titres et champs des cartes.

## Types de colonnes pris en charge dans la fenêtre de détail

| Type Grist | Éditeur |
| --- | --- |
| Text | zone de texte |
| Numeric, Int | champ numérique |
| Bool | case à cocher |
| Date, DateTime | sélecteur de date / date et heure |
| Choice | liste déroulante |
| ChoiceList | cases à cocher |
| Ref | liste déroulante (colonne affichée de la table référencée) |
| RefList | cases à cocher |
| Autres (pièces jointes…) | lecture seule |

## Installation

### 1. Héberger le widget (GitHub Pages)

1. Poussez ce dépôt sur GitHub.
2. Dans le dépôt : **Settings → Pages → Build and deployment**, source *Deploy from a branch*, branche `main`, dossier `/ (root)`.
3. Le widget est alors disponible à l'adresse :

   ```
   https://<utilisateur-ou-organisation>.github.io/grist-kanban-dsfr/
   ```

### 2. L'ajouter dans Grist

1. Dans votre document, ajoutez un widget de type **Custom** sur la table voulue.
2. Choisissez **Custom URL** et collez l'adresse GitHub Pages ci-dessus.
3. Réglez l'accès sur **Accès complet au document** (*Full document access*). Il est nécessaire pour lire les choix des colonnes et le contenu des tables référencées.

### 3. Configurer

Cliquez sur **Configurer** en haut du widget (ou sur l'option « Open configuration » du panneau Grist) :

1. **Colonnes du kanban** : choisissez la colonne Choice / Ref qui définit les colonnes.
2. **Titre de la carte** : choisissez le champ utilisé comme titre.
3. **Champs sous le titre** : ajoutez des champs et choisissez leur forme.
4. **Champs de la fenêtre de détail** : cochez les champs à afficher dans la popup.

La configuration est enregistrée avec le widget dans le document Grist.

## Tester hors de Grist

Ouvrez `index.html` directement dans un navigateur : le widget passe en **mode démo** avec des données fictives (le badge « Mode démo » s'affiche en bas à gauche). Pratique pour travailler le design sans document Grist.

## Limites connues

- L'ordre des cartes à l'intérieur d'une colonne n'est pas géré.
- Les valeurs *DateTime* sont lues et écrites sans tenir compte du fuseau horaire de la colonne.
- Les styles DSFR et les icônes sont chargés depuis le CDN jsDelivr (`@gouvfr/dsfr@1.12.1`) : une connexion internet est nécessaire. Pour une utilisation hors ligne ou sans CDN, hébergez les fichiers DSFR avec le widget et modifiez les deux balises `<link>` en tête de `index.html`.
- La structure de la table (colonnes, choix, contenu des tables référencées) est lue au chargement : utilisez le bouton **Recharger** après l'avoir modifiée.

## Note sur le DSFR

Le Système de design de l'État est destiné aux sites et services publics de l'administration. Vérifiez les [conditions d'utilisation](https://www.systeme-de-design.gouv.fr/) avant tout usage en dehors de ce cadre.

## Structure du dépôt

```
grist-kanban-dsfr/
├── index.html   # le widget (HTML, CSS et JS)
└── README.md
```
