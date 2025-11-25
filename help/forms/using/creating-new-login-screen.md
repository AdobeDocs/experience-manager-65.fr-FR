---
title: Création d’un écran de connexion
description: Comment modifier la page de connexion des modules de LiveCycle, par exemple de l’espace de travail d’AEM Forms ou de Forms Manager.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 5cb906b6-6a3c-498c-94f5-27a9071ea934
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 98%

---

# Création d’un écran de connexion{#creating-a-new-login-screen}

Vous pouvez modifier l’écran de connexion de tous les modules AEM Forms qui utilisent l’écran de connexion AEM Forms. Par exemple, les modifications affectent à la fois l’écran de connexion de Forms Manager et de l’espace de travail d’AEM Forms.

## Prérequis {#prerequisite}

1. Connectez-vous à `/lc/crx/de` avec des droits d’administrateur.
1. Procédez comme suit :

   1. Répliquez la structure hiérarchique : de `/libs/livecycle/core/content` vers `/apps/livecycle/core/content`.

      Conservez les mêmes propriétés (nœud/dossier) et contrôle d’accès.

   1. Copiez le dossier de contenu :

      de: `/libs/livecycle/core`

      vers: `/apps/livecycle/core`.

   1. Supprimez le contenu du dossier `/apps/livecycle/core`.

1. Procédez comme suit :

   1. Répliquez la structure hiérarchique : de `/libs/livecycle/core/components/login` vers `/apps/livecycle/core/components/login`. Conservez les mêmes propriétés (nœud/dossier) et contrôle d’accès.

   1. Copiez le dossier de composants de `/libs/livecycle/core` vers `/apps/livecycle/core`.

   1. Supprimez le contenu du dossier `/apps/livecycle/core/components/login`.

### Ajout de nouveaux paramètres régionaux {#adding-a-new-locale}

1. Copiez le dossier `i18n`

   * de `/libs/livecycle/core/components/login`
   * vers `/apps/livecycle/core/components/login`

1. Supprimez tous les dossiers contenus dans `i18n` sauf un, comme `en`, par exemple.

1. Sur le dossier `en`, procédez comme suit :

   1. Donnez au dossier le nom de l’ensemble de paramètres régionaux que vous souhaitez prendre en charge. Par exemple, `ar`.

   1. Modifiez la valeur de la propriété `jcr:language` en `ar` (pour le dossier `ar`).

   >[!NOTE]
   >
   >Si les paramètres régionaux sont une combinaison de code langue-pays, comme `ar-DZ`, modifiez le nom du dossier et la valeur de la propriété en `ar-DZ`.

1. Copier `login.jsp` :

   * de `/libs/livecycle/core/components/login`
   * vers `/apps/livecycle/core/components/login`

1. Modifiez le fragment de code suivant pour `/apps/livecycle/core/components/login/login.jsp` :

   ***Les paramètres régionaux sont un code de langue***

   ```jsp
   String browserLocale = "en";
   
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   To

   ```jsp
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("ar")) {
               browserLocale = "ar";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   ```jsp
   String browserLocale = "en";
   
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

   To

   ```jsp
   String browserLocale = "en";
       for(int i=0; i<locales.length; i++)
       {
           String prioperty = locales[i];
           if(prioperty.trim().equalsIgnoreCase("ar-DZ")) {
               browserLocale = "ar-DZ";
               break;
           }
           if(prioperty.trim().startsWith("en")) {
               browserLocale = "en";
               break;
           }
           if(prioperty.trim().startsWith("de")){
               browserLocale = "de";
               break;
           }
           if(prioperty.trim().startsWith("ja")){
               browserLocale = "ja";
               break;
           }
           if(prioperty.trim().startsWith("fr")){
               browserLocale = "fr";
               break;
           }
       }
   ```

***Pour modifier les paramètres régionaux par défaut***.

```jsp
   String browserLocale = "en";
   for(int i=0; i<locales.length; i++)

   To

   String browserLocale = "ar";
   for(int i=0; i<locales.length; i++)
```

### Ajouter du nouveau texte ou modifier du texte existant {#adding-new-text-or-modifying-existing-text}

1. Copiez le dossier `i18n`

   * de `/libs/livecycle/core/components/login`
   * vers `/apps/livecycle/core/components/login`

1. Modifiez la valeur de la propriété `sling:message` du nœud (sous le dossier du code des paramètres régionaux souhaité) pour laquelle vous souhaitez modifier le texte. La traduction est effectuée via la clé mentionnée dans la valeur de la propriété `sling:key` du nœud.

1. Pour ajouter une nouvelle paire clé-valeur, effectuez les opérations suivantes : Vérifiez un exemple dans la capture d’écran qui suit.

   1. Créez un nœud de type `sling:MessageEntry` ou copiez un nœud existant et renommez-le, sous tous les dossiers de paramètres régionaux.
   1. Copier `login.jsp` :

      * de `/libs/livecycle/core/components/login`

      * vers `/apps/livecycle/core/components/login`

   1. Modifiez `/apps/livecycle/core/components/login/login.jsp` pour incorporer le texte nouvellement ajouté.

   ![Ajout d’une nouvelle paire clé-valeur](assets/capture_new.png)

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

   To

   ```jsp
   div class="loginContent">
   
                       <span class="loginFlow"></code>
                       <span class="loginVersion"><%= i18n.get("My Welcome Message") %></code>
                       <span class="loginVersion"><%= i18n.get("Version: 11.0.0") %></code>
                       <span class="loginTitle"><%= i18n.get("Login") %></code>
                       <% if (loginFailed) {%>
   ```

### Ajout d’un nouveau style ou modification d’un style existant {#adding-new-style-or-modifying-existing-style}

1. Copiez le nœud `login` :

   * de `/libs/livecycle/core/content`
   * vers `/apps/livecycle/core/content`

1. Supprimez les fichiers `login.js` et `jquery-1.8.0.min.js` du noeud `/apps/livecycle/core/content/login.`
1. Modifiez les styles du fichier CSS.
1. Pour ajouter de nouveaux styles :

   1. Ajoutez de nouveaux styles à `/apps/livecycle/core/content/login/login.css`
   1. Copier `login.jsp`

      * de `/libs/livecycle/core/components/login`

      * vers `/apps/livecycle/core/components/login`

   1. Modifiez `/apps/livecycle/core/components/login/login.jsp` pour incorporer les styles nouvellement ajoutés.


Par exemple :

* Ajoutez le code suivant à `/apps/livecycle/core/content/login/login.css`.

  ```
  css.newLoginContentArea {
      width: 700px;
      padding: 100px 0px 0px 100px;
  }
  ```

* Modifiez les éléments suivants dans `/apps/livecycle/core/components/login.jsp`.


  ```jsp
  <div class="loginContentArea">
  ```

  To

  ```jsp
  <div class="newLoginContentArea">
  ```

>[!NOTE]
>
>Si les images contenues dans `/apps/livecycle/core/content/login` (copiées à partir de `/libs/livecycle/core/content/login`) sont supprimées, supprimez les références correspondantes dans CSS.

### Ajoutez de nouvelles images {#add-new-images}

1. Suivez les étapes des sections Ajout d’un nouveau style ou Modification d’un style existant (présentées ci-dessus).
1. Ajoutez de nouvelles images dans `/apps/livecycle/core/content/login`. Pour ajouter une image :

   1. Installez le client WebDAV.
   1. Naviguez jusqu’au dossier `/apps/livecycle/core/content/login` à l’aide du client webDAV. Pour plus d’informations, voir [Accès WebDAV](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/webdav-access.html?lang=fr).

   1. Ajoutez de nouvelles images.

1. Ajoutez de nouveaux styles dans `/apps/livecycle/core/content/login/login.css,` correspondant aux nouvelles images ajoutées dans `/apps/livecycle/core/content/login`.
1. Utilisez les nouveaux styles dans `login.jsp` dans `/apps/livecycle/core/components`.

   Par exemple :


   ```css
   .newLoginContainerBkg {
   
    background-image: url(my_Bg.gif);
    background-repeat: no-repeat;
    background-position: left top;
    width: 727px;
   }
   ```


   * Modifiez les éléments suivants dans /apps/livecycle/core/components/login.jsp.

   ```jsp
   <div class="loginContainerBkg">
   ```

   À

   ```jsp
   <div class="newLginContainerBkg">
   ```
