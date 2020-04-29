---
title: 'Communautés '
seo-title: 'Communautés '
description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique
seo-description: Les membres de la communauté interagissent avec d’autres membres par courrier électronique
uuid: a4b98769-c219-4e18-8e80-9a806ab979ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 33c85af4-4c56-487a-ba60-55211cb9f72c
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Communautés {#communities-subscriptions}

## Présentation {#overview}

Depuis le [FP1](deploy-communities.md#latestfeaturepack)des communautés, les membres de la communauté peuvent interagir avec la communauté par courriel à l’aide d’une fonction appelée  .

  sont similaires aux [notifications](notifications.md) , car les membres peuvent s&#39;abonner à des articles de blog, des sujets de forum ou des questions sur la qualité de vie.

Ce qui distingue   des notifications est :

* Les membres ne peuvent s&#39;abonner lorsqu&#39;ils suivent les autres membres.
* La seule action que les membres doivent effectuer est de sélectionner `Email Subscriptions` quand ils suivent.
* Lorsque la réponse par courrier électronique est configurée, les membres peuvent effectivement publier du contenu en répondant simplement au courrier électronique reçu.

### Conditions requises {#requirements}

**Configurer le courrier électronique**

Le courrier électronique doit être configuré pour que   être fonctionnel et que les membres puissent répondre par courrier électronique.

Pour plus d’informations sur la configuration du courrier électronique, voir [Configuration du courrier électronique](email.md).

**Activer   et suivre**

Les composants doivent être configurés afin d’activer   *et les* éléments suivants. Les fonctionnalités qui permettent   sont [blog](blog-feature.md), [forum](forum.md) et [QnA](working-with-qna.md).

##  de  de suivi {#subscriptions-from-following}

![chlimage_1-5](assets/chlimage_1-5.png)

Le bouton **Suivre** permet de suivre les entrées sous forme de  , de  et/ou de notifications. Chaque fois que le bouton **Suivre** est sélectionné, il est possible d’activer ou de désactiver une sélection.

Si l’une des méthodes suivantes est sélectionnée, le texte du bouton devient **Suivant**. Pour des raisons pratiques, il est possible de choisir `Unfollow All` de désactiver toutes les méthodes.

Le bouton **Suivre** inclut l’ `Email Subscriptions` option uniquement lorsqu’un forum, une évaluation qualité de service ou un blog est configuré pour activer l’ de  par courrier électronique. Ce bouton apparaît :

* Sur la page principale des fonctionnalités du forum activé, QnA ou blog enverra un courrier électronique à tous les   sous cette fonctionnalité.

* Pour une entrée spécifique, telle qu’un sujet de forum, une question sur la qualité de l’expérience ou un article de blog, enverra un courriel lorsqu’il y a   pour cette entrée spécifique.

## Réponse par courriel {#reply-by-email}

Lorsque le courrier électronique est [configuré pour répondre par courrier électronique](email.md#configure-polling-importer), le membre qui s’est abonné reçoit un courrier électronique contenant le contenu publié et un lien vers le contenu en ligne.

S’ils répondent à l’e-mail, le contenu qu’ils saisissent dans la réponse apparaîtra comme contenu en ligne.

![chlimage_1-6](assets/chlimage_1-6.png)

Le temps nécessaire à la publication d’une réponse est contrôlé par l’intervalle [de mise à jour de l’importateur d’](email.md#configure-polling-importer)interrogation.

![chlimage_1-7](assets/chlimage_1-7.png)

