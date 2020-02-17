---
title: Configuration des services de stockage pour les brouillons et les envois
seo-title: Configuration des services de stockage pour les brouillons et les envois
description: Découvrez comment configurer un stockage pour les brouillons et les envois
seo-description: Découvrez comment configurer un stockage pour les brouillons et les envois
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# Configuration des services de stockage pour les brouillons et les envois {#configuring-storage-services-for-drafts-and-submissions}

## Présentation {#overview}

Avec AEM Forms, vous pouvez stocker :

* **Brouillons** : formulaire de travail en cours que les utilisateurs finaux remplissent et enregistrent pour une utilisation ultérieure, puis envoient ultérieurement.

* **Envois** : formulaires envoyés contenant les données fournies par l’utilisateur.

Les services de données et de métadonnées d’AEM Forms Portal offrent la prise en charge des brouillons et des envois. Par défaut, les données sont stockées dans l’instance de publication, qui subit ensuite une réplication inversée sur l’instance d’auteur configurée afin d’être disponible pour infiltration sur d’autres instances de publication.

Le problème de l’approche prête à l’emploi existante est qu’elle stocke toutes les données sur une instance de publication, y compris les données personnelles.

Outre l’approche par défaut mentionnée ci-dessus, une autre mise en œuvre disponible consiste à transférer directement les données de formulaire à des fins de traitement, plutôt que de les enregistrer localement. Les clients qui sont préoccupés à l’idée de stocker des données potentiellement sensibles sur l’instance de publication peuvent choisir la solution alternative, dans laquelle les données sont envoyées à un serveur de traitement. Le traitement s’effectuant dans l’instance d’auteur, les données restent généralement dans un périmètre sécurisé.

>[!NOTE]
>
>Lorsque vous utilisez l’action d’envoi Forms Portal ou activez les données de stockage dans l’option de portail de formulaires dans un formulaire adaptatif, les données du formulaire sont stockées dans le référentiel AEM. Dans un environnement de production, il est recommandé de ne pas stocker des données de formulaire de brouillon ou envoyées dans le référentiel AEM. Au contraire, vous devez intégrer le composant de brouillons et d’envoi à un stockage sécurisé comme la base de données d’entreprise pour stocker des brouillons et des données de formulaires envoyés.
>
>Pour plus d’informations, voir [Exemple d’intégration d’un composant de brouillons et d’envois à la base de données](/help/forms/using/integrate-draft-submission-database.md).

## Configuration des services de brouillons et envois Forms Portal {#configuring-forms-portal-drafts-and-submissions-services}

In the AEM Web Console Configuration ( `https://[host]:[port]/system/console/configMgr`), click to open **Forms Portal Draft and Submission Configuration** in edit mode.

Indiquez les valeurs des propriétés en fonction de vos besoins comme décrit ci-dessous :

### Services de stockage de données sur l’instance de publication prêts à l’emploi {#out-of-the-box-services-to-store-data-on-publish-instance}

Les données subissent une réplication inversée sur l’instance d’auteur configurée.

<table>
 <tbody>
  <tr>
   <th>Propriétés</th>
   <th>Valeur</th>
  </tr>
  <tr>
   <td>Service de données de brouillon de Forms Portal (Identifiant du service de données de brouillon (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées de brouillon de Forms Portal (Identifiant du service de métadonnées de brouillon (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de données d’envoi de Forms Portal (Identifiant du service de données d’envoi (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées d’envoi de Forms Portal (Identifiant du service de métadonnées d’envoi (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Services de stockage de données sur l’instance de traitement à distance prêts à l’emploi {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Les données sont publiées directement sur l’instance à distance configurée

<table>
 <tbody>
  <tr>
   <th>Propriétés</th>
   <th>Valeur</th>
  </tr>
  <tr>
   <td>Service de données de brouillon de Forms Portal (service d’identification des données de brouillon (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées de brouillon de Forms Portal (Identifiant du service de métadonnées de brouillon (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de données d’envoi de Forms Portal (Identifiant du service de données d’envoi (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées d’envoi de Forms Portal (Identifiant du service de métadonnées d’envoi (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Outre la configuration spécifiée ci-dessus, fournissez les informations sur l’instance de traitement à distance configurée.

In the AEM Web Console Configuration ( `https://[host]:[port]/system/console/configMgr`), click to open **AEM DS Settings Service** in edit mode. Dans la boîte de dialogue de service des paramètres AEM DS, renseignez les informations sur l’URL du serveur de traitement, y compris le nom d’utilisateur et le mot de passe.

>[!NOTE]
>
>Un exemple de mise en œuvre est également fourni pour le stockage des données utilisateur dans une base de données. To understand how to configure data and metadata services to store user data in an external database, see [Sample for integrating drafts &amp; submissions component with database](/help/forms/using/integrate-draft-submission-database.md).

