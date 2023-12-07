---
title: "Didacticiel\_: Créer une communication interactive "
description: Créer une communication interactive en utilisant tous les blocs de construction
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: aaacee66-6bbe-498b-91b1-3a9545ff1aeb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1884'
ht-degree: 39%

---

# Didacticiel : Créer une communication interactive {#tutorial-create-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Ce tutoriel fait partie de la série [Création de votre première communication interactive](/help/forms/using/create-your-first-interactive-communication.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et accomplir le cas d’utilisation complet du tutoriel.

Une fois que vous avez créé tous les blocs de création, tels que le modèle de données de formulaire, les fragments de document, les modèles et les thèmes pour la version web, vous pouvez commencer à créer une communication interactive.

Les communications interactives peuvent être fournies par deux canaux : impression et web. Vous pouvez également créer une communication interactive avec le canal d’impression comme gabarit. L’impression en tant qu’option principale pour le canal web garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression. Elle garantit également que les modifications apportées au canal d’impression sont synchronisées dans le canal web. Les auteurs de communication interactive sont toutefois autorisés à interrompre l’héritage pour des composants spécifiques du canal web.

Ce tutoriel vous guide tout au long des étapes de création de communications interactives pour les canaux d’impression et web. À la fin de ce didacticiel, vous serez capable de :

* Créer une communication interactive pour le canal d’impression
* Créer une communication interactive pour le canal web
* Créer des communications interactives d’impression et web avec l’impression comme Principal

## Créer des communications interactives pour l’impression et le web sans synchronisation {#create-interactive-communications-for-print-and-web-with-no-synchronization}

### Créer une communication interactive pour le canal d’impression {#create-interactive-communication-for-print-channel}

Voici la liste des ressources qui ont déjà été créées dans ce tutoriel et qui sont nécessaires lors de la création de la communication interactive pour le canal d’impression :

**Modèle d’impression :** [create_first_ic_print_template](../../forms/using/create-templates-print-web.md)

**Modèle de données de formulaire :** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragments de document :** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**Fragments de mise en page :** [table_lf](../../forms/using/create-templates-print-web.md)

**Images :** PayNow et ValueAddedServices

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionner **Créer** et sélectionnez **Communication interactive**. L’assistant **Créer une communication interactive** s’affiche.
1. Spécifiez **create_first_ic** dans les champs **Titre** et **Nom**. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Suivant**.
1. Dans l’assistant **Canaux** :

   1. Spécifier **create_first_ic_print_template** comme modèle d’impression et sélectionnez **Sélectionner**. Assurez-vous que la case **Utiliser l’impression en tant que page principale pour le canal web** n’est pas cochée.

   1. Spécifier **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** comme modèle Web et sélectionnez **Sélectionner**.

   1. Sélectionnez **Créer**.

   Un message de confirmation s’affiche pour confirmer que la communication interactive a bien été créée.

1. Sélectionner **Modifier** pour ouvrir la communication interactive dans le volet de droite.
1. Accédez à l’onglet **Ressources** et appliquez le filtre pour afficher uniquement les fragments de document dans le volet gauche.
1. Faites glisser les fragments de document suivants vers leurs zones cibles dans la communication interactive :

   | Fragment de document | Zone cible |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | Frais |

   ![Fragments de document pour les communications interactives](assets/create_first_ic_doc_fragments_new.png)

1. Sélectionner **Graphiques** zone cible, puis sélectionnez **+** pour ajouter une **Graphique** composant.
1. Sélectionnez le composant Graphique et sélectionnez ![configure_icon](assets/configure_icon.png) (Configuration). Les propriétés du graphique s’affichent dans le volet de gauche :

   1. Attribuez un nom au graphique.
   1. Sélectionnez **Diagramme circulaire** dans la liste déroulante **Type de graphique**.
   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Calls** dans la section **Axe X**. Sélectionner ![done_icon](assets/done_icon.png).
   1. Sélectionnez **Fréquence** dans la liste déroulante **Fonctions**.
   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Appels** dans la section **Axe Y**. Sélectionner ![done_icon](assets/done_icon.png).
   1. Sélectionner ![done_icon](assets/done_icon.png) pour enregistrer les propriétés du graphique.

1. Accédez à l’onglet **Actifs** et appliquez le filtre pour afficher uniquement les fragments de mise en page dans le volet gauche. Faites glisser le fragment de mise en page **table_lf** dans la zone cible **Appels détaillés**.
1. Sélectionnez le champ de texte dans le **Date** et sélectionnez ![configure_icon](assets/configure_icon.png) (Configuration).
1. Sélectionnez **Objet du modèle de données** dans la liste déroulante **Type de liaison** et sélectionnez **calls** > **calldate**. Sélectionner ![done_icon](assets/done_icon.png) deux fois pour enregistrer les propriétés.

   De même, créez une liaison avec **calltime**, **callnumber**, **callduration** et **callcharges** pour les champs texte dans les colonnes **Heure**, **Numéro**, **Durée** et **Frais**.

1. Sélectionner **PayNow** zone cible, puis sélectionnez **+** pour ajouter une **Image** composant.
1. Sélectionnez le composant Image et sélectionnez ![configure_icon](assets/configure_icon.png) (Configuration). Les propriétés de l’image s’affichent dans le volet de gauche :

   1. Spécifier **PayNow** comme nom de l’image dans la variable **Nom** champ .
   1. Sélectionner **Télécharger**, sélectionnez l’image enregistrée sur le système de fichiers local, puis sélectionnez **Ouvrir**.
   1. Sélectionner ![done_icon](assets/done_icon.png) pour enregistrer les propriétés de l’image.

1. Répétez les étapes 13 et 14 pour ajouter l’image **ValueAddedServices** à la zone cible **ValueAddedServices**.

### Créer une communication interactive pour canal web {#create-interactive-communication-for-web-channel}

Voici la liste des ressources qui ont déjà été créées dans ce tutoriel et qui sont nécessaires lors de la création de la communication interactive pour le canal web :

**Modèle web :** [Create_First_IC_Web_Template](../../forms/using/create-templates-print-web.md)

**Modèle de données de formulaire :** [FDM_Create_First_IC](../../forms/using/create-form-data-model0.md)

**Fragments de document :** [bill_details_first_ic, customer_details_first_ic, bill_summary_first_ic, summary_charges_first_ic](../../forms/using/create-document-fragments.md)

**Images :** PayNowWeb et ValueAddedServicesWeb

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionner **Créer** et sélectionnez **Communication interactive**. L’assistant **Créer une communication interactive** s’affiche.
1. Spécifiez **create_first_ic** dans les champs **Titre** et **Nom**. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Suivant**.
1. Dans l’assistant **Canaux** :

   1. Spécifier **create_first_ic_print_template** comme modèle d’impression et sélectionnez **Sélectionner**. Assurez-vous que la case **Utiliser l’impression en tant que page principale pour le canal web** n’est pas cochée.

   1. Spécifier **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** comme modèle Web et sélectionnez **Sélectionner**.

   1. Sélectionnez **Créer**.

   Un message de confirmation s’affiche pour confirmer que la communication interactive a bien été créée.

1. Sélectionner **Modifier** pour ouvrir la communication interactive dans le volet de droite.
1. Sélectionnez la variable **Canaux** dans le volet de gauche, puis sélectionnez **Web**.
1. Accédez à l’onglet **Ressources** et appliquez le filtre pour afficher uniquement les fragments de document dans le volet gauche.
1. Faites glisser les fragments de document suivants vers leurs zones cibles dans la communication interactive :

   | Fragment de document | Zone cible |
   |---|---|
   | bill_details_first_ic | BillDetails |
   | customer_details_first_ic | CustomerDetails |
   | bill_summary_first_ic | BillSummary |
   | summary_charges_first_interactive_communication | Frais |

1. Sélectionner **Résumé des frais** zone cible, puis sélectionnez **+** pour ajouter une **Graphique** composant.
1. Sélectionnez le composant Graphique et sélectionnez ![configure_icon](assets/configure_icon.png) (Configuration). Les propriétés du graphique s’affichent dans le volet de gauche :

   1. Attribuez un nom au graphique.
   1. Sélectionnez **Diagramme circulaire** dans la liste déroulante **Type de graphique**.

   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Calls** dans la section **Axe X**. Sélectionner ![done_icon](assets/done_icon.png).

   1. Sélectionnez **Fréquence** dans la liste déroulante **Fonctions**.

   1. Sélectionnez la propriété **calltype** à partir du type d’objet du modèle de données **Appels** dans la section **Axe Y**. Sélectionner ![done_icon](assets/done_icon.png).

   1. Sélectionner ![done_icon](assets/done_icon.png) pour enregistrer les propriétés du graphique.

1. Sélectionnez l’onglet **Sources de données** dans le volet gauche et faites glisser l’objet de modèle de données **calls** vers la zone cible **Appels détaillés**. Toutes les propriétés de l’objet de modèle de données **calls** sont affichées sous forme de colonnes de tableau dans la zone cible **Appels détaillés** dans le volet droit.

   Selon le cas d’utilisation, vous avez besoin des colonnes Date d’appel, Heure d’appel, Numéro d’appel, Durée d’appel et Frais d’appel dans le tableau.

   ![Tableau pour la communication interactive](assets/table_ic_web_new.png)

1. Sélectionnez l’en-tête de colonne du tableau **Mobilenum** et sélectionnez **Plus d’options** > **Supprimer colonne**. De même, supprimez la colonne **calltype**.
1. Sélectionnez la variable **Calldate** en-tête de colonne du tableau et sélectionnez ![edit](assets/edit.png) (Modifier) pour renommer le texte en **Date de l’appel**. De même, renommez les autres en-têtes de colonne du tableau.
1. En fonction du cas d’utilisation, insérez une **Payer maintenant** dans la communication interactive qui permet à l’utilisateur d’effectuer le paiement en cliquant sur le bouton . Pour insérer le bouton, procédez comme suit :

   1. Sélectionner **Payer maintenant** zone cible, puis sélectionnez **+** pour ajouter une **Texte** composant.

   1. Sélectionnez le composant de texte, puis sélectionnez ![edit](assets/edit.png) (Modifier).
   1. Renommez le texte en **Payer maintenant**.
   1. Sélectionnez le texte et cliquez sur l’icône Lien hypertexte.
   1. Spécifiez l’URL de paiement dans la variable **Chemin** champ .
   1. Sélectionner **Nouvel onglet** de **Cible** liste déroulante.

   1. Sélectionner ![done_icon](assets/done_icon.png) pour enregistrer les propriétés de l’hyperlien.

1. Sélectionnez **Style** dans la liste déroulante en regard de l’option **Aperçu**.

   ![Sélectionner le mode Style pour la communication interactive](assets/select_style_ic_web_new.png)

1. Personnalisez le texte de l’hyperlien pour l’afficher en tant que bouton dans la communication interactive en suivant les étapes suivantes :

   1. Sélectionnez le composant de texte, puis sélectionnez ![edit](assets/edit.png) (Modifier).
   1. Dans le **Bordure** , spécifiez **1,5 px** as **Largeur de la bordure**, sélectionnez **Plein** as **Style de bordure**, et spécifiez **46 px** as **Rayon de bordure**.

   1. Sélectionnez Rouge comme couleur d’arrière-plan pour le bouton dans le **Contexte** .
   1. Dans le **Marge** champ pour **Dimensions et position** , sélectionnez **Modifier simultanément** et définissez la variable **Right** margin as **450 px**. Les zones Haut, Bas et Gauche sont définies comme vides.

   ![Insérez un lien hypertexte dans la communication interactive](assets/ic_web_hyperlink_new.png)

1. Sélectionner **Payer maintenant** zone cible, puis sélectionnez **+** pour ajouter une **Image** composant.
1. Sélectionnez le composant Image et sélectionnez ![configure_icon](assets/configure_icon.png) (Configuration). Les propriétés de l’image s’affichent dans le volet de gauche :

   1. Spécifier **PayNow** comme nom de l’image dans la variable **Nom** champ .

   1. Sélectionner **Télécharger**, sélectionnez la variable **PayNowWeb** image enregistrée sur le système de fichiers local, puis sélectionnez **Ouvrir**.

   1. Sélectionner ![done_icon](assets/done_icon.png) pour enregistrer les propriétés de l’image.

1. Selon le cas d’utilisation, insérez un bouton **S’abonner** dans la communication interactive qui permet à l’utilisateur de s’abonner aux services à valeur ajoutée en cliquant sur le bouton.

   Répétez les étapes 13 à 17 pour ajouter un bouton **S’abonner** à la zone cible des **services à valeur ajoutée** et ajouter l’image **ValueAddedServicesWeb**.

## Création de communications interactives pour l’impression et le web avec synchronisation automatique {#create-interactive-communications-for-print-and-web-with-auto-synchronization}

Vous pouvez également créer une communication interactive en activant la synchronisation automatique entre les canaux d’impression et web. Pour activer la synchronisation automatique, sélectionnez l’option Imprimer en tant que gabarit lors de la création de la communication interactive. La sélection de l’option Imprimer comme option principale garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression. Elle garantit également que les modifications apportées au canal d’impression sont répercutées dans le canal web.

Pour dériver le contenu du canal web à l’aide du canal d’impression, procédez comme suit :

1. Connectez-vous à l’instance d’auteur AEM et accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionner **Créer** et sélectionnez **Communication interactive**. L’assistant **Créer une communication interactive** s’affiche.
1. Spécifiez **create_first_ic** dans les champs **Titre** et **Nom**. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Suivant**.
1. Dans l’assistant **Canaux** :

   1. Spécifier **create_first_ic_print_template** comme modèle d’impression et sélectionnez **Sélectionner**.

   1. Cochez la case **Utiliser l’impression en tant que page principale pour le canal web**.
   1. Spécifier **Create_First_IC_templates** folder > **Create_First_IC_Web_Template** comme modèle Web et sélectionnez **Sélectionner**.

   1. Sélectionnez **Créer**.

   Un message de confirmation s’affiche pour confirmer que la communication interactive a bien été créée.

1. Sélectionner **Modifier** pour ouvrir la communication interactive dans le volet de droite.
1. Exécutez les étapes 6 à 15 de la section [Créer une communication interactive pour le canal d’impression](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-print-channel).
1. Sélectionnez la variable **Canaux** dans le volet de gauche, puis sélectionnez **Web** pour générer automatiquement le contenu pour le canal web à partir du canal d’impression.
1. Comme la case **Utiliser l’impression en tant que page principale pour le canal web** est cochée à l’étape 4, le contenu et les liaisons sont générés automatiquement pour le canal web à partir du canal d’impression.

   Le contenu du canal d’impression est inséré sous le contenu du modèle de canal web. Pour modifier le contenu du canal web généré automatiquement à partir du canal d’impression, vous pouvez annuler l’héritage pour n’importe quelle zone cible.

   Passez la souris sur la zone cible appropriée du canal web et sélectionnez ![annulation inheritance](assets/cancelinheritance.png) (Annuler l’héritage), puis dans le **Annuler l’héritage** boîte de dialogue, sélectionnez **Oui**.

   ![Annuler l’héritage](assets/cancel_inheritance_web_channel_new.png)

   Si vous avez annulé l’héritage d’un composant, vous pouvez le réactiver. Pour réactiver l’héritage, passez la souris sur la bordure de la zone cible concernée, qui inclut le composant, puis sélectionnez ![réactiver l’héritage](assets/reenableinheritance.png).

1. Sélectionnez la variable **Contenu** dans le volet de gauche.
1. Faites glisser le contenu du canal web généré automatiquement vers les panneaux existants du modèle web à l’aide de l’arborescence de contenu. Voici la liste des composants qui doivent être réorganisés :

   * Composant Informations de facturation dans le panneau Informations de facturation
   * Composant Détails client du panneau Détails client
   * Composant Résumé de facturation dans le panneau Résumé de facturation
   * Composant Résumé des frais dans le panneau Résumé des frais
   * Fragment de disposition (tableau) dans le panneau Appels détaillés

   ![Arborescence de contenu web](assets/ic_web_content_tree_new.png)

1. Répétez les étapes 13 à 18 de la section [Créer une communication interactive pour canal web](../../forms/using/create-interactive-communication0.md#create-interactive-communication-for-web-channel) pour insérer les hyperliens **Payer maintenant** et **S’abonner** dans le canal web de la communication interactive.
