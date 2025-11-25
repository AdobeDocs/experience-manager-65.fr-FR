---
title: Création
description: Principes de création et de publication dans Adobe Experience Manager 6.5.
exl-id: dcda537a-1bb2-4ce3-9904-40d158b47556
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 100%

---

# Création{#authoring}

## Principe de création (et de publication) {#concept-of-authoring-and-publishing}

AEM vous met à disposition deux environnements :

* Création
* Publication

Ces environnements interagissent pour vous permettre de rendre le contenu disponible sur votre site Web, afin que vos visiteurs et visiteuses puissent y accéder.

L’environnement de création fournit les mécanismes de création, de mise à jour et de révision de ce contenu avant de le publier :

* Un auteur ou une autrice créent et révisent le contenu (qui peut être de plusieurs types, par exemple des pages, des ressources, des publications, etc.)
* qui, à un moment donné, sera publié sur votre site Web.

![Vue d’ensemble des environnements](assets/chlimage_1-132.png)

Dans l’environnement de création, les fonctions d’AEM sont accessibles dans deux interfaces utilisateur. Dans l’environnement de publication, vous concevez l’aspect de l’interface proposée aux utilisateurs et utilisatrices.

### Environnement de création {#author-environment}

L’auteur ou l’autrice travaille dans l’**environnement de création**. Cet environnement fournit une interface simple d’utilisation (interface utilisateur graphique ou interface utilisateur) pour la création de contenu.  Cette interface se trouve derrière le pare-feu d’une entreprise qui fournit une protection complète et implique que l’auteur ou l’autrice se connecte à l’aide d’un compte doté des droits d’accès appropriés.

>[!NOTE]
>
>Votre compte doit disposer des droits d’accès appropriés pour créer, modifier ou publier du contenu.

Selon la configuration de votre instance et de vos droits d’accès personnels, vous pouvez effectuer de nombreuses tâches sur votre contenu, notamment (entre autres) :

* la génération d’un nouveau contenu ou la modification du contenu existant sur une page ;
* utiliser les modèles prédéfinis pour créer des pages de contenu ;
* la création, modification et gestion de vos ressources et collections ;
* la création, modification et gestion de vos publications ;
* développer vos campagnes et les ressources associées ;
* développer et gérer des sites communautaires ;
* le déplacement, la copie ou la suppression des pages de contenu, des ressources, etc. ;
* la publication (ou annulation de la publication) de pages, de ressources, etc.

Certaines tâches administratives peuvent aussi vous aider à gérer votre contenu :

* des workflows qui déterminent le mode de gestion des modifications, par exemple, appliquer une révision avant une publication
* des projets qui coordonnent des tâches individuelles

>[!NOTE]
>
>AEM est également [administré](/help/sites-administering/home.md) (pour la plupart des tâches) à partir de l’environnement de création.

#### Environnement de publication {#publish-environment}

Une fois prêt, le contenu du site AEM est publié dans l’**environnement de publication**. Ici, vos pages sont mises à la disposition de l’audience prévue, en fonction de l’aspect global de l’interface que vous avez conçue.

En règle générale, l’environnement de publication est situé en « zone démilitarisée » : en d’autres termes, il est disponible sur internet, mais n’est plus protégé par le réseau interne.

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
>  Ces termes techniques décrivent le déplacement des données (par exemple de contenu de la page, de fichiers, de code, de commentaires de l’utilisateur ou de l’utilisatrice) d’un environnement à un autre, c’est-à-dire lors de la publication ou de la réplication inverse des commentaires d’utilisateurs ou d’utilisatrices.
>

#### Dispatcher {#dispatcher}

Afin que les visiteurs et visiteuses de votre site Web bénéficient de performances optimales, le **[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr)** implémente des mécanismes de mise en cache et d’équilibrage de la charge.
