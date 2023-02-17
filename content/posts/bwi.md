---
title: "💧 MVP de prévision hydrologique - from scratch"
date: 2018-11-28T15:14:39+10:00
featured: true
draft: false
weight: 1
---

[BWI](https://bwi.earth) est une entreprise de prévision et d'anticipation des **risques hydrologiques** qui a fait
appel à notre collectif pour accélérer la création de son MVP notamment sur l'ETL et ses algorithmes prévisionnels, mais 
également sur la structuration du projet et la mise en place des process de dev.

Autant dire que le scope de notre intervention était large et le défi de taille ! En voici un bref aperçu.

||||||||||

![Blue Water Intelligence](/images/posts/bwi-illustration.png)

> *Chez Blue Water Intelligence, le duo Full Craft a réalisé pendant 3 mois un formidable travail de développement,
> d’architecture, d’optimisation des méthodes, et de coaching de développeurs moins expérimentés.
> Je vous recommande vivement leurs services, des experts fiables au service de la réussite de vos projets logiciels.*
> 
> Jérémy Fain, CEO

## 💧L'entreprise : Blue Water Intelligence (BWI)

--- 

[BWI](https://bwi.earth) est une entreprise de prévision et d'anticipation des **risques hydrologiques** qui a fait 
appel à notre collectif pour accélérer la création de son produit et **diminuer son time to market**, au moment même de la création de son activité.


## 🎯 Objectif

--- 

Nous avons travaillé avec leurs experts en hydrologie et leur équipe de développement pour mettre en place les processus
d'**ETL (Extract, Transform, Load)** adaptés et les **algorithmes prévisionnels** qui constituent leur core product dans
le but de présenter un **PoC** à leurs clients au plus tôt tout en constituant les fondations de leur **MVP**.

## 👷‍♂️ Structuration

--- 

Notre expérience a permis de mettre rapidement en place tout l'environnement de développement qui constitue désormais le socle technique de leur activité.

Guidelines, best practices, infrastructure, CI/CD, testing, gestion des dépendances... autant de grains de sable qu'on préfère cimenter avant qu'ils ne viennent gripper les rouages.


La création d'une infrastructure data standard (VPC, DB, S3, serverless, containers), sécurisée et souple a été la première brique de l'édifice.

Bien sûr, nous avons pris part au lead des développeurs data *en continu* pour leur laisser **la pleine maîtrise de leur produit**.

## 🏗️ Data Engineering

--- 

De l'ETL aux données finales, nous avons développé toute la chaîne de données :
- data scrapping, création du **data lake**
- data cleaning, création de la **data warehouse**
- data loading (clustering, cache) : mise à disposition des données à assimiler via des APIs internes

## 👨‍🔬 Data Science

--- 

En collaboration étroite avec les hydrologues, nous avons appréhendé les concepts et problématiques métier pour
implémenter les premiers **algorithmes prévisionnels** et en affiner la pertinence au fur et à mesure.

## 📊 Bilan

--- 

**En seulement 3 mois**, BWI a pu présenter à ses clients un **PoC fiable** et dispose d'une **architecture technique solide pour son MVP**.


La mise en place à tous les niveaux de pratiques de qualité, de vérification et de non-régression a été la colonne vertébrale de cette mission et assure des développements futurs encore plus fluides, efficaces et qualitatifs.
