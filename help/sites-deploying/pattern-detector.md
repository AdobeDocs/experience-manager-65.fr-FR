---
title: Évaluation de la complexité de la mise à niveau à l’aide de l’outil de détection des motifs
seo-title: Évaluation de la complexité de la mise à niveau à l’aide de l’outil de détection des motifs
description: Découvrez comment utiliser l’outil de détection des motifs pour évaluer la complexité de votre mise à niveau.
seo-description: Découvrez comment utiliser l’outil de détection des motifs pour évaluer la complexité de votre mise à niveau.
uuid: 84d0add9-3123-4188-9877-758911b1899f
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: b5607343-a13b-4520-a771-f1a555bfcc7b
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 89%

---


# Évaluation de la complexité de la mise à niveau à l’aide de l’outil de détection des motifs

## Présentation {#overview}

Cette fonctionnalité vous permet de déterminer si les instances existantes d’AEM peuvent être mises à niveau en détectant les motifs qui :

1. enfreignent certaines règles et qui sont exécutés dans des zones qui seront affectées ou écrasées par la mise à niveau ;
1. utilisent une API ou une fonctionnalité d’AEM 6.x non rétrocompatible sur AEM 6.5 et qui risque d’échouer après la mise à niveau.

Cela peut servir à évaluer l’ampleur des tâches de développement nécessaires pour effectuer une mise à niveau vers AEM 6.5.

## Méthode de configuration {#how-to-set-up}

L’outil de détection des motifs est publié séparément sous forme de [module](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/compatpack/pd-all-aem65) qui fonctionne sous toutes les versions AEM sources, depuis la version 6.1 jusqu’à la version 6.5, et cible la mise à niveau AEM 6.5. Il peut être installé à l&#39;aide du [Gestionnaire de modules](/help/sites-administering/package-manager.md).

## Utilisation {#how-to-use}

>[!NOTE]
>
>L’outil de détection des motifs peut être exécuté sur n’importe quel environnement, y compris sur les instances locales de développement. Toutefois, pour :
>
>* augmenter le taux de détection
>* éviter les ralentissements sur les instances critiques de l’entreprise

>
>
en même temps, il est recommandé de l’exécuter **dans des environnements d’évaluation** qui sont aussi proches que possible des environnements de production sur le plan des applications utilisateur, du contenu et des configurations.

Vous pouvez appliquer plusieurs méthodes pour vérifier le résultat de l’outil de détection des motifs :

* **Via la console Felix Inventory :**

1. Accédez à AEM Web Console en accédant à *https://serveraddress:serverport/system/console/configMgr*.
1. Sélectionnez **État – Outil de détection des motifs**, comme illustré ci-dessous :

   ![capture d&#39;écran-2018-2-5détecteur à motifs](assets/screenshot-2018-2-5pattern-detector.png)

* **Via une interface JSON standard ou une interface en mode texte réactive**
* **Via une interface de lignes JSON réactives, **qui génère un document JSON distinct dans chaque ligne.

Vous trouverez, ci-dessous, une description détaillée de ces deux méthodes :

## Interface réactive {#reactive-interface}

L’interface réactive permet de traiter le rapport d’infractions dès que l’on suspecte le moindre problème.

Le résultat est actuellement disponible sous 2 URL :

1. Interface en mode texte brut
1. Interface JSON

## Gestion de l’interface en mode texte brut  {#handling-the-plain-text-interface}

Les informations contenues dans la sortie se présentent sous la forme d’une série d’entrées d’événement. Il existe deux canaux : un pour la publication des infractions et un autre pour la publication de la progression.

Ils peuvent être obtenus en utilisant les commandes suivantes :

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep SUSPICION
```

La sortie se présente comme suit :

```
2018-02-13T14:18:32.071+01:00 [SUSPICION] The pattern=ECU/extraneous.content.usage was found by detector=ContentAccessDetector with id=a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f message="Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid". More info at=https://www.adobe.com/go/aem6_EC
```

Vous pouvez filtrer la progression à l’aide de la commande `grep` :

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.txt | tee patterns-report.log | grep PROGRESS
```

Ce qui donne le résultat suivant :

```
2018-02-13T14:19:26.909+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=45780/16 MB items, found=0 suspicions so far in period=PT5.005S (throughput=34667 items/sec)
2018-02-13T14:19:31.904+01:00 [PROGRESS] emitted=127731/52 MB patterns (from=6.5), analysed=106050/39 MB items, found=0 suspicions so far in period=PT10S (throughput=23378 items/sec)
2018-02-13T14:19:35.685+01:00 [PROGRESS] Finished in period=PT13.782
```

## Gestion de l’interface JSON  {#handling-the-json-interface}

De même, JSON pourra être traité à l’aide de l’[outil jq](https://stedolan.github.io/jq/) dès qu’il sera publié.

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == true)'
```

Avec le résultat suivant :

```
{
  "timestamp": "2018-02-13T14:20:18.894+01:00",
  "suspicion": true,
  "pattern": {
    "code": "ECU",
    "type": "extraneous.content.usage",
    "detective": "ContentAccessDetector",
    "moreInfo": "https://www.adobe.com/go/aem6_ECU"
  },
  "item": {
    "id": "a07fd94318f12312c165e06d890cbd3c2c8b8dad0c030663db8b4c800dd7c33f",
    "message": "Cross-boundary overlay of internal marked path /libs/granite/operations/components/commons/commons.jsp/jcr:content referenced at /apps/granite/operations/components/commons/commons.jsp/jcr:content with properties redefined: jcr:lastModifiedBy, jcr:mimeType, jcr:data, jcr:lastModified, jcr:uuid"
  }
}
```

Un rapport de progression est généré toutes les 5 secondes et il est possible de récupérer les informations de progression en excluant les messages autres que ceux marqués comme suspects :

```shell
curl -Nsu 'admin:admin' https://localhost:4502/system/console/status-pattern-detector.json | tee patterns-report.json | jq --unbuffered -C 'select(.suspicion == false)'
```

Avec le résultat suivant :

```
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:17.279+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 57209,
    "itemsAnalysedSize": "26 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT5.003S",
    "elapsedTimeMilliseconds": 5003,
    "itemsPerSecond": 36965
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:22.276+01:00",
  "type": "PROGRESS",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 113194,
    "itemsAnalysedSize": "46 MB",
    "suspicionsFound": 0
  },
  "progress": {
    "elapsedTime": "PT10S",
    "elapsedTimeMilliseconds": 10000,
    "itemsPerSecond": 24092
  }
}
{
  "suspicion": false,
  "timestamp": "2018-02-13T14:21:25.762+01:00",
  "type": "FINISHED",
  "database": {
    "patternsEmitted": 127731,
    "patternsEmittedSize": "52 MB",
    "databasesEmitted": [
      "6.5"
    ]
  },
  "state": {
    "itemsAnalysed": 140744,
    "itemsAnalysedSize": "63 MB",
    "suspicionsFound": 1
  },
  "progress": {
    "elapsedTime": "PT13.486S",
    "elapsedTimeMilliseconds": 13486,
    "itemsPerSecond": 19907
  }
}
{
  "suspicion": false,
  "type": "SUMMARY",
  "suspicionsFound": 1,
  "totalTime": "PT13.487S"
}
```

>[!NOTE]
>
>La méthode recommandée consiste à enregistrer toute la sortie à partir de curl dans le fichier, puis de la traiter via `jq` ou `grep` pour effectuer un filtrage sur le type d’informations.

## Domaine de détection {#scope}

Actuellement, l’outil de détection des motifs permet de vérifier :

* l’incompatibilité des exportations et importations de lots OSGi ;
* la surutilisation des ressources de type Sling et des super types (avec superpositions de contenu de chemin de recherche) ;
* définitions des index de chêne (compatibilité)
* les modules VLT (surutilisation) ;
* la compatibilité des nœuds rep:User (dans le contexte de la configuration OAuth).

>[!NOTE]
>
>Notez que l’outil de détection des motifs tente de prévoir avec précision les avertissements pour la mise à niveau. Cependant, il peut générer des faux positifs dans certains scénarios.
