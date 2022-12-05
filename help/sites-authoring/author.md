---
title: Création
seo-title: Authoring
description: Concepts de création dans AEM
seo-description: Concepts of authoring in AEM
uuid: eaa5f613-a138-4215-8f84-dfc962fe7fa7
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 81ff6f6f-11b3-4f8e-80e6-b3e104158394
docset: aem65
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Création  {#authoring}

## Concept de création (et de publication) {#concept-of-authoring-and-publishing}

AEM vous propose deux environnements :

* Création
* Publication

Ces environnements interagissent afin que vous puissiez rendre le contenu disponible sur votre site web, pour que vos visiteurs puissent le lire.

L’environnement de création fournit les mécanismes de création, de mise à jour et de révision de ce contenu avant de le publier :

* Un auteur crée et révise le contenu (qui peut être de plusieurs types, par exemple des pages, des ressources, des publications, etc.)
* qui, à un moment donné, sera publié sur votre site Web.

![chlimage_1-132](assets/chlimage_1-132.png)

Dans l’environnement de création, les fonctions d’AEM sont accessibles dans deux interfaces utilisateur. Dans l’environnement de publication, vous concevez l’aspect de l’interface proposée aux utilisateurs.

### Environnement de création {#author-environment}

L’auteur travaille dans ce qu’on appelle l’**environnement de création**. Il s’agit d’une interface facile à utiliser (interface utilisateur graphique) pour créer le contenu. En fait, cette interface se trouve habituellement derrière le pare-feu d’une entreprise qui fournit une protection complète et implique que l’auteur se connecte à l’aide d’un compte doté des droits d’accès appropriés.

>[!NOTE]
>
>Votre compte doit disposer des droits d’accès appropriés pour la création, la modification ou la publication de contenu.

En fonction de la configuration de votre instance et de vos droits d’accès personnels, vous pouvez effectuer diverses tâches sur votre contenu, par exemple :

* générer un nouveau contenu ou modifier le contenu existant sur une page
* utiliser les modèles prédéfinis pour créer des pages de contenu ;
* créer, modifier et gérer vos ressources et collections ;
* créer, modifier et gérer vos publications ;
* développer vos campagnes et les ressources associées ;
* développer et gérer des sites communautaires ;
* déplacer, copier ou supprimer des pages de contenu, des ressources, etc. ;
* publier des pages, des ressources, etc. (ou annuler leur publication).

Certaines tâches administratives peuvent aussi vous aider à gérer votre contenu :

* workflow qui déterminent le mode de gestion des modifications ; par exemple, appliquer une révision avant une publication.
* projets qui coordonnent des tâches individuelles.

>[!NOTE]
>
>Pour la plupart des tâches, l’environnement de création permet également d’[administrer](/help/sites-administering/home.md) AEM.

#### Environnement de publication {#publish-environment}

Une fois prêt, le contenu du site AEM est publié dans l’**environnement de publication**. Ici, vos pages sont mises à la disposition de l’audience prévue, en fonction de l’aspect global de l’interface que vous avez conçue.

Dans le cas d’un site web ordinaire, l’environnement de publication est situé à l’intérieur de la zone DMZ ; en d’autres termes, il est disponible sur Internet, mais il ne bénéficie plus de la protection absolue de votre réseau interne.

Lorsque le site AEM est un [site communautaire](/help/communities/overview.md), ou inclut des [composants de Communities](/help/communities/author-communities.md), des utilisateurs (membres) connectés peuvent interagir avec les fonctions de Communities. Par exemple, ils peuvent interagir sur un forum, publier un commentaire ou suivre d’autres membres. Les membres peuvent être autorisés à effectuer des activités normalement réservées à l’environnement de création, telles que la création de nouvelles pages (groupes de communautés), d’articles de blog et la modération des publications d’autres membres.

>[!NOTE]
>
>Il existe malheureusement une interférence dans la terminologie utilisée. Cela peut se produire avec les fonctions suivantes :
>
>* **Publier/Annuler la publication**
>  Termes principalement utilisés pour évoquer les opérations qui rendent votre contenu publiquement accessible dans votre environnement de publication (ou non).
>
>* **Activer/Désactiver**
>  Ces termes sont synonymes de publication/annulation de la publication.
>
>* **Répliquer/Réplication**
>  Ces termes techniques décrivent le déplacement des données (par exemple de contenu de la page, de fichiers, de code, de commentaires de l’utilisateur) d’un environnement à un autre ; par ex., lors de la publication ou de la réplication inverse des commentaires d’utilisateur.
>


#### Dispatcher {#dispatcher}

Afin que les visiteurs de votre site Web bénéficient de performances optimales, le **[Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/user-guide.html)** met en œuvre des mécanismes de mise en cache et d’équilibrage de la charge.
