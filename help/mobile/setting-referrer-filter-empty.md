---
title: Définition du filtre de référent sur Autoriser vide
description: En savoir plus sur le filtre de référent. Pour permettre à Adobe Experience Manager (AEM) Mobile Application Viewer d’afficher des applications sur votre instance d’auteur, vous devez définir le filtre de référent de HTML sur "autoriser vide".
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 2f02f541-92db-469b-bf23-ec64d2e282ff
source-git-commit: 6799f1d371734b69c547f3c0c68e1e633aa63229
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 3%

---

# Définition du filtre de référent sur Autoriser vide{#setting-your-referrer-filter-to-allow-empty}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Pour permettre à Adobe Experience Manager (AEM) Mobile Application Viewer d’afficher des applications sur votre instance d’auteur, vous devez définir le filtre de référent de HTML sur &quot;autoriser vide&quot;.

Si vous n’avez pas l’intention d’utiliser la visionneuse d’applications pour passer en revue les applications dans les états de développement et d’évaluation, il n’est pas nécessaire de modifier le paramètre par défaut du filtre de référent.

Dans votre instance d’auteur en cours d’exécution d’AEM, accédez à : [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr) et recherchez &quot;Apache Sling Referrer Filter&quot;. Cliquez pour modifier le filtre de référent et cochez la case &quot;autoriser vide&quot; (voir l’image ci-dessous). Appuyez ensuite sur le bouton d’enregistrement et fermez la page du navigateur.

![Paramètres du filtre de référent](assets/chlimage_1-106.png)
