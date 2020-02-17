---
title: Abonnements aux communautés
seo-title: Abonnements aux communautés
description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique
seo-description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Abonnements aux communautés {#communities-subscriptions}

## Présentation {#overview}

À compter du [FP1](deploy-communities.md#latestfeaturepack)Collectivités, les membres de la communauté peuvent interagir avec la communauté par courriel à l’aide d’une fonction appelée abonnements.

Les abonnements sont similaires aux [notifications](notifications.md) , car les membres peuvent s’abonner lorsqu’ils suivent des articles de blog, des sujets de forum ou des questions sur la qualité de l’expérience.

Ce qui distingue les abonnements des notifications est :

* Les membres ne peuvent pas s&#39;abonner en suivant les autres membres
* La seule action que les membres doivent effectuer est de sélectionner `Email Subscriptions` lors de la
* Lorsque la réponse par courrier électronique est configurée, les membres peuvent effectivement publier du contenu en répondant simplement au courrier électronique reçu.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

Le courrier électronique doit être configuré pour que les abonnements soient fonctionnels et que les membres puissent répondre par courrier électronique.

Pour plus d’informations sur la configuration du courrier électronique, voir [Configuration du courrier électronique](email.md).

**Activer les abonnements et suivre**

Les composants doivent être configurés pour activer les abonnements *et les* suivants. Les fonctionnalités qui autorisent les abonnements sont [blog](blog-feature.md), [forum](forum.md) et [QnA](working-with-qna.md).

## Abonnements de la section suivante {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

Le bouton **Suivre** permet de suivre les entrées sous forme d’activités, d’abonnements et/ou de notifications. Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton devient **Suivant**. Pour des raisons pratiques, il est possible de choisir `Unfollow All` de désactiver toutes les méthodes.

Le bouton **Suivre** n’inclut l’ `Email Subscriptions` option que lorsqu’un forum, une évaluation quantitative ou un blog est configuré pour activer les abonnements au courrier électronique. Ce bouton apparaît.

* Sur la page principale de la fonctionnalité du forum activé, de la bibliothèque d’évaluation ou du blog

   * Envoie un courrier électronique pour toute activité sous cette fonctionnalité

* Pour une entrée spécifique, telle qu’un sujet de forum, une question sur la qualité de l’expérience ou un article de blog

   * Envoie un courrier électronique lorsqu&#39;il y a une activité pour cette entrée spécifique

## Réponse par courriel {#reply-by-email}

Lorsque le courrier électronique est [configuré pour répondre par courrier électronique](email.md#configure-polling-importer), le membre qui s’est abonné reçoit un courrier électronique contenant le contenu publié et un lien vers le contenu en ligne.

S’ils répondent à l’e-mail, le contenu qu’ils saisissent dans la réponse apparaîtra comme contenu en ligne.

![chlimage_1-6](assets/chlimage_1-6.png)

Le temps nécessaire à la publication d’une réponse est contrôlé par l’intervalle [de mise à jour de l’importateur d’](email.md#configure-polling-importer)interrogation.

![chlimage_1-7](assets/chlimage_1-7.png)

