---
title: Script d’analyse des requêtes
seo-title: Script d’analyse des requêtes
description: Le script d’analyse des requêtes facilite l’analyse des fichiers access.log et génère un rapport lisible pour vos activités de traitement ultérieures.
seo-description: Le script d’analyse des requêtes facilite l’analyse des fichiers access.log et génère un rapport lisible pour vos activités de traitement ultérieures.
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 47%

---

# Script d’analyse des requêtes{#request-analysis-script}

## Télécharger {#download}

Ce script est conçu pour faciliter l’analyse des fichiers `access.log` produisant ainsi un rapport lisible en vue d’un traitement ultérieur.

[Obtenir le fichier](assets/analyse-access.sh)

## Description {#description}

Ce script est conçu pour faciliter l’analyse des fichiers `access.log` produisant ainsi un rapport lisible en vue d’un traitement ultérieur.

Il produit le nombre global de requêtes, GET vs POST, la répartition des requêtes au fil du temps, etc.

La sortie est en syntaxe Markdown, il sera donc plus facile de la convertir en PDF avec des outils tels que pandoc ou de l’afficher dans un navigateur avec des modules externes tels que la visionneuse Markdown.

Il peut analyser un chemin personnalisé fourni dans la ligne de commande.

Prise du commentaire dans le fichier qui vous indique comment l’exécuter :

Analysez CQ `access.log` en extrapolant diverses informations et en produisant une sortie Markdown sur `stdout`.

## Utilisation {#usage}

`./analyse-access.sh access.log.2013-&ast;`

vous pouvez fournir des chemins personnalisés supplémentaires à analyser dans la ligne de commande

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

vous pouvez enregistrer la sortie en une seule passe

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
