---
title: Importation et gestion des applications
seo-title: Importation et gestion des applications
description: Découvrez comment importer et gérer des applications.
seo-description: Découvrez comment importer et gérer des applications.
uuid: 7fba6c4e-1a3e-4a4b-9201-acf2ff66a9df
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: dc53a6d0-317a-4abd-990c-455e13f8b824
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 98%

---


# Importation et gestion des applications{#import-and-manage-applications}

Dans AEM forms, une *application* est un conteneur destiné à stocker des actifs nécessaires à la mise en œuvre d’une solution AEM forms. Ces actifs peuvent être des conceptions de formulaires, des fragments de formulaires, des images, des processus, des fichiers DDX, des guides de formulaires, des pages HTML et des fichiers SWF. Durant la phase de développement d’un projet, les utilisateurs de Workbench peuvent déployer des applications directement à partir de l’affichage Applications dans Workbench. Une fois déployées, ces applications s’affichent dans Administration Console, dans l’onglet Applications de la page Gestion des applications.

Lorsqu’une application est terminée et prête à être déployée sur un serveur de production, l’utilisateur de Workbench crée un package de l’application sous forme de *fichier d’application AEM forms* (.lca). Un administrateur se sert ensuite d’Administration Console pour importer et déployer ce fichier d’application, à l’aide de l’onglet Applications de la page Gestion des applications.

Vous pouvez également utiliser l’onglet Archives de la page Gestion des applications pour importer les fichiers LCA créés à l’aide de Workbench 8.x.

>[!NOTE]
>
>la compatibilité des fichiers LCA issus d’une version ultérieure n’est pas nécessairement ascendante ; il s’agit là d’un problème connu. Bien qu’il soit possible d’afficher et d’importer des fichiers LCA d’une version ultérieure d’AEM forms (par exemple, d’une version non définitive), cette opération n’est pas prise en charge et peut entraîner un comportement aberrant.

Importez et gérez les applications créées avec Workbench dans l’onglet Applications. Les administrateurs d’applications peuvent également exporter la configuration d’exécution pour une application. L’exportation de la configuration d’exécution évite d’avoir à reconfigurer manuellement les paramètres dans l’environnement de production avant d’exécuter les applications déployées. Le fichier de configuration d’exécution contient les éléments suivants :

* les paramètres de configuration du service ;
* les paramètres de configuration du pool ;
* les paramètres de configuration du point de fin ;
* les paramètres de sécurité.

## Importation d’une application ou d’une archive {#import-an-application-or-archive}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cliquez sur Importer.
1. Cliquez sur Parcourir et sélectionnez le fichier LCA à importer, puis cliquez sur Aperçu. Les informations relatives à l’application s’affichent dans la page Aperçu de l’application.
1. (Facultatif) Pour afficher une liste des actifs contenus dans l’application, cliquez sur Afficher les éléments.
1. (Facultatif) Pour déployer les actifs au moment de l’exécution, sélectionnez Déployer les éléments à l’exécution à la fin de l’importation. Si vous ne sélectionnez pas cette option, vous pourrez déployer les actifs ultérieurement.
1. Cliquez sur Importer. L’application s’affiche dans l’onglet Applications.
1. Connectez-vous au référentiel CRX avec vos informations d’identification d’administrateur.
1. Accédez à content/dam/lcapplications.

   >[!NOTE]
   >
   >les applications importées s’affichent dans le nœud lcapplications.

1. Cliquez sur l’une des applications importées.

   L’onglet Propriétés sur le côté droit affiche les propriétés du nœud CRX sélectionné.

   La propriété **syncState** indique l’état de synchronisation des données entre le serveur AEM forms et le référentiel CRX. Dès que le processus d’importation commence, cet état est défini sur 0 (zéro). Cet état indique que les données ne sont pas synchronisées actuellement. Lorsque les données sont synchronisées, l’état est défini sur 1.

## Déploiement d’une application  {#deploy-an-application}

Vous pouvez déployer des applications importées par vous-même, ou des applications que des utilisateurs de Workbench ont importées à partir de Workbench.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cochez la case correspondant à l’application à déployer puis cliquez sur Déployer.
1. Cliquez sur OK dans la boîte de dialogue de confirmation.

## Annulation du déploiement d’une application  {#undeploy-an-application}

Vous pouvez annuler le déploiement des applications au moment de l’exécution.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cochez la case correspondant à l’application dont vous souhaitez annuler le déploiement puis cliquez sur Annuler le déploiement.
1. Cliquez sur OK dans la boîte de dialogue de confirmation.

## Suppression d’une application du serveur  {#remove-an-application-from-the-server}

Annulez le déploiement de l’application avant de la supprimer du serveur.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cochez la case correspondant à l’application à supprimer puis cliquez sur Supprimer.
1. Cliquez sur OK dans la boîte de dialogue de confirmation.

## Importation de la configuration d’exécution d’une application  {#import-an-application-s-runtime-configuration}

Si un administrateur d’applications a exporté la configuration d’exécution pour une application, vous pouvez l’importer dans l’application déployée. Vous pouvez l’importer à l’aide d’Administration Console ou via le déploiement LCA par scripts.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cliquez sur le nom de l’application.
1. Cliquez sur Importer configuration d’exécution.
1. Cliquez sur Parcourir et sélectionnez le fichier XML qui contient la configuration d’exécution.
1. Cliquez sur Importer.

## Exportation de la configuration d’exécution d’une application  {#export-an-application-s-runtime-configuration}

Vous pouvez exporter les informations de configuration d’exécution des applications déployées.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des applications.
1. Cliquez sur le nom de l’application.
1. Cliquez sur Exporter configuration d’exécution et enregistrez le fichier de configuration (XML) généré.

## Déploiement par scripts d’applications AEM forms  {#scripted-deployment-of-aem-forms-applications}

Vous pouvez également utiliser un outil de déploiement par scripts pour déployer des fichiers d’application, y compris un fichier settings.xml qui spécifie les paramètres suivants :

* les paramètres de configuration du service ;
* les paramètres de configuration du pool ;
* les paramètres de configuration du point de fin ;
* les paramètres de sécurité.

Le déploiement par script vous évite d’avoir à reconfigurer manuellement les paramètres dans l’environnement de production avant d’exécuter les applications déployées.

1. Ouvrez une invite de commande et accédez à *[la racine aem-forms]*/sdk/misc/Foundation/ArchiveManagement.
1. Pour des instructions plus détaillées, lisez le fichier ReadMe.txt.
1. Modifiez manuellement les fichiers scriptedDeploy.bat et sample-files/settings.xml, tel qu’indiqué dans le fichier ReadMe.txt.
1. Exécutez le fichier scriptedDeploy.bat. Cette action déploie le fichier d’archives AEM forms avec les paramètres de remplacement.

