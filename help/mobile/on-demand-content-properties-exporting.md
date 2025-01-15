---
title: Utilisation des propriétés de contenu pour exporter du contenu
description: La page suivante affiche les propriétés et les nœuds de l’application.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 3%

---

# Utilisation des propriétés de contenu pour exporter du contenu{#using-content-properties-to-export-content}

{{ue-over-mobile}}

Les applications sont représentées sous la forme *cq:Pages* dans AEM.

Ils partagent les mêmes propriétés communes que celles de n’importe quel *cq:Page* en plus des autres affichées ci-dessous qui représentent les propriétés de prise en charge de l’intégration.

## Propriétés d’application {#app-properties}

Le tableau suivant présente **Propriétés et nœuds de l’application**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>String:Path</td>
   <td><p>Chemin d’accès à un Cloud Service On-Demand mobile configuré. Utilisé pour les actions d’AEM Mobile sur Mobile On-Demand (appel d’API)</p> <p>Cette association est configurée via la mosaïque Gérer la connexion lorsqu’un auteur choisit un Cloud Service Mobile On-Demand auquel associer l’application.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>Chemin d’accès aux configurations d’exportation de l’application. La configuration de l’exportation est un dossier avec 2 modèles de configuration d’exportation ContentSync enfants ;</p> <p><i>dps-article</i> : configuration de l’exportation ContentSync pour exporter le contenu de l’article</p> <p><i>dps-HTMLResources</i> : configuration de l’exportation de ContentSync pour exporter des ressources partagées d’application/d’article</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Chaîne</td>
   <td><p>ID/URI du projet Mobile On-Demand auquel cette application est liée.</p> <p>Cette association est configurée via la mosaïque Gérer la connexion lorsqu’un auteur sélectionne le projet dans une liste de projets disponibles pour le Cloud Service mobile à la demande associé.</p> </td>
  </tr>
  <tr>
   <td>dps-projectTitle</td>
   <td>Chaîne</td>
   <td>Titre de l’application.</td>
  </tr>
  <tr>
   <td>dps-resourceType</td>
   <td>Chaîne</td>
   <td>Type de contenu.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploaded</td>
   <td>Date</td>
   <td>Date du dernier chargement des ressources partagées d'AEM vers AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>Identifiant de l’utilisateur ayant effectué le dernier chargement de la demande de ressources partagées d’AEM vers AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>String:Path</td>
   <td>Chemin d’accès à une configuration de tableau de bord. Le chemin d’accès peut être redirigé vers une configuration de tableau de bord personnalisée, si nécessaire.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String:Path</td>
   <td><p>Chemin d’accès à un cq:Component qui est ou qui étend <i>mobileapps/core/components/instance.</i></p> <p>Cela permet d’assurer la présence et le rendu dans le catalogue d’applications.</p> </td>
  </tr>
 </tbody>
</table>

Vous pouvez utiliser ***Propriétés du contenu*** pour créer du contenu. Consultez les ressources suivantes pour créer et exporter des articles et des ressources partagées :

* [Propriétés du contenu](/help/mobile/content-properties.md)
* [Création de la configuration d’exportation d’articles](/help/mobile/creating-article-export-configuration.md)
* [Création d’une configuration d’exportation de ressources partagées](/help/mobile/creating-shared-resources-export-configuration.md)
