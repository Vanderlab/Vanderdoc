---
layout: post
title: Comment créer un post de Blog ?
date: 2017-01-18
categories: blog
---

## Vous vous demandez comment poster sur le Blog ?


Envie de partager votre expérience au Vanderlab ? De raconter les avancées du jour sur un projet en cours ? Rien de plus simple, il suffit de créer un post de blog en [Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) comme suit :

* Créez un nouveau fichier `.md` dans le dossier `_posts`, dont le nom respecte la syntaxe suivante : `AAAA-MM-JJ-titre-du-post.md`.
* Copiez l'entête suivante au sommet de votre fichier :

```---
---
layout: post
title: Comment créer un post de Blog ?
date: 2017-01-18
categories: blog
---
```
* Modifier le titre et la date de l'entête pour qu'elle corresponde à votre post.
* Rédiger votre post en respectant la [syntaxe du Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#emphasis) comme dans l'exemple ci-dessous :

[image]: /images/ExempleMarkdown.png "Un exemple de Markdown"
![alt text][image]

* Plus qu'à enregistrer et soumettre puis aller à la page `https://vanderlab.github.io/blog/AAA/MM/JJ/titre-du-post`, votre contribution est affichée !
