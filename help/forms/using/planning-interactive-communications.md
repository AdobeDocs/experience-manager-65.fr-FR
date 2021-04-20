---
title: '"Didacticiel : Planifier la communication interactive"'
seo-title: Planifier votre communication interactive
description: Planifier la structure de votre communication interactive
seo-description: Planifier la structure de votre communication interactive
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 89%

---


# Didacticiel : Planifier la communication interactive {#tutorial-plan-the-interactive-communication}

Planifier la structure de votre communication interactive

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Ce didacticiel est une étape de la série [Créer votre première série de communications interactives](/help/forms/using/create-your-first-interactive-communication.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

La première étape de la planification d’une communication interactive consiste à finaliser le contenu de cette dernière. Des experts spécialisés appartenant entre autres aux services juridique, financier, de support ou marketing peuvent vous aider à finaliser le contenu. Une fois le contenu finalisé, vous devez l’analyser pour identifier les différents types de ressources requis pour créer la communication interactive.

## Observations relatives à la planification {#planning-considerations}

Une communication interactive comprend les éléments suivants :

* Un **texte statique** qui inclut principalement les parties de la communication interactive qui sont de nature générique et qui sont incluses dans la communication pour tous les clients : par exemple l’en-tête, le pied de page, les salutations ou les clauses de non-responsabilité.
* Des **données provenant d’un système d’arrière-plan (modèle de données de formulaire)** qui sont spécifiques au client et fusionnées de manière dynamique avec la communication interactive : par exemple, le numéro de police ou l’adresse peuvent être obtenus à l’aide du modèle de données de formulaire.
* La **mise en page ou les modèles** pour la version d’impression et web de la communication interactive.
* L’**ordre** dans lequel les différents paragraphes de texte apparaissent dans la communication interactive.
* **Données saisies par un employé de première ligne (interface utilisateur de l’agent)** qui personnalise la communication avant de l’envoyer. par exemple, la date d’échéance du paiement.

* Des **données conditionnelles** qui sont renseignées en fonction de conditions prédéfinies : Par exemple, la date de génération de la communication interactive.
* Des **images stockées dans un référentiel**, tels que des logos et des images de signature. Les images comme les logos de l’entreprise sont présentes dans la majorité ou dans toutes les communications interactives.
* Des **graphiques et tableaux** nécessaires pour simplifier la représentation de données complexes dans une communication interactive

## Structure de la communication interactive {#anatomy-of-the-interactive-communication}

Une fois que vous avez finalisé le contenu et les éléments utilisés pour créer votre communication interactive, vous pouvez créer une structure pour la communication interactive. Les informations de la structure doivent être répertoriées dans la section [Observations relatives à la planification](/help/forms/using/planning-interactive-communications.md#planning-considerations). En fonction de notre cas d’utilisation, voici un exemple de structure de facture mensuelle qu’un opérateur de télécommunications envoie à ses clients.

La structure comprend des données avec les modes de saisie suivants :

* Texte statique
* Modèle de données de formulaire
* Interface utilisateur de l’agent
* Données conditionnelles
* Images

Dans chaque section, le texte en gras représente le texte statique. La base de données comprend les tableaux des clients, des factures et des appels. Un modèle de données de formulaire peut recevoir des données de n’importe lequel de ces tableaux. Pour plus d’informations, voir [Création d’un modèle de données de formulaire](/help/forms/using/create-form-data-model0.md).

Le tableau suivant illustre la source de données de chaque champ de la structure de la communication interactive :

<table>
 <tbody>
  <tr>
   <td>Section</td>
   <td>Texte statique</td>
   <td>FDM </td>
   <td>Interface utilisateur de l’agent</td>
   <td>Images</td>
  </tr>
  <tr>
   <td>Informations de facturation</td>
   <td><p>N° de facture</p> <p>Date de facturation</p> <p>Période de facturation</p> <p>Votre planification</p> </td>
   <td><p>Valeur du champ <strong>Votre planification</strong></p> <p>Tableau - client</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>N° de facture</li>
     <li>Date de facturation</li>
     <li>Période de facturation</li>
    </ul> <p> </p> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Informations sur le client</td>
   <td><p>Lieu de livraison</p> <p>Code du pays</p> <p>Numéro de mobile</p> <p>Autre numéro de téléphone</p> <p>Numéro de relation</p> <p>Nombre de connexions</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Nom</li>
     <li>Adresse</li>
     <li>Numéro de mobile</li>
     <li>Autre numéro de téléphone</li>
     <li>Numéro de relation</li>
    </ul> <p>Tableau - client</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Lieu de livraison</li>
     <li>Code du pays</li>
     <li>Nombre de connexions</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Récapitulatif de facturation</td>
   <td><p>Solde précédent</p> <p>Paiements</p> <p>Ajustements</p> <p>Facturation de la période en cours</p> <p>Montant dû</p> <p>Échéance</p> </td>
   <td><p>Valeur du champ <strong>Facturer la période de facturation actuelle </strong></p> <p>Tableau - factures</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Solde précédent</li>
     <li>Paiements</li>
     <li>Ajustements</li>
     <li>Montant dû</li>
     <li>Échéance</li>
    </ul> </td>
   <td>—</td>
  </tr>
  <tr>
   <td>Récapitulatif des frais</td>
   <td><p>Frais d’appel</p> <p>Frais de conférence téléphonique</p> <p>Frais de SMS </p> <p>Frais d’Internet mobile</p> <p>Frais d’itinérance nationale</p> <p>Frais d’itinérance internationale</p> <p>Frais de services à valeur ajoutée</p> <p>Frais totaux</p> <p>TOTAL À PAYER</p> <p>Condition sur le champ Frais de services Ajoutés de valeur</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Frais d’appel</li>
     <li>Frais de conférence téléphonique</li>
     <li>Frais de SMS </li>
     <li>Frais d’Internet mobile</li>
     <li>Frais d’itinérance nationale</li>
     <li>Frais d’itinérance internationale</li>
     <li>Frais de services à valeur ajoutée</li>
     <li>Total des frais (champ calculé à partir des frais d’utilisation)</li>
     <li>TOTAL PAYABLE (champ de calcul usagecharges)</li>
    </ul> <p>Tableau - factures</p> </td>
   <td>Aucun champ</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Appels détaillés - Sortants</td>
   <td><p>Noms des colonnes :</p>
    <ul>
     <li>Date</li>
     <li>Heure</li>
     <li>Nombre</li>
     <li>Durée</li>
     <li>Frais</li>
    </ul> </td>
   <td><p>Toutes les valeurs</p> <p>Tableau - appels</p> </td>
   <td>Aucun champ</td>
   <td>—</td>
  </tr>
  <tr>
   <td>Payez maintenant</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Services à valeur ajoutée</td>
   <td>—</td>
   <td>—</td>
   <td>—</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>

