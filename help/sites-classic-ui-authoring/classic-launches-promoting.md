---
title: Promotion de lancements
description: Vous devez convertir des pages de lancement afin de renvoyer le contenu dans la source (production) avant de le publier. Lorsqu’une page de lancement est convertie, la page correspondante des pages sources est remplacée par la page convertie.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 100%

---

# Promotion de lancements{#promoting-launches}

Vous devez convertir des pages de lancement afin de renvoyer le contenu dans la source (production) avant de le publier. Lorsqu’une page de lancement est convertie, la page correspondante des pages sources est remplacée par la page convertie. Voici les options disponibles lors de la conversion d’une page de lancement :

* Faut-il convertir uniquement la page en cours ou l’intégralité du lancement ?
* Faut-il convertir les pages enfants de la page active ?
* Faut-il convertir l’intégralité du lancement ou uniquement des pages qui ont été modifiées ?

## Promotion de pages de lancement {#promoting-launch-pages}

Pour convertir des pages, procédez comme suit lors de la modification de la page de lancement à convertir :

1. Dans l’onglet **Page** de sidekick, cliquez sur **Convertir le lancement**.
1. Spécifiez les pages à convertir :

   * (Par défaut) Pour ne convertir que la page en cours, sélectionnez **Convertir les changements de page en version d’exploitation**.
   * Pour convertir également les pages enfants de la page en cours, sélectionnez **Inclure les sous-pages**.
   * Pour convertir toutes les pages du lancement, sélectionnez **Convertir l’intégralité du lancement en version de production**.

1. Pour ajouter des pages d’exploitation à un package de workflow, sélectionnez **Ajouter au package de workflow**, puis sélectionnez le package de workflow.
1. Cliquez sur **Convertir**.

## Traitement de pages converties à l’aide du workflow AEM {#processing-promoted-pages-using-aem-workflow}

Utilisez des modèles de processus pour effectuer le traitement en bloc des pages de lancement converties :

1. Créez un package de workflow.
1. Lorsque les personnes créant du contenu convertissent des pages de lancement, elles les stockent dans le package de workflow.
1. Démarrez un modèle de workflow en utilisant le package comme payload.

Pour lancer automatiquement un workflow lors de la conversion de pages, [configurez un lanceur de workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) pour le nœud du package.

Par exemple, vous pouvez générer automatiquement des requêtes d’activation de page lorsque les personnes créant du contenu convertissent des pages de lancement. Configurez un lanceur de workflow pour démarrer le workflow Demander l’activation lorsque le nœud du package est modifié.

![chlimage_1-136](assets/chlimage_1-136.png)
