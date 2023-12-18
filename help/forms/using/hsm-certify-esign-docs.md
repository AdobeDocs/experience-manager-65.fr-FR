---
title: Utiliser HSM pour signer ou certifier des documents numériquement
description: Utilisez le serveur HSM ou le module eToken pour signer/certifier des documents PDF.
contentOwner: vishgupt
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
source-git-commit: 4a4a75018e960733908f40c631a24203290be55c
workflow-type: ht
source-wordcount: '655'
ht-degree: 100%

---

# Utiliser HSM pour signer ou certifier des documents numériquement {#use-hsm-to-digitally-sign-or-certify-documents}

Les modules de sécurité matérielle (HSM) et e-tokens sont des modules informatiques dédiés, sécurisés et résistants aux modifications, conçus pour gérer, traiter et stocker en toute sécurité des clés numériques. Ces modules sont directement associés à un ordinateur ou à un serveur réseau.

Adobe Experience Manager Forms peut utiliser les informations d&#39;identification stockées sur un HSM ou etoken en vue d&#39;être signé électroniquement ou appliquer les signatures numériques côté serveur à un document. Pour utiliser un module HSM ou etoken avec AEM Forms :

1. [Activez le service DocAssurance](#configuredocassurance).
1. [Créez un alias pour le module HSM ou etoken dans la console web AEM](#configuredeviceinaemconsole).
1. [Utilisez les API du service DocAssurance pour signer ou certifier les documents avec des clés numériques stockées sur le module](#programatically).

## Avant de configurer les modules HSM ou etoken avec AEM Forms  {#configurehsmetoken}

* Installez le [module complémentaire AEM Forms](Chttps://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
* Installez et configurez le logiciel client de HSM ou etoken sur le même ordinateur que le serveur AEM. Le logiciel client est nécessaire pour communiquer avec les modules HSM et e-token.

## Activer le service DocAssurance {#configuredocassurance}

Par défaut, le service DocAssurance n’est pas activé. Effectuez les étapes suivantes pour activer le service :

1. Arrêtez l’instance auteur de votre environnement AEM Forms. 

1. Ouvrez le fichier [AEM_root]\crx-quickstart\conf\sling.properties pour le modifier.

   >[!NOTE]
   >
   >Si vous avez utilisé le fichier [AEM_root]\crx-quickstart\bin\start.bat pour démarrer l’instance AEM, ouvrez le fichier [AEM_root]\crx-quickstart\sling.properties pour le modifier.

1. Ajoutez ou remplacez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.sun=sun.*,com.sun.*,sun.misc.*
   sling.bootdelegation.ibm=com.ibm.xml.*,com.ibm.*
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Enregistrez et fermez le fichier sling.properties.
1. Redémarrez l’instance AEM.

<!--

## Set up certificates for Reader extensions {#set-up-certificates-for-reader-extensions}

Perform the following steps to setup certificates:

1. Log in to AEM Author instance as an administrator.

1. Click **Adobe Experience Manager** on Global Navigation Bar. Go to **Tools** &gt;  **Security** &gt;  **Users**.
1. Click the **name** field of the user account. The **Edit User Settings** page opens.
1. On the AEM Author instance, certificates reside in a KeyStore. If you have not created a KeyStore earlier, click **Create KeyStore** and set a new password for the KeyStore. If the server already contains a KeyStore, skip this step.

1. On the **Edit User Settings** page, click **Manage KeyStore**.

1. On KeyStore Management dialog, expand the **Add Private Key from Key Store file** option and provide an alias. The alias is used to perform the Reader Extensions operation.
1. To upload the certificate file, click **Select Key Store File** and upload a `.pfx` file.
1. Add the **Key Store Password**,**Private Key Password**, and **Private Key Alias** that is associated with the certificate to the respective fields. Click **Submit**.

   >[!NOTE]
   >
   >To determine the **Private Key Alias** of a certificate, you can use the Java keytool command: `keytool -list -v -keystore [keystore-file] -storetype pkcs12`

   >[!NOTE]
   >
   >In the **Key Store Password** and **Private Key Password** fields, specify the password provided with the certificate file.

>[!NOTE]
>
>For AEM Forms on OSGi, to verify the signed PDF, the root certificate installed in the Trust Store.

>[!NOTE]
>
>On moving to production environment, replace your evaluation credentials with production credentials. Ensure that you delete your old Reader Extensions credentials, before updating an expired or evaluations credential.

-->


## Création d’un alias pour l’appareil  {#configuredeviceinaemconsole}

L&#39;alias contient l&#39;ensemble des paramètres dont a besoin un module HSM ou etoken. Suivez les instructions ci-dessous pour créer un alias pour les informations d&#39;identification de chaque module HSM ou etoken qu&#39;utilisent eSign ou les signatures numériques :

1. Ouvrez la console AEM. L’URL par défaut de la console AEM est https://&lt;host>:&lt;port>/system/console/configMgr
1. Ouvrez le **Service de configuration des informations d’identification HSM** et spécifiez les valeurs des champs suivants :

   * **Alias d’authentification** : spécifiez une chaîne utilisée pour identifier l’alias. Cette valeur est utilisée en tant que propriété pour certaines opérations de signatures numériques, comme l’opération de saisie du champ de signature.
   * **Chemin de la DLL** : spécifiez le chemin d’accès de la bibliothèque cliente de votre module HSM ou e-token sur le serveur. Par exemple, `C:\Program Files\LunaSA\cryptoki.dll`. Dans un environnement organisé en cluster, vous devez vous assurer que tous les serveurs du cluster utilisent un chemin identique.
   * **Code secret HSM** : indiquez le mot de passe requis pour accéder à la clé du module.
   * **Identifiant d’emplacement HSM** : indiquez un identifiant d’emplacement de type entier. L’ID d’emplacement est défini pour les clients de façon individuelle. Il est utilisé pour identifier l’emplacement sur le module HSM qui contient la clé privée pour signer/certifier.

   >[!NOTE]
   >
   >Lors de la configuration d’Etoken, entrez une valeur numérique pour le champ d’identifiant d’emplacement HSM. Une valeur numérique est nécessaire pour que les opérations de signature fonctionnent.

   * **Certificat SHA1** : indiquez la valeur SHA1 (empreinte numérique) du fichier de clé publique (.cer) pour les informations d’identification que vous utilisez. Veillez à ce que la valeur SHA1 ne contienne aucun espace.
   * **Type de module HSM** : sélectionnez l’éditeur du module HSM (Luna ou autre) ou eToken.

   Cliquez sur **Enregistrer**. Le module de sécurité matérielle est configuré pour AEM Forms. Désormais, vous pouvez utiliser le module de sécurité matérielle avec AEM Forms pour signer ou certifier des documents.

## Utiliser les API du service DocAssurance pour signer ou certifier un document avec des clés numériques stockées sur le module {#programatically}

L’exemple de code suivant utilise un module HSM ou e-token pour signer ou certifier un document.

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

Si vous avez effectué une mise à niveau à partir d’AEM 6.0 Forms ou AEM 6.1 Forms et que vous utilisiez le service DocAssurance dans la version précédente, alors :

* Pour utiliser le service DocAssurance sans module HSM ni e-token, continuez à utiliser le code existant.
* Pour utiliser le service DocAssurance avec un module HSM ou etoken, remplacez le code de l&#39;objet existant CredentialContext par l&#39;API indiquée ci-dessous.

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

Pour plus d’informations sur les API et un exemple de code du service DocAssurance, consultez [Utilisation des Services de document AEM par programmation](/help/forms/using/aem-document-services-programmatically.md).
