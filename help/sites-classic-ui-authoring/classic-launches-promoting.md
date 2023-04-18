---
title: Promotion de lancements
description: Vous devez convertir des pages de lancement pour que le contenu soit à nouveau déplacé dans la source (production) avant de le publier. Lorsqu’une page de lancement est convertie, la page correspondante des pages sources est remplacée par la page convertie.
uuid: 91f1c6ac-8c4e-4459-aaab-feaa32befc45
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 8d38c6f7-8fea-4d27-992d-03b604b9541f
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: 3013adc3-bec6-4ecc-aefd-f8df2b86dfef
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 31%

---

# Promotion de lancements{#promoting-launches}

Vous devez convertir des pages de lancement pour que le contenu soit à nouveau déplacé dans la source (production) avant de le publier. Lorsqu’une page de lancement est convertie, la page correspondante des pages sources est remplacée par la page convertie. Les options suivantes sont disponibles lors de la promotion d’une page de lancement :

* Indique s’il faut convertir uniquement la page active ou l’intégralité du lancement.
* Indique s’il faut convertir les pages enfants de la page active.
* Faut-il convertir l’intégralité du lancement ou uniquement des pages qui ont été modifiées ?

## Promotion de pages de lancement {#promoting-launch-pages}

Pour convertir des pages, procédez comme suit lors de la modification de la page de lancement à convertir :

1. Sur le **Page** dans le sidekick, cliquez sur **Convertir le lancement**.
1. Spécifiez les pages à convertir :

   * (Par défaut) Pour ne convertir que la page en cours, sélectionnez **Convertir les changements de page en version d’exploitation**.
   * Pour convertir également les pages enfants de la page en cours, sélectionnez **Inclure les sous-pages**.
   * Pour promouvoir toutes les pages du lancement, sélectionnez **Convertir Le Lancement Complet En Version De Production**.

1. Pour ajouter des pages de production à un module de workflow, sélectionnez **Ajouter au module de processus** puis sélectionnez le module de workflow.
1. Cliquez sur **Convertir**.

## Traitement de pages converties à l’aide du workflow AEM {#processing-promoted-pages-using-aem-workflow}

Utilisez des modèles de workflow pour effectuer le traitement en bloc des pages de lancements promues :

1. Créez un module de workflow.
1. Lorsque les auteurs convertissent des pages Launch, ils les stockent dans le module de workflow.
1. Démarrez un modèle de workflow en utilisant le module comme charge utile.

Pour démarrer automatiquement un workflow lors de la conversion de pages, [configuration d’un lanceur de workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) pour le noeud de package.

Par exemple, vous pouvez générer automatiquement des demandes d’activation de page lorsque les auteurs convertissent des pages de lancement. Configurez un lanceur de workflow pour démarrer le workflow Demander l’activation lorsque le noeud de module est modifié.

![chlimage_1-136](assets/chlimage_1-136.png)
