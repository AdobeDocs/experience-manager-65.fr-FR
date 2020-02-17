---
title: Utilisation des propriétés de contenu pour exporter du contenu
seo-title: Utilisation des propriétés de contenu pour exporter du contenu
description: La page suivante présente les propriétés et les noeuds de l’application.
seo-description: La page suivante présente les propriétés et les noeuds de l’application.
uuid: 73f1832f-e457-47d0-a0e1-80af90897d31
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: a3006835-b1d2-47d6-959a-cdb692e34e1e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utilisation des propriétés de contenu pour exporter du contenu{#using-content-properties-to-export-content}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les applications sont représentées par *cq:Pages* dans AEM.

Ils partagent les mêmes propriétés communes que celles trouvées dans n’importe quel *cq:Page* , en plus des autres propriétés présentées ci-dessous qui représentent les propriétés de prise en charge de l’intégration.

## Propriétés d’application {#app-properties}

Le tableau suivant présente les propriétés de l’ **application et les noeuds**.

<table>
 <tbody>
  <tr>
   <td><strong>PropertyName</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>dps-cloudConfig</td>
   <td>Chaîne:Chemin</td>
   <td><p>Chemin d’accès à un service Mobile On-Demand Cloud configuré. Utilisé pour les actions à la demande d'AEM Mobile vers Mobile (appel d'API)</p> <p>Cette association est configurée via le volet Gérer la connexion lorsqu’un auteur choisit un service Mobile On-Demand Cloud pour associer l’application.</p> </td>
  </tr>
  <tr>
   <td>dps-exportTemplate</td>
   <td>Chaîne:Chemin</td>
   <td><p>Chemin d’accès aux configurations d’exportation de l’application. La configuration d'exportation est un dossier avec 2 modèles enfants de configuration d'exportation ContentSync ;</p> <p><i>dps-article</i>: Configuration de l’exportation ContentSync pour exporter le contenu d’un article</p> <p><i>dps-HTMLResources</i>: Configuration de l’exportation ContentSync pour exporter des ressources partagées d’application/article</p> </td>
  </tr>
  <tr>
   <td>dps-projectId</td>
   <td>Chaîne</td>
   <td><p>ID/URI du projet Mobile On-Demand auquel cette application est liée/liée.</p> <p>Cette association est configurée via le volet Gérer la connexion lorsqu’un auteur choisit le projet dans la liste des projets disponibles pour le service Cloud à la demande Mobile associé.</p> </td>
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
   <td>Date du dernier transfert des ressources partagées d'AEM vers AEM Mobile.</td>
  </tr>
  <tr>
   <td>dps-sharedHTMLResources-lastUploadedBy</td>
   <td>String:userid</td>
   <td>Identifiant de l'utilisateur qui a effectué le dernier transfert de la demande de ressources partagées d'AEM vers AEM Mobile.</td>
  </tr>
  <tr>
   <td>page-dashboard-config</td>
   <td>Chaîne:Chemin</td>
   <td>Chemin d’accès à une configuration de tableau de bord. Le chemin d’accès peut être redirigé vers une configuration de tableau de bord personnalisée, selon les besoins.</td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>Chaîne:Chemin</td>
   <td><p>Chemin d’accès à un composant cq:Component qui est ou étend <i>mobileapps/core/components/instance.</i></p> <p>Vous obtenez ainsi la visibilité et le rendu dans le catalogue des applications.</p> </td>
  </tr>
 </tbody>
</table>

Vous pouvez utiliser les propriétés ***du*** contenu pour créer du contenu. Reportez-vous aux ressources suivantes pour créer et exporter des articles et des ressources partagées :

* [Propriétés du contenu](/help/mobile/content-properties.md)
* [Création de la configuration d’exportation d’article](/help/mobile/creating-article-export-configuration.md)
* [Création de la configuration d&#39;exportation des ressources partagées](/help/mobile/creating-shared-resources-export-configuration.md)
