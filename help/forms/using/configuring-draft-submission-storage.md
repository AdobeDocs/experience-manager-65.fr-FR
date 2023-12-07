---
title: Configurer des services de stockage pour les brouillons et les envois
description: Découvrez comment configurer le stockage des brouillons et des envois
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 34%

---

# Configurer des services de stockage pour les brouillons et les envois {#configuring-storage-services-for-drafts-and-submissions}

## Présentation {#overview}

Avec AEM Forms, vous pouvez stocker les éléments suivants :

* **Brouillons** : formulaire de travail en cours que les utilisateurs finaux remplissent et enregistrent pour une utilisation ultérieure, puis envoient ultérieurement.

* **Envois** : formulaires envoyés contenant les données fournies par l’utilisateur.

Les services de données et de métadonnées du portail AEM Forms prennent en charge les brouillons et les envois. Par défaut, les données sont stockées dans l’instance de publication, qui est ensuite répliquée par inverse vers l’instance d’auteur configurée afin d’être disponible pour infiltration sur d’autres instances de publication.

L’approche prête à l’emploi existante a pour préoccupation de stocker toutes les données sur l’instance de publication, y compris les données pouvant être des informations d’identification personnelles (PII).

Outre l’approche par défaut mentionnée ci-dessus, une autre implémentation est également disponible pour transférer directement les données de formulaire au traitement au lieu de les enregistrer localement. Les clients qui se préoccupent du stockage de données potentiellement sensibles sur l’instance de publication peuvent choisir l’autre implémentation dans laquelle les données sont envoyées à un serveur de traitement. Comme le traitement se produit sur l’instance d’auteur, il reste généralement dans une zone sécurisée.

>[!NOTE]
>
>Lorsque vous utilisez l’action d’envoi Forms Portal ou activez les données de stockage dans l’option de portail de formulaires dans un formulaire adaptatif, les données du formulaire sont stockées dans le référentiel AEM. Dans un environnement de production, il est recommandé de ne pas stocker des données de formulaire de brouillon ou envoyées dans le référentiel AEM. Au contraire, vous devez intégrer le composant de brouillons et d’envoi à un stockage sécurisé comme la base de données d’entreprise pour stocker des brouillons et des données de formulaires envoyés.
>
>Pour plus d’informations, voir [Exemple d’intégration d’un composant de brouillons et d’envois à la base de données](/help/forms/using/integrate-draft-submission-database.md).

## Configuration des services de brouillons et d’envois du portail Forms {#configuring-forms-portal-drafts-and-submissions-services}

Dans la configuration de la console web AEM (`https://[host]:'port'/system/console/configMgr`), cliquez pour ouvrir la **Configuration des brouillons et des envois sur le portail Formulaires** en mode modification.

Spécifiez les valeurs des propriétés en fonction de vos besoins, comme décrit ci-dessous :

### Services prêts à l’emploi pour stocker des données sur l’instance de publication {#out-of-the-box-services-to-store-data-on-publish-instance}

Les données sont répliquées à l’inverse vers l’instance d’auteur configurée.

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Valeur</th>
  </tr>
  <tr>
   <td>Service de données de brouillon du portail Forms (identifiant du service de données de brouillon )<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées de brouillon du portail Forms (identifiant du service de métadonnées de brouillon )<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de données d’envoi du portail Forms (identifiant du service de données d’envoi) (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées d’envoi du portail Forms (identifiant du service de métadonnées d’envoi) (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Services prêts à l’emploi pour stocker des données sur une instance de traitement à distance {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Les données sont directement transmises à une instance distante configurée

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Valeur</th>
  </tr>
  <tr>
   <td>Service de données de brouillon du portail Forms (identifiant du service de données de brouillon )<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées de brouillon du portail Forms (identifiant du service de métadonnées de brouillon )<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de données d’envoi du portail Forms (identifiant du service de données d’envoi) (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Service de métadonnées d’envoi du portail Forms (identifiant du service de métadonnées d’envoi) (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Outre la configuration spécifiée ci-dessus, fournissez des informations sur l’instance de traitement à distance configurée.

Dans la configuration de la console web AEM (`https://[host]:'port'/system/console/configMgr`), cliquez pour ouvrir le **Service des paramètres AEM DS** en mode modification. Dans la boîte de dialogue Service des paramètres d’AEM, fournissez des informations sur l’URL du serveur de traitement, le nom d’utilisateur du serveur de traitement et le mot de passe.

>[!NOTE]
>
>Un exemple de mise en oeuvre est également fourni pour le stockage des données utilisateur dans une base de données. Pour comprendre comment configurer les services de données et métadonnées afin de stocker les données utilisateur dans une base de données externe, consultez la section [Exemple d’intégration d’un composant brouillons et envois à la base de données](/help/forms/using/integrate-draft-submission-database.md).
