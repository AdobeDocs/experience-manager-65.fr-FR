---
title: Outil AEM Repo
description: AEM Repo Tool est une solution simple pour transférer du contenu JCR entre votre système de fichiers local et le serveur AEM par le biais de la ligne de commande comparable à FTP. L’outil AEM Repo est similaire à l’outil Jackrabbit FileVault, à la différence qu’il est plus rapide, a des dépendances minimales et est un simple script Bash.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 73%

---

# Outil AEM Repo{#aem-repo-tool}

L’outil AEM Repo est une solution simple pour transférer du contenu JCR entre votre système de fichiers local et le serveur AEM via une ligne de commande comparable à FTP. L’outil AEM Repo est similaire à l’[outil Jackrabbit FileVault](/help/sites-developing/ht-vlttool.md), à la différence qu’il est plus rapide, a des dépendances minimales et est un simple script Bash.

Cet outil simplifie le transfert des fichiers pour le développeur et peut également être intégré dans IntelliJ et Eclipse afin de rendre le développement encore plus efficace.

## du commerce électronique {#overview}

Pour un chemin donné dans une structure FileVault `jcr_root` dans le système de fichiers, l’outil AEM Repo crée un package avec un seul filtre pour l’ensemble de la sous-arborescence et le transmet en push au serveur (de façon similaire à la méthode `put` du FTP), l’extrait du serveur (`get`) ou compare les différences (`status` et `diff`).

Cet outil ne prend pas en charge les chemins de filtre multiples ou `filter.xml` de FileVault.

>[!CAUTION]
>
>L’outil AEM Repo Tool remplace toujours l’intégralité du fichier ou du répertoire spécifié.

## Téléchargement et documentation {#download-and-documentation}

L’outil [AEM Repo Tool est disponible sur GitHub via ce lien](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) et s’accompagne d’instructions d’installation et d’utilisation détaillées.

Si vous souhaitez télécharger la source de l’outil Repo AEM, consultez le projet GitHub lié ci-dessous.

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrir le projet outils sur GitHub](https://github.com/Adobe-Marketing-Cloud/tools)
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip).
