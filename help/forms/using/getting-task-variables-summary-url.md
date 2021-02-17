---
title: Obtention de variables de tâche dans l’URL de résumé
seo-title: Obtention de variables de tâche dans l’URL de résumé
description: Comment réutiliser les informations d’une tâche et générer une URL de résumé pour résumer ou décrire une tâche.
seo-description: Comment réutiliser les informations d’une tâche et générer une URL de résumé pour résumer ou décrire une tâche.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 96%

---


# Obtention de variables de tâche dans l’URL de résumé {#getting-task-variables-in-summary-url}

La page Résumé affiche des informations liées aux tâches. Cet article décrit comment vous pouvez réutiliser les informations liées aux tâches dans la page Résumé.

Dans cet exemple d’orchestration, un employé envoie un formulaire de demande de permission. Le formulaire d’application passe ensuite au responsable de l’employé pour approbation.

1. Créez un exemple de rendu HTML (html.esp) pour resourseType **Employees/PtoApplication**.

   Le rendu suppose que les propriétés suivantes sont définies sur le nœud :

   * ename
   * empid
   * reason
   * duration

   >[!NOTE]
   >
   >Ce rendu est le modèle de page de résumé.

   L’exemple de code suivant pour ce rendu est contenu dans :

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Modifiez l’orchestration pour extraire les quatre propriétés à partir des données de formulaire envoyées. Créez ensuite un nœud dans CRX de type **Employees/PtoApplication**, avec les propriétés renseignées.

   1. Créez un processus **create PTO summary** et utilisez-le comme sous-processus avant la tâche **Affecter une tâche** dans votre orchestration.
   1. Définissez **employeeName**, **employeeID**, **ptoReason**, **totalDays** et **nodeName** comme variables d’entrée dans votre nouveau processus. Ces variables seront transmises en tant que données de formulaire envoyées.

      Définissez également une variable de sortie **ptoNodePath** qui sera utilisée lors de la définition de l’URL de résumé.

   1. Dans le processus **create PTO summary**, utilisez le composant **set value** pour définir les détails d’entrée dans un mappage **nodeProperty**(**nodeProps**).

      Les clés de ce mappage doivent être identiques à celles définies dans votre rendu HTML à l’étape précédente.

      Ajoutez aussi une clé **sling:resourceType** avec la valeur **Employees/PtoApplication** dans le mappage.

   1. Utilisez le sous-processus **storeContent** du service **ContentRepositoryConnector** dans le processus **create PTO summary**. Ce sous-processus crée un nœud CRX.

      Il prend trois variables d’entrée :

      * **Chemin d’accès au dossier** : le chemin du dossier dans lequel le nouveau nœud CRX est créé. Définissez le chemin comme **/content**.
      * **Nom de nœud** : affectez la variable d’entrée nodeName à ce champ. Il s’agit d’une chaîne de nom de nœud unique.
      * **Type** de noeud : Définissez le type  **nt:unstructured**. La sortie de ce processus est nodePath. Le nodePath est le chemin CRX du nœud que vous venez de créer. Le nodePath serait la dernière sortie du processus de résumé **create PTO**.
   1. Transmettez les données de formulaire envoyées (**employeeName**, **employeeID**, **ptoReason** et **totalDays**) comme entrée du nouveau processus **create PTO summary**. Prenez la sortie comme **ptoSummaryNodePath**.


1. Définissez l’URL de résumé comme expression XPath contenant les détails du serveur avec **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Dans l’espace de travail AEM Forms, lorsque vous ouvrez une tâche, l’URL de résumé accède au nœud CRX et le rendu HTML affiche le résumé.

Il est possible de modifier la mise en page du résumé sans modifier le processus. Le rendu HTML affiche le résumé correctement.
