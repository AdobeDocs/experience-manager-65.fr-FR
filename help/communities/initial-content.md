---
title: Contenu d’environnement de test initial
description: Découvrez comment utiliser le modèle Page dans l’environnement de test pour créer une page principale pour une version anglaise d’un site web et une page enfant de la page principale.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 068a0fff-ca48-4847-ba3f-d78416c97f6d
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 3%

---

# Contenu d’environnement de test initial {#initial-sandbox-content}

Dans cette section, vous créez les pages suivantes qui utilisent toutes le [modèle de page](initial-app.md#createthepagetemplate) :

* SCF Sandbox Site, qui redirige vers la version anglaise de la page principale.

   * Environnement de test SCF : page principale de la version anglaise du site.

   * Lecture SCF - Enfant de la page principale sur laquelle lire.

Ce tutoriel ne décrit pas les [copies de langue](../../help/sites-administering/tc-prep.md). Il est conçu de sorte que la page racine puisse mettre en oeuvre la détection de la langue souhaitée pour l’utilisateur par le biais de l’en-tête de l’HTML et rediriger vers la page principale appropriée pour la langue. La convention consiste à utiliser le code de pays à deux lettres pour le nom de noeud de la page, par exemple &quot;en&quot; pour l’anglais et &quot;fr&quot; pour le français.

## Créer les premières pages {#create-first-pages}

Maintenant qu’il existe un [modèle de page](initial-app.md#createthepagetemplate), vous pouvez établir la page racine du site web dans le répertoire /content.

1. L’interface utilisateur standard fournit actuellement des plans directeurs pour la création de sites. Comme ce tutoriel crée un site simple, l’IU classique est utile.

   Pour passer à l’IU classique, sélectionnez la navigation globale et survolez le côté droit de l’icône Projets . Sélectionnez l’icône *Passer à l’IU classique* qui s’affiche :

   ![classic-ui](assets/classic-ui.png)

   La possibilité de passer à l’IU classique doit être [ activée par un administrateur](../../help/sites-administering/enable-classic-ui.md).

1. Sur la [page d’accueil classique de l’interface utilisateur](http://localhost:4502/welcome.html), sélectionnez **[!UICONTROL Sites web]**.

   ![classic-ui-website](assets/classic-ui-website.png)

   Vous pouvez également accéder directement à l’IU classique pour les sites web en accédant à [/siteadmin.](http://localhost:4502/siteadmin)

1. Dans le volet de l’explorateur, sélectionnez **[!UICONTROL Sites Web]**, puis, dans la barre d’outils, sélectionnez **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**.

   Dans la boîte de dialogue **[!UICONTROL Créer une page]**, saisissez ce qui suit :

   * Titre : `SCF Sandbox Site`
   * Nom : `an-scf-sandbox`
   * Sélectionnez **[!UICONTROL Un Modèle SCF Sandbox Play]**
   * Cliquez sur **[!UICONTROL Créer]**.

   ![classic-ui-create-page](assets/classic-ui-create-page.png)

1. Dans le volet de l’explorateur, sélectionnez la page que vous avez créée, `/Websites/SCF Sandbox Site`, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]** :

   * Titre : `SCF Sandbox`
   * Nom : `en`
   * Sélectionnez **[!UICONTROL Un Modèle SCF Sandbox Play]**
   * Cliquez sur **[!UICONTROL Créer]**.

1. Dans le volet de l’explorateur, sélectionnez la page que vous avez créée, `/Websites/SCF Sandbox Site/SCF Sandbox`, puis cliquez sur **[!UICONTROL Nouveau]** > **[!UICONTROL Nouvelle page]**

   * Titre : `SCF Play`
   * Nom : `play`
   * Sélectionnez **[!UICONTROL Un Modèle SCF Sandbox Play]**
   * Cliquez sur **[!UICONTROL Créer]**.

1. C’est ainsi que le site web s’affiche désormais dans la console Sites web . Notez que les pages enfants de l’élément sélectionné dans le volet de l’explorateur s’affichent dans le volet de droite où elles peuvent être gérées.

   ![classic-ui-website-page](assets/classic-ui-website-page.png)

   Il s’agit de la vue référentiel de ce qui a été créé à l’aide de l’outil Site Web et du modèle :

   ![classic-ui-repository-view](assets/classic-ui-repository-view.png)

## Ajout du chemin de conception {#add-the-design-path}

Lorsque ` [/etc/designs/an-scf-sandbox](setup-website.md#setupthedesigntreeetcdesigns)` a été créé à l’aide de la section conceptions de la console Outils, la propriété &quot;

* `cq:template="/libs/wcm/core/templates/designpage"`

A été défini, ce qui offre la possibilité facultative de référencer des ressources de conception dans un script à l’aide de `currentDesign.getPath()`. par exemple,

* `% String favIcon = currentDesign.getPath() + "/favicon.ico"; %`


   * Nom : `cq:designPath`
   * Type : `String`
   * Valeur : `/etc/designs/an-scf-sandbox`

* Cliquez sur le vert `[+] Add`

Le référentiel doit apparaître comme suit :

![classic-ui-repository-path](assets/classic-ui-repository-path.png)

* Cliquez sur **[!UICONTROL Enregistrer tout]**

Si vous rencontrez des problèmes lors de l’enregistrement de la configuration, reconnectez-vous et configurez à nouveau.

>[!NOTE]
>
>L’utilisation de `cq:designPath` est facultative et n’est pas liée à l’ [utilisation de clientlibs](develop-app.md#includeclientlibsintemplate), qui sont requises car les composants SCF utilisent [clientlibs](client-customize.md#clientlibs-for-scf) pour gérer leurs JS et CSS.
