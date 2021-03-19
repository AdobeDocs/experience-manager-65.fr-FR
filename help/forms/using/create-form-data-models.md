---
title: Créer un modèle de données de formulaire
seo-title: Créer un modèle de données de formulaire
description: Découvrez comment créer des modèles de données de formulaire avec ou sans sources de données configurées.
seo-description: Découvrez comment créer des modèles de données de formulaire avec ou sans sources de données configurées.
uuid: 5a94f733-0c08-41bb-983f-e7d34816d8fb
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integration
discoiquuid: 7c392909-ff84-4411-b44f-16f99dffac54
docset: aem65
feature: Modèle de données de formulaire
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 69%

---


# Créer un modèle de données de formulaire{#create-form-data-model}

![](do-not-localize/data-integeration.png)

L’intégration de données d’AEM Forms fournit une interface utilisateur intuitive permettant de créer et d’utiliser des modèles de données de formulaire. Un modèle de données de formulaire se base sur les sources de données pour l’échange des données ; toutefois, vous pouvez créer un modèle de données de formulaire avec ou sans source de données. Il existe deux approches de création d’un modèle de données de formulaire, selon que vous avez ou non configuré les sources de données :

* **Utilisation de sources** de données préconfigurées : Si vous avez configuré les sources de données comme décrit dans  [Configurer les sources](../../forms/using/configure-data-sources.md) de données, vous pouvez les sélectionner lors de la création d’un modèle de données de formulaire. Tous les objets, les services et les propriétés de modèle de données provenant des sources de données sélectionnées sont alors disponibles dans le modèle de données de formulaire.

* **Sans sources de données** : si vous n’avez pas configuré les sources de données pour votre modèle de données du formulaire, vous pouvez toujours le créer sans sources de données. Vous pouvez utiliser le modèle de données de formulaire pour créer des formulaires adaptatifs et une communication interactive et les tester à l’aide des exemples de données. Lorsque des sources de données sont disponibles, vous pouvez lier le modèle de données de formulaire à des sources de données qui se reflèteront automatiquement dans les formulaires adaptatifs et les communications interactives associées.

>[!NOTE]
>
>Vous devez être membre des groupes **fdm-author** et **forms-user** pour pouvoir créer et utiliser le modèle de données de formulaire. Contactez votre administrateur AEM pour devenir membre des groupes.

## Créer un modèle de données de formulaire {#data-sources}

Assurez-vous d’avoir configuré les sources de données que vous prévoyez d’utiliser dans le modèle de données de formulaire comme décrit dans [Configuration des sources de données](../../forms/using/configure-data-sources.md). Procédez comme suit pour créer un modèle de données de formulaire basé sur des sources de données configurées :

1. Dans l’instance d’auteur AEM, accédez à **[!UICONTROL Forms (Formulaires) > Data Integrations]** (Intégrations de données).
1. Appuyez sur **[!UICONTROL Create (Créer) > Form Data Model]** (Modèle de données de formulaire).
1. Dans la boîte de dialogue Créer un modèle de données de formulaire :

   * Attribuez un nom au modèle de données de formulaire.
   * (**Facultatif**) Spécifiez le titre, la description et les balises du modèle de données de formulaire.
   * (**Facultatif et applicable uniquement si les sources de données sont configurées**) Cochez l’icône en regard du champ **[!UICONTROL Configuration de la source de données]** et sélectionnez le nœud de configuration où se trouvent les services cloud pour les sources de données que vous voulez utiliser. Ceci restreint la liste des sources de données que vous pouvez sélectionner à la page suivante parmi les sources disponibles dans le nœud de configuration sélectionné. Cependant, toutes les bases de données JDBC et les sources de données des profils d’utilisateurs AEM sont répertoriées par défaut. Si vous ne sélectionnez pas de nœud de configuration, les sources de données de tous les nœuds de configuration sont répertoriées.

   Appuyez sur **[!UICONTROL Next]** (Suivant).

1. (**Applicable uniquement si des sources de données sont configurées**) L’écran **[!UICONTROL Sélectionner la source de données]** répertorie les sources de données disponibles, le cas échéant. Sélectionnez les sources de données que vous souhaitez utiliser dans le modèle de données de formulaire.
1. Appuyez sur **[!UICONTROL Créer]** et, dans la boîte de dialogue de confirmation, appuyez sur **[!UICONTROL Ouvrir]** pour ouvrir l’éditeur du modèle de données de formulaire.

Examinons les différents composants de l’interface utilisateur de l’éditeur de modèles de données de formulaire.

![Un modèle de données de formulaire avec trois sources de données : un service RESTful, un profil utilisateur AEM et un système RDBMS](assets/fdm-ui.png)

**A.** Sources de donnéesRépertorie les sources de données dans un modèle de données de formulaire. Développez une source de données pour vue ses objets et services de modèle de données.

**B. Actualiser les** définitions de source de donnéesRécupère toute modification des définitions de source de données à partir de sources de données configurées et les met à jour dans l’onglet Sources de données de l’éditeur de modèles de données de formulaire.

**C. Zone** ModelContent dans laquelle apparaissent les objets de modèle de données ajoutés.

**D. Zone** ServicesContent dans laquelle apparaissent des opérations ou des services de source de données ajoutés.

**E.** ToolbarTools pour travailler avec le modèle de données de formulaire. La barre d’outils affiche plus d’options en fonction de l’objet sélectionné dans le modèle de données de formulaire.

**F. Ajouter la** sélectionAjoute les objets et les services de modèle de données sélectionnés au modèle de données de formulaire.

Pour plus d’informations sur l’éditeur de modèles de données de formulaire et sur la façon dont vous pouvez l’utiliser pour modifier et configurer le modèle de données de formulaire, voir [Utilisation du modèle de données de formulaire](../../forms/using/work-with-form-data-model.md).

## Mettre à jour les sources de données {#update}

Pour ajouter ou mettre à jour des sources de données dans un modèle de données de formulaire existant, procédez comme suit.

1. Accédez à **[!UICONTROL Forms > Data Integrations]**, sélectionnez le modèle de données de formulaire dans lequel vous souhaitez ajouter ou mettre à jour des sources de données, puis appuyez sur **[!UICONTROL Propriétés]**.
1. Dans les propriétés du modèle de données de formulaire, accédez à l’onglet **[!UICONTROL Mettre à jour la source]**.

   Dans l’onglet Mettre à jour la source :

   * Appuyez sur l’icône de navigation dans le champ **[!UICONTROL Configuration contextuelle]** et sélectionnez un nœud de configuration où se trouve la configuration cloud de la source de données que vous voulez utiliser. Si vous ne sélectionnez pas de nœud, les configurations cloud qui se trouvent uniquement dans le nœud `global` sont répertoriées lorsque vous appuyez sur **[!UICONTROL Ajouter des sources]**.

   * Pour ajouter une nouvelle source de données, appuyez sur **[!UICONTROL Ajouter des sources]** et sélectionnez les sources de données à ajouter au modèle de données de formulaire. Toutes les sources de données configurées en `global` et le nœud de configuration sélectionné, le cas échéant, s’affichent.

   * Pour remplacer une source de données existante par une autre source de données du même type, appuyez sur l’icône **[!UICONTROL Modifier]** de la source de données et sélectionnez-en une dans la liste des sources de données disponibles.
   * Pour supprimer une source de données existante, appuyez sur l’icône **[!UICONTROL Supprimer]** correspondant à la source de données. L’icône Supprimer est désactivée si un objet de modèle de données dans la source de données est ajouté au modèle de données de formulaire.

   ![fdm-properties](assets/fdm-properties.png)

1. Appuyez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer les mises à jour.

>[!NOTE]
>
>Lorsque vous ajoutez de nouvelles sources de données ou que vous mettez à jour les sources de données existantes dans un modèle de données de formulaire, assurez-vous de mettre à jour les références de liaison, le cas échéant, dans les formulaires adaptatifs et les communications interactives qui utilisent le modèle de données de formulaire mis à jour.

## Étapes suivantes {#next-steps}

Vous disposez maintenant d’un modèle de données de formulaire auquel des sources de données ont été ajoutées. Vous pouvez ensuite modifier le modèle de données de formulaire pour ajouter et configurer les objets et services du modèle de données, ajouter des associations entre les objets du modèle de données, modifier les propriétés, ajouter des objets et propriétés du modèle de données personnalisés, générer des exemples de données, etc.

Pour plus d’informations, voir [Utilisation du modèle de données de formulaire](../../forms/using/work-with-form-data-model.md).
