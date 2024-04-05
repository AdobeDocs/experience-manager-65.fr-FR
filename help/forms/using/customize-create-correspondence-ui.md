---
title: Personnaliser l’interface utilisateur de création de correspondance
description: Découvrez comment personnaliser une interface utilisateur (IU) de correspondance telle que le logo dans l’environnement AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 100%

---

# Personnaliser l’interface de création de correspondance{#customize-create-correspondence-ui}

## Présentation {#overview}

Correspondence Management vous permet d’adapter le modèle de solution à l’identité graphique de votre société afin de conserver la valorisation de votre marque. Le changement d’identité graphique de l’interface utilisateur comprend la modification du logo de la société, qui est affiché dans le coin supérieur gauche de l’interface utilisateur de création de correspondance.

Vous pouvez changer le logo dans l’interface utilisateur de création de correspondance pour le remplacer par le logo de votre entreprise.

![L’icône personnalisée dans l’interface utilisateur de création de correspondance](assets/0_1_introscreenshot.png)

L’icône personnalisée dans l’interface utilisateur de création de correspondance

### Modification du logo dans l’interface utilisateur de création de correspondance {#changing-the-logo-in-the-create-correspondence-ui}

Pour configurer une image de logo de votre choix, procédez comme suit :

1. Créez la [structure de dossier appropriée dans CRX](#creatingfolderstructure).
1. [Chargez le fichier du nouveau logo](#uploadlogo) dans le dossier que vous avez créé dans CRX.

1. [Configurez le CSS](#createcss) de CRX pour faire référence au nouveau logo.
1. Effacez l’historique du navigateur, puis [actualisez l’interface utilisateur Créer une correspondance](#refreshccrui).

## Création de la structure de dossiers requise {#creatingfolderstructure}

Créez la structure de dossiers, comme expliqué ci-dessous, pour héberger l’image de logo et la feuille de style personnalisées. La nouvelle structure de dossiers avec le dossier racine/apps est similaire à la structure du dossier /libs.

Pour toute personnalisation, créez une structure de dossiers parallèle, comme expliqué ci-dessous, dans la branche /apps.

La branche `/apps` (structure de dossiers) :

* Garantit que vos fichiers sont sûrs en cas de mise à jour du système. En cas de mise à niveau d’un pack de fonctionnalités ou d’un correctif, la branche `/libs` est mise à jour et si vous hébergez vos modifications dans la branche `/libs`, elles sont écrasées.
* Vous aide à ne pas toucher au système/à la branche actuels, que vous pouvez ébranler par erreur si vous utilisez les emplacements par défaut pour enregistrer les fichiers personnalisés.
* Permet à vos ressources d’obtenir une priorité plus élevée lorsqu’AEM recherche des ressources. AEM est configuré pour rechercher une ressource d’abord dans la branche `/apps` puis dans la branche `/libs`. Ce mécanisme signifie que le système utilise votre recouvrement (et les personnalisations qui y sont définies).

Suivez les étapes ci-dessous pour créer la structure de dossiers requise dans la branche `/apps` :

1. Accédez à `https://'[server]:[port]'/[ContextPath]/crx/de` et connectez-vous en tant qu’administrateur ou administratrice.
1. Dans le dossier des applications, créez un dossier nommé `css` dont le chemin d’accès/la structure est similaire au dossier css (situé dans le dossier ccrui).

   Marche à suivre pour créer le dossier css :

   1. Cliquez avec le bouton droit sur le dossier **css** à l’emplacement suivant et sélectionnez **Nœud de recouvrement** : `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![Nœud de recouvrement](assets/1_overlaynode_css.png)

   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin:** `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      **Emplacement du recouvrement:** `/apps/`

      **Correspondance des types de nœuds :** vérifié.

      ![Chemin d’accès au nœud de recouvrement](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >Ne modifiez pas la branche `/libs`. Toute modification que vous apportez peut être perdue, car cette branche est sujette à des modifications lorsque vous :
      >
      >    
      >    
      >    * Effectuez une mise à niveau sur votre instance.
      >    * Appliquez un correctif.
      >    * Installez un pack de fonctionnalités.
      >    
      >

   1. Cliquez sur **OK**. Le dossier CSS est créé au niveau du chemin d’accès indiqué.

1. Dans le dossier des applications, créez un dossier nommé `imgs` dont le chemin d’accès/la structure est similaire au dossier `imgs` (situé dans le dossier ccrui).

   1. Cliquez avec le bouton droit sur le dossier **imgs** dans le chemin d’accès suivant et sélectionnez **Nœud de recouvrement** : `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. Assurez-vous que la boîte de dialogue du nœud de recouvrement possède les valeurs suivantes :

      **Chemin d’accès :** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **Emplacement du recouvrement :** /apps/

      **Respect des types de nœud :** activé

   1. Cliquez sur **OK**.

      >[!NOTE]
      >
      >Vous pouvez également créer manuellement la structure de dossiers dans le dossier /apps.

1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications sur le serveur.

## Télécharger le nouveau logo dans CRX {#uploadlogo}

Téléchargez votre fichier de logo personnalisé dans CRX. Les règles HTML standard régissent le rendu du logo. Les formats de fichiers image pris en charge le sont selon le navigateur utilisé pour accéder à AEM Forms. Tous les navigateurs prennent en charge les formats JPEG, GIF et PNG. Pour en savoir plus, reportez-vous à la documentation du navigateur sur les formats d’image pris en charge.

* Les dimensions par défaut de l’image de logo sont 48 px &#42; 48 px. Assurez-vous que l’image est de cette taille ou d’une taille supérieure à 48 px &#42; 48 px.
* Si la hauteur de l’image de logo est de plus de 50 px, l’interface utilisateur de création de correspondance réduit l’image à une hauteur maximale de 50 px, car il s’agit de la hauteur de l’en-tête. Lors de la réduction de l’image, l’interface utilisateur de création de correspondance conserve les proportions de votre image.
* L’interface utilisateur de création de correspondance n’agrandit pas votre image si elle est petite. Vous devez donc vous assurer que vous utilisez une image de logo d’au moins 48 px de haut et d’une largeur suffisante pour la clarté.

Suivez les étapes ci-dessous pour télécharger le fichier du logo personnalisé dans CRX :

1. Accédez à `https://'[server]:[port]'/[contextpath]/crx/de`. Le cas échéant, connectez-vous en tant qu’administrateur.
1. Dans CRXDE, faites un clic droit sur le dossier **imgs** au niveau du chemin d’accès suivant et sélectionez **Créer > Créer un fichier** :

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![Créer un nouveau nœud dans le dossier imgs](assets/2_contentexplorernewnode.png)

1. Dans la boîte de dialogue Créer un fichier, entrez le nom du fichier au format CustomLogo.png (ou le nom de fichier de votre logo).

   ![CustomLogo.png en tant que nouveau nœud](assets/3_contentexplorernewnode_customlogo.png)

1. Cliquez sur **Enregistrer tout**.

   Dans le nouveau fichier que vous avez créé (ici CustomLogo.png), la propriété jcr:content s’affiche.

1. Cliquez sur jcr:content dans la structure de dossiers.

   Les propriétés de jcr:content s’affichent.

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. Double-cliquez sur la propriété **jcr:data**.

   La boîte de dialogue Edit jcr:data s’affiche.

   Cliquez maintenant sur le dossier newlogo.png, puis double-cliquez sur jcr:content (option dim) et définissez le type nt:resource. Dans le cas contraire, créer une propriété du nom de jcr:content.

1. Dans la boîte de dialogue Edit jcr:data, cliquez sur **Parcourir** et sélectionnez le fichier image que vous souhaitez utiliser comme logo (ici, CustomLogo.png).

   Les formats de fichiers image pris en charge le sont selon le navigateur utilisé pour accéder à AEM Forms. Tous les navigateurs prennent en charge les formats JPEG, GIF et PNG. Pour en savoir plus, reportez-vous à la documentation du navigateur sur les formats d’image pris en charge.

   ![Exemple de fichier de logo personnalisé](assets/geometrixx-outdoors.png)

   Exemple : CustomLogo.png à utiliser comme logo personnalisé

1. Cliquez sur **Enregistrer tout**.

## Créer le CSS pour intégrer le logo à l’interface utilisateur {#createcss}

L’image de logo nécessite une feuille de style supplémentaire à charger dans le contexte du contenu.

Effectuez les étapes suivantes pour créer la feuille de style pour le rendu du logo avec l’interface utilisateur :

1. Accédez à `https://'[server]:[port]'/[contextpath]/crx/de`. Le cas échéant, connectez-vous en tant qu’administrateur.
1. Créez un fichier appelé customcss.css (vous ne pouvez pas utiliser de nom différent) à l’emplacement suivant :

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   Procédure à suivre pour créer le fichier customcss.css :

   1. Faites un clic droit sur le dossier **css** et sélectionnez **Créer > Créer un fichier**.
   1. Dans la boîte de dialogue Nouveau fichier, indiquez le nom du CSS comme `customcss.css`(vous ne pouvez pas utiliser de nom différent), puis cliquez sur **OK**.
   1. Ajoutez le code suivant dans le fichier CSS que vous venez de créer. Dans la partie content:url du code, indiquez le nom de l’image que vous avez téléchargée dans le dossier imgs dans CRXDE.

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. Cliquez sur **Enregistrer tout**.

## Actualiser l’interface utilisateur de création de correspondance pour voir le logo personnalisé {#refreshccrui}

Effacez le cache du navigateur, puis ouvrez l’instance de l’interface utilisateur de création de correspondance dans votre navigateur afin de voir votre logo personnalisé.

![Interface utilisateur de création de correspondance avec un logo personnalisé](assets/0_1_introscreenshot-1.png)

L’icône personnalisée dans l’interface utilisateur de création de correspondance
