---
layout: post
title: Theremuino
date: 2017-03-02
permalink: projets/theremuino.html
---

## Une version augmentée FAUST et Max du théremine Arduino

Introduction :
=====

Le theremuino est une version améliorée du [thérémine Arduino](https://www.arduino.cc/), qui est associée à un patch [Max](https://cycling74.com) et
des sons et instruments générés en [FAUST](https://faust.grame.fr). Le tout a été encapsulé dans une miniature de thérémine imprimée en 3D.

Matériel :
=====

* Un carte Arduino Uno
* Une breadboard + connecteurs
* 2 potentiomètres
* Une photorésistance
* Logiciel Max7 + external [faustgen~]
* Filament PLA


Réalisation :
=====

## Réalisation du patch Max

Le patch sert ici de générateur de son. Plutôt que de passer par un buzzer Piezo directement connecté à l'Arduino, j'ai souhaiter créer un son propre à cet instrument. Le patch permet de générer ce son (ici une onde sinusoïdale simple) et de lui appliquer des effets. Le patch s'articule comme suit :
 - L'objet [serial] permet de récupérer les données de l'Arduino émises en communication série.
 - L'external [faustgen~] développé par le [Grame - CNCM](http://www.grame.fr/) et [disponible sur leur site](http://faust.grame.fr/download/) dédié au langage FAUST permet de programmer en FAUST un instrument en faisant appel à diverses librairies.
 - Max permet de faire le lien entre cet instrument et la carte Arduino, et de sortir le son depuis l'ordinateur ou des haut-parleurs connectés à celui-ci.




[image]: /images/ExempleMarkdown.png "Un exemple de Markdown"
![alt text][image]



`Exemple de ligne code`, texte texte texte.

Annexes :
=====

```---
Citation
bloc de
code
```

Incenderat autem audaces usque ad insaniam homines ad haec, quae nefariis egere conatibus, Luscus quidam curator urbis subito visus: eosque ut heiulans baiolorum praecentor ad expediendum quod orsi sunt incitans vocibus crebris. qui haut longe postea ideo vivus exustus est.
