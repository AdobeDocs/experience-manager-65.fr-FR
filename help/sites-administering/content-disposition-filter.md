---
title: Filtre de disposition du contenu
description: Découvrez comment utiliser le filtre de disposition du contenu pour empêcher les attaques XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
exl-id: 1c3d0d48-5c31-42a8-8698-922d7c2127e9
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: ht
source-wordcount: '239'
ht-degree: 100%

---

# Filtre de disposition du contenu {#content-disposition-filter}

Le filtre de disposition de contenu est une fonctionnalité de sécurité contre les attaques XSS sur les fichiers SVG.

Une fois installé, le filtre bloque l’accès à toutes les ressources. Par exemple, il vous a été impossible d’afficher un PDF en ligne. Cette section décrit comment configurer le filtre selon vos besoins.

## Configuration du filtre de disposition du contenu {#configure-content-disposition-filter}

Vous pouvez visualiser le [filtre de disposition de contenu Apache Sling dans GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Les options du filtre de disposition du contenu offrent les fonctionnalités suivantes :

* **Chemins de disposition du contenu :** une liste des chemins d’accès pour lesquels le filtre est appliqué, suivie d’une liste de types MIME à exclure sur ce chemin. Ce chemin d’accès doit être un chemin absolu et peut contenir un caractère générique (`*`) à la fin, pour faire correspondre chaque chemin de ressource avec le préfixe de chemin donné. Par exemple : `/content/*:image/jpeg,image/svg+xml` applique le filtre à chaque nœud dans `/content?` à l’exception des images JPG et SVG.

* **Chemins d’accès aux ressources exclues :** une liste de ressources exclues. Chaque chemin doit être absolu et complet. La correspondance des préfixes et les caractères génériques ne sont pas pris en charge.

* **Activer pour tous les chemins d’accès aux ressources :** cet indicateur contrôle l’activation de ce filtre pour tous les chemins, à l’exception des chemins d’accès aux ressources exclues. En définissant cet indicateur sur « true », vous pouvez ignorer les chemins de disposition du contenu. Indépendamment de la configuration, seuls les chemins d’accès aux ressources sont concernés, lesquels contiennent une propriété nommée « `jcr:data` » ou « `jcr:content/jcr:data` ».
