---
title: "Didacticiel\_: Planifier la communication interactive"
seo-title: Plan your Interactive Communication
description: Planifier la structure de votre communication interactive
seo-description: Plan the anatomy for your Interactive Communication
uuid: 1c2b5c5b-c655-4559-8748-3e0b343779c2
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 75b2d424-91d3-45b4-a5d7-fb49ab558582
feature: Interactive Communication
exl-id: ea0c8971-56f4-4094-87e4-1b222b73951f
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 26%

---

# Didacticiel : planifier la communication interactive {#tutorial-plan-the-interactive-communication}

Planifier la structure de votre communication interactive

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

Ce tutoriel fait partie de la série [Création de votre première communication interactive](/help/forms/using/create-your-first-interactive-communication.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et accomplir le cas d’utilisation complet du tutoriel.

La première étape de la planification d’une communication interactive consiste à finaliser le contenu de la communication interactive. Des experts spécialisés de services tels que le droit, les finances, le soutien ou le marketing peuvent vous aider à finaliser le contenu. Une fois le contenu finalisé, vous devez l’analyser afin d’identifier les différents types de ressources requis pour créer la communication interactive.

## Observations relatives à la planification {#planning-considerations}

Une communication interactive comprend les éléments suivants :

* **Texte statique** inclut principalement les parties de la communication interactive qui sont génériques par nature et qui sont incluses dans la communication à tous les clients. Par exemple, en-tête, pied de page, salutation ou clauses de non-responsabilité.
* **Données provenant d’un système principal (modèle de données de formulaire)** est spécifique au client et est fusionné dynamiquement avec la communication interactive. Par exemple, le numéro ou l’adresse de la stratégie peut être source à l’aide du modèle de données de formulaire.
* **Mise en page ou modèles** pour les versions d’impression et web de la communication interactive.
* **Commande** dans laquelle les différents paragraphes de texte apparaissent dans la communication interactive.
* Les **données saisies par un employé du front office (Interface utilisateur de l’agent**) qui personnalise la communication avant de l’envoyer. Par exemple, la date d’échéance du paiement.

* **Données conditionnelles** qui est renseigné en fonction de conditions prédéfinies. Par exemple, la date à laquelle la communication interactive est générée.
* **Images stockées dans un référentiel**, comme les logos et les images de signature. Les images telles que les logos de l’entreprise apparaissent dans la plupart ou dans toutes les communications interactives.
* **Tableaux et tableaux** requis pour simplifier la représentation de données complexes dans une communication interactive

## Anatomie de la communication interactive {#anatomy-of-the-interactive-communication}

Une fois que vous avez finalisé le contenu et les éléments utilisés pour créer votre communication interactive, vous pouvez créer une anatomie de la communication interactive. Les détails de l’anatomie doivent être répertoriés dans la variable [Observations relatives à la planification](/help/forms/using/planning-interactive-communications.md#planning-considerations) . En fonction de notre cas d’utilisation, voici un exemple d’anatomie de la facture mensuelle qu’un opérateur de télécommunications envoie à ses clients.

L’anatomie inclut des données avec les modes de saisie suivants :

* Du texte statique
* Modèle de données de formulaire
* Interface utilisateur de l’agent
* Données conditionnelles
* Images

Dans chaque section, le texte en gras représente le texte statique. La base de données comprend les tableaux des clients, des factures et des appels. Un modèle de données de formulaire peut recevoir des données de n’importe lequel de ces tableaux. Pour plus d’informations, voir [Créer un modèle de données de formulaire](/help/forms/using/create-form-data-model0.md).

Le tableau suivant illustre la source de données pour chaque champ de l’anatomie de la communication interactive :

<table>
 <tbody>
  <tr>
   <td>Section</td>
   <td>Du texte statique</td>
   <td>FDM </td>
   <td>Interface utilisateur de l’agent</td>
   <td>Images</td>
  </tr>
  <tr>
   <td>Informations de facturation</td>
   <td><p>Facture Non</p> <p>Date de facturation</p> <p>Période de facturation</p> <p>Votre plan</p> </td>
   <td><p>Valeur pour <strong>Votre plan </strong>field</p> <p>Table - customer</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Facture Non</li>
     <li>Date de facturation</li>
     <li>Période de facturation</li>
    </ul> <p> </p> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Détails du client</td>
   <td><p>Lieu de livraison</p> <p>Code d’état</p> <p>Numéro de mobile</p> <p>Autre numéro de contact</p> <p>Numéro de relation</p> <p>Nombre de connexions</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Nom</li>
     <li>Adresse</li>
     <li>Numéro de mobile</li>
     <li>Autre numéro de contact</li>
     <li>Numéro de relation</li>
    </ul> <p>Table - customer</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Lieu de livraison</li>
     <li>Code d’état</li>
     <li>Nombre de connexions</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Résumé de facturation</td>
   <td><p>Solde précédent</p> <p>Paiements</p> <p>Ajustements</p> <p>Facturation de la période de facturation actuelle</p> <p>Montant dû</p> <p>Échéance</p> </td>
   <td><p>Valeur du champ <strong>Facturation de la période en cours</strong></p> <p>Tableau - bills</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Solde précédent</li>
     <li>Paiements</li>
     <li>Ajustements</li>
     <li>Montant dû</li>
     <li>Échéance</li>
    </ul> </td>
   <td>--</td>
  </tr>
  <tr>
   <td>Récapitulatif des frais</td>
   <td><p>Frais d’appel</p> <p>Frais de conférence téléphonique</p> <p>Frais de SMS </p> <p>Frais Internet mobiles</p> <p>Frais d’itinérance nationale</p> <p>Frais d’itinérance internationale</p> <p>Frais de services à valeur ajoutée</p> <p>Frais totaux</p> <p>TOTAL À PAYER</p> <p>Champ Condition sur les frais de services à valeur ajoutée</p> </td>
   <td><p>Valeurs des champs suivants :</p>
    <ul>
     <li>Frais d’appel</li>
     <li>Frais de conférence téléphonique</li>
     <li>Frais de SMS </li>
     <li>Frais Internet mobiles</li>
     <li>Frais d’itinérance nationale</li>
     <li>Frais d’itinérance internationale</li>
     <li>Frais de services à valeur ajoutée</li>
     <li>Total des frais (champ calculé d’usagecharges)</li>
     <li>MONTANT TOTAL PAYABLE (champ calculé à partir des frais d’utilisation)</li>
    </ul> <p>Tableau - bills</p> </td>
   <td>Aucun champ</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Appels détaillés - Sortant</td>
   <td><p>Noms des colonnes :</p>
    <ul>
     <li>Date </li>
     <li>estimé</li>
     <li>Nombre</li>
     <li>Durée</li>
     <li>Frais</li>
    </ul> </td>
   <td><p>Toutes les valeurs</p> <p>Tableau - Appels</p> </td>
   <td>Aucun champ</td>
   <td>--</td>
  </tr>
  <tr>
   <td>Payer maintenant</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>PayNow</td>
  </tr>
  <tr>
   <td>Services à valeur ajoutée</td>
   <td>--</td>
   <td>--</td>
   <td>--</td>
   <td>ValueAddedServices</td>
  </tr>
 </tbody>
</table>
