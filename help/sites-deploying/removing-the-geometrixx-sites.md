---
title: Suppression des sites de Geometrixx
description: Découvrez comment supprimer l’exemple de contenu de Geometrixx.
uuid: 07d20837-3375-4e64-bb07-3e4d10452335
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 56761a36-ce21-46e1-856f-75a7e94acae9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 15%

---


# Suppression des sites de Geometrixx{#removing-the-geometrixx-sites}

AEM s’accompagne d’un ensemble de sites web Geometrixx donnés à titre d’exemple. Vous pouvez supprimer cet exemple de contenu via la fonction **Gestionnaire de modules**.

Les packages individuels liés à geometrixx sont les suivants :

* `cq-geometrixx-outdoors-ugc-pkg-<version>.zip`
* `cq-geometrixx-pkg-<version>.zip`
* `cq-content-mac-<version>.zip`
* `cq-geometrixx-login-pkg-<version>.zip`
* `cq-geometrixx-users-pkg-<version>.zip`
* `cq-geometrixx-workflow-pkg-<version>.zip`
* `cq-geometrixx-outdoors-pkg-<version>.zip`
* `cq-geometrixx-commons-pkg-<version>.zip`
* `cq-geometrixx-media-pkg-<version>.zip`

Pour supprimer un module individuel, cliquez simplement sur **Désinstaller** sur ce paquet.

Il existe également un super package :

* `cq-geometrixx-all-pkg-5.6.12.zip`

Ce package comprend tous les packages individuels ci-dessus. Pour supprimer tout le contenu associé à geometrixx à la fois, cliquez sur **Désinstaller** sur ce paquet. Le super-package passe à l’état désinstallé, et tous les packages individuels disparaissent de la vue Package Manager.

Vous disposez à présent d’une instance AEM « vide », sans aucun site de démonstration.

>[!NOTE]
>
>Lors de la mise à niveau, les sites Geometrixx sont automatiquement réinstallés. Supprimez les sites web Geometrixx après la mise à niveau si vous ne souhaitez pas ces exemples.

