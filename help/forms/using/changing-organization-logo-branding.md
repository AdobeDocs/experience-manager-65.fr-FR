---
title: Modifier le logo de l’organisation pour l’identité graphique
seo-title: Changing the organization logo for branding
description: Pour attribuer une marque à l’espace de travail AEM Forms, remplacez le logo par défaut par celui de votre organisation.
seo-description: To brand AEM Forms workspace provide the logo of your organization by customizing the default logo.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: ht
source-wordcount: '133'
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
   >Pour plus d’informations sur l’accès à WebDAV, consultez la section [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr).

1. Reportez-vous à l’image du nouveau logo dans la feuille de style sous /apps/ws/css/newStyle.css en ajoutant le style suivant.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
