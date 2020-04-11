---
title: Hébergement de deux instances d’espace de travail AEM Forms sur un serveur
seo-title: Hébergement de deux instances d’espace de travail AEM Forms sur un serveur
description: Comment les administrateurs LC peuvent-ils personnaliser WS HTML pour l’hébergement de deux instances sur un serveur unique accessible via différentes URL ?
seo-description: Comment les administrateurs LC peuvent-ils personnaliser WS HTML pour l’hébergement de deux instances sur un serveur unique accessible via différentes URL ?
uuid: 0584f512-6b92-4418-b71c-93605cfa1927
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 1254a7c2-2c67-4661-803e-afd53e817916
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Hébergement de deux instances d’espace de travail AEM Forms sur un serveur {#hosting-two-aem-forms-workspace-instances-on-one-server}

L’installation et les paramètres par défaut d’AEM Forms permettent la mise à disposition d’un seul espace de travail AEM Forms sur le serveur. Cela dit, vous pouvez être amené à héberger deux instances différentes d’AEM Forms sur un serveur AEM Forms unique. Les deux instances sont accessibles via différentes URL.

Les administrateurs d’AEM Forms personnalisent l’espace de travail afin de créer deux URL différentes et de rendre disponibles deux espaces de travail sur le même serveur. Dans cet article de personnalisation, nous supposons que les deux espaces de travail sont accessibles à l’adresse `https://'[server]:[port]'/lc/ws` et `https://'[server]:[port]':/lc/ws2`.

Procédez comme suit pour configurer l’espace de travail AEM Forms.

1. Installez le package de développement de l’espace de travail AEM Forms sur votre serveur. Voir [Package de développement](/help/forms/using/introduction-customizing-html-workspace.md#p-crx-package-p) pour obtenir des instructions de création.
1. Connectez-vous à CRXDE Lite en tant qu’administrateur en accédant à `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Copiez et collez le nœud ws dans /content. Attribuez au nœud le nom ws2. Cliquez sur **[!UICONTROL Enregistrer tout]**. Dans les propriétés de ce nœud, attribuez à `sling:resourceType` la valeur ws2. Cliquez sur **[!UICONTROL Enregistrer tout]**. 

1. Copiez le dossier ws dans /libs et collez-le dans /apps. Attribuez au dossier le nom ws2. Cliquez sur **[!UICONTROL Enregistrer tout]**. 
1. In `GET.jsp` at `/apps/ws2`, make the following code changes. Remplacez le code :

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" /><html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/libs/ws/index.html'" />
   ```

   par le code suivant :

   ```
   <html lang="en">
   <head>
       <meta charset="utf-8">
       <title>Workspace Next</title>
       <meta http-equiv="refresh" content="0;URL='/lc/apps/ws2/index.html'" />
   ```

1. In `registry.js` at `/apps/ws2/js`, change path of templates to refer to templates at `/apps/ws2/js/runtime/templates`. Remplacez le code :

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/libs/ws/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

   par le code suivant :

   ```css
   "tasklist" : {
   "name": "tasklist",
   "path": "tasklistview",
   "model": "tasklist",
   "template": "text!/lc/apps/ws2/js/runtime/templates/tasklist.html",
   "utility": "utility",
   "view": "taskview",
   "errorModel": null
   }
   ```

1. Dans `userinfo.js` at `/apps/ws2/js/runtime/models` and `/apps/ws2/js/runtime/views`, remplacez la chaîne `/lc/content/ws` par `lc/content/ws2`.

1. Dans `/apps/ws2/js/runtime/services/service.js`, modifiez le chemin dans `getLocalizationData` la fonction pour qu’il pointe vers `/lc/apps/ws2/Locale.html`.

1. To refer to `pdf.html` of the new Workspace, change the path of `pdf.html` in `/apps/ws2/js/runtime/views/forms/pdftaskform.js`.

1. To refer to `pdf.html` of the new Workspace, change paths of `pdf.html` and `WsNextAdapter.swf` in `startprocess.html`, `taskdetails.html`, and `processinstancehistory.html` at `/apps/ws2/js/runtime/templates`.

1. Copy `/etc/map/ws` folder and paste at `/etc/map`. Attribuez le nom ws2 à ce nouveau dossier. Cliquez sur Enregistrer tout.

1. In properties of `ws2`, change value of `sling:redirect` to `content/ws2`.

1. Modifiez la valeur de `sling:match` en `^[^/\||]/[^/\||]/ws2$`.
