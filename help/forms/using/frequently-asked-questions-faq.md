---
title: Questions fréquentes sur les formulaires adaptatifs, les formulaires HTML5 et AEM Forms
description: Questions fréquentes sur la disposition, la prise en charge des scripts et la portée des formulaires adaptatifs, des formulaires HTML5 et d’AEM Forms.
docset: aem65
exl-id: 19a6e431-de66-4d5c-924f-f9c1a195390c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 100%
---
# Questions fréquentes {#frequently-asked-questions-faq}

1. Pourquoi les champs de codes à barres et de signature n’apparaissent pas dans mon formulaire HTML5 ?

   Réponse : les champs de codes à barres et de signatures ne sont pas adaptés aux cas de figures impliquant du HTML ou des périphériques mobiles. Ces champs apparaissent comme des zones non interactives. Cependant, AEM Forms Designer propose un nouveau champ de griffonnage de signature qui peut être utilisé à la place du champ de signature. Vous pouvez également ajouter un [widget personnalisé](../../forms/using/custom-widgets.md) pour les codes à barres et l’intégrer.
