---
title: Filtre de disposition du contenu
seo-title: Filtre de disposition du contenu
description: Découvrez comment utiliser le filtre de disposition du contenu pour empêcher les attaques XSS.
seo-description: Découvrez comment utiliser le filtre de disposition du contenu pour empêcher les attaques XSS.
uuid: 145a88e0-9fa8-42db-b189-eda507c33049
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
discoiquuid: badfaa18-472e-4777-a7dc-9c28441b38b7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 48%

---


# Filtre de disposition du contenu{#content-disposition-filter}

Le filtre de disposition du contenu est une fonctionnalité de sécurité permettant de lutter contre les attaques XSS sur des fichiers SVG.

Une fois installé, le filtre bloque l’accès à toutes les ressources. Par exemple, il vous a été impossible d’afficher un PDF en ligne. Cette section explique comment configurer ce filtre en fonction de vos besoins.

## Configuration du filtre de disposition du contenu {#configure-content-disposition-filter}

You can view the [Apache Sling Content Disposition Filter in GitHub](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java).

Les options Filtre de disposition du contenu offrent les fonctionnalités suivantes :

* Chemins d’accès à la disposition du contenu : liste de chemins d&#39;accès où le filtre sera appliqué, suivie d&#39;une liste de types MIME à exclure sur ce chemin. Ce chemin doit être un chemin absolu et peut contenir un caractère générique (&#39;&amp;ast;&#39;) à la fin, pour faire correspondre chaque chemin de ressource avec le préfixe de chemin d&#39;accès donné. Par exemple : /content/&amp;ast;:image/jpeg,image/svg+xml &quot; applique le filtre à chaque noeud de /content, à l’exception des images jpg et svg

* Chemins d’accès aux ressources exclues : une liste de ressources exclues. Chaque chemin doit être absolu et complet. La correspondance des préfixes et les caractères génériques ne sont pas pris en charge.

* Activer pour tous les chemins d’accès aux ressources : cet indicateur contrôle l’activation de ce filtre pour tous les chemins, à l’exception des chemins d’accès aux ressources exclues. En définissant cette valeur sur « true », vous pouvez ignorer les chemins de disposition du contenu. Indépendamment de la configuration, seuls les chemins de ressources sont couverts qui contiennent une propriété nommée jcr:data ou jcr:content jcr:data.

