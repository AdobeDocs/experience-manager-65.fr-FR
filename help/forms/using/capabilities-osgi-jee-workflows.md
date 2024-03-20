---
title: Actions et fonctionnalités des processus AEM sur OSGi et des processus AEM Forms JEE
description: Actions et fonctionnalités des processus AEM sur OSGi et des processus AEM Forms JEE
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 97%

---

# Actions et fonctionnalités des processus AEM sur OSGi et des processus AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Boîte de réception AEM et espace de travail HTML {#aem-inbox-and-html-workspace}

Vous pouvez utiliser la boîte de réception AEM pour exécuter et surveiller les workflows AEM Forms sur OSGi. En revanche, l’espace de travail HTML vous permet d’exécuter et de surveiller les workflows AEM Forms JEE. Le tableau suivant vous aide à comprendre les différentes actions importantes disponibles dans la boîte de réception AEM pour les workflows AEM sur OSGi et dans l’espace de travail HTML pour les processus AEM Forms JEE.

<table>
 <tbody>
  <tr>
   <td>Actions</td>
   <td>Boîte de réception AEM</td>
   <td>Espace de travail HTML</td>
  </tr>
  <tr>
   <td>Démarrage d’un processus, d’une tâche ou d’une application de formulaire<br /> </td>
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
   <td>Notifications par e-mail</td>
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
   <td>Personnaliser les éléments de l’interface utilisateur</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Affectation d’une tâche à plusieurs utilisateurs ou utilisatrices</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
 </tbody>
</table>

## Workflows AEM axés sur les formulaires sur OSGi et workflows AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Les workflows AEM de formulaire sur OSGi et les workflows AEM Forms JEE (gestion des processus AEM Forms on JEE) ont un ensemble de fonctionnalités différent. Le tableau suivant vous aide à comprendre les fonctionnalités importantes disponibles dans les workflows AEM centrés sur les formulaires sur OSGi et les workflows AEM Forms on JEE :

<table>
 <tbody>
  <tr>
   <td>Fonctionnalités</td>
   <td>Processus AEM de formulaire sur OSGi<br /> </td>
   <td>Workflows AEM Forms JEE</td>
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
   <td>Prise en charge</td>
   <td>Prise en charge<br /> </td>
  </tr>
  <tr>
   <td>Modèles d’e-mail personnalisés</td>
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
   <td>Boucles dans un workflow</td>
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
   <td>Signature électronique (Adobe Sign)</td>
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
   <td>Effectuer le rendu de la tâche terminée en tant que formulaire adaptatif ou document PDF</td>
   <td>Pris en charge</td>
   <td>Pris en charge [4]</td>
  </tr>
  <tr>
   <td>Intégration à Correspondence Management</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
   <tr>
   <td>Passerelles, AUCUNE ATTENTE </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
   <tr>
   <td>Variables pour stocker les données </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Division ET, OU</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Avatar de l’utilisateur ou de l’utilisatrice</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Envoi d’un e-mail à la fin du workflow</td>
   <td>Pris en charge <sup>[7]</sup></td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Appeler un service web à partir d’un workflow</td>
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
   <td>Contrôle précis de la section détails du workflow</td>
   <td>Pris en charge</td>
   <td>Pas de prise en charge</td>
  </tr>
  <tr>
   <td>Service d’interrogation / de planification</td>
   <td>Disponible prêt à l’emploi</td>
   <td>Implémentation personnalisée requise</td>
  </tr>
  <tr>
   <td>Application Formulaires adaptatifs</td>
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
   <td>Exécuter Script</td>
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
   <td>Lancement d’un processus à l’aide des données de processus existantes<br /> </td>
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
   <td>Rechercher des modèles</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge<br /> </td>
  </tr>
  <tr>
   <td>Intégration à des applications tierces</td>
   <td>Pas de prise en charge <sup>[6]</sup></td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Pièces jointes de tâche pour application ou point de départ du workflow</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>E-mail de rappel</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Modification du titre à l’expiration de la tâche</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>E-mail relatif à la délégation de tâche et la demande de tâche</td>
   <td>Pas de prise en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Délégation entre des groupes séparés</td>
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
   <td>Non pris en charge.</td>
   <td>Non pris en charge.</td>
  </tr>
  <tr>
   <td>Titre dynamique</td>
   <td>Non pris en charge.</td>
   <td>Non pris en charge.</td>
  </tr>
    <tr>
   <td>Description dynamique</td>
   <td>Non pris en charge.</td>
   <td>Non pris en charge.</td>
  </tr>
 </tbody>
</table>

1. Vous pouvez utiliser les workflows AEM de formulaire sur OSGi pour signer un formulaire adaptatif rempli. Les processus AEM de formulaire sur OSGi prennent en charge la signature hors du formulaire. L’expérience de [signature dans le formulaire](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) n’est pas prise en charge.

1. Vous devez avoir accès à la boîte de réception AEM pour exécuter et surveiller les workflows AEM Forms sur OSGi et à l’espace de travail HTML pour exécuter et surveiller les workflows AEM Forms JEE.
1. Les services documentaires AEM Forms natifs sont disponibles pour les processus AEM de formulaire sur OSGi et les processus AEM Forms on JEE. AEM Workflow utilise des services documentaires natifs pour les processus AEM de formulaire sur OSGi et les workflows AEM Forms JEE (gestion des processus).
1. Les workflows AEM Forms JEE peuvent uniquement rendre un formulaire adaptatif. Ils ne prennent pas en charge le rendu d’un formulaire adaptatif comme document PDF.
1. Les workflows AEM Forms JEE n’ont pas d’étape distincte pour Adobe Sign. Vous avez besoin d’un formulaire adaptatif Adobe Sign pour les workflows AEM Forms JEE. Pour plus d’informations, voir la [documentation d’Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Vous pouvez utiliser l’étape [Appeler le service de modèle de données du formulaire](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) pour appeler un service web et publier ou récupérer des données à partir d’une application tierce.
1. Vous pouvez utiliser l’étape [Envoyer un e-mail](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) pour envoyer des e-mails.

## Différences entre les fonctionnalités de la boîte de réception AEM et l’application AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Deux des moyens principaux de lancer un workflow basé sur l’utilisation de Forms sont la [boîte de réception AEM](../../forms/using/manage-applications-inbox.md) et l’application AEM Forms. Les fonctionnalités de la boîte de réception AEM et de l’application AEM Forms sont cependant différentes. AEM boîte de réception fonctionne uniquement avec [Workflows basés sur l’utilisation de Forms](../../forms/using/aem-forms-workflow.md) pendant que l’application AEM Forms fonctionne avec les processus Forms et la gestion des processus.

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
