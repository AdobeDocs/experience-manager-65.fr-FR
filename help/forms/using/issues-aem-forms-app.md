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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

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

1. On the connected server, navigate to **Adobe Experience Manager > Tools > Operations > Web Console**.
1. Recherchez et cliquez sur **Service de configuration de formulaire adaptatif**.
1. Dans la boîte de dialogue Service de configuration de formulaire adaptatif, activez **Rendre les noms de fichier uniques**.

   If **Make File Names Unique** setting is disabled, users experience data loss if they try to submit adaptive forms with multiple attachments.

1. Cliquez sur **Enregistrer**.

## Les brouillons de formulaires HTML5 envoyés par les utilisateurs de l’espace de travail ne sont pas visibles sur le portail {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

For HTML5 forms enabled in AEM Forms app with **Save as Draft** HTML Render Profile, the saved drafts are not visible to workspace users. Pour afficher les brouillons enregistrés de formulaires HTML5 envoyés par les utilisateurs de l’espace de travail sur le portail, procédez comme suit :

1. Ouvrez CRXDE et connectez-vous avec les informations d’identification de l’administrateur.

   URL: `https://<server>:<port>/lc/crx/de/index.jsp`

1. Dans le chemin d’accès racine CRXDE, dans Liste de contrôle d’accès, sous Contrôle d’accès, cliquez sur **+**.
1. Dans la boîte de dialogue **Ajouter une nouvelle entrée**, cliquez sur le bouton de recherche de groupe du champ Entité principale.
1. Dans le champ Nom de la boîte de dialogue Sélectionner une entité principale, saisissez `PERM_WORKSPACE_USER`, puis cliquez sur **Rechercher**.
1. Select `PERM_WORKSPACE_USER` group in the Select Principal dialog and click **OK**.
1. Dans la boîte de dialogue Ajouter une entrée, le groupe `PERM_WORKSPACE_USER` est sélectionné dans le champ Entité principale.

   Enable `jcr:read` privileges for the user group.

1. Cliquez sur **OK**.

## Les formulaires HTML5 (non mis en cache) ne parviennent pas à se charger dans l’application AEM Forms {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Lorsque l’application AEM Forms est connectée à une ancienne version du serveur AEM Forms, le chargement des formulaires HTML5 non mis en cache échoue dans l’application AEM Forms.

Exécutez les étapes suivantes afin de résoudre ce problème :

1. Dans l’instance d’auteur, accédez à **Adobe Experience Manager > Outils > Formulaires > Configurer le service hors ligne de l’application Workspace > Configurer maintenant**.
1. Dans la page **Service hors ligne de l’application Workspace**, cliquez sur **Cache de ressource manuel**.

   URL : https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. Dans l’onglet **Cache de ressource manuel**, cliquez sur le bouton **+** pour ajouter un chemin d’accès CRX.
1. In the **Add a New Resource** field, type: /etc.clientlibs/fd/xfaforms/I18N/en_US.js and click **Add**.
1. Cliquez sur **Enregistrer**.

## AEM Forms ne se synchronise pas sous Windows {#aem-forms-do-not-sync-on-windows}

Dans l’application AEM Forms sous Windows, un formulaire n’est pas synchronisé au serveur connecté si le chemin d’accès du formulaire ou de l’une de ses ressources comporte au moins 256 caractères.

Modifiez le chemin d’accès du formulaire et de ses ressources pour réduire le nombre de caractères à moins de 256.

## Version de Gradle non prise en charge {#unsupported-version-of-gradle}

**** Message d’erreur : Le projet utilise une version non prise en charge de Gradle.

Le message d’erreur s’affiche lorsque vous créez l’application AEM Forms dans Android Studio. Le problème se produit en raison d’une version non prise en charge de Gradle prise en charge sur le système.

**** Résolution : Cliquez sur **Réparer le wrapper Gradle et réimportez le projet** pour résoudre le problème.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problèmes de compatibilité des modules externes Gradle et Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**** Message d’erreur : Les versions du module Android Gradle et Gradle ne sont pas compatibles.

The error message is displayed when you select **Build APK** option from the **Build** menu on the Android Studio user interface.

![gradle_plugin_compatibilité](assets/gradle_plugin_compatibility.png)

**** Résolution : Ouvrez le fichier **Gradle Scripts** > **gradle-wrapper.properties** et modifiez la propriété **distributionUrl** .

For example, the Android Studio console recommends downgrading the Gradle version to 3.5. Edit the version in **distributionUrl** of **gradle-wrapper.properties** file.

Select **Build** > **Build APK** again to resolve the error and generate the .apk file.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)

