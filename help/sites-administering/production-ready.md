---
title: Exécution d’AEM en mode Prêt pour l’exploitation
seo-title: Running AEM in Production Ready Mode
description: Découvrez comment exécuter AEM en mode Prêt pour la production.
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 100%

---

# Exécution d’AEM en mode Prêt pour l’exploitation{#running-aem-in-production-ready-mode}

Avec AEM 6.1, Adobe introduit le nouveau mode d’exécution `"nosamplecontent"` visant à automatiser les étapes nécessaires pour préparer le déploiement d’une instance AEM dans un environnement d’exploitation.

Le nouveau mode d’exécution configure non seulement automatiquement l’instance pour qu’elle soit conforme aux bonnes pratiques de sécurité décrites dans la liste de contrôle de sécurité, mais en plus supprime tous les exemples d’applications et de configurations geometrixx dans le processus.

>[!NOTE]
>
>Puisque, pour des raisons pratiques, le mode Prêt pour la production d’AEM couvre uniquement une majorité de tâches requises pour sécuriser une instance, il est vivement conseillé de consulter la [liste de contrôle de sécurité](/help/sites-administering/security-checklist.md) avant de passer à la publication dans votre environnement de production.
>
>De plus, notez qu’exécuter AEM en mode Prêt pour la production aura pour effet de désactiver l’accès à CRXDE Lite. Si vous en avez besoin à des fins de débogage, consultez la section [Activation de CRXDE Lite dans AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Pour pouvoir exécuter AEM en mode Prêt pour l’exploitation, il vous suffit d’ajouter le composant `nosamplecontent` via le commutateur de mode d’exécution `-r` à vos arguments de démarrage existants :

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Par exemple, vous pouvez utiliser le mode Prêt pour l’exploitation afin de lancer une instance de création avec la persistance MongoDB comme suit :

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Modifications faisant partie du mode Prêt pour l’exploitation {#changes-part-of-the-production-ready-mode}

Plus spécifiquement, les modifications de configuration suivantes seront effectuées lorsque AEM est exécuté en mode Prêt pour l’exploitation :

1. Le **lot de prise en charge CRXDE** (`com.adobe.granite.crxde-support`) est désactivé par défaut dans le mode Prêt pour l’exploitation. Il peut être installé à tout moment à partir du référentiel Maven public Adobe. La version 3.0.0 est requise pour AEM 6.1.

1. Le lot **Accès aux référentiels WebDAV simple Apache Sling** (`org.apache.sling.jcr.webdav`) ne sera disponible que sur les instances de **création**.

1. Les utilisateurs nouvellement créés devront changer de mot de passe à la première connexion. Ceci ne s’applique pas à l’administrateur.
1. L’option **Générer les informations de débogage** est désactivée pour le **gestionnaire de script Java Apache Sling**.

1. Les options **Contenu mappé** et **Générer les informations de débogage** sont désactivées pour le **gestionnaire de script JSP Apache Sling**.

1. Le **filtre de gestion de contenu web Day CQ** est défini sur `edit` sur les instances de **création** et sur `disabled` sur les instances de **publication**.

1. **Le gestionnaire de bibliothèque HTML Adobe Granite** est configuré avec les paramètres suivants :

   1. **Minimiser :** `enabled`
   1. **Déboguer :** `disabled`
   1. **Gzip :** `enabled`
   1. **Synchroniser :** `disabled`

1. Le servlet **GET Apache Sling** est configuré pour prendre en charge les configurations sécurisées par défaut, comme suit :

| **Configuration** | **Auteur** | **Publication** |
|---|---|---|
| Rendu TXT | disabled | disabled |
| Rendu HTML | disabled | disabled |
| Rendu JSON | enabled | enabled |
| Rendu XML | disabled | disabled |
| json.maximumresults | 1000 | 100 |
| Indexation automatique | disabled | disabled |
