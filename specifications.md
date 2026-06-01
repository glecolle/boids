# Boids

## Description

Boids est une applicaton permettant de simuler un vol d'oiseaux de manière simplifiée.

## Architecture

Il s'agit d'une application mono page sans serveur contenue dans un unique fichier index.html contenant le html, le JS et le CSS. Le but est de rester le plus léger et simple possible.

## Design

L'application utilise un thème clair.
L'application adopte un "responsive" design pour s'afficher convenablement sur les différentes tailles d'écrans.
On vise un taux de rafraichissement de 60 images par secondes.
La zone d'affichage des oiseaux est un élement canvas.
Un panneau de contrôle permet de modifier les paramètres configurables de la simulation.

### Écrans dont la largeur est strictement inférieure à 1440 pixels.
Le canvas occupe toute la hauteur disponible (100 vh) et toute la largeur disponible (100 vw).
Le panneau de controle mesure la largeur de l'écran et est accessible en dessous du canvas à l'aide de l'ascenceur. La séparation avec le canvas est de 16px;

### Écrans dont la largeur est supérieure à 1900 pixels.

Le panneau de controle mesure 220 pixels de large et se trouve à droite. La séparation avec le canvas est de 16px;
Le canvas occupe toute la hauteur disponible (100 vh) et toute la largeur disponible (100vw).

## Fonctionnel

Le canvas affiche des mouvements d'oiseaux vus de dessus en 2 dimensions.

Chaque oiseau est représenté par une flèche dont la base est évidée (comme ce caractère : ⮞) de 8 pixels de long dans la direction et le sens de l'oiseau avec les variantes suivantes :
- la couleur de fond est gris clair (#ccc) pour oiseaux avec 0 voisins
- la couleur de fond est gris foncé (#555) pour les oiseaux avec 10 voisins ou plus

Les oiseaux démarrent à une position aléatoire sur le canvas.

En cliquant sur le canvas, on peut ajouter un ou des obstacles à l'endroit du clic qui sera évité par les oiseaux. Cet obstacle est un disque vert de 50 pixels de diamètre. Un nouveau clic sur l'obstacle permet de le supprimer.
Un bouton situé sous le panneau de contrôle permette de supprimer tous les obstacles.

Chaque oiseau adopte un comportement avec les règles suivantes par priorité :
- il vole toujours à la même vitesse (vitesse configurable entre 1 et 200 px/s, 75 par défaut), seul l'angle du boid est ajusté
- lorsqu'un oiseau traverse sur un bord, il est téléporté sur le bord opposé, le voisinage est donc à prendre en compte de chaque côté des bords quand un oiseau en est à proximité
- il évite l'obstacle quand il est présent dans son voisinage en déviant sa trajectoire du côté qui demande le moins de déviation, il cherche à laisser au moins 10 pixels de marge entre sa trajectoire et l'obstacle
- il évite de voler trop près des autres oiseaux (distance minimale configurable dans le panneau de contrôle, 20 px par défaut, de 1 à 100px)
- il calque progressivement sa direction en fonction des oiseaux se trouvant à moins de 60 pixels de lui (distance de proximité configurable de 1 à 100px) mais ne voit pas les oiseaux dans un cône de 120° derrière lui
- il tend à se rapprocher très légèrement de son plus proche voisin, jusqu'à la distance miniale
- un facteur turbulence permet de d'ajouter de l'aléa dans la direction et la vitesse, les aleas sont independants pour la vitesse et la direction mais partagent le même maximum configurable (1 degré ou px/s par défaut, entre 0 et 5, par pas de 0.1)
- l'angle de rotation maximal est configurable en degrés par secondes (1 à 360), par défaut à 100 degrés par seconde.

Le nombre de d'oiseaux affichés doit être configurable avec mise à jour immédiate (min = 1 et max = 1000 oiseaux, 50 par défaut) en ajoutant ou supprimant des oiseaux de la simulation de manière aléatoire.

## Codage

Le code et les commnentaires sont écrits en anglais.
Pour les blocs, il y a toujours des accolades et l'ouverture d'accolade est en fin de ligne tandis que la fermeture d'accolade est sur une ligne seule, exemple :

    if (check) {
	    //code
    }

L'oiseau doit être modélisé avec toutes ses propriétés dans une classe Boid.
L'application est modélisée dans une classe App.
Le CSS est utilisé pour positionner/présenter le canvas et les éléments du panneau de contôle.