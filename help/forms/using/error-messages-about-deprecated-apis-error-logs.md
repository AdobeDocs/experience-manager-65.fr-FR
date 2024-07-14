---
title: Messages d’erreur relatifs aux API obsolètes dans les journaux d’erreurs
description: Messages d’erreur relatifs aux API obsolètes dans les journaux d’erreurs
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 100%

---


# Messages d’erreur relatifs aux API obsolètes dans les journaux d’erreurs {#error-messages-about-deprecated-apis-in-error-logs}

Le problème s’applique aux versions suivantes :

* Formulaires avec Experience Manager 6.5

## Problème {#issue}

* Les messages d’erreur suivants apparaissent dans le fichier error.log :
  ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## Résolution {#workaround}

1. Installer [Experience Manager Forms Service Pack 13 ou version ultérieure (6.5.13.0 ou version ultérieure)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr)
1. Utiliser le lien suivant pour télécharger le package (fichier .jar avec résolution) depuis la Distribution logicielle :

   https://experience.adobe.com/#/downloads/content/software-distribution/r/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Ouvrir le Gestionnaire e configuration d’Experience Manager et installer le fichier com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar téléchargé.

Le problème est résolu.