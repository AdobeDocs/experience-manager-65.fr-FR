---
title: Groupes et privilèges AEM Forms sur OSGi
description: Affecter des utilisateurs et des utilisatrices à des groupes pour gérer Adobe Experience Manager (AEM) Forms sur OSGi
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
docset: aem65
role: Admin,User
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 100%
---
# Groupes et privilèges AEM Forms sur OSGi{#aem-forms-on-osgi-groups-and-privileges}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquer ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/forms-groups-privileges-tasks.html?lang=fr) |
| AEM 6.5 | Cet article |

Vous pouvez [créer des groupes](/help/sites-administering/user-group-ac-admin.md#group-administration) et affecter des politiques et des [utilisateurs et utilisatrices](/help/sites-administering/user-group-ac-admin.md#user-administration) aux groupes dans Adobe Experience Manager (AEM). Ces politiques contrôlent les privilèges des utilisateurs et des utilisatrices qui font partie du groupe.

Une fois que vous avez installé le [package du module complémentaire AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), les groupes mentionnés dans cet article, tels que forms-user et forms-power-user, sont automatiquement disponibles pour affectation. Le tableau suivant répertorie les tâches qu’une personne peut effectuer pour AEM Forms sur OSGi en fonction des affectations de groupe :

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
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Créer, prévisualiser, publier et soumettre des formulaires adaptatifs</li> 
     <li>Créer, prévisualiser et publier des communications interactives et des fragments de document</li> 
     <li>Créer des scripts pour les formulaires adaptatifs à l’aide d’un éditeur de code</li> 
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
   <td>template-authors <sup>[2]</sup></td> 
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
     <li>Accéder aux lettres ou aux communications interactives de Correspondence Management à l’aide de l’interface utilisateur de l’agent</li> 
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
     <li>Utiliser les applications de boîte de réception AEM<br /> <strong>Remarque :</strong> vous devez disposer des affectations de groupe cm-agent-users et workflow-users pour accéder à l’interface utilisateur de l’agent de communication interactive dans la boîte de réception AEM.</li> 
     <li>Gérer les instances de workflow</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>Configurer PDF Generator</li> 
     <li>Configurer le dossier de contrôle</li> 
     <li>Gérer les applications de processus</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. L’utilisateur disposant des privilèges de groupe forms-user ne peut pas écrire de scripts pour les formulaires adaptatifs.
1. L’utilisateur disposant des privilèges template-authors ne peut pas écrire de scripts pour les modèles.
