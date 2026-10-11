---
title: Mise à jour du lien vers la documentation
description: Comment mettre à jour la destination du lien d’aide de Workspace dans l’espace de travail AEM Forms pour qu’il pointe vers le lien de documentation personnalisé.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 100%
---
# Mise à jour du lien vers la documentation {#updating-the-link-to-the-documentation}

Vous pouvez accéder au contenu de l’aide par défaut pour l’espace de travail AEM Forms en sélectionnant **Aide > Aide de Workspace**. Le chemin pointe vers la documentation en ligne sur le site Web d’Adobe. Cependant, vous pouvez le mettre à jour pour qu’il pointe vers une autre URL.

Tenez compte des cas d’utilisation suivants où vous pouvez modifier l’URL d’aide par défaut :

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
