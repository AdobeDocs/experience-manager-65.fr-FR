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

À partir des communautés [FP1](deploy-communities.md#latestfeaturepack), les membres de la communauté peuvent interagir avec la communauté par courrier électronique à l’aide d’une fonctionnalité appelée abonnements.

Les abonnements sont similaires aux [notifications](notifications.md) Les membres peuvent s’abonner lorsqu’ils suivent des articles de blog, des sujets de forum ou des questions Q&amp;R.

Ce qui distingue les abonnements des notifications est :

* Les membres ne peuvent pas s’abonner lorsqu’ils suivent d’autres membres.
* La seule action que les membres peuvent effectuer est de sélectionner `Email Subscriptions` lorsque vous procédez comme suit.
* Lorsque la réponse par courrier électronique est configurée, les membres peuvent effectivement publier du contenu en répondant simplement à l’e-mail reçu.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

L&#39;email doit être paramétré pour que les abonnements soient fonctionnels et que les membres puissent répondre par email.

Pour obtenir des instructions sur la configuration du courrier électronique, voir [Configuration du courrier électronique](email.md).

**Activation des abonnements et suivez les**

Les composants doivent être configurés pour activer les abonnements. *et* suivant . Fonctionnalités qui autorisent les abonnements : [blog](blog-feature.md), [forum](forum.md) et [Q&amp;R](working-with-qna.md).

## Abonnements à partir de {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

La variable **Suivez** permet de suivre les entrées sous forme d’activités, d’abonnements et/ou de notifications. Chaque fois que la fonction **Suivez** est sélectionné, il est possible d’activer ou de désactiver une sélection.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton devient **Suivre**. Pour des raisons pratiques, il est possible de sélectionner `Unfollow All` pour désactiver toutes les méthodes.

La variable **Suivez** inclut le bouton `Email Subscriptions` n’est disponible que lorsqu’un forum, QnA ou blog est configuré pour activer les abonnements aux emails. Ce bouton apparaît :

* Sur la page principale du forum activé, Q&amp;R ou blog enverra un e-mail pour toutes les activités sous cette fonction.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question Q&amp;R ou un article de blog, enverra un email lorsqu’il y a une activité pour cette entrée spécifique.

## Répondre par email {#reply-by-email}

Lorsque le courrier électronique est [configuré pour répondre par email](email.md#configure-polling-importer), le membre qui s’est abonné recevra un email avec le contenu publié et un lien vers le contenu en ligne.

S&#39;ils répondent à l&#39;email, le contenu qu&#39;ils saisissent dans la réponse apparaîtra sous forme de contenu en ligne.

![email-response](assets/email-reply.png)

Le temps nécessaire à la publication d’une réponse est contrôlé par la variable [intervalle de mise à jour de l’importateur d’interrogations](email.md#configure-polling-importer).

![QA](assets/qa.png)
