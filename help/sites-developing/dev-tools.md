---
title: Outils de développement
seo-title: Outils de développement
description: Pour développer vos applications JCR, Apache Sling ou AEM, plusieurs jeux d’outils sont disponibles.
seo-description: Pour développer vos applications JCR, Apache Sling ou AEM, plusieurs jeux d’outils sont disponibles.
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 62%

---


# Outils de développement{#development-tools}

Pour développer vos applications JCR, Apache Sling ou AEM, les jeux d’outils suivants sont disponibles :

* one set consisting of [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) and WebDAV. CRXDE Lite est incorporé dans CRX/AEM et permet d’effectuer des tâches de développement standard dans le navigateur. Avec CRXDE Lite, vous pouvez créer et modifier des fichiers (par exemple, dotés des extensions .jsp et .java), des dossiers, des modèles, des composants, des boîtes de dialogue, des nœuds, des propriétés et des lots lors de la connexion et de l’intégration à SVN.

   CRXDE Lite est recommandé lorsque vous n’avez pas d’accès direct au serveur CRX/AEM, lorsque vous développez une application en étendant ou en modifiant les composants prêts à l’emploi et les lots Java ou lorsque vous n’avez pas besoin d’un débogueur dédié, de la saisie du code et de la mise en surbrillance de la syntaxe.

* one set consisting of an Integrated Development Environment (for example: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) or [IntelliJ](/help/sites-developing/ht-intellij.md)), a build tool (for example: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault which has been developed by Adobe to map a repository to a file system, a version control system (for example: Subversion), a bug tracker system (for example: Jira), a central dependency management system (for example: Apache Archiva) and a build automation system (for example: Apache Continuum).

   Cette configuration permet d’intégrer complètement votre application (contenu, code, configuration) dans tout environnement et processus de développement. Le lien entre les différents éléments est la représentation du système de fichiers du référentiel par l’intermédiaire de FileVault car tous les outils de développement mentionnés ci-dessus peuvent utiliser des fichiers.

## Extensions pour les environnements de développement intégrés {#extensions-for-integrated-development-environments}

Adobe a sorti les extensions suivantes :

* [Extension AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extension AEM Brackets](/help/sites-developing/aem-brackets.md)
* [Extension AEM IntelliJ (de Headwire)](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)

### Autres outils {#other-tools}

AEM est livré avec d’autres outils qui facilitent le développement :

* [Éditeur de boîtes de dialogue](/help/sites-developing/dialog-editor.md)
* [Utilisation du traducteur pour gérer les dictionnaires](/help/sites-developing/i18n-translator.md)
* [Gestion des packages à l’aide de Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Développement de projets AEM à l’aide d’Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Développement de projets AEM à l’aide de IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Utilisation de l’outil VLT](/help/sites-developing/ht-vlttool.md)
* [Utilisation de l’outil de serveur proxy](/help/sites-developing/ht-proxy-server.md)
* [Outil de conversion de boîte de dialogue](/help/sites-developing/dialog-conversion.md)
* [Outil AEM Repo](/help/sites-developing/aem-repo-tool.md)

Outils facilitant la création de projets :

* [Archétype de projet AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Modèles AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Le didacticiel suivant peut être intéressant pour le démarrage d’un nouveau projet AEM :
>[Prise en main de AEM Sites Partie 1 - Configuration du projet](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

