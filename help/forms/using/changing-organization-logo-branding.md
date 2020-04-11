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
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Modification du logo de l’organisation pour l’identité graphique {#changing-the-organization-logo-for-branding}

Le logo de l’entreprise est affiché dans l’angle supérieur gauche de l’espace de travail d’AEM Forms. Pour mettre le logo à jour, suivez les instructions de la section [Étapes génériques de la configuration de l’espace de travail d’AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization), puis les étapes suivantes.

1. Créez un logo et nommez le fichier `NewWorkspace.png`. Placez le fichier image dans le dossier /apps/ws/images à l’aide d’un client WebDAV.

   >[!NOTE]
   >
   >la taille recommandée de l’image de logo est de 218 px × 20 px.

   >[!NOTE]
   >
   >For more information about WebDAV access, see [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

1. Reportez-vous à l’image du nouveau logo dans la feuille de style sous /apps/ws/css/newStyle.css en ajoutant le style suivant.

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
