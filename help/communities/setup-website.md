---
title: Configurer la structure du site Web
seo-title: Configurer la structure du site Web
description: Configuration des répertoires
seo-description: Configuration des répertoires
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# Configurer la structure du site Web {#setup-website-structure}

Pour configurer votre site Web, les instructions ci-dessous décrivent les dossiers à créer aux emplacements suivants :

* `/apps/an-scf-sandbox`

   C’est là que résident les applications et modèles personnalisés.

* `/etc/designs/an-scf-sandbox`

   C’est ici que résident les éléments de conception téléchargeables.

* `/content/an-scf-sandbox`

   C&#39;est là que résident les pages Web téléchargeables.

Le code de ce didacticiel repose sur le fait que le nom du dossier principal est identique pour l’application, la conception et le contenu. Si vous choisissez un autre nom pour votre site Web, remplacez toujours `an-scf-sandbox` par le nom que vous avez choisi.

>[!NOTE]
>
>A propos des noms :
>
>* Les noms affichés dans CRXDE sont des noms de noeud qui forment le chemin d’accès au contenu adressable.
>* Les noms de noeud peuvent contenir des espaces, mais lorsqu&#39;ils sont utilisés dans un URI, l&#39;espace doit être codé en &quot;%20&quot; ou &quot;+&quot;.
>* Les noms de noeud peuvent contenir des tirets et des traits de soulignement, mais ils doivent être codés lorsqu’ils sont référencés comme nom de package dans un fichier Java. Les tirets et les traits de soulignement sont remplacés par des traits de soulignement suivis de leur valeur Unicode :

   >
   >   
   * trait d&#39;union devient &#39;_002d&#39;
   >   * trait de soulignement devient &#39;_005f&#39;


## Configuration du répertoire d’applications (/apps) {#setup-the-application-directory-apps}

Le répertoire /apps du référentiel contient le code permettant de mettre en oeuvre le comportement et le rendu des pages diffusées à partir du répertoire /content.

Le répertoire /apps est protégé et n’est pas accessible au public, tout comme les répertoires /content et /etc/designs.

1. Créez le dossier `/apps/an-scf-sandbox`.

   Utilisation de **[!UICONTROL CRXDE Lite]** dans le volet d’exploration

   1. Sélectionnez le dossier `/apps`.
   1. Cliquez avec le bouton droit de la souris sur **[!UICONTROL Créer]**... ou appuyez sur **[!UICONTROL Créer...]**.
   1. Sélectionnez **[!UICONTROL Créer un dossier...]**.
   1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez `an-scf-sandbox`.
   1. Cliquez sur **[!UICONTROL OK]**.

1. Créez le sous-dossier **[!UICONTROL components]**.

   1. Sélectionnez le dossier `/apps/an-scf-sandbox`.
   1. Cliquez sur **[!UICONTROL Créer > Créer un dossier]**.
   1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez **[!UICONTROL composants]**.
   1. Cliquez sur **[!UICONTROL OK]**.

1. Créez un sous-dossier **[!UICONTROL templates]**.

   1. Sélectionnez le dossier `/apps/an-scf-sandbox`.
   1. Cliquez sur **[!UICONTROL Créer > Créer un dossier]**.
   1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez **[!UICONTROL templates]**.
   1. Cliquez sur **[!UICONTROL OK]**.
   1. Sélectionnez à nouveau `/apps/an-scf-sandbox`.
   1. Sélectionnez **[!UICONTROL Enregistrer tout]**.

   Comme pour tout processus de modification, économisez souvent. Si vous rencontrez des problèmes lors de la saisie des données, c’est peut-être parce que votre connexion a expiré ou que vous devez enregistrer les modifications précédentes.

1. La structure dans le volet explorateur du CRXDE Lite doit maintenant ressembler à quelque chose comme ceci :

   ![crxde-template](assets/crxde-template.png)

## Configurer le répertoire de conception (/etc/designs) {#setup-the-design-directory-etc-designs}

Le répertoire /etc/designs contient les images, les scripts et les feuilles de style à télécharger avec le contenu de la page.

1. Pour utiliser l’outil Designer dans l’interface utilisateur classique, accédez à [https://&lt;serveur>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Remarque : Si vous utilisez CRXDE Lite pour créer un noeud de type `cq:Page`, le Contrôle d&#39;accès et la réplication ne seront pas définis sur les paramètres par défaut pour une page.

1. Dans le volet explorateur, sélectionnez le dossier **[!UICONTROL Conceptions]**, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**.

   Entrer :

   * Titre : **[!UICONTROL Un sandbox SCF]**
   * Nom : **[!UICONTROL an-scf-sandbox]**
   * Sélectionner **[!UICONTROL Modèle de page de conception]**

   Cliquez sur **[!UICONTROL Créer]**.

   ![design-template](assets/design-template.png)

1. Actualisez le volet explorateur si le dossier &quot;Un sandbox SCF&quot; n&#39;apparaît pas.

1. Revenez au CRXDE Lite (http:// localhost:4502/crx/de) et développez /etc/designs pour voir le noeud nommé &quot;an-scf-sandbox&quot;.

   Dans le volet inférieur droit de CRXDE, vous pouvez vue les onglets Propriétés, Contrôle d&#39;accès et Réplication pour voir ce qui a été défini à l’aide du modèle de page de conception.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configuration du répertoire de contenu (/content) {#setup-the-content-directory-content}

Le répertoire /content du référentiel est l’emplacement où réside le contenu du site Web. Les chemins sous /content comprennent les chemins d’accès de l’URL pour les requêtes du navigateur.

** Après la création du  [modèle de ](initial-app.md#createthepagetemplate) page dans le cadre de l’application initiale, le contenu de la page initiale peut être créé en fonction du modèle....  [**⇒**](initial-app.md)
