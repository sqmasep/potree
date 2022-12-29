# Introduction

Suite à un challenge, j'ai fork le projet opensource Potree et j'ai pour mission d'ajouter la fonctionnalité de redimensionner en largeur le panel gauche (le menu)

# Réflexion

1. Je vais probablement utiliser quelques constantes, comme une maxWidth qui ne pourra pas être dépassée lors du redimensionnement.

2. J'ai remarqué dans les fichiers sources, que le `<div id="potree_sidebar_container"></div>` n'avait pas de contenu, j'en ai conclus que le contenu était généré dynamiquement en JS côté client.

3. En utilisant "potree_sidebar_container" dans la recherche sur VSCode, j'ai trouvé un fichier JS qui correspondait, nommé `viewer.js`. Je découvre qu'il y a une fonction `load` utilisée, j'en déduis que c'est à cet endroit qu'est chargé le menu côté client.

4. Je vois un `sidebarContainer.css("width", "300px");` déjà défini par Potree, c'est ici que sont définis les différentes fonctionnalités du menu et c'est bien ici où je peux en ajouter d'autres.

5. Je remarque ensuite que ce projet (Potree) utilise jQueryUI (grâce au `$()`). Je connais cette librairie que de nom, donc je décide de regarder si elle propose une fonctionnalité de redimensionnement et c'est disponible via le `.resizable()`. Je parcours les arguments et options dans la documentation et en quelques lignes je peux contrôler totalement la largeur du menu.

# Code ajouté (dans `viewer.js`)

```js
sidebarContainer.css("z-index", "100000000");

sidebarContainer.resizable({
  handles: "e",
  minWidth: 300,
  maxWidth: 500,
});
```
