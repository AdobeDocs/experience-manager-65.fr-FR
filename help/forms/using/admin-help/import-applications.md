---
title: Importer et gérer des applications
description: Découvrez comment importer et gérer des applications. Une application est un conteneur destiné à stocker des ressources requises pour la mise en oeuvre d’une solution d’AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: f17726c0-3591-4d25-a8b5-3a7024249a56
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 3%

---

# Importer et gérer des applications{#import-and-manage-applications}

Dans AEM formulaires, une *application* est un conteneur destiné à stocker les ressources requises pour la mise en oeuvre d’une solution d’AEM forms. Les conceptions de formulaire, les fragments de formulaire, les images, les processus, les fichiers DDX, les guides de formulaire, les pages de HTML et les fichiers de SWF sont des exemples de ressources. Pendant la phase de développement d’un projet, les utilisateurs de Workbench peuvent déployer des applications directement à partir de la vue Applications de Workbench. Une fois déployées, ces applications s’affichent dans Administration Console, dans l’onglet Applications de la page Gestion des applications.

Lorsqu’une application est terminée et prête à être déployée sur un serveur de production, l’utilisateur de Workbench la regroupe en une *AEM fichier d’application de formulaires* (.lca). Ensuite, un administrateur utilise Administration Console pour importer et déployer le fichier de l’application, à l’aide de l’onglet Applications de la page Gestion des applications.

Vous pouvez également utiliser l’onglet Archives de la page Gestion des applications pour importer les fichiers LCA créés à l’aide de Workbench 8.x.

>[!NOTE]
>
>Il existe un problème connu selon lequel les fichiers LCA d’une version ultérieure ne sont pas nécessairement rétrocompatibles. Bien qu’il soit possible d’afficher et d’importer des fichiers LCA à partir d’une version ultérieure d’AEM forms (par exemple, une version d’aperçu), cette opération n’est pas prise en charge et peut entraîner un comportement aberrant.

Utilisez l’onglet Applications pour importer et gérer les applications créées dans Workbench. Les administrateurs d’applications peuvent également exporter la configuration d’exécution d’une application. L’exportation de la configuration d’exécution élimine la nécessité de reconfigurer manuellement les paramètres dans l’environnement de production avant de démarrer les applications déployées. Le fichier de configuration d’exécution contient :

* paramètres de configuration du service
* paramètres de configuration du pool
* paramètres de configuration des points d’entrée
* profils de sécurité

## Importer une application ou une archive {#import-an-application-or-archive}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cliquez sur Importer.
1. Cliquez sur Parcourir et sélectionnez le fichier .lca à importer, puis cliquez sur Aperçu. La page Aperçu de l’application affiche des informations sur l’application.
1. (Facultatif) Pour afficher la liste des actifs contenus dans l’application, cliquez sur Afficher les actifs.
1. (Facultatif) Pour déployer les actifs au moment de l’exécution, sélectionnez Déployer les actifs au moment de l’exécution à la fin de l’importation. Si vous ne sélectionnez pas cette option, vous pouvez déployer les ressources ultérieurement.
1. Cliquez sur Importer. L’application apparaît dans l’onglet Applications .
1. Connectez-vous au référentiel CRX avec les informations d’identification de l’administrateur.
1. Accédez à content/dam/lcapplications

   >[!NOTE]
   >
   >Les applications importées s&#39;affichent dans le noeud lcapplications .

1. Cliquez sur l’une des applications importées.

   L’onglet Propriétés à droite affiche les propriétés du noeud CRX sélectionné.

   La variable **syncState** indique l’état de synchronisation des données entre AEM serveur forms et le référentiel CRX. Dès que le processus d’importation commence, cet état est défini sur 0 (zéro). Cet état indique que les données ne sont actuellement pas synchronisées. Lorsque les données sont synchronisées, l’état est défini sur 1.

## Déployer une application {#deploy-an-application}

Vous pouvez déployer des applications que vous avez importées ou que des utilisateurs de Workbench ont importées depuis Workbench.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cochez la case en regard de l’application à déployer et cliquez sur Déployer.
1. Cliquez sur OK dans la boîte de dialogue de confirmation qui s’affiche.

## Annulation du déploiement d’une application {#undeploy-an-application}

Vous pouvez annuler le déploiement des applications à partir du runtime.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cochez la case en regard de l’application dont vous souhaitez annuler le déploiement, puis cliquez sur Annuler le déploiement.
1. Cliquez sur OK dans la boîte de dialogue de confirmation qui s’affiche.

## Suppression d’une application du serveur {#remove-an-application-from-the-server}

Annulez le déploiement de l’application avant de la supprimer du serveur.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cochez la case en regard de l’application à supprimer, puis cliquez sur Supprimer.
1. Cliquez sur OK dans la boîte de dialogue de confirmation qui s’affiche.

## Importation de la configuration d’exécution d’une application {#import-an-application-s-runtime-configuration}

Si un administrateur d’applications a exporté la configuration d’exécution pour une application, vous pouvez l’importer dans l’application déployée. Vous pouvez l’importer à l’aide de la console d’administration ou via un déploiement LCA par script.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cliquez sur le nom de l’application.
1. Cliquez sur Importer la configuration d’exécution.
1. Cliquez sur Parcourir et sélectionnez le fichier XML qui contient la configuration d’exécution.
1. Cliquez sur Importer.

## Exportation de la configuration d’exécution d’une application {#export-an-application-s-runtime-configuration}

Vous pouvez exporter les informations de configuration d’exécution pour les applications déployées.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cliquez sur le nom de l’application.
1. Cliquez sur Exporter la configuration d’exécution et enregistrez le fichier de configuration (XML) généré.

## Déploiement par script des applications AEM forms {#scripted-deployment-of-aem-forms-applications}

Vous pouvez également utiliser un outil de déploiement par script pour déployer les fichiers d’application, y compris un fichier settings.xml spécifiant les paramètres suivants :

* paramètres de configuration du service
* paramètres de configuration du pool
* paramètres de configuration des points d’entrée
* profils de sécurité

Le déploiement par script élimine la nécessité de reconfigurer manuellement les paramètres dans l’environnement de production avant de démarrer les applications déployées.

1. A l’invite de commande, accédez à *[aem-forms root]*/sdk/misc/Foundation/ArchiveManagement.
1. Consultez le fichier ReadMe.txt pour obtenir des instructions plus détaillées.
1. Modifiez manuellement les fichiers scriptedDeploy.bat et sample-files/sample.xml comme décrit dans le fichier readme.txt.
1. Exécutez le fichier scriptedDeploy.bat . Cette action déploie le fichier d’archive d’AEM forms avec les paramètres de remplacement.
