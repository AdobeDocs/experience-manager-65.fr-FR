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
role: Administrator
exl-id: 338be220-659a-459c-8e90-55e3a11ddeb0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 2%

---

# Abonnements des communautés {#communities-subscriptions}

## Présentation {#overview}

À partir de Communities [FP1](deploy-communities.md#latestfeaturepack), les membres de la communauté peuvent interagir avec la communauté par courrier électronique à l’aide d’une fonctionnalité appelée abonnements.

Les abonnements sont similaires aux [notifications](notifications.md), car les membres peuvent s’abonner lorsqu’ils suivent des articles de blog, des sujets de forum ou des questions Q&amp;R.

Ce qui distingue les abonnements des notifications est :

* Les membres ne peuvent pas s’abonner lorsqu’ils suivent d’autres membres.
* La seule action que les membres peuvent effectuer est de sélectionner `Email Subscriptions` en suivant la liste.
* Lorsque la réponse par courrier électronique est configurée, les membres peuvent effectivement publier du contenu en répondant simplement à l’e-mail reçu.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

L&#39;email doit être paramétré pour que les abonnements soient fonctionnels et que les membres puissent répondre par email.

Pour plus d’informations sur la configuration de l’e-mail, voir [Configuration de l’e-mail](email.md).

**Activation des abonnements et suivez**

Les composants doivent être configurés pour activer les abonnements *et* suivants. Les fonctionnalités qui autorisent les abonnements sont [blog](blog-feature.md), [forum](forum.md) et [QnA](working-with-qna.md).

## Abonnements à partir de la balise {#subscriptions-from-following}

![subscription-following](assets/subscription-following.png)

Le bouton **Suivre** permet de suivre les entrées en tant qu’activités, abonnements et/ou notifications. Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton passe à **Suivant**. Pour des raisons pratiques, il est possible de sélectionner `Unfollow All` pour désactiver toutes les méthodes.

Le bouton **Suivre** comprend l’option `Email Subscriptions` uniquement lorsqu’un forum, une correspondance ou un blog est configuré pour activer les abonnements aux emails. Ce bouton apparaît :

* Sur la page principale du forum activé, Q&amp;R ou blog enverra un e-mail pour toutes les activités sous cette fonction.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question Q&amp;R ou un article de blog, enverra un email lorsqu’il y a une activité pour cette entrée spécifique.

## Réponse par courriel {#reply-by-email}

Lorsque l’adresse électronique est [configurée pour répondre par adresse électronique](email.md#configure-polling-importer), le membre qui s’est abonné recevra un courrier électronique contenant le contenu publié et un lien vers le contenu en ligne.

S&#39;ils répondent à l&#39;email, le contenu qu&#39;ils saisissent dans la réponse apparaîtra en ligne.

![email-response](assets/email-reply.png)

Le temps nécessaire à la publication d’une réponse est contrôlé par l’[intervalle de mise à jour de l’importateur d’interrogations](email.md#configure-polling-importer).

![AQ](assets/qa.png)
