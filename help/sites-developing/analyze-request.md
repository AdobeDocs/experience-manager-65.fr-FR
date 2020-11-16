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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 47%

---


# Script d’analyse des requêtes{#request-analysis-script}

## Téléchargement {#download}

This script is made to ease the analysis of the `access.log` files producing a readable report for later processing.

[Obtenir le fichier](assets/analyse-access.sh)

## Description {#description}

This script is made to ease the analysis of the `access.log` files producing a readable report for later processing.

Il produit le nombre global de requêtes, GET vs POST, la répartition des requêtes au fil du temps, etc.

La sortie est effectuée en syntaxe Markdown. Il sera donc plus facile de la convertir en PDF avec des outils tels que pandoc ou de l’afficher dans un navigateur avec des plug-ins tels que Markdown viewer.

Il peut analyser un chemin personnalisé fourni sur la ligne de commande.

Prise du commentaire dans le fichier qui vous indique comment l’exécuter :

Analyse CQ `access.log` extrapolating various informations and producing a Markdown output on `stdout`.

## Utilisation {#usage}

`./analyse-access.sh access.log.2013-&ast;`

vous pouvez fournir des chemins personnalisés supplémentaires à analyser dans la ligne de commande

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

vous pouvez enregistrer la sortie en une seule passe

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
