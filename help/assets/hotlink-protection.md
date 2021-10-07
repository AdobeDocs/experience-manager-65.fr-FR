---
title: Activation de la protection de lien dynamique dans Dynamic Media
description: Informations sur l’activation de la protection de lien dynamique dans Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 47%

---

# Activation de la protection de lien dynamique dans Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

On parle de lien dynamique lorsqu’un site web tiers utilise du code HTML pour afficher une image de votre site web. Il utilise votre bande passante chaque fois que l’image est demandée, car le navigateur du visiteur y accède directement depuis votre serveur. Le lien dynamique *protection* est une méthode permettant d’empêcher d’autres sites web d’accéder directement à des images, des CSS ou du code JavaScript sur vos pages web. Ce type de protection contribue à réduire l’utilisation inutile de bande passante sous votre compte Dynamic Media.

[Le ](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) service clientèle du Experience Manager peut configurer un filtre de référent au niveau du réseau CDN (Content Delivery Network), de sorte que le contenu Dynamic Media ne soit diffusé que sur les sites web figurant sur votre liste de sites web autorisés pour le domaine.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du réseau CDN prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre réseau CDN personnalisé n’est pris en charge avec cette fonctionnalité. Pour activer la protection de lien dynamique, un administrateur doit créer un ticket d’assistance clientèle d’Adobe pour demander la modification de configuration à votre compte Dynamic Media. L’activation de la protection de lien dynamique n’implique aucun frais supplémentaires.
