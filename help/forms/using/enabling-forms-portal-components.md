---
title: Activation des composants du portail Formulaires
description: Les composants du portail Formulaires prêts à l’emploi sont désactivés par défaut. Activez les groupes Services de document et Prédicats de services de document pour activer les composants du portail Formulaires.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
feature: Forms Portal
exl-id: 572194b7-063b-4c38-af43-aba78e9c51c6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '332'
ht-degree: 100%

---

# Activation des composants du portail Formulaires {#enabling-forms-portal-components}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-forms-portal.html?lang=fr) |
| AEM 6.5 | Cet article |

Les composants du portail Formulaires prêts à l’emploi ne sont pas disponibles. Pour que les composants apparaissent dans la liste des composants disponibles dans AEM sidekick, procédez comme suit :

1. Connectez-vous à l’instance d’auteur de votre site web et ouvrez une page AEM Sites.

1. Pour les pages utilisant un modèle statique, procédez comme suit :

   1. Dans l’en-tête de la page, sélectionnez ![canvas-drop-down](assets/canvas-drop-down.png) > **Conception** pour ouvrir la page en mode Conception.
   1. Sélectionnez n’importe quel composant (avec une bordure bleue), puis ![field-level](assets/field-level.png) pour choisir le système de paragraphe contenant le composant actif.
   1. Dans le système de paragraphes, sélectionnez ![settings-icon](assets/settings_icon.png) pour ouvrir la boîte de dialogue Modifier pour le système de paragraphe.
   1. Dans la liste **[!UICONTROL Composants autorisés]**, cochez les cases des composants **[!UICONTROL Services de document]** et **[!UICONTROL Prédicats de services de document]**. Sélectionnez **[!UICONTROL OK]**.

1. Pour les pages utilisant un modèle dynamique, procédez comme suit :

   1. Dans l’en-tête de la page, sélectionnez ![Propriétés](assets/properties.png) > **Modifier le modèle** pour ouvrir le modèle de la page.
   1. Sélectionnez **Conteneur de dispositions**, puis ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Dans l’onglet **Composants autorisés**, activez les options **Services de document et Prédicats de services de document**, puis sélectionnez ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Vous pouvez également activer des composants spécifiques de ces catégories en les sélectionnant. Pour plus d’informations sur les composants et leur utilisation, voir [Créer une page de portail de formulaires](/help/forms/using/creating-form-portal-page.md) et [Incorporer le composant Link dans une page](/help/forms/using/embedding-link-component-page.md).

Désormais, les catégories de composant Services de document et Prédicats de services de document sont disponibles dans l’explorateur de composants. Les composants sont activés pour toutes les pages qui utilisent le même modèle.

## Articles connexes

* [Activer des composants du portail Formulaires](/help/forms/using/enabling-forms-portal-components.md)
* [Créer une page du portail Formulaires](/help/forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Brouillons et Envois](/help/forms/using/draft-submission-component.md)
* [Personnaliser le stockage des brouillons de formulaires et des formulaires envoyés](/help/forms/using/draft-submission-component.md)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](/help/forms/using/introduction-publishing-forms.md)
