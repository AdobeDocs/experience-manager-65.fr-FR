---
title: Publication et dépublication de formulaires et documents
seo-title: Publishing and unpublishing forms and documents
description: Vous pouvez planifier la publication et l’annulation de la publication de formulaires. Les formulaires publiés sont répliqués sur l’instance de publication.
seo-description: You can schedule publishing and unpublishing of forms. Published forms are replicated on the publish instance.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 49%

---

# Publication et dépublication de formulaires et documents{#publishing-and-unpublishing-forms-and-documents}

AEM Forms vous permet de créer, publier et dépublier des formulaires en toute facilité. Pour plus d’informations sur AEM Forms, voir [Présentation de la gestion des formulaires](../../forms/using/introduction-managing-forms.md).

Le serveur AEM Forms fournit deux instances : création et publication. L’instance Auteur est destinée à la création et la gestion d’éléments et de ressources de formulaire. L’instance de publication est destinée à conserver les ressources et les ressources connexes disponibles pour les utilisateurs finaux. Vous pouvez importer des fichiers XDP et des PDF forms en mode création. Pour plus d’informations, voir [Obtention de documents XDP et PDF dans AEM Forms](../../forms/using/get-xdp-pdf-documents-aem.md).

## Ressources prises en charge  {#supported-assets-nbsp}

AEM Forms prend en charge les types d’éléments suivants :

* Formulaires adaptatifs
* Documents adaptatifs
* Fragments de formulaire adaptatif
* Thèmes
* Modèles de formulaire (formulaires XFA)
* Formulaires PDF
* Document (documents de PDF plats)
* Ensembles de formulaire
* Ressource (images, schémas et feuilles de style)

Au départ, toutes les ressources sont disponibles uniquement dans l’instance d’auteur. Un administrateur ou un auteur de formulaires peut publier tous les actifs, à l’exception des ressources.

Lorsque vous sélectionnez un formulaire et que vous le publiez, ses actifs et ressources associés sont également publiés. Toutefois, les ressources dépendantes ne sont pas publiées. Dans ce contexte, les ressources et les ressources connexes sont des ressources qu’une ressource publiée utilise ou auxquelles elle fait référence. Les ressources dépendantes sont des ressources qui font référence à une ressource publiée.

Votre Forms adaptatif peut utiliser certaines configurations, paramètres et personnalisations qui ne sont pas publiés automatiquement. Il est recommandé de publier ou d’activer ces ressources avant de publier un formulaire adaptatif.

* Modèles de formulaire adaptatif modifiables
* Configurations de Cloud Service pour Adobe Sign, Typekit, reCAPTCHA et les modèles de données de formulaire
* Les autres configurations de services Cloud ne sont activées que si l’utilisateur dispose d’autorisations d’administrateur.
* Personnalisations. Il s’agit notamment, mais sans s’y limiter :

   * Dispositions personnalisées
   * Aspects personnalisés
   * Fichier CSS : utilisé en tant qu’entrée dans la boîte de dialogue des propriétés du conteneur de formulaires adaptatifs
   * Catégorie de bibliothèque cliente : utilisée en tant qu’entrée dans la boîte de dialogue des propriétés du conteneur de formulaires adaptatifs
   * Toute autre bibliothèque cliente pouvant être incluse dans le modèle de formulaire adaptatif.
   * Chemins de conception

## États d’un élément {#asset-states}

Un élément peut présenter les états suivants :

* **Dépublié** : élément qui n’a jamais été publié (l’état Dépublié s’applique uniquement aux éléments de Forms. Les éléments de Correspondence Management n’ont pas l’état Dépublié.)
* **Publié** : élément qui a été publié et qui est disponible sur l’instance de publication.
* **Modifié** : élément qui est modifié après avoir été publié.

## Publication d’un élément {#publish-an-asset}

1. Connectez-vous au serveur AEM Forms.
1. Utilisez l’une des méthodes suivantes pour sélectionner et publier un élément.

   1. Déplacez le pointeur sur une ressource et sélectionnez **[!UICONTROL Publier]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. Effectuez l’une des opérations suivantes, puis sélectionnez Publier :

      * Si le mode Carte est actif, sélectionnez **[!UICONTROL Entrer la sélection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png), puis sélectionnez la ressource. L’élément est sélectionné.
      * Si vous êtes en mode Liste, cochez la case d’une ressource. L’élément est sélectionné.
      * Sélectionnez une ressource pour afficher ses détails.
      * Affichez les propriétés d’un élément en appuyant sur Afficher les propriétés ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >Ne sélectionnez pas plusieurs éléments. La publication simultanée de plusieurs éléments n’est pas prise en charge.

1. Au lancement de la procédure de publication, une boîte de dialogue de confirmation s’ouvre. Elle répertorie l’ensemble des éléments et des ressources connexes. Dans la boîte de dialogue contenant les ressources connexes, sélectionnez **[!UICONTROL Publier]**. L’élément est publié et la boîte de dialogue Publication réussie apparaît.

   >[!NOTE]
   >
   >Dans le cas des formulaires adaptatifs, à côté des éléments connexes, le nom de la page Formulaire adaptatif est également affiché.

   ![Boîte de dialogue de confirmation comprenant l’ensemble des ressources et des éléments connexes](assets/p4.png)

   Boîte de dialogue de confirmation comprenant l’ensemble des ressources et des éléments connexes.

   >[!NOTE]
   >
   >Pour Forms Manager, si l’utilisateur n’est pas autorisé à publier les éléments répertoriés, l’action Publication est désactivée. Un élément qui nécessite des autorisations supplémentaires est affiché en rouge.

   Une fois l’élément publié, ses propriétés de métadonnées sont copiées dans l’instance Publication et son état passe à Publié. L’état des ressources dépendantes qui sont publiées est également modifié en Publié.

   Après avoir publié une ressource, vous pouvez utiliser le portail Forms pour afficher toutes les ressources sur une page web. Pour plus d’informations, voir [Présentation de la publication de formulaires sur un portail](../../forms/using/introduction-publishing-forms.md).

## Publication de tous les éléments de Correspondence Management {#publish-all-the-correspondence-management-assets}

AEM Forms permet de modifier tous les éléments de Correspondence Management sur un serveur en une seule fois. Les éléments publiés comportent tous les éléments de Correspondence Management et dépendances connexes.

Procédez comme suit pour publier tous les éléments de Correspondence Management sur un serveur :

1. Connectez-vous au serveur AEM Forms.
1. Sélectionner **Adobe Experience Manager** dans la barre de navigation globale.
1. Sélectionner ![outils](assets/tools.png), puis sélectionnez **Forms**.
1. Sélectionner **Publication des actifs de Correspondence Management**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   La page Publier tous les actifs de gestion de correspondance apparaît et affiche les informations sur la dernière fois où le processus de publication des actifs de gestion de correspondance a été tenté.

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. Sélectionner **Publier** et, dans le message de confirmation, sélectionnez **OK**.

   A la fin du traitement par lot, vous pouvez afficher les détails de la dernière exécution. Cela inclut des informations telles que la connexion de l’administrateur et si le lot a réussi ou échoué.

   >[!NOTE]
   >
   >Le processus de publication ne peut pas être annulé une fois lancé. En outre, pendant que le processus de publication est en cours, ne procédez à aucune création, suppression, modification ou publication d’éléments, ou ne lancez aucune opération d’exportation d’éléments de Correspondence Management.

## Automatisation de la publication ou de la dépublication de formulaires et documents {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms vous permet de planifier la publication et l’annulation de publication de ressources pour Forms et documents. Vous pouvez spécifier la planification dans l’éditeur de métadonnées. Pour plus d’informations sur la gestion des métadonnées de formulaire, reportez-vous à la section [Gestion des métadonnées de formulaire.](../../forms/using/manage-form-metadata.md)

Procédez comme suit pour planifier la date et l’heure de publication et de dépublication des éléments de formulaires et documents :

1. Sélectionnez une ressource et sélectionnez **[!UICONTROL Afficher les propriétés]**. La page Propriétés des métadonnées s’ouvre.
1. Sur la page Propriétés des métadonnées, sélectionnez **[!UICONTROL Avancé]**, puis sélectionnez **[!UICONTROL Modifier]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. Sélectionnez la date et l’heure dans les champs **[!UICONTROL Heure de début de publication]** et **[!UICONTROL Heure de fin de publication]**.\
   Sélectionner **[!UICONTROL Terminé]** ![aem6forms_check](assets/aem6forms_check.png).

## Dépublication d’un élément {#unpublish-an-asset}

1. Sélectionnez une ressource publiée, puis sélectionnez **[!UICONTROL Dépublier]** ![dépublier](assets/unpublish.png).
1. Utilisez l’une des actions suivantes pour sélectionner et dépublier un élément.

   1. Déplacez le pointeur sur une ressource et sélectionnez **[!UICONTROL Dépublier]** ![dépublier](assets/unpublish.png).
   1. Effectuez l’une des opérations suivantes, puis sélectionnez Annuler la publication :

      * Si le mode Carte est actif, sélectionnez **[!UICONTROL Entrer la sélection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png), puis sélectionnez la ressource. L’élément est sélectionné.

      * Si vous êtes en mode Liste, passez la souris sur une ressource et sélectionnez ![selectassetcheckmark](assets/selectassetcheckmark.png) . L’élément est sélectionné.

      * Sélectionnez une ressource pour afficher ses détails.
      * Affichez les propriétés d’un élément en appuyant sur Afficher les propriétés ![viewproperties](assets/viewproperties.png).

1. Au lancement de la procédure de dépublication, une boîte de dialogue de confirmation s’ouvre. Sélectionner **[!UICONTROL Dépublier]**.

   >[!NOTE]
   >
   >La dépublication affecte uniquement l’élément sélectionné ; les éléments enfants et référencés ne sont pas concernés.

## Rétablissement de la version précédemment publiée d’une ressource ou d’une lettre {#revert-an-asset-or-letter-to-the-previously-published-version}

Chaque fois que vous publiez une ressource ou une lettre après l’avoir modifiée, une version de la ressource ou de la lettre est créée. Vous pouvez rétablir une ressource ou une lettre sur une version précédemment publiée. Vous devrez peut-être le faire si un problème se produit avec la version actuelle de la ressource ou du document.

>[!NOTE]
>
>Ne pas rétablir l’état de publication d’une lettre si une ressource dépendante utilisée dans cette lettre publiée est supprimée du système.

1. Sélectionnez une ressource et sélectionnez **[!UICONTROL Revenir à la version précédemment publiée]** ![inverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. Avant que l’élément ne soit rétabli, une boîte de dialogue de confirmation s’affiche. Sélectionner **[!UICONTROL Rétablir]**.

   La version précédemment publiée de l’élément ou de la lettre est rétablie.

## Suppression d’un élément {#delete-an-asset}

>[!NOTE]
>
>La suppression d’une ressource la supprime de l’instance de publication. La suppression d’une ressource supprime également son historique des versions, à l’exception de la version de base.

1. Sélectionnez une ressource et sélectionnez **[!UICONTROL Supprimer]** ![delete](assets/delete.png).

   >[!NOTE]
   >
   >L’option de suppression est également disponible quand vous affichez les détails de l’élément en appuyant sur l’élément ou quand vous affichez les propriétés d’un élément en appuyant sur Afficher les propriétés ![viewproperties](assets/viewproperties.png).

1. Avant que l’élément soit supprimé, une boîte de dialogue de confirmation s’affiche. Sélectionnez **[!UICONTROL Supprimer]**.

   >[!NOTE]
   >
   >Seul l’élément sélectionné est supprimé et les éléments dépendants ne sont pas supprimés. Pour vérifier les références d’une ressource, sélectionnez ![références](assets/references.png) puis sélectionnez une ressource.
   >
   >
   >Si la ressource que vous tentez de supprimer est une ressource enfant d’une autre ressource, elle n’est pas supprimée. Pour supprimer une telle ressource, supprimez les références de cette ressource des autres ressources, puis réessayez.

## Formulaires adaptatifs protégés {#protected-adaptive-forms}

Vous pouvez activer l’authentification pour les formulaires auxquels les utilisateurs sélectionnés doivent accéder. Lorsque vous activez l’authentification pour vos formulaires, les utilisateurs voient un écran de connexion avant d’y accéder. Seuls les utilisateurs disposant d’informations d’identification autorisées peuvent accéder aux formulaires.

Pour activer une authentification pour vos formulaires :

1. Dans votre navigateur, ouvrez configMgr dans l’instance de publication.\
   URL : `https://<hostname>:<PublishPort>/system/console/configMgr`

1. Dans la configuration de la console Web d’Adobe Experience Manager, cliquez sur **Service d’authentification Apache Sling** pour le configurer.
1. Dans la boîte de dialogue Service d’authentification d’Apache Sling qui s’affiche, utilisez le bouton **+** pour ajouter des chemins d’accès.\
   Lorsque vous ajoutez un chemin, le service d’authentification est activé pour les formulaires de ce chemin.
