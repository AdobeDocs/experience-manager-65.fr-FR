---
title: Contenu initial du sandbox
seo-title: Contenu initial du sandbox
description: Créer le contenu
seo-description: Créer le contenu
uuid: 9810fe47-8d1a-4238-9b9c-0cc47c63d97a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: e8f28cd5-7950-4aab-bf62-3d4ed3d33cbd
translation-type: tm+mt
source-git-commit: c798eb79dc9f8e58cef86cf90af02622c3a2ed78
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 7%

---


# Contenu initial du sandbox {#initial-sandbox-content}

Dans cette section, vous créez les pages suivantes qui utilisent toutes le modèle [de](initial-app.md#createthepagetemplate)page :

* Site SCF Sandbox, qui redirige vers la version anglaise de la page principale.

   * SCF Sandbox - Page principale de la version anglaise du site.

   * SCF Play - Enfant de la page principale sur laquelle jouer.

Bien que ce didacticiel ne s&#39;intéresse pas aux copies [de](../../help/sites-administering/tc-prep.md)langue, il est conçu de sorte que la page racine puisse mettre en oeuvre la détection de la langue préférée par l&#39;utilisateur via l&#39;en-tête HTML et rediriger vers la page principale appropriée pour la langue. La convention consiste à utiliser le code de pays à deux lettres pour le nom de noeud de la page, par exemple &quot;en&quot; pour l’anglais, &quot;fr&quot; pour le français, etc.

## Créer des premières pages {#create-first-pages}

Maintenant qu&#39;il existe un modèle [de](initial-app.md#createthepagetemplate)page, nous pouvons établir la page racine du site Web dans le répertoire /content.

1. L’interface utilisateur standard fournit actuellement des plans pour la création de sites. Comme ce tutoriel crée un site simple, l&#39;interface utilisateur classique est utile.

   Pour passer à l’interface utilisateur classique, sélectionnez une navigation globale et passez la souris sur le côté droit de l’icône Projets. Sélectionnez l’icône *Basculer vers l’interface utilisateur* classique qui s’affiche :

   ![chlimage_1-36](assets/chlimage_1-36.png)

   La possibilité de passer à l’interface utilisateur classique doit être [activée par un administrateur](../../help/sites-administering/enable-classic-ui.md).

1. Dans la page [d’accueil](http://localhost:4502/welcome.html)de l’IU **[!UICONTROL classique, sélectionnez]** Sites Web.

   ![chlimage_1-37](assets/chlimage_1-37.png)

   Vous pouvez également accéder directement à l’interface utilisateur classique des sites Web en accédant à [/siteadmin.](http://localhost:4502/siteadmin)

1. Dans le volet explorateur, sélectionnez **[!UICONTROL Sites Web]** , puis dans la barre d’outils, sélectionnez **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**.

   In the **[!UICONTROL Create Page]** dialog, enter the following:

   * Titre: `SCF Sandbox Site`
   * Nom (name) : `an-scf-sandbox`
   * Sélectionner **[!UICONTROL Un Modèle SCF Sandbox Play]**
   * Cliquez sur **[!UICONTROL Créer]**

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Dans le volet explorateur, sélectionnez la page que vous venez de créer `/Websites/SCF Sandbox Site`, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**:

   * Titre: `SCF Sandbox`
   * Nom (name) : `en`
   * Sélectionner **[!UICONTROL Un Modèle SCF Sandbox Play]**
   * Cliquez sur **[!UICONTROL Créer]**

1. Dans le volet explorateur, sélectionnez la page que vous venez de créer `/Websites/SCF Sandbox Site/SCF Sandbox`, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page.]**

   * Titre: `SCF Play`
   * Nom (name) : `play`
   * Sélectionner **[!UICONTROL Un Modèle SCF Sandbox Play]**
   * Cliquez sur **[!UICONTROL Créer]**

1. C’est ainsi que le site Web s’affiche désormais dans la console Sites Web. Notez que les pages enfants de l&#39;élément sélectionné dans le volet explorateur s&#39;affichent dans le volet de droite où elles peuvent être gérées.

   ![chlimage_1-39](assets/chlimage_1-39.png)

   Il s’agit de la vue de référentiel de ce qui a été créé à l’aide de l’outil Site Web et du modèle :

   ![chlimage_1-40](assets/chlimage_1-40.png)

## Ajouter le chemin de conception {#add-the-design-path}

Lors de la ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` création à l’aide de la section conceptions de la console Outils, la propriété &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

était définie, ce qui permet facultativement de référencer des ressources de conception dans un script utilisant `currentDesign.getPath()`. Par exemple, 

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nom : `cq:designPath`
   * Type : `String`
   * Valeur : `/etc/designs/an-scf-sandbox`

* Cliquez sur le vert `[+] Add`

Le référentiel doit apparaître comme suit :

![chlimage_1-41](assets/chlimage_1-41.png)

* Cliquez sur **[!UICONTROL Enregistrer tout]**

En cas de problème lors de l’enregistrement de la configuration, reconnectez-vous et configurez à nouveau.

>[!NOTE]
>
>L’utilisation de `cq:designPath` est facultative et n’est pas liée à l’ [utilisation de clientlibs](develop-app.md#includeclientlibsintemplate), qui sont essentiellement requis puisque les composants SCF utilisent [clientlibs](client-customize.md#clientlibs-for-scf) pour gérer leurs fichiers JS et CSS.


