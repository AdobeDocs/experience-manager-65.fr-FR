---
title: Définition de votre filtre Référent sur Autoriser vide
description: En savoir plus sur le filtrage des référents. Pour permettre à la visionneuse d’applications mobiles Adobe Experience Manager (AEM) d’afficher des applications sur votre instance d’auteur, vous devez définir votre filtre de référent HTML sur « autoriser vide ».
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
solution: Experience Manager
feature: Mobile
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 3%
---
# Définition de votre filtre Référent sur Autoriser vide{#setting-your-referrer-filter-to-allow-empty}

{{ue-over-mobile}}

Pour permettre à la visionneuse d’applications mobiles Adobe Experience Manager (AEM) d’afficher des applications sur votre instance d’auteur, vous devez définir votre filtre de référent HTML sur « autoriser vide ».

Si vous n’avez pas l’intention d’utiliser la visionneuse d’applications pour passer en revue les applications dans les états de développement et d’évaluation, vous n’avez pas besoin de modifier le paramètre par défaut du filtre référent.

Dans votre instance d’auteur AEM en cours d’exécution, accédez à : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) et recherchez « Filtre de référent Apache Sling ». Cliquez pour modifier le filtre référent et cochez la case « Autoriser les champs vides » (voir l’image ci-dessous). Appuyez ensuite sur le bouton Enregistrer et fermez la page du navigateur.

![Paramètres de filtrage des référents](assets/chlimage_1-106.png)
