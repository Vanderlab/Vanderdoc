---
layout: post
title: Aidy 3D
date: 2017-05-15
permalink: projets/aidy3d.html
---

## La mascotte de l'IME "Notre École" prend vie !

Introduction :
=====

Dans le cadre d'in cross organisé par L'IME "Notre école", nous avons réalisé une version 3D de leur mascotte, le petit Aidy, à partir du logo au format .JPG.

Matériel :
=====

* Logiciel Inkscape
* Logiciel Blender
* Imprimante 3D
* PLA
* Superglue


Réalisation :
=====

## Passage de la 2D à la 3D

On a utilisé Blender pour passer de la 2D à la 3D, mais le logiciel nécessite un fichier SVG.
On a donc utilisé Inkscape pour verctoriser le JPG en SVG, grâce à l'outils Chemin/Vectoriser le Bitmap.
Je vous laisse vous référer au très bon tuto de [Références 3D](https://www.references3d.com/convertir-une-image-en-objet-3d-blender/#.WRnJ-hOLTMV) que j'ai moi-même utilisé pour effectuer l'opération :


[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/watch?v=sO-AI0nfnTs/0.jpg)](https://www.youtube.com/watch?v=sO-AI0nfnTs)

La difficulté ici a été de partir d'une image en couleurs et de créer par la suite 2 fichiers SVG, un pour le corps de Aidy et un pour son coeur. J'ai donc vectorisé en prenant en compte les couleur puis séparé les couleurs différentes. Pour la couche rouge du coeur j'ai ensuite supprimé tous les noeuds autres que le coeur, créé un double que j'ai creusé dans la forme bleue du corps en utilisant l'outil `Chemin/Différence`.

Ne reste plus qu'à extruder le tout dans Blender (cf. tuto ci-dessus).
Voici quelques images de mon procédé :

[Vectorisation du logo]: /images/Aidy/jpeg_vs_svg.png
![alt text][Vectorisation du logo]

[Découpe de la forme du coeur]: /images/Aidy/Coeur1.png
![alt text][Découpe de la forme du coeur]

J'ai aussi ajouté un morceau en prévision de l'emboîtage dans un socle :

[Ajout pour socle]: /images/Aidy/Pied_socle.png
![alt text][Ajout pour socle]

[Extrusion en 3D]: /images/Aidy/Pied_socle.png
![alt text][Extrusion en 3D]

##Création du socle

La petit Aidy ne tenant pas sur ses pattes, il a fallu créer un socle pour le faire tenir.
J'ai pour cela utilisé Blender.

Je suis partie d'un mesh cube que j'ai redimensionné en modifiant les paramètres de dimension dans le menu latéral droit (N pour le faire apparaître/disparaître).
Aidy faisant 161x108x10mm, il fallait un socle assez large et assez haut pour que le rajout au pied de 4mm puisse s'emboîter dedans. J'ai donc créé un pavé de `80x20x6mm`.

[Socle]: /images/Aidy/1.png
![alt text][Socle]

[Socle]: /images/Aidy/3.png
![alt text][Socle]

[Socle]: /images/Aidy/4.png
![alt text][Socle]


Pour créer l'encoche d'emboîtage du pied j'ai créé un second mesh cube redimensionné à la taille de l'encoche, soit `10x2x4mm`, et dont je me sui servi pour appliquer un booléen sur mon premier cube.

[Socle]: /images/Aidy/5.png
![alt text][Socle]

[Socle]: /images/Aidy/6.png
![alt text][Socle]

Pour creuser une forme en appliquant un booléen :

- sélectionner la forme à creuser (clique droit dessus)
- sélectionner la petite clé à molette dans le menu de droite

[Socle]: /images/Aidy/7.png
![alt text][Socle]

- cliquer sur `add modifier` et séléctionner `boolean`

[Socle]: /images/Aidy/8.png
![alt text][Socle]

- Choisir l'opération `difference`et l'objet qui servira à creuser

[Socle]: /images/Aidy/10.png
![alt text][Socle]

- Déplacer l'objet qui sert à creuser dans un autre calque (touche M) puis cliquer sur appliquer.
- Le socle est maintenant creusé :

[Socle]: /images/Aidy/11.png
![alt text][Socle]

- Plus qu'à exporter le fichier .STL

[Socle]: /images/Aidy/12.png
![alt text][Socle]


## Impression 3D

Après avoir exporté votre fichier en .STL il ne reste plus qu'à passer à l'impression en 3D, en 3 parties pour les 2 couleurs différentes, le corps et socle en PLA bleu et le coeur en PLA rouge.
Attention : il m' fallu remettre mon fichier à l'échelle avant l'impression !

[Print]: /images/Aidy/Aidy1.jpg
![alt text][Print]

[Print]: /images/Aidy/Aidy3.jpg
![alt text][Print]

## Assemblage

Plus qu'à assembler les pièces, coller à la superglue et raboter si nécessaire là où il faut !

[Print]: /images/Aidy/Aidy4.jpg
![alt text][Print]

[Print]: /images/Aidy/Aidy5.jpg
![alt text][Print]

[Print]: /images/Aidy/Aidy6.jpg
![alt text][Print]
