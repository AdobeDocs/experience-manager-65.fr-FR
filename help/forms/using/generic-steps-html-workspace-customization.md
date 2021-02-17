---
title: Procédure générique de personnalisation de l’espace de travail AEM Forms
seo-title: Procédure générique de personnalisation de l’espace de travail AEM Forms
description: Initiation à la personnalisation de l’interface utilisateur de l’espace de travail AEM Forms.
seo-description: Initiation à la personnalisation de l’interface utilisateur de l’espace de travail AEM Forms.
uuid: da6310b4-1c58-468d-85c6-975fd2c141f9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: dd3218c4-2bb2-40fc-9141-5823b0ea4224
docset: aem65
translation-type: tm+mt
source-git-commit: e863089a4328b7222b60429c82ca3df2b8e1dd05
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 40%

---


# Procédure générique de personnalisation de l’espace de travail AEM Forms {#generic-steps-for-aem-forms-workspace-customization}

Voici la procédure générique à suivre pour personnaliser Workspace HTML :

1. Connectez-vous au CRXDE Lite en accédant à `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Créez un dossier `sling:Folder` nommé `ws` à `/apps`, s&#39;il n&#39;existe pas. Pour créer un dossier `sling:Folder`, cliquez avec le bouton droit sur le dossier `apps` et sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Créer un noeud]**. Indiquez le nom `ws`, sélectionnez le type `sling:Folder` et cliquez sur **[!UICONTROL OK]**. Cliquez sur **[!UICONTROL Enregistrer tout]**.
1. Accédez à `/apps/ws` et accédez à l&#39;onglet **[!UICONTROL Contrôle d&#39;accès]**.
1. Sélectionnez l&#39;option **[!UICONTROL Repository]**. Dans la liste **[!UICONTROL Contrôle d&#39;accès]**, cliquez sur **[!UICONTROL +]** pour ajouter une nouvelle entrée. Cliquez de nouveau sur **[!UICONTROL +]**.
1. Recherchez et sélectionnez l&#39;entité de sécurité **PERM_WORKSPACE_USER**.

   ![Sélectionnez l’entité de sécurité PERM_WORKSPACE_USER dans le cadre des étapes génériques de personnalisation de Workspace HTML](assets/perm_workspace_user.png)

1. Attribuez le privilège `jcr:read` à l&#39;entité de sécurité.
1. Cliquez sur **[!UICONTROL Enregistrer tout]**.
1. Copiez les fichiers `GET.jsp`, `index` et `html.jsp` du dossier `/libs/ws` dans le dossier `/apps/ws`.
1. Copiez le dossier `/libs/ws/locales` dans le dossier `/apps/ws`. Cliquez sur **[!UICONTROL Enregistrer tout]**.
1. Mettez à jour les références et les chemins relatifs dans le fichier `GET.jsp`, comme indiqué ci-dessous, puis cliquez sur **[!UICONTROL Enregistrer tout]**.

   ```javascript
   <meta http-equiv="refresh" content="0;URL='/lc/apps/ws/index.html'" />
   ```

1. Procédez comme suit pour des personnalisations CSS :

   1. Accédez au dossier `/apps/ws` et créez un nouveau dossier nommé `css`.

   1. Dans le dossier `css`, créez un fichier nommé `newStyle.css`.

   1. Ouvrez `/apps/ws/html`.jsp et changez de

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/jquery-ui.css"/>
   ```

   vers

   ```javascript
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/style.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="css/newStyle.css" />
   <link lang="en" rel="stylesheet" type="text/css" href="../../libs/ws/css/jquery-ui.css"/>
   ```

   >[!NOTE]
   >
   >Placez l’entrée du fichier CSS défini par l’utilisateur après l’entrée de style.css, comme illustré ci-dessus.

1. Dans le fichier /apps/ws/html.jsp, changez

   ```jsp
   <script data-main="js/main" src="js/libs/require/require.js"></script>
   ```

   vers

   ```jsp
   <script data-main="js/main" src="../../libs/ws/js/libs/require/require.js"></script>
   ```

1. Procédez comme suit :

   1. Créez un dossier nommé `js` à `/apps/ws`. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   1. Créez un dossier nommé `libs` à `/apps/ws/js`. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   1. Copiez le dossier `/libs/ws/js/libs/jqueryui` dans `/apps/ws/js/libs`. Cliquez sur **[!UICONTROL Enregistrer tout]**.

1. Procédez comme suit pour des personnalisations HTML :

   1. Sous `/apps/ws/js`, créez un dossier nommé `runtime`. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   1. Sous `/apps/ws/js/runtime`, créez un dossier nommé `templates`. Cliquez sur **[!UICONTROL Enregistrer tout]**.

   1. Copiez `/libs/ws/js/main.js` dans `/apps/ws/js/main.js`.

   1. Copiez /libs/ws/js/registry.js dans `/apps/ws/js/registry.js`.

1. Cliquez sur **[!UICONTROL Enregistrer tout]**, effacez le cache et actualisez l’espace de travail AEM Forms.

   Accédez à l’URL `https://'[server]:[port]'/lc/ws` et connectez-vous avec les informations d’identification d’administrateur/de mot de passe. Le navigateur redirige vers `https://'[server]:[port]'/lc/apps/ws/index.html`.
