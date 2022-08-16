---
title: Définition de votre filtre de référent sur Autoriser vide
seo-title: Setting Your Referrer Filter to Allow Empty
description: Consultez cette page pour en savoir plus sur le filtre de référent. Pour permettre à la visionneuse d’applications AEM Mobile d’afficher les applications sur votre instance d’auteur, vous devez définir le filtre de référent de HTML sur "autoriser vide".
seo-description: Follow this page to learn about Referrer Filter. In order to allow the AEM Mobile Application Viewer to view apps on your Author instance, you'll need to set your HTML referrer filter to 'allow empty'.
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 54%

---

# Définition de votre filtre de référent sur Autoriser vide{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Pour permettre à la visionneuse d’applications AEM Mobile d’afficher les applications sur votre instance d’auteur, vous devez définir le filtre de référent de HTML sur &quot;autoriser vide&quot;.

Si vous n’avez pas l’intention d’utiliser la visionneuse d’application pour passer en revue les applications se trouvant aux stades de développement et intermédiaire, il n’est pas nécessaire de modifier le paramètre par défaut du filtre de référent.

Dans votre instance d’auteur en cours d’exécution d’AEM, accédez à : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) et recherchez &quot;Apache Sling Referrer Filter&quot;. Cliquez pour modifier le filtre de référent et cochez la case « autoriser vide » (voir l’image ci-dessous). Cliquez ensuite sur le bouton Enregistrer et fermez la page du navigateur.

![Paramètres du filtre de référent](assets/chlimage_1-106.png)
