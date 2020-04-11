---
title: Intégration des composants de l’espace de travail AEM Forms dans des applications Web
seo-title: Intégration des composants de l’espace de travail AEM Forms dans des applications Web
description: Comment réutiliser les composants d’espace de travail AEM Forms dans vos propres applications Web pour profiter de leurs fonctionnalités et d’une intégration étroite.
seo-description: Comment réutiliser les composants d’espace de travail AEM Forms dans vos propres applications Web pour profiter de leurs fonctionnalités et d’une intégration étroite.
uuid: bb9b8aa0-3f41-4f44-8eb7-944e778ee8a6
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6be87939-007e-42c7-8a41-e34ac2b8bed4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Intégration des composants de l’espace de travail AEM Forms dans des applications Web {#integrating-aem-forms-workspace-components-in-web-applications}

Vous pouvez utiliser les [composants](/help/forms/using/description-reusable-components.md) de l’espace de travail AEM Forms dans votre propre application Web. L’exemple d’implémentation suivant utilise des composants d’un paquet de développement d’espace de travail AEM Forms installé sur une instance CRX™ pour créer une application Web. Personnalisez la solution ci-dessous en fonction de vos besoins. The sample implementation reuses `UserInfo`, `FilterList`, and `TaskList`components inside a web portal.

1. Connectez-vous à CRXDE Lite   à `https://'[server]:[port]'/lc/crx/de/`. Assurez-vous que vous avez installé un package de développement d’espace de travail AEM Forms.
1. Créez un chemin `/apps/sampleApplication/wscomponents`.
1. Copiez css, images, js/libs, js/runtime et js/registry.js

   * de `/libs/ws`
   * vers `/apps/sampleApplication/wscomponents`.

1. Créez un fichier demomain.js dans le dossier /apps/sampleApplication/wscomponents/js. Copiez le code de /libs/ws/js/main.js dans demomain.js.
1. Dans demomain.js, supprimez le code pour initialiser le routeur et ajoutez le code suivant :

   ```
   require(['initializer','runtime/util/usersession'],
       function(initializer, UserSession) {
           UserSession.initialize(
               function() {
                   // Render all the global components
                   initializer.initGlobal();
               });
       });
   ```

1. Create a node under /content by name `sampleApplication` and type `nt:unstructured`. In the properties of this node add `sling:resourceType` of type String and value `sampleApplication`. Dans la liste de contrôle d’accès de ce nœud, ajoutez une entrée pour `PERM_WORKSPACE_USER` autorisant des privilèges jcr:read. Also, in the Access Control List of `/apps/sampleApplication` add an entry for `PERM_WORKSPACE_USER` allowing jcr:read privileges.
1. Dans `/apps/sampleApplication/wscomponents/js/registry.js` Mettre à jour les chemins de `/lc/libs/ws/` à `/lc/apps/sampleApplication/wscomponents/` pour les valeurs de modèle.
1. In your portal home page JSP file at `/apps/sampleApplication/GET.jsp`, add the following code to include the required components inside the portal.

   ```as3
   <script data-main="/lc/apps/sampleApplication/wscomponents/js/demomain" src="/lc/apps/sampleApplication/wscomponents/js/libs/require/require.js"></script>
   <div class="UserInfoView gcomponent" data-name="userinfo"></div>
   <div class="filterListView gcomponent" data-name="filterlist"></div>
   <div class="taskListView gcomponent" data-name="tasklist"></div>
   ```

   Incluez également les fichiers CSS requis pour les composants d’espace de travail AEM Forms.

   >[!NOTE]
   >
   >Chaque composant est ajouté à la balise du composant (ayant la classe gcomponent) pendant le rendu. Assurez-vous que votre page d’accueil contient ces balises. Voir le fichier `html.jsp` de l’espace de travail AEM Forms pour en savoir plus sur les balises de contrôle de base.

1. Pour personnaliser les composants, agrandissez les vues existantes pour le composant requis comme suit :

   ```as3
   define([
       ‘jquery’,
       ‘underscore’,
       ‘backbone’,
       ‘runtime/views/userinfo'],
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

1. Modifiez le portail CSS pour configurer la mise en page, le positionnement et le style des composants souhaités sur votre portail. Par exemple, vous souhaitez garder la couleur d’arrière-plan en noir pour ce portail pour afficher correctement le composant userInfo. You can do this by changing background color in `/apps/sampleApplication/wscomponents/css/style.css` as follows:

   ```as3
   body {
       font-family: "Myriad pro", Arial;
       background: #000;    //This was origianlly #CCC
       position: relative;
       margin: 0 auto;
   }
   ```
