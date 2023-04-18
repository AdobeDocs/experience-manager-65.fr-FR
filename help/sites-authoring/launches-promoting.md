---
title: Convertir les lancements
description: Vous convertissez les pages de lancement pour replacer le contenu dans la source (production) avant de le publier.
uuid: 2dc41817-fcfb-4485-a085-7b57b9fe89ec
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 3d4737ef-f758-4540-bc8f-ecd9f05f6bb0
docset: aem65
legacypath: /content/docs/en/aem/6-0/author/site-page-features/launches
exl-id: f59f12a2-ecd6-49cf-90ad-621719fe51bf
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 49%

---

# Conversion de lancements{#promoting-launches}

Vous devez convertir des pages de lancement pour que le contenu soit à nouveau déplacé dans la source (production) avant de le publier. Lorsqu’une page de lancement est convertie, la page correspondante des pages sources est remplacée par la page convertie. Les options suivantes sont disponibles lors de la promotion d’une page de lancement :

* Indique s’il faut convertir uniquement la page active ou l’intégralité du lancement.
* Indique s’il faut convertir les pages enfants de la page active.
* Faut-il convertir l’intégralité du lancement ou uniquement des pages qui ont été modifiées ?
* Permet de supprimer le lancement après la conversion.

>[!NOTE]
>
>Après avoir converti les pages de lancement en pages cibles (**Production**), vous pouvez activer la variable **Production** pages en tant qu’entité (pour accélérer le processus). Ajoutez les pages à un module de workflow et utilisez-les comme charge utile pour un workflow qui active un module de pages. Vous devez créer le module de workflow avant de promouvoir le lancement. Voir [Traitement de pages converties à l’aide du workflow AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Un lancement unique ne peut pas être promu simultanément. Cela signifie que deux actions simultanées de conversion à partir du même lancement peuvent entraîner une erreur : `Launch could not be promoted` (ainsi que des erreurs de conflit dans le journal).

>[!CAUTION]
>
>Lors de la promotion du lancement des pages *modifiées*, les modifications des branches source et de lancement sont prises en compte.

## Conversion de pages de lancement {#promoting-launch-pages}

>[!NOTE]
>
>Cela couvre l’action manuelle de promotion des pages de lancement lorsqu’il n’y a qu’un seul niveau de lancement. Voir :
>
>* [Conversion d’un lancement imbriqué](#promoting-a-nested-launch) lorsqu’il y a plusieurs lancements dans la structure.
>* [Lancements – Ordre des événements](/help/sites-authoring/launches.md#launches-the-order-of-events) pour en savoir plus sur la conversion et la publication automatiques.
>


Vous pouvez promouvoir des lancements à partir de l’une des **Sites** ou la console **Lancements** console :

1. Ouvrez :

   * la valeur **Sites** console :

      1. Ouvrez le [rail de références](/help/sites-authoring/author-environment-tools.md#showingpagereferences) et sélectionnez la page source souhaitée à l’aide du [mode de sélection](/help/sites-authoring/basic-handling.md) (ou sélectionnez et ouvrez le rail de références, l’ordre n’a pas d’importance). Toutes les références seront affichées.

      1. Sélectionner **Lancements** (Lancements (1), par exemple) pour afficher une liste des lancements spécifiques.
      1. Sélectionnez le lancement spécifique pour afficher les actions disponibles.
      1. Sélectionnez **Convertir le lancement** pour ouvrir l’assistant.
   * la valeur **Lancements** console :

      1. Sélectionnez votre lancement (appuyez/cliquez sur la miniature).
      1. Sélectionnez **Convertir**.


1. Dans la première étape, vous pouvez spécifier :

   * **Cible**

      * **Supprimer le lancement après la promotion**
   * **Portée**

      * **Convertir le lancement complet**
      * **Promouvoir les pages modifiées**
      * **Convertir la page active**
      * **Convertir la page active et les sous-pages**

   Par exemple, lorsque vous sélectionnez l’option visant à convertir uniquement les pages modifiées :

   ![launches-pd-06](assets/launches-pd-06.png)

   >[!NOTE]
   >
   >Cela couvre un seul lancement, si vous avez imbriqué des lancements, voir [Conversion d’un lancement imbriqué](#promoting-a-nested-launch).

1. Sélectionner **Suivant** pour continuer.
1. Vous pouvez passer en revue les pages à convertir. Elles dépendent de la plage de pages sélectionnée :

   ![chlimage_1-102](assets/chlimage_1-102.png)

1. Sélectionnez **Convertir**.

## Conversion de pages de lancement lors de leur modification {#promoting-launch-pages-when-editing}

Lorsque vous modifiez une page de lancement, l’action **Convertir le lancement** est également disponible dans les **informations sur la page**. Cette action ouvre l’assistant pour collecter les informations nécessaires.

![chlimage_1-103](assets/chlimage_1-103.png)

>[!NOTE]
>
>Cette option est disponible pour les lancements simples et [imbriqués](#promoting-a-nested-launch).

## Promotion d’un lancement imbriqué {#promoting-a-nested-launch}

Après avoir créé un lancement imbriqué, vous pouvez le convertir en pages source, y compris la source racine (en exploitation).

![chlimage_1-104](assets/chlimage_1-104.png)

1. Comme pour la [création d’un lancement imbriqué](#creatinganestedlaunchlaunchwithinalaunch), recherchez et sélectionnez le lancement en question dans la console de **lancements** ou le rail de **références**.
1. Sélectionnez **Convertir le lancement** pour ouvrir l’assistant.

1. Saisissez les informations demandées :

   * **Cible**

      * **Convertir la cible**
Vous pouvez convertir un lancement vers n’importe quelle source.

      * **Supprimer le lancement après la conversion**
Après la conversion, le lancement sélectionné et les lancements imbriqués seront automatiquement supprimés.
   * **Portée**
Ici, vous pouvez indiquer s’il faut convertir l’intégralité du lancement ou uniquement les pages qui ont été modifiées. Si ce dernier cas se produit, vous pouvez alors choisir d’inclure/exclure des sous-pages. La configuration par défaut consiste à promouvoir uniquement les modifications de page pour la page active :

      * **Convertir le lancement complet**
      * **Promouvoir les pages modifiées**
      * **Convertir la page active**
      * **Convertir la page active et les sous-pages**

   ![chlimage_1-105](assets/chlimage_1-105.png)

1. Sélectionnez **Suivant**.
1. Vérifiez les détails de la conversion avant de sélectionner **Convertir** :

   ![chlimage_1-106](assets/chlimage_1-106.png)

   >[!NOTE]
   >
   >Les pages répertoriées dépendent de la variable **Portée** défini et éventuellement les pages qui ont été modifiées.

1. Vos modifications seront promues et répercutées dans la variable **Lancements** console :

   ![chlimage_1-107](assets/chlimage_1-107.png)

## Traitement de pages converties à l’aide du workflow AEM {#processing-promoted-pages-using-aem-workflow}

Utilisez des modèles de workflow pour effectuer le traitement en bloc des pages de lancements promues :

1. Créez un module de workflow.
1. Lorsque les auteurs convertissent des pages Launch, ils les stockent dans le module de workflow.
1. Démarrez un modèle de workflow en utilisant le module comme charge utile.

Pour démarrer automatiquement un workflow lors de la conversion de pages, [configuration d’un lanceur de workflow](/help/sites-administering/workflows-starting.md#workflows-launchers) pour le noeud de package.

Par exemple, vous pouvez générer automatiquement des demandes d’activation de page lorsque les auteurs convertissent des pages de lancement. Configurez un lanceur de workflow pour démarrer le workflow Demander l’activation lorsque le noeud de module est modifié.

![chlimage_1-108](assets/chlimage_1-108.png)
