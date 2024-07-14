---
title: Supprimer les sites Geometrixx
description: Découvrez comment supprimer l’exemple de contenu Geometrixx.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 100%

---


# Supprimer les sites Geometrixx{#removing-the-geometrixx-sites}

AEM s’accompagne d’un ensemble de sites web Geometrixx donnés à titre d’exemple. Vous pouvez supprimer cet exemple de contenu via le **Gestionnaire de modules**.

Les packages individuels liés à geometrixx sont les suivants :

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

Pour supprimer un package individuel, cliquez simplement sur **Désinstaller** pour ce package.

Il existe également un super package :

* `cq-geometrixx-all-pkg-5.6.12.zip`

Ce package comprend tous les packages individuels ci-dessus. Pour supprimer tout le contenu associé à geometrixx à la fois, cliquez sur **Désinstaller** sur ce package. Le super package passe alors au statut désinstallé et tous les packages qui le composent disparaissent de la vue du gestionnaire de modules.

Vous disposez à présent d’une instance AEM « vide », sans aucun site de démonstration.

>[!NOTE]
>
>Lors de la mise à niveau, les sites Geometrixx sont automatiquement réinstallés. Si vous n’avez pas besoin de ces exemples, vous pourrez supprimer les sites web Geometrixx après la mise à niveau.

