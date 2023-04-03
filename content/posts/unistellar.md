---
title: "🔭 Détection d’objets dans les images astronomiques"
date: 20222-11-28T15:14:39+10:00
featured: true
draft: false
weight: 2
---

[Unistellar](https://www.unistellar.com/fr/) commercialise des télescopes connectés pour le grand public. L'entreprise 
place la R&D au coeur de sa démarche produit. Afin de caractériser rapidement le potentiel du télescope pour 
l'identification d'objets célestes, l'entreprise nous a demandé de poser les bases d'une **nouvelle méthode de détection**, 
incluant un prototype de démonstration et des résultats mesurables.

||||||||||

![Unistellar](/images/posts/unistellar-illustration.png)

## 🔭 L’entreprise : Unistellar

--- 

Co-fondée par quatre chercheurs dont deux ont travaillé sous la direction du **prix Nobel de physique 2018**,
[Unistellar](https://www.unistellar.com/fr/) conçoit, construit et commercialise un **télescope pour le grand public**,
permettant à ses utilisateurs de participer à des campagnes de science citoyenne.

L'outil de data analysis utilisé pour ces campagnes fut créé par l'un des membres de notre équipe en 2020. 
L’une des campagnes a fait l’objet d’une [publication](https://www.nature.com/articles/s41586-023-05852-9) dans la 
**prestigieuse revue scientifique Nature** en mars 2023.


## 🎯 Objectif

--- 

L’entreprise souhaitait étudier le potentiel des images capturées par ses télescopes pour la détection d’objets 
astronomiques, et améliorer son insight sur les données enregistrées par ses utilisateurs.

Cette mission s'inscrit dans la **démarche de R&D** portée par les fondateurs de l'entreprise.

## 👨‍🔬 Réalisation

--- 

La mission s'est déroulée selon plusieurs axes structurants :

- Analyse des métadonnées d’observation : nombre d’observations, heure de l’observation, nombre d’objets observés, classification par type d’objet, par luminosité (magnitude visuelle)…
- Conception et création d’un pipeline de normalisation des données: calibration astrométrique, retrait des bad pixels, stacking, soustraction du bruit de fond
- Identification de plusieurs critères de détection, implémentation de ces critères, rejet des objets célestes connus
- Développement d’un POC de détection appliquant ces critères aux images normalisées
- Création d’outils de visualisation des objets détectés

## 📊 Bilan

--- 

Après seulement quelques semaines de développement, un prototype logiciel basé sur ces critères a permis l'identification de 70% des objets du dataset de validation avec un taux de faux positifs inférieur à 10% et sans overfitting.

**Plus de 600 objets célestes non référencés** ont été identifiés sur le dataset de test.

Un pipeline de détection a été livré sous forme de POC exploitable en l'état, accompagné d'une webapp de visualisation de l'output du pipeline.

Cette étude menée avec succès constitue la base sur laquelle l'entreprise s'appuie en interne pour affiner sa solution de détection.