---
title: Stockage personnalisé pour le composant Brouillons et envois
description: Découvrez comment personnaliser le stockage des données utilisateur pour les brouillons et les envois.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
feature: Forms Portal
exl-id: b1300eeb-2653-4bb5-b2fd-88048c9c43b9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 100%

---

# Stockage personnalisé pour le composant Brouillons et envois {#custom-storage-for-drafts-and-submissions-component}

## Présentation {#overview}

AEM Forms vous permet d’enregistrer un formulaire sous forme de brouillon. La fonctionnalité de brouillon vous permet de mettre à jour un formulaire de travail en cours, que vous pouvez remplir et envoyer ultérieurement sur n’importe quel appareil.

Par défaut, AEM Forms stocke les données utilisateur associées au brouillon et à l’envoi d’un formulaire dans le nœud `/content/forms/fp` de l’instance de publication. En outre, les composants du portail AEM Forms fournissent des services de données, que vous pouvez utiliser pour personnaliser l’implémentation du stockage des données utilisateur pour les brouillons et les envois. Par exemple, vous pouvez stocker des données utilisateur dans un magasin de données.

## Conditions préalables requises  {#prerequisites}

* Activer des [composants Portail Formulaires](/help/forms/using/enabling-forms-portal-components.md)
* Créer une [page Portail Formulaires](/help/forms/using/creating-form-portal-page.md)
* Activer des [formulaires adaptatifs pour le Portail Formulaires](/help/forms/using/draft-submission-component.md)
* En savoir plus sur les [détails d’implémentation du stockage personnalisé](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Service de données de brouillon {#draft-data-service}

Pour personnaliser le stockage des données utilisateur pour les brouillons, vous devez implémenter toutes les méthodes de l’interface `DraftDataService`. L’exemple de code suivant décrit les méthodes et les arguments.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null if there is creation
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
>La valeur minimale pour la longueur du champ d’ID du brouillon est de 26 caractères. Adobe recommande de définir la longueur de l’ID du brouillon sur 26 caractères ou plus.

## Service Submission Data  {#submission-data-service}

Pour personnaliser le stockage des données utilisateur pour les envois, vous devez implémenter toutes les méthodes de l’interface `SubmitDataService`.  L’exemple de code suivant décrit les méthodes et les arguments.

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

Le portail Formulaires utilise le concept d’identifiant universel unique (UUID) pour générer un ID unique pour chaque brouillon et formulaire envoyé. Vous pouvez également générer un ID unique de votre choix. Vous pouvez implémenter l’interface FPKeyGeneratorService, remplacer ses méthodes et développer une logique personnalisée pour générer un identifiant unique personnalisé pour chaque brouillon et formulaire envoyé. En outre, définissez le classement de service de l’implémentation de génération d’ID personnalisé sur une valeur supérieure à 0. Cela garantit que l’implémentation personnalisée est utilisée à la place de l’implémentation par défaut.

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

Pour utiliser l’annotation ci-dessus, importez les éléments suivants dans votre projet :

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```
