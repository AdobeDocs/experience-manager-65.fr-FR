---
title: '"Didacticiel : Créer une communication interactive "'
seo-title: Create an Interactive Communication for Print and Web
description: Créer une communication interactive en utilisant tous les blocs de construction
seo-description: Create an Interactive Communication using all building blocks
uuid: 5ffaa86f-87c7-4673-8b41-63ec61421be2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ac5d8d4f-fc13-4e8d-819c-c5db07fa6870
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 100%

---

# Didacticiel : Créer une communication interactive {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Ce tutoriel fait partie de la série [Création de votre première communication interactive](/help/forms/using/create-your-first-interactive-communication.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

Une fois que vous avez créé tous les blocs de construction, tels que le modèle de données de formulaire, les fragments de document, les modèles et les thèmes pour la version web, vous pouvez commencer à créer une communication interactive.

Les communications interactives peuvent être fournies par deux canaux : impression et web. Vous pouvez également créer une communication interactive en configurant le canal d’impression comme option principale. L’impression comme option principale pour le canal web garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression. Elle garantit également que les modifications apportées dans le canal d’impression sont synchronisées dans le canal web. Les auteurs de communication interactive sont toutefois autorisés à interrompre l’héritage pour des composants spécifiques dans le canal web.

Ce didacticiel vous guide pas à pas dans la création de communications interactives pour les canaux d’impression et web. À la fin de ce didacticiel, vous serez capable de :

* Créer une communication interactive pour le canal d’impression
* Créer une communication interactive pour le canal web
* Créer des communications interactives pour les versions impression et web avec l’impression comme option principale

## Créer des communications interactives pour les versions impression et web sans aucune synchronisation {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Créer une communication interactive pour le canal d’impression {#create-interactive-communication-for-print-channel}

Voici la liste des ressources qui ont déjà été créées dans ce didacticiel et qui sont nécessaires à la création de la communication interactive pour le canal d’impression :

**Modèle d’impression :** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modèle de données de formulaire :** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragments de document :** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**Fragments de mise en page :** [table_lf](../../forms/using/create-templates-print-web.md)

**Images :** PayNow et ValueAddedServices

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Appuyez sur **Créer** et sélectionnez **Communication interactive**. L’assistant **Créer une communication interactive** s’affiche.
1. Spécifiez **create_first_ic** dans les champs **Titre** et **Nom**. Sélectionnez **FDM_Create_First_IC** comme modèle de données de formulaire et appuyez sur **Suivant**.
1. Dans l’assistant **Canaux** :

   1. Spécifiez **create_first_ic_print_template** comme modèle d’impression et appuyez sur **Sélectionner**. Assurez-vous que la case **Utiliser l’impression en tant que page principale pour le canal web** n’est pas cochée.

   1. Spécifiez le dossier **Create_First_IC_templates** > **Create_First_IC_Web_Template** en tant que modèle web et appuyez sur **Sélectionner**.

   1. Appuyez sur **Créer**.

   Un message de confirmation s’affiche pour confirmer que la communication interactive a été créée correctement.

1. Appuyez sur **Modifier** pour ouvrir la communication interactive dans le volet droit.
1. Accédez à l’onglet **Ressources** et appliquez le filtre pour afficher uniquement les fragments de document dans le volet gauche.
1. Faites glisser les fragments de documents suivants vers leurs zones cibles dans la communication interactive :

   | Fragment de document | Zone cible |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | Frais |

   ![Fragments de document pour les communications interactives](assets/create_first_ic_doc_fragments_new.png)

1. Appuyez sur **Graphiques** dans la zone cible et appuyez sur **+** pour ajouter un composant **Graphique.**
1. Appuyez sur le composant Graphique et sélectionnez ![configure_icon](assets/configure_icon.png) (Configurer). Les propriétés du graphique s’affichent dans le volet gauche :

   1. Spécifiez un nom pour le diagramme.
   1. Sélectionnez **Diagramme circulaire** dans la liste déroulante **Type de graphique**.
   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Calls** dans la section **Axe X**. Appuyez sur ![done_icon](assets/done_icon.png).
   1. Sélectionnez **Fréquence** dans la liste déroulante **Fonctions**.
   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Appels** dans la section **Axe Y**. Appuyez sur ![done_icon](assets/done_icon.png).
   1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés du graphique.

1. Accédez à l’onglet **Actifs** et appliquez le filtre pour afficher uniquement les fragments de mise en page dans le volet gauche. Faites glisser le fragment de mise en page **table_lf** dans la zone cible **Appels détaillés**.
1. Sélectionnez le champ de texte dans la colonne **Date** et appuyez sur ![configure_icon](assets/configure_icon.png) (Configurer).
1. Sélectionnez **Objet du modèle de données** dans la liste déroulante **Type de liaison** et sélectionnez **calls** > **calldate**. Appuyez deux fois sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés.

   De même, créez une liaison avec **calltime**, **callnumber**, **callduration** et **callcharges** pour les champs texte dans les colonnes **Heure**, **Numéro**, **Durée** et **Frais**.

1. Appuyez sur la zone cible **PayNow** et appuyez sur **+** pour ajouter un composant **Image**.
1. Appuyez sur le composant Image et sélectionnez ![configure_icon](assets/configure_icon.png) (Configurer). Les propriétés de l’image s’affichent dans le volet gauche :

   1. Spécifiez **PayNow** comme nom de l’image dans le champ **Nom**.
   1. Appuyez sur **Télécharger**, sélectionnez l’image   enregistrée sur le système de fichiers local puis appuyez sur **Ouvrir**.
   1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés de l’image.

1. Répétez les étapes 13 et 14 pour ajouter l’image **ValueAddedServices** à la zone cible **ValueAddedServices**.

### Créer une communication interactive pour canal web {#create-interactive-communication-for-web-channel}

Voici la liste des ressources qui ont déjà été créées dans ce didacticiel et qui sont nécessaires à la création de la communication interactive pour le canal web :

**Modèle web :** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modèle de données de formulaire :** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragments de document :** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**Images :** PayNowWeb et ValueAddedServicesWeb

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Appuyez sur **Créer** et sélectionnez **Communication interactive**. L’assistant **Créer une communication interactive** s’affiche.
1. Spécifiez **create_first_ic** dans les champs **Titre** et **Nom**. Sélectionnez **FDM_Create_First_IC** comme modèle de données de formulaire et appuyez sur **Suivant**.
1. Dans l’assistant **Canaux** :

   1. Spécifiez **create_first_ic_print_template** comme modèle d’impression et appuyez sur **Sélectionner**. Assurez-vous que la case **Utiliser l’impression en tant que page principale pour le canal web** n’est pas cochée.

   1. Spécifiez le dossier **Create_First_IC_templates** > **Create_First_IC_Web_Template** en tant que modèle web et appuyez sur **Sélectionner**.

   1. Appuyez sur **Créer**.

   Un message de confirmation s’affiche pour confirmer que la communication interactive a été créée correctement.

1. Appuyez sur **Modifier** pour ouvrir la communication interactive dans le volet droit.
1. Appuyez sur l’onglet **Canaux** dans le volet gauche et appuyez sur **Web**.
1. Accédez à l’onglet **Ressources** et appliquez le filtre pour afficher uniquement les fragments de document dans le volet gauche.
1. Faites glisser les fragments de documents suivants vers leurs zones cibles dans la communication interactive :

   | Fragment de document | Zone cible |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | Frais |

1. Appuyez sur **Résumé des frais** dans la zone cible et appuyez sur **+** pour ajouter un composant **Graphique**.
1. Appuyez sur le composant Graphique et sélectionnez ![configure_icon](assets/configure_icon.png) (Configurer). Les propriétés du graphique s’affichent dans le volet gauche :

   1. Spécifiez un nom pour le diagramme.
   1. Sélectionnez **Diagramme circulaire** dans la liste déroulante **Type de graphique**.

   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Calls** dans la section **Axe X**. Appuyez sur ![done_icon](assets/done_icon.png).

   1. Sélectionnez **Fréquence** dans la liste déroulante **Fonctions**.

   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Appels** dans la section **Axe Y**. Appuyez sur ![done_icon](assets/done_icon.png).

   1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés du graphique.

1. Sélectionnez l’onglet **Sources de données** dans le volet gauche et faites glisser l’objet de modèle de données **calls** vers la zone cible **Appels détaillés**. Toutes les propriétés de l’objet de modèle de données **calls** sont affichées sous forme de colonnes de tableau dans la zone cible **Appels détaillés** dans le volet droit.

   Selon le cas d’utilisation, vous avez besoin des colonnes Date d’appel, Heure d’appel, Numéro d’appel, Durée d’appel et Frais d’appel dans le tableau.

   ![Tableau pour la communication interactive](assets/table_ic_web_new.png)

1. Sélectionnez l’en-tête de colonne du tableau **Mobilenum** et sélectionnez **Plus d’options** > **Supprimer colonne**. De même, supprimez la colonne **calltype**.
1. Sélectionnez l’en-tête de la colonne **Calldate** du tableau et appuyez sur ![Modifier](assets/edit.png) pour remplacer le texte par **Date de l’appel**. De même, renommez les autres en-têtes des colonnes du tableau.
1. Selon le cas d’utilisation, insérez un bouton **Payer maintenant** dans la communication interactive qui permet à l’utilisateur d’effectuer le paiement en cliquant sur le bouton. Effectuez les étapes suivantes pour insérer le bouton :

   1. Appuyez sur **Payer maintenant** dans la zone cible et appuyez sur **+** pour ajouter un composant **Texte**.

   1. Appuyez sur le composant texte et appuyez sur ![Modifier](assets/edit.png).
   1. Renommez le texte avec **Payer maintenant**.
   1. Sélectionnez le texte et appuyez sur l’icône Hyperlien.
   1. Spécifiez l’URL de paiement dans le champ **Chemin d’accès**.
   1. Sélectionnez **Nouvel onglet** dans la liste déroulante **Cible**.

   1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés hyperlien.

1. Sélectionnez **Style** dans la liste déroulante en regard de l’option **Aperçu**.

   ![Sélectionner le mode Style pour la communication interactive](assets/select_style_ic_web_new.png)

1. Personnalisez le texte de l’hyperlien pour l’afficher en tant que bouton dans la communication interactive en suivant les étapes suivantes :

   1. Appuyez sur le composant texte et sélectionnez ![Modifier](assets/edit.png) (Modifier).
   1. Dans la section **Bordure**, spécifiez **1,5 px** comme **largeur de bordure**, sélectionnez **Solide** comme **style de bordure** et spécifiez **46 px** comme **rayon de bordure**.

   1. Sélectionnez Rouge comme couleur d’arrière-plan pour le bouton dans la section **Arrière-plan**.
   1. Dans le champ **Marge** de la section **Dimensions et position**, appuyez sur l’icône **Modifier simultanément** et définissez la marge de **droite** à **450 px**. Les zones Haut, Bas et Gauche sont définies comme vides.

   ![Insérez un lien hypertexte dans la communication interactive](assets/ic_web_hyperlink_new.png)

1. Appuyez sur **Payer maintenant** dans la zone cible, puis appuyez sur **+** pour ajouter un composant **Image**.
1. Appuyez sur le composant Image et sélectionnez ![configure-icon](assets/configure_icon.png) (Configurer). Les propriétés de l’image s’affichent dans le volet gauche :

   1. Spécifiez **PayNow** comme nom de l’image dans le champ **Nom**.

   1. Appuyez sur **Télécharger**, sélectionnez l’image **PayNowWeb** enregistrée sur le système de fichiers local puis appuyez sur **Ouvrir**.

   1. Appuyez sur ![done_icon](assets/done_icon.png) pour enregistrer les propriétés de l’image.

1. Selon le cas d’utilisation, insérez un bouton **S’abonner** dans la communication interactive qui permet à l’utilisateur de s’abonner aux services à valeur ajoutée en cliquant sur le bouton.

   Répétez les étapes 13 à 17 pour ajouter un bouton **S’abonner** à la zone cible des **services à valeur ajoutée** et ajouter l’image **ValueAddedServicesWeb**.

## Créer des communications interactives pour les versions impression et web avec synchronisation automatique {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

Vous pouvez également créer une communication interactive en activant la synchronisation automatique entre les canaux d’impression et web. Pour activer la synchronisation automatique, sélectionnez Impression comme option principale lors de la création de la communication interactive. La sélection d’Impression comme option principale garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression. Elle garantit également que les modifications apportées dans le canal d’impression sont répercutées dans le canal web.

Exécutez les étapes suivantes pour dériver le contenu du canal web à l’aide du canal d’impression :

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Appuyez sur **Créer** et sélectionnez **Communication interactive**. L’assistant **Créer une communication interactive** s’affiche.
1. Spécifiez **create_first_ic** dans les champs **Titre** et **Nom**. Sélectionnez **FDM_Create_First_IC** comme modèle de données de formulaire et appuyez sur **Suivant**.
1. Dans l’assistant **Canaux** :

   1. Spécifiez **create_first_ic_print_template** comme modèle d’impression et appuyez sur **Sélectionner**.

   1. Cochez la case **Utiliser l’impression en tant que page principale pour le canal web**.
   1. Spécifiez le dossier **Create_First_IC_templates** > **Create_First_IC_Web_Template** en tant que modèle web et appuyez sur **Sélectionner**.

   1. Appuyez sur **Créer**.

   Un message de confirmation s’affiche pour confirmer que la communication interactive a été créée correctement.

1. Appuyez sur **Modifier** pour ouvrir la communication interactive dans le volet droit.
1. Exécutez les étapes 6 à 15 de la section [Créer une communication interactive pour le canal d’impression](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel).
1. Appuyez sur l’onglet **Canaux** dans le volet gauche et appuyez sur **Web** pour générer automatiquement du contenu pour le canal web à partir du canal d’impression.
1. Comme la case **Utiliser l’impression en tant que page principale pour le canal web** est cochée à l’étape 4, le contenu et les liaisons sont générés automatiquement pour le canal web à partir du canal d’impression.

   Le contenu du canal d’impression est inséré sous le contenu du modèle de canal web. Pour modifier le contenu du canal web qui a été généré automatiquement à partir du canal d’impression, vous pouvez annuler l’héritage pour toute zone cible.

   Passez le curseur sur la zone cible correspondante dans le canal web et sélectionnez ![cancelinheritance](assets/cancelinheritance.png) (Annuler l’héritage) puis, dans la boîte de dialogue **Annuler l’héritage**, appuyez sur **Oui**.

   ![Annuler l’héritage](assets/cancel_inheritance_web_channel_new.png)

   Si vous avez annulé l’héritage d’un composant, vous pouvez le réactiver. Pour réactiver l’héritage, passez le curseur au-dessus de la limite de la zone cible pertinente incluant le composant et appuyez sur ![reenableinheritance](assets/reenableinheritance.png).

1. Sélectionnez l’onglet **Contenu** dans le volet gauche.
1. Faites glisser le contenu du canal web généré automatiquement dans les panneaux existants du modèle web à l’aide de l’arborescence de contenu. Voici la liste des composants qui doivent être réorganisés :

   * Composant Informations de facturation dans le panneau Informations de facturation
   * Composant Informations sur le client dans le panneau Informations sur le client
   * Composant Récapitulatif de facturation dans le panneau Récapitulatif de facturation
   * Composant Récapitulatif des frais dans le panneau Récapitulatif des frais
   * Fragment de mise en page (tableau) dans le panneau Appels détaillés

   ![Arborescence de contenu web](assets/ic_web_content_tree_new.png)

1. Répétez les étapes 13 à 18 de la section [Créer une communication interactive pour canal web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) pour insérer les hyperliens **Payer maintenant** et **S’abonner** dans le canal web de la communication interactive.
