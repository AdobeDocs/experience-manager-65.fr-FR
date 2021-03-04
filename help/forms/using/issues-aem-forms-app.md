---
title: Résolution des problèmes liés à l’application AEM Forms
seo-title: Résolution des problèmes liés à l’application AEM Forms
description: Découvrez les problèmes courants qui se produisent avec l’application AEM Forms, ainsi que la manière de les résoudre.
seo-description: Découvrez les problèmes courants qui se produisent avec l’application AEM Forms, ainsi que la manière de les résoudre.
uuid: a5cc3065-0ebf-48c0-a8fe-f1061632ca90
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 2f45a965-590b-43b1-95c6-df4b74ad15b9
translation-type: tm+mt
source-git-commit: 3690d2d76ce13064bd3946f4f6fea1a2759cdf37
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 64%

---


# Résolution des problèmes liés à l’application AEM Forms {#troubleshoot-aem-forms-app}

Cet article décrit les messages d’erreur qui peuvent s’afficher pendant la création de l’application AEM Forms et les étapes pour les résoudre.

Les sections de cet article incluent :

* [Perte des pièces jointes pour les utilisateurs iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Les brouillons de formulaires HTML5 envoyés par les utilisateurs de l’espace de travail ne sont pas visibles sur le portail](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Les formulaires HTML5 (non mis en cache) ne parviennent pas à se charger dans l’application AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms ne se synchronise pas sous Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Version de Gradle non prise en charge](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problèmes de compatibilité des modules externes Gradle et Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perte des pièces jointes pour les utilisateurs iOS {#attachment-loss-for-ios-users}

L’application AEM Forms pour iOS configurée pour se synchroniser avec AEM Forms sur OSGi ne prend en charge que les pièces jointes au niveau du champ. Toutes les pièces jointes doivent avoir des noms uniques. Si plusieurs pièces jointes ont un nom identique, une seule pièce jointe est conservée et toutes les autres portant le même nom sont perdues. Suivez les étapes ci-après pour empêcher les utilisateurs des périphériques iOS de subir une perte de données :

1. Sur le serveur connecté, accédez à **Adobe Experience Manager > Tools > Operations > Web Console**.
1. Recherchez et cliquez sur **[!UICONTROL Formulaire adaptatif et Configuration du Canal Web de communication interactive]**.
1. Dans la boîte de dialogue [!UICONTROL Configuration du Canal Web de formulaire adaptatif et de communication interactive], activez **Rendre les noms de fichier uniques**.

   Si le paramètre **Rendre les noms de fichier uniques** est désactivé, les utilisateurs subissent une perte de données s’ils tentent d’envoyer des formulaires adaptatifs avec plusieurs pièces jointes.

1. Cliquez sur **Enregistrer**.

## Les brouillons de formulaires HTML5 envoyés par les utilisateurs de l’espace de travail ne sont pas visibles sur le portail {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Pour les formulaires HTML5 activés dans l’application AEM Forms avec le Profil de rendu HTML **Enregistrer en tant que brouillon**, les brouillons enregistrés ne sont pas visibles pour les utilisateurs de l’espace de travail. Pour vue des brouillons enregistrés de formulaires HTML5 envoyés par les utilisateurs de l’espace de travail sur le portail, effectuez les étapes suivantes :

1. Ouvrez CRXDE et connectez-vous avec les informations d’identification de l’administrateur.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Dans le chemin d’accès racine CRXDE, dans Liste de contrôle d’accès, sous Contrôle d’accès, cliquez sur **+**.
1. Dans la boîte de dialogue **Ajouter une nouvelle entrée**, cliquez sur le bouton de recherche de groupe du champ Entité principale.
1. Dans le champ Nom de la boîte de dialogue Sélectionner une entité principale, saisissez `PERM_WORKSPACE_USER`, puis cliquez sur **Rechercher**.
1. Sélectionnez le groupe `PERM_WORKSPACE_USER` dans la boîte de dialogue Sélectionner une entité de sécurité et cliquez sur **OK**.
1. Dans la boîte de dialogue Ajouter une entrée, le groupe `PERM_WORKSPACE_USER` est sélectionné dans le champ Entité principale.

   Activez les privilèges `jcr:read` pour le groupe d’utilisateurs.

1. Cliquez sur **OK**.

## Les formulaires HTML5 (non mis en cache) ne parviennent pas à se charger dans l’application AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Lorsque l’application AEM Forms est connectée à une ancienne version du serveur AEM Forms, le chargement des formulaires HTML5 non mis en cache échoue dans l’application AEM Forms.

Exécutez les étapes suivantes afin de résoudre ce problème :

1. Dans l’instance d’auteur, accédez à **Adobe Experience Manager > Outils > Formulaires > Configurer le service hors ligne de l’application Workspace > Configurer maintenant**.
1. Dans la page **Service hors ligne de l’application Workspace**, cliquez sur **Cache de ressource manuel**.

   URL : https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. Dans l’onglet **Cache de ressource manuel**, cliquez sur le bouton **+** pour ajouter un chemin d’accès CRX.
1. Dans le champ **Ajouter une nouvelle ressource**, saisissez : /etc.clientlibs/fd/xfaforms/I18N/en_US.js et cliquez sur **Ajouter**.
1. Cliquez sur **Enregistrer**.

## AEM Forms ne se synchronise pas sous Windows  {#aem-forms-do-not-sync-on-windows}

Dans l’application AEM Forms sous Windows, un formulaire n’est pas synchronisé au serveur connecté si le chemin d’accès du formulaire ou de l’une de ses ressources comporte au moins 256 caractères.

Modifiez le chemin d’accès du formulaire et de ses ressources pour réduire le nombre de caractères à moins de 256.

## Version de Gradle non prise en charge  {#unsupported-version-of-gradle}

**Message d’erreur :** le projet utilise une version non prise en charge de Gradle.

Le message d’erreur s’affiche lorsque vous créez l’application AEM Forms dans Android Studio. Le problème se produit en raison d’une version non prise en charge de Gradle prise en charge sur le système.

**Résolution :** Cliquez sur  **Corriger le wrapper Gradle et réimportez le** projet pour résoudre le problème.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problèmes de compatibilité des modules externes Gradle et Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Message d’erreur :** les versions du module Android Gradle et Gradle ne sont pas compatibles.

Le message d’erreur s’affiche lorsque vous sélectionnez l’option **Build APK** dans le menu **Build** de l’interface utilisateur d’Android Studio.

![gradle_plugin_compatibilité](assets/gradle_plugin_compatibility.png)

**Résolution :** Ouvrez  **Gradle Scripts** >  **gradle-wrapper.** properties et modifiez la propriété  **** distributionUrlproperty.

Par exemple, la console Android Studio recommande de mettre à niveau la version Gradle vers 3.5. Modifiez la version dans le fichier **distributionUrl** de **gradle-wrapper.properties**.

Sélectionnez à nouveau **Build** > **Build APK** pour résoudre l’erreur et générer le fichier .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

