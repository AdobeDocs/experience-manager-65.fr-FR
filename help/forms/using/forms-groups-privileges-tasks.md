---
title: AEM Forms sur les groupes et privilèges OSGi
seo-title: AEM Forms sur les groupes et privilèges OSGi
description: Affecter des utilisateurs aux groupes pour gérer AEM Forms sur OSGi
seo-description: Affecter des utilisateurs aux groupes pour gérer AEM Forms sur OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 494551d3d886c1ed70d252a28b03cfa9d8e82a6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 78%

---


# AEM Forms sur les groupes et privilèges OSGi{#aem-forms-on-osgi-groups-and-privileges}

Vous pouvez [créer des groupes](/help/sites-administering/user-group-ac-admin.md#group-administration) et affecter des stratégies et des [utilisateurs](/help/sites-administering/user-group-ac-admin.md#user-administration) aux groupes dans AEM. Ces stratégies contrôlent les privilèges des utilisateurs qui font partie du groupe.

Once you install [AEM Forms add-on package](../../forms/using/installing-configuring-aem-forms-osgi.md), the groups mentioned in this article, such as forms-users and forms-power-user, are automatically available for assignment. Le tableau suivant répertorie les tâches qu’un utilisateur peut effectuer pour AEM Forms sur OSGi en fonction des affectations de groupe :

<table>
 <tbody>
  <tr>
   <td>Groupe</td> 
   <td>Tâches</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Créer, prévisualiser, publier et soumettre des formulaires adaptatifs</li> 
     <li>Créer, prévisualiser et publier des communications interactives et des fragments de document</li> 
     <li>Charger les ressources vers une instance AEM</li> 
     <li>Créer des thèmes</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-user</td> 
   <td>
    <ul> 
     <li>Créer, prévisualiser, publier et soumettre des formulaires adaptatifs</li> 
     <li>Créer, prévisualiser et publier des communications interactives et des fragments de document</li> 
     <li>Créer des scripts pour les formulaires adaptatifs à l’aide de l’éditeur de code</li> 
     <li>Charger des ressources, y compris des scripts</li> 
     <li>Créer des thèmes</li> 
     <li>Importer des packages contenant des données XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Examiner les envois</li> 
     <li>Approuver ou refuser des envois</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Créer et prévisualiser des formulaires adaptatifs ou des modèles de communication interactive</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Créer et modifier un modèle de données de formulaire</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Accéder aux lettres ou aux communications interactives de Correspondence Management à l’aide de l’interface utilisateur de l’agent</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>Créer une application de boîte de réception</li> 
     <li>Créer un modèle de processus</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>Utiliser AEM applications<br /> de boîte de réception <strong>Remarque : </strong>Pour accéder à l'interface utilisateur de l'agent de communications interactives dans AEM boîte de réception, vous devez disposer d'affectations de groupe cm-agent-users et de groupes workflow-users.</li> 
     <li>Gérer les instances de processus</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>Configurer PDF Generator</li> 
     <li>Configurer Watched folder</li> 
     <li>Gérer les applications de processus</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. L’utilisateur disposant de droits de groupe d’utilisateurs de formulaires ne peut pas écrire de scripts pour les formulaires adaptatifs.
1. L’utilisateur disposant des privilèges template-authors ne peut pas écrire de scripts pour les modèles.

