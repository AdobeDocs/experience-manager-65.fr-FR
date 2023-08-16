---
title: Comment activer les composants principaux de Forms adaptatif sur AEM 6.5 Forms ?
seo-title: How to enable Adaptive Forms Core Components on AEM 6.5 Forms?
description: Guide détaillé pour vous aider à activer les composants principaux de Forms adaptatif dans un environnement Forms 6.5 AEM.
seo-description: Step-by-Step guide to help you enable Adaptive Forms Core Components on an AEM 6.5 Forms environment.
keywords: Activez les composants principaux, composants principaux Forms adaptatif, composants principaux sur la version 6.5, composants principaux Forms adaptatifs sur AEM 6.5, composants principaux AF sur AEM 6.5 et composants principaux Forms 6.5.
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---


# Activation des composants principaux de Forms adaptatif sur AEM Forms 6.5 {#enable-adaptive-forms-core-components}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=fr) |
| AEM 6.5 | Cet article |

**S’applique à :** ✅ Composants principaux de formulaire adaptatif ❎ Composants de base de formulaire adaptatif.

L’activation des composants principaux de Forms adaptatif vous permet de commencer à créer, publier et diffuser des [Forms adaptatif basé sur les composants principaux](create-an-adaptive-form-core-components.md) et [Forms adaptatif sans affichage](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=fr) de votre environnement Forms 6.5 AEM.

Pour activer les composants principaux Forms adaptatifs sur votre environnement Forms 6.5 AEM, configurez et déployez une [AEM Archetype 41 ou version ultérieure](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr) basé sur un projet (avec les options de formulaire activées) sur toutes vos instances d’auteur et de publication.

Cet article fournit des instructions détaillées sur la configuration et le déploiement d’AEM archetype 41 ou version ultérieure sur votre environnement Forms AEM 6.5 pour activer les composants principaux Forms adaptatif.


## Conditions préalables requises {#prerequisites}

Avant d’activer les composants principaux de Forms adaptatif dans un environnement Forms 6.5 AEM :

* [Mise à niveau vers AEM 6.5 Forms Service Pack 16 (6.5.16.0) ou version ultérieure](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html).

* Installez la dernière version de [Apache Maven](https://maven.apache.org/download.cgi).

* Installez un éditeur de texte brut. Par exemple, Microsoft Visual Studio Code.

## Créer et déployer le dernier projet basé sur AEM Archetype

Pour créer un archétype AEM 41 ou [later](https://github.com/adobe/aem-project-archetype) basé sur le projet et le déployez sur toutes vos instances d’auteur et de publication :

1. Connectez-vous à votre ordinateur, en tant qu’administrateur, en hébergeant et en exécutant votre instance Forms AEM 6.5.
1. Ouvrez l’invite de commande ou le terminal et exécutez la commande suivante pour créer AEM projet Archetype (avec les options de formulaire activées) :

   * Microsoft Windows

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate ^
      -D archetypeGroupId=com.adobe.aem ^
      -D archetypeArtifactId=aem-project-archetype ^
      -D archetypeVersion=41 ^
      -D appTitle="My Form" ^
      -D appId="myform" ^
      -D groupId="com.myform" ^
      -D includeFormsenrollment="y" ^
      -D aemVersion="6.5.15" 
   ```

   * Linux ou Apple macOS

   ```Shell
      mvn -B org.apache.maven.plugins:maven-archetype-plugin:3.2.1:generate \
      -D archetypeGroupId=com.adobe.aem \
      -D archetypeArtifactId=aem-project-archetype \
      -D archetypeVersion=41 \
      -D appTitle="My Form" \
      -D appId="myform" \
      -D groupId="com.myform" \
      -D includeFormsenrollment="y" \
      -D aemVersion="6.5.15" 
   ```

   Lorsque vous exécutez la commande ci-dessus, veillez à tenir compte des points suivants :

   * Ne modifiez pas la valeur de la variable `aemVersion` de `6.5.15.0` à tout autre chose.

   * Définissez la variable `archetypeVersion` de `41` ou plus tard. Pour obtenir la dernière version, reportez-vous à la section Configuration requise dans [AEM Archétype de projet](https://github.com/adobe/aem-project-archetype) la documentation.

   * Mettez à jour la commande afin de refléter les valeurs spécifiques de votre environnement, y compris le `appTitle`, `appId`, et `groupId`. Définissez également la valeur de la variable  `includeFormsenrollment` de `y`. Si vous utilisez Forms Portal, définissez la variable `includeExamples=y` pour inclure les composants principaux du portail Forms dans votre projet.


1. (Uniquement pour les projets basés sur la version 41 de l’archétype) Une fois le projet d’archétype AEM créé, activez les thèmes pour les Forms adaptatif basés sur les composants principaux. Pour activer les thèmes :

   1. Ouvrez le [AEM archetype Project Folder]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html pour modification :

   1. Ajoutez le code suivant à la ligne 21 :

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Ajouter le code mentionné ci-dessus à la ligne 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Enregistrez et fermez le fichier.

1. Mettez à jour le projet pour inclure la dernière version des composants principaux Forms :

   1. Ouvrez le [AEM archetype Project Folder]/pom.xml pour modification.
   1. Définir la version de `core.forms.components.version` et `core.forms.components.af.version` to [derniers composants principaux Forms](https://github.com/adobe/aem-core-forms-components/tree/release/650) version.

   1. Enregistrez et fermez le fichier.


1. Une fois le projet AEM Archetype créé, créez le package de déploiement pour votre environnement. Pour créer le module :

   1. Accédez au répertoire racine de votre projet AEM Archetype.

   1. Exécutez la commande suivante pour créer le projet AEM Archetype pour votre environnement :

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   Une fois le projet AEM Archetype créé, un module AEM est généré. Vous trouverez le package à l’adresse [AEM archetype Project Folder]\all\target\[appid].all-[version].zip

1. Utilisez la variable [Gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) pour déployer le [AEM archetype Project Folder]\all\target\[appid].all-[version]Package .zip sur toutes les instances d’auteur et de publication.

>[!NOTE]
>
>
>
> * Si vous rencontrez des difficultés pour accéder à la boîte de dialogue de connexion sur une instance de publication, essayez d’installer le module via le gestionnaire de modules à l’aide de l’URL : `http://[Publish Server URL]:[PORT]/system/console` pour vous connecter. Cela vous permet d’accéder à la page de connexion d’une instance de publication, ce qui vous permet de poursuivre le processus d’installation.
> * Ne supprimez pas ou ne supprimez pas le projet Archetype après son déploiement dans votre environnement. Le projet Archetype est nécessaire pour ajouter des thèmes de composants principaux de Forms adaptatif personnalisés et nouveaux à votre environnement.

Les composants principaux sont activés pour votre environnement. Un modèle de formulaire adaptatif basé sur des composants principaux vierge et un thème de canevas 3.0 sont déployés dans votre environnement, ce qui vous permet de [Création d’un Forms adaptatif basé sur les composants principaux](create-an-adaptive-form-core-components.md).

## Foire aux questions

### Que sont les composants principaux ?

La variable [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) sont un ensemble de composants WCM (Web Content Management, gestion de contenu web) normalisés permettant d’AEM accélérer le temps de développement et de réduire les coûts de maintenance de vos sites web.

### Quelles sont les fonctionnalités ajoutées pour activer les composants principaux ?


Lorsque les composants principaux de Forms adaptatif sont activés pour votre environnement, un modèle de formulaire adaptatif basé sur les composants principaux vierge et le thème Canevas 3.0 sont ajoutés à votre environnement. Après avoir activé les composants principaux de Forms adaptatif pour votre environnement, vous pouvez :

* Création d’un Forms adaptatif basé sur des composants principaux.
* Créez des modèles de formulaires adaptatifs basés sur des composants principaux.
* Créez des thèmes personnalisés pour les modèles de formulaires adaptatifs basés sur les composants principaux.
* Servez les représentations JSON du formulaire adaptatif basé sur les composants principaux aux canaux tels que les applications mobiles, web, natives et les services qui nécessitent une représentation sans tête d’un formulaire.

## Prochaines étapes

* [Création d’un formulaire adaptatif basé sur des composants principaux](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Création ou ajout d’un formulaire adaptatif à une page AEM Sites ou à un fragment d’expérience](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Création de thèmes pour le Forms adaptatif basé sur les composants principaux](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Création d’un modèle pour le Forms adaptatif basé sur les composants principaux](template-editor.md)