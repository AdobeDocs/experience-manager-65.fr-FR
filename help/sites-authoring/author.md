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
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 78%

---

# Création  {#authoring}

## Concept de création (et de publication) {#concept-of-authoring-and-publishing}

AEM fournit deux environnements :

* Création
* Publication

Ces fonctions interagissent pour vous permettre de rendre le contenu disponible sur votre site web, de sorte que vos visiteurs puissent le lire.

L’environnement de création fournit les mécanismes de création, de mise à jour et de révision de ce contenu avant de le publier :

* Un auteur crée et révise le contenu (qui peut être de plusieurs types, par exemple des pages, des ressources, des publications, etc.)
* qui, à un moment donné, sera publié sur votre site Web.

![Présentation des environnements](assets/chlimage_1-132.png)

Dans l’environnement de création, les fonctions d’AEM sont accessibles dans deux interfaces utilisateur. Dans l’environnement de publication, vous concevez l’aspect de l’interface proposée aux utilisateurs.

### Environnement de création {#author-environment}

L’auteur travaille dans ce qu’on appelle l’**environnement de création**. Il s’agit d’une interface facile à utiliser (interface utilisateur graphique) pour créer le contenu. En fait, cette interface se trouve habituellement derrière le pare-feu d’une entreprise qui fournit une protection complète et implique que l’auteur se connecte à l’aide d’un compte doté des droits d’accès appropriés.

>[!NOTE]
>
>Votre compte doit disposer des droits d’accès appropriés pour créer, modifier ou publier du contenu.

Selon la configuration de votre instance et de vos droits d’accès personnels, vous pouvez effectuer de nombreuses tâches sur votre contenu, notamment (entre autres) :

* générer du nouveau contenu ou modifier du contenu existant sur une page ;
* utiliser les modèles prédéfinis pour créer des pages de contenu ;
* créer, modifier et gérer vos ressources et collections ;
* créer, modifier et gérer vos publications ;
* développer vos campagnes et les ressources associées ;
* développer et gérer des sites communautaires ;
* déplacer, copier ou supprimer des pages de contenu, des ressources, etc. ;
* publier (ou annuler la publication) des pages, des ressources, etc.

Certaines tâches administratives peuvent aussi vous aider à gérer votre contenu :

* workflow qui déterminent le mode de gestion des modifications ; par exemple, application d’une révision avant publication
* projets qui coordonnent des tâches individuelles

>[!NOTE]
>
>AEM est également [administré](/help/sites-administering/home.md) (pour la plupart des tâches) à partir de l’environnement de création.

#### Environnement de publication {#publish-environment}

Une fois prêt, le contenu du site AEM est publié dans l’**environnement de publication**. Ici, vos pages sont mises à la disposition de l’audience prévue, en fonction de l’aspect global de l’interface que vous avez conçue.

En règle générale, l’environnement de publication se trouve à l’intérieur de la zone démilitarisée ; en d&#39;autres termes, disponible sur l&#39;internet, mais plus sous la pleine protection du réseau interne.

Lorsque le site AEM est un [site communautaire](/help/communities/overview.md), ou inclut des [composants de Communities](/help/communities/author-communities.md), des utilisateurs (membres) connectés peuvent interagir avec les fonctions de Communities. Par exemple, ils peuvent interagir sur un forum, publier un commentaire ou suivre d’autres membres. Les membres peuvent être autorisés à effectuer des activités normalement réservées à l’environnement de création, telles que la création de nouvelles pages (groupes de communautés), d’articles de blog et la modération des publications d’autres membres.

>[!NOTE]
>
>Il existe malheureusement une interférence dans la terminologie utilisée. Cela peut se produire avec les fonctions suivantes :
>
>* **Publier/dépublier**
>  Termes principalement utilisés pour évoquer les opérations qui rendent votre contenu publiquement accessible dans votre environnement de publication (ou non).
>
>* **Activer/Désactiver**
>  Ces termes sont synonymes de publication/dépublication.
>
>* **Répliquer/Réplication**
>  Ces termes techniques décrivent le déplacement des données (par exemple de contenu de la page, de fichiers, de code, de commentaires de l’utilisateur) d’un environnement à un autre ; par ex., lors de la publication ou de la réplication inverse des commentaires d’utilisateur.
>

#### Dispatcher {#dispatcher}

Afin que les visiteurs de votre site Web bénéficient de performances optimales, le **[Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/user-guide.html)** met en œuvre des mécanismes de mise en cache et d’équilibrage de la charge.
