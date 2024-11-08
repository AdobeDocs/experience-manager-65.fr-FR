---
title: Utilisation des propriétés de contenu pour exporter du contenu
description: La page suivante présente les propriétés et les noeuds de l’application.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: db1c33c9-8539-436d-b4d0-3d5e6fd688ed
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 9%

---

# Utilisation des propriétés de contenu pour exporter du contenu{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les applications sont représentées sous la forme *cq:Pages* dans AEM.

Ils partagent les mêmes propriétés communes que celles trouvées dans tout *cq:Page* en plus des autres propriétés affichées ci-dessous qui représentent les propriétés de prise en charge de l’intégration.

## Propriétés d’application {#app-properties}

Le tableau suivant affiche les **propriétés et noeuds de l’application**.

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
   <td><p>Chemin d’accès à un Cloud Service Mobile On Demand configuré. Utilisé pour les actions AEM Mobile vers Mobile On Demand (appel API)</p> <p>Cette association est configurée via la mosaïque Gérer la connexion lorsqu’un auteur choisit un Cloud Service Mobile On-Demand auquel associer l’application.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>String:Path</td>
   <td><p>Chemin des configurations d’exportation de l’application. La configuration d’exportation est un dossier avec 2 modèles de configuration d’exportation ContentSync enfants ;</p> <p><i>dps-article</i> : configuration d’exportation ContentSync pour exporter le contenu d’article</p> <p><i>dps-HTMLResources</i> : configuration de l'export ContentSync pour exporter des ressources partagées d'application/d'article</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Chaîne</td>
   <td><p>Identifiant/URI du projet Mobile On-Demand auquel cette application est liée/liée.</p> <p>Cette association est configurée via la mosaïque Gérer la connexion lorsqu’un auteur sélectionne le projet dans la liste des projets disponibles pour le Cloud Service Mobile On-Demand associé.</p> </td>
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
   <td>Date du dernier chargement des ressources partagées depuis AEM vers AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>Chaîne : userid</td>
   <td>Identifiant de l’utilisateur qui a effectué le dernier chargement de requête de ressources partagées depuis AEM vers AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>String:Path</td>
   <td>Chemin d’accès à une configuration de tableau de bord. Le chemin peut être redirigé vers une configuration de tableau de bord personnalisée, si nécessaire.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>String:Path</td>
   <td><p>Chemin d’accès à un cq:Component qui est ou étend <i>mobileapps/core/components/instance.</i></p> <p>Cela permet d’assurer la présence et le rendu dans le catalogue d’applications.</p> </td>
  </tr>
 </tbody>
</table>

Vous pouvez utiliser ***Propriétés du contenu*** pour créer du contenu. Reportez-vous aux ressources suivantes pour créer et exporter des articles et des ressources partagées :

* [Propriétés du contenu](/help/mobile/content-properties.md)
* [Création d’une configuration d’exportation d’article](/help/mobile/creating-article-export-configuration.md)
* [Création de la configuration de l&#39;export des ressources partagées](/help/mobile/creating-shared-resources-export-configuration.md)
