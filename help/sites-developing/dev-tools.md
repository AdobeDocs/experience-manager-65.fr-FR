---
title: Outils de développement
seo-title: Development Tools
description: Pour développer vos applications JCR, Apache Sling ou AEM, plusieurs jeux d’outils sont disponibles.
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: 4967a6d9ad92272a1ff442456fe65de51cc46a73
workflow-type: ht
source-wordcount: '373'
ht-degree: 100%

---

# Outils de développement{#development-tools}

Pour développer vos applications JCR, Apache Sling ou AEM, les jeux d’outils suivants sont disponibles :

* Un jeu composé de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) et WebDAV. CRXDE Lite est incorporé dans CRX/AEM et permet d’effectuer des tâches de développement standard dans le navigateur. Avec CRXDE Lite, vous pouvez créer et modifier des fichiers (par exemple, dotés des extensions .jsp et .java), des dossiers, des modèles, des composants, des boîtes de dialogue, des nœuds, des propriétés et des lots lors de la connexion et de l’intégration à SVN.

   CRXDE Lite est recommandé si vous ne disposez pas d’un accès direct au serveur CRX/AEM, lorsque vous développez une application en étendant ou en modifiant les composants prêts à l’emploi et les bundles Java ou lorsque vous n’avez pas besoin d’un débogueur dédié, de la complétion de code et de la mise en surbrillance de la syntaxe.

* Un jeu composé d’un environnement de développement intégré (IDE) (par exemple : [Eclipse](/help/sites-developing/howto-projects-eclipse.md) ou [IntelliJ](/help/sites-developing/ht-intellij.md)), d’un outil de génération (par exemple : [Apache Maven](/help/sites-developing/ht-projects-maven.md)), de FileVault développé par Adobe pour mapper un référentiel à un système de fichiers, d’un système de contrôle de versions (par exemple : Subversion), d’un système de suivi des bogues (par exemple : Jira), d’un système central de gestion des dépendances (par exemple : Apache Archiva) et d’un système d’automatisation de la génération (par exemple : Apache Continuum).

   Cette configuration permet d’intégrer complètement votre application (contenu, code, configuration) dans tout environnement et processus de développement. Le lien entre les différents éléments est la représentation du système de fichiers du référentiel par l’intermédiaire de FileVault car tous les outils de développement mentionnés ci-dessus peuvent utiliser des fichiers.

## Extensions pour les environnements de développement intégrés {#extensions-for-integrated-development-environments}

Adobe a sorti les extensions suivantes :

* [Extension AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extension AEM Brackets](/help/sites-developing/aem-brackets.md)

### Autres outils {#other-tools}

AEM est livré avec d’autres outils qui facilitent le développement :

* [Éditeur de boîtes de dialogue](/help/sites-developing/dialog-editor.md)
* [Utilisation du traducteur pour gérer les dictionnaires](/help/sites-developing/i18n-translator.md)
* [Gestion des packages à l’aide de Maven](/help/sites-developing/vlt-mavenplugin.md)
* [Développement de projets AEM à l’aide d’Eclipse](/help/sites-developing/howto-projects-eclipse.md)
* [Création de projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md)
* [Développement de projets AEM à l’aide de IntelliJ IDEA](/help/sites-developing/ht-intellij.md)
* [Utilisation de l’outil VLT](/help/sites-developing/ht-vlttool.md)
* [Utilisation de l’outil de serveur proxy](/help/sites-developing/ht-proxy-server.md)
* [Outils de modernisation d’AEM](/help/sites-developing/modernization-tools.md)
* [Outil AEM Repo](/help/sites-developing/aem-repo-tool.md)

Outils facilitant la création de projets :

* [Archétype de projet AEM](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [Modèles AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Le tutoriel suivant peut s’avérer intéressant pour démarrer un nouveau projet AEM :
>[Prise en main d’AEM Sites - Partie 1 - Configuration du projet](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
