---
title: "🦾 Refactoring d'architecture mobile de contrôle de drone"
date: 2018-11-28T15:14:39+10:00
featured: true
draft: false
weight: 3
---

On pense souvent au front-end comme à une externalité, de la **plomberie** entre API et UI avec pas mal de design. 
Cependant, dès qu'on sort des applications basiques, on peut commencer à entrevoir des glitches résultant de cette 
vision simpliste - également très répandue chez les développeurs mobiles eux-mêmes. Quand de plus l'application est 
réellement complexe, implique des IoT, des protocoles de synchronisation alambiqués avec plusieurs sources, des specs
pas vraiment sèches, un prestataire un peu désorganisé qui n'a pas l'habitude de projets de cette ampleur et une 
deadline très serrée... 

**Who you gonna call ?** 👻💥

||||||||||

![VeryStrictDNA Company](/images/posts/drone-illustration.png)

## 🦜 L'entreprise

--- 

Dans l'incapacité de la citer, nous dirons simplement que c'est une belle entreprise qui produit des **drones de qualité 
professionnelle** 🤔


## 🎯 Objectif

--- 

Après des livraisons d'une qualité douteuse de la part de son prestataire de développement mobile, la direction a décidé
de mettre fin à son contrat et de constituer une équipe de freelances pour remettre d'aplomb la codebase et itérer 
rapidement pour la sortie de son nouveau drone professionnel qui n'attendait plus que l'application mobile - uniquement
iOS (UIKit) dans un premier temps. De plus, une des promesses de cette application était d'en fournir une version 
allégée et **OS**, permettant à des partenaires de coder leurs propres comportements.

C'est moi (Pierre) qui suis intervenu en tant que **lead architect**.

## 👷‍♂️ Architecture pragmatique

--- 

MVC, MVP, MVVM, TCA... Les architectures iOS sont légion. Si les conditions s'y prêtent, je conseille TCA, qui offre les meilleures garanties et une SoC très stricte. Mais comme il s'agit d'une architecture très particulière les condition n'étaient pas réunies pour s'engager sur cette voie.

On distinguait un semblant de MVVM dans le code existant. Comme c'est le modèle le plus répandu actuellement et qu'il est relativement bien compris par les développeurs, nous sommes partis de cette base et l'avons adaptée en MVVM + Coordinator.

Cependant, une fois le paradigme principal choisi, ce sont les conventions pratiques qui induisent à la fois l'efficacité du développement et la qualité finale du code.

Je les ai établies pour bénéficier des principales qualités des modèles stricts tout en court-circuitant les conventions à faible valeur ajoutée pour augmenter tant que possible l'efficacité du développement.

Après **l'écriture de guidelines** adéquates nourries d'exemples concrets et leur présentation à l'équipe, le travail a pu commencer.

## 🏗️ Refactor par étranglement avec 7 développeurs

--- 

Nous étions une équipe conséquente sur ce projet, et heureusement ! Le lead dans ce contexte a représenté une part 
importante de mon travail. Expliquer, aider, review, soutenir, peer-coder...

Mais mon compromis d'architecture pragmatique s'est avéré assez facile à prendre en main pour que cette partie diminue 
rapidement.

En pratique, nous avons établi quelques règles :

- tout ce qui peut être remis d'aplomb à moindre frais doit l'être dès qu'on effectue une quelconque modification dessus. On peut aller plus loin par capillarité lorsque c'est assez direct, c'est-à-dire sans ajouter de temps de développement trop important.
- on me fait remonter toutes les parties du code qui nécessitent des modifications conséquentes (nouveau service, création
de coordinator, remise à plat du modèle...) pour prévoir le chantier
- j'écris la grande majorité de la couche service, et je review tout ce qui y touche significativement
- partout où le refactor n'est pas assez avancé, on injecte les services via un singleton pour identifier clairement les 
zones à refactor

De plus, nous avons bien sûr attribué des rôles aux développeurs selon leurs compétences pour maximiser l'efficacité des
attributions, et **fait monter en compétence toute l'équipe** sur les paradigmes de l'architecture mais également sur la 
programmation réactive avec Combine.

Enfin, j'ai organisé de grosses sessions de **peer-programming** pour les régions les plus intriquées du code avec les 
développeurs UI ou de l'autre côté avec les développeurs du SDK bas niveau.

L'objectif était alors double : accélérer le développement des parties à haute variance, mais aussi me confronter à 
toutes les couches de l'application pour valider ou ajuster le modèle métier.

Très vite, la mise à plat à la volée du code UI existant a **dégagé une architecture concrète** de services de feature UI et
de coordinators. Les zones legacy du code ont été cloisonnées progressivement, ce qui a d'autant facilité leur 
refactoring le moment venu. Et un **ensemble de services cohérent** a petit à petit remplacé les implémentations éparses des règles business.

Pendant ce temps, **l'application restait testable**, nous informions l'équipe de QA des features refactorées à tester 
et consommions leurs retours.

## 👨‍🔬 Développement des services critiques

--- 

En parallèle, il s'agissait également de refactor et créer les services en interaction avec le SDK bas niveau de 
contrôle du drone, les différentes APIs et la persistance locale. Ici, pas question de prendre les raccourcis propres à 
l'UI.

Au contraire, je n'ai pas hésité à multiplier les services, les **machines à état** et les modèles intermédiaires 
explicitant les règles business unitaires de l'app pour arriver à un modèle simple exposé à l'UI reposant sur **des bases 
solides et explicites**.

La coopération avec les éditeurs (internes) du SDK a été cruciale, puisque certains besoins métier ont déclenché des 
chaînes de modification :
**Mobile App -> SDK (Swift) -> Core SDK (C++) -> Drone Firmware (Python / C++)**


La **documentation** détaillée des services est nécessaire - d'autant plus pour la partie open-source, mais nous avons
eu la satisfaction de constater que, dans la plupart des cas, les interfaces des nouveaux services étaient suffisamment 
explicites pour être consommées **sans ambigüité** par les développeurs en charge de l'UI.

## 📊 Bilan

--- 

Ce drone constituait **l'état de l'art du drone professionnel**, avec une myriade de fonctionnalités (photogrammétrie,
reconnaissance et suivi d'individu, piste d'atterrissage en mouvement, plan de vol,...). Même si toutes étaient 
théoriquement réalisables grâce au SDK, la confrontation au cahier des charges de haut niveau de l'UX et aux 
interactions possibles entre les fonctionnalités (combinatoire gigantesque!) a déclenché un raz-de-marée de 
problématiques, d'arbitrages et de modifications (que ce soit du SDK, des APIs, ...ou du cahier des charges).

Malgré des conditions initiales peu rassurantes, une complexité sans équivoque et une équipe de freelances sans 
connaissance préalable du produit, nous avons tenu des délais record tout en assurant une haute qualité de code, 
d'architecture, et une excellente stabilité de l'application.

**En 6 mois, toute l'infrastructure de l'application avait été reprise et complétée**. Le drone est finalement arrivé sur 
le marché avec **un retard inférieur à celui calculé au lancement de la mission**, et tout-à-fait tolérable c
ommercialement.