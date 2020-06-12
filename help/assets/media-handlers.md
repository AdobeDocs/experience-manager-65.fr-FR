---
title: Process assets using media handlers and workflows in [!DNL Adobe Experience Manager].
description: Découvrez les gestionnaires de médias et comment utiliser des workflows pour effectuer des tâches sur vos ressources numériques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 17fa61fd0aff066bd59f4b6384d2d91bb97b749c
workflow-type: tm+mt
source-wordcount: '2119'
ht-degree: 54%

---


# Process assets using media handlers and workflows {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] est fourni avec un ensemble de workflows et de gestionnaires de médias par défaut pour traiter les ressources. Un processus définit les tâches à exécuter sur les ressources, puis délègue les tâches spécifiques aux gestionnaires de médias, par exemple la génération de miniatures ou l’extraction de métadonnées.

Un processus peut être configuré pour s’exécuter automatiquement lorsqu’une ressource d’un type MIME particulier est téléchargée. The processing steps are defined in terms of a series of [!DNL Assets] media handlers. [!DNL Experience Manager] fournit certains [gestionnaires intégrés](#default-media-handlers) et des gestionnaires supplémentaires peuvent être [conçus et personnalisés](#creating-a-new-media-handler) ou définis en déléguant le processus à un [outil de ligne de commande](#command-line-based-media-handler).

Media handlers are services in [!DNL Assets] that perform specific actions on assets. For example, when an MP3 audio file is uploaded into [!DNL Experience Manager], a workflow triggers an MP3 handler that extracts the metadata and generates a thumbnail. Les gestionnaires de médias sont généralement utilisés conjointement avec des workflows. La plupart des types MIME courants sont pris en charge dans [!DNL Experience Manager]. Il est possible d’effectuer des tâches spécifiques sur les ressources en étendant/créant des processus, en étendant/créant des gestionnaires de médias ou en désactivant/activant des gestionnaires de médias.

>[!NOTE]
>
>Reportez-vous à la page [Formats pris en charge par Assets](assets-formats.md) pour une description de tous les formats pris en charge par , ainsi que des fonctionnalités prises en charge pour chaque format.[!DNL Assets]

## Default media handlers {#default-media-handlers}

The following media handlers are available within [!DNL Assets] and handle the most common MIME types:

<!-- TBD: 
* Apply correct formatting once table is moved to MD.
* Java versions shouldn't be set to 1.5. Must be updated.
-->

| Nom du gestionnaire | Nom du service (dans la console système) | Types MIME pris en charge |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | `com.day.cq.dam.core.impl.handler.TextHandler` | text/plain |
| [!UICONTROL PdfHandler] | `com.day.cq.dam.handler.standard.pdf.PdfHandler` | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | `com.day.cq.dam.core.impl.handler.JpegHandler` | image/jpeg |
| [!UICONTROL Mp3Handler] | `com.day.cq.dam.handler.standard.mp3.Mp3Handler` | audio/mpeg |
| [!UICONTROL ZipHandler] | `com.day.cq.dam.handler.standard.zip.ZipHandler` | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | `com.day.cq.dam.handler.standard.pict.PictHandler` | image/pict |
| [!UICONTROL StandardImageHandler] | `com.day.cq.dam.core.impl.handler.StandardImageHandler` | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | `com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler` | application/msword |
| [!UICONTROL MSPowerPointHandler] | `com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler` | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | `com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler` | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | `com.day.cq.dam.handler.standard.epub.EPubHandler` | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | `com.day.cq.dam.core.impl.handler.GenericAssetHandler` | Solution de secours au cas où aucun autre gestionnaire n’aurait été trouvé pour extraire des données d’une ressource |

Tous les gestionnaires effectuent les tâches suivantes :

* extraction de toutes les métadonnées disponibles dans la ressource.
* création d’une image miniature d’un fichier.

Pour vue des gestionnaires de médias actifs :

1. Dans votre navigateur, accédez à la page suivante : `http://localhost:4502/system/console/components`.
1. Cliquez sur `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Une liste comportant tous les gestionnaires de médias actifs est affichée. Par exemple :

![chlimage_1-437](assets/chlimage_1-437.png)

## Use media handlers in workflows to perform tasks on assets {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Les gestionnaires de médias sont des services généralement utilisés conjointement avec des processus.

[!DNL Experience Manager] comporte des processus par défaut pour le traitement des ressources. Pour les afficher, ouvrez la console de workflow et cliquez sur l’onglet **[!UICONTROL Modèles]** : les titres de workflow commençant par concernent des ressources.[!DNL Assets]

Les workflows existants peuvent être étendus et de nouveaux workflows peuvent être créés pour gérer les ressources en fonction d’exigences spécifiques.

L’exemple suivant indique comment développer le workflow de **[!UICONTROL synchronisation AEM Assets]**, de sorte que des sous-ressources soient générées pour toutes les ressources, à l’exception des documents PDF.

### Désactivation ou activation d’un gestionnaire de médias {#disabling-enabling-a-media-handler}

Les gestionnaires de médias peuvent être désactivés ou activés par le biais de la console de gestion web Apache Felix. Lorsque le gestionnaire de médias est désactivé, ses tâches ne sont pas réalisées sur les ressources.

Pour activer/désactiver un gestionnaire de médias :

1. Dans votre navigateur, accédez à la page suivante : `https://<host>:<port>/system/console/components`.
1. Cliquez sur **[!UICONTROL Désactiver]** en regard du nom du gestionnaire de médias. Par exemple : `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Actualisez la page : une icône s’affiche en regard du gestionnaire de médias pour indiquer qu’il est désactivé.
1. Pour activer le gestionnaire de médias, cliquez sur le bouton **[!UICONTROL Activer]** en regard de son nom.

### Create a new media handler {#creating-a-new-media-handler}

Pour prendre en charge un nouveau type de médias ou exécuter des tâches spécifiques sur une ressource, il est nécessaire de créer un gestionnaire de médias. Cette section décrit la procédure à suivre.

#### Important classes and interfaces {#important-classes-and-interfaces}

La meilleure façon de démarrer une implémentation est d’hériter d’une implémentation abstraite fournie qui prend en charge l’essentiel du traitement et qui fournit un comportement par défaut raisonnable : à savoir la classe `com.day.cq.dam.core.AbstractAssetHandler`.

Cette classe fournit déjà un descripteur de service abstrait. Donc, si vous héritez de cette classe et que vous utilisez le plug-in maven-sling-plugin, assurez-vous que vous avez défini l’indicateur inherit sur `true`.

Implémentez les méthodes suivantes :

* `extractMetadata()` : extraction de toutes les métadonnées disponibles.
* `getThumbnailImage()` : création d’une miniature à partir de la ressource transmise.
* `getMimeTypes()` : renvoi des types MIME de la ressource.

Voici un exemple de modèle :

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

L’interface et les classes sont les suivantes :

* `com.day.cq.dam.api.handler.AssetHandler` : cette interface décrit le service qui ajoute la prise en charge de types MIME spécifiques. L’ajout d’un nouveau type MIME requiert l’implémentation de cette interface. L’interface contient des méthodes pour importer et exporter les documents spécifiques, pour créer des miniatures et extraire des métadonnées.
* `com.day.cq.dam.core.AbstractAssetHandler` : cette classe sert de base pour toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités communes.
* Classe `com.day.cq.dam.core.AbstractSubAssetHandler` :
   * Cette classe sert de base à toutes les autres mises en oeuvre de gestionnaires de ressources et fournit des fonctionnalités utilisées communes ainsi que des fonctionnalités utilisées courantes pour l’extraction de sous-ressources.
   * Le meilleur moyen de début d’une implémentation consiste à hériter d’une implémentation abstraite fournie qui prend en charge la plupart des choses et fournit un comportement par défaut raisonnable : la classe com.day.cq.dam.core.AbstractAssetHandler.
   * Cette classe fournit déjà un descripteur de service abstrait. Donc, si vous héritez de cette classe et que vous utilisez le plug-in maven-sling-plugin, assurez-vous que vous avez défini l’indicateur inherit sur true.

Les méthodes suivantes doivent être implémentées :

* `extractMetadata()` : cette méthode extrait toutes les métadonnées disponibles.
* `getThumbnailImage()` : cette méthode crée une miniature de la ressource transmise.
* `getMimeTypes()` : cette méthode renvoie le ou les types MIME de la ressource.

Voici un exemple de modèle :

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }

L’interface et les classes sont les suivantes :

* `com.day.cq.dam.api.handler.AssetHandler` : cette interface décrit le service qui ajoute la prise en charge de types MIME spécifiques. L’ajout d’un nouveau type MIME requiert l’implémentation de cette interface. L’interface contient des méthodes pour importer et exporter les documents spécifiques, pour créer des miniatures et extraire des métadonnées.
* `com.day.cq.dam.core.AbstractAssetHandler` : cette classe sert de base pour toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités communes.
* `com.day.cq.dam.core.AbstractSubAssetHandler` : cette classe sert de base pour toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités communes, ainsi que la fonctionnalité commune d’extraction de sous-ressources.

#### Example: create a specific text handler {#example-create-a-specific-text-handler}

Dans cette section, vous allez créer un gestionnaire de texte spécifique qui génère des miniatures avec un filigrane.

Procédez comme suit :

Reportez-vous à Outils [de](../sites-developing/dev-tools.md) développement pour installer et configurer Eclipse avec un [!DNL Maven] module externe et pour configurer les dépendances nécessaires au [!DNL Maven] projet.

After you perform the following procedure, when you upload a TXT file into [!DNL Experience Manager], the file&#39;s metadata are extracted and two thumbnails with a watermark are generated.

1. Dans Eclipse, créez un `myBundle`[!DNL Maven] projet :

   1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
   1. In the dialog, expand the [!DNL Maven] folder, select [!DNL Maven] project and click **[!UICONTROL Next]**.
   1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
   1. Définir un [!DNL Maven] projet :

      * Group Id: `com.day.cq5.myhandler`.
      * Id d’artefact : myBundle.
      * Name: My [!DNL Experience Manager] bundle.
      * Description: This is my [!DNL Experience Manager] bundle.
   1. Cliquez sur **[!UICONTROL Terminer]**.


1. Set the [!DNL Java] compiler to version 1.5:

   1. Right-click the `myBundle` project, select [!UICONTROL Properties].
   1. Select [!UICONTROL Java Compiler] and set following properties to 1.5:

      * Niveau de conformité du compilateur
      * Compatibilité des fichiers .class générés
      * Compatibilité source
   1. Cliquez sur **[!UICONTROL OK]**. In the dialog window, click **[!UICONTROL Yes]**.


1. Replace the code in the `pom.xml` file with the following code:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. Créez le package `com.day.cq5.myhandler` contenant les [!DNL Java] classes sous `myBundle/src/main/java`:

   1. Under myBundle, right-click `src/main/java`, select New, then Package.
   1. Name it `com.day.cq5.myhandler` and click Finish.

1. Créez la [!DNL Java] classe `MyHandler`:

   1. Dans [!DNL Eclipse], sous `myBundle/src/main/java`, cliquez avec le bouton droit sur le `com.day.cq5.myhandler` package. Sélectionnez [!UICONTROL Nouveau], puis [!UICONTROL Classe].
   1. In the dialog window, name the [!DNL Java] class `MyHandler` and click [!UICONTROL Finish]. [!DNL Eclipse] crée et ouvre le fichier `MyHandler.java`.
   1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two whitespaces in a row we don't want to double count.
     // The starting of the document is always a whitespace.
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compile the [!DNL Java] class and create the bundle:

   1. Right-click the `myBundle` project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
   1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). Le nouveau gestionnaire de texte est à présent actif dans [!DNL Experience Manager].
1. In your browser, open the [!UICONTROL Apache Felix Web Management Console]. Select the [!UICONTROL Components] tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

## Command Line based media handler {#command-line-based-media-handler}

[!DNL Experience Manager] vous permet d’exécuter n’importe quel outil de ligne de commande dans un workflow pour convertir des ressources (comme ) et ajouter le nouveau rendu à la ressource. [!DNL ImageMagick] You only need to install the command-line tool on the disk hosting the [!DNL Experience Manager] server and to add and configure a process step to the workflow. Le processus appelé, `CommandLineProcess`, permet également d’effectuer un filtrage en fonction de types MIME spécifiques et de créer plusieurs miniatures sur la base du nouveau rendu.

Les conversions suivantes peuvent être automatiquement exécutées et stockées dans [!DNL Assets]:

* Transformation EPS et AI à l’aide d’[ImageMagick](https://www.imagemagick.org/script/index.php) et de [Ghostscript](https://www.ghostscript.com/).
* Transcodage vidéo FLV à l’aide de [FFmpeg](https://ffmpeg.org/).
* Encodage MP3 à l’aide de [LAME](http://lame.sourceforge.net/).
* Traitement audio à l’aide de [SOX](http://sox.sourceforge.net/).

>[!NOTE]
>
>Sur les systèmes autres que Windows, l’outil FichierMpeg renvoie une erreur lors de la génération de rendus pour une ressource vidéo dont le nom de fichier contient un guillemet simple (’). Si le nom de votre fichier vidéo comprend une apostrophe, supprimez-la avant de charger le fichier dans [!DNL Experience Manager].

Le processus `CommandLineProcess` effectue les opérations suivantes par ordre d’apparition dans la liste :

* Filtre le fichier en fonction des types MIME indiqués, le cas échéant.
* Creates a temporary directory on the disk hosting the [!DNL Experience Manager] server.
* Diffuse le fichier d’origine vers le répertoire temporaire.
* Exécute la commande définie par les arguments de l’étape. La commande est exécutée dans le répertoire temporaire avec les autorisations de l’utilisateur exécutant [!DNL Experience Manager].
* Streams the result back into the rendition folder of the [!DNL Experience Manager] server.
* Supprime le répertoire temporaire.
* Crée des miniatures basées sur ces rendus, si spécifié. Le nombre et les dimensions des miniatures sont définis par les arguments de l’étape.

### An example using [!DNL ImageMagick] {#an-example-using-imagemagick}

The following example shows you how to set up the command line process step so that every time an asset with the miMIME e-type GIF or TIFF is added to `/content/dam` on the [!DNL Experience Manager] server, a flipped image of the original is created together with three additional thumbnails (140x100, 48x48, and 10x250).

To do this, use [!DNL ImageMagick]. [!DNL ImageMagick] est un logiciel gratuit de ligne de commande utilisé pour créer, modifier et composer des images bitmap.

Install [!DNL ImageMagick] on the disk hosting the [!DNL Experience Manager] server:

1. Install [!DNL ImageMagick]: See [ImageMagick documentation](https://www.imagemagick.org/script/download.php).
1. Configurez l’outil afin de pouvoir exécuter convert sur la ligne de commande.
1. Pour vérifier si cet outil est installé correctement, exécutez la commande `convert -h` sur la ligne de commande.

   L’écran d’aide qui s’affiche alors répertorie toutes les options possibles de l’outil convert.

   >[!NOTE]
   >
   >In some versions of Windows, the convert command may fail to run because it conflicts with the native convert utility that is part of [!DNL Windows] installation. In this case, mention the complete path for the [!DNL ImageMagick] software used to convert image files to thumbnails. Par exemple, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. To see if the tool runs properly, add a JPG image to the working directory and run the command convert `<image-name>.jpg -flip <image-name>-flipped.jpg` on the command line. Une image inversée est ajoutée au répertoire. Then, add the command line process step to the **[!UICONTROL DAM Update Asset]** workflow.
1. Accédez à la console **[!UICONTROL Workflow]**.
1. Dans l’onglet **[!UICONTROL Modèles]**, modifiez le modèle **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]**.
1. Modifiez les [!UICONTROL arguments] de l&#39;étape de rendu **** Web en : `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`.
1. Enregistrez le workflow.

Pour tester le workflow modifié, ajoutez une ressource à `/content/dam`.

1. Dans le système de fichiers, obtenez une image TIFF de votre choix. Renommez-la `myImage.tiff` et copiez-la dans `/content/dam` en utilisant, par exemple, WebDAV.
1. Accédez à la console **[!UICONTROL CQ5 DAM]**, par exemple `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Ouvrez la ressource **[!UICONTROL myImage.tiff]** et vérifiez que l’image inversée et les trois miniatures ont bien été créées.

#### Configure the CommandLineProcess process step {#configuring-the-commandlineprocess-process-step}

Cette section décrit la procédure à suivre pour définir les [!UICONTROL Arguments du processus] de [!UICONTROL CommandLineProcess].

Séparez les valeurs des arguments [!UICONTROL de] processus à l’aide de la virgule et ne les débuts pas avec un espace blanc.

| Argument-Format | Description |
|---|---|
| mime:&lt;mime-type> | Argument facultatif. Le processus est appliqué si la ressource présente le même type MIME que celui de l’argument. <br>Plusieurs types MIME peuvent être définis. |
| tn:&lt;width>:&lt;height> | Argument facultatif. Le processus crée une miniature avec les dimensions définies dans l’argument. <br>Plusieurs miniatures peuvent être définies. |
| cmd: &lt;command> | Définit la commande qui sera exécutée. La syntaxe dépend de l’outil de ligne de commande. Une seule commande peut être définie. <br>Vous pouvez utiliser les variables suivantes pour créer la commande :<br>`${filename}`: nom du fichier d’entrée, par exemple original.jpg <br> `${file}`: nom de chemin d’accès complet du fichier d’entrée, par exemple /tmp/cqdam0816.tmp/original.jpg <br> `${directory}`: du fichier d’entrée, par exemple /tmp/cqdam0816.tmp <br>`${basename}`: nom du fichier d’entrée sans son extension, par exemple original <br>`${extension}`: extension du fichier d’entrée, par exemple JPG. |

For example, if [!DNL ImageMagick] is installed on the disk hosting the [!DNL Experience Manager] server and if you create a process step using [!UICONTROL CommandLineProcess] as Implementation and the following values as [!UICONTROL Process Arguments]:

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

then, when the workflow runs, the step only applies to assets that have `image/gif` or `mime:image/tiff` as `mime-types`, it creates a flipped image of the original, converts it into JPG and creates three thumbnails that have the dimensions: 140x100, 48x48, and 10x250.

Use the following [!UICONTROL Process Arguments] to create the three standard thumbnails using [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Use the following [!UICONTROL Process Arguments] to create the web-enabled rendition using [!DNL ImageMagick]:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>The [!UICONTROL CommandLineProcess] step only applies to assets (nodes of type `dam:Asset`) or descendants of an asset.

>[!MORELIKETHIS]
>
>* [Traiter les actifs](assets-workflow.md)

