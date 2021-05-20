---
title: Actions et fonctionnalités des processus AEM sur OSGi et des processus AEM Forms JEE
description: Actions et fonctionnalités des processus AEM sur OSGi et des processus AEM Forms JEE
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 72%

---

# Actions et fonctionnalités des processus AEM sur OSGi et des processus AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Boîte de réception AEM et espace de travail HTML {#aem-inbox-and-html-workspace}

Vous pouvez utiliser AEM boîte de réception pour exécuter et surveiller les processus d’AEM Forms sur OSGi. En revanche, HTML Workspace vous permet d’exécuter et de surveiller les processus AEM Forms JEE. Le tableau suivant vous aide à comprendre diverses actions importantes disponibles dans AEM boîte de réception pour les processus d’AEM Forms sur OSGi et dans HTML Workspace pour les processus AEM Forms JEE.

<table>
 <tbody>
  <tr>
   <td>Actions</td>
   <td>Boîte de réception AEM</td>
   <td>Espace de travail HTML</td>
  </tr>
  <tr>
   <td>Démarrage d’un processus, d’une tâche ou d’une application de formulaire<br />  </td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Envoi de tâches</td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Affectation d’une tâche à un groupe</td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Envoi à plusieurs itinéraires</td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Suivi de l’historique des tâches et du récapitulatif des tâches</td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Notifications électroniques</td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Réaffectation de tâches</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Pièces jointes de champ pour les formulaires adaptatifs</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Vue Calendrier</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Commentaires de tâche</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Files d’attente (file d’attente personnelle partagée, réclamer des tâches de la file d’attente)</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Notification d’absence</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
    <tr>
   <td>Personnalisation des éléments de l’interface utilisateur</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Affectation d’une tâche à plusieurs utilisateurs</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
 </tbody>
</table>

## Processus AEM de formulaire sur OSGi et processus AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Les processus AEM de formulaire sur OSGi et les processus AEM Forms JEE (gestion des processus AEM Forms on JEE) ont un ensemble de fonctionnalités différent. Le tableau suivant vous aide à comprendre les fonctionnalités importantes disponibles dans les processus d’AEM basés sur l’utilisation de Forms on OSGi et les processus AEM Forms on JEE :

<table>
 <tbody>
  <tr>
   <td>Fonctionnalités</td>
   <td>Processus AEM de formulaire sur OSGi<br /> </td>
   <td>Processus AEM Forms JEE</td>
  </tr>
  <tr>
   <td>Formulaires adaptatifs</td>
   <td>Pris en charge</td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Intégration à d’autres solutions AEM</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Signature tactile</td>
   <td>Pris en charge</td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Modèles de courrier électronique personnalisés</td>
   <td>Pris en charge</td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Définition de la priorité des tâches</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Expiration d’une tâche après échéance</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Boucles dans un processus</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Choix dynamique d’une personne désignée </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Utilisation des métadonnées personnalisées</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Signature électronique (Adobe Sign)</td>
   <td>Pris en charge <sup>[1]</sup></td>
   <td>Pris en charge <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gérer les applications de tâche et de formulaire</td>
   <td>Pris en charge <sup>[2]</sup><br /> </td>
   <td>Pris en charge <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Services de document</td>
   <td>Pris en charge <sup>[3]</sup></td>
   <td>Pris en charge <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Effectuer le rendu de la tâche terminée en tant que formulaire ou document PDF</td>
   <td>Pris en charge</td>
   <td>Pris en charge [4]</td>
  </tr>
  <tr>
   <td>Intégration à Correspondence Management</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
   <tr>
   <td>Gateways, NO WAIT </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
   <tr>
   <td>Variables pour stocker des données </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Division OU ET</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Avatar de l’utilisateur</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Envoyer un courrier électronique à la fin du processus</td>
   <td>Pris en charge <sup>[7]</sup></td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Appeler un service Web à partir d’un processus</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Signature numérique</td>
   <td>Pris en charge<br /> </td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Bouton Réinitialiser</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Étapes de workflow</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Formulaires adaptatifs en lecture seule</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Masquage du bouton d’enregistrement par défaut</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Contrôle précis de la section détails de processus</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Service d’interrogation/de planification</td>
   <td>Disponible prêt à l’emploi</td>
   <td>Implémentation personnalisée requise</td>
  </tr>
  <tr>
   <td>Application Forms adaptative</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Incohérence affectant le service assembleur</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Service PDF Generator</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Service Forms</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Service Output</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Document Assurance</td>
   <td>Pris en charge</td>
   <td>Pris en charge </td>
  </tr>
  <tr>
   <td>Exécuter le script</td>
   <td>Prend en charge ECMAScript</td>
   <td>Prend en charge les fragments de code Java</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>  
  <tr>
   <td>Formulaires HTML5, formulaires PDF interactifs, jeu de formulaires</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Rapports de workflow</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Signature numérique</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Catégories de point de départ</td>
   <td>Pas de prise en charge </td>
   <td>Pris en charge </td>
  </tr>
  <tr>
   <td>Approbation de tâches en masse </td>
   <td>Pas de prise en charge </td>
   <td>Pris en charge </td>
  </tr>
  <tr>
   <td>Enregistrer le brouillon avec un nom personnalisé</td>
   <td>Pas de prise en charge </td>
   <td>Pris en charge </td>
  </tr>
  <tr>
   <td>Lancer un processus à l’aide des données de processus existantes<br /> </td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge </td>
  </tr>
  <tr>
   <td>Enregistrement d’un point de départ en tant que brouillon</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Vue Gestionnaire</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Rechercher dans les modèles</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Intégration à des applications tierces</td>
   <td>Non pris en charge <sup>[6]</sup></td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Pièces jointes de tâche pour application ou point de départ de processus</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Courrier électronique de rappel</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Modifier le titre à l’expiration de la tâche</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Courrier électronique relatif à la délégation de tâche et la demande de tâche</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Déléguer entre des groupes séparés</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Transformation XSLT</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Priorité des tâches dynamique</td>
   <td>Pas de prise en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Titre dynamique</td>
   <td>Pas de prise en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
    <tr>
   <td>Description dynamique</td>
   <td>Pas de prise en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
 </tbody>
</table>

1. Vous pouvez utiliser des processus d’AEM basés sur l’utilisation de Forms sur OSGi pour signer un formulaire adaptatif rempli. Les processus AEM de formulaire sur OSGi prennent en charge la signature hors du formulaire. L’expérience de [signature dans le formulaire](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) n’est pas prise en charge.

1. Vous avez besoin de l’accès à AEM Boîte de réception pour exécuter et surveiller les processus basés sur l’utilisation de Forms sur AEM Forms OSGi et Workspace HTML afin d’exécuter et de surveiller les processus AEM Forms JEE.
1. Les services documentaires AEM Forms natifs sont disponibles pour les processus AEM de formulaire sur OSGi et les processus AEM Forms on JEE. AEM Workflow utilise des services de document natifs pour les processus d’AEM basés sur l’utilisation de Forms on OSGi et AEM Forms JEE (Process Management).
1. Les processus AEM Forms JEE peuvent uniquement rendre un formulaire adaptatif. Ils ne prennent pas en charge le rendu d’un formulaire adaptatif comme document PDF.
1. Les processus AEM Forms JEE n’ont pas d’étape distincte pour Adobe Sign. Vous avez besoin d’un formulaire adaptatif Adobe Sign pour les processus AEM forms JEE. Pour plus d’informations, voir la [documentation d’Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Vous pouvez utiliser l’étape [Invoquer le service de modèle de données de formulaire](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) pour appeler un service Web et publier ou récupérer des données d’une application tierce.
1. Vous pouvez utiliser l’étape [Envoyer un email](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) pour envoyer des emails.

## Différences entre les fonctionnalités de la boîte de réception AEM et l’application AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Deux des méthodes principales pour lancer un workflow centré sur Forms utilisent [AEM Boîte de réception](../../forms/using/manage-applications-inbox.md) et l’application AEM Forms. Les fonctionnalités de la boîte de réception AEM et de l’application AEM Forms sont cependant différentes. AEM boîte de réception fonctionne uniquement avec les [workflows centrés sur Forms](../../forms/using/aem-forms-workflow.md) tandis que l’application AEM Forms fonctionne avec les workflows centrés sur Forms et la gestion des processus.

La table suivante répertorie les fonctionnalités de la boîte de réception AEM et de l’application AEM Forms :

<table>
 <tbody>
  <tr>
   <td><p><strong>Actions</strong></p> </td>
   <td><p><strong>Boîte de réception AEM</strong></p> </td>
   <td><p><strong>Application AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Démarrage d’une application de formulaire</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Envoi de tâches</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Délégation de tâches</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pas de prise en charge</p> </td>
  </tr>
  <tr>
   <td><p>Suivi de l’historique des tâches et du récapitulatif des tâches</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pas de prise en charge</p> </td>
  </tr>
  <tr>
   <td><p>Ajout de pièces jointes au niveau de la tâche</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Affichage de pièces jointes au niveau de la tâche</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Ajout de pièces jointes au niveau du champ</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Affichage de la vue de calendrier</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pas de prise en charge</p> </td>
  </tr>
  <tr>
   <td><p>Ajout de commentaires</p> </td>
   <td><p>Pris en charge</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
 </tbody>
</table>
