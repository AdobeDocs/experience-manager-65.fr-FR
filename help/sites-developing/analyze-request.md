---
title: Script d’analyse des requêtes
seo-title: Request Analysis Script
description: Le script d’analyse des requêtes facilite l’analyse des fichiers access.log et génère un rapport lisible pour vos activités de traitement ultérieures.
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '171'
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
