---
title: Stockage personnalisé pour le composant Drafts & Submissions
seo-title: Stockage personnalisé pour le composant Brouillons et envois
description: Découvrez comment personnaliser le stockage des données utilisateur pour les brouillons et les envois.
seo-description: Découvrez comment personnaliser le stockage des données utilisateur pour les brouillons et les envois.
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: 615b0db6da0986d7a74c42ec0d0e14bad7ede168
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 70%

---


# Stockage personnalisé pour les composants Drafts et Submissions {#custom-storage-for-drafts-and-submissions-component}

## Présentation {#overview}

AEM Forms vous permet d’enregistrer un formulaire sous forme de brouillon. La fonctionnalité de brouillon vous permet de mettre à jour un formulaire de travail en cours, que vous pouvez remplir et envoyer ultérieurement sur n’importe quel périphérique.

By default, AEM Forms stores the user data associated with the draft and submission of a form in the `/content/forms/fp` node on the Publish instance. En outre, les composants du portail AEM Forms fournissent des services de données, que vous pouvez utiliser pour personnaliser l’implémentation du stockage des données utilisateur pour les brouillons et les envois. Par exemple, vous pouvez stocker des données utilisateur dans un magasin de données.

## Conditions préalables  {#prerequisites}

* Activation des composants du portail de [formulaires](/help/forms/using/enabling-forms-portal-components.md)
* Create a [forms portal page](/help/forms/using/creating-form-portal-page.md)
* Activation des formulaires [adaptatifs pour le portail de formulaires](/help/forms/using/draft-submission-component.md)
* Découvrez les détails de [mise en oeuvre de l’enregistrement personnalisé](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Service de données de brouillon {#draft-data-service}

Pour personnaliser le stockage des données utilisateur pour les brouillons, vous devez implémenter toutes les méthodes de l’interface `DraftDataService`. L’exemple de code suivant décrit les méthodes et les arguments.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

>[!NOTE]
>
>La longueur minimale du champ ID de brouillon est de 26 caractères. L’Adobe recommande de définir la longueur du brouillon d’ID sur 26 caractères ou plus.

## Service Submission Data {#submission-data-service}

Pour personnaliser le stockage des données utilisateur pour les envois, vous devez implémenter toutes les méthodes de l’interface `SubmitDataService`. L’exemple de code suivant décrit les méthodes et les arguments.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

Le portail Forms utilise le concept d’identificateur unique universel (UUID) pour générer un identificateur unique pour chaque brouillon et formulaire envoyé. Vous pouvez également générer un identifiant unique de votre choix. Vous pouvez implémenter l’interface FPKeyGeneratorService, remplacer ses méthodes et développer une logique personnalisée pour générer un identifiant unique personnalisé pour chaque brouillon et formulaire envoyé. En outre, définissez le rang de service de l’implémentation de génération d’ID personnalisé sur une valeur supérieure à 0. Cela garantit que l’implémentation personnalisée est utilisée à la place de l’implémentation par défaut.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Vous pouvez utiliser l’annotation ci-dessous pour augmenter le classement du service pour l’ID personnalisé généré avec le code ci-dessus :

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Pour utiliser l’annotation ci-dessus, importe les éléments suivants dans votre projet :

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```

