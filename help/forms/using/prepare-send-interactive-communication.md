---
title: Préparer et envoyer une communication interactive à l’aide de l’interface utilisateur de l’agent
description: L’interface utilisateur de l’agent permet aux agentes et aux agents de préparer et d’envoyer une communication interactive au post-traitement. L’agent ou l’agente apporte les modifications nécessaires dans la mesure du possible et envoie la communication interactive en post-traitement, comme un e-mail ou une impression.
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Interactive Communication
exl-id: 4fb82e9b-f870-47db-ac92-2d7510acace8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2010'
ht-degree: 100%

---

# Préparer et envoyer une communication interactive à l’aide de l’interface utilisateur de l’agent {#prepare-and-send-interactive-communication-using-the-agent-ui}

L’interface utilisateur de l’agent permet aux agentes et aux agents de préparer et d’envoyer une communication interactive au post-traitement. L’agent ou l’agente apporte les modifications nécessaires dans la mesure du possible et envoie la communication interactive en post-traitement, comme un e-mail ou une impression.

## Présentation {#overview}

Après la création d’une communication interactive, l’agent peut ouvrir la communication interactive dans l’interface utilisateur de l’agent et préparer une copie pour le destinataire en saisissant les données et en gérant le contenu et les pièces jointes. Enfin, l’agent peut envoyer la communication interactive en post-traitement.

Tout en préparant la communication interactive à l’aide de l’interface utilisateur de l’agent, l’agent gère les aspects suivants de la communication interactive dans l’interface utilisateur de l’agent avant de l’envoyer en post-traitement :

* **Données** : l’onglet Données de l’interface utilisateur de l’agent ou de l’agente affiche toutes les variables modifiables par l’agent ou l’agente et les propriétés de modèle de données de formulaire déverrouillées dans la communication interactive. Ces variables/propriétés sont créées lors de la modification ou de la création de fragments de document inclus dans la communication interactive. L’onglet Données comprend également tous les champs qui sont créés dans le modèle de canal XDP/impression. L’onglet Données n’apparaît que lorsque des variables, des propriétés de modèle de données de formulaire ou des champs de la communication interactive peuvent être modifiés par l’agent.
* **Contenu** : dans l’onglet Contenu, l’agent gère le contenu, tel que des fragments de documents et des variables de contenu dans la communication interactive. L’agent peut effectuer les modifications dans le fragment de document, comme autorisé, tout en créant la communication interactive dans les propriétés de ces fragments de document. L’agent peut également réorganiser, ajouter/supprimer un fragment de document et ajouter des sauts de page, si cela est autorisé.
* **Pièces jointes** : l’onglet Pièces jointes apparaît dans l’interface utilisateur de l’agent uniquement si la communication interactive comporte des pièces jointes ou si l’agent a accès à la bibliothèque. L’agent peut être autorisé ou non à modifier les pièces jointes.

## Préparation d’une communication interactive à l’aide de l’interface utilisateur de l’agent {#prepare-interactive-communication-using-the-agent-ui}

1. Sélectionnez **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionnez la communication interactive appropriée et appuyez sur **[!UICONTROL Ouvrir l’interface utilisateur de l’agent ou de l’agente]**.

   >[!NOTE]
   >
   >L’interface utilisateur de l’agent ne fonctionne que si la communication interactive sélectionnée possède un canal d’impression.

   ![openagentiui](assets/openagentiui.png)

   En fonction du contenu et des propriétés de la communication interactive, l’interface utilisateur de l’agent affiche les trois onglets suivants : Données, Contenu et Pièces jointes.

   ![agentuitabs](assets/agentuitabs.png)

   Procédez à la saisie des données, à la gestion du contenu et à la gestion des pièces jointes.

### Saisir des données {#enter-data}

1. Dans l’onglet Données, saisissez les données des variables, les propriétés du modèle de données de formulaire et les champs du modèle d’impression (XDP), selon les besoins. Remplissez tous les champs obligatoires identifiés par un astérisque (*) pour activer le bouton **Envoyer**.

   Sélectionnez une valeur de champ de données dans l’aperçu de la communication interactive pour mettre en surbrillance le champ de données correspondant dans l’onglet Données et vice versa.

### Gérer le contenu {#manage-content}

Dans l’onglet Contenu, gérez le contenu tel que les fragments de document et les variables de contenu dans la communication interactive.

1. Sélectionnez **[!UICONTROL Contenu]**. L’onglet des Contenus de la communication interactive s’affiche.

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. Modifiez les fragments de document, selon les besoins, dans l’onglet Contenu. Pour focaliser l’attention sur le fragment approprié dans la hiérarchie des contenus, vous pouvez sélectionner la ligne ou le paragraphe qui correspond dans l’aperçu de la communication interactive ou sélectionner le fragment directement dans la hiérarchie des contenus.

   Par exemple, le fragment de document avec la ligne « Effectuer un paiement en ligne dès maintenant… » est sélectionné dans l’aperçu du graphique ci-dessous et le même fragment de document est sélectionné dans l’onglet Contenu.

   ![contentmodulefocus](assets/contentmodulefocus.png)

   Dans l’onglet Contenu ou Données, en appuyant sur Mettre en surbrillance les modules sélectionnés dans les Contenus (![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) dans le coin supérieur gauche de l’aperçu, vous pouvez activer ou désactiver la fonctionnalité d’accès au fragment de document lorsque le texte, le paragraphe ou le champ de données approprié est sélectionné dans l’aperçu.

   Les fragments qui peuvent être modifiés par l’agent ou l’agente lors de la création de la communication interactive comportent l’icône Modifier le contenu sélectionné (![iconeditselectedcontent](assets/iconeditselectedcontent.png)). Sélectionnez l’icône Modifier le contenu sélectionné pour lancer le fragment en mode d’édition et y apporter des modifications. Utilisez les options suivantes pour mettre en forme et gérer le texte :

   * [Options de mise en forme](#formattingtext)

      * [Copier-coller du texte formaté depuis d’autres applications](#pasteformattedtext)
      * [Parties du texte en surbrillance](#highlightemphasize)

   * [Caractères spéciaux](#specialcharacters)
   * [Raccourcis clavier](/help/forms/using/keyboard-shortcuts.md)

   Pour plus d’informations sur les actions disponibles pour différents fragments de document dans l’interface utilisateur de l’agent, consultez la section [Actions et informations disponibles dans l’interface utilisateur de l’agent](#actionsagentui).

1. Pour insérer un saut de page sur la communication interactive imprimée, placez le curseur à l’endroit où vous souhaitez insérer un saut de page et sélectionnez Saut de page avant ou Saut de page après (![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   Un espace réservé explicite de saut de page est inséré dans la communication interactive. Pour voir l’impact d’un saut de page explicite sur la communication interactive, reportez-vous à l’aperçu avant impression.

   ![explicitpagebreak](assets/explicitpagebreak.png)

   Procédez à la gestion des pièces jointes de la communication interactive.

### Gestion des pièces jointes {#manage-attachments}

1. Sélectionnez **[!UICONTROL Pièce jointe]**. L’interface utilisateur de l’agent affiche les pièces jointes disponibles de la manière dont elles ont été configurées lors de la création de la communication interactive.

   Vous pouvez choisir de ne pas envoyer de pièce jointe avec la communication interactive en appuyant sur l’icône Aperçu et vous pouvez sélectionner la croix dans la pièce jointe pour la supprimer de la communication interactive (si l’agent ou l’agente a le droit de supprimer ou de masquer la pièce jointe). Pour les pièces jointes spécifiées comme obligatoires, lors de la création de la communication interactive, les icônes Afficher et Supprimer sont désactivées.

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. Sélectionnez l’icône Accès à la bibliothèque (![libraryaccess](assets/libraryaccess.png)) pour accéder à la bibliothèque de contenu et insérer des ressources DAM comme pièces jointes.

   >[!NOTE]
   >
   >L’icône d’accès à la bibliothèque n’est disponible que si l’accès à la bibliothèque a été activé lors de la création de la communication interactive (dans les propriétés du conteneur de documents du canal d’impression).

1. Si l’ordre des pièces jointes n’a pas été verrouillé lors de la création de la communication interactive, vous pouvez réorganiser les pièces jointes en sélectionnant une pièce jointe et en appuyant sur les flèches haut et bas.
1. Utilisez Aperçu web et Aperçu avant impression pour voir si les deux sorties sont conformes à vos besoins.

   Si vous trouvez les aperçus satisfaisants, sélectionnez **[!UICONTROL Envoyer]** pour soumettre/envoyer la communication interactive en post-traitement. Sinon, quittez l’aperçu pour revenir aux modifications.

## Mise en forme du texte {#formattingtext}

Lors de la modification d’un fragment de texte dans l’interface utilisateur de l’agent ou de l’agente, la barre d’outils change en fonction du type de modifications que vous choisissez d’effectuer : police, paragraphe ou liste :

![typeofformattingtoolbar](assets/typeofformattingtoolbar.png) ![Barre d’outils des polices](do-not-localize/fonttoolbar.png)

Barre d’outils de la police

![Barre d’outils Paragraphe](do-not-localize/paragraphtoolbar.png)

Barre d’outils Paragraphe

![Barre d’outils de la liste](do-not-localize/listtoolbar.png)

Barre d’outils de la liste

### Mettre des parties de texte en surbrillance/en évidence {#highlightemphasize}

Pour mettre des parties de texte en surbrillance/en évidence dans un fragment modifiable, sélectionnez le texte, puis la couleur de surbrillance.

![surlignttextagentui](assets/highlighttextagentui.png)

### Coller le texte formaté {#pasteformattedtext}

![pastedtext](assets/pastedtext.png)

### Insérer des caractères spéciaux dans le texte {#specialcharacters}

L’interface utilisateur de l’agent ou de l’agente offre une prise en charge intégrée de 210 caractères spéciaux. L’administrateur peut [ajouter la prise en charge de plus de caractères/de caractères spéciaux grâce à la personnalisation](/help/forms/using/custom-special-characters.md).

#### Livraison des pièces jointes {#attachmentdelivery}

* Si la communication interactive est générée à l’aide des API côté serveur sous la forme d’un PDF, interactif ou non, alors le PDF généré contient des pièces jointes au format PDF.
* Si un post-traitement associé à une communication interactive est chargé dans le cadre des opérations d’envoi à l’aide de l’interface utilisateur de l’agent, les pièces jointes sont transmises en tant que paramètre List&lt;com.adobe.idp.Document> inAttachmentDocs.
* Les workflows du mécanisme de diffusion, tels que l’envoi par e-mail et l’impression, diffusent également les pièces jointes avec la version PDF de la communication interactive.

## Actions et informations disponibles dans l’interface utilisateur de l’agent ou de l’agente {#actionsagentui}

### Fragments de document {#document-fragments}

![ ](do-not-localize/contentoptionsdocfragments.png)

* **Flèches haut/bas** : flèches permettant de déplacer les fragments de document vers le haut ou vers le bas dans la communication interactive.
* **Supprimer** : si cela est autorisé, supprimez le fragment de document de la communication interactive.
* **Saut de page avant** (applicable aux modules enfant de la zone cible) : insère un saut de page avant le fragment de document.
* **Retrait** : augmente ou réduit le retrait d’un fragment de document.
* **Saut de page après** (applicable aux modules enfant de la zone cible) : insère un saut de page après le fragment de document.

![docfragoptions](assets/docfragoptions.png)

* Modification (fragments de texte uniquement) : ouvrez l’éditeur de texte enrichi pour modifier le fragment de document texte. Pour plus d’informations, voir [Formatage de texte](#formattingtext).

* Sélection (icône représentant un œil) : inclut\exclut le fragment de document de la communication interactive.
* Valeurs vides (information) : indique le nombre de variables vides dans le fragment de document.

### Fragments de document de la liste {#list-document-fragments}

![listoptions](assets/listoptions.png)

* Insertion d’une ligne vide : permet d’insérer une nouvelle ligne vide.
* Sélection (icône représentant un œil) : inclut\exclut le fragment de document de la communication interactive.
* Ignorer les puces/numérotations : permet d’ignorer les puces/numéros dans le fragment de document de la liste.
* Valeurs vides (information) : indique le nombre de variables vides dans le fragment de document.

## Enregistrer des communications interactives en tant que brouillons {#save-as-draft}

Vous pouvez utiliser l’interface utilisateur de l’agent pour enregistrer un ou plusieurs brouillons pour chaque communication interactive et récupérer le brouillon ultérieurement pour continuer à travailler dessus. Vous pouvez spécifier un nom différent pour chaque brouillon afin de l’identifier.

Adobe recommande d’exécuter ces instructions en séquence pour enregistrer une communication interactive en tant que brouillon.

### Activer la fonction Enregistrer en tant que brouillon {#before-save-as-draft}

Par défaut, la fonction Enregistrer en tant que brouillon n’est pas activée. Pour activer cette fonction, effectuez les étapes suivantes :

1. Implémentez l’Interface du fournisseur de services (SPI) [ccrDocumentInstance](https://helpx.adobe.com/fr/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html).

   La SPI vous permet d’enregistrer la version préliminaire de la communication interactive dans la base de données avec un ID de brouillon comme identifiant unique. Ces instructions supposent que vous ayez des connaissances préalables sur la création d’un lot OSGi à l’aide d’un projet Maven.

   Pour obtenir un exemple d’implémentation de SPI, voir [Exemple d’implémentation SPI ccrDocumentInstance](#sample-ccrDocumentInstance-spi).
1. Ouvrez `http://<hostname>:<port>/ system/console/bundles` et sélectionnez **[!UICONTROL Installer/Mettre à jour]** pour charger le lot OSGi. Vérifiez que l’état du package chargé s’affiche comme étant **Actif**. Redémarrez le serveur si l’état du package ne s’affiche pas comme étant **Actif**.
1. Accédez à `https://'[server]:[port]'/system/console/configMgr`.
1. Sélectionnez **[!UICONTROL Créer la configuration de correspondance]**.
1. Sélectionnez **[!UICONTROL Activer l’enregistrement à l’aide de CCRDocumentInstanceService]**, puis **[!UICONTROL Enregistrer]**.

### Enregistrer une communication interactive en tant que brouillon {#save-as-draft-agent-ui}

Effectuez les étapes suivantes pour enregistrer une communication interactive en tant que brouillon :

1. Sélectionnez une communication interactive dans Forms Manager, puis **[!UICONTROL Ouvrir l’interface utilisateur de l’agent]**.

1. Apportez les modifications appropriées dans l’interface utilisateur de l’agent ou de l’agente et sélectionnez **[!UICONTROL Enregistrer en tant que brouillon]**.

1. Spécifiez le nom du brouillon dans le champ **[!UICONTROL Nom]** et sélectionnez **[!UICONTROL Terminé]**.

Une fois que vous avez enregistré la communication interactive en tant que brouillon, sélectionnez **[!UICONTROL Enregistrer les modifications]** pour enregistrer d’autres modifications apportées au brouillon.

### Récupérer le brouillon d’une communication interactive {#retrieve-draft}

Après avoir enregistré une communication interactive en tant que brouillon, vous pouvez la récupérer pour continuer à travailler dessus. Récupérez la communication interactive en procédant comme suit :

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[draftID] fait référence à l’identifiant unique de la version préliminaire qui est générée après l’enregistrement d’une communication interactive en tant que brouillon.

### Exemple d’implémentation SPI ccrDocumentInstance {#sample-ccrDocumentInstance-spi}

Mettez en œuvre la SPI `ccrDocumentInstance` pour enregistrer une communication interactive en tant que brouillon. Vous trouverez, ci-dessous, un exemple d’implémentation de la SPI `ccrDocumentInstance`.

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

Les opérations `save`, `update`, `get`, et `getAll` appellent le service de base de données pour enregistrer une communication interactive en tant que brouillon, mettre à jour une communication interactive, récupérer des données de la base de données et récupérer des données pour toutes les communications interactives disponibles dans la base de données. Cet exemple utilise `mySQLDataBaseServiceCRUD` comme nom du service de base de données.

Le tableau suivant explique l’exemple `ccrDocumentInstance` d’implémentation de la SPI. Cela explique comment les opérations `save`, `update`, `get`, et `getAll` appellent le service de base de données dans l’exemple d’implémentation.

<table> 
 <tbody>
 <tr>
  <td><p><strong>Opération</strong></p></td>
  <td><p><strong>Exemples de services de base de données</strong></p></td> 
   </tr>
  <tr>
   <td><p>Vous pouvez créer un brouillon pour une communication interactive ou l’envoyer directement. L’API de l’opération d’enregistrement vérifie si la communication interactive est envoyée en tant que brouillon et inclut un nom de brouillon. L’API appelle ensuite le service mySQLDataBaseServiceCRUD avec l’étape Enregistrer en tant que méthode d’entrée.</p></br><img src="assets/save-as-draft-save-operation.png"/></td>
   <td><p>Le service mySQLDataBaseServiceCRUD vérifie l’étape Enregistrer en tant que méthode d’entrée et génère un ID de brouillon généré automatiquement et le renvoie à AEM. La logique de génération d’un ID de brouillon peut varier en fonction de la base de données.</p></br><img src="assets/save-operation-service.png"/></td>
   </tr>
  <tr>
   <td><p>L’API pour l’opération de mise à jour récupère l’état du brouillon de communication interactive et vérifie si la communication interactive inclut un nom de brouillon. L’API appelle le service mySQLDataBaseServiceCRUD pour mettre à jour cet état dans la base de données.</p></br><img src="assets/save-as-draft-update-operation.png"/></td>
   <td><p>Le service mySQLDataBaseServiceCRUD vérifie l’étape Mettre à jour en tant que méthode d’entrée et enregistre l’état du brouillon de communication interactive dans la base de données.</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>L’API de l’opération GET vérifie si la communication interactive inclut un ID de brouillon. L’API appelle ensuite le service mySQLDataBaseServiceCRUD avec l’étape Get en tant que méthode d’entrée pour récupérer les données de la communication interactive.</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>Le service mySQLDataBaseServiceCRUD vérifie l’étape Get en tant que méthode d’entrée et récupère les données de la communication interactive en fonction de l’ID de brouillon.</p></br><img src="assets/get-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>L’API de l’opération getAll appelle le service mySQLGetALLData pour récupérer les données de toutes les communications interactives enregistrées dans la base de données.</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>Le service mySQLGetALLData récupère des données pour toutes les communications interactives enregistrées dans la base de données.</p></br><img src="assets/getall-operation-service.png"/></td>
   </tr>
  </tbody>
</table>

Voici un exemple de fichier `pom.xml` faisant partie de l’implémentation :

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
         xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
        </dependency>
    </dependencies>


    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-bundle-plugin</artifactId>
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>Veillez à mettre à jour la dépendance `aemfd-client-sdk` à la version 6.0.160 dans le fichier `pom.xml`.
