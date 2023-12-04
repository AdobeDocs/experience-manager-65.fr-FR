---
title: "Didacticiel\_: Créer des fragments de document"
description: Créer des fragments de document pour la communication interactive
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: 81429735-cd52-4621-8dc2-10dd89df3052
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1653'
ht-degree: 53%

---

# Didacticiel : Créer des fragments de document{#tutorial-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Ce tutoriel fait partie de la série [Création de votre première communication interactive](/help/forms/using/create-your-first-interactive-communication.md). Adobe vous recommande de suivre la série dans un ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du tutoriel.

Les fragments de document sont des composants réutilisables d’une correspondance qui sont utilisés pour composer une communication interactive. Les fragments de document sont composés des types suivants :

* Texte : une ressource texte est un élément de contenu comprenant un ou plusieurs paragraphes de texte. Un paragraphe peut être statique ou dynamique.
* Liste : la liste est un groupe de fragments du document, incluant du texte, des listes, des conditions et des images.
* Condition : les conditions vous permettent de définir le contenu à inclure dans la communication interactive en fonction des données reçues du formulaire de modèle de données.

Ce tutoriel vous guide à travers les étapes pour créer plusieurs fragments de document de texte en fonction de la structure fournie à la section [Planifier la communication interactive](/help/forms/using/planning-interactive-communications.md). À la fin de ce tutoriel, vous devriez pouvoir effectuer les opérations suivantes :

* Créer des fragments de document
* Créer des variables
* Créer et appliquer des règles

![text_document_fragments](assets/text_document_fragments.gif)

Voici la liste des fragments de document créés dans ce didacticiel :

* [Informations de facturation](../../forms/using/create-document-fragments.md#step-create-bill-details-text-document-fragment)
* [Informations sur le client](../../forms/using/create-document-fragments.md#step-create-customer-details-text-document-fragment)
* [Récapitulatif de facturation](../../forms/using/create-document-fragments.md#step-create-bill-summary-text-document-fragment)
* [Récapitulatif des frais](../../forms/using/create-document-fragments.md#step-create-summary-of-charges-text-document-fragment)

Chaque fragment de document comprend des champs avec du texte statique, des données reçues du modèle de données de formulaire et des données saisies à l’aide de l’interface utilisateur de l’agent. Tous ces champs ont été décrits dans la section [Planifier la communication interactive](/help/forms/using/planning-interactive-communications.md).

Lors de la création de fragments de document dans ce didacticiel, des variables sont créées pour les champs recevant des données à l’aide de l’interface utilisateur de l’agent.

Utilisez **FDM_Create_First_IC** comme décrit dans la section [Créer un modèle de données de formulaire](../../forms/using/create-form-data-model0.md), comme le modèle de données de formulaire pour créer des fragments de document dans ce tutoriel.

## Étape 1 : création d’un fragment de document texte de détails de facturation {#step-create-bill-details-text-document-fragment}

Le fragment de document de détails de facturation comprend les champs suivants :

| Champ | Source de données |
|---|---|
| Facture Non | Interface utilisateur de l’agent |
| Période de facturation | Interface utilisateur de l’agent |
| Date de facturation | Interface utilisateur de l’agent |
| Votre plan | Modèle de données de formulaire |

Pour créer des variables pour les champs dont la source de données est l’interface utilisateur de l’agent, créer du texte statique et utiliser des éléments de modèle de données de formulaire dans le fragment de document, procédez comme suit :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.

1. Sélectionnez **Créer** > **Texte**.
1. Saisissez les informations suivantes :

   1. Entrée **bill_details_first_ic** comme nom dans la variable **Titre** champ . Le titre est automatiquement renseigné dans la variable **Nom** champ .

   1. Sélectionner **Modèle de données de formulaire** de la **Modèle de données** .

   1. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Sélectionner**.

   1. Sélectionnez **Suivant**.

1. Sélectionnez la variable **Variables** dans le volet de gauche, puis sélectionnez **Créer**.
1. Dans le **Créer une variable** section :

   1. Entrée **Invoicenumber** comme nom de la variable.
   1. Sélectionner **Chaîne** comme type.
   1. Sélectionnez **Créer**.

   ![Créer une variable de type Chaîne](assets/variable_create_string_new.png)

   Répétez les étapes 4 et 5 pour créer les variables suivantes :

   * Billperiod : type de chaîne
   * BillDate : type de date

   ![Informations de facturation](assets/variable_bill_details_new.png)

1. Créez du texte statique pour les champs suivants à l’aide du volet de droite :

   * Facture Non
   * Période de facturation
   * Date de facturation
   * Votre plan

   ![Du texte statique](assets/variable_bill_details_static_text_new.png)

1. Placez le curseur en regard du champ **N° de facture** et cliquez deux fois sur la variable **InvoiceNumber** de l’onglet **Variables** dans le volet de gauche.
1. Placez le curseur en regard du champ **Période de facturation**, puis double-cliquez sur la variable **Billperiod**.
1. Placez le curseur en regard du champ **Date de facturation**, puis double-cliquez sur la variable **Bill Date**.
1. Sélectionnez l’onglet **Objets de modèle de données** dans le volet gauche.
1. Placez le curseur en regard du champ **Votre planification**, puis double-cliquez sur la propriété **customer** > **customerplan**.

   ![bill_details_customerplan_fdm](assets/bill_details_customerplan_fdm.png)

1. Cliquez sur **Enregistrer** pour créer le fragment de document texte de détails de facturation.

## Étape 2 : création d’un fragment de document texte de détails du client {#step-create-customer-details-text-document-fragment}

Le fragment de document Customer Details comprend les champs suivants :

| Champ | Source de données |
|---|---|
| Nom du client | Modèle de données de formulaire |
| Adresse | Modèle de données de formulaire |
| Lieu de livraison | Interface utilisateur de l’agent |
| Code d’état | Interface utilisateur de l’agent |
| Numéro de mobile | Modèle de données de formulaire |
| Autre numéro de contact | Modèle de données de formulaire |
| Numéro de relation | Modèle de données de formulaire |
| Nombre de connexions | Interface utilisateur de l’agent |

Pour créer des variables pour les champs dont la source de données est l’interface utilisateur de l’agent, créer du texte statique et utiliser des éléments de modèle de données de formulaire dans le fragment de document, procédez comme suit :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Sélectionnez **Créer** > **Texte**.
1. Saisissez les informations suivantes :

   1. Saisissez **customer_details_first_ic** comme nom dans le champ **Titre**. Le titre est automatiquement renseigné dans la variable **Nom** champ .

   1. Sélectionner **Modèle de données de formulaire** de la **Modèle de données** .

   1. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Sélectionner**.

   1. Sélectionnez **Suivant**.

1. Sélectionnez la variable **Variables** dans le volet de gauche, puis sélectionnez **Créer**.
1. Dans le **Créer une variable** section :

   1. Saisissez **Placesupply** comme nom de la variable.
   1. Sélectionner **Chaîne** comme type.
   1. Sélectionnez **Créer**.

   Répétez les étapes 4 et 5 pour créer les variables suivantes :

   * Statecode : type de nombre
   * Numberconnections : type de nombre

1. Sélectionnez l’onglet **Objets de modèle de données**, placez le curseur dans le volet de droite, double-cliquez sur la propriété **client** > **name**.
1. Cliquez sur Entrée pour déplacer le curseur sur la ligne suivante et double-cliquez sur la propriété **client** > **address**.
1. Créez du texte statique pour les champs suivants à l’aide du volet de droite :

   * Numéro de mobile
   * Autre numéro de contact
   * Lieu de livraison
   * Numéro de relation
   * Code d’état
   * Nombre de connexions

   ![Texte statique des détails du client](assets/customer_details_static_text_new.png)

1. Placez le curseur en regard du champ **Numéro de mobile** et double-cliquez sur la propriété **client** > **mobilenum**.
1. Placez le curseur en regard du champ **Autre numéro de téléphone** et double-cliquez sur la propriété client > **alternatemobilenumber**.
1. Placez le curseur en regard du champ **Numéro de relation** et double-cliquez sur la propriété **client** > **relationshipnumber**.
1. Sélectionnez l’onglet **Variables**, placez le curseur en regard du champ **Lieu des prestations** et double-cliquez sur la variable **Placesupply**.
1. Placez le curseur en regard du champ **Code du pays** et double-cliquez sur la variable **Statecode**.
1. Placez le curseur en regard du champ **Nombre de connexions** et double-cliquez sur la variable **Numberconnections**.

   ![Informations sur le client](assets/customer_details_df2_new.png)

1. Cliquez sur **Enregistrer** pour créer le fragment de document texte Détails du client.

## Étape 3 : Création d’un fragment de document de texte de résumé de facturation {#step-create-bill-summary-text-document-fragment}

Le fragment de document de résumé de facturation comprend les champs suivants :

| Champ | Source de données |
|---|---|
| Solde précédent | Interface utilisateur de l’agent |
| Paiements | Interface utilisateur de l’agent |
| Ajustements | Interface utilisateur de l’agent |
| Facturation de la période de facturation actuelle | Modèle de données de formulaire |
| Montant dû | Interface utilisateur de l’agent |
| Échéance | Interface utilisateur de l’agent |

Pour créer des variables pour les champs dont la source de données est l’interface utilisateur de l’agent, créer du texte statique et utiliser des éléments de modèle de données de formulaire dans le fragment de document, procédez comme suit :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Sélectionnez **Créer** > **Texte**.
1. Saisissez les informations suivantes :

   1. Saisissez **bill_summary_first_ic** comme nom dans le champ **Titre**. Le titre est automatiquement renseigné dans la variable **Nom** champ .

   1. Sélectionner **Modèle de données de formulaire** de la **Modèle de données** .

   1. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Sélectionner**.

   1. Sélectionnez **Suivant**.

1. Sélectionnez la variable **Variables** dans le volet de gauche, puis sélectionnez **Créer**.
1. Dans le **Créer une variable** section :

   1. Saisissez **Previousbalance** comme nom de la variable.
   1. Sélectionnez **Numéro** comme type.
   1. Sélectionnez **Créer**.

   Répétez les étapes 4 et 5 pour créer les variables suivantes :

   * Paiements : type de nombre
   * Ajustements : type de nombre
   * Amountdue : Type de nombre
   * Duedate : type de date

1. Créez du texte statique pour les champs suivants à l’aide du volet de droite :

   * Solde précédent
   * Paiements
   * Ajustements
   * Facturation de la période de facturation actuelle
   * Montant dû
   * Échéance
   * Les frais de retard de paiement après la date d&#39;échéance sont de 20 $

   ![Texte statique du résumé de facturation](assets/bill_summary_static_new.png)

1. Placez le curseur en regard du champ **Solde précédent** et double-cliquez sur la variable **Previousbalance**.
1. Placez le curseur en regard du champ **Paiements** et double-cliquez sur la variable **Payments**.
1. Placez le curseur en regard du champ **Réglages** et double-cliquez sur la variable **Adjustments**.
1. Placez le curseur en regard du champ **Montant dû** et double-cliquez sur la variable **Amountdue**.
1. Placez le curseur en regard du champ **Date d’échéance** et double-cliquez sur la variable **Duedate**.
1. Sélectionnez l’onglet **Objets de modèle de données**, placez le curseur en regard du champ **Facturation de la période en cours** dans le volet de droite, puis double-cliquez sur la propriété **factures** > **usagecharges**.

   ![Récapitulatif de facturation](assets/bill_summary_static_variables_new.png)

1. Cliquez sur **Enregistrer** pour créer le fragment de document texte Détails du client.

## Étape 4 : Création d’un fragment de document de résumé des frais {#step-create-summary-of-charges-text-document-fragment}

Le résumé des frais de fragments de document comprend les champs suivants :

| Champ | Source de données |
|---|---|
| Frais d’appel | Modèle de données de formulaire |
| Frais de conférence téléphonique | Modèle de données de formulaire |
| Frais de SMS | Modèle de données de formulaire |
| Frais Internet mobiles | Modèle de données de formulaire |
| Frais d’itinérance nationale | Modèle de données de formulaire |
| Frais d’itinérance internationale | Modèle de données de formulaire |
| Frais de services à valeur ajoutée | Modèle de données de formulaire |
| Frais totaux | Modèle de données de formulaire |
| TOTAL À PAYER | Modèle de données de formulaire |

Pour créer du texte statique et utiliser des éléments de modèle de données de formulaire dans le fragment de document, procédez comme suit :

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Fragments de document]**.
1. Sélectionnez **Créer** > **Texte**.
1. Saisissez les informations suivantes :

   1. Saisissez **summary_charges_first_ic** comme nom dans le champ **Titre**. Le titre se génère automatiquement dans le champ Nom.

   1. Sélectionner **Modèle de données de formulaire** de la **Modèle de données** .

   1. Sélectionner **FDM_Create_First_IC** comme modèle de données de formulaire et sélectionnez **Sélectionner**.

   1. Sélectionnez **Suivant**.

1. Créez du texte statique pour les champs suivants à l’aide du volet de droite :

   * Frais d’appel
   * Frais de conférence téléphonique
   * Frais de SMS
   * Frais Internet mobiles
   * Frais d’itinérance nationale
   * Frais d’itinérance internationale
   * Frais de services à valeur ajoutée
   * Frais totaux
   * TOTAL À PAYER

   ![Récapitulatif des frais](assets/summary_charges_static_new.png)

1. Sélectionnez l’onglet **Objets de modèle de données**.
1. Placez le curseur en regard du champ **Frais d’appel** et double-cliquez sur la propriété **factures** > **callcharges**.
1. Placez le curseur en regard du champ **Frais de conférence téléphonique** et double-cliquez sur la propriété **factures** > **confcallcharges**.
1. Placez le curseur en regard du champ **Frais de SMS** et double-cliquez sur la propriété **factures** > **smscharges**.
1. Placez le curseur en regard du champ **Frais d’Internet mobile** et double-cliquez sur la propriété **factures** > **internetcharges**.
1. Placez le curseur en regard du champ **Frais d’itinérance nationale** et double-cliquez sur la propriété **factures** > **roamingnational**.
1. Placez le curseur en regard du champ **Frais d’itinérance internationale** et double-cliquez sur la propriété **factures** > **roamingintnl**.
1. Placez le curseur en regard du champ **Services à valeur ajoutée** et double-cliquez sur la propriété **factures** > **vas**.
1. Placez le curseur en regard du champ **Frais totaux** et double-cliquez sur la propriété **factures** > **usagecharges**.
1. Placez le curseur en regard du champ **TOTAL À PAYER** et double-cliquez sur la propriété **factures** > **usagecharges**.

   ![Récapitulatif des frais](assets/summary_charges_static_fdm_new.png)

1. Sélectionnez le texte dans le **Frais de services à valeur ajoutée** ligne et sélectionnez **Créer une règle** pour créer une condition d’après laquelle la ligne est affichée dans la communication interactive :
1. Sur le **Créer une règle** fenêtre contextuelle :

   1. Sélectionner **Modèles et variables de données** puis **bills** > **callcharges**.

   1. Sélectionner **est inférieur à** comme opérateur.
   1. Sélectionner **Nombre** et saisissez la valeur **60**.

   Selon cette condition, la ligne Frais de services à valeur ajoutée ne s’affiche que si la valeur du champ Frais d’appel est inférieure à 60.

   ![create_rules_caption](assets/create_rules_caption.gif)

1. Cliquez sur **Enregistrer** pour créer le texte Résumé des frais Fragment de document.
