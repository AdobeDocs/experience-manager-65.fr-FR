---
title: FAQ sur la fin de vie de la visionneuse DHTML
seo-title: FAQ sur la fin de vie de la visionneuse DHTML
description: À compter du 31 janvier 2014, la plateforme de la visionneuse DHTML de Scene7 aura officiellement atteint sa fin de vie. Cette notification vous fournit les réponses aux questions fréquentes pour que vous puissiez vous préparer à cette transition vers la nouvelle plateforme de notre visionneuse HTML5.
seo-description: À compter du 31 janvier 2014, la plateforme de la visionneuse DHTML de Scene7 aura officiellement atteint sa fin de vie. Cette notification vous fournit les réponses aux questions fréquentes pour que vous puissiez vous préparer à cette transition vers la nouvelle plateforme de notre visionneuse HTML5.
uuid: a78c03b3-6513-42e1-881f-6a9551659769
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: d94244ac-a5f6-4c95-ab8c-26b41d25863f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# FAQ sur la fin de vie de la visionneuse DHTML{#dhtml-viewer-end-of-life-faqs}

À compter du 31 janvier 2014, la plateforme de la visionneuse DHTML de Scene7 aura officiellement atteint sa fin de vie. Cette notification vous fournit les réponses aux questions fréquentes pour que vous puissiez vous préparer à cette transition vers la nouvelle plateforme de notre visionneuse HTML5.

**Quelle est la modification ?**

À compter du 31 janvier 2014, Scene7 mettra officiellement fin à la prise en charge de la plateforme de la visionneuse DHTML.

**Que signifie la fin de vie ?**

Fin de vie signifie que (1) Scene7 n’ajoutera plus d’améliorations aux fonctionnalités de la plateforme de la visionneuse DHTML, (2) Scene7 ne traitera ou ne proposera plus de correctifs de bogues sur la plateforme de la visionneuse DHTML et (3) l’assistance clientèle n’assurera plus la résolution des incidents ni la prise en charge des problèmes ou questions liés à la visionneuse DHTML.

**Pourquoi Scene7 apporte-t-il cette modification ?**

Les normes web évoluent constamment et DHTML est une ancienne technologie de développement web qui est rapidement remplacée par HTML5. La plus grande limite à DHTML en tant que plate-forme est qu’il n’est pas capable de créer la richesse de l’expérience que HTML5 peut désormais prendre en charge de manière cohérente et plus facile entre navigateurs. Par exemple, ces restrictions incluent l’absence de prise en charge d’un navigateur à l’autre pour :

* Les curseurs personnalisés
* Les angles arrondis
* Les animations (par exemple, tourner la page, effectuer un zoom)
* Les effets (par exemple, ombres, rayonnement)
* La prise en charge complète des polices
* La lecture vidéo sans module externe

Spécifiques à la plateforme de la visionneuse DHTML Scene7, la solution basée sur JSP et les API JavaScript n’étaient pas optimisées pour que les appareils mobiles tirent parti des fonctionnalités tactiles multipoints et des fonctionnalités de mouvement. Et même si les visionneuses DHTML proposées à partir de 2011/début 2012 étaient optimisées pour les appareils mobiles, elles étaient difficiles à personnaliser et à tenir à jour en raison de l’absence d’un cadre de développement flexible basé sur le composant SDK.

En raison de ces restrictions sur le langage DHTML et de l’évolution rapide du secteur grâce à HTML5 comme nouvelle norme sur les ordinateurs de bureau et les appareils mobiles, Scene7 a décidé d’investir dans une plate-forme de visionneuse HTML5. Cet investissement apportera à nos clients une plateforme robuste sur laquelle ils peuvent concevoir des visionneuses interactives plus riches et plus motivantes capables de toucher les utilisateurs sur de multiples écrans, y compris les ordinateurs de bureau et les appareils iOS et Android.

**Comment puis-je savoir si ma visionneuse utilise la plateforme DHTML ?**

Pour déterminer si la visionneuse que votre entreprise utilise fait appel à la plateforme DHTML et est donc concernée par cette modification, veuillez vérifier si :

1. Votre entreprise utilise une visionneuse Scene7 prête à l’emploi répertoriée dans ce tableau, où la &quot;technologie de la visionneuse&quot; est désignée comme &quot;DHTML&quot; :

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Votre entreprise utilise une visionneuse qui a été créée en tant que nouveau paramètre prédéfini à partir d’une visionneuse Scene7 prête à l’emploi dans le tableau suivant, où la &quot;technologie de la visionneuse&quot; est désignée comme &quot;DHTML&quot; :

   [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html#WS1c46793299cf21d77e926d1613177f0a020-8000)

1. Votre entreprise utilise un lecteur personnalisé créé à partir de la solution DHTML basée sur JSP :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#JSP_Reference)

1. Votre entreprise utilise un lecteur de contenu personnalisé créé à partir de l’API Javascript :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#API_Reference)

1. Votre entreprise utilise un lecteur de contenu personnalisé créé avec l’API de fenêtre déroulante multi-écran DHTML :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Multi-screen_Flyout_Viewer)

1. Votre entreprise utilise un lecteur de contenu personnalisé créé avec l’API de fenêtre déroulante de bureau DHTML :

   [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Desktop_Flyout_Viewer)

1. Votre entreprise utilise une bibliothèque de détection de périphériques qui fait partie du package des visionneuses DHTML :

   Recherchez JS figurant dans « sj_deviceDetect.js » dans votre code.

   This has been replaced by new JS device detection code here: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Detecting_devices_and_browsers) .

**Qu’est-ce que la plateforme de visionneuse de remplacement ?**

Le remplacement de DHTML est la plateforme de visionneuse HTML5 Scene7, comportant :

* Des visionneuses clé en main HTML5 comprenant des interactions optimisées mobiles sur de nombreux types de visionneuses, y compris le zoom de base, le zoom déroulant, les jeux d’images, les jeux de nuanciers, les visionneuses à 360° et les supports variés. For full up-to-date examples of these viewers, please refer to: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
* Le SDK de la visionneuse HTML5 autorise une personnalisation étendue des visionneuses Adobe Scene7 pour les sites et les appareils pris en charge par HTML5 (par exemple, iOS et Android), ce qui garantit une flexibilité et une créativité inégalées pour améliorer l’aspect et l’interactivité de la visionneuse. L’avantage de l’utilisation de composants aux performances optimisées réutilisables est la réduction du coût total du développement de la visionneuse et l’accélération du développement personnalisé.

**Quand la plateforme de la visionneuse HTML5 disposera-t-elle des fonctions dont j’ai besoin pour faire la transition depuis la plateforme de la visionneuse DHTML ?**

Scene7 a diffusé le premier SDK de visionneuse HTML5 à l’automne 2011 avec le lancement de la version 5.5. Depuis, nous avons ajouté de nombreuses fonctions à la plateforme et étendu la prise en charge pour un nombre croissant de visionneuses. Pour la plupart des besoins de la visionneuse, il est probable que la plate-forme de la visionneuse HTML5 dispose déjà des fonctionnalités dont vous avez besoin pour migrer maintenant. Et nous continuons à investir activement dans cette plateforme de visionneuse avec des versions chaque trimestre.

Pour déterminer si la plateforme de la visionneuse HTML5 peut aujourd’hui répondre à vos besoins, voir la documentation suivante :

[https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#About_HTML5_Viewers) (pour les fonctionnalités de visionneuses prêtes à l’emploi et les fonctionnalités de personnalisation)

[https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html) (pour accéder à la documentation de l’API SDK)

Si vous ne savez toujours pas si le kit SDK de visionneuse HTML5 peut répondre à vos besoins, consultez notre équipe de services professionnels.

**Comment faire passer mes visionneuses vers la plateforme HTML5 ?**

Pour faire passer vos visionneuses vers la plateforme HTML5, Scene7 propose les options suivantes :

1. Use one of the Scene7 out-of-box HTML5 viewers, examples of which can be found here: [https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html](https://microsite.omniture.com/t2/help/en_US/s7/vlist/vlist.html)
1. Configurez l’une des visionneuses HTML5 prêtes à l’emploi Scene7 sous la configuration de l’application SPS. This will allow you to customize certain behavior such as viewer size, transitions, zoom behavior, etc: [https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html](https://help.adobe.com/en_US/scene7/using/WS6E593DEA-7D81-4cd6-84B0-85E8BB274176.html)
1. Customize look and feel of the Scene7 out-of-box HTML5 viewers by modifying CSS to change visual design such as button artwork, placement, transparency, background colors, etc: [https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers](https://microsite.omniture.com/t2/help/en_US/s7/viewers_ref/index.html#Customizing_HTML5_Viewers)
1. Create a custom HTML5 viewer from scratch using the SDK which can be downloaded here: [https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html](https://help.adobe.com/en_US/scene7/using/WSd4272150f67705c11b002eec12fcba4dee6-8000.html). Vous pouvez contacter des services professionnels pour créer le lecteur personnalisé ou demander à votre propre équipe de développement Web de le créer.

**Qu’en est-il des navigateurs qui ne prennent pas en charge HTML5 ?**

HTML5 est pris en charge sur de nombreux appareils mobiles et navigateurs web et continue à gagner du terrain. Actuellement, même si HTML5 n’est pas pris en charge par Internet Explorer 8 ou version ultérieure, Scene7 a innové dans sa plate-forme de visionneuse HTML5 pour étendre la prise en charge même à IE 7 et IE 8. Avec la plate-forme de la visionneuse HTML5 Scene7, vous pouvez atteindre l’écrasante majorité des utilisateurs de bureau et de mobile avec une seule plate-forme de développement.

La configuration système requise actuelle à partir de la version 2.2.1 du kit SDK HTML5 est la suivante :

* Microsoft® Windows® XP ou version ultérieure, Macintosh® OS X 10.6 ou version ultérieure
* Firefox 17, Safari 5.1, Chrome 23, Internet Explorer 7 ou version ultérieure
* iOS 3.2.2 ou version ultérieure
* Certifié sur iPhone3 ou version ultérieure et iPad1 ou version ultérieure (navigateurs natifs)
* Android OS 2.2 ou version ultérieure

Pour vérifier si votre navigateur est compatible avec notre plate-forme de visionneuse HTML5, lancez l’exemple de visionneuse suivant :

[https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image](https://s7d1.scene7.com/s7viewers/html5/flyout.html?asset=Scene7SharedAssets/Sample%20Image)

Si vous voyez l’image agrandie en pointant avec votre souris ou en faisant glisser votre doigt sur l’image principale, il s’agit d’un navigateur ou appareil pris en charge.

**Quelles sont les options qui s’offrent à moi si je souhaite continuer à utiliser ma visionneuse DHTML existante en production ?**

Bien que vous puissiez continuer à travailler en production avec des lecteurs DHTML, il est important de noter qu’il n’y aura aucune amélioration, aucun correctif de bogues ni aucun service à la clientèle après le 31 janvier 2014. Par conséquent, nous recommandons fortement à tous les clients de migrer vers notre plateforme de visionneuse HTML5, plus robuste. . Toutefois, si la situation de votre entreprise empêche cette migration d’ici la fin de la commercialisation, vous avez la possibilité de souscrire à des services professionnels pour prolonger la période de maintenance prise en charge. Pour plus d’informations, contactez votre responsable de compte.

**Qui dois-je contacter pour plus d’informations ?**

Si cette FAQ n’a pas répondu à toutes vos questions, veuillez contacter le support ([s7support@adobe.com](mailto:s7support@adobe.com)) ou votre responsable de compte Adobe.
