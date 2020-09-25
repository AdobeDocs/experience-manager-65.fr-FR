---
title: Gestion des audiences
seo-title: Gestion des audiences
description: La console Audiences vous permet de créer, d’organiser et de gérer les audiences associées à votre compte Adobe Target ou de gérer des segments pour ContextHub. ou contexte client
seo-description: 'La console Audiences vous permet de créer, d’organiser et de gérer les audiences associées à votre compte Adobe Target ou de gérer des segments pour ContextHub ou ClientContext :'
uuid: 76408a8c-25db-4e9f-8a69-27e820a2a7cf
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9a7a31f9-aeb8-455f-a07e-7b1d1f0a88b6
docset: aem65
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 93%

---


# Gestion des audiences{#managing-audiences}

La console Audiences vous permet de créer, d’organiser et de gérer les audiences associées à votre compte Adobe Target ou de gérer des segments pour ContextHub ou ClientContext :

* Ajouter des audiences (audiences d’Adobe Target ou segments ContextHub).
* Gérer des audiences.

An Audience, called *segment* in ContextHub and Client Context, is a class of visitors defined by specific criteria, which then determines who sees a targeted activity. Lorsque vous ciblez une activité, vous pouvez sélectionner des audiences directement dans le processus de ciblage ou en créer de nouvelles dans la console Audiences.

Dans la console Audiences, les audiences sont organisées par marque.

Les audiences sont disponibles en mode Ciblage pour [créer du contenu ciblé](/help/sites-authoring/content-targeting-touch.md) ou pour créer des audiences (mais vous devez créer des audiences Adobe Target dans la console Audiences). Les audiences que vous créez en mode Ciblage apparaissent dans la console Audiences.

Les audiences sont accompagnées d’un libellé qui décrit le type d’audience défini :

* CH - segment ContextHub
* CC - segment ClientContext
* AT - audience Adobe Target

## Création d’un segment ContextHub dans la console Audiences  {#creating-a-contexthub-segment-in-the-audiences-console}

Vous pouvez créer un segment ContextHub dans la console Audiences ou durant le processus de ciblage.

Pour créer un segment ContextHub dans la console Audiences :

1. Dans la console Navigation, cliquez ou appuyez sur **Personnalisation**. Cliquez ou appuyez sur **Audiences**.
1. Cliquez ou appuyez sur **Créer un segment ContextHub**.

   ![capture d&#39;écran_2019-03-05at124034](assets/screen-shot_2019-03-05at124034.png)

1. Dans la boîte de dialogue **Nouveau segment ContextHub**, saisissez un titre, ajustez l’amplification et cliquez sur **Créer**. Votre nouveau segment ContextHub apparaît dans la liste des audiences.

   >[!NOTE]
   >
   >Vous pouvez trier la liste modifiée en appuyant ou en cliquant sur **Modifié** pour la trier par ordre décroissant afin de voir toutes les audiences nouvellement créées.

Pour plus d’informations sur la création de segments à l’aide de ContextHub, voir la documentation [Configuration de la segmentation avec ContextHub](/help/sites-administering/segmentation.md).

## Création d’une audience Adobe Target dans la console Audiences {#creating-an-adobe-target-audience-using-the-audience-console}

Vous pouvez créer des audiences Adobe Target directement dans AEM à l’aide de la console Audiences.

Les audiences sont définies par des règles qui déterminent qui est inclus dans une activité Target. Une définition d’audience peut contenir plusieurs règles. De plus, chaque règle peut inclure plusieurs paramètres.

Lorsque vous utilisez plusieurs règles, elles sont combinées par l’opérateur booléen ET, ce qui signifie qu’un candidat potentiellement membre d’une audience doit répondre à toutes les conditions définies pour être inclus dans l’activité. Par exemple, si vous définissez une règle de système d’exploitation ET une règle de navigateur, seuls les visiteurs qui utilisent le système d’exploitation défini ET le navigateur défini sont inclus dans l’activité.

>[!NOTE]
>
>If you do not see **Create Target Audience **in the **Create** menu, you do not have the necessary permissions to create an audience. You need write permissions under **/etc/segmentation** to be able to create audiences. Le groupe content-authors dispose par défaut d’autorisations d’écriture.

Pour créer une audience Adobe Target :

1. Dans la console Navigation, cliquez ou appuyez sur **Personnalisation**. Cliquez ou appuyez sur **Audiences**.

   ![screen-shot_2019-03-05at124139](assets/screen-shot_2019-03-05at124139.png)

1. Dans la console Audiences, appuyez ou cliquez sur **Créer**, puis sur **Créer le public cible**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Dans la boîte de dialogue **Configuration d’Adobe Target**, choisissez la configuration cible et cliquez ou appuyez sur **OK**.
1. Dans la zone Règle nº 1, cliquez ou appuyez sur le type d’attribut et entrez les informations d’attribut dans les champs disponibles. Lorsque vous avez terminé, cochez la case située à droite de l’attribut pour l’enregistrer. Voir [Attributs et leurs options](#attributes-and-their-options) pour plus d’informations sur tous les attributs.
1. Cliquez sur **Ajouter une règle** pour ajouter une autre règle. Entrez autant de règles que nécessaire. Les règles sont combinées avec l’opérateur booléen ET, ce qui signifie que l’audience doit répondre à toutes les exigences de chaque règle pour être éligible à une activité.
1. Cliquez ou appuyez sur **Suivant**.
1. Saisissez le nom de l’audience et cliquez ou appuyez sur le bouton **Enregistrer**.
1. Cliquez ou appuyez sur **Enregistrer**. Votre audience est répertoriée dans la liste des audiences.

### Attributs et leurs options  {#attributes-and-their-options}

Vous pouvez créer des règles de ciblage pour chacun des attributs suivants :

| **Attribut** | **Description** | **Pour plus d’informations** |
|---|---|---|
| **Mobile** | Périphériques mobiles Target basés sur des paramètres tels que l’appareil mobile, le type d’appareil, el fabricant de l’appareil, les dimensions de l’écran (en pixels), etc. | Reportez-vous à la [documentation relative au ciblage mobile](https://docs.adobe.com/content/help/fr-FR/target/using/audiences/create-audiences/categories-audiences/mobile.html) dans Adobe Target. |
| **Personnalisé** | Les paramètres personnalisés sont des paramètres mbox. Si vous transférez des paramètres mbox à des mbox ou utilisez la fonction targetPageParams, ces paramètres apparaissent ici pour utilisation dans les audiences. | Reportez-vous à la [documentation relative aux paramètres personnalisés](https://docs.adobe.com/content/help/fr-FR/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) dans Adobe Target. |
| **Système d’exploitation** | Vous pouvez cibler les visiteurs qui utilisent un système d’exploitation en particulier. | Utilisateurs de Target sous Linux, Mac ou Windows. |
| **Pages du site** | Visiteurs ciblés qui se trouvent sur une page spécifique ou qui possèdent un paramètre de mbox spécifique. | Reportez-vous à la [documentation relative aux pages de site](https://docs.adobe.com/content/help/fr-FR/target/using/audiences/create-audiences/categories-audiences/site-pages.html) dans Adobe Target. |
| **Navigateur** | Vous pouvez cibler les visiteurs qui utilisent un navigateur spécifique ou des options de navigateur spécifiques lors de l’accès à votre page. | Reportez-vous à la [documentation relative aux options de navigateur](https://docs.adobe.com/help/fr-FR/target/using/audiences/create-audiences/categories-audiences/browser.html) dans Adobe Target. |
| **Profil du visiteur** | Visiteurs Target qui respectent des paramètres de profil spécifiques. | Reportez-vous à la [documentation relative aux profils de visiteur](https://docs.adobe.com/content/help/fr-FR/target/using/audiences/visitor-profiles/visitor-profile.html) dans Adobe Target. |
| **Sources de trafic** | Visiteurs ciblés selon le moteur de recherche ou la page d’entrée qui les renvoie au site. | Reportez-vous à la [documentation relative aux sources de trafic](https://docs.adobe.com/content/help/fr-FR/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) dans Adobe Target. |

## Modification d’une audience dans la console Audiences {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Vous pouvez seulement modifier les audiences Adobe Target qui ont été créées dans l’instance d’AEM dans laquelle vous procédez aux modifications. Les audiences Target créées dans différents environnements AEM ne peuvent pas être modifiées.

Vous pouvez modifier n’importe quelle audience ContextHub ou ClientContext à partir de la console Audiences. Vous pouvez également modifier des audiences Adobe Target à condition qu’elles aient été créées dans AEM :

1. Dans la console Navigation, cliquez ou appuyez sur **Personnalisation**. Cliquez ou appuyez sur **Audiences**.
1. Cliquez ou appuyez sur l’icône en regard du segment ContextHub ou ClientContext à modifier, puis cliquez ou appuyez sur **Modifier**.
1. Apportez toutes les modifications dans l’éditeur de segment. Reportez-vous à la documentation relative à [ClientContext](/help/sites-administering/campaign-segmentation.md) ou à [ContextHub](/help/sites-developing/ch-configuring.md).
