---
title: Activation des composants de Forms Portal
seo-title: Activation des composants de Forms Portal
description: Les composants du portail de formulaires prêts à l’emploi sont désactivés par défaut. Activez les groupes Services de document et Prédicats de services de document pour activer les composants du portail de formulaires.
seo-description: Les composants du portail de formulaires prêts à l’emploi sont désactivés par défaut. Activez les groupes Services de document et Prédicats de services de document pour activer les composants du portail de formulaires.
uuid: 92d25da6-f1df-4ac0-bf84-2edf9e2722b3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 4d318908-c724-4582-a82b-6e9b1c55705b
translation-type: tm+mt
source-git-commit: a209b2dda04985a3f2d7c6838f11f0b5dc62d520

---


# Activation des composants de Forms Portal {#enabling-forms-portal-components}

Les composants Forms Portal ne sont pas disponibles pour une utilisation immédiate. Pour faire apparaître les composants dans la liste des composants disponibles dans le panneau latéral AEM, procédez comme suit :

1. Connectez-vous à l’instance d’auteur de votre site Web et ouvrez une page Sites AEM.

1. Pour les pages utilisant un modèle statique, procédez comme suit :

   1. In the page header, tap ![canvas-drop-down](assets/canvas-drop-down.png) > **Design** to open the page in Design mode.
   1. Tap any component (with a blue border) and then tap ![field-level](assets/field-level.png) to select the paragraph system containing the current component.
   1. In the paragraph system, tap ![settings_icon](assets/settings_icon.png) to open the Edit dialog for the paragraph system.
   1. Dans la liste **[!UICONTROL Composants autorisés]**, cochez les cases des composants **[!UICONTROL Services de document]** et **[!UICONTROL Prédicats de services de document]**. Appuyez sur **[!UICONTROL OK]**.

1. Pour les pages utilisant un modèle dynamique, procédez comme suit :

   1. Dans l’en-tête de la page, appuyez sur ![Propriétés](assets/properties.png) > **Modifier le modèle** pour ouvrir le modèle de la page.
   1. Appuyez sur Conteneur **de mise en page** et appuyez sur ![Gestion](/help/forms/using/assets/feedmanagement.png)des flux. Dans l’onglet Composants **** autorisés, activez les options **Document Services et Prédicats** Document Services, puis appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Vous pouvez également activer des éléments spécifiques de ces catégories en sélectionnant les composants individuellement. Pour plus d’informations sur les composants et leur utilisation, voir [Création d’une page de portail de formulaires](/help/forms/using/creating-form-portal-page.md) et [Intégration du composant Link dans une page](/help/forms/using/embedding-link-component-page.md).

Désormais, les catégories de composant Services de document et Prédicats de services de document sont disponibles dans l’explorateur de composants. Les composants sont activés pour toutes les pages qui utilisent le même modèle.

## Articles connexes

* [Activation des composants Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* [Créer une page Forms Portal](/help/forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Drafts and Submissions](/help/forms/using/draft-submission-component.md)
* [Personnalisation du stockage des brouillons et des formulaires envoyés](/help/forms/using/draft-submission-component.md)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](/help/forms/using/introduction-publishing-forms.md)
