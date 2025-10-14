---
title: Comment activer les composants principaux des formulaires adaptatifs sur AEM Forms 6.5 ?
description: Guide détaillé pour vous aider à activer les composants principaux des formulaires adaptatifs dans un environnement AEM Forms 6.5.
keywords: Activer les composants principaux, Composants principaux des formulaires adaptatifs, Composants principaux sur la version 6.5, Composants principaux des formulaires adaptatifs sur AEM 6.5, Composants principaux FA sur AEM 6.5, Composants principaux Forms 6.5
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 6585ea71-6242-47d3-bc59-6f603cf507b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 0487a5669fbaab35974eb85eb099b82e0847a4f9
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 96%

---

# Activer les composants principaux des formulaires adaptatifs sur AEM Forms 6.5 {#enable-adaptive-forms-core-components}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components.html?lang=fr) |
| AEM 6.5 | Cet article |

<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

L’activation des composants principaux des formulaires adaptatifs vous permet de commencer à créer, à publier et à diffuser des [formulaires adaptatifs basés sur des composants principaux](create-an-adaptive-form-core-components.md) et des [formulaires adaptatifs découplés](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=fr) de votre environnement AEM Forms 6.5.

Pour activer les composants principaux des formulaires adaptatifs sur votre environnement AEM Forms 6.5, configurez et déployez un [archétype AEM 41 ou version ultérieure](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=fr) basé sur un projet (avec les options de formulaire activées) sur toutes vos instances de création et de publication.

Cet article fournit des instructions détaillées sur la configuration et le déploiement de l’archétype AEM 41 ou version ultérieure sur votre environnement AEM Forms 6.5 pour activer les composants principaux des formulaires adaptatifs. Vous pouvez vous référer à la liste ci-dessous pour les versions compatibles avec **AEM 6.5** pour activer les composants principaux de Forms :

## Conditions préalables {#prerequisites}

Avant d’activer les composants principaux des formulaires adaptatifs dans un environnement AEM Forms 6.5 :

* [Effectuez un mise à niveau vers le pack de services 16 d’AEM 6.5 Forms (6.5.16.0) ou une version ultérieure](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=fr).

* Installez la dernière version d’[Apache Maven](https://maven.apache.org/download.cgi).

* Installez un éditeur de texte brut. Par exemple, Microsoft Visual Studio Code.

## Créer et déployer le dernier projet d’archétype AEM

Pour créer un projet d’archétype AEM 41 ou [version ultérieure](https://github.com/adobe/aem-project-archetype) et le déployer sur toutes vos instances de création et de publication, procédez comme suit :

1. Connectez-vous à l’ordinateur qui héberge et exécute votre instance AEM 6.5 Forms en tant qu’administrateur ou administratrice.
1. Ouvrez l’invite de commande ou le terminal et exécutez la commande suivante pour créer un projet d’archétype AEM (avec les options de formulaire activées) :

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
      -D aemVersion="6.5.23" 
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
      -D aemVersion="6.5.23" 
   ```

   Lorsque vous exécutez la commande ci-dessus, tenez compte des points suivants :

   * Définissez la propriété `archetypeVersion` sur `41` ou plus. Pour obtenir la dernière version, reportez-vous à la section de configuration requise dans la documentation [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype).

   * Mettez à jour la commande afin de refléter les valeurs spécifiques de votre environnement, y compris pour `appTitle`, `appId` et `groupId`. Définissez également la valeur de la propriété `includeFormsenrollment` sur `y`. Si vous utilisez le portail Formulaires, définissez l’option `includeExamples=y` de façon à inclure les composants principaux du portail Formulaires dans votre projet.


1. (Uniquement pour les projets basés sur l’archétype 41) Une fois le projet d’archétype AEM créé, activez les thèmes des formulaires adaptatifs basés sur les composants principaux. Pour activer les thèmes, procédez comme suit :

   1. Ouvrez le [Dossier du projet d’archétype AEM]/ui.apps/src/main/content/jcr_root/apps/__appId__/components/adaptiveForm/page/customheaderlibs.html pour modification :

   1. Ajoutez le code suivant à la ligne 21 :

      ```XML
      <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html"
      data-sly-use.formstructparser="com.adobe.cq.forms.core.components.models.form.FormStructureParser"
      data-sly-test.themeClientLibRef="${formstructparser.themeClientLibRefFromFormContainer}">
      <sly data-sly-test="${themeClientLibRef}" data-sly-call="${clientlib.css @ categories=themeClientLibRef}"/>
      </sly>
      ```

      ![Ajouter le code mentionné ci-dessus à la ligne 21](/help/forms/using/assets/code-to-enable-themes.png)

   1. Enregistrez et fermez le fichier.

1. Mettez à jour le projet pour inclure la dernière version des composants principaux des formulaires :

   1. Ouvrez le [Dossier du projet d’archétype AEM]/pom.xml pour modification.
   1. Définissez la version de `core.forms.components.version` et de `core.forms.components.af.version` sur la version des [derniers composants principaux de formulaires](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=fr#aem-as-form-version-history) et assurez-vous que les deux ont la même version que la version des **composants principaux de formulaires** mentionnée dans le tableau. Définissez la version de `core.wcm.components.version` comme indiqué dans les [composants principaux WCM](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/versions.html?lang=fr).

      >[!WARNING]
      >
      >* Lors de la création d’un projet d’archétype avec la version 45, `[AEM Archetype Project Folder]/pom.xml` définit initialement la version des composants principaux de formulaires sur 1.1.28. Avant de créer ou de déployer le projet d’archétype, mettez à jour la version des composants principaux de formulaires vers la version 1.1.26. Vous trouverez la dernière version dans l’[historique des versions d’AEM 6.5 Forms](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/version.html?lang=fr#aem-as-form-version-history).

      >[!NOTE]
      >
      >* Si vous configurez une autre topologie, assurez-vous que les URL d’envoi, de préremplissage et autres URL requises, ainsi que les sélecteurs nécessaires (par exemple, `/content/forms/*model.json`), sont ajoutés à la liste autorisée au niveau de la couche Dispatcher.

   1. Enregistrez et fermez le fichier.


1. Une fois le projet d’archétype AEM créé, créez le package de déploiement pour votre environnement. Pour créer le package, procédez comme suit :

   1. Accédez au répertoire racine de votre projet d’archétype AEM.

   1. Exécutez la commande suivante pour créer le projet d’archétype AEM pour votre environnement :

      ```Shell
      mvn clean install
      ```

      ![archetypebuild-success](/help/forms/using/assets/corecomponent-build-successful.png)


   Une fois le projet d’archétype AEM créé, un package AEM est généré. Vous trouverez le package dans le [Dossier du projet d’archétype AEM]\all\target\[appid].all-[version].zip

1. Utilisez le [Gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) pour déployer le package [Dossier du projet d’archétype AEM]\all\target\[appid].all-[version].zip sur toutes les instances de création et de publication.

>[!NOTE]
>
>
>
> * Si vous rencontrez des difficultés pour accéder à la boîte de dialogue de connexion sur une instance de publication, essayez d’installer le module via le gestionnaire de modules à l’aide de l’URL `http://[Publish Server URL]:[PORT]/system/console` pour vous connecter. Cela vous permet d’accéder à la page de connexion de l’instance de publication et de poursuivre le processus d’installation.
> * Ne supprimez pas le projet d’archétype après son déploiement dans votre environnement. Le projet d’archétype est nécessaire pour ajouter des thèmes de composants principaux de formulaires adaptatifs nouveaux ou personnalisés à votre environnement.

Les composants principaux sont activés pour votre environnement. Un modèle vierge de formulaire adaptatif basé sur des composants principaux et un thème Canvas 3.0 sont déployés sur votre environnement. Vous pouvez maintenant [créer un formulaire adaptatif basé sur les composants principaux](create-an-adaptive-form-core-components.md).

## Questions fréquentes

### Que sont les composants principaux ?

Les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) sont un ensemble de composants WCM (Web Content Management, gestion de contenu web) normalisés pour AEM dont l’objectif est d’accélérer le développement et de réduire les coûts de maintenance de vos sites web.

### Quelles sont les fonctionnalités des composants principaux ?


Lorsque les composants principaux des formulaires adaptatifs sont activés pour votre environnement, un modèle de formulaire adaptatif vierge basé sur les composants principaux et le thème Canvas 3.0 sont ajoutés à votre environnement. Après avoir activé les composants principaux des formulaires adaptatifs pour votre environnement, vous pouvez :

* Créer un formulaire adaptatif basé sur des composants principaux.
* créer des modèles de formulaires adaptatifs basés sur des composants principaux ;
* créer des thèmes personnalisés pour les modèles de formulaires adaptatifs basés sur des composants principaux ;
* Diffuser les représentations JSON des formulaires adaptatifs basés sur les composants principaux à divers canaux tels que les applications mobiles, web et natives, ainsi que les services qui nécessitent une représentation découplée d’un formulaire.

## Prochaines étapes

* [Création d’un formulaire adaptatif basé sur des composants principaux](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Création ou ajout d’un formulaire adaptatif à une page AEM Sites ou à un fragment d’expérience](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Créer des thèmes pour formulaires adaptatifs basés sur les composants principaux](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [Création d’un modèle pour les formulaires adaptatifs basés sur les composants principaux](template-editor.md)
