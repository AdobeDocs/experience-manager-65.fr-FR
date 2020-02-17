---
title: Notifications de communautés
seo-title: Notifications de communautés
description: Les communautés AEM disposent de notifications qui affichent des événements présentant un intérêt pour le membre de la communauté connecté
seo-description: Les communautés AEM disposent de notifications qui affichent des événements présentant un intérêt pour le membre de la communauté connecté
uuid: 2f5ea4b5-7308-414e-a3f8-2e8aa76b1ef4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: ab9088b7-a691-4153-ac82-1e8c0a19ed5d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Notifications de communautés{#communities-notifications}

## Présentation {#overview}

Les communautés AEM fournissent une section de notifications qui affiche les événements présentant un intérêt pour le membre de la communauté connecté.

Les notifications sont similaires aux [activités](/help/communities/essentials-activities.md) et aux [abonnements](/help/communities/subscriptions.md) , qui peuvent provenir de

* le membre qui publie du contenu
* le membre qui choisit de suivre un autre membre
* le membre choisissant de suivre des rubriques, des articles et d&#39;autres fils de contenu spécifiques
* le balisage du membre (@mentions) un autre membre de la communauté dans un contenu généré par un utilisateur

Ce qui distingue les notifications des activités et des abonnements est

* un lien vers la section des notifications est toujours présent dans l’en-tête d’un site communautaire.

   * les activités exigent que la fonction [de flux d&#39;](/help/communities/functions.md#activity-stream-function) activité soit incluse dans la structure du site communautaire
   * les abonnements nécessitent [la configuration du courrier électronique](/help/communities/email.md)

* la mise en oeuvre des notifications s’effectue via des canaux extensibles et enfichables

   * les activités sont disponibles uniquement sur le Web.
   * abonnements disponibles uniquement par courrier électronique

À compter du [FP1](/help/communities/deploy-communities.md#latestfeaturepack)des Communautés, les canaux de notification disponibles sont

* le canal Web, accessible à l’aide du `Notifications` lien
* canal de courrier électronique, disponible lorsque le courrier électronique est correctement configuré

Les canaux futurs sont mobiles et de bureau.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

Le courrier électronique doit être configuré pour que le canal de courrier électronique fonctionne pour que les notifications.

Pour plus d’informations sur la configuration du courrier électronique, voir [Configuration du courrier électronique](/help/communities/analytics.md).

**Activer le suivi**

Les composants doivent être configurés pour activer les éléments suivants. Les fonctionnalités qui permettent ce qui suit sont [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendar, filelibrary etcommentaires.](/help/communities/calendar.md)[](/help/communities/file-library.md)[](/help/communities/comments.md)

Notez que

* les composants utilisés dans les modèles [de](/help/communities/sites.md) site de la communauté et les modèles [de](/help/communities/tools-groups.md) groupe peuvent déjà être configurés pour autoriser les éléments suivants :

* les profils de membres sont déjà configurés pour permettre aux autres membres de suivre

## Notifications de suivi {#notifications-from-following}

![chlimage_1-243](assets/chlimage_1-243.png)

Le **Suivre **bouton permet de suivre les entrées comme activités, abonnements et/ou notifications. Chaque fois que le **Suivre **bouton est sélectionné, il est possible d&#39;activer ou de désactiver une sélection. La `Email Subscriptions` sélection n’est présente que lorsqu’elle est configurée.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton devient **Suivant**. Pour des raisons pratiques, il est possible de choisir `Unfollow All` de désactiver toutes les méthodes.

Le **Suivre **bouton apparaîtra.

* lors de l’affichage du profil d’un autre membre
* sur une page de présentation principale, telle que les forums, la qualité de vie et les blogs

   * suit toute l’activité de cette fonctionnalité générale

* pour une entrée spécifique, telle qu’un sujet de forum, une question QnA ou un article de blog

   * suit toute activité pour cette entrée spécifique

## Gestion des paramètres de notification {#managing-notification-settings}

En sélectionnant le lien Paramètres de notification dans la page Notifications, chaque membre peut gérer le mode de réception des notifications.

Le canal Web est toujours activé.

![chlimage_1-244](assets/chlimage_1-244.png)

Le canal de courrier électronique, qui repose sur une [configuration appropriée du courrier électronique](/help/communities/email.md), fournit les mêmes paramètres que pour le canal Web.

Le canal de messagerie est désactivé par défaut.

![chlimage_1-245](assets/chlimage_1-245.png)

Il peut être activé par un membre, mais dépend toujours de la configuration du courrier électronique.

![chlimage_1-246](assets/chlimage_1-246.png)

## Affichage des notifications {#viewing-notifications}

### Notifications Web {#web-notifications}

Un [assistant a créé un site](/help/communities/sites-console.md) communautaire et inclut désormais un lien vers la `Notifications` fonction dans la barre d’en-tête du site au-dessus de la bannière. Contrairement aux messages, les notifications sont créées pour chaque site de la communauté, tandis que les messages doivent être activés pendant le processus de création du site.

Lors de la visite du site publié, la sélection du `Notifications` lien affichera toutes les notifications du membre.

![chlimage_1-247](assets/chlimage_1-247.png)

### Notifications par e-mail {#email-notifications}

Lorsque le canal de courrier électronique est activé, le membre reçoit un courrier électronique contenant un lien vers le contenu sur le Web.

![chlimage_1-248](assets/chlimage_1-248.png)

## Personnalisation des notifications par courrier électronique {#customize-email-notifications}

Les entreprises peuvent personnaliser les notifications par courrier électronique en [superposant](/help/communities/client-customize.md#overlays) les modèles dans **/libs/settings/community/templates/email/html**.

Par exemple, pour modifier les notifications par courrier électronique de mentions (pour un composant de communautés), ajoutez une condition ** if **pour la **mention de verbe** dans les modèles des composants pour lesquels vous avez activé la prise en charge des **@mentions** .

Pour modifier le modèle de notifications par courrier électronique pour @mentions dans les commentaires de blog, placez le modèle prêt à l’emploi à l’adresse suivante : **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/fr**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```

