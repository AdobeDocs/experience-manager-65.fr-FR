---
title: Configuration de la structure de site web
seo-title: Configuration de la structure de site web
description: Configuration des répertoires
seo-description: Configuration des répertoires
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---

# Configuration de la structure de site Web {#setup-website-structure}

Pour configurer votre site web, les instructions ci-dessous décrivent les dossiers à créer aux emplacements suivants :

* `/apps/an-scf-sandbox`

   C’est là que résident les applications et modèles personnalisés.

* `/etc/designs/an-scf-sandbox`

   C’est là que résident les éléments de conception téléchargeables.

* `/content/an-scf-sandbox`

   C’est là que se trouvent les pages web téléchargeables.

Le code de ce tutoriel repose sur le fait que le nom du dossier principal est le même pour l’application, la conception et le contenu. Si vous choisissez un autre nom pour votre site web, remplacez toujours `an-scf-sandbox` par le nom que vous avez choisi.

>[!NOTE]
>
>À propos des noms :
>
>* Les noms affichés dans CRXDE sont des noms de noeud qui forment le chemin d’accès au contenu adressable.
>* Les noms de noeud peuvent contenir des espaces, mais lorsqu’ils sont utilisés dans un URI, l’espace doit être encodé en &#39;%20&#39; ou &#39;+&#39;.
>* Les noms de noeud peuvent contenir des tirets et des traits de soulignement, mais ils doivent être codés lorsqu’ils sont référencés en tant que nom de module dans un fichier Java. Les tirets et les traits de soulignement sont précédés d’un trait de soulignement suivi de leur valeur Unicode :

   >
   >   
   * Le trait d’union devient &quot;_002d&quot;
   >   * trait de soulignement devient &#39;_005f&#39;


## Configuration du répertoire des applications (/apps) {#setup-the-application-directory-apps}

Le répertoire /apps du référentiel contient le code avec implémente le comportement et le rendu des pages diffusées à partir du répertoire /content .

Le répertoire /apps est protégé et n’est pas accessible publiquement, tout comme les répertoires /content et /etc/designs.

1. Créez le dossier `/apps/an-scf-sandbox` .

   Utilisation de **[!UICONTROL CRXDE Lite]** dans le volet de l’explorateur

   1. Sélectionnez le dossier `/apps` .
   1. Cliquez avec le bouton droit de la souris sur **[!UICONTROL Créer]**... ou appuyez sur **[!UICONTROL Créer...]** .
   1. Sélectionnez **[!UICONTROL Créer un dossier...]**.
   1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez `an-scf-sandbox`.
   1. Cliquez sur **[!UICONTROL OK]**.

1. Créez le sous-dossier **[!UICONTROL components]** .

   1. Sélectionnez le dossier `/apps/an-scf-sandbox` .
   1. Cliquez sur **[!UICONTROL Créer > Créer un dossier]**.
   1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez **[!UICONTROL components]**.
   1. Cliquez sur **[!UICONTROL OK]**.

1. Créez le sous-dossier **[!UICONTROL templates]** .

   1. Sélectionnez le dossier `/apps/an-scf-sandbox` .
   1. Cliquez sur **[!UICONTROL Créer > Créer un dossier]**.
   1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez **[!UICONTROL templates]**.
   1. Cliquez sur **[!UICONTROL OK]**.
   1. Sélectionnez à nouveau `/apps/an-scf-sandbox`.
   1. Sélectionnez **[!UICONTROL Enregistrer tout]**.

   Comme pour tout processus de modification, enregistrez souvent. Si vous rencontrez des problèmes lors de la saisie des données, c’est peut-être parce que votre connexion a expiré ou que vous devez enregistrer les modifications précédentes.

1. La structure du volet d’exploration du CRXDE Lite doit maintenant ressembler à celle-ci :

   ![crxde-template](assets/crxde-template.png)

## Configurer le répertoire de conception (/etc/designs) {#setup-the-design-directory-etc-designs}

Le répertoire /etc/designs contient les images, les scripts et les feuilles de style à télécharger avec le contenu de la page.

1. Pour utiliser l’outil Designer dans l’interface utilisateur classique, accédez à [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Remarque : Si vous utilisez CRXDE Lite pour créer un noeud de type `cq:Page`, le contrôle d’accès et la réplication ne sont pas définis sur les paramètres par défaut d’une page.

1. Dans le volet de l’explorateur, sélectionnez le dossier **[!UICONTROL Conceptions]** , puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**.

   Entrer :

   * Titre : **[!UICONTROL Sandbox SCF]**
   * Nom : **[!UICONTROL an-scf-sandbox]**
   * Sélectionnez **[!UICONTROL Modèle de page de conception]**

   Cliquez sur **[!UICONTROL Créer]**.

   ![design-template](assets/design-template.png)

1. Actualisez le volet d’exploration si le dossier &quot;An SCF Sandbox&quot; n’apparaît pas.

1. Revenez au CRXDE Lite (http:// localhost:4502/crx/de) et développez /etc/designs pour voir le noeud nommé &quot;an-scf-sandbox&quot;.

   Dans le volet inférieur droit de CRXDE, vous pouvez afficher les onglets Propriétés, Contrôle d’accès et Réplication pour voir ce qui a été défini à l’aide du modèle de page de conception.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configuration du répertoire de contenu (/content) {#setup-the-content-directory-content}

Le répertoire /content du référentiel est l’emplacement où réside le contenu du site web. Les chemins sous /content comprennent les chemins d’accès de l’URL pour les requêtes de navigateur.

** Après la création du  [modèle de ](initial-app.md#createthepagetemplate) page dans le cadre de l’application initiale, le contenu initial de la page peut être créé en fonction du modèle....  [**⇒**](initial-app.md)
