---
title: Abonnements des communautés
description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 1%

---

# Abonnements des communautés {#communities-subscriptions}

## Vue d’ensemble {#overview}

À partir de Communities [FP1](deploy-communities.md#latestfeaturepack), les membres de la communauté peuvent interagir avec la communauté par e-mail à l’aide d’une fonctionnalité appelée abonnements.

Les abonnements sont similaires aux [notifications](notifications.md), car les membres peuvent s&#39;abonner lorsqu&#39;ils suivent des articles de blog, des sujets de forum ou des questions Q&amp;R.

Ce qui distingue les abonnements des notifications est :

* Les membres ne peuvent pas s’abonner lorsqu’ils suivent d’autres membres.
* La seule action que les membres peuvent effectuer est de sélectionner `Email Subscriptions` lorsque vous procédez comme suit.
* Lorsque la réponse par courrier électronique est configurée, les membres peuvent effectivement publier du contenu en répondant simplement à l’e-mail reçu.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

L&#39;email doit être paramétré pour que les abonnements soient fonctionnels et que les membres puissent répondre par email.

Pour obtenir des instructions sur la configuration de l’e-mail, voir [Configuration de l’e-mail](email.md).

**Activer les abonnements et suivre**

Les composants doivent être configurés pour activer les abonnements *et* suivants. Les fonctionnalités qui autorisent les abonnements sont les suivantes : [blog](blog-feature.md), [forum](forum.md) et [Q&amp;R](working-with-qna.md).

## Abonnements à partir de {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

Le bouton **Suivre** permet de suivre les entrées en tant qu’activités, abonnements et/ou notifications. Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection.

Si une méthode de suivi est sélectionnée, le texte du bouton devient **Suivant**. Pour des raisons pratiques, il est possible de sélectionner `Unfollow All` pour désactiver toutes les méthodes.

Le bouton **Suivre** inclura l’option `Email Subscriptions` uniquement lorsqu’un forum, une correspondance ou un blog est configuré pour activer les abonnements aux emails. Ce bouton apparaît :

* Sur la page principale du forum activé, Q&amp;R ou blog enverra un e-mail pour toutes les activités sous cette fonction.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question Q&amp;R ou un article de blog, enverra un email lorsqu’il y a une activité pour cette entrée spécifique.

## Répondre par email {#reply-by-email}

Lorsque le message électronique est [configuré pour répondre par courrier électronique](email.md#configure-polling-importer), le membre qui s’est abonné reçoit un message électronique avec le contenu publié et un lien vers le contenu en ligne.

S&#39;ils répondent à l&#39;email, le contenu qu&#39;ils saisissent dans la réponse apparaîtra sous forme de contenu en ligne.

![email-response](assets/email-reply.png)

Le temps nécessaire à la publication d’une réponse est contrôlé par l’ [intervalle de mise à jour de l’importateur d’interrogations](email.md#configure-polling-importer).

![QA](assets/qa.png)
