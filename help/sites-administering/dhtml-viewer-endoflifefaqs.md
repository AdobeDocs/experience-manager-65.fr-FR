---
title: FAQ sur la fin de prise en charge de la visionneuse DHTML
seo-title: FAQ sur la fin de prise en charge de la visionneuse DHTML
description: À compter du 31 janvier 2014, la plate-forme de la visionneuse DHTML de Scene7 aura officiellement atteint sa fin de vie. Cette notification vous fournit les réponses aux questions fréquentes pour que vous puissiez vous préparer à cette transition vers la nouvelle plate-forme de notre visionneuse HTML5.
seo-description: À compter du 31 janvier 2014, la plate-forme de la visionneuse DHTML de Scene7 aura officiellement atteint sa fin de vie. Cette notification vous fournit les réponses aux questions fréquentes pour que vous puissiez vous préparer à cette transition vers la nouvelle plate-forme de notre visionneuse HTML5.
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: 283802809d665cd979e2f1a4fa969b6ddc491ed6
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 98%

---


# FAQ sur la fin de prise en charge de la visionneuse DHTML{#dhtml-viewer-end-of-life-faqs}

À compter du 31 janvier 2014, la plate-forme de la visionneuse DHTML de Scene7 aura officiellement atteint sa fin de vie. Cette notification vous fournit les réponses aux questions fréquentes pour que vous puissiez vous préparer à cette transition vers la nouvelle plate-forme de notre visionneuse HTML5.

**Quelle est la modification ?**

À compter du 31 janvier 2014, Scene7 mettra officiellement fin à la prise en charge de la plate-forme de la visionneuse DHTML.

**Que signifie fin de vie ?**

Fin de vie signifie que (1) Scene7 n’ajoutera plus d’améliorations aux fonctionnalités de la plate-forme de la visionneuse DHTML, (2) Scene7 ne traitera ou ne proposera plus de correctifs de bogues sur la plate-forme de la visionneuse DHTML et (3) l’assistance clientèle n’assurera plus la résolution des incidents ni la prise en charge des problèmes ou questions liés à la visionneuse DHTML.

**Pourquoi Scene7 apporte-t-il cette modification ?**

Les normes web évoluent constamment et DHTML est une ancienne technologie de développement web qui est rapidement remplacée par HTML5. La plus grande limitation de la norme DHTML en tant que plate-forme est qu’elle n’est pas capable de proposer une expérience aussi riche que le HTML5, qui peut désormais offrir cette qualité d’expérience de manière homogène et plus facilement d’un navigateur à l’autre. Par exemple, ces restrictions incluent l’absence de prise en charge d’un navigateur à l’autre pour :

* Les curseurs personnalisés
* Les angles arrondis
* Les animations (par exemple, tourner la page, effectuer un zoom)
* Les effets (par exemple, ombres, rayonnement)
* La prise en charge complète des polices
* La lecture vidéo sans module externe

Spécifiques à la plate-forme de la visionneuse DHTML Scene7, la solution basée sur JSP et les API JavaScript n’étaient pas optimisées pour que les appareils mobiles tirent parti des fonctionnalités tactiles multipoints et des fonctionnalités de mouvement. Et même si les visionneuses DHTML proposées à partir de 2011/début 2012 étaient optimisées pour les appareils mobiles, elles étaient difficiles à personnaliser et à tenir à jour en raison de l’absence d’un cadre de développement flexible basé sur le composant SDK.

Motivé par ces restrictions de DHTML et l’adoption rapide de HTML5 par le secteur en tant que norme émergente sur les ordinateurs de bureau et les appareils mobiles, Scene7 a décidé d’investir dans une plate-forme de visionneuse HTML5. Cet investissement apportera à nos clients une plate-forme robuste sur laquelle ils peuvent concevoir des visionneuses interactives plus riches et plus motivantes, capables de toucher les utilisateurs sur plusieurs écrans, y compris les ordinateurs de bureau et les appareils iOS et Android.

**Comment puis-je savoir si ma visionneuse utilise la plate-forme DHTML ?**

Pour déterminer si la visionneuse que votre entreprise utilise fait appel à la plate-forme DHTML et est donc concernée par cette modification, veuillez vérifier si :

1. Votre entreprise utilise une visionneuse Scene7 clé en main répertoriée dans ce tableau, où la « technologie de visionneuse » est nommée « DHTML » :

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Votre entreprise utilise une visionneuse qui a été créée sous la forme d’un nouveau paramètre prédéfini basé sur une visionneuse Scene7 clé en main dans ce tableau où la « technologie de visionneuse » est désignée comme « DHTML » :

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Votre entreprise utilise une visionneuse personnalisée créée à partir de la solution DHTML JSP :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. Votre entreprise utilise une visionneuse personnalisée créée à partir de l’API JavaScript :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. Votre entreprise utilise une visionneuse personnalisée créée avec l’API déroulante multi-écran DHTML :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. Votre entreprise utilise une visionneuse personnalisée créée avec l’API de fenêtre déroulante DHTML :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. Votre entreprise utilise une bibliothèque de détection d’appareil qui fait partie du module de visionneuses DHTML :

   Recherchez JS figurant dans « sj_deviceDetect.js » dans votre code.

   Cela a été remplacé par le nouveau code de détection d’appareil JS ici : [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers).

**Qu’est-ce que la plate-forme de visionneuse de remplacement ?**

Le remplacement de DHTML est la plate-forme de visionneuse HTML5 Scene7, comportant :

* Des visionneuses clé en main HTML5 comprenant des interactions optimisées mobiles sur de nombreux types de visionneuses, y compris le zoom de base, le zoom déroulant, les jeux d’images, les jeux d’échantillons, les visionneuses à 360° et les supports variés. Pour obtenir des exemples complets à jour de ces visionneuses, consultez la page : [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* Le SDK de la visionneuse HTML5 permet de personnaliser de façon étendue les visionneuses Adobe Scene7 pour les sites et les appareils pris en charge par HTML5 (iOS et Android, par exemple), pour une flexibilité et une créativité inégalées afin d’améliorer l’aspect et l’interactivité de la visionneuse. L’avantage de l’utilisation de composants réutilisables aux performances optimisées est la réduction du coût total du développement de la visionneuse et l’accélération du développement personnalisé.

**Quand la plate-forme de la visionneuse HTML5 disposera-t-elle des fonctions dont j’ai besoin pour faire la transition depuis la plate-forme de la visionneuse DHTML ?**

Scene7 a diffusé le premier SDK de visionneuse HTML5 à l’automne 2011 avec le lancement de la version 5.5. Depuis, nous avons ajouté de nombreuses fonctions à la plate-forme et étendu la prise en charge pour un nombre croissant de visionneuses. Pour ce qui est des exigences de visionneuse les plus courantes, la plate-forme de la visionneuse HTML5 dispose déjà probablement des fonctions dont vous avez besoin pour migrer maintenant. Et nous continuons à investir activement dans cette plate-forme de visionneuse avec la publication de nouvelles versions tous les trimestres.

Pour savoir si la plate-forme de la visionneuse HTML5 peut aujourd’hui répondre à vos besoins, consultez la documentation suivante :

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (pour les fonctionnalités de visionneuse clé en main et les capacités de personnalisation)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (pour accéder à la documentation de l’API de SDK)

Si vous ne savez toujours pas si le kit SDK de visionneuse HTML5 peut répondre à vos besoins, consultez notre équipe de services professionnels.

**Comment faire passer mes visionneuses vers la plate-forme HTML5 ?**

Pour faire passer vos visionneuses vers la plate-forme HTML5, Scene7 propose les options suivantes :

1. Utilisez l’une des visionneuses HTML5 clé en main Scene7, dont vous trouverez des exemples ici : [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Configurez l’une des visionneuses HTML5 clé en main Scene7 dans la configuration d’application SPS. Cela vous permettra de personnaliser un certain comportement, comme la taille de la visionneuse, les transitions, le comportement du zoom, etc. : [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Personnalisez l’apparence des visionneuses HTML5 clé en main Scene7 en modifiant les feuilles CSS afin de changer la conception visuelle, comme l’illustration des boutons, le placement, la transparence, les couleurs d’arrière-plan, etc. : [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Créez une visionneuse HTML5 personnalisée de A à Z à l’aide du kit SDK, que vous pouvez télécharger ici : [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Vous pouvez faire appel à des services professionnels pour créer la visionneuse personnalisée ou en confier la création à votre propre équipe de développement web.

**Qu’en est-il des navigateurs qui ne prennent pas en charge HTML5 ?**

HTML5 est pris en charge sur de nombreux appareils mobiles et navigateurs web et continue à gagner du terrain. Actuellement, même si HTML5 n’est pas pris en charge dans Internet Explorer 8 ou ses versions antérieures, Scene7 a mis à jour la plate-forme de visionneuse HTML5 pour étendre la prise en charge à IE 7 et IE 8. Avec la plate-forme de visionneuse HTML5 Scene7, vous pouvez toucher l’écrasante majorité des utilisateurs d’ordinateurs et d’appareils mobiles avec une seule plate-forme de développement.

La configuration système requise actuelle à partir de la version 2.2.1 du kit SDK HTML5 est la suivante :

* Microsoft® Windows® XP ou version ultérieure, Macintosh® OS X 10.6 ou version ultérieure
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 ou version ultérieure
* iOS 3.2.2 ou version ultérieure
* Certifié sur iPhone3 ou version ultérieure et iPad1 ou version ultérieure (navigateurs natifs)
* Android OS 2.2 ou version ultérieure

Pour vérifier si votre navigateur est compatible avec notre plate-forme de visionneuse HTML5, lancez l’exemple de visionneuse suivante :

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Si vous voyez l’image agrandie en pointant avec votre souris ou en faisant glisser votre doigt sur l’image principale, il s’agit d’un navigateur ou appareil pris en charge.

**Quelles sont les options qui s’offrent à moi si je souhaite continuer à utiliser ma visionneuse DHTML existante en production ?**

Bien que vous puissiez encore rester en production avec les visionneuses DHTML, il est important de noter qu’il n’y aura pas d’améliorations, de correctifs, ni d’assistance client après le 31 janvier 2014. Par conséquent, nous recommandons fortement à tous les clients de migrer vers notre plate-forme de visionneuse HTML5, qui s’avère plus robuste. Toutefois, si la situation de votre entreprise empêche cette migration d’ici la fin de la commercialisation, vous avez la possibilité de souscrire à des services professionnels pour prolonger la période de maintenance prise en charge. Pour plus d’informations, contactez votre responsable de compte.

**Qui dois-je contacter pour plus d’informations ?**

Si ce FAQ n&#39;a pas répondu à toutes vos questions, veuillez [utiliser le Admin Console pour créer un dossier](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) d&#39;assistance ou contactez votre gestionnaire de compte d&#39;Adobe.
