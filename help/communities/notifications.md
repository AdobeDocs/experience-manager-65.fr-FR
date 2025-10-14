---
title: Notifications de communautés
description: AEM Communities comporte des notifications qui affichent des événements présentant un intérêt pour le membre de la communauté connecté
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: cadb62c9-210d-4204-8abc-d0cf70960392
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 1%

---

# Notifications de communautés {#communities-notifications}

## Vue d’ensemble {#overview}

AEM Communities fournit une section de notifications qui affiche les événements d’intérêt pour les membres de la communauté connectés.

Les notifications sont similaires aux [activités](/help/communities/essentials-activities.md) et [abonnements](/help/communities/subscriptions.md), car elles peuvent provenir de :

* Le membre qui publie du contenu.
* Le membre qui choisit de suivre un autre membre.
* Le membre choisit de suivre des rubriques, des articles et d’autres threads de contenu spécifiques.
* Le balisage des membres (@mention) est un autre membre de la communauté dans un contenu généré par l’utilisateur.

Ce qui distingue les notifications des activités et des abonnements est :

* Un lien vers la section des notifications est toujours présent dans l’en-tête d’un site de la communauté :

   * Les activités nécessitent que la [fonction de flux d’activités](/help/communities/functions.md#activity-stream-function) soit incluse dans la structure du site de la communauté.
   * Les abonnements nécessitent la [configuration de l’email](/help/communities/email.md).

* La mise en oeuvre des notifications s’effectue par le biais de canaux évolutives et enfichables :

   * Les activités ne sont disponibles que sur le web.
   * Les abonnements ne sont disponibles que par email.

À partir de Communities [FP1](/help/communities/deploy-communities.md#latestfeaturepack), les canaux de notification disponibles sont les suivants :

* Le canal web, accessible à l’aide du lien `Notifications`.
* Canal email, disponible lorsque l’email est correctement configuré.

Les futurs canaux seront mobiles et de bureau.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

Pour que les notifications soient fonctionnelles, le canal Email doit être configuré.

Pour obtenir des instructions sur la configuration de l’e-mail, voir [Configuration de l’e-mail](/help/communities/analytics.md).

**Activer Suivre**

Les composants doivent être configurés pour activer les éléments suivants. Les fonctionnalités qui permettent ce qui suit sont [blog](/help/communities/blog-feature.md), [forum](/help/communities/forum.md), [Q&amp;R](/help/communities/working-with-qna.md), [calendar](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md) et [comments](/help/communities/comments.md).

**Remarque** :

* Les composants utilisés dans la communauté [modèles de site](/help/communities/sites.md) et [modèles de groupe](/help/communities/tools-groups.md) peuvent déjà être configurés pour être suivis.

* Les profils de membre sont déjà configurés pour permettre aux autres membres de suivre.

## Notifications de suivi {#notifications-from-following}

![notifications](assets/notifications.png)

Le bouton **[!UICONTROL Suivre]** permet de suivre les entrées en tant qu’activités, abonnements et/ou notifications. Chaque fois que le bouton **[!UICONTROL Suivre]** est sélectionné, il est possible d’activer ou de désactiver une sélection. La sélection `Email Subscriptions` n’est présente que lorsqu’elle est configurée.

Si une méthode de suivi est sélectionnée, le texte du bouton devient **[!UICONTROL Suivant]**. Pour des raisons pratiques, il est possible de sélectionner `Unfollow All` pour désactiver toutes les méthodes.

Le bouton **[!UICONTROL Suivre]** s’affiche :

* Lors de l’affichage du profil d’un autre membre.
* Sur une page principale, comme les forums, les Q&amp;R et les blogs :

   * Suit toutes les activités pour cette fonction générale.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question Q&amp;R ou un article de blog :

   * Suit toutes les activités pour cette entrée spécifique.

## Gestion des paramètres de notification {#managing-notification-settings}

En sélectionnant le lien Paramètres de notification sur la page Notifications, chaque membre peut gérer le mode de réception des notifications.

Le canal web est toujours activé.

![notifications14](assets/notifications1.png)

Le canal email, qui repose sur la [configuration correcte de l&#39;email](/help/communities/email.md), fournit les mêmes paramètres que pour le canal web.

Le canal email est désactivé par défaut.

![notifications2](assets/notifications2.png)

Il peut être activé par un membre, mais dépend toujours de la configuration de l&#39;email.

![notifications3](assets/notifications3.png)

## Affichage des notifications {#viewing-notifications}

### Notifications web {#web-notifications}

Un [site de communauté créé par l’assistant](/help/communities/sites-console.md) inclut désormais un lien vers la fonction `Notifications` dans la barre d’en-tête du site au-dessus de la bannière. Contrairement aux messages, les notifications sont créées pour chaque site de la communauté, tandis que les messages doivent être activés pendant le processus de création du site.

Lors de la visite du site publié, la sélection du lien `Notifications` affichera toutes les notifications pour le membre.

![notifications4](assets/notifications4.png)

### Notifications par e-mail {#email-notifications}

Lorsque le canal Email est activé, le membre reçoit un email contenant un lien vers le contenu sur le web.

![notifications5](assets/notifications5.png)

## Personnalisation des notifications par courrier électronique {#customize-email-notifications}

Les organisations peuvent personnaliser les notifications par courrier électronique en [&#x200B; superposant &#x200B;](/help/communities/client-customize.md#overlays) les modèles sur **/libs/settings/community/templates/email/html**.

Par exemple, pour modifier les notifications par courrier électronique de mentions (pour un composant Communities), ajoutez une condition **if** pour verb **mentions** dans les modèles des composants pour lesquels vous avez activé la prise en charge de **@mentions**.

Pour modifier le modèle de notifications électroniques pour @mention dans les commentaires de blog, placez le modèle prêt à l’emploi à l’adresse : **/libs/settings/community/templates/email/html/social.journal.components.hbs.comment/en**

```java
{{#equals this.verb "mention"}}\
    A new mention <a href="{{objectUrl}}">comment</a> {{#if this.target.properties.[jcr:title]}}to the article "{{{target.displayName}}}" {{/if}}was added by {{{user.name}}} on {{dateUtil this.published format="EEE, d MMM yyyy HH:mm:ss z"}}.\n \
{{/equals}}\
```
