---
title: Traiter les fichiers à l’aide des gestionnaires de médias et des processus
description: Découvrez les gestionnaires de médias et comment utiliser les processus pour effectuer des tâches sur vos ressources numériques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Processe assets using media handlers and workflows {#processing-assets-using-media-handlers-and-workflows}

Les ressources Adobe Experience Manager (AEM) sont fournies avec un ensemble de processus par défaut et de gestionnaires de médias pour traiter les ressources. Le processus définit les tâches générales à exécuter sur les ressources, puis délègue les tâches spécifiques aux gestionnaires de médias, par exemple la génération de miniatures ou l’extraction de métadonnées.

Vous pouvez définir un processus qui doit s’exécuter automatiquement lorsqu’une ressource d’un type particulier est téléchargée sur le serveur. Les étapes de traitement sont définies en termes d’une série de gestionnaires de médias AEM Assets. AEM provides some [built in handlers,](#default-media-handlers) and additional ones can be either [custom developed](#creating-a-new-media-handler) or defined by delegating the process to a [command line tool](#command-line-based-media-handler).

Les gestionnaires de médias sont des services au sein des ressources AEM qui exécutent des actions spécifiques sur des ressources. Par exemple, lorsqu’un fichier audio MP3 est téléchargé dans AEM, un processus déclenche un gestionnaire MP3 qui extrait les métadonnées et génère une miniature. Les gestionnaires de médias sont généralement utilisés conjointement avec des processus. La plupart des types MIME courants sont pris en charge dans AEM. Il est possible d’effectuer des tâches spécifiques sur les ressources en étendant/créant des processus, en étendant/créant des gestionnaires de médias ou en désactivant/activant des gestionnaires de médias.

>[!NOTE]
>
>Please refer to the [Assets supported formats](assets-formats.md) page for a description of all the formats supported by AEM Assets as well as features supported for each format.

## Gestionnaires de médias par défaut {#default-media-handlers}

Les gestionnaires de médias suivants sont disponibles dans AEM Assets et gèrent les types MIME les plus courants :

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

| Nom du gestionnaire | Nom du service (dans la console système) | Types MIME pris en charge |
|---|---|---|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/image |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | de secours au cas où aucun autre gestionnaire n’aurait été trouvé pour extraire des données d’un fichier |

Tous les gestionnaires effectuent les tâches suivantes :

* extraction de toutes les métadonnées disponibles dans la ressource.
* création d’une miniature à partir de la ressource.

Il est possible d’afficher les gestionnaires de médias actifs :

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. Click the link `com.day.cq.dam.core.impl.store.AssetStoreImpl`.
1. Une liste comportant tous les gestionnaires de médias actifs est affichée. Par exemple :

![chlimage_1-437](assets/chlimage_1-437.png)

## Use Media Handlers in Workflows to perform tasks on Assets {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

Les gestionnaires de médias sont des services généralement utilisés conjointement avec des processus.

AEM comporte des processus par défaut pour le traitement des ressources. To view them, open the Workflow console and click the **[!UICONTROL Models]** tab: the workflow titles that start with AEM Assets are the assets specific ones.

Les processus existants peuvent être étendus et de nouveaux processus peuvent être créés pour gérer les ressources en fonction d’exigences spécifiques.

The following example shows how to enhance the **[!UICONTROL AEM Assets Synchronization]** workflow so that sub-assets are generated for all assets except PDF documents.

### Désactivation ou activation d’un gestionnaire de médias {#disabling-enabling-a-media-handler}

Les gestionnaires de médias peuvent être désactivés ou activés par le biais de la console de gestion web Apache Felix. Lorsque le gestionnaire de médias est désactivé, ses tâches ne sont pas réalisées sur les ressources.

Pour activer/désactiver un gestionnaire de médias :

1. In your browser, navigate to `https://<host>:<port>/system/console/components`.
1. Cliquez sur **[!UICONTROL Désactiver]** en regard du nom du gestionnaire de médias. Par exemple: `com.day.cq.dam.handler.standard.mp3.Mp3Handler`.
1. Actualisez la page : une icône s’affiche en regard du gestionnaire de médias pour indiquer qu’il est désactivé.
1. To enable the media handler, click **[!UICONTROL Enable]** next to the name of the media handler.

### Create a new Media Handler {#creating-a-new-media-handler}

Pour prendre en charge un nouveau type de médias ou exécuter des tâches spécifiques sur une ressource, il est nécessaire de créer un gestionnaire de médias. Cette section décrit la procédure à suivre.

#### Classes et interfaces importantes {#important-classes-and-interfaces}

The best way to start an implementation is to inherit from a provided abstract implementation that takes care of most things and provides reasonable default behavior: the `com.day.cq.dam.core.AbstractAssetHandler` class.

Cette classe fournit déjà un descripteur de service abstrait. Donc, si vous héritez de cette classe et que vous utilisez le plug-in maven-sling-plugin, assurez-vous que vous avez défini l’indicateur inherit sur `true`.

Mettez en oeuvre les méthodes suivantes :

* `extractMetadata()`: extrait toutes les métadonnées disponibles.
* `getThumbnailImage()`: crée une image miniature en dehors du fichier transmis.
* `getMimeTypes()`: renvoie les types MIME de ressource.

Voici un exemple de modèle :

`package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts } `

L’interface et les classes sont les suivantes :

* `com.day.cq.dam.api.handler.AssetHandler` interface : Cette interface décrit le service qui ajoute la prise en charge de types MIME spécifiques. L’ajout d’un nouveau type MIME requiert l’implémentation de cette interface. L’interface contient des méthodes pour importer et exporter les documents spécifiques, pour créer des miniatures et extraire des métadonnées.
* `com.day.cq.dam.core.AbstractAssetHandler` class : Cette classe sert de base à toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités courantes utilisées.
* `com.day.cq.dam.core.AbstractSubAssetHandler` catégorie:
   * Cette classe sert de base à toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités utilisées communes ainsi que des fonctionnalités utilisées courantes pour l’extraction de sous-ressources.
   * La meilleure façon de démarrer une implémentation est d’hériter d’une implémentation abstraite fournie qui prend en charge l’essentiel du traitement et qui fournit un comportement par défaut raisonnable : à savoir la classe com.day.cq.dam.core.AbstractAssetHandler.
   * Cette classe fournit déjà un descripteur de service abstrait. Donc, si vous héritez de cette classe et que vous utilisez le plug-in maven-sling-plugin, assurez-vous que vous avez défini l’indicateur inherit sur true.

Les méthodes suivantes doivent être implémentées :

* `extractMetadata()`: cette méthode extrait toutes les métadonnées disponibles.
* `getThumbnailImage()`: cette méthode crée une image miniature en dehors de la ressource transmise.
* `getMimeTypes()`: cette méthode renvoie le ou les types MIME de ressource.

Voici un exemple de modèle :

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component hérite=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ classe publique MyMediaHandler étend com.day.cq.dam.core.AbstractAssetHandler { // implémenter les parties pertinentes }

L’interface et les classes sont les suivantes :

* `com.day.cq.dam.api.handler.AssetHandler` interface : Cette interface décrit le service qui ajoute la prise en charge de types MIME spécifiques. L’ajout d’un nouveau type MIME requiert l’implémentation de cette interface. L’interface contient des méthodes pour importer et exporter les documents spécifiques, pour créer des miniatures et extraire des métadonnées.
* `com.day.cq.dam.core.AbstractAssetHandler` class : Cette classe sert de base à toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités courantes utilisées.
* `com.day.cq.dam.core.AbstractSubAssetHandler` class :Cette classe sert de base à toutes les autres implémentations de gestionnaires de ressources et fournit des fonctionnalités utilisées communes ainsi que des fonctionnalités utilisées courantes pour l’extraction de sous-ressources.

#### Exemple : créer un gestionnaire de texte spécifique {#example-create-a-specific-text-handler}

Dans cette section, vous allez créer un gestionnaire de texte spécifique qui génère des miniatures avec un filigrane.

Procédez comme suit :

Reportez-vous à Outils [de](../sites-developing/dev-tools.md) développement pour installer et configurer Eclipse avec un module externe Maven et pour configurer les dépendances nécessaires au projet Maven.

Lorsque vous téléchargez un fichier txt dans AEM après avoir effectué la procédure suivante, les métadonnées du fichier sont extraites, et deux miniatures comportant un filigrane sont générées.

1. Dans Eclipse, créez le projet `myBundle` Maven :

   1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
   1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
   1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
   1. Définissez le projet Maven :

      * Id de groupe : com.day.cq5.myhandler
      * Id d’artefact : myBundle
      * Nom : Mon lot AEM
      * Description : Nom de mon lot AEM
   1. Cliquez sur **[!UICONTROL Terminer]**.


1. Réglez le compilateur Java sur la version 1.5 :

   1. Right-click the `myBundle` project, select Properties.
   1. Sélectionnez Compilateur Java et définissez les propriétés suivantes sur 1.5 :

      * Niveau de conformité du compilateur
      * Compatibilité des fichiers .class générés
      * Compatibilité source
   1. Cliquez sur **[!UICONTROL OK]**. Dans la boîte de dialogue, cliquez sur Oui.


1. Remplacez le code du fichier pom.xml par le code suivant :

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

1. Créez le package `com.day.cq5.myhandler` contenant les classes Java sous `myBundle/src/main/java`:

   1. Under myBundle, right-click `src/main/java`, select New, then Package.
   1. Name it `com.day.cq5.myhandler` and click Finish.

1. Créez la classe Java `MyHandler`:

   1. In Eclipse, under `myBundle/src/main/java`, right-click the `com.day.cq5.myhandler` package, select New, then Class.
   1. Dans la boîte de dialogue, attribuez le nom MyHandler à la classe Java, puis cliquez sur Finish (Terminer). Eclipse crée le fichier MyHandler.java et l’ouvre.
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
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
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
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Compilez la classe Java et créez le lot :

   1. Right-click the myBundle project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
   1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). Le nouveau gestionnaire de texte est à présent actif dans AEM.
1. Dans votre navigateur, ouvrez la console de gestion web Apache Felix. Select the Components tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

## Gestionnaire de médias en ligne de commande {#command-line-based-media-handler}

AEM vous permet d’exécuter n’importe quel outil de ligne de commande au sein d’un flux de travaux pour convertir des fichiers (comme ImageMagick) et ajouter le nouveau rendu à la ressource. Vous avez uniquement besoin d’installer l’outil de ligne de commande sur le disque hébergeant le serveur AEM, puis d’ajouter et de configurer une étape au processus. The invoked process, called `CommandLineProcess`, also enables to filter according to specific MIME types and to create multiple thumbnails based on the new rendition.

Les conversions suivantes peuvent être automatiquement exécutées et stockées dans AEM Assets :

* Transformation EPS et AI à l’aide d’[ImageMagick](https://www.imagemagick.org/script/index.php) et de [Ghostscript](https://www.ghostscript.com/)
* Transcodage vidéo FLV à l’aide de [FFmpeg](https://ffmpeg.org/)
* Encodage MP3 à l’aide de [LAME](http://lame.sourceforge.net/)
* Traitement audio à l’aide de [SOX](http://sox.sourceforge.net/)

>[!NOTE]
>
>Sur les systèmes non Windows, l’outil FFMpeg renvoie une erreur lors de la génération de rendus pour un fichier vidéo dont le nom de fichier contient un guillemet simple (&#39;). Si le nom de votre fichier vidéo comporte une apostrophe unique, supprimez-la avant de charger le fichier dans AEM.

The `CommandLineProcess` process performs the following operations in the order they are listed:

* Filtre le fichier en fonction des types MIME indiqués, le cas échéant.
* Crée un répertoire temporaire sur le disque hébergeant le serveur AEM.
* Envoie le fichier d’origine en continu vers le répertoire temporaire.
* Exécute la commande définie par les arguments de l’étape. La commande est en cours d’exécution dans le répertoire temporaire avec les autorisations de l’utilisateur exécutant AEM.
* Renvoie le résultat dans le dossier de rendu du serveur AEM.
* Supprime le répertoire temporaire.
* Crée des miniatures basées sur ces rendus, si spécifié. Le nombre et les dimensions des miniatures sont définis par les arguments de l’étape.

### Exemple utilisant ImageMagick {#an-example-using-imagemagick}

L’exemple suivant montre comment configurer l’étape de processus de ligne de commande de sorte qu’à chaque fois qu’une ressource de type MIME gif ou tiff est ajoutée à /content/dam sur le serveur AEM, une image inversée de l’original est créée avec trois miniatures supplémentaires (140x100, 48x48 et 10x250).

Pour ce faire, vous utiliserez ImageMagick. ImageMagick est une suite logicielle gratuite permettant de créer, modifier et composer des images bitmap, généralement à partir de la ligne de commande.

Installez d’abord ImageMagick sur le disque hébergeant le serveur AEM :

1. Install ImageMagick: please refer to the [ImageMagick documentation](https://www.imagemagick.org/script/download.php).
1. Configurez l’outil pour pouvoir exécuter la conversion sur la ligne de commande.
1. To see if the tool is installed properly, run the following command `convert -h` on the command line.

   L’écran d’aide qui s’affiche alors répertorie toutes les options possibles de l’outil convert.

   >[!NOTE]
   >
   >Dans certaines versions de Windows (par exemple, Windows SE), la commande convert peut ne pas fonctionner car elle est en conflit avec l&#39;utilitaire de conversion natif qui fait partie de l&#39;installation de Windows. Dans ce cas, indiquez le chemin complet de l’utilitaire ImageMagick utilisé pour convertir les fichiers image en miniatures. Par exemple, `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`.

1. To see if the tool runs properly, add a .jpg image to the working directory and run the command convert `<image-name>.jpg -flip <image-name>-flipped.jpg` on the command line.

   Une image inversée est ajoutée au répertoire.

Then, add the command line process step to the **[!UICONTROL DAM Update Asset]** workflow:

1. Go to the **[!UICONTROL Workflow]** console.
1. In the **[!UICONTROL Models]** tab, edit the **[!UICONTROL DAM Update Asset]** model.
1. Change the settings of the **[!UICONTROL Web enabled rendition]** step as follows:

   **Arguments** :

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. Enregistrez le workflow.

Pour tester le flux de travaux modifié, ajoutez une ressource à `/content/dam`.

1. Dans le système de fichiers, sélectionnez une image.tiff. Rename it to `myImage.tiff` and copy it to `/content/dam`, for example by using WebDAV.
1. Go to the **[!UICONTROL CQ5 DAM]** console, for example `http://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. Open the asset **[!UICONTROL myImage.tiff]** and verify that the flipped image and the three thumbnails have been created.

#### Configuration de l’étape du processus CommandLineProcess {#configuring-the-commandlineprocess-process-step}

Cette section décrit la procédure à suivre pour définir les **Arguments du processus** de **CommandLineProcess**.

The values of the **Process Arguments** must be separated by a comma and must not start with a whitespace.

| Argument-Format | Description |
|---|---|
| mime:&lt;mime-type> | Argument facultatif. Le processus est appliqué si la ressource a le même type MIME que celui de l’argument. <br>Plusieurs types MIME peuvent être définis. |
| tn:&lt;largeur>:&lt;hauteur> | Argument facultatif. Le processus crée une miniature avec les dimensions définies dans l’argument. <br>Plusieurs miniatures peuvent être définies. |
| cmd : &lt;command> | Définit la commande qui sera exécutée. La syntaxe dépend de l’outil de ligne de commande. Une seule commande peut être définie. <br>Vous pouvez utiliser les variables suivantes pour créer la commande:<br>`${filename}`: nom du fichier d’entrée, par exemple original.jpg <br> `${file}`: nom complet du chemin d’accès du fichier d’entrée, par exemple /tmp/cqdam0816.tmp/original.jpg <br> `${directory}`: du fichier d’entrée, par exemple /tmp/cqdam0816.tmp <br>`${basename}`: nom du fichier d’entrée sans son extension, par exemple original <br>`${extension}`: extension du fichier d’entrée, par exemple jpg |

Par exemple, si ImageMagick est installé sur le disque hébergeant le serveur AEM et que vous créez une étape de processus en utilisant **CommandLineProcess** en tant qu’implémentation et les valeurs suivantes en tant qu’**arguments de processus** :

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

puis, lors de l’exécution du workflow, l’étape s’applique uniquement aux ressources dont les types MIME sont image/gif ou mime:image/tiff, elle crée ensuite une image inversée de l’original, puis la convertit en .jpg et génère trois miniatures aux dimensions suivantes : 140x100, 48x48 et 10x250.

Use the following **Process Arguments** to create the three standard thumbnails using ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

Use the following **Process Arguments** to create the web-enabled rendition using ImageMagick:

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>The **CommandLineProcess** step only applies to Assets (nodes of type `dam:Asset`) or descendants of an Asset.
