---
title: Lancement des API de Services de document à partir d’un flux de travail AEM
seo-title: Initiate Document Services APIs from AEM Workflow
description: Découvrez comment appeler AEM Document Services sur DDX ou des entrées fournies. Voir également Conversion d’un PDF en PDF/A
seo-description: Learn how to invoke AEM Document services on DDX or supplied inputs. Also see hwo to convert PDF to PDF/A
uuid: aacec2df-1ad6-4ff2-a99d-ef206efcdc09
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 8b85bdc7-3864-49c9-81b0-cf15b8e986d9
exl-id: 123087a2-9d09-4579-9185-2ccd7d25bf8d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 100%

---

# Lancement des API de Services de document à partir d’un flux de travail AEM  {#initiate-document-services-apis-from-aem-workflow}

## Assembler {#assembler}

AEM Forms fournit des workflows personnalisés pour appeler les API du service Assembler suivantes :

* **invoke** : permet d’appeler des opérations spécifiées dans input DDX sur les entrées fournies.
* **toPDFA** : permet de convertir un document PDF d’entrée en document PDF/A.

### Flux de travail Invoke DDX {#invoke-ddx-workflow}

Le workflow **Appeler DDX** appelle l’API du service Assembler `Invoke`, que vous pouvez utiliser pour assembler ou désassembler des documents, ajouter des filigranes à des PDF, etc.

1. Faites glisser l’étape de flux de travail **[!UICONTROL Invoke DDX]** sous l’onglet Forms Workflow dans Sidekick.
1. Cliquez deux fois sur l’étape supplémentaire de flux de travail pour modifier le composant.
1. Dans la boîte de dialogue Modifier le composant, configurez les documents d’entrée, les options d’environnement et les documents de sortie, puis cliquez sur **[!UICONTROL OK]**.

#### Documents d’entrée {#input-documents}

Le flux de travail Invoke DDX nécessite les documents d’entrée suivants :

* **DDX** : il s’agit d’une entrée obligatoire pour l’étape de flux de travail Invoke DDX et elle peut être spécifiée en sélectionnant l’une des options suivantes dans la liste déroulante d’entrée DDX.

   * *Relative To Payload* : le fichier DDX input est relatif au dossier de charge pour l’élément de flux de travail.
   * *Use Payload* : la charge pour l’élément de flux est utilisée comme document input DDX.
   * *Absolute Path* : chemin d’accès absolu au document DDX dans le référentiel CRX.

* **Create Map from PayLoad** : si vous activez cette option, les documents sous le dossier de charge sont ajoutés au mappage de document d’entrée pour l’API `invoke` dans Assembler. Le nom du nœud pour chaque document est utilisé comme clé dans la carte.

* **Input Document’s Map** : indique la carte de document d’entrée. Vous pouvez ajouter plusieurs entrées, où chaque entrée spécifie la clé du document dans la carte et la source du document.

#### Options d’environnement {#environment-options}

L’onglet Environment Options permet de définir différentes options de traitement pour l’API d’appel.

* *Job Log Level* : indique le niveau de journal pour les journaux de traitement.
* *Validate Only* : vérifie la validité d’input DDX.

* *Fail On Error* : indique si l’appel au service Assembler peut échouer en cas d’erreur. La valeur par défaut est False.

#### Documents de sortie {#output-documents}

Selon input DDX, l’API d’appel peut produire plusieurs documents de sortie. L’onglet Output documents vous permet de sélectionner le document de sortie à enregistrer.

1. *Save Output dans Payload* : enregistre les documents de sortie sous le dossier de payload, ou remplace la payload, si celle-ci est un fichier.
1. *Output Document’s Map* : permet de spécifier explicitement où enregistrer chaque document de sortie en ajoutant une entrée par document de sortie. Chaque entrée spécifie le document et l’emplacement d’enregistrement. Output document peut écraser la charge ou être enregistré dans le dossier de charge. Cette option peut être utile lorsque qu’il y a plusieurs documents de sortie.

1. *Job Log* : indique l’emplacement d’enregistrement du document de journal de tâche, ce qui peut être utile pour le dépannage des échecs.

### Flux de travail de conversion en PDF/A {#convert-to-pdf-a-workflow}

L’étape de flux de travail Convert to PDF/A (Convertir en PDF/A) appel l’API du service d’Assembler `toPDFA`. Il est utilisé pour convertir des documents PDF en documents conformes au format PDF/A.

1. Faites glisser l’étape de flux de travail **[!UICONTROL ConvertToPDFA]** sous l’onglet Forms Workflow dans Sidekick.

1. Cliquez deux fois sur l’étape supplémentaire de flux de travail pour modifier le composant.
1. Dans la boîte de dialogue Modifier le composant, configurez les documents d’entrée, les options de conversion et les documents de sortie, puis cliquez sur **[!UICONTROL OK]**.

#### Documents d’entrée {#input-documents-1}

Spécifiez la source du document à convertir en fichier conforme au format PDF/A de l’une des manières suivantes.

* *Relative To Payload* : le document d’entrée est relatif au dossier de charge pour l’élément de flux de travail. 
* *Use Payload* : la charge pour l’élément de flux est utilisée comme document d’entrée.
* *Absolute Path* : chemin d’accès absolu au document d’entrée dans le référentiel CRX.

#### Options de conversion {#conversion-options}

L’onglet Conversion Options permet de spécifier des options qui affectent le processus de conversion PDF/A.

* *Compliance* : indique la norme PDF/A auquel la sortie PDF/A doit se conformer.
* *Result Level* : indique le niveau de journal à utiliser pour les journaux de conversion PDF/A.
* *Signatures* : indique la façon dont les signatures du document d’entrée doivent être traitées lors de la conversion.
* *Color Space* : indique l’espace colorimétrique prédéfini à utiliser pour le document de sortie PDF/A.
* *Vérifier la conversion* : indique si le document converti en PDF/A doit être vérifié pour assurer la conformité PDF/A après conversion.
* *Job Log Level* : indique le niveau de journal à utiliser pour les journaux de traitement.

* *Metadata Extension Schema* : indique le chemin du schéma d’extension de métadonnées à utiliser pour les propriétés XMP dans les métadonnées du document PDF.

#### Documents de sortie {#output-documents-1}

L’onglet Output documents vous permet de spécifier la destination des documents de sortie

* *PDFA Document* : indique l’emplacement où le document PDF/A converti est enregistré. Ce paramètre peut écraser le document de charge utile ou l’enregistrer dans le dossier de charge utile.
* *Conversion Log* : indique l’emplacement où les journaux de conversion sont enregistrés. Ce paramètre peut écraser le document de charge utile ou l’enregistrer dans le dossier de charge utile.

## Formulaires {#forms}

Le flux de travail Render PDF Form est une enveloppe de l’API du service Forms `renderPDFForm` qui permet de créer un PDF à l’aide d’un modèle XDP et de fichiers de données .xml.

### Flux de travail Render PDF Form {#render-pdf-form-workflow}

1. Faites glisser l’étape de flux de travail Render PDF Form sous l’onglet Forms Workflow dans Sidekick. 
1. Cliquez deux fois sur l’étape supplémentaire de flux de travail pour modifier le composant.
1. Dans la boîte de dialogue Modifier le composant, configurez les documents d’entrée, les documents de sortie et les paramètres supplémentaires, puis cliquez sur **[!UICONTROL OK]**.

#### Documents d’entrée {#input-documents-2}

* *Template File* : indique l’emplacement du modèle XDP. Ce champ est obligatoire.

* *Data Document* : indique l’emplacement du fichier de données XML qui doit être fusionné avec le modèle.

#### Documents de sortie {#output-documents-2}

* *Output Document* : indique le nom du formulaire PDF généré.

#### Paramètres supplémentaires {#additional-parameters}

* *Content Root* : indique le chemin d’accès au dossier du référentiel dans lequel les fragments et les images utilisés dans le modèle XDP d’entrée sont stockés.
* *Submit Url* : indique l’URL d’envoi par défaut du formulaire PDF généré.
* *Locale* : indique la langue par défaut du formulaire PDF généré.
* *Acrobat Version* : indique la version d’Acrobat ciblée pour le formulaire PDF généré.
* *Tagged PDF* : indique si le PDF généré est accessible.
* *XCI document* : indique le chemin d’accès au fichier XCI.

## Sortie {#output}

Le flux de travail Generate Non Interactive PDF Workflow (Générer un PDF non interactif) est une enveloppe de l’API de service Output `generatePDFOutput`. Il est utilisé pour générer des documents PDF non interactifs à partir de modèles XDP et des fichiers .xml de données.

### Flux de travail Generate Non Interactive PDF Output   {#generate-non-interactive-pdf-output-workflow-nbsp}

1. Faites glisser le flux de travail de sortie PDF non interactif sous l’onglet Forms Workflow dans Sidekick.
1. Cliquez deux fois sur l’étape supplémentaire de flux de travail pour modifier le composant.
1. Dans la boîte de dialogue Modifier le composant, configurez les documents d’entrée, les documents de sortie et les paramètres supplémentaires, puis cliquez sur **[!UICONTROL OK]**.

#### Documents d’entrée {#input-documents-3}

* *Template File* : indique l’emplacement du modèle XDP. Ce champ est obligatoire.

* *Data Document* : indique l’emplacement du fichier de données XML qui doit être fusionné avec le modèle.

#### Documents de sortie {#output-document}

*Output Document* : indique le nom du formulaire PDF généré.

#### Paramètres supplémentaires {#additional-parameters-1}

* *Content Root* : indique le chemin d’accès au dossier du référentiel dans lequel les fragments et les images utilisés dans le modèle XDP d’entrée sont stockés.
* *Locale* : indique la langue par défaut du formulaire PDF généré.
* *Acrobat Version* : indique la version d’Acrobat ciblée pour le formulaire PDF généré.
* Linearized PDF : indique si le PDF généré doit être optimisé pour l’affichage Web.
* *Tagged PDF* : indique si le PDF généré est accessible.
* *XCI document* : indique le chemin d’accès au fichier XCI.
