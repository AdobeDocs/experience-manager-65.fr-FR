---
title: Obtention des variables de tâche dans l’URL de résumé
description: Réutiliser les informations sur une tâche et générer une URL de résumé pour résumer ou décrire une tâche.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '431'
ht-degree: 100%

---

# Obtention des variables de tâche dans l’URL de résumé {#getting-task-variables-in-summary-url}

La page Résumé affiche des informations liées aux tâches. Cet article explique comment réutiliser les informations relatives aux tâches dans la page de résumé.

Dans cet exemple d’orchestration, un employé envoie un formulaire de demande de permission. Le formulaire de candidature est ensuite transmis à la personne responsable de l’employé pour approbation.

1. Créez un exemple de moteur de rendu HTML (html.esp) pour resourcesType **Employees/PtoApplication**.

   Le moteur de rendu suppose que les propriétés suivantes sont définies sur le nœud :

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

1. Modifiez l’orchestration pour extraire les quatre propriétés à partir des données de formulaire envoyées. Après cela, créez un nœud dans CRX de type **Employees/PtoApplication**, avec les propriétés renseignées.

   1. Créez un processus **create PTO summary** et utilisez-le comme sous-processus avant l’opération **Attribuer une tâche** dans votre orchestration.
   1. Définissez **employeeName**, **employeeID**, **ptoReason**, **totalDays** et **nodeName** comme variables d’entrée dans votre nouveau processus. Ces variables seront transmises en tant que données de formulaire envoyées.

      Définissez également une variable de sortie **ptoNodePath** qui est utilisée lors de la définition de l’URL de résumé.

   1. Dans le processus **create PTO summary**, utilisez le composant **set value** pour définir les détails d’entrée dans un mappage **nodeProperty**(**nodeProps**).

      Les clés de cette carte doivent être les mêmes que celles définies dans votre moteur de rendu HTML à l&#39;étape précédente.

      Ajoutez également une clé **sling:resourceType** avec une valeur **Employees/PtoApplication** dans la carte.

   1. Utilisez le sous-processus **storeContent** du service **ContentRepositoryConnector** dans le processus **create PTO summary**. Ce sous-processus crée un nœud CRX.

      Il faut trois variables d&#39;entrée :

      * **Chemin d’accès au dossier** : le chemin du dossier dans lequel le nouveau nœud CRX est créé. Définissez le chemin comme **/content**.
      * **Nom de nœud** : affectez la variable d’entrée nodeName à ce champ. Il s’agit d’une chaîne de nom de nœud unique.
      * **Type de nœud :** définissez le type comme **nt:unstructured**. La sortie de ce processus est nodePath. Le nodePath est le chemin CRX du nœud que vous venez de créer. Le ndoePath serait la sortie finale du processus de résumé **create PTO**.

   1. Transmettez les données du formulaire soumis (**employeeName**, **employeeID**, **ptoReason** et **totalDays**) comme entrée dans le nouveau processus **create PTO summary**. Prenez la sortie comme **ptoSummaryNodePath**.

1. Définissez l’URL de résumé en tant qu’expression XPath contenant les détails du serveur ainsi que **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Dans l’espace de travail AEM Forms, lorsque vous ouvrez une tâche, l’URL de résumé accède au nœud CRX et le moteur de rendu HTML affiche le résumé.

Il est possible de modifier la mise en page du résumé sans modifier le processus. Le moteur de rendu HTML affiche le résumé de manière appropriée.
