---
title: Résolution des problèmes liés à l’application AEM Forms
description: Découvrez les problèmes courants liés à l’application AEM Forms, ainsi que la manière de les résoudre.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: caec5fc3-db52-4bf5-8eb2-17e5189ab819
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 100%

---

# Résolution des problèmes liés à l’application AEM Forms {#troubleshoot-aem-forms-app}

Cet article décrit les messages d’erreur qui peuvent s’afficher lors de la création de l’application AEM Forms ainsi que les étapes à suivre pour les résoudre.

Les sections de cet article incluent :

* [Perte des pièces jointes pour les utilisateurs iOS](/help/forms/using/issues-aem-forms-app.md#attachment-loss-for-ios-users)
* [Les brouillons de formulaires HTML5 envoyés par les utilisateurs de l’espace de travail ne sont pas visibles sur le portail](/help/forms/using/issues-aem-forms-app.md#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal)
* [Les formulaires HTML5 (non mis en cache) ne parviennent pas à se charger dans l’application AEM Forms](/help/forms/using/issues-aem-forms-app.md#html-forms-not-cached-fail-to-load-in-aem-forms-app)
* [AEM Forms ne se synchronise pas sous Windows](/help/forms/using/issues-aem-forms-app.md#aem-forms-do-not-sync-on-windows)
* [Version de Gradle non prise en charge](/help/forms/using/issues-aem-forms-app.md#unsupported-version-of-gradle)
* [Problèmes de compatibilité des modules externes Gradle et Android Gradle](/help/forms/using/issues-aem-forms-app.md#gradle-and-android-gradle-plug-in-compatibility-issues)

## Perte des pièces jointes pour les utilisateurs iOS {#attachment-loss-for-ios-users}

L’application AEM Forms pour iOS configurée pour se synchroniser avec AEM Forms sur OSGi ne prend en charge que les pièces jointes au niveau du champ. Toutes les pièces jointes doivent porter des noms uniques. Si plusieurs pièces jointes ont un nom identique, une seule pièce jointe est conservée et toutes les autres portant le même nom sont perdues. Suivez les étapes ci-après pour empêcher les utilisateurs des appareils iOS de subir une perte de données :

1. Sur le serveur connecté, accédez à **Adobe Experience Manager > Outils > Opérations > Console web**.
1. Recherchez et cliquez sur **[!UICONTROL configuration du canal web des formulaires adaptatifs et de la communication interactive]**.
1. Dans la boîte de dialogue [!UICONTROL Configuration du canal web des formulaires adaptatifs et de la communication interactive], activez **Rendre les noms de fichiers uniques**.

   Si le paramètre **Rendre les noms de fichiers uniques** est désactivé, les utilisateurs subissent une perte de données s’ils essaient d’envoyer des formulaires adaptatifs avec plusieurs pièces jointes.

1. Cliquez sur **Enregistrer**.

## Les brouillons de formulaires HTML5 envoyés par les utilisateurs et utilisatrices de l’espace de travail ne sont pas visibles sur le portail. {#html-form-drafts-submitted-by-workspace-users-are-not-visible-on-the-portal}

Pour les formulaires HTML5 activés dans l’application AEM Forms, avec le profil de rendu HTML **Enregistrer sous version préliminaire**, les versions préliminaires enregistrées ne sont pas visibles pour les utilisateurs de l’espace de travail. Pour afficher les versions préliminaires enregistrées des formulaires HTML5 envoyés par les utilisateurs de l’espace de travail sur le portail, procédez comme suit :

1. Ouvrez CRXDE et connectez-vous avec les informations d’identification de l’administrateur.

   URL : `https://<server>:<port>/lc/crx/de/index.jsp`

1. Dans le chemin d’accès racine CRXDE, dans Liste de contrôle d’accès, sous Contrôle d’accès, cliquez sur **+**.
1. Dans la boîte de dialogue **Ajouter une nouvelle entrée**, cliquez sur le bouton de recherche de groupe du champ Entité principale.
1. Dans le champ Nom de la boîte de dialogue Sélectionner une entité principale, saisissez `PERM_WORKSPACE_USER`, puis cliquez sur **Rechercher**.
1. Sélectionnez le groupe `PERM_WORKSPACE_USER` dans la boîte de dialogue Entité principale et cliquez sur **OK**.
1. Dans la boîte de dialogue Ajouter une entrée, le groupe `PERM_WORKSPACE_USER` est sélectionné dans le champ Entité principale.

   Activez les privilèges `jcr:read` pour le groupe d’utilisateurs.

1. Cliquez sur **OK**.

## Les formulaires HTML5 (non mis en cache) ne parviennent pas à se charger dans l’application AEM Forms. {#html-forms-not-cached-fail-to-load-in-aem-forms-app}

Lorsque l’application AEM Forms est connectée à une ancienne version du serveur AEM Forms, le chargement des formulaires HTML5 non mis en cache échoue dans l’application AEM Forms.

Exécutez les étapes suivantes afin de résoudre ce problème :

1. Dans l’instance d’auteur, accédez à **Adobe Experience Manager > Outils > Formulaires > Configurer le service hors ligne de l’application Workspace > Configurer maintenant**.
1. Dans la page **Service hors ligne de l’application Workspace**, cliquez sur **Cache de ressource manuel**.

   URL : https://&lt;server>:&lt;port>/libs/fd/workspace-offline/content/config.html

1. Dans l’onglet **Cache de ressource manuel**, cliquez sur le bouton **+** pour ajouter un chemin d’accès CRX.
1. Dans le champ **Ajouter une nouvelle ressource**, entrez : /etc.clientlibs/fd/xfaforms/I18N/en_US.js et cliquez sur **Ajouter**.
1. Cliquez sur **Enregistrer**.

## AEM Forms ne se synchronise pas sous Windows. {#aem-forms-do-not-sync-on-windows}

Dans l’application AEM Forms sous Windows, un formulaire ne se synchronise pas avec le serveur connecté si le chemin d’accès du formulaire ou de l’une de ses ressources comporte au moins 256 caractères.

Modifiez le chemin d’accès du formulaire et à ses ressources pour réduire le nombre de caractères à moins de 256.

## Version de Gradle non prise en charge. {#unsupported-version-of-gradle}

**Message d’erreur :** le projet utilise une version de Gradle non prise en charge.

Le message d’erreur s’affiche lorsque vous créez l’application AEM Forms dans Android Studio. Le problème se produit en raison d’une version non prise en charge de Gradle sur le système.

**Résolution :** cliquez sur **Corriger le wrapper Gradle et importer le projet à nouveau** pour résoudre le problème.

![gradle_unsupported_version](assets/gradle_unsupported_version.png)

## Problèmes de compatibilité des modules externes Gradle et Android Gradle {#gradle-and-android-gradle-plug-in-compatibility-issues}

**Message d’erreur :** les versions du plug-in Gradle Android et Gradle ne sont pas compatibles.

Le message d’erreur s’affiche lorsque vous sélectionnez l’option **Générer APK** dans le menu **Générer** sur l’interface utilisateur d’Android Studio.

![gradle_plugin_compatibility](assets/gradle_plugin_compatibility.png)

**Résolution :** ouvrez le fichier **Scripts Gradle** > **gradle-wrapper.properties** et modifiez la propriété **distributionUrl**.

Par exemple, la console d’Android Studio recommande de rétrograder la version de Gradle vers la version 3.5. Modifiez la version dans **distributionUrl** du fichier **gradle-wrapper.properties**.

Sélectionnez à nouveau **Générer** > **Générer APK** pour résoudre l’erreur et générer le fichier .apk.

![gradle_wrapper_properties](assets/gradle_wrapper_properties.png)
