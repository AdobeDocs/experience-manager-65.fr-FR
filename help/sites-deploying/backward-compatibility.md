---
title: Compatibilité ascendante dans AEM 6.5
seo-title: Backward Compatibility in AEM 6.5
description: Découvrez comment conserver la compatibilité de vos applications et configurations avec AEM 6.5
seo-description: Learn how to keep your apps and configurations compatible with AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
exl-id: c432a014-2dab-4c49-a25b-e4f461d13f9b
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 53%

---

# Compatibilité ascendante dans AEM 6.5{#backward-compatibility-in-aem}

## du commerce électronique {#overview}

>[!NOTE]
>
>Pour obtenir la liste des modifications de contenu et de configuration qui ne font pas partie du module de compatibilité, voir [Restructuration des référentiels dans AEM](/help/sites-deploying/repository-restructuring.md).

Dans AEM 6.5, toutes les fonctionnalités ont été développées dans une optique de compatibilité descendante.

Dans la majorité des cas, les utilisateurs qui exécutent AEM 6.3 ne doivent pas changer le code ni les personnalisations lorsqu’ils effectuent la mise à niveau. S’agissant d’AEM 6.1 et 6.2, aucune autre modification importante n’est à signaler lors d’une mise à niveau vers la version 6.3.

Dans les cas où la compatibilité descendante des fonctionnalités ne peut pas être conservée, il est possible de garantir la rétrocompatibilité des lots et du contenu en installant un package de compatibilité pour la version 6.4 (pour savoir où télécharger ce package, consultez la procédure de configuration ci-dessous). Dans la plupart des cas, ce package rétablit la compatibilité des applications compatibles avec AEM 6.4.

Le package de compatibilité vous permet d’exécuter AEM en mode de compatibilité et de différer le développement personnalisé par rapport aux nouvelles fonctionnalités d’AEM :

>[!NOTE]
>
>Notez que le package de compatibilité n’est qu’une solution temporaire visant à différer le développement requis pour garantir une compatibilité avec AEM 6.5. Il est recommandé de ne l’utiliser qu’en dernier ressort si vous ne parvenez pas à remédier aux problèmes de compatibilité par le biais du développement immédiatement après la mise à niveau. Il est vivement recommandé de passer en mode natif et de désinstaller le package de compatibilité une fois que vous avez décidé de procéder au développement personnalisé basé sur la version 6.5 et de bénéficier de toutes les fonctionnalités de la version 6.5.

![sase](assets/sase.png)

Le module de compatibilité possède deux modes : **Routage activé** et **Routage désactivé**.

AEM 6.5 peut ainsi être exécuté en trois modes :

**Mode natif :**

Le mode natif est destiné aux clients qui souhaitent utiliser toutes les nouvelles fonctionnalités d’AEM 6.5 et qui sont prêts à effectuer un certain développement pour que leurs personnalisations fonctionnent avec toutes les nouvelles fonctionnalités.

Cela signifie que vous devrez peut-être effectuer des ajustements dans votre application immédiatement après la mise à niveau.

**Mode de compatibilité : package de compatibilité installé avec le routage activé**

Le mode de compatibilité est destiné aux clients qui disposent de personnalisations d’interfaces non rétrocompatibles. Cela permet à AEM de s’exécuter en mode de compatibilité et de différer le développement personnalisé requis par rapport aux nouvelles fonctionnalités AEM qui ne sont pas compatibles avec certaines de vos données de code personnalisé.

**Mode hérité : module de compatibilité installé avec le mode Routage désactivé**

Le mode hérité est destiné aux clients disposant d’interfaces personnalisées basées sur du code hérité ou obsolète d’AEM qui a été déplacé dans le package de compatibilité.

![sapte](assets/sapte.png)

## Méthode de configuration {#how-to-set-up}

Le **module de compatibilité AEM 6.4 pour la version 6.5** peut être installé en tant que package à l’aide du gestionnaire de modules. Vous pouvez télécharger le [module de compatibilité AEM 6.4 pour la version 6.5 sur le site](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=compat*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=20&amp;package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fcompatpack%2Faem-compat-cq65-to-cq64) de la distribution logicielle.

Une fois le package de compatibilité installé, le routage peut être activé ou désactivé à l’aide d’un commutateur dans la configuration OSGI, comme indiqué ci-dessous :

![Sélecteurs de compatibilité](assets/compat-switches.png)

Une fois le package de compatibilité installé et configuré, les fonctionnalités sont utilisées sur la base du mode de compatibilité choisi.
