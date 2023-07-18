---
title: Outils de développement
description: Pour développer vos applications JCR, Apache Sling ou Adobe Experience Manager, plusieurs ensembles d’outils sont disponibles.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 36%

---

# Outils de développement{#development-tools}

Pour développer vos applications JCR, Apache Sling ou Adobe Experience Manager (AEM), les ensembles d’outils suivants sont disponibles :

* Un jeu composé de [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) et WebDAV. CRXDE Lite est incorporé dans CRX/AEM et permet d’effectuer des tâches de développement standard dans le navigateur. Avec CRXDE Lite, vous pouvez créer et modifier des fichiers (tels que .jsp et .java), des dossiers, des modèles, des composants, des boîtes de dialogue, des noeuds, des propriétés et des lots lors de la journalisation et de l’intégration à SVN.

  CRXDE Lite est recommandé lorsque vous n’avez pas d’accès direct au serveur CRX/AEM, lorsque vous développez une application en étendant ou modifiant les composants prêts à l’emploi et les lots Java™ ou lorsque vous n’avez pas besoin d’un débogueur dédié, de la complétion de code et de la mise en surbrillance de la syntaxe.

* un ensemble constitué des éléments suivants :
   * Un Environnement De Développement Intégré. Par exemple : [Eclipse](/help/sites-developing/howto-projects-eclipse.md) ou [IntelliJ](/help/sites-developing/ht-intellij.md).
   * Un outil de création. Par exemple : [Apache Maven](/help/sites-developing/ht-projects-maven.md).
   * FileVault qui a été développé par Adobe pour mapper un référentiel à un système de fichiers, un système de contrôle de version. Par exemple, Subversion.
   * Système de suivi des bogues. Par exemple, Jira.
   * Un système central de gestion des dépendances. Par exemple, Apache Archiva.
   * Et un système d&#39;automatisation de la construction. Par exemple, Apache Continuum.

  Cette configuration vous permet d’intégrer complètement votre application (contenu, code, configuration) dans n’importe quel environnement et processus de développement. Le lien entre les différents éléments est la représentation du système de fichiers du référentiel via FileVault, car tous les outils de développement mentionnés précédemment peuvent fonctionner avec des fichiers.

## Extensions pour les environnements de développement intégrés {#extensions-for-integrated-development-environments}

Adobe a publié les extensions suivantes :

* [Extension AEM Eclipse](/help/sites-developing/aem-eclipse.md)
* [Extension AEM Brackets](/help/sites-developing/aem-brackets.md)

### Autres outils {#other-tools}

AEM des navires dotés d&#39;autres outils qui facilitent le développement :

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

* [Archétype de projet AEM](https://github.com/adobe/aem-project-archetype)
* [Modèles AEM Lazybones](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>Le tutoriel suivant peut s’avérer intéressant pour démarrer un nouveau projet AEM :
>[Prise en main d’AEM Sites - Partie 1 - Configuration du projet](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
