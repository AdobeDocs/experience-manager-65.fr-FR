---
title: Mise à jour du lien vers la documentation
description: Comment mettre à jour la destination du lien d’aide de Workspace dans l’espace de travail AEM Forms pour qu’il pointe vers votre lien de documentation personnalisé.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 60%

---

# Mise à jour du lien vers la documentation  {#updating-the-link-to-the-documentation}

Vous pouvez accéder au contenu de l’aide par défaut pour l’espace de travail AEM Forms en sélectionnant **Aide > Aide de Workspace**. Le chemin pointe vers la documentation en ligne sur le site Web d’Adobe. Cependant, vous pouvez le mettre à jour pour qu’il pointe vers une autre URL.

Tenez compte des cas d’utilisation suivants où vous pouvez modifier l’URL d’aide par défaut :

* Pour fournir une aide localisée dans une langue de votre choix.
* Pour fournir un contenu d’aide personnalisé pour votre espace de travail personnalisé.

Pour mettre à jour l’URL de la documentation en ligne, suivez la [Procédure générique de personnalisation](/help/forms/using/generic-steps-html-workspace-customization.md), puis les étapes suivantes.

1. Copiez le fichier `userinfo.html` de `/libs/ws/js/runtime/templates` vers `/apps/ws/js/runtime/templates`.
1. Modification:

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
   1. Recherchez et remplacez `text!/lc/libs/ws/js/runtime/templates/userinfo.html` avec `text!/lc/apps/ws/js/runtime/templates/userinfo.html`.
