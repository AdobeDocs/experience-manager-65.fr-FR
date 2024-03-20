---
title: Personnaliser les services de données de brouillon et d’envoi
description: AEM Forms, par défaut, stocke les brouillons et les formulaires adaptatifs envoyés, dans un nœud par défaut de l’instance de publication. Cependant, vous pouvez configurer les services de données de brouillon et d’envoi d’AEM Forms pour personnaliser le stockage des brouillons et des formulaires adaptatifs envoyés.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 100%

---

# Personnaliser les services de données Drafts &amp; Submission {#customizing-draft-and-submission-data-services}

## Présentation {#overview}

AEM Forms permet aux utilisateurs et utilisatrices d’enregistrer un formulaire adaptatif en tant que brouillon. La fonctionnalité de brouillon permet aux utilisateurs et utilisatrices de conserver un formulaire en cours de création. Un utilisateur ou une utilisatrice peut ensuite remplir et envoyer le formulaire à tout moment à partir de n’importe quel appareil.

Par défaut, AEM Forms stocke les données utilisateur associées aux brouillons et aux envois sur l’instance de publication dans le nœud `/content/forms/fp`.

Cependant, les composants du Portail Formulaires AEM fournissent des services de données qui vous permettent de personnaliser l’implémentation du stockage des données utilisateur pour les brouillons et les envois. Vous pouvez, par exemple, stocker les données dans un magasin de données implémenté au sein de votre organisation.

Pour personnaliser le stockage des données utilisateur, vous devez implémenter les services de [données de brouillon](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) et de [données d’envoi](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Conditions préalables requises {#prerequisites}

* Activer des [composants Portail Formulaires](/help/forms/using/enabling-forms-portal-components.md)
* Créer une [page Portail Formulaires](/help/forms/using/creating-form-portal-page.md)
* Activer des [formulaires adaptatifs pour le Portail Formulaires](/help/forms/using/draft-submission-component.md)
* En savoir plus sur les [détails d’implémentation du stockage personnalisé](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Service de données de brouillon {#draft-data-service}

Pour personnaliser le stockage des données de brouillon utilisateur, vous devez fournir une implémentation pour toutes les méthodes de l’interface `DraftAFDataService`.

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
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") if there is update
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

## Service Submission Data {#submission-data-service}

Pour personnaliser le stockage des données d’envoi utilisateur, vous devez fournir une implémentation pour toutes les méthodes de l’interface `SubmittedAFDataService`.

Vous trouverez une description des méthodes et de leurs arguments dans l’exemple de code suivant de l’interface :

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
