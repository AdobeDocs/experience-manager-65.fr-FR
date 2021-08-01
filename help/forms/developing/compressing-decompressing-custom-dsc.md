---
title: Comment transmettre des informations d’identification à l’aide des en-têtes de sécurité du service Web ?
description: Découvrez comment transmettre des informations d’identification à l’aide des en-têtes WS-security
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Compression et décompression de fichiers à l’aide d’un DSC personnalisé d’AEM Forms on JEE {#compressing-decompressing-files}

## Connaissances préalables {#prerequisites}

Expérience avec la gestion des processus d’AEM Forms on JEE, la programmation Java de base et la création de composants personnalisés.

**Autres produits requis**

Éditeur Java tel que [Eclipse](https://www.eclipse.org/) ou [Netbeans IDE](https://netbeans.apache.org/)

## Niveau d’utilisateur {#user-level}

Intermédiaire

AEM Forms on JEE permet aux développeurs de créer un DSC (Document Service Container) personnalisé pour créer des fonctionnalités prêtes à l’emploi enrichies. La création de ces composants est enfichable dans l’environnement d’exécution d’AEM Forms on JEE et a la finalité prévue. Cet article explique comment créer un service ZIP personnalisé qui peut être utilisé pour compresser une liste de fichiers dans un fichier .zip et décompresser un fichier .zip en une liste de documents.

## Création d’un composant DSC personnalisé {#create-custom-dsc-component}

Créez un composant DSC personnalisé avec deux opérations de service pour compresser et décompresser la liste des documents. Ce composant utilise le package java.util.zip pour la compression et la décompression. Pour créer un composant personnalisé, procédez comme suit :

1. Ajoutez le fichier adobe-livecycle-client.jar à la bibliothèque .
1. Ajout des icônes requises
1. Création d’une classe publique
1. Créez deux méthodes publiques appelées UnzipDocument et ZipDocuments
1. Écrire la logique de compression et de décompression

Le code se trouve ici :

```java
/*
 * Custom DSC : ZIP Utility
 * Purpose: This is a LiveCycle ES2 custom component used to Compress & Decompress List of Documents
 * Author: Nithiyanandam Dharmadass
 * Organization: Ministry of Finance, Kingdom of Bahrain
 * Last modified Date: 18/Apr/2011
 */
package nith.lces2.dsc;

import java.util.zip.ZipEntry;
import java.util.zip.ZipInputStream;
import com.adobe.idp.Document;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.ArrayList;
import java.util.List;
import java.util.zip.ZipOutputStream;

public class ZIPService {

    static final int BUFFER = 2048; // 2MB buffer size

    public java.util.List UnzipDocument(com.adobe.idp.Document zipDocument) throws Exception {
        ZipInputStream zis = new ZipInputStream(zipDocument.getInputStream());

        ZipEntry zipFile;

        List resultList = new ArrayList();

        while ((zipFile = zis.getNextEntry()) != null) {

            ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();

            int count;  // an int variable to hold the number of bytes read from input stream
            byte data[] = new byte[BUFFER];
            while ((count = zis.read(data, 0, BUFFER)) != -1) {
                byteArrayOutStream.write(data, 0, count);   // write to byte array
            }

            com.adobe.idp.Document unzippedDoc = new Document(byteArrayOutStream.toByteArray());  // create an idp document
            unzippedDoc.setAttribute("file", zipFile.getName());
            unzippedDoc.setAttribute("wsfilename", zipFile.getName());  // update the wsfilename attribute
            resultList.add(unzippedDoc);
        }
        return resultList;  // List of uncompressed documents
    }

    public com.adobe.idp.Document ZipDocuments(java.util.List listOfDocuments,java.lang.String zipFileName) throws Exception {

        if (listOfDocuments == null || listOfDocuments.size() == 0) {
            return null;
        }

        ByteArrayOutputStream byteArrayOutStream = new ByteArrayOutputStream();
        ZipOutputStream zos = new ZipOutputStream(byteArrayOutStream);  // ZIP Output Stream

        for (int i = 0; i < listOfDocuments.size(); i++) {
            Document doc = (Document) listOfDocuments.get(i);
            InputStream docInputStream = doc.getInputStream();
            ZipEntry zipEntry = new ZipEntry(doc.getAttribute("file").toString());
            zos.putNextEntry(zipEntry);
            int count;
            byte data[] = new byte[BUFFER];
            while ((count = docInputStream.read(data, 0, BUFFER)) != -1) {
                zos.write(data, 0, count);  // Read document content and add to zip entry
            }
            zos.closeEntry();
        }
        zos.flush();
        zos.close();

        Document zippedDoc = new Document(byteArrayOutStream.toByteArray());
        if(zipFileName==null || zipFileName.equals(""))
        {
            zipFileName = "CompressedList.zip";
        }
        zippedDoc.setAttribute("file", zipFileName);
        return zippedDoc;
    }
}
```

## Création d’un fichier Component.XML {#create-component-xml-file}

Un fichier component.xml doit être créé dans le dossier racine du package qui a défini les opérations de service et leurs paramètres.

Le fichier component.xml s’affiche ici :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns="http://adobe.com/idp/dsc/component/document">
<!-- Unique id identifying this component -->
   <component-id>ZipService</component-id>

<!-- Version -->
   <version>1.0</version>

<!-- Start of the Service definition -->
   <services>
<!-- Unique name for service descriptor.
           The value is used as the default name for
           deployed services -->
      <service name="ZipService">
<!-- service implementation class definition -->
        <implementation-class>nith.lces2.dsc.ZIPService</implementation-class>

<!-- description -->
        <description>Compress or Decompress list of documents</description>

<!--  You can provide your own icons for a distinct look   -->
          <small-icon>icons/Zip_icon16.png</small-icon>
          <large-icon>icons/Zip_icon32.png</large-icon>


<!-- automatically deploys the service and starts it after installation -->
         <auto-deploy service-id="ZipService" />

         <operations>
<!-- method name in the interface setSmtpHost-->
            <operation name="UnzipDocument">
<!-- input parameters to the "send" method -->
              <input-parameter name="zipDocument" title="Input ZIP Document" type="com.adobe.idp.Document">
                    <hint>A ZIP File to be decompressed</hint>
                </input-parameter>
                <output-parameter name="resultList" title="Decompressed list of documents" type="java.util.List">
                    <hint>Decompressed ZIP list</hint>
                </output-parameter>
            </operation>
            <operation name="ZipDocuments">
<!-- input parameters to the "send" method -->
              <input-parameter name="listOfDocuments" title="List of Documents" type="java.util.List">
                    <hint>A list of documents to be Compressed</hint>
                </input-parameter>
                <input-parameter name="zipFileName" title="Result File Name" type="java.lang.String">
                    <hint>The name of compressed file (optional)</hint>
                </input-parameter>

                <output-parameter name="zippedDoc" title="Compressed Zip file" type="com.adobe.idp.Document">
                    <hint>Compressed ZIP File</hint>
                </output-parameter>
            </operation>
             </operations>
      </service>
   </services>
</component>
```

## Regroupement et déploiement du composant {#packaging-deploying-component}

1. Compilez le projet java et créez un fichier .JAR.
1. Déployez le composant (fichier .JAR) sur le runtime AEM Forms on JEE via Workbench.
1. Démarrez le service à partir de Workbench (voir l’illustration ci-dessous).

![Conception de processus](assets/process-design.jpg)

## Utilisation du service ZIP dans les workflows {#using-zip-service-in-workflows}

L’opération UnzipDocument du service personnalisé peut désormais accepter une variable de document comme entrée et renvoyer une liste de variables de document comme sortie.

![Décompresser le document](assets/unzip-doc.jpg)

De même, l’opération ZipDocuments du composant personnalisé peut accepter une liste de documents comme entrée, les compresser en tant que fichier zip et renvoyer le document compressé.

![Zip Document](assets/zip-doc.jpg)

L’orchestration de workflow suivante montre comment décompresser le fichier ZIP donné, le compresser à nouveau dans un autre fichier ZIP et renvoyer la sortie (voir l’illustration ci-dessous).

![Décompresser le workflow](assets/unzip-zip-process.jpg)

## Certains cas d’utilisation commerciale {#business-use-cases}

Vous pouvez utiliser ce service ZIP pour les cas d’utilisation suivants :

* Recherchez tous les fichiers d’un dossier donné et renvoyez-les sous la forme d’un document compressé.

* Fournissez un fichier ZIP contenant un certain nombre de documents PDF que vous pourrez étendre au lecteur après les avoir décompressés. Cela nécessite le module Reader Extensions d’AEM Forms on JEE.

* Fournissez un fichier ZIP contenant un type de document hétérogène qui peut être décompressé et converti en document PDF à l’aide du service Generate PDF.

* La stratégie protège une liste de documents et renvoie un fichier ZIP.

* Permet aux utilisateurs de télécharger toutes les pièces jointes d’une instance de processus sous la forme d’un fichier ZIP unique.



