---
title: Modification du logo de l’organisation pour l’identité graphique
seo-title: Modification du logo de l’organisation pour l’identité graphique
description: Pour attribuer une identité graphique à l’espace de travail d’AEM Forms, fournissez le logo de votre entreprise en personnalisant le logo par défaut.
seo-description: Pour attribuer une identité graphique à l’espace de travail d’AEM Forms, fournissez le logo de votre entreprise en personnalisant le logo par défaut.
uuid: f0c340ee-2e54-4bb0-9c30-383cc1bbadb8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2c651302-f4ef-4211-b897-f5942ed0ffb1
exl-id: 49572f2a-f3ec-4ee6-98b8-2563de1cf96c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 82%

---

# Modification du logo de l’organisation pour l’identité graphique {#changing-the-organization-logo-for-branding}

Le logo de l’entreprise est affiché dans l’angle supérieur gauche de l’espace de travail d’AEM Forms. Pour mettre le logo à jour, suivez les instructions de la section [Étapes génériques de la configuration de l’espace de travail d’AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization), puis les étapes suivantes.

1. Créez un logo et nommez le fichier `NewWorkspace.png`. Placez le fichier image dans le dossier /apps/ws/images à l’aide d’un client WebDAV.

   >[!NOTE]
   >
   >la taille recommandée de l’image de logo est de 218 px × 20 px.

   >[!NOTE]
   >
   >Pour plus d’informations sur l’accès WebDAV, voir [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Reportez-vous à l’image du nouveau logo dans la feuille de style sous /apps/ws/css/newStyle.css en ajoutant le style suivant.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
