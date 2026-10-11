---
title: Intégration des composants de l’espace de travail AEM Forms dans des applications web
description: Comment réutiliser les composants de l’espace de travail AEM Forms dans vos propres applications web pour utiliser les fonctionnalités et fournir une intégration étroite.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: bb4a500d-c34f-4586-83f0-ad7ef69b4fb1
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 91%
---
# Intégration des composants de l’espace de travail AEM Forms dans des applications web {#integrating-aem-forms-workspace-components-in-web-applications}

Vous pouvez utiliser les [composants](/help/forms/using/description-reusable-components.md) de l’espace de travail AEM Forms dans votre propre application web. L’exemple d’implémentation suivant utilise des composants d’un package de développement d’espace de travail AEM Forms installé sur une instance CRX™ pour créer une application web. Personnalisez la solution ci-dessous en fonction de vos besoins. L’exemple d’implémentation réutilise les composants `UserInfo`, `FilterList` et `TaskList` dans un portail Web.

1. Connectez-vous à l’environnement CRXDE Lite à l’adresse `https://'[server]:[port]'/lc/crx/de/`. Assurez-vous que vous avez installé un package de développement d’espace de travail AEM Forms.
1. Créez un chemin d’accès `/apps/sampleApplication/wscomponents`.
1. Copiez css, images, js/libs, js/runtime et js/registry.js

   * de `/libs/ws`
   * vers `/apps/sampleApplication/wscomponents`.

1. Créez un fichier demomain.js dans le dossier /apps/sampleApplication/wscomponents/js. Copiez le code de /libs/ws/js/main.js dans demomain.js.
1. Dans demomain.js, supprimez le code pour initialiser le routeur et ajoutez le code suivant :

   ```javascript
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Créez un nœud sous /content du nom de `sampleApplication` et du type `nt:unstructured`. Dans les propriétés de ce nœud, ajoutez `sling:resourceType` du type chaîne et de la valeur `sampleApplication`. Dans la liste de contrôle d’accès de ce nœud, ajoutez une entrée pour `PERM_WORKSPACE_USER` autorisant des privilèges jcr:read. En outre, dans la liste de contrôle d’accès de `/apps/sampleApplication`, ajoutez une entrée pour `PERM_WORKSPACE_USER` autorisant des privilèges jcr:read.
1. Dans `/apps/sampleApplication/wscomponents/js/registry.js`, mettez à jour les chemins d’accès de `/lc/libs/ws/` à `/lc/apps/sampleApplication/wscomponents/` pour les valeurs des modèles.
1. Dans le fichier JSP de la page d’accueil de votre portail, à l’adresse `/apps/sampleApplication/GET.jsp`, ajoutez le code suivant pour inclure les composants requis dans le portail.

   ```jsp
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Incluez également les fichiers CSS requis pour les composants de l’espace de travail AEM Forms.

   >[!NOTE]
   >
   >Chaque composant est ajouté à la balise du composant (ayant la classe gcomponent) pendant le rendu. Assurez-vous que votre page d’accueil contient ces balises. Voir le fichier `html.jsp` de l’espace de travail AEM Forms pour en savoir plus sur les balises de contrôle de base.

1. Pour personnaliser les composants, vous pouvez étendre les vues existantes pour le composant requis comme suit :

   ```javascript
   define([
       'jquery',
       'underscore',
       'backbone',
       'runtime/views/userinfo'],
       function($, _, Backbone, UserInfo){
           var demoUserInfo = UserInfo.extend({
               //override the functions to customize the functionality
               render: function() {
                   UserInfo.prototype.render.call(this); // call the render function of the super class
                   …
                   //other tasks
                   …
               }
           });
           return demoUserInfo;
   });
   ```

1. Modifiez le portail CSS pour configurer la disposition, le positionnement et le style des composants souhaités sur votre portail. Par exemple, vous souhaitez garder la couleur d’arrière-plan en noir pour ce portail pour afficher correctement le composant userInfo. Vous pouvez le faire en modifiant la couleur d’arrière-plan dans `/apps/sampleApplication/wscomponents/css/style.css` comme suit :

   ```css
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
