---
title: Messages d’erreur relatifs aux API obsolètes dans les journaux d’erreur
description: Messages d’erreur relatifs aux API obsolètes dans les journaux d’erreur
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---


# Messages d’erreur relatifs aux API obsolètes dans les journaux d’erreur {#error-messages-about-deprecated-apis-in-error-logs}

Le problème s’applique aux versions suivantes :

* Experience Manager 6.5 Forms

## Problème {#issue}

* Les messages d’erreur suivants apparaissent dans le fichier error.log :
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## Résolution {#workaround}

1. Installer [Experience Manager Forms Service Pack 13 ou version ultérieure (6.5.13.0 ou version ultérieure)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr)
1. Utilisez le lien suivant pour télécharger le package (fichier .jar avec résolution) depuis Distribution logicielle :

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Ouvrez Experience Manager Configuration Manager et installez le fichier com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar téléchargé.

Le problème est résolu.