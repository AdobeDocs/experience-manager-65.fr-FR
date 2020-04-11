---
title: Personnalisation de la liste des instances de processus
seo-title: Personnalisation de la liste des instances de processus
description: Comment personnaliser les propriétés affichées dans une instance de processus de l’espace de travail AEM Forms.
seo-description: Comment personnaliser les propriétés affichées dans une instance de processus de l’espace de travail AEM Forms.
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personnalisation de la liste des instances de processus {#customizing-the-listing-of-process-instances}

La liste des instances de processus est affichée dans l’onglet Suivi de l’espace de travail AEM Forms.

Dans la liste des instances de processus, pour chaque instance de processus, l’espace de travail AEM Forms indique certaines propriétés de cette instance. Les propriétés suivantes sont disponibles pour chaque instance de processus. Ces propriétés sont stockées en tant qu’attributs dans le modèle du composant de l’instance de processus et peuvent être utilisées dans sa vue et son modèle.

<table>
 <tbody>
  <tr>
   <td><strong>Propriétés</strong></td>
   <td><strong>Commentaires</strong></td>
  </tr>
  <tr>
   <td>description</td>
   <td>Description de l’instance de processus.</td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>Nom de l’initiateur de l’instance de processus.</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>ID de l’initiateur de l’instance de processus.</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>Horodatage indiquant quand le processus s’est achevé.</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>Identifiant de l’instance de processus.</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = Initié<br /> 1 = En cours d’exécution<br /> 2 = Terminé<br /> 3 = En cours d’achèvement<br /> 4 = Interrompu<br /> 5 = En cours d’interruption<br /> 6 = Suspendu<br /> 7 = En cours de suspension<br /> 8 = En cours d’annulation de suspension</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>Nom du processus.</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>Horodatage indiquant quand le processus a commencé.</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>Tableau d’objets de variables de processus. Chaque objet de variable de processus contient les paramètres <strong>name</strong> (le nom de la variable de processus), <strong>value</strong> (la valeur de la variable de processus, et<strong> type</strong> (le type de la valeur de processus).</td>
  </tr>
 </tbody>
</table>

**Exemple:**

To display the `description` property of the process instance in the process instance card, perform the following steps.

1. Suivez la [Procédure générique de personnalisation de l’espace de travail AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Procédez comme suit :

   1. Copiez /libs/ws/js/runtime/templates/processinstance.html dans /apps/ws/js/runtime/templates/, s’il n’existe pas. Cliquez sur **Enregistrer tout**.
   1. Ajouter description du processus div avec class = &#39;processDescription&#39; inprocessinstance.html.

   ```
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. Procédez comme suit :

   1. Ouvrez /apps/ws/js/registry.js pour le modifier.
   1. Recherchez et remplacez `text!/lc/libs/ws/js/runtime/templates/processinstance.html`par `text!/lc/`**des applications **/ws/js/runtime/templates/processinstance.html.

1. Les changements ci-dessus peuvent nécessiter une mise à jour du fichier CSS en ajoutant une entrée dans la feuille de style /apps/ws/css/newStyle.css comme suit :

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
