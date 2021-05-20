---
title: Activation de la protection de lien dynamique dans Dynamic Media
description: Informations sur l’activation de la protection de lien dynamique dans Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: Business Practitioner, Administrator
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 19%

---

# Activation de la protection de lien dynamique dans Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Les liens chauds sont utilisés lorsqu’un site web tiers utilise du code HTML pour afficher une image de votre site web. Il utilise votre bande passante chaque fois que l’image est demandée, car le navigateur du visiteur y accède directement depuis votre serveur. Le lien dynamique *protection* est une méthode permettant d’empêcher d’autres sites web d’accéder directement à des images, des css ou du code JavaScript sur vos pages web. Ce type de protection contribue à réduire l’utilisation inutile de bande passante sous votre compte Dynamic Media.

[Le ](https://helpx.adobe.com/fr/support.html) support Adobe peut configurer un filtre de référent au niveau du réseau CDN (Content Delivery Network), de sorte que le contenu Dynamic Media ne soit diffusé que sur les sites web figurant sur votre liste de sites web autorisés pour le domaine.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du réseau de diffusion de contenu prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre réseau de diffusion de contenu personnalisé n’est pris en charge avec cette fonctionnalité. Pour activer la protection de lien dynamique, un administrateur doit créer un ticket d’assistance clientèle Adobe pour demander la modification de configuration à votre compte Dynamic Media. L’activation de la protection de lien dynamique n’entraîne aucun coût supplémentaire.
