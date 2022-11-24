---
title: Expiration des certificats des extensions de Reader et son impact
description: Expiration des certificats des extensions de Reader et son impact
exl-id: 4e14e0dc-f248-4f6e-a075-6012b6792d9d
source-git-commit: bbc8fdf2eb7dd35600e2e2a87550e9de557f0eb0
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 4%

---


# Expiration des certificats des extensions de Reader et son impact {#expiration-of-reader-extensions-certificates-and-its-impact}

Les clients Adobe Experience Manager Forms (AEM Forms) disposant de licences Adobe Managed Services ou On-premise Enterprise Base ont le droit d’utiliser le service Acrobat Reader DC Extensions. Le service permet à une entreprise de partager facilement des documents de PDF interactifs en étendant la fonctionnalité d’Acrobat Reader avec des droits d’utilisation supplémentaires. Le service ajoute des droits d’utilisation à un document de PDF et active des fonctionnalités qui ne sont pas disponibles lorsqu’un document de PDF est ouvert à l’aide de Adobe Acrobat Reader, telles que l’ajout de commentaires à un document, le remplissage de formulaires et l’enregistrement du document. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents définis avec des droits d’utilisation. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document de PDF dont les droits sont activés dans Acrobat Reader peut effectuer les opérations activées pour ce document.

Adobe tire parti d’une infrastructure à clé publique (PKI) pour émettre des certificats numériques à utiliser dans le cadre de l’activation de licences et de fonctionnalités. Adobe a émis des certificats sous l’autorité de certification &quot;Adobe Root CA&quot;, qui expirera le 7 janvier 2023. Une nouvelle autorité de certification, &quot;Adobe Root CA G2&quot; et des certificats basés sur la nouvelle autorité de certification sont désormais disponibles.

Les anciens certificats (certificats basés sur une &quot;autorité de certification racine d’Adobe&quot;) ne fonctionnent plus après le 7 janvier 2023. Adobe vous recommande de commencer à utiliser les nouveaux certificats — ceux basés sur &quot;Adobe Root CA G2&quot; — pour étendre vos documents PDF au plus tard le 7 janvier 2023.  Vous pouvez [obtenir de nouveaux certificats à partir du site web de licences d’Adobe](https://licensing.adobe.com/) ou prise en charge des Adobes.

Tous les documents de PDF, Reader étendu à l’aide des anciens certificats avant le 7 janvier 2023, y compris ceux téléchargés par vos clients, continueront à travailler avec tous les droits d’utilisation qui leur sont appliqués et ne nécessitent aucune mise à jour.

## Foire aux questions

**Q. Quelle est la différence entre un certificat racine d’Adobe et un certificat Acrobat Reader Extensions ? Le certificat racine d’Adobe dépend-il d’un certificat Acrobat Reader Extensions ? Ces deux certificats arrivent-ils à expiration en janvier 2023 ?**

A. L’autorité de certification racine de l’Adobe est l’autorité de certification à partir de laquelle un certificat Acrobat Reader Extensions est émis. Le 7 janvier 2023, &quot;Adobe Root CA&quot; et tous les certificats émis à partir de celui-ci expirent.

**Q. Une communication précédente de l’Adobe concernant l’expiration des certificats et l’impact sur l’utilisation/l’ouverture de PDF a-t-elle été envoyée ? Cette communication doit-elle être ignorée ?**
A. Sur la base d&#39;une réévaluation de la situation, tous les documents PDF étendus à l&#39;aide de certificats de production délivrés par l&#39;ancienne &quot;autorité de certification racine des Adobes&quot; avant le 7 janvier 2023 continuent à fonctionner sans changement après le 7 janvier 2023. Si vous avez déjà mis à jour vos PDF, l’expérience ne changera pas.


**Q. Qui dois-je contacter si j’ai d’autres questions ?**

A. Vous pouvez contacter [Prise en charge des Adobes](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) ou soulevez un ticket d’assistance.

**Q. Que se passe-t-il si je n’ai pas mis à jour mon certificat avant le 7 janvier 2023 ?**

A. Tous les documents PDF étendus à l’aide de certificats de production délivrés par l’ancienne &quot;autorité de certification racine des Adobes&quot; avant le 7 janvier 2023 continuent à fonctionner sans modification après le 7 janvier 2023. Les PDF étendus avec des certificats d’évaluation ne fonctionnent pas après la date d’expiration.

**Q. La description des nouveaux certificats est-elle différente de celle des anciens certificats ?**

A. La description des nouveaux certificats des extensions Acrobat Reader mentionne **G3-P24** comme nom du programme. Dans la description des anciens certificats (certificats basés sur &quot;Adobe Root CA&quot;), **P24** est mentionné comme nom du programme.

**Q. Comment obtenir les derniers certificats ?**

A. Tous les clients Forms autorisés (avec principale licence) peuvent télécharger les nouveaux certificats (certificats basés sur &quot;Adobe Root CA G2&quot;) à partir de la [Adobe Licensing Website](https://licensing.adobe.com/). Si vous ne parvenez pas à trouver le certificat sur le site web de licences Adobe, contactez [Prise en charge des Adobes](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=en#support) ou soulevez un ticket d’assistance.

**Q. Mes documents PDF étendus à l’aide de certificats émis par l’ancienne autorité de certification racine de l’Adobe (l’ancienne autorité de certification) continuent-ils à fonctionner après le 7 janvier 2023 ?**

R. Oui, tous les documents PDF étendus à l’aide de certificats de production délivrés par l’&quot;autorité de certification racine de l’Adobe&quot; (ancienne autorité de certification) avant le 7 janvier 2023 continuent à fonctionner sans modification après le 7 janvier 2023. Les documents PDF étendus avec des certificats d’évaluation ne fonctionnent plus au-delà de la date d’expiration.

**Q. Quelle version de Adobe Acrobat Reader est requise pour continuer à utiliser les documents de PDF étendus avec les certificats émis à partir de l’&quot;Adobe Root CA&quot; (l’ancienne autorité de certification) ?**

R. Adobe Acrobat Reader 2020 ou version ultérieure est requis pour utiliser des documents PDF étendus avec &quot;Adobe Root CA&quot; (l’ancienne autorité de certification). Il s’agit de la version prise en charge d’Acrobat Reader au moment de la publication de ce document. Si vous utilisez une [version d’Adobe Acrobat non prise en charge](https://helpx.adobe.com/fr/support/programs/eol-matrix.html), Adobe recommande que vous [télécharger et installer la dernière version de Adobe Acrobat Reader](https://get.adobe.com/fr/reader/).

**Q. Quelle version de Adobe Acrobat Reader est requise pour continuer à utiliser les documents PDF étendus avec les certificats délivrés par &quot;Adobe Root CA 2&quot; (la nouvelle autorité de certification) ?**

R. Adobe Acrobat Reader 2020 ou version ultérieure est requis pour utiliser les documents PDF étendus avec &quot;Adobe Root CA 2&quot; (la nouvelle autorité de certification). Si vous utilisez une [version de Adobe Acrobat Reader non prise en charge](https://helpx.adobe.com/support/programs/eol-matrix.html), Adobe recommande que vous [télécharger et installer la dernière version de Adobe Acrobat Reader](https://get.adobe.com/reader/).

**Q. Puis-je supprimer un ancien certificat d’extensions Acrobat Reader et en ajouter un nouveau sur un serveur Adobe Experience Manager Forms tout en continuant à utiliser l’alias existant ?**

R. Oui, vous pouvez supprimer un ancien certificat Acrobat Reader Extensions et en ajouter un nouveau avec l’alias existant sur un serveur Adobe Experience Manager Forms.

**Q. Puis-je conserver les certificats des extensions Acrobat Reader nouvelles et anciennes sur un serveur Adobe Experience Manager Forms ?**

R. Oui, vous pouvez conserver les deux certificats mais avec des alias différents sur un serveur Adobe Experience Manager Forms. Depuis le 7 janvier 2023, vous ne pouvez utiliser que le nouveau certificat pour étendre par Reader un document de PDF.

**Q. Puis-je importer le même certificat Acrobat Reader Extensions dans tous les environnements Adobe Experience Manager Forms ?**

R. Oui, le même certificat Acrobat Reader Extensions peut être utilisé dans plusieurs environnements.

**Q. Comment vérifier les droits d’utilisation appliqués à un document de PDF ?**

A. Vous pouvez utiliser la variable [getDocumentUsageRights](https://experienceleague.adobe.com/docs/experience-manager-65/forms/developer-reference/programming-aem-forms-jee/java-api-quick-start-code-examples/acrobat-reader-dc-extensions-service.html?lang=en#quick-start-soap-mode-retrieving-credential-information-using-the-java-api) API permettant de récupérer les informations sur les droits d’utilisation appliqués à un document de PDF.

**Q. Comment modifier le mot de passe d’un fichier de certificat Acrobat Reader Extensions ?**

A. Sous Microsoft Windows, pour modifier le mot de passe du certificat, installez le certificat à l’aide de Microsoft Management Console (MMC) et sélectionnez **Marquer la clé comme exportable**. Une fois installé, exportez le certificat avec une clé privée et utilisez un autre mot de passe pour le fichier PFX.


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

You can use the Trust Store Management pages to import a new credential. The Trust Store may contain more than one Reader Extensions credential. You must designate one of those credentials as the default Reader Extensions credential. The default credential is used when a Workbench user is unable to determine which credential to use during process creation. These rules apply to default credentials:

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

For example keytool -v -list -storetype pkcs12 -keystore 1005566.pfx where 1005566.pfx is the name of my pfx file

<!-- ### Remove usage rights from existing rights-enabled PDF documents

Remove usage rights from existing rights-enabled PDF documents before applying usage rights with latest credentials. You can remove the usage rights for a document by invoking the removeUsageRights API from within the docAssuranceServiceAPI. For detailed information, see [Remove Usage Rights](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

#### Apply the usage rights to PDF documents 

To apply usage rights in an AEM Forms on OSGi environment, Create custom OSGi service to usage rights to the documents. You can also create a servlet with a POST method to return the reader extended PDF to the user. For detailed instructions, see [Applying Reader Extensions](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).  -->
