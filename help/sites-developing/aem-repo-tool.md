---
title: Outil AEM Repo
seo-title: Outil AEM Repo
description: L’outil AEM Repo est une solution simple pour transférer du contenu JCR entre votre système de fichiers local et le serveur AEM via une ligne de commande comparable à FTP. L’outil AEM Repo est similaire à l’outil Jackrabbit FileVault, à la différence qu’il est plus rapide, a des dépendances minimales et est un simple script Bash.
seo-description: L’outil AEM Repo est une solution simple pour transférer du contenu JCR entre votre système de fichiers local et le serveur AEM via une ligne de commande comparable à FTP. L’outil AEM Repo est similaire à l’outil Jackrabbit FileVault, à la différence qu’il est plus rapide, a des dépendances minimales et est un simple script Bash.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 80%

---


# Outil AEM Repo{#aem-repo-tool}

L’outil AEM Repo est une solution simple pour transférer du contenu JCR entre votre système de fichiers local et le serveur AEM via une ligne de commande comparable à FTP. L&#39;outil AEM Repo est semblable à l&#39;outil [Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), mais il est plus rapide, avec des dépendances minimales et est un script bash simple.

Cet outil simplifie les transferts de fichiers qu’effectuent le développeur et peut également être intégré à IntelliJ et Eclipse pour optimiser l’activité de développement.

## Présentation {#overview}

Pour un chemin d&#39;accès donné dans une structure de fichier `jcr_root` sur le système de fichiers, AEM Repo Tool crée un package avec un filtre unique pour l&#39;ensemble de la sous-arborescence et le transmet au serveur (semblable à FTP `put`), le récupère du serveur ( `get`) ou compare les différences ( `status` et `diff`).

Cet outil ne prend pas en charge les chemins de filtre multiples ou `filter.xml` de FileVault.

>[!CAUTION]
>
>Veuillez noter que l’outil Repo AEM écrase toujours le fichier ou le répertoire spécifié dans son intégralité.

## Téléchargement et documentation {#download-and-documentation}

L’outil [AEM Repo Tool est disponible sur GitHub via ce lien](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) et s’accompagne d’instructions d’installation et d’utilisation détaillées.

Si vous souhaitez télécharger la source de l’outil Repo AEM, reportez-vous au projet GitHub ci-dessous.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrir le projet outils sur GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip).

