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
feature: Portail Formulaires
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 48%

---


# Activation des composants de Forms Portal {#enabling-forms-portal-components}

Les composants Forms Portal ne sont pas disponibles pour une utilisation immédiate. Pour que les composants apparaissent dans la liste des composants disponibles dans AEM sidekick, procédez comme suit :

1. Connectez-vous à l’instance de création de votre site web et ouvrez une page AEM Sites.

1. Pour les pages utilisant un modèle statique, procédez comme suit :

   1. Dans l’en-tête de la page, appuyez sur ![liste déroulante de canevas](assets/canvas-drop-down.png) > **Conception** pour ouvrir la page en mode de conception.
   1. Appuyez sur n’importe quel composant (avec une bordure bleue), puis appuyez sur ![field-level](assets/field-level.png) pour sélectionner le système de paragraphes contenant le composant actif.
   1. Dans le système de paragraphes, appuyez sur ![settings_icon](assets/settings_icon.png) pour ouvrir la boîte de dialogue Modifier du système de paragraphes.
   1. Dans la liste **[!UICONTROL Composants autorisés]**, cochez les cases des composants **[!UICONTROL Services de document]** et **[!UICONTROL Prédicats de services de document]**. Appuyez sur **[!UICONTROL OK]**.

1. Pour les pages utilisant un modèle dynamique, procédez comme suit :

   1. Dans l’en-tête de la page, appuyez sur ![properties](assets/properties.png) > **Modifier le modèle** pour ouvrir le modèle de la page.
   1. Appuyez sur **Layout Container** et appuyez sur ![FeedManagement](/help/forms/using/assets/feedmanagement.png). Dans l’onglet **Composants autorisés**, activez les options **Services de document et Prédicats de services de document**, puis appuyez sur ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

>[!NOTE]
>
>Vous pouvez également activer des éléments spécifiques de ces catégories en sélectionnant les composants individuellement. Pour plus d’informations sur les composants et leur utilisation, voir [Création d’une page de portail de formulaires](/help/forms/using/creating-form-portal-page.md) et [Intégration du composant Link dans une page](/help/forms/using/embedding-link-component-page.md).

Désormais, les catégories de composant Services de document et Prédicats de services de document sont disponibles dans l’explorateur de composants. Les composants sont activés pour toutes les pages qui utilisent le même modèle.

## Articles connexes

* [Activation des composants de Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* [Page du portail de formulaires](/help/forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Drafts &amp; Submissions](/help/forms/using/draft-submission-component.md)
* [Personnalisation du stockage des brouillons et des formulaires envoyés](/help/forms/using/draft-submission-component.md)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](/help/forms/using/introduction-publishing-forms.md)
