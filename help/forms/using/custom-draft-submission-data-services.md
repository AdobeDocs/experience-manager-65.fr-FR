---
title: Personnalisation des services de données Drafts & Submission
seo-title: Personnalisation des services de données Drafts & Submission
description: Par défaut, AEM Forms stocke des formulaires adaptatifs préliminaires (brouillons) et envoyés dans un nœud par défaut de l’instance de publication. Vous pouvez toutefois configurer les services Drafts & Submission d’AEM Forms afin de personnaliser le stockage des formulaires adaptatifs préliminaires et envoyés.
seo-description: Par défaut, AEM Forms stocke des formulaires adaptatifs préliminaires (brouillons) et envoyés dans un nœud par défaut de l’instance de publication. Vous pouvez toutefois configurer les services Drafts & Submission d’AEM Forms afin de personnaliser le stockage des formulaires adaptatifs préliminaires et envoyés.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 80%

---


# Personnalisation des services de données Drafts &amp; Submission {#customizing-draft-and-submission-data-services}

## Présentation {#overview}

AEM Forms permettent aux utilisateurs d’enregistrer un formulaire adaptatif en tant que brouillon. La fonctionnalité de brouillon offre aux utilisateurs la possibilité de conserver un formulaire de travail en cours. L’utilisateur peut ensuite remplir et envoyer le formulaire à tout moment, depuis n’importe quel périphérique.

Par défaut, AEM Forms stocke les données utilisateur associées au brouillon et à l’envoi sur l’instance de publication dans le noeud `/content/forms/fp`.

Cependant, les composants du portail AEM Forms fournissent des services de données qui vous permettent de personnaliser la mise en œuvre du stockage des données utilisateur pour les brouillons et les envois. Vous pouvez, par exemple, stocker les données dans un entrepôt de données implémenté au sein de votre entreprise.

Pour personnaliser le stockage des données utilisateur, vous devez implémenter les services de données [drafts](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) &amp; [submission](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Conditions préalables {#prerequisites}

* Activer [les composants du portail Forms](/help/forms/using/enabling-forms-portal-components.md)
* Créer une [page du portail de formulaires](/help/forms/using/creating-form-portal-page.md)
* Activer [les formulaires adaptatifs pour Forms Portal](/help/forms/using/draft-submission-component.md)
* Découvrez [les détails d&#39;implémentation de l&#39;enregistrement personnalisé](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Service de données de brouillon {#draft-data-service}

Pour personnaliser le stockage des données de brouillon, vous devez fournir une implémentation pour toutes les méthodes de l’interface `DraftAFDataService`.

Vous trouverez une description des méthodes et de leurs arguments dans l’échantillon de code suivant de l’interface : 

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## Service Submission Data   {#submission-data-service}

Pour personnaliser l’enregistrement des données d’envoi des utilisateurs, vous devez fournir une implémentation pour toutes les méthodes de l’interface `SubmittedAFDataService`.

Vous trouverez une description des méthodes et de leurs arguments dans l’échantillon de code suivant de l’interface : 

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```

