---
title: "Didacticiel\_: Créer des modèles"
description: Créer des modèles d’impression et web pour la communication interactive
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 29%

---

# Didacticiel : Créer des modèles{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Ce tutoriel fait partie de la série [Création de votre première communication interactive](/help/forms/using/create-your-first-interactive-communication.md). Il est recommandé de suivre la série par ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du tutoriel.

Pour créer une communication interactive, vous devez disposer de modèles disponibles sur le serveur d’AEM pour les canaux d’impression et web.

Les modèles pour le canal d’impression sont créés dans Adobe Forms Designer et téléchargés sur le serveur AEM. Ces modèles peuvent ensuite être utilisés lors de la création d’une communication interactive.

Les modèles pour le canal web sont créés dans AEM. Les auteurs et les administrateurs de modèles peuvent créer, modifier et activer des modèles web. Une fois créés et activés, ces modèles peuvent être utilisés lors de la création d’une communication interactive.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création de modèles pour les canaux d’impression et web afin qu’ils puissent être utilisés lors de la création de communications interactives. À la fin de ce didacticiel, vous serez capable de :

* Création de modèles XDP pour le canal d’impression à l’aide d’Adobe Forms Designer
* Téléchargement des modèles XDP vers le serveur AEM Forms
* Créer et activer des modèles pour le canal web

## Créer un modèle pour le canal d’impression {#create-template-for-print-channel}

Créez et gérez un modèle pour le canal d’impression de la communication interactive à l’aide des tâches suivantes :

* [Créer un modèle XDP à l’aide de Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Télécharger un modèle XDP sur le serveur AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Création d’un modèle XDP pour les fragments de mise en page](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Créer un modèle XDP à l’aide de Forms Designer {#create-xdp-template-using-forms-designer}

En fonction du [cas d’utilisation](/help/forms/using/create-your-first-interactive-communication.md) et de la [structure](/help/forms/using/planning-interactive-communications.md), créez les sous-formulaires suivants dans le modèle XDP :

* Informations sur la facturation : comprend un fragment de document
* Détails du client : comprend un fragment de document
* Résumé de facturation : comprend un fragment de document
* Résumé : comprend un fragment de document (sous-formulaire Frais) et un graphique (sous-formulaire Graphiques)
* Appels détaillés : comprend un tableau (fragment de disposition)
* Payer maintenant : comprend une image
* Services à valeur ajoutée : comprend une image

![create_print_template](assets/create_print_template.gif)

Ces sous-formulaires s’affichent en tant que zones cible dans le modèle d’impression après le téléchargement du fichier XDP sur le serveur Forms. Toutes les entités telles que les fragments de document, les graphiques, les fragments de mise en page et les images sont ajoutées aux zones cible lors de la création de la communication interactive.

Pour créer un modèle XDP pour le canal d’impression, procédez comme suit :

1. Ouvrez Forms Designer, puis sélectionnez **Fichier** > **Nouveau** > **Utiliser un formulaire vierge,** select **Suivant**, puis sélectionnez **Terminer** pour ouvrir le formulaire à des fins de création de modèle.

   Assurez-vous que les options **Bibliothèque d’objets** et **Objet** sont sélectionnées dans le menu **Fenêtre**.

1. Faites glisser le composant **Sous-formulaire** de la **bibliothèque d’objets** vers le formulaire.
1. Sélectionnez le sous-formulaire pour afficher les options du sous-formulaire dans le **Objet** dans le volet de droite.
1. Sélectionnez l’onglet **Sous-formulaire** et sélectionnez **Distribué** dans la liste déroulante **Contenu**. Pour ajuster la longueur, faites glisser le point de fin gauche du sous-formulaire.
1. Dans l’onglet **Liaisons** :

   1. Spécifiez **billdetails** dans le champ **Nom**.

   1. Sélectionnez **Aucune liaison de données** dans la liste déroulante **Liaison de données**.

   ![Sous-formulaire Designer](assets/forms_designer_subform_new.png)

1. De même, sélectionnez le sous-formulaire racine et l’onglet **Sous-formulaire**, puis sélectionnez **Distribué** dans la liste déroulante **Contenu**. Dans l’onglet **Liaisons** :

   1. Spécifiez **TelecaBill** dans le champ **Nom**.

   1. Sélectionnez **Aucune liaison de données** dans la liste déroulante **Liaison de données**.

   ![Sous-formulaire pour le modèle dʼimpression](assets/root_subform_print_template_new.png)

1. Répétez les étapes 2 à 5 pour créer les sous-formulaires suivants :

   * BillDetails
   * CustomerDetails
   * BillSummary
   * Résumé : sélectionnez l’onglet **Sous-formulaire**, puis **Positionné** dans la liste déroulante **Contenu** de ce sous-formulaire. Insérez les sous-formulaires suivants dans le **Résumé** sous-formulaire.

      * Frais
      * Graphiques

   * ItemizedCalls
   * PayNow
   * ValueAddedServices

   Pour gagner du temps, vous pouvez également copier et coller des sous-formulaires existants pour créer d’autres sous-formulaires.

   Pour changer la variable **Graphiques** Sélectionnez le sous-formulaire situé à droite du sous-formulaire Frais . **Graphiques** dans le volet de gauche, sélectionnez le sous-formulaire **Disposition** et indiquez une valeur pour la variable **AncreX** champ . La valeur doit être supérieure à la valeur du champ **Largeur** pour le sous-formulaire **Frais**. Sélectionnez la variable **Frais** et sélectionnez le sous-formulaire **Disposition** pour afficher la valeur de la variable **Largeur** champ .

1. Faites glisser l’objet **Texte** de la **bibliothèque d’objets** vers le formulaire et saisissez le texte **Composez le XXXX pour vous abonner** dans la zone.
1. Cliquez avec le bouton droit de la souris sur l’objet texte dans le volet de gauche, sélectionnez **Renommer l’objet** et saisissez le nom de l’objet texte **S’abonner**.

   ![Modèle XDP](assets/print_xdp_template_subform_new.png)

1. Sélectionnez **Fichier** > **Enregistrer sous** pour enregistrer le fichier sur le système de fichiers local :

   1. Accédez à l’emplacement où vous pouvez enregistrer le fichier et indiquez le nom en tant que **create_first_ic_print_template**.
   1. Sélectionner **.xdp** de la **Enregistrer en tant que type** liste déroulante.

   1. Sélectionnez **Enregistrer**.

### Télécharger un modèle XDP sur le serveur AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Une fois que vous avez créé un modèle XDP à l’aide de Forms Designer, vous devez le charger sur le serveur AEM Forms afin qu’il soit disponible lors de la création de la communication interactive.

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionner **Créer** > **Téléchargement du fichier**.

   Naviguez et sélectionnez le **create_first_ic_print_template** template (XDP) et select **Ouvrir** pour importer le modèle XDP sur le serveur AEM Forms.

### Création d’un modèle XDP pour les fragments de mise en page {#create-xdp-template-for-layout-fragments}

Pour créer un fragment de mise en page pour le canal d’impression de la communication interactive, créez un fichier XDP à l’aide de Forms Designer et téléchargez-le sur le serveur AEM Forms.

1. Ouvrez Forms Designer, puis sélectionnez **Fichier** > **Nouveau** > **Utiliser un formulaire vierge,** select **Suivant**, puis sélectionnez **Terminer** pour ouvrir le formulaire à des fins de création de modèle.

   Assurez-vous que les options **Bibliothèque d’objets** et **Objet** sont sélectionnées dans le menu **Fenêtre**.

1. Faites glisser le composant **Tableau** de la **bibliothèque d’objets** vers le formulaire.
1. Dans la boîte de dialogue Insérer un tableau :

   1. Indiquez le nombre de colonnes sous la forme **5**.
   1. Spécifiez le nombre de rangées de contenu sous la forme **1**.
   1. Sélectionnez la variable **Inclure la rangée d’en-tête dans le tableau** .
   1. Onglet **OK**.

1. Sélectionner **+** dans le volet de gauche en regard de **Tableau** 1 et clic droit **Cell1** et sélectionnez **Rename Object** to **Date**.

   De même, renommez **Cell2**, **Cell3**, **Cell4**, et **Cellule5** to **Heure**, **Nombre**, **Durée**, et **Frais** respectivement.

1. Cliquez sur les champs de texte d’en-tête dans l’**affichage Designer** et renommez-les comme suit : **Heure**, **Numéro**, **Durée** et **Frais**.

   ![Fragment de mise en page](assets/layout_fragment_print_new.png)

1. Sélectionnez **Rangée 1** dans le volet gauche et sélectionnez **Objet** > **Liaison** > **Rangée pour chaque élément**.

   ![Répétition des propriétés pour le fragment de disposition](assets/layout_fragment_print_repeat_new.png)

1. Faites glisser le composant **Champ de texte** de la **bibliothèque d’objets** vers l’**affichage Designer**.

   ![Champ de texte pour le fragment de disposition](assets/layout_fragment_print_text_field_new.png)

   De même, faites glisser et déposez le **Champ de texte** au composant **Heure**, **Nombre**, **Durée**, et **Frais** lignes.

1. Sélectionnez **Fichier** > **Enregistrer sous** pour enregistrer le fichier sur le système de fichiers local :

   1. Accédez à l’emplacement où vous pouvez enregistrer le fichier et indiquez le nom en tant que **table_lf**.
   1. Sélectionner **.xdp** de la **Enregistrer en tant que type** liste déroulante.

   1. Sélectionnez **Enregistrer**.

   Une fois que vous avez créé un modèle XDP pour le fragment de mise en page à l’aide de Forms Designer, vous devez [charger](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) sur le serveur AEM Forms afin que le modèle puisse être utilisé lors de la création de fragments de mise en page.

## Créer un modèle pour le canal web {#create-template-for-web-channel}

Créez et gérez un modèle pour le canal web de la communication interactive à l’aide des tâches suivantes :

* [Créer un dossier pour les modèles](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Créer le modèle](../../forms/using/create-templates-print-web.md#create-the-template)
* [Activer le modèle](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Activer les boutons dans les communications interactives](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Création d’un dossier pour les modèles {#create-folder-for-templates}

Pour créer un modèle de canal web, définissez un dossier dans lequel vous pourrez enregistrer les modèles créés. Une fois que vous avez créé un modèle dans ce dossier, activez-le pour permettre aux utilisateurs de formulaires de créer un canal web d’une communication interactive basée sur le modèle.

Pour créer un dossier pour les modèles modifiables, procédez comme suit :

1. Sélectionner **Outils** ![icône en forme de marteau](assets/hammer-icon.svg) > **Explorateur de configuration**.
   * Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).
1. Dans la page du navigateur de configuration, sélectionnez **Créer**.
1. Dans le **Créer une configuration** dialog, spécifiez **Create_First_IC_templates** comme titre du dossier, cochez **Modèles modifiables**, puis sélectionnez **Créer**.

   ![Configurer des modèles web](assets/create_first_ic_web_template_new.png)

   Le dossier **Create_First_IC_templates** est créé et répertorié sur la page du **navigateur de configuration**.

### Créer le modèle {#create-the-template}

En fonction du [cas d’utilisation](/help/forms/using/create-your-first-interactive-communication.md) et de la [structure](/help/forms/using/planning-interactive-communications.md), créez les panneaux suivants dans le modèle web :

* Informations sur la facturation : comprend un fragment de document
* Détails du client : comprend un fragment de document
* Résumé de facturation : comprend un fragment de document
* Résumé des frais : comprend un fragment de document et un graphique (mise en page à deux colonnes)
* Appels détaillés : comprend un tableau
* Payer maintenant : comprend un bouton et une image **Payer maintenant**
* Services à valeur ajoutée : comprend un bouton et une image **S’abonner**.

![create_web_template](assets/create_web_template.gif)

Toutes les entités telles que les fragments de document, les graphiques, les tableaux, les images et les boutons sont ajoutées lors de la création de la communication interactive.

Pour créer un modèle pour le canal web dans le **Create_First_IC_templates** procédez comme suit :

1. Accédez au dossier de modèle approprié en sélectionnant **Outils** > **Modèles** > **Create_First_IC_templates** dossier.
1. Sélectionnez **Créer**.
1. Sur le **Sélection d’un type de modèle** assistant de configuration, sélectionnez **Communication interactive - Canal web** et sélectionnez **Suivant**.
1. Dans l’assistant de configuration **Détails du modèle**, spécifiez comme titre pour le modèle **Create_First_IC_Web_Template**. Spécifiez une description facultative et sélectionnez **Créer**.

   Un message de confirmation indiquant que **Create_First_IC_Web_Template** sʼaffiche.

1. Sélectionner **Ouvrir** pour ouvrir le modèle dans l’éditeur de modèles.
1. Sélectionner **Contenu initial** dans la liste déroulante en regard de la fonction **Aperçu** .

   ![Éditeur de modèles](assets/template_editor_initial_content_new.png)

1. Sélectionner **Panneau racine** puis sélectionnez **+** pour afficher la liste des composants à ajouter au modèle.
1. Pour ajouter un panneau au-dessus du panneau **Panneau racine**, sélectionnez **Panneau** dans la liste.
1. Sélectionnez la variable **Contenu** dans le volet de gauche. Le nouveau panneau ajouté à l’étape 8 s’affiche sous le **Panneau racine** dans l’arborescence de contenu.

   ![Arborescence de contenu](assets/content_tree_root_panel_new.png)

1. Sélectionnez le panneau, puis sélectionnez ![configure_icon](assets/configure_icon.png) (Configuration).
1. Dans le volet Propriétés :

   1. Spécifier **billdetails** dans le champ Nom .
   1. Spécifier **Informations de facturation** dans le champ Titre .
   1. Sélectionner **1** de la **Nombre de colonnes** liste déroulante.

   1. Pour enregistrer les propriétés, sélectionnez ![Enregistrer](/help/forms/using/assets/done_icon.png).

   Le nom du panneau est mis à jour pour **Informations de facturation** dans l’arborescence de contenu.

1. Répétez les étapes 7 à 11 pour ajouter des panneaux avec les propriétés suivantes au modèle :

   | Nom | Titre | Nombre de colonnes |
   |---|---|---|
   | customerdetails | Détails du client | 1 |
   | billsummary | Résumé de facturation | 1 |
   | summarycharges | Récapitulatif des frais | 2 |
   | itemisedcalls | Appels détaillés | 1 |
   | paynow | Payer maintenant | 2 |
   | zone | Services à valeur ajoutée | 1 |

   L’image suivante illustre l’arborescence de contenu après l’ajout de tous les panneaux au modèle :

   ![Arborescence de contenu pour tous les panneaux](assets/content_tree_all_panels_new.png)

### Activer le modèle {#enable-the-template}

Une fois que vous avez créé le modèle Web, vous devez l&#39;activer pour l&#39;utiliser lors de la création de la communication interactive.

Pour activer le modèle Web, procédez comme suit :

1. Sélectionner **Outils** ![icône en forme de marteau](assets/hammer-icon.svg) > **Modèles**.
1. Accédez au **Create_First_IC_Web_Template** modèle, sélectionnez-le, puis sélectionnez **Activer**.
1. Sélectionner **Activer** pour confirmer.

   Le modèle est activé et son état s’affiche comme Activé. Vous pouvez utiliser ce modèle lors de la création de la communication interactive pour le canal web.

### Activer les boutons dans les communications interactives {#enabling-buttons-in-interactive-communications}

En fonction du cas d’utilisation, vous devez inclure la variable **Payer maintenant** et **Abonner** des boutons (composants de formulaires adaptatifs) dans la communication interactive. Pour activer l’utilisation de ces boutons dans la communication interactive, procédez comme suit :

1. Sélectionnez **Structure** dans la liste déroulante en regard de l’option **Prévisualisation**.
1. Sélectionnez la variable **Conteneur de documents** panneau racine à l’aide de l’arborescence de contenu et sélectionnez **Stratégie** pour sélectionner les composants autorisés à être utilisés dans la communication interactive.

   ![Configuration de la politique](assets/structure_configure_policy_new.png)

1. Dans le **Composants autorisés** de la **Propriétés** , sélectionnez **Bouton** de la **Formulaire adaptatif** composants.

   ![Composants autorisés](assets/allowed_components_af_new.png)

1. Pour enregistrer les propriétés, sélectionnez ![save](assets/done_icon.png).
