---
title: Script d’analyse des requêtes
description: Ce script facilite l’analyse des fichiers access.log et génère un rapport lisible pour vos activités de traitement ultérieures.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 100%
---
# Script d’analyse des requêtes{#request-analysis-script}

## Télécharger {#download}

Ce script facilite l’analyse des fichiers `access.log` et génère un rapport lisible pour vos activités de traitement ultérieures.

[Obtenir le fichier](assets/analyse-access.sh)

## Description {#description}

Ce script facilite l’analyse des fichiers `access.log` et génère un rapport lisible pour vos activités de traitement ultérieures.

Il produit le nombre global de requêtes, GET vs POST, la répartition des requêtes au fil du temps, etc.

La sortie est présentée en syntaxe Markdown facile à convertir au format PDF avec des outils comme pandoc ou à présenter dans un navigateur avec des modules externes comme l’observateur Markdown.

Il peut également analyser le chemin personnalisé saisi dans la ligne de commande.

Se servir du commentaire dans le fichier qui vous indique comment l’exécuter :

Analysez le CQ `access.log` en extrapolant diverses informations et en générant une sortie MarkDown sur `stdout`.

## Utilisation {#usage}

`./analyse-access.sh access.log.2013-&ast;`

vous pouvez fournir des chemins personnalisés supplémentaires à analyser dans la ligne de commande

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

vous pouvez enregistrer la sortie en une seule passe

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
