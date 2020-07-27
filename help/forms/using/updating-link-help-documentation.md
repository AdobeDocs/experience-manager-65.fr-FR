---
title: Mise à jour du lien vers la documentation
seo-title: Mise à jour du lien vers la documentation
description: Comment mettre à jour la destination du lien d’aide de l’espace de travail dans l’espace de travail AEM Forms pour renvoyer à votre lien de documentation personnalisé.
seo-description: Comment mettre à jour la destination du lien d’aide de l’espace de travail dans l’espace de travail AEM Forms pour renvoyer à votre lien de documentation personnalisé.
uuid: 64056d10-1451-44ed-8f25-81a21037dc75
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 788c427f-190f-4580-9efd-6a4c4a008837
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 94%

---


# Mise à jour du lien vers la documentation {#updating-the-link-to-the-documentation}

Vous pouvez accéder au contenu de l’aide par défaut pour l’espace de travail AEM Forms en sélectionnant **Aide > Aide de Workspace**. Le chemin pointe vers la documentation en ligne sur le site Web d’Adobe. Cependant, vous pouvez le mettre à jour pour qu’il pointe vers une autre URL.

Tenez compte des cas d’utilisation suivants lorsque vous souhaitez changer l’URL d’aide par défaut :

* Pour fournir une aide localisée dans une langue de votre choix.
* Pour fournir un contenu d’aide personnalisé pour votre espace de travail personnalisé.

Pour mettre à jour l’URL de la documentation en ligne, suivez la [Procédure générique de personnalisation](/help/forms/using/generic-steps-html-workspace-customization.md), puis les étapes suivantes.

1. Copy the `userinfo.html` file from `/libs/ws/js/runtime/templates` to `/apps/ws/js/runtime/templates`.
1. Remplacer :

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   vers

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. Procédez comme suit :

   1. Ouvrez /apps/ws/js/registry.js pour le modifier.
   1. Search and replace `text!/lc/libs/ws/js/runtime/templates/userinfo.html` with `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
