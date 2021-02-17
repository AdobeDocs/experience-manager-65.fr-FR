---
title: Utiliser HSM pour signer ou certifier des documents numériquement
seo-title: Utiliser HSM pour certifier des documents signés électroniquement
description: Utiliser des modules HSM ou etoken pour certifier des documents signés électroniquement
seo-description: Utiliser des modules HSM ou etoken pour certifier des documents signés électroniquement
uuid: bbe057c1-6150-41f9-9c82-4979d31d305d
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 536bcba4-b754-4799-b0d2-88960cc4c44a
translation-type: tm+mt
source-git-commit: 35b2c9c8c79b3cc3d81e0b92ea17cd7d599fa7ee
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 86%

---


# Utiliser HSM pour signer ou certifier des documents numériquement {#use-hsm-to-digitally-sign-or-certify-documents}

Les modules de sécurité matérielle (HSM) et etokens sont des modules informatiques dédiés, sécurisés de manière renforcée et résistants aux modifications conçus pour gérer, traiter et stocker les clés numériques en toute sécurité. Ces modules sont directement associés à un ordinateur ou à un serveur réseau.

Adobe Experience Manager Forms peut utiliser les informations d’identification stockées sur un HSM ou etoken en vue d’être signé électroniquement ou appliquer les signatures numériques côté serveur à un document. Pour utiliser un module HSM ou etoken avec AEM Forms :

1. Activez le service DocAssurance.
1. Configurez les certificats avec l’extension Lecture.
1. Créez un alias pour le module HSM ou etoken dans la console Web AEM.
1. Utilisez les API du service DocAssurance pour signer ou certifier les documents avec les clés numériques stockées sur le module.

## Avant de configurer les modules HSM ou etoken avec AEM Forms{#configurehsmetoken} 

* Installez le [module complémentaire AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html).
* Installez et configurez le logiciel client du HSM ou etoken sur le même ordinateur que le serveur AEM Le logiciel client est requis pour communiquer avec les modules HSM et etoken.
* (Microsoft windows uniquement) Configurez la variable d’environnement JAVA_HOME_32 de façon à ce qu’elle pointe vers le répertoire d’installation de la version 32 bits du kit de développement Java 8 (JDK 8). Le chemin d’accès par défaut du répertoire est le suivant : C:\Program Files(x86)\Java\jdk&lt;version>
* (AEM Forms sur OSGi uniquement) installez le certificat racine dans le trust store. Cela est nécessaire pour vérifier le PDF signé 

>[!NOTE]
>
>Sous Microsoft Windows, les clients à 32 bits uniquement de LunaSA ou EToken sont pris en charge.

## Activer le service DocAssurance {#configuredocassurance}

Par défaut, le service DocAssurance n’est pas activé. Effectuez les étapes suivantes pour activer le service :

1. Arrêtez l’instance auteur de votre environnement AEM Forms. 

1. Ouvrez le fichier [AEM_root]\crx-quickstart\conf\sling.properties pour le modifier.

   >[!NOTE]
   >
   >Si vous avez utilisé le fichier [AEM_root]\crx-quickstart\bin\start.bat pour début de l’instance AEM, ouvrez le fichier [AEM_root]\crx-quickstart\sling.properties pour le modifier.

1. Ajoutez ou remplacez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Enregistrez et fermez le fichier sling.properties.
1. Redémarrez l’instance AEM.

## Configuration des certificats pour Reader Extensions {#set-up-certificates-for-reader-extensions}

Effectuez les étapes suivantes pour configurer des certificats :

1. Connectez-vous à l’instance Auteur AEM en tant qu’administrateur.

1. Cliquez sur **Adobe Experience Manager** dans la barre de navigation générale. Accédez à **Outils **> **Sécurité **> **Utilisateurs**.
1. Cliquez sur le champ **nom** du compte d’utilisateur. La page **Modifier les paramètres utilisateur** s’affiche.
1. Sur l’instance d’auteur AEM, les certificats résident dans un KeyStore. Si vous n’avez pas créé de KeyStore précédemment, cliquez sur **Créer KeyStore** et définissez un nouveau mot de passe pour le KeyStore. Si le serveur contient déjà un KeyStore, ignorez cette étape.

1. Sur la page **Modifier les paramètres utilisateur**, cliquez sur **Gérer le KeyStore**.

1. Dans la boîte de dialogue Gestion du KeyStore, développez l&#39;option **Ajouter la clé privée à partir du fichier Key Store** et fournissez un alias. L’alias est utilisé pour effectuer l’opération Reader Extensions.
1. Pour télécharger le fichier de certificat, cliquez sur **Sélectionner le fichier de stockage de clés** et téléchargez un fichier `.pfx`.
1. Ajoutez les **mot de passe du magasin de clés**, **mot de passe de la clé privée** et **alias de la clé privée** associés au certificat dans les champs respectifs. Cliquez sur **Envoyer**.

   >[!NOTE]
   >
   >Pour déterminer l&#39;alias de clé privée P **d&#39;un certificat, vous pouvez utiliser la commande Java keytool : `keytool -list -v -keystore [keystore-file] -storetype pkcs12`**

   >[!NOTE]
   >
   >Dans les champs **Mot de passe du magasin de clés** et **Mot de passe de la clé privée**, saisissez le mot de passe fourni avec le fichier de certificat.

>[!NOTE]
>
>Pour AEM Forms sur OSGi, pour vérifier le PDF signé, le certificat racine est installé dans le magasin d’approbations.

>[!NOTE]
>
>Pour passer à l’environnement de production, remplacez les informations d’identification d’évaluation par celles de production. Veillez à supprimer vos anciennes informations d’identification d’extensions de Reader avant de mettre à jour des informations d’identification expirées ou d’évaluation.

## Création d’un alias pour le périphérique{#configuredeviceinaemconsole} 

L’alias contient l’ensemble des paramètres dont a besoin un périphérique HSM ou etoken. Suivez les instructions ci-dessous pour créer un alias pour les informations d’identification de chaque module HSM ou etoken qu’utilisent eSign ou les signatures numériques :

1. Ouvrez la console AEM. L’URL par défaut de la console AEM est https://&lt;hôte>:&lt;port>/system/console/configMgr
1. Ouvrez le **Service de configuration des informations d’identification HSM** et spécifiez les valeurs des champs suivants :

   * **Alias d’authentification** : spécifiez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée en tant que propriété pour certaines opérations de signatures numériques, comme l’opération de saisie du champ de signature.
   * **Chemin du DLL** : spécifiez le chemin d’accès complet à la bibliothèque cliente de votre module HSM ou etoken sur le serveur. Par exemple, C:\Program Files\LunaSA\cryptoki.dll. Dans un environnement organisé en grappe, ce chemin d’accès doit être identique pour l’ensemble des serveurs de la grappe.
   * **Code secret HSM** : indiquez le mot de passe requis pour accéder à la clé du module.
   * **Id d’emplacement HSM** : indiquez un identifiant d’emplacement de type entier. L’ID d’emplacement est défini pour les clients de façon individuelle. Si vous enregistrez un second ordinateur sur une partition différente (par exemple, HSMPART2 sur le même module HSM), l’emplacement 1 est associé à la partition HSMPART2 pour ce client.

   >[!NOTE]
   >
   >Lors de la configuration d’Etoken, spécifiez une valeur numérique pour le champ d’ID d’emplacement HSM. Une valeur numérique est nécessaire pour que les opérations de signature fonctionnent.

   * **Certificat SHA1** : indiquez la valeur SHA1 (empreinte numérique) du fichier de clé publique (.cer) pour les informations d’identification utilisées. Veillez à ce que la valeur SHA1 ne contienne aucun espace. Si vous utilisez un certificat physique, cette valeur n’est pas requise.
   * **Type de module HSM** : sélectionnez l’éditeur du module HSM (Luna ou autre) ou eToken.

   Cliquez sur **Enregistrer**. Le module de sécurité matérielle est configuré pour AEM Forms. Désormais, vous pouvez utiliser le module de sécurité matérielle avec AEM Forms pour signer ou certifier des documents.

## Utiliser les API du service DocAssurance pour signer ou certifier un document avec des clés numériques stockées sur le module   {#programatically}

L’exemple de code suivant utilise HSM ou etoken pour signer ou certifier un document.

```java
/*************************************************************************
 *
 * ADOBE CONFIDENTIAL
 * ___________________
 *
 * Copyright 2014 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
package com.adobe.docassurance.samples;

import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;

import javax.jcr.Binary;
import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.api.SlingRepository;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.adobe.aemfd.docmanager.Document;
import com.adobe.fd.docassurance.client.api.DocAssuranceException;
import com.adobe.fd.docassurance.client.api.DocAssuranceService;
import com.adobe.fd.docassurance.client.api.DocAssuranceServiceOperationTypes;
import com.adobe.fd.docassurance.client.api.SignatureOptions;
import com.adobe.fd.signatures.client.types.exceptions.InvalidArgumentException;
import com.adobe.fd.signatures.pdf.inputs.CredentialContext;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferences;
import com.adobe.fd.signatures.pdf.inputs.DSSPreferencesImpl;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions;
import com.adobe.fd.signatures.pdf.inputs.UnlockOptions;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.PDFSignatureAppearanceType;
import com.adobe.fd.signatures.pdf.inputs.PDFSignatureAppearenceOptions.TextDirection;
import com.adobe.fd.signatures.pki.client.types.common.HashAlgorithm;
import com.adobe.fd.signatures.pki.client.types.common.RevocationCheckStyle;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.CRLPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.GeneralPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PKIPreferencesImpl;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferences;
import com.adobe.fd.signatures.pki.client.types.prefs.PathValidationPreferencesImpl;

/**
 * Digital signatures can be applied to PDF documents to provide a level of security. Digital signatures, like handwritten signatures, provide a means by which signers
 * identify themselves and make statements about a document. The technology used to digitally sign documents helps to ensure that both the signer and recipients are clear
 * about what was signed and confident that the document was not altered since it was signed.
 *
 * PDF documents are signed by means of public-key technology. A signer has two keys: a public key and a private key. The private key is stored in a user's credential that
 * must be available at the time of signing. The public key is stored in the user's certificate that must be available to recipients to validate the signature. Information
 * about revoked certificates is found in certificate revocation lists (CRLs) and Online Certificate Status Protocol (OCSP) responses distributed by Certificate Authorities (CAs).
 * The time of signing can be obtained from a trusted source known as a Timestamping Authority.
 *
 * The following Java code example digitally signs a PDF document that is based on a PDF file.
 * The alias that is specified for the security credential is secure, and revocation checking is performed.
 * Because no CRL or OCSP server information is specified, the server information is obtained from the certificate used to
 * digitally sign the PDF document
 *
 * PreRequisites - Digital certificate for signing the document has to be uploaded on Granite Key Store
 */

@Component
@Service(value=Sign.class)
public class Sign{
 @Reference
 private DocAssuranceService docAssuranceService;

 @Reference
    private SlingRepository slingRepository;

 @Reference
    private JcrResourceResolverFactory jcrResourceResolverFactory ;

 /**
  *
  * @param inputFile - path to the pdf document stored at JCR node
  * @param outputFile - path to the pdf document where the output needs to be stored
  * @throws IOException
  * @throws RepositoryException
  * @throws InvalidArgumentException
  * @throws DocAssuranceException
  */
 public void signExtend(String inputFile, String outputFile, String alias) throws IOException, RepositoryException, InvalidArgumentException, DocAssuranceException{

  Document inDoc = new Document(inputFile);
  Document outDoc = null;

  Session adminSession = null;
        ResourceResolver resourceResolver = null;
        try {

          /** resourceResolver with admin privileges to be passed to SignatureServiceAPI and Reader Extensions
          the resource resolver for signature options has to be corresponding to the user who has the signing certificate in his granite key store
          the resource resolver for signature options has to be corresponding to the user who has the credential for reader extension in his granite key store
          here we are using the same resource resolver
          */
          adminSession = slingRepository.loginAdministrative(null);
             resourceResolver = jcrResourceResolverFactory.getResourceResolver(adminSession);

             //retrieve specifications for each of the services, you may pass null if you don't want to use that service
             //as we don't want encryption in this case, passing null for Encryption Options
             //for encrypted document pass Unlock Options - see the method getUnlockOptions() below
    outDoc = docAssuranceService.secureDocument(inDoc, null, getSignatureOptions(alias,resourceResolver),null,null);
        }
  catch(Exception e){
   e.printStackTrace();
  }
        finally{
            /**
             * always close the PDFDocument object after your processing is done.
             */
            if(inDoc != null){
                inDoc.close();
            }
            if(adminSession != null && adminSession.isLive()){
                if(resourceResolver != null){
                    resourceResolver.close();
                }
                adminSession.logout();
            }
        }

        //flush the output document contents to JCR Node
  flush(outDoc, outputFile);

 }

 /**
  *
  * @param rr resource resolver corresponding to the user with the access to signing credential for the
  * given alias "allcertificatesanypolicytest11ee_new" in this case
  * @return SignatureOptions
  */
 private SignatureOptions getSignatureOptions(String alias, ResourceResolver rr){

  //create an instance of SignatureOptions
  SignatureOptions signatureOptions = SignatureOptions.getInstance();

  //set the operation you want to perform - SIGN/CERTIFY
  signatureOptions.setOperationType(DocAssuranceServiceOperationTypes.SIGN);

  //field to sign
  String fieldName = "Signature1" ;

        //Hash Algo to be used to compute digest the PDF document
        HashAlgorithm algo = HashAlgorithm.SHA384;

        //Reason for signing/certifying
        String reason = "Test Reason";

        //location of the signer
        String location = "Test Location";

        //contact info of the signer
        String contactInfo = "Test Contact";

        //Create a PDFSignatureAppearanceOptions object
        //and show date information
        PDFSignatureAppearenceOptions appOptions = new PDFSignatureAppearenceOptions(
                PDFSignatureAppearanceType.NAME, null, 1.0d, null, true, true,
                true, true, true, true, true, TextDirection.AUTO);

        signatureOptions.setSignatureFieldName(fieldName);
        signatureOptions.setAlgo(algo);
        signatureOptions.setContactInfo(contactInfo);
        signatureOptions.setLocation(location);
        signatureOptions.setSigAppearence(appOptions);
        signatureOptions.setReason(reason);
        signatureOptions.setDssPref(getDSSPreferences(rr));
        signatureOptions.setCredential(new CredentialContext(alias, rr, true));
  return signatureOptions;
 }

 private DSSPreferences getDSSPreferences(ResourceResolver rr){
  //sets the DSS Preferences
        DSSPreferencesImpl prefs = DSSPreferencesImpl.getInstance();
        prefs.setPKIPreferences(getPKIPreferences());
        GeneralPreferencesImpl gp = (GeneralPreferencesImpl) prefs.getPKIPreferences().getGeneralPreferences();
        gp.setDisableCache(true);
        return prefs;
    }

    private PKIPreferences getPKIPreferences(){
     //sets the PKI Preferences
        PKIPreferences pkiPref = new PKIPreferencesImpl();
        pkiPref.setCRLPreferences(getCRLPreferences());
        pkiPref.setPathPreferences(getPathValidationPreferences());
        return pkiPref;
    }

    private CRLPreferences getCRLPreferences(){
        //specifies the CRL Preferences
        CRLPreferencesImpl crlPrefs = new CRLPreferencesImpl();
        crlPrefs.setRevocationCheck(RevocationCheckStyle.CheckIfAvailable);
        crlPrefs.setGoOnline(true);
        return crlPrefs;
    }

    private PathValidationPreferences getPathValidationPreferences(){
     //sets the path validation preferences
        PathValidationPreferencesImpl pathPref = new PathValidationPreferencesImpl();
        pathPref.setDoValidation(false);
        return pathPref;

    }

    /**
     * sets Unlock Options for encrypted PDF
     */
    private UnlockOptions getUnlockOptions(){
        UnlockOptions unlockOptions = new UnlockOptions();
        //sets the Open Password for password encrypted PDF
        unlockOptions.setPassword("OpenPassword");

        //for Certificate Encrypted Document, set the alias of the credential uploaded in the user's key store
        //and corresponding resource resolver

        return unlockOptions;

    }
    /**
     * This method copies the data from {@code Document}, to the specified file at the given resourcePath.
     * @param doc
     * @param resourcePath
     * @throws IOException
     */
    private void flush(Document doc, String resourcePath) throws IOException {
   //extracts the byte data from Document
   byte[] output = doc.getInlineData();
   Binary opBin;
   Session adminSession = null;
      try {
         adminSession = slingRepository.loginAdministrative(null);

         //get access to the specific node
         //here we are assuming that node exists
           Node node = adminSession.getNode(resourcePath);

           //convert byte[] to Binary
           opBin = adminSession.getValueFactory().createBinary((InputStream)new ByteArrayInputStream(output));

           //set the Binary data value to node's jcr:data
           node.getNode("jcr:content").getProperty("jcr:data").setValue(opBin);
      } catch (RepositoryException e) {

      }
      finally{

       if(adminSession != null && adminSession.isLive()){
        try {
      adminSession.save();
      adminSession.logout();
     } catch (RepositoryException e) {

     }

             }
      }

  }
}
```

Si vous avez effectué la mise à niveau d’AEM 6.0 Forms ou AEM 6.1 Forms et que vous utilisiez le service DocAssurance dans la version précédente, alors :

* Pour utiliser le service DocAssurance sans module HSM ni etoken, continuez à utiliser le code existant.
* Pour utiliser le service DocAssurance avec un module HSM ou etoken, remplacez le code de l’objet existant CredentialContext par l’API indiquée ci-dessous.

```java
/**
  *
  * @param credentialAlias alias of the PKI Credential stored in CQ Key Store or
  * the alias of the HSM Credential configured using HSM Credentials Configuration Service.
  * @param resourceResolver corresponding to the user with the access to the key store and trust store.
  * @param isHSMCredential if the alias is corresponding to HSM Credential.
  */
 public CredentialContext(String credentialAlias, ResourceResolver resourceResolver, boolean isHSMCredential);
```

Pour en savoir plus sur les API et des exemples de code du service DocAssurance, consultez [Utilisation des Services de document AEM par programmation](/help/forms/using/aem-document-services-programmatically.md).
