---
title: Compatibilité descendante dans AEM 6.5
seo-title: Compatibilité descendante dans AEM 6.5
description: Découvrez comment faire en sorte que vos applications et configurations restent compatibles avec AEM 6.5
seo-description: Découvrez comment faire en sorte que vos applications et configurations restent compatibles avec AEM 6.5
uuid: 81dc2771-f59b-4b24-8932-9e938cba05e0
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: f3b4ec1d-9054-47d4-afcb-0a0121b94190
docset: aem65
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 82%

---


# Compatibilité descendante dans AEM 6.5{#backward-compatibility-in-aem}

## Présentation {#overview}

>[!NOTE]
>
>Pour obtenir la liste des modifications de contenu et de configuration qui ne font pas partie du module de compatibilité, consultez la section [Restructuration des référentiels dans AEM](/help/sites-deploying/repository-restructuring.md).

Dans AEM 6.5, toutes les fonctionnalités ont été développées dans une optique de compatibilité descendante.

Dans la majorité des cas, les utilisateurs qui exécutent AEM 6.3 ne doivent pas changer le code ni les personnalisations lorsqu’ils effectuent la mise à niveau. S’agissant d’AEM 6.1 et 6.2, aucune autre modification importante n’est à signaler lors d’une mise à niveau vers la version 6.3.

Pour les exceptions où les fonctionnalités n&#39;ont pas pu être maintenues avec une compatibilité ascendante, les problèmes d&#39;incompatibilité ascendante pour les lots et le contenu peuvent être atténués en installant un package de compatibilité pour la version 6.4 (voir comment configurer ci-dessous pour plus d&#39;informations sur l&#39;emplacement de téléchargement). Dans la plupart des cas, ce module rétablit la compatibilité des applications compatibles avec AEM 6.4.

Le module de compatibilité vous permet d’exécuter AEM en mode de compatibilité et de différer le développement personnalisé par rapport à de nouvelles fonctionnalités d’AEM :

>[!NOTE]
>
>Notez que le module de compatibilité n’est qu’une solution temporaire visant à différer le développement requis pour garantir une compatibilité avec AEM 6.5. Il est recommandé de ne l’utiliser qu’en dernier ressort si vous ne parvenez pas à remédier aux problèmes de compatibilité par le biais du développement immédiatement après la mise à niveau. Il est vivement conseillé de basculer vers le mode natif et de désinstaller le module de compatibilité dès que vous décidez de procéder au développement personnalisé basé sur 6.5 et de tirer pleinement parti des fonctionnalités de la version 6.5.

![saut](assets/sase.png)

Le module de compatibilité propose deux modes : **Routage activé** et **Routage désactivé**.

Cela vous permet d’exécuter AEM 6.5 dans trois modes différents :

**Mode natif :**

Le mode natif s’adresse aux personnes qui souhaitent utiliser toutes les nouvelles fonctionnalités d’AEM 6.5 et sont disposées à effectuer certaines tâches de développement pour que leurs personnalisations fonctionnent avec l’ensemble de ces fonctionnalités.

Cela signifie que des ajustements devront peut-être être effectués dans votre application juste après la mise à niveau.

**Mode de compatibilité : module de compatibilité installé avec le mode Routage activé**

Le mode de compatibilité s’adresse aux utilisateurs dont les personnalisations des interfaces ne sont pas rétrocompatibles. Cela permet à AEM de s’exécuter en mode de compatibilité et de différer le développement personnalisé requis par rapport aux nouvelles fonctionnalités d’AEM incompatibles avec une partie de votre code personnalisé.

**Mode hérité : module de compatibilité installé avec le mode Routage désactivé**

Le mode hérité s’adresse aux utilisateurs qui possèdent des interfaces personnalisées basées sur du code hérité ou obsolète d’AEM qui a été déplacé dans le module de compatibilité.

![sapte](assets/sapte.png)

## Méthode de configuration {#how-to-set-up}

Le package de compatibilité AEM 6.3 peut être installé en tant que package à l’aide de Package Manager. Vous pouvez télécharger le package de compatibilité [AEM 6.3 à partir du site Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/compatpack/aem-compat-cq64-to-cq63).

Une fois le module de compatibilité installé, le routage peut être activé ou désactivé à l’aide d’un commutateur dans la configuration OSGI, comme indiqué ci-dessous :

![screen_shot_2017-11-27at122421pm](assets/screen_shot_2017-11-27at122421pm.png)

Une fois le module de compatibilité installé et configuré, les fonctionnalités sont utilisées sur la base du mode de compatibilité choisi.
