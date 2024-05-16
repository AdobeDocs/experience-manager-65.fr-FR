---
title: Expiration des certificats Reader Extensions et son impact
description: Expiration des certificats Reader Extensions et son impact
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1088'
ht-degree: 100%

---


# Expiration des certificats Reader Extensions et son impact {#expiration-of-reader-extensions-certificates-and-its-impact}

Les client(e)s Adobe Experience Manager Forms (AEM Forms) disposant de licences Adobe Managed Services ou On-premise Enterprise Base ont le droit d’utiliser le service Extensions d’Acrobat Reader DC. Le service permet à une organisation de partager facilement des documents PDF interactifs en optimisant la fonctionnalité d’Acrobat Reader avec des droits d’utilisation supplémentaires. Le service ajoute des droits d’utilisation à un document PDF et active des fonctionnalités qui ne sont généralement pas disponibles à l’ouverture d’un document PDF dans Adobe Acrobat Reader, comme l’ajout de commentaires dans un document, le remplissage de formulaires et l’enregistrement du document. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents définis avec des droits d’utilisation. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur ou une utilisatrice qui ouvre un document PDF dont les droits sont activés dans Acrobat Reader peut effectuer les opérations qui sont autorisées pour ce document.

Adobe exploite une infrastructure à clé publique (PKI) pour émettre les certificats numériques à utiliser dans le cadre de l’activation de licences et de fonctionnalités. Adobe a émis des certificats sous l’autorité de certification **Adobe Root CA**, qui arrivera à expiration le 7 janvier 2023. L’expiration de certificat n’a aucune incidence sur les documents PDF étendus utilisant des certificats de type Production émis à partir des certificats basés sur **Adobe Root CA** (anciens certificats). Tous les documents PDF dotés d’extensions Reader utilisant des anciens certificats avant le 7 janvier 2023, y compris ceux téléchargés par vos clientes et clients, continueront à fonctionner avec tous les droits d’utilisation qui leur sont appliqués et ne nécessitent aucune mise à jour.

Une nouvelle autorité de certification, **Adobe Root CA G2**, et des certificats basés sur la nouvelle autorité de certification sont désormais disponibles. Commencez à utiliser les nouveaux certificats avant ou à partir du 7 janvier 2023, ceux basés sur **Adobe Root CA G2**, pour doter vos nouveaux documents PDF de l’extension Reader.  Vous pouvez [obtenir de nouveaux certificats à partir du site Adobe Licensing Website](https://licensing.adobe.com/) ou de l’assistance d’Adobe.

## Foire aux questions

**Q. Quelle est la différence entre un certificat d’Adobe Root et un certificat Extensions d’Acrobat Reader ? Le certificat d’Adobe Root dépend-il d’un certificat Extensions d’Acrobat Reader ? Ces deux certificats arrivent-ils à expiration en janvier 2023 ?**

R. L’autorité de certification d’Adobe Root est l’autorité de certification à partir de laquelle un certificat Extensions d’Acrobat Reader est émis. Le 7 janvier 2023, « Adobe Root CA » et tous les certificats émis à partir de celui-ci expirent.

**Q. Une communication précédente d’Adobe concernant l’expiration des certificats et l’impact sur l’utilisation/l’ouverture de documents PDF a été envoyée. Cette communication doit-elle être ignorée ?**

R. Sur la base de la réévaluation de la situation, tous les documents PDF étendus à l’aide de certificats de production délivrés par l’ancienne autorité de certification « Adobe Root CA » avant le 7 janvier 2023 continueront à fonctionner sans changement après le 7 janvier 2023. Si vous avez déjà mis à jour vos documents PDF, l’expérience ne change pas.

**Q. Qui dois-je contacter si j’ai des questions supplémentaires ?**

R. Vous pouvez contacter l’[Assistance Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) ou créer un ticket d’assistance.

**Q. Que se passe-t-il si je n’ai pas mis à jour mon certificat avant le 7 janvier 2023 ?**

R. Tous les documents PDF étendus à l’aide de certificats de production délivrés par l’ancienne autorité de certification « Adobe Root CA » avant le 7 janvier 2023 continueront à fonctionner sans modification après le 7 janvier 2023. Les PDF étendus avec des certificats d’évaluation ne fonctionneront pas après la date d’expiration.

**Q. La description des nouveaux certificats est-elle différente de celle des anciens certificats ?**

R. La description des nouveaux certificats Extensions d’Acrobat Reader mentionne **G3-P24** comme nom du programme. Dans la description des anciens certificats (certificats basés sur « Adobe Root CA »), **P24** est mentionné comme nom du programme.

**Q. Comment obtenir les derniers certificats ?**

R. Tous les client(e)s Forms autorisé(e)s (avec une licence active) peuvent télécharger les nouveaux certificats (certificats basés sur « Adobe Root CA G2 ») à partir d’[Adobe Licensing Website](https://licensing.adobe.com/). Si vous ne parvenez pas à trouver le certificat sur Adobe Licensing Website, contactez l’[assistance d‘Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) ou ouvrez un ticket d’assistance.

**Q. Mes documents PDF étendus à l’aide de certificats émis par « Adobe Root CA » (l’ancienne autorité de certification) continuent-ils à fonctionner après le 7 janvier 2023 ?**

R. Oui, tous les documents PDF étendus à l’aide de certificats de production délivrés par « Adobe Root CA » (l’ancienne autorité de certification) avant le 7 janvier 2023, continueront à fonctionner sans modification après le 7 janvier 2023. Les documents PDF étendus avec des certificats d’évaluation ne fonctionneront plus au-delà de la date d’expiration.

**Q. Quelle version d’Adobe Acrobat Reader est requise pour continuer à utiliser les documents PDF étendus avec les certificats émis à partir de « Adobe Root CA » (l’ancienne autorité de certification) ?**

R. La version 2020 d’Adobe Acrobat Reader ou une version ultérieure est requise pour utiliser des documents PDF étendus avec « Adobe Root CA » (l’ancienne autorité de certification). Il s’agit de la version prise en charge par Acrobat Reader au moment de la publication de ce document. Si vous utilisez une [version d’Adobe Acrobat non prise en charge](https://helpx.adobe.com/fr/support/programs/eol-matrix.html), Adobe recommande que vous [téléchargiez et installiez la dernière version d’Adobe Acrobat Reader](https://get.adobe.com/fr/reader/).

**Q. Quelle version d’Adobe Acrobat Reader est requise pour continuer à utiliser les documents PDF étendus avec les certificats délivrés par « Adobe Root CA 2 » (la nouvelle autorité de certification) ?**

R. La version 2020 d’Adobe Acrobat Reader ou une version ultérieure est requise pour utiliser les documents PDF étendus avec « Adobe Root CA 2 » (la nouvelle autorité de certification). Si vous utilisez une [version d’Adobe Acrobat Reader non prise en charge](https://helpx.adobe.com/fr/support/programs/eol-matrix.html), Adobe recommande que vous [téléchargiez et installiez la dernière version d’Adobe Acrobat Reader](https://get.adobe.com/fr/reader/).

**Q. Puis-je supprimer un ancien certificat Extensions d’Acrobat Reader et en ajouter un nouveau sur un serveur Adobe Experience Manager Forms tout en continuant à utiliser l’alias existant ?**

R. Oui, vous pouvez supprimer un ancien certificat Extensions d’Acrobat Reader et en ajouter un nouveau avec l’alias existant sur un serveur Adobe Experience Manager Forms.

**Q. Puis-je conserver les nouveaux et les anciens certificats Acrobat Reader Extensions sur un serveur Adobe Experience Manager Forms ?**

R. Oui, vous pouvez conserver les deux certificats, mais avec des alias différents sur un serveur Adobe Experience Manager Forms. Après le 7 janvier 2023, vous ne pourrez utiliser que le nouveau certificat pour étendre Reader à un document PDF.

**Q. Puis-je importer le même certificat Extensions d’Acrobat Reader dans tous les environnements Adobe Experience Manager Forms ?**

R. Oui, le même certificat Extensions d’Acrobat Reader peut être utilisé dans plusieurs environnements.

**Q. Comment vérifier les droits d’utilisation appliqués à un document PDF ?**

R. Vous pouvez utiliser l’API [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=fr#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) pour récupérer les informations concernant les droits d’utilisation appliqués à un document PDF.

**Q. Comment modifier le mot de passe d’un fichier de certificat Extensions d’Acrobat Reader ?**

R. Sous Microsoft Windows, pour modifier le mot de passe du certificat, installez le certificat à l’aide de Microsoft Management Console (MMC) et sélectionnez **Marquer la clé comme exportable**. Une fois installé, exportez le certificat avec une clé privée et utilisez un autre mot de passe pour le fichier PFX.


<!-- 
## Applying the certificates {#obtaning-and-applying-the-certificates} 

You can choose one of the following paths to apply latest certificates:

* [Updating certificates for an AEM Forms on JEE environment](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment) 
* [Updating certificates for an AEM Forms on OSGi environment](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>The document uses the term certificates and credentials interchangeably.

### Pre-requisites {#Pre-requisites}

Updating the certificates requires using actions available on AEM Forms administrator console and Reader Extension APIs provided by AEM Forms. The document is intended for users and administrators with knowledge of using Adobe Experience Manger Forms APIs. Before you start, ensure that: 

* the user has administrator rights on underlying AEM Forms environment. 
* the user has setup the [development environment](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) and has access to it.
* [obtain the certificates](#obtain-the-certificates).


### Obtain the certificates {#obtain-the-certificates}

The Rights credential is delivered as a digital certificate that contains the public key, the private key, and the password used to access the credential.

If your organization purchases a production version of Reader Extensions, the production Rights credential is delivered by Adobe Licensing Website (LWS). A production Rights credential is unique to your organization and can enable the specific usage rights that you require.

If you obtained Reader Extensions through a partner or software provider who integrated Reader Extensions into their software, the Rights credential is provided to you by that partner who, in turn, receives this credential from Adobe.

>[!NOTE]
>
>The Rights credential cannot be used for typical document signing or assertion of identity. For these applications, you can use a self-sign certificate or acquire an identity certificate from a Certificate Authority (CA).

The following types of Rights credentials are available:

**Customer Evaluation**: A credential with a short validity period that is provided to customers who want to evaluate Reader Extensions. Usage rights applied to documents using this credential expire when the credential expires. This type of credential is valid only for two to three months.

**Production**: A credential with a long validity period that is provided to customers who purchased the full product. Production credentials are unique to each customer but can be installed on multiple systems.

If you have already used certificates to reader extend PDF files, download a production certificate from [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

### Applying certificates for an AEM Forms on JEE environment {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment} 

Applying new certificates on AEM Forms on JEE stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import and configure credentials 

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. Designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

* If you import a Reader Extensions credential and the Trust Store contains no other Reader Extensions credentials, it is set as the default.
* If you import a Reader Extensions credential with the Default option selected, the default type is removed from an existing default credential. The imported credential becomes the default.
* You cannot delete a default Reader Extensions credential. To delete the default credential, first set another credential as the default. An exception to this rule is that if there is only one credential, you can delete it even though it is the default.
* You cannot update a default Reader Extensions credential.

To import the credentials: 

1. In administration console, click Settings > Trust Store Management > Local Credentials.
1. Click Import and, under Trust Store Type, select Acrobat Reader DC extensions Credential.
1. (Optional) To indicate that this credential is the default credential to use with Acrobat Reader DC extensions, select Default.
1. In the Alias box, type an identifier for the credential. This identifier is used as the display name for the credential in Acrobat Reader DC extensions. This alias is also used to access the credential programmatically using the AEM forms SDK.
1. Click Choose File to locate the credential, type the password of the credential, and then click OK.

If the error message "Failed to import credential due to either incorrect file format, or incorrect password" appears, verify that the password is valid.

You can also import and delete credentials programmatically. (See [Programming with AEM forms](../../developing/credentials.md).)

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. AEM Forms on JEE provides APIs to remove usage rights. For detailed instructions, see [Removing Usage Rights from PDF Documents](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

To remove usage rights for AEM Forms on JEE processes developed in Workbench, see [Workbench Help](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf). 

#### Apply the usage rights to PDF documents 

After importing new credentials, you can apply usage rights to PDF documents using the Acrobat Reader DC extensions Java Client API and web service.  For details, see [Applying Usage Rights to PDF Documents](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents). 


### Applying certificates for an AEM Forms on OSGi environment {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

Applying new certificates on AEM Forms on OSGi stack requires importing new credentials and applying usage rights. You can use admin console to import credentials and AEM Forms Reader Extension APIs to apply usage rights. 

#### Import credentials {#Import-credentials}

In an AEM Forms on OSGi environment, a Reader Extension credential is associated with fd-service user. Before adding credentials for fd-user key store, perform the following steps to create a key store: 

1. Log in to your AEM Author instance as an Administrator.
1. Go to **[!UICONTROL Tools]**> **[!UICONTROL Security]**>**[!UICONTROL Users]**.
1. Scroll down the list of users until you find fd-service user account.
1. Click **[!UICONTROL fd-service]** user.
1. Click keystore tab.
1. Click **[!UICONTROL Create KeyStore]**.
1. Set the KeyStore Access Password and save your settings to create the KeyStore password.

After creating the key-store, add credentials to fd-service user. The following video explains the steps: 

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

The following command list the details of the pfx file. Before running the command, navigate to the directory that contains the .pfx file.

`keytool -v -list -storetype pkcs12 -keystore [name of your .pfx file]`

For example, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
