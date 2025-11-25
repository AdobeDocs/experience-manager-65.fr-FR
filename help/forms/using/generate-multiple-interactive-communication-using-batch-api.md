---
title: Utiliser l’API Batch pour générer plusieurs communications interactives
description: Utiliser l’API Batch pour générer plusieurs communications interactives
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '2134'
ht-degree: 100%

---

# Générer plusieurs communications interactives à l’aide de l’API Batch {#use-batch-api-to-generate-multiple-ic}

Vous pouvez utiliser l’API Batch pour générer plusieurs communications interactives à partir d’un modèle. Le modèle consiste en une communication interactive sans données. L’API Batch combine des données avec un modèle pour créer une communication interactive. L’API est utile pour la production en masse de communications interactives. Par exemple, les factures de téléphone ou les relevés de cartes de crédit pour plusieurs clients.

L’API Batch accepte les enregistrements (données) au format JSON et à partir d’un modèle de données de formulaire. Le nombre de communications interactives générées est égal aux enregistrements spécifiés dans le fichier JSON d’entrée dans le modèle de données de formulaire configuré. Grâce à l’API, vous pouvez générer des sorties d’impression et web. L’option IMPRESSION génère un document PDF, tandis que l’option WEB génère des données au format JSON pour chaque enregistrement individuel.

## Utiliser lʼAPI Batch {#using-the-batch-api}

Vous pouvez utiliser l’API Batch en conjonction avec les dossiers de contrôle ou comme une API REST autonome. Pour utiliser l’API Batch, vous devez configurer un modèle, un type de sortie (HTML, IMPRESSION ou les deux), des paramètres régionaux, un service de préremplissage et le nom des communications interactives générées.

Pour générer une communication interactive, vous devez combiner un enregistrement à un modèle de communication interactive. Les API Batch peuvent lire les enregistrements (données pour les modèles de communication interactive) directement à partir d’un fichier JSON ou d’une source de données externe accessible via le modèle de données de formulaire. Vous pouvez conserver chaque enregistrement dans un fichier JSON distinct ou créer un tableau JSON pour conserver tous les enregistrements dans un seul fichier.

**Enregistrement unique dans un fichier JSON**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**Plusieurs enregistrements dans un fichier JSON**

```json
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### Utiliser l’API Batch avec les dossiers de contrôle {#using-the-batch-api-watched-folders}

Pour une utilisation plus facile de l’API, AEM Forms fournit un service Watched Folder, déjà configuré pour utiliser l’API Batch et prêt à l’emploi. Vous pouvez accéder au service via l’interface utilisateur d’AEM Forms afin de générer plusieurs communications interactives. Vous pouvez également créer des services personnalisés en fonction de vos besoins. Pour utiliser l’API Batch avec le dossier de contrôle, employez les méthodes répertoriées ci-dessous :

* Spécifiez les données d’entrée (enregistrements) au format de fichier JSON pour générer une communication interactive
* Utilisez des données d’entrée (enregistrements) enregistrées dans une source de données externe et accessibles via un modèle de données de formulaire pour générer une communication interactive.

#### Spécifiez les enregistrements de données d’entrée au format de fichier JSON pour générer une communication interactive. {#specify-input-data-in-JSON-file-format}

Pour générer une communication interactive, vous devez combiner un enregistrement à un modèle de communication interactive. Vous pouvez créer un fichier JSON distinct pour chaque enregistrement ou créer un tableau JSON pour conserver tous les enregistrements dans un seul fichier :

Pour créer une communication interactive à partir d’enregistrements sauvegardés dans un fichier JSON, procédez comme suit :

1. Créez un [Dossier de contrôle](/help/forms/using/creating-configure-watched-folder.md) et configurez-le pour quʼil utilise l’API Batch :
   1. Connectez-vous à votre instance de création AEM Forms.
   1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Configurer le dossier de contrôle]**. Sélectionnez **[!UICONTROL Nouveau]**.
   1. Spécifiez le **[!UICONTROL Nom]** et le **[!UICONTROL Chemin dʼaccès]** physique du dossier. Par exemple, `c:\batchprocessing`.
   1. Sélectionnez lʼoption **[!UICONTROL Service]** dans le champ **[!UICONTROL Traiter le fichier avec]**.
   1. Sélectionnez le service **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** dans le champ **[!UICONTROL Nom du service]**.
   1. Spécifiez un **[!UICONTROL Modèle de fichier de sortie]**. Par exemple, le [modèle](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-watched-folder-endpoints.html?lang=fr#about-file-patterns) %F/ indique que le dossier de contrôle peut trouver des fichiers d’entrée dans un sous-dossier du dossier de contrôle\entrée.
1. Configurer les paramètres avancés
   1. Ouvrez l’onglet **[!UICONTROL Avancé]** et ajoutez les propriétés personnalisées suivantes :

      | Propriété | Type | Description |
      |--- |--- |--- |
      | templatePath | Chaîne | Spécifiez le chemin dʼaccès du modèle de communication interactive à utiliser. Par exemple, `/content/dam/formsanddocuments/testsample/mediumic`. Il s’agit d’une propriété obligatoire. |
      | recordPath | Chaîne | La valeur du champ recordPath permet de définir le nom d’une communication interactive. Vous pouvez définir le chemin dʼaccès du champ d’un enregistrement comme valeur du champ recordPath. Par exemple, si vous spécifiez /employee/Id, la valeur du champ ID devient le nom de la communication interactive correspondante. La valeur par défaut est une valeur [UUID aléatoire](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booléen | Donnez la valeur False à cette propriété. Vous pouvez utiliser le paramètre usePrefillService pour préremplir la communication interactive avec des données récupérées à partir du service de préremplissage configuré pour la communication interactive correspondante. Lorsque usePrefillService est défini sur true, les données JSON en entrée (pour chaque enregistrement) sont traitées comme des arguments FDM. La valeur par défaut est false.  |
      | batchType | Chaîne | Définissez la valeur sur PRINT, WEB ou WEB_AND_PRINT. La valeur par défaut est WEB_AND_PRINT. |
      | paramètres régionaux | Chaîne | Spécifiez les paramètres régionaux de la communication interactive de sortie. Le service prêt à l’emploi n’utilise pas l’option des paramètres régionaux, mais vous pouvez créer un service personnalisé pour générer des communications interactives localisées. La valeur par défaut est en_US. |

   1. Sélectionnez **[!UICONTROL Créer]**.
1. Utilisez le dossier de contrôle pour générer une communication interactive :
   1. Ouvrez le dossier de contrôle. Accédez au dossier d’entrée.
   1. Créez un dossier dans le dossier d’entrée et placez le fichier JSON dans le dossier nouvellement créé.
   1. Attendez que le dossier de contrôle traite le fichier. Lorsque le traitement commence, le fichier d’entrée et le sous-dossier contenant le fichier sont déplacés vers le dossier intermédiaire.
   1. Ouvrez le dossier de sortie pour afficher la sortie :
      * Lorsque vous spécifiez l’option PRINT dans la configuration du dossier de contrôle, une sortie PDF pour la communication interactive est générée.
      * Lorsque vous spécifiez l’option WEB dans la configuration du dossier de contrôle, un fichier JSON par enregistrement est généré. Vous pouvez utiliser ce fichier JSON pour [préremplir un modèle web](#web-template).
      * Lorsque vous spécifiez les options PRINT et WEB, des documents PDF et un fichier JSON par enregistrement sont générés.

#### Utiliser des données d’entrée enregistrées dans une source de données externe et accessibles via un modèle de données de formulaire pour produire une communication interactive {#use-fdm-as-data-source}

Vous combinez des données (enregistrements) enregistrées dans une source de données externe avec un modèle de communication interactive pour produire une communication interactive. Lorsque vous créez une communication interactive, vous la connectez à une source de données externe via un modèle de données de formulaire (FDM) pour accéder aux données. Vous pouvez configurer le service de traitement par lot des dossiers de contrôle pour qu’il récupère des données à l’aide du même modèle de données de formulaire à partir d’une source de données externe. Pour [créer une communication interactive à partir d’enregistrements sauvegardés dans une source de données externe :](/help/forms/using/work-with-form-data-model.md)

1. Configurer le modèle de données de formulaire du modèle
   1. Ouvrez le modèle de données de formulaire associé au modèle de communication interactive.
   1. Sélectionnez l’OBJET DE MODÈLE DE NIVEAU SUPÉRIEUR, puis Modifier les propriétés.
   1. Sélectionnez votre service de récupération ou dʼobtention dans le champ Service de lecture du volet Modifier les propriétés.
   1. Sélectionnez l’icône en forme de crayon de l’argument de service de lecture pour lier l’argument à un attribut de requête et spécifier la valeur de liaison. Elle lie l’argument de service à la valeur d’attribut de liaison ou littérale spécifiée, qui est transmise au service en tant qu’argument pour extraire les détails associés à la valeur spécifiée de la source de données.

      Dans cet exemple, l’argument id prendra la valeur de l’attribut id du profil d’utilisateur ou d’utilisatrice et le transmettra en tant qu’argument au service de lecture. Il lira et renverra les valeurs des propriétés associées à partir de l’objet de modèle de données de la personne employée pour l’attribut id spécifié. Ainsi, si vous spécifiez 00250 dans le champ id du formulaire, le service de lecture lira les détails de la personne employée avec l’ID de personne employée 00250.

      ![Configurer l’attribut de requête](assets/request-attribute.png)

   1. Enregistrez les propriétés et le modèle de données de formulaire.
1. Configurer la valeur de l’attribut de requête
   1. Créez un fichier .json sur votre système de fichiers et ouvrez-le pour le modifier.
   1. Créez un tableau JSON et spécifiez l’attribut principal pour récupérer les données du modèle de données de formulaire. Par exemple, le fichier JSON suivant demande à FDM d’envoyer les données des enregistrements dont l’ID est 27126 ou 27127 :

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1. Enregistrez et fermez le fichier.

1. Créer et configurer un [Dossier de contrôle](/help/forms/using/creating-configure-watched-folder.md) pour quʼil utilise le service API Batch
   1. Connectez-vous à votre instance de création AEM Forms.
   1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Configurer le dossier de contrôle]**. Sélectionnez **[!UICONTROL Nouveau]**.
   1. Spécifiez le **[!UICONTROL Nom]** et le **[!UICONTROL Chemin dʼaccès]** physique du dossier. Par exemple, `c:\batchprocessing`.
   1. Sélectionnez lʼoption **[!UICONTROL Service]** dans le champ **[!UICONTROL Traiter le fichier avec]**.
   1. Sélectionnez le service **[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** dans le champ **[!UICONTROL Nom du service]**.
   1. Spécifiez un **[!UICONTROL Modèle de fichier de sortie]**. Par exemple, le [modèle](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/administrator-help/configuring-watched-folder-endpoints.html?lang=fr#about-file-patterns) %F/ indique que le dossier de contrôle peut trouver des fichiers d’entrée dans un sous-dossier du dossier de contrôle\entrée.
1. Configurer les paramètres avancés
   1. Ouvrez l’onglet **[!UICONTROL Avancé]** et ajoutez les propriétés personnalisées suivantes :

      | Propriété | Type | Description |
      |--- |--- |--- |
      | templatePath | Chaîne | Spécifiez le chemin dʼaccès du modèle de communication interactive à utiliser. Par exemple, /content/dam/formsanddocuments/testsample/mediumic. Il s’agit d’une propriété obligatoire. |
      | recordPath | Chaîne | La valeur du champ recordPath permet de définir le nom d’une communication interactive. Vous pouvez définir le chemin dʼaccès du champ d’un enregistrement comme valeur du champ recordPath. Par exemple, si vous spécifiez /employee/Id, la valeur du champ ID devient le nom de la communication interactive correspondante. La valeur par défaut est une valeur [UUID aléatoire](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()). |
      | usePrefillService | Booléen | Définissez la valeur sur « true ». La valeur par défaut est false. Lorsque la valeur est définie sur « true », l’API Batch lit les données du modèle de données de formulaire configuré et les transmet dans la communication interactive. Lorsque la méthode usePrefillService est définie sur « true », les données JSON d’entrée (pour chaque enregistrement) sont traitées comme des arguments FDM. |
      | batchType | Chaîne | Définissez la valeur sur PRINT, WEB ou WEB_AND_PRINT. La valeur par défaut est WEB_AND_PRINT. |
      | paramètres régionaux | Chaîne | Spécifiez les paramètres régionaux de la communication interactive de sortie. Le service prêt à l’emploi n’utilise pas l’option des paramètres régionaux, mais vous pouvez créer un service personnalisé pour générer des communications interactives localisées. La valeur par défaut est en_US. |

   1. Sélectionnez **[!UICONTROL Créer]**.
1. Utilisez le dossier de contrôle pour générer une communication interactive :
   1. Ouvrez le dossier de contrôle. Accédez au dossier d’entrée.
   1. Créez un dossier dans le dossier d’entrée. Mettez le fichier JSON créé à l’étape 2 dans le dossier nouvellement créé.
   1. Attendez que le dossier de contrôle traite le fichier. Lorsque le traitement commence, le fichier d’entrée et le sous-dossier contenant le fichier sont déplacés vers le dossier intermédiaire.
   1. Ouvrez le dossier de sortie pour afficher la sortie :
      * Lorsque vous spécifiez l’option PRINT dans la configuration du dossier de contrôle, une sortie PDF pour la communication interactive est générée.
      * Lorsque vous spécifiez l’option WEB dans la configuration du dossier de contrôle, un fichier JSON par enregistrement est généré. Vous pouvez utiliser ce fichier JSON pour [préremplir un modèle web](#web-template).
      * Lorsque vous spécifiez les options PRINT et WEB, des documents PDF et un fichier JSON par enregistrement sont générés.

## Appeler l’API par lot à l’aide de requêtes REST

Vous pouvez appeler [l’API par lot](https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/index.html) par le biais de requêtes REST (Representational State Transfer). Cela vous permet de fournir un point d’entrée REST aux autres utilisateurs et utilisatrices pour accéder à l’API et de configurer vos propres méthodes de traitement, de stockage et de personnalisation de la communication interactive. Vous pouvez développer votre propre servlet Java personnalisé pour déployer l’API sur votre instance AEM.

Avant de déployer le servlet Java, vérifiez que vous disposez d’une communication interactive et que les fichiers de données correspondants sont prêts. Effectuez les étapes suivantes pour créer et déployer le servlet Java™ :

1. Connectez-vous à votre instance AEM et créez une communication interactive. Pour utiliser la communication interactive mentionnée dans l’exemple de code ci-dessous, [cliquez ici](assets/SimpleMediumIC.zip).
1. [Créez et déployez un projet AEM en utilisant Apache Maven](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/aem-project-archetype.html?lang=fr) sur votre instance AEM.
1. Ajoutez le [SDK client AEM Forms version 6.0.12](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) ou ultérieure dans la liste des dépendances du fichier POM de votre projet AEM. Par exemple,

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. ouvrez le projet Java™, créez un fichier .java, par exemple CCMBatchServlet.java. Ajoutez le code suivant au fichier :

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import java.util.Date;
   
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. Dans le code ci-dessus, remplacez le chemin d’accès du modèle (setTemplatePath) par le chemin d’accès de votre modèle et définissez la valeur de l’API setBatchType :
   * Lorsque vous spécifiez l’option PRINT, une sortie PDF est générée pour la communication interactive.
   * Lorsque vous spécifiez l’option WEB, un fichier JSON par enregistrement est généré. Vous pouvez utiliser ce fichier JSON pour [préremplir un modèle web](#web-template).
   * Lorsque vous spécifiez les options PRINT et WEB, des documents PDF et un fichier JSON par enregistrement sont générés.

1. [Utilisez Maven pour déployer le code mis à jour sur votre instance AEM.](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/aem-project-archetype.html?lang=fr).
1. Pour générer la communication interactive, appelez l’API Batch. L’impression de l’API par lot renvoie un flux de fichiers PDF et .json en fonction du nombre d’enregistrements. Vous pouvez utiliser le fichier JSON pour [préremplir un modèle web](#web-template). Si vous utilisez le code ci-dessus, l’API est déployée à l’adresse `http://localhost:4502/bin/batchServlet`. Le code imprime et renvoie un flux de fichiers PDF et JSON.

### Préremplir un modèle Web {#web-template}

Lorsque vous définissez le batchType pour effectuer le rendu du canal web, l’API génère un fichier JSON pour chaque enregistrement de données. Vous pouvez utiliser la syntaxe suivante pour fusionner le fichier JSON avec le canal Web correspondant afin de générer une communication interactive :

**Syntaxe**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**Exemple**
Si votre fichier JSON se trouve à l’emplacement `C:\batch\mergedJsonPath.json` et que vous utilisez le modèle de communication interactive ci-dessous : `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`.

Alors, l’URL suivante sur le nœud de publication affiche le canal Web de la communication interactive
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

Outre l’enregistrement des données sur le système de fichiers, vous pouvez stocker les fichiers JSON dans le référentiel CRX, le système de fichiers, le serveur Web ou vous pouvez accéder aux données via le service de préremplissage OSGI. Les syntaxes pour fusionner les données en utilisant les différents protocoles sont les suivantes :

* **Protocole CRX**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **Protocole de fichier**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **Protocole du service de préremplissage**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

  SERVICE_NAME fait référence au nom du service de préremplissage OSGI. Voir Création et exécution d’un service de préremplissage.

  IDENTIFIER fait référence à toutes les métadonnées requises par le service de préremplissage OSGI pour récupérer les données de préremplissage. Un identifiant de la personne connectée est un exemple de métadonnées pouvant être utilisées.

* **Protocole HTTP**
  `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>Seul le protocole CRX est activé par défaut. Pour activer d’autres protocoles pris en charge, consultez [Configurer le service de préremplissage à l’aide de Configuration Manager](https://experienceleague.adobe.com/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=fr).
