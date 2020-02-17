---
title: Création
seo-title: Création
description: Concepts de création dans AEM
seo-description: Concepts de création dans AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Création{#authoring}

## Concept de création (et de publication) {#concept-of-authoring-and-publishing}

AEM vous propose deux environnements :

* Création
* Publication

Ces environnements interagissent afin que vous puissiez rendre le contenu disponible sur votre site web, pour que vos visiteurs puissent le lire.

L’environnement de création fournit les mécanismes de création, de mise à jour et de révision de ce contenu avant de le publier :

* Un auteur crée et révise le contenu (qui peut être de plusieurs types, par ex. pages, ressources, publications, etc.)
* qui, à un moment donné, sera publié sur votre site web.

![chlimage_1-132](assets/chlimage_1-132.png)

Dans l’environnement de création, les fonctions d’AEM sont accessibles dans deux interfaces utilisateur. Dans l’environnement de publication, vous concevez l’aspect de l’interface proposée aux utilisateurs.

>[!NOTE]
>
>La documentation d’AEM est elle-même conçue dans AEM.
>
>Il est aussi utilisé, avec le dispatcher, pour la publication.

### Environnement de création {#author-environment}

The author works in what is known as the **author environment**. This provides an easy to use interface (graphical user interface (GUI or UI)) for creating the content. It is usually located behind a company&#39;s firewall that provides full protection and requires the author to login, using an account that has been assigned the appropriate access rights.

>[!NOTE]
>
>Votre compte doit disposer des droits d’accès appropriés pour la création, la modification ou la publication de contenu.

En fonction de la configuration de votre instance et de vos droits d’accès personnels, vous pouvez effectuer diverses tâches sur votre contenu, par exemple :

* générer un nouveau contenu ou modifier le contenu existant sur une page
* utiliser les modèles prédéfinis pour créer des pages de contenu ;
* créer, modifier et gérer vos ressources et collections
* créer, modifier et gérer vos publications ;
* développer vos campagnes et les ressources associées
* développer et gérer des sites communautaires
* déplacer, copier ou supprimer des pages de contenu, des ressources, etc. ;
* publier des pages, des ressources, etc. (ou annuler leur publication).

Certaines tâches administratives peuvent aussi vous aider à gérer votre contenu :

* worfklow qui déterminent le mode de gestion des modifications ; par exemple, appliquer une révision avant une publication.
* projets qui coordonnent des tâches individuelles.

>[!NOTE]
>
>Pour la plupart des tâches, l’environnement de création permet également d’[administrer](/help/sites-administering/home.md) AEM.

#### Environnement de publication {#publish-environment}

When ready, the AEM site&#39;s content is published to the **publish environment**. Ici, vos pages sont mises à la disposition de l’audience prévue, en fonction de l’aspect global de l’interface que vous avez conçue.

Dans le cas d’un site web ordinaire, l’environnement de publication est situé à l’intérieur de la zone DMZ ; en d’autres termes, il est disponible sur Internet, mais il ne bénéficie plus de la protection absolue de votre réseau interne.

Lorsque le site AEM est un [site communautaire](/help/communities/overview.md), ou inclut des [composants de Communities](/help/communities/author-communities.md), des utilisateurs (membres) connectés peuvent interagir avec les fonctions de Communities. Par exemple, ils peuvent publier sur un forum, publier un commentaire ou suivre d’autres membres. Les membres peuvent être autorisés à effectuer des activités normalement réservées à l’environnement de création, telles que la création de nouvelles pages (groupes de communautés), d’articles de blog et la modération des publications d’autres membres.

>[!NOTE]
>
>Il existe malheureusement une interférence dans la terminologie utilisée. Cela peut se produire avec les fonctions suivantes :
>
>* **Publier / Annuler la publication**
   >  Il s’agit des principaux termes des actions qui rendent votre contenu public dans votre environnement de publication (ou pas).
   >
   >
* **Activer / désactiver**
   >  Ces termes sont synonymes de publication/annulation de publication.
   >
   >
* **Répliquer / Réplication**
   >  Il s&#39;agit des termes techniques utilisés pour indiquer le mouvement des données (par exemple, contenu de la page, fichiers, code, commentaires des utilisateurs) d&#39;un environnement à un autre; c’est-à-dire lors de la publication ou de la réplication inversée des commentaires des utilisateurs.
>



#### Répartiteur {#dispatcher}

To optimize performance for visitors to your website, the **[dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)**implements load balancing and caching.
