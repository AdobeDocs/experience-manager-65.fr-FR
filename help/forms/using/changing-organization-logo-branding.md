---
title: Modifier le logo de l’organisation pour l’identité graphique
description: Pour attribuer une marque à l’espace de travail AEM Forms, remplacez le logo par défaut par celui de votre organisation.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 100%
---
# Modifier le logo de l’organisation pour l’identité graphique {#changing-the-organization-logo-for-branding}

Le logo de l’organisation s’affiche dans le coin supérieur gauche de l’espace de travail AEM Forms. Pour mettre à jour le logo, suivez les [Étapes génériques de personnalisation de l’espace de travail AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization), puis les étapes ci-après.

1. Créez un logo et nommez le fichier `NewWorkspace.png`. Placez le fichier image dans le dossier /apps/ws/images à l’aide d’un client WebDAV.

   >[!NOTE]
   >
   >La taille recommandée de l’image de logo est de 218 px × 20 px.

   >[!NOTE]
   >
   >Pour plus d’informations, voir [Accès WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=fr).

   [Accès WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=fr)

1. Reportez-vous à l’image du nouveau logo dans la feuille de style sous /apps/ws/css/newStyle.css en ajoutant le style suivant.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
