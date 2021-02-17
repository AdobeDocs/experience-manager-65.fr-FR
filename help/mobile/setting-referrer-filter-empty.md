---
title: Définition de votre filtre de référent sur Autoriser vide
seo-title: Définition de votre filtre de référent sur Autoriser vide
description: Suivez cette page pour en savoir plus sur le filtre de Parrain. Pour autoriser l’application AEM Mobile Application Viewer à vue les applications de votre instance d’auteur, vous devez définir votre filtre de parrain HTML sur "Autoriser vide".
seo-description: Suivez cette page pour en savoir plus sur le filtre de Parrain. Pour autoriser l’application AEM Mobile Application Viewer à vue les applications de votre instance d’auteur, vous devez définir votre filtre de parrain HTML sur "Autoriser vide".
uuid: 4fb0f95c-ac8f-4a14-8c46-6616d9d4f380
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 8fb7d088-94bf-4799-98b3-8fa58eef83df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 47%

---


# Définition de votre filtre de référent sur Autoriser vide{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Pour autoriser l’application AEM Mobile Application Viewer à vue les applications de votre instance d’auteur, vous devez définir votre filtre de parrain HTML sur &quot;Autoriser vide&quot;.

Si vous n’avez pas l’intention d’utiliser la visionneuse d’application pour passer en revue les applications se trouvant aux stades de développement et intermédiaire, il n’est pas nécessaire de modifier le paramètre par défaut du filtre de référent.

Dans l’instance d’auteur en cours d’exécution de l’AEM, accédez à : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) et recherchez &quot;Apache Sling Parrain Filter&quot;. Cliquez pour modifier le filtre de référent et cochez la case « autoriser vide » (voir l’image ci-dessous). Cliquez ensuite sur le bouton Enregistrer et fermez la page du navigateur.

![Paramètres du filtre de référent](assets/chlimage_1-106.png)
