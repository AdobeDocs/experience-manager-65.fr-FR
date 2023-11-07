---
title: Obtention des variables de tâche dans l’URL de résumé
description: Comment réutiliser les informations sur une tâche et générer une URL de résumé pour résumer ou décrire une tâche.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 42%

---

# Obtention des variables de tâche dans l’URL de résumé {#getting-task-variables-in-summary-url}

La page Résumé affiche des informations liées aux tâches. Cet article décrit comment réutiliser les informations liées aux tâches dans la page de résumé.

Dans cet exemple d’orchestration, un employé envoie un formulaire de demande de permission. Le formulaire de demande est ensuite transmis au responsable de l’employé pour approbation.

1. Création d’un exemple de moteur de rendu de HTML (html.esp) pour resourseType **Employees/PtoApplication**.

   Le moteur de rendu suppose que les propriétés suivantes soient définies sur le noeud :

   * ename
   * empid
   * reason
   * durée

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

1. Modifiez l’orchestration pour extraire les quatre propriétés à partir des données de formulaire envoyées. Ensuite, créez un noeud dans CRX de type **Employees/PtoApplication**, avec les propriétés renseignées.

   1. Création d’un processus **create PTO summary** et l’utiliser comme sous-processus avant la **Assign Task** dans votre orchestration.
   1. Définissez **employeeName**, **employeeID**, **ptoReason**, **totalDays** et **nodeName** comme variables d’entrée dans votre nouveau processus. Ces variables seront transmises en tant que données de formulaire envoyées.

      Définition également d’une variable de sortie **ptoNodePath** qui est utilisé lors de la définition de l’URL de résumé.

   1. Dans le processus **create PTO summary**, utilisez le composant **set value** pour définir les détails d’entrée dans un mappage **nodeProperty**(**nodeProps**).

      Les clés de ce mappage doivent être identiques à celles définies dans votre moteur de rendu de HTML à l’étape précédente.

      Ajoutez également une **sling:resourceType** clé avec valeur **Employees/PtoApplication** sur la carte.

   1. Utilisez le sous-processus **storeContent** du service **ContentRepositoryConnector** dans le processus **create PTO summary**. Ce sous-processus crée un noeud CRX.

      Il prend trois variables d’entrée :

      * **Chemin d’accès au dossier** : le chemin du dossier dans lequel le nouveau nœud CRX est créé. Définissez le chemin en tant que **/content**.
      * **Nom de nœud** : affectez la variable d’entrée nodeName à ce champ. Il s’agit d’une chaîne de nom de nœud unique.
      * **Type de nœud :** définissez le type comme **nt:unstructured**. La sortie de ce processus est nodePath. Le nodePath est le chemin CRX du nœud que vous venez de créer. Le nodePath serait la sortie finale de la variable **create PTO** processus de résumé.

   1. Transmettre les données de formulaire envoyées (**employeeName**, **employeeID**, **ptoReason**, et **totalDays**) comme entrée du nouveau processus. **create PTO summary**. Prendre la sortie comme **ptoSummaryNodePath**.

1. Définissez l’URL de résumé en tant qu’expression XPath contenant les détails du serveur avec **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

Dans l’espace de travail AEM Forms, lorsque vous ouvrez une tâche, l’URL de résumé accède au noeud CRX et le moteur de rendu de HTML affiche le résumé.

Il est possible de modifier la mise en page du résumé sans modifier le processus. Le moteur de rendu de HTML affiche le résumé de manière appropriée.
