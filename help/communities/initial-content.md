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
source-git-commit: 85f3b8f2a5f079954f4907037c1c722a6b25fd91

---


# Contenu initial du sandbox {#initial-sandbox-content}

Dans cette section, vous créez les pages suivantes qui utilisent toutes le modèle [de](initial-app.md#createthepagetemplate)page :

* Site de Sandbox SCF, qui redirigera vers la version anglaise de la page principale.

   * SCF Sandbox - Page principale de la version anglaise du site.

      * SCF Play - Enfant de la page principale sur laquelle jouer.

Bien que ce didacticiel ne s’intéresse pas aux copies [de](../../help/sites-administering/tc-prep.md)langue, il est conçu de sorte que la page racine puisse implémenter la détection de la langue préférée par l’utilisateur via l’en-tête HTML et rediriger vers la page principale appropriée pour la langue. La convention consiste à utiliser le code pays à deux lettres pour le nom de noeud de la page, par exemple &quot;en&quot; pour l’anglais, &quot;fr&quot; pour le français, etc.

## Créer des premières pages {#create-first-pages}

Maintenant qu&#39;il existe un modèle [de](initial-app.md#createthepagetemplate)page, nous pouvons établir la page racine du site Web dans le répertoire /content.

1. L’interface utilisateur standard fournit actuellement des plans pour la création de sites. Comme ce didacticiel crée un site simple, l’interface utilisateur classique est utile.

   Pour passer à l’interface utilisateur classique, sélectionnez la navigation globale et passez la souris sur le côté droit de l’icône Projets. Sélectionnez l’icône *Passer à l’interface utilisateur* classique qui s’affiche :

   ![chlimage_1-36](assets/chlimage_1-36.png)

   La possibilité de passer à l’interface utilisateur classique doit être [activée par un administrateur](../../help/sites-administering/enable-classic-ui.md).

1. Dans la page [d’accueil](http://localhost:4502/welcome.html)classique de l’interface utilisateur, sélectionnez **[!UICONTROL Sites]** Web.

   ![chlimage_1-37](assets/chlimage_1-37.png)

   Vous pouvez également accéder directement à l’interface utilisateur classique des sites Web en accédant à [/siteadmin.](http://localhost:4502/siteadmin)

1. Dans le volet de l’explorateur, sélectionnez **[!UICONTROL Sites]** Web, puis dans la barre d’outils, sélectionnez **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**.

   In the **[!UICONTROL Create Page]** dialog, enter the following:

   * Titre: `SCF Sandbox Site`
   * Nom: `an-scf-sandbox`
   * Sélectionner **[!UICONTROL Un Modèle De Lecture Sandbox SCF]**
   * Cliquez sur **[!UICONTROL Créer]**
   ![chlimage_1-38](assets/chlimage_1-38.png)

1. Dans le volet de l’explorateur, sélectionnez la page que vous venez de créer `/Websites/SCF Sandbox Site`, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**:

   * Titre: `SCF Sandbox`
   * Nom: `en`
   * Sélectionner **Un Modèle De Lecture Sandbox SCF **
   * Cliquez sur **Créer **

1. Dans le volet de l’explorateur, sélectionnez la page que vous venez de créer `/Websites/SCF Sandbox Site/SCF Sandbox`, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page.]**

   * Titre: `SCF Play`
   * Nom: `play`
   * Sélectionner **[!UICONTROL Un Modèle De Lecture Sandbox SCF]**
   * Cliquez sur **[!UICONTROL Créer]**

1. C’est ainsi que le site Web s’affiche désormais dans la console Sites Web. Notez que les pages enfants de l’élément sélectionné dans le volet d’exploration s’affichent dans le volet de droite, où elles peuvent être gérées.

   ![chlimage_1-39](assets/chlimage_1-39.png)

   Il s’agit du  de référentiel de ce qui a été créé à l’aide de l’outil Site Web et du modèle :

   ![chlimage_1-40](assets/chlimage_1-40.png)

## Ajouter le chemin de conception {#add-the-design-path}

Lors de la ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` création à l’aide de la section conceptions de la console Outils, la propriété &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

était définie, ce qui permet facultativement de référencer des ressources de conception dans un script à l’aide de `currentDesign.getPath()`. Par exemple

* &lt;% StringIcon = currentDesign.getPath() + &quot;/favicon.ico&quot;; %>


   * Nom: `cq:designPath`
   * Type: `String`
   * Valeur: `/etc/designs/an-scf-sandbox`

* Cliquez sur le vert `[+] Add`

Le référentiel doit se présenter comme suit :

![chlimage_1-41](assets/chlimage_1-41.png)

* Cliquez sur **[!UICONTROL Enregistrer tout]**

[ Des problèmes d&#39;épargne ? Connectez-vous à nouveau ! ]

>[!NOTE]
>
>L’utilisation de cq:designPath est facultative et n’est pas liée à l’ [utilisation de clientlibs](develop-app.md#includeclientlibsintemplate), qui sont essentiellement requises puisque les composants SCF utilisent [clientlibs](client-customize.md#clientlibs-for-scf) pour gérer leurs fichiers JS et CSS.


