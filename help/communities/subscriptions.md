---
title: Abonnements des communautés
seo-title: Abonnements des communautés
description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique.
seo-description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique.
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 2fcd87cd1def7fc265ba40c83b50db86618f3b70
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Abonnements des communautés {#communities-subscriptions}

## Présentation {#overview}

À compter de la section Collectivités [FP1](deploy-communities.md#latestfeaturepack), les membres de la communauté peuvent interagir avec la communauté par courriel à l’aide d’une fonction appelée abonnements.

Les Abonnements sont similaires aux [notifications](notifications.md) , car les membres peuvent s&#39;abonner lorsqu&#39;ils suivent des articles de blog, des sujets de forum ou des questions sur la qualité de l&#39;expérience.

Ce qui distingue les abonnements des notifications est :

* Les membres ne peuvent s&#39;abonner lorsqu&#39;ils suivent d&#39;autres membres.
* La seule action que les membres doivent entreprendre est de sélectionner `Email Subscriptions` quand ils suivent.
* Lorsque la réponse par courrier électronique est configurée, les membres peuvent effectivement publier du contenu en répondant simplement au courrier électronique reçu.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

Le courriel doit être configuré pour que les abonnements soient fonctionnels et que les membres puissent répondre par courriel.

Pour obtenir des instructions sur la configuration du courrier électronique, voir [Configuration du courrier électronique](email.md).

**Activer les Abonnements et suivre**

Les composants doivent être configurés pour activer les abonnements *et les* éléments suivants. Les fonctionnalités qui permettent aux abonnements sont [blog](blog-feature.md), [forum](forum.md) et [QnA](working-with-qna.md).

## Abonnements de suivi {#subscriptions-from-following}

![abonnement suivant](assets/subscription-following.png)

Le bouton **Suivre** permet de suivre les entrées comme activités, abonnements et/ou notifications. Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection.

Si une méthode de suivi est sélectionnée, le texte du bouton devient **Suivant**. Pour plus de commodité, il est possible de choisir `Unfollow All` de désactiver toutes les méthodes.

Le bouton **Suivre** inclut l&#39; `Email Subscriptions` option uniquement lorsqu&#39;un forum, une QnA ou un blog est configuré pour activer les abonnements de messagerie. Ce bouton apparaît :

* Sur la page principale de la fonctionnalité pour le forum activé, QnA, ou blog Envoie un courriel pour toute l&#39;activité sous cette fonction.

* Pour une entrée spécifique, telle qu&#39;un sujet de forum, une question QnA ou un article de blog Envoie un courriel lorsqu&#39;il y a activité pour cette entrée spécifique.

## Répondre par courriel {#reply-by-email}

Lorsque le courrier électronique est [configuré pour répondre par courrier électronique](email.md#configure-polling-importer), le membre qui s’est abonné reçoit un courrier électronique contenant le contenu publié et un lien vers le contenu en ligne.

S&#39;ils répondent à l&#39;e-mail, le contenu qu&#39;ils saisissent dans la réponse apparaîtra en ligne.

![email-response](assets/email-reply.png)

Le temps nécessaire à la publication d&#39;une réponse est contrôlé par l&#39;intervalle [de mise à jour de l&#39;importateur d&#39;](email.md#configure-polling-importer)interrogation.

![AQ](assets/qa.png)

