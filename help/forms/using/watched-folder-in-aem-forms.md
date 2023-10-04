---
title: Dossier de contrôle dans AEM Forms
description: Un administrateur peut placer un dossier sous surveillance et lancer une opération de workflow, de service ou de script lorsqu’un fichier est placé dans le dossier contrôlé.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: fbf5c7c3-cb01-4fda-8e5d-11d56792d4bf
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '7148'
ht-degree: 36%

---

# Dossier de contrôle dans AEM Forms{#watched-folder-in-aem-forms}

Un administrateur peut configurer un dossier réseau, appelé dossier de contrôle (en anglais Watched Folder), de sorte que lorsqu’un utilisateur y place un fichier (par exemple un fichier PDF), un workflow, un service ou une opération d’exécution de script démarre pour le traitement du fichier ajouté. Après que le service a effectué l’opération spécifiée, il enregistre le fichier obtenu dans un dossier de sortie spécifié. Pour plus d’informations sur les workflows, le service et le script, voir [Différentes méthodes de traitement des fichiers](#variousmethodsforprocessingfiles).

## Création d’un dossier de contrôle {#create-a-watched-folder}

Vous pouvez utiliser l’une des méthodes suivantes pour créer un dossier de contrôle sur le système de fichiers :

* Lors de la configuration des propriétés d’un nœud de configuration du dossier de contrôle, indiquez le chemin d’accès complet du répertoire parent dans la propriété folderPath (chemin du fichier) et ajoutez le nom du dossier de contrôle à créer, comme indiqué dans l’exemple suivant :`C:/MyPDFs/MyWatchedFolder`
Le dossier `MyWatchedFolder` n’existe pas, AEM Forms tente de créer un dossier à l’emplacement spécifié.

* Créez un dossier dans le système de fichiers avant de configurer un point d’entrée Watched Folder, puis indiquez son chemin d’accès complet dans la propriété folderPath (chemin de fichier). Pour plus d’informations sur la propriété folderPath, voir [Propriétés Watched Folder](#watchedfolderproperties).

>[!NOTE]
>
>Dans un environnement de grappes de serveur, le dossier à utiliser comme dossier de contrôle doit être accessible, modifiable et partagé sur le système de fichiers ou le réseau. Chaque instance du serveur d’applications de la grappe doit avoir accès au même dossier partagé. Sous Windows, créez un lecteur réseau mappé sur tous les serveurs et spécifiez le chemin du lecteur réseau mappé dans la propriété folderPath.

## Créer un noeud de configuration du dossier de contrôle {#create-watched-folder-configuration-node}

Pour configurer un dossier de contrôle, créez un noeud de configuration du dossier de contrôle. Pour créer un nœud de configuration, veuillez suivre les étapes ci-après :

1. Connectez-vous à CRX-DE Lite en tant qu’administrateur et accédez au dossier de /etc/fd/watchfolder/config.

1. Créer un nœud de type `nt:unstructured`. Par exemple, watchedfolder

   >[!NOTE]
   >
   >Le nom du noeud du dossier de contrôle ne peut pas contenir d’espaces ni de caractères spéciaux.

1. Ajoutez les propriétés suivantes au nœud :

   * `folderPath`
   * `inputProcessorType`
   * `inputProcessorId`
   * `outputFilePattern`

   Pour obtenir la liste complète des propriétés prises en charge, voir [Propriétés du dossier de contrôle](#watchedfolderproperties).

1. Cliquez sur **Enregistrer tout**. Après la création du nœud et l’enregistrement des propriétés. Les dossiers `input`, `result`, `failure`, `preserve` et `stage` sont créés au chemin d’accès spécifié dans la propriété `folderPath`.

   La tâche de numérisation démarre l’analyse du dossier de contrôle dans un laps de temps défini.

## Propriétés Watched Folder {#watchedfolderproperties}

Vous pouvez configurer les propriétés suivantes pour un dossier de contrôle.

* **folderPath (chaîne)**: chemin d’accès au dossier à analyser à des intervalles de temps définis. Pour un environnement organisé en grappe, le dossier doit se trouver à un emplacement partagé avec tous les serveurs disposant d’un accès complet au serveur. Il s’agit d’une propriété obligatoire.
* **inputProcessorType (chaîne)**: type du processus à démarrer. Vous pouvez spécifier le workflow, le script, ou le service. Il s’agit d’une propriété obligatoire.
* **inputProcessorId (chaîne)**: le comportement de la propriété inputProcessorId est basé sur la valeur spécifiée pour la propriété inputProcessorType. Il s’agit d’une propriété obligatoire. La liste suivante détaille toutes les valeurs possibles de la propriété inputProcessorType et la condition requise correspondante pour la propriété inputProcessorType :

   * Pour le workflow, spécifiez le modèle de workflow à exécuter. Par exemple, /etc/workflow/models/&lt;workflow_name>/jcr:content/model
   * Pour le script, spécifiez le chemin JCR du script à exécuter. Par exemple, /etc/fd/watchfolder/test/testScript.ecma
   * Pour le service, spécifiez le filtre utilisé pour localiser un service OSGi. Le service est enregistré comme une implémentation de l’interface de com.adobe.aemfd.watchfolder.service.api.ContentProcessor.

* **runModes (chaîne)**: liste séparée par des virgules de modes d’exécution autorisés pour l’exécution du workflow. Voici quelques exemples :

   * auteur 

   * publication

   * auteur, publication

   * publication, auteur

>[!NOTE]
>
>Si le serveur qui héberge le dossier Watched Folder ne dispose pas d’un mode d’exécution spécifié, le dossier est toujours activé, sans tenir compte des modes d’exécution sur le serveur.

* **outputFilePattern (chaîne)**: modèle du fichier de sortie. Vous pouvez spécifier un modèle de dossier ou de fichier. Si un modèle de dossier est spécifié, les fichiers de sortie portent des noms comme décrit dans les workflows. Si un modèle de fichier est spécifié, les fichiers de sortie portent des noms comme décrit dans le modèle de fichier. [Modèle de fichier et de dossier](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) peut également spécifier une structure de répertoire pour les fichiers de sortie. Il s’agit d’une propriété obligatoire.

* **stageFileExpirationDuration (long, -1 par défaut)** : Le nombre de secondes à attendre pour qu’un fichier/dossier d’entrée ayant déjà été collecté pour traitement soit traité comme ayant expiré et défini comme étant un échec. Ce mécanisme d’expiration n’est activé que lorsque la valeur de cette propriété est un nombre positif.

>[!NOTE]
>
>Remarque : même lorsqu’une entrée est marquée comme ayant expiré à l’aide de ce mécanisme, il se peut que son traitement se poursuive en arrière-plan mais qu’elle prenne simplement plus de temps que prévu. Si le contenu d’entrée a été consommé avant que le mécanisme de dépassement de délai ne soit activé, le traitement peut même se terminer ultérieurement et la sortie être vidée dans le dossier des résultats. Si le contenu n’a pas été consommé avant le délai d’expiration, il est très probable que le traitement s’arrête ultérieurement lors de la tentative d’utilisation du contenu. Cette erreur sera également consignée dans le dossier failure pour la même entrée. D’un autre côté, si le traitement de l’entrée n’est jamais activé en raison d’une tâche intermittente/d’un échec de déclenchement de workflow (scénario que le mécanisme d’expiration vise à résoudre), aucune de ces deux éventualités ne se produira bien sûr. Par conséquent, pour toutes les entrées du dossier failure qui ont été marquées comme des échecs en raison d’un délai d’attente (recherchez les messages du formulaire &quot;Fichier non traité après un temps important, marquez comme échec !&quot; dans le journal des erreurs), il est conseillé d’analyser le dossier des résultats (ainsi que le dossier des erreurs lui-même pour une autre entrée pour la même entrée) afin de vérifier si les éventualités décrites auparavant se sont vraiment produites.

* **deleteExpiredStageFileOnlyWhenThrottled (Boolean, valeur par défaut true) :** si le mécanisme d’expiration doit ou non s’activer uniquement lorsque le dossier de contrôle est ralenti. Le mécanisme est plus pertinent pour les dossiers de contrôle ralentis, car un petit nombre de fichiers qui traînent à l’état non traité (en raison d’erreurs de traitement/de workflow intermittentes) peuvent étrangler le traitement de l’ensemble du lot lorsque le ralentissement est activé. Si cette propriété est conservée sur true (valeur par défaut), le mécanisme d’expiration ne s’active pas pour les dossiers de contrôle qui ne sont pas ralentis. Si la propriété est conservée sur false, le mécanisme s’active toujours tant que la propriété stageFileExpirationDuration est un nombre positif.

* **pollInterval (Long)** : le laps de temps en secondes pour l’analyse du dossier de contrôle en sortie. A moins que le paramètre Ralentissement ne soit activé, l’attribut Intervalle de répétition doit être supérieur à la durée du traitement d’une tâche moyenne, faute de quoi le système risque d’être surchargé. La valeur par défaut est 5. Pour plus d’informations, voir la description de la taille du lot . La valeur de pollinterval doit être supérieure ou égale à un.
* **excludeFilePattern (chaîne)** : une liste dont les éléments sont séparés par des points-virgules (;) qu’un dossier de contrôle utilise pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Aucun fichier ou dossier avec ce modèle n’est analysé en vue du traitement. Ce paramètre est utile lorsque l’entrée est un dossier contenant plusieurs fichiers. Vous pouvez copier le contenu du dossier dans un dossier dont le nom sera choisi par le dossier de contrôle. Cela empêche Watched Folder de sélectionner un dossier à traiter avant que le dossier ne soit complètement copié dans le dossier input. La valeur par défaut est « null ».
Vous pouvez utiliser des [modèles de fichiers](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p) pour exclure les types de fichiers suivants :

   * Fichiers possédant des extensions de nom de fichier particulières, par exemple &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * Fichiers portant des noms spécifiques ; par exemple, data&#42; exclurait les fichiers et les dossiers nommés data1, data2, etc.
   * Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

      * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
      * &#42;.[dD][Aa]&#39;port&#39;
      * &#42;.[Xx][Mm][Ll]

Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

* **includeFilePattern (chaîne)** : liste dont les éléments sont séparés par des points-virgules (;) utilisés par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Ainsi, si l’attribut IncludeFilePattern a la valeur input&#42;, tous les fichiers et les dossiers correspondant à input&#42; sont sélectionnés. Cela concerne les fichiers et les dossiers nommés input1, input2, etc. La valeur par défaut est &#42; et elle désigne tous les fichiers et dossiers. Vous pouvez utiliser des modèles de fichiers pour inclure les types de fichiers suivants :

   * Fichiers possédant des extensions de nom de fichier particulières, par exemple &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
   * Fichiers portant des noms spécifiques, par exemple data.&#42; à savoir les fichiers et les dossiers nommés data1, data2, etc.

* Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

   * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;

      * &#42;.[dD][Aa]&#39;port&#39;
      * &#42;.[Xx][Mm][Ll]

Pour plus d’informations sur les modèles de fichiers, voir [À propos des modèles de fichier](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p)

* **waitTime (Long)** : le temps d’attente (en millisecondes) avant de pouvoir analyser un fichier ou un dossier après sa création. Par exemple, si la durée d’attente est de 3 600 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce dernier sera sélectionné à l’issue d’un laps de temps de 59 minutes ou plus. La valeur par défaut est 0. Ce paramètre est utile pour garantir qu’un fichier ou un dossier est entièrement copié dans le dossier input. Par exemple, si vous devez traiter un fichier volumineux dont le téléchargement dure dix minutes, définissez une durée d’attente de 10&#42;60 &#42;1 000 millisecondes. Cela empêche le dossier de contrôle d’analyser le fichier s’il n’a pas dix minutes.
* **purgeDuration (Long)** : les fichiers et les sous-dossiers du dossier Résultats sont vidés lorsqu’ils sont plus anciens que cette valeur. Cette valeur est mesurée en jours. Ce paramètre s’avère utile pour s’assurer que le dossier de résultats n’est pas plein. Une valeur de -1 jour indique de ne jamais supprimer le dossier de résultats. La valeur par défaut est -1.
* **resultFolderName (chaîne)** : le dossier dans lequel les résultats enregistrés sont stockés. Si les résultats ne s’affichent pas dans ce dossier, vérifiez le dossier des échecs. Les fichiers en lecture seule ne sont pas traités ; ils sont enregistrés dans le dossier des échecs. Cette valeur peut être un chemin d’accès absolu ou relatif avec les modèles de fichiers suivants :

   * %F = préfixe du nom du fichier
   * %E = extension du nom du fichier
   * %Y = année (complète)
   * %y = année (deux derniers chiffres)
   * %M = mois
   * %D = jour du mois
   * %d = jour de l’année
   * %H = heure (horloge 24 heures)
   * %h = heure (horloge 12 heures)
   * %m = minute
   * %s = seconde
   * %l = milliseconde
   * %R = nombre aléatoire (entre 0 et 9)
   * %P = ID de processus ou de tâche

  Par exemple, s’il est 20 h, que nous sommes le 17 juillet 2009 et que vous indiquez C:/Test/WF0/failure/%Y/%M/%D/%H/, le dossier de résultats est C:/Test/WF0/failure/2009/07/17/20

  Si le chemin d’accès n’est pas absolu, mais relatif, le dossier est créé dans le dossier de contrôle. La valeur par défaut est result/%Y/%M/%D/, qui correspond au dossier des résultats dans le dossier de contrôle. Pour plus d’informations sur les modèles de fichiers, voir [À propos des modèles de fichiers](../../forms/using/watched-folder-in-aem-forms.md#p-file-and-folder-patterns-p).

>[!NOTE]
>
>Plus les dossiers de résultats sont petits, plus les performances de Watched Folder augmentent. Par exemple, si la charge estimée pour le dossier de contrôle est de 1 000 fichiers par heure, essayez un modèle comme result/%Y%M%D%H afin qu’un nouveau sous-dossier soit créé toutes les heures. Si la charge est plus faible (par exemple, 1 000 fichiers par jour), vous pouvez utiliser un modèle du type result/%Y%M%D.

* **failureFolderName (chaîne)** : le dossier dans lequel les fichiers d’échec sont enregistrés. Cet emplacement est toujours lié au dossier de contrôle. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier result. Les fichiers en lecture seule ne sont pas traités ; ils sont enregistrés dans le dossier des échecs. La valeur par défaut est failure/%Y/%M/%D/.
* **preserveFolderName (chaîne) :** Emplacement de stockage des fichiers après traitement réussi. Le chemin d’accès peut être absolu, relatif ou nul. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier result. La valeur par défaut est preserve/%Y/%M/%D/.
* **batchSize (Long)** : le nombre de fichiers ou de dossiers à sélectionner par analyse. Utilisez pour éviter une surcharge du système ; l’analyse simultanée d’un trop grand nombre de fichiers peut entraîner un blocage. La valeur par défaut est 2.

  Les paramètres Intervalle d’enquête et Taille du lot permettent de déterminer le nombre de fichiers sélectionnés par le dossier de contrôle pour chaque analyse. Watched Folder utilise un pool de threads Quartz pour analyser le dossier input. Le pool de threads est partagé avec d’autres services. Si l’intervalle d’analyse est court, les threads analysent souvent le dossier input. Si des fichiers sont déposés régulièrement dans le dossier de contrôle, il est préférable que l’intervalle d’analyse soit court. Si les fichiers sont déposés peu fréquemment, utilisez un intervalle d’analyse plus long afin que les autres services puissent utiliser les threads.

  Si un volume important de fichiers est déposé, définissez une grande taille de lot. Par exemple, si le service exécuté par le point d’entrée du dossier de contrôle peut traiter 700 fichiers par minute et que les utilisateurs déposent des fichiers dans le dossier d’entrée à la même fréquence, la définition de la Taille du lot sur 350 et de l’Intervalle d’enquête sur 30 secondes permet de maintenir les performances du dossier de contrôle sans avoir à subir les conséquences d’une analyse du dossier de contrôle trop fréquente.

  Lorsque des fichiers sont déposés dans le dossier de contrôle, ce dernier les répertorie dans les entrées, ce qui réduit parfois les performances si l’analyse s’effectue toutes les secondes. L’allongement de l’intervalle d’analyse permet d’améliorer les performances. Si le volume des fichiers déposés est réduit, ajustez la Taille du lot et l’Intervalle de répétition en conséquence. Par exemple, si 10 fichiers sont déposés toutes les secondes, essayez de définir l’intervalle de répétition sur 1 seconde et la taille du lot sur 10.

* **throttleOn (Boolean)** : lorsque cette option est sélectionnée, elle permet de limiter le nombre de tâches du dossier de contrôle qu’AEM Forms peut traiter en une seule fois. La valeur Taille du lot détermine le nombre maximal de tâches. La valeur par défaut est true. Voir [A propos du ralentissement](../../forms/using/watched-folder-in-aem-forms.md#p-about-throttling-p).

* **overwriteDuplicateFilename (booléen)** : lorsque cet attribut est défini sur True, les fichiers du dossier des résultats et du dossier de fichiers conservés sont remplacés. Lorsque la valeur est False, les fichiers et les dossiers comportant un suffixe d’index numérique sont utilisés pour le nom. La valeur par défaut est False.
* **preserveOnFailure (Booléen)**: conservez les fichiers d’entrée en cas d’échec de l’exécution de l’opération sur un service. La valeur par défaut est true.
* **inputFilePattern (chaîne)**: spécifie le modèle des fichiers d’entrée pour un dossier de contrôle. Crée une liste autorisée des fichiers.
* **asynch (booléen)** : identifie le type d’appel comme étant asynchrone ou synchrone. La valeur par défaut est true (asynchrone). Le traitement des fichiers est une tâche gourmande en ressources. Conservez la valeur de l’indicateur asynch sur true pour éviter que le thread principal de la tâche d’analyse ne soit étouffé. Dans un environnement organisé en grappes, il est essentiel de conserver l’indicateur true pour activer l’équilibrage de charge pour les fichiers en cours de traitement sur les serveurs disponibles. Si l’indicateur est défini sur false, la tâche d’analyse tente d’effectuer le traitement de chaque fichier/dossier de niveau supérieur de manière séquentielle dans son propre thread. Ne définissez pas l’indicateur sur false sans raison spécifique, par exemple, le traitement basé sur un workflow sur une configuration de serveur unique.

>[!NOTE]
>
>Par conception, les workflows sont asynchrones. Même si vous définissez la valeur sur false, les workflows sont lancés en mode asynchrone.

* **enabled (booléen)**: désactive et active la numérisation d’un dossier de contrôle. Définissez enabled sur true pour lancer l’analyse du dossier de contrôle. La valeur par défaut est true.
* **payloadMapperFilter :** lorsqu’un dossier est configuré comme dossier de contrôle, une structure de dossiers est créée dans le dossier de contrôle. La structure dispose de dossiers pour fournir des entrées, recevoir des sorties (résultats), enregistrer les données en cas d’échec, conserver les données pour les processus de longue durée et enregistrer les données pour différentes étapes. La structure de dossiers d’un dossier de contrôle peut servir de charge utile pour les processus basés sur l’utilisation de Forms. Un mappeur de charge utile vous permet de définir la structure d’une charge utile qui utilise un dossier de contrôle pour l’entrée, la sortie et le traitement. Par exemple, si vous utilisez le mappeur par défaut, celui-ci mappe le contenu du dossier de contrôle avec le dossier [payload]\input and [payload]\output. Deux mises en oeuvre de mappeur de charge prêt à l’emploi sont disponibles. Si vous n’avez pas [une implémentation personnalisée](../../forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilisez une implémentation prête à l’emploi :

   * **Mappeur par défaut :** utilisez le mappeur de payload par défaut pour conserver les contenus d’entrée et de sortie des dossiers de contrôle dans des dossiers d’entrée et de sortie distincts dans la payload. De plus, dans le chemin d’accès de la payload d’un workflow, utilisez les chemins d’accès [payload]/input/ et [payload]/output pour récupérer et sauvegarder le contenu.

   * **Mappeur de payload basé sur des fichiers simples :** utilisez le mappeur de payload basé sur des fichiers simples pour conserver les contenus d’entrée et de sortie directement dans le dossier de la payload. Il ne crée aucune hiérarchie supplémentaire, comme le mappeur par défaut.

### Paramètres de configuration personnalisés {#custom-configuration-parameters}

Outre les propriétés de configuration du dossier de contrôle répertoriées ci-dessus, vous pouvez également spécifier des paramètres de configuration personnalisés. Les paramètres personnalisés sont transmis au code de traitement des fichiers. Il permet au code de modifier son comportement en fonction de la valeur du paramètre. Pour spécifier un paramètre :

1. Connectez-vous à CRXDE-Lite et accédez au nœud de configuration du dossier de contrôle.
1. Ajoutez un paramètre de propriété.&lt;property_name> au noeud de configuration du dossier de contrôle. Le type de la propriété ne peut être que Booléen, Date, Décimal, Double, Long et Chaîne. Vous pouvez spécifier des propriétés à une et plusieurs valeurs.

>[!NOTE]
>
>Si le type de données de la propriété est Double, spécifiez une virgule dans la valeur de ces propriétés. Pour toutes les propriétés, si le type de données est Double et qu’aucune virgule n’est spécifiée dans la valeur, le type est converti en Long.

Ces propriétés sont transmises sous la forme d’un mappage inaltérable de type Map&lt;string object=&quot;&quot;> au code de traitement. Le code de traitement peut être un ECMAScript, un workflow ou un service. Les valeurs fournies pour les propriétés sont disponibles en tant que paires clé-valeur dans la carte. La clé est le nom de la propriété et la valeur est la valeur de la propriété. Pour plus d’informations sur les paramètres de configuration personnalisés, voir l’image suivante :

![Un nœud de configuration du dossier de contrôle possédant des propriétés obligatoires, certaines propriétés facultatives, certains paramètres de configuration](assets/custom-configuration-parameters.png)

Un nœud de configuration du dossier de contrôle possédant des propriétés obligatoires, quelques propriétés facultatives, quelques paramètres de configuration.

#### Variables mutables pour les flux de travail {#mutable-variables-for-workflows}

Vous pouvez créer des variables mutables pour les méthodes de traitement de fichiers basées sur un workflow. Ces variables servent de conteneurs pour les données circulant entre les étapes d’un workflow. Pour créer ces variables :

1. Connectez-vous à CRXDE-Lite et accédez au nœud de configuration du dossier de contrôle.

1. Ajoutez une propriété workflow.var.&lt;variable_name> au noeud de configuration du dossier de contrôle.

   Le type de la propriété ne peut être que Booléen, Date, Décimal, Double, Long et Chaîne. Les propriétés à plusieurs valeurs sont également prises en charge. Pour les propriétés à plusieurs valeurs, la valeur disponible pour l’étape du workflow est un tableau de type spécifié.

   >[!NOTE]
   >
   >Si le type de données de la propriété est Double, spécifiez une virgule dans la valeur de ces propriétés. Pour toutes les propriétés, si le type de données est Double et qu’aucune virgule n’est spécifiée dans la valeur, le type est converti en Long.

>[!NOTE]
>
>La spécification JCR requiert une valeur par défaut pour les propriétés. Les valeurs par défaut sont disponibles pour les étapes d’un workflow de traitement. Indiquez donc les valeurs par défaut appropriées.

![custom-configuration-parameters2](assets/custom-configuration-parameters2.png)

## Différentes méthodes de traitement des fichiers {#variousmethodsforprocessingfiles}

Vous pouvez démarrer un workflow, un service ou un script pour traiter les emplacements de documents dans un dossier de contrôle.

### Utilisation d’un service pour traiter les fichiers d’un dossier de contrôle   {#using-a-service-to-process-files-of-a-watched-folder-nbsp}

Un service est une implémentation personnalisée de l’interface de `com.adobe.aemfd.watchfolder.service.api.ContentProcessor`. Il est enregistré avec OSGi avec quelques propriétés personnalisées. Les propriétés personnalisées de l’implémentation la rendent unique et permettent d’identifier l’implémentation.

#### Implémentation personnalisée de l’interface ContentProcessor {#custom-implementation-of-the-contentprocessor-interface}

L’implémentation personnalisée accepte un contexte de traitement (un objet de type com.adobe.aemfd.watchfolder.service.api.ProcessorContext), lit les documents d’entrée et les paramètres de configuration du contexte, traite les entrées et ajoute de nouveau la sortie au 
contexte. ProcessorContext dispose des API suivants :

* **getWatchFolderId** : renvoie l’ID du dossier de contrôle.
* **getInputMap**: renvoie un mappage de type Map. Les clés de la carte sont le nom du fichier d’entrée et un objet document contenant le contenu du fichier. Utilisez l’API getinputMap pour lire les fichiers d’entrée.
* **getConfigParameters**: renvoie un mappage inaltérable de type Map. La carte contient
les paramètres de configuration d’un dossier de contrôle.

* **setResult** : l’implémentation de ContentProcessor
utilise l’API pour passer le document de sortie au dossier de résultats. Vous pouvez attribuer un nom au fichier de sortie à l’API setResult. L’API peut choisir d’utiliser ou d’ignorer le fichier fourni en fonction du dossier de sortie ou du modèle de fichier spécifié. Si un modèle de dossier est spécifié, les fichiers de sortie portent des noms comme décrit dans les workflows. Si un modèle de fichier est spécifié, les fichiers de sortie portent des noms comme décrit dans le modèle de fichier.

Par exemple, le code suivant est une implémentation personnalisée de l’interface ContentProcessor avec une propriété foo=bar personnalisée.

```java
@Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
@Service(value = {OutputWriter.class, ContentProcessor.class})
@Property(name = "foo", value = "bar")
public class OutputWriter implements ContentProcessor {
```

while [configuration d’un dossier de contrôle](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p), si vous spécifiez la propriété inputProcessorId (foo=bar) et la propriété inputProcessorType en tant que service, alors le service mentionné ci-dessus (implémentation personnalisée) est utilisé pour traiter les fichiers d’entrée du dossier de contrôle.

L’exemple suivant est également une implémentation personnalisée de l’interface ContentProcessor. Dans cet exemple, le service accepte les fichiers d’entrée, copie les fichiers à un emplacement temporaire et renvoie un objet document avec le contenu du fichier. Le contenu de l’objet document est enregistré dans le dossier result. Le chemin d’accès physique du dossier de résultats est configuré dans la variable [Noeud de configuration du dossier de contrôle](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

```java
@Component(immediate = true)
@Service(value = ContentProcessor.class)
@Property(name = "serviceSelector", value = "testProcessor1")
public class TestContentProcessor1 implements ContentProcessor {
    @Override
    public void processInputs(ProcessorContext context) throws Exception {
        Map.Entry<String, Document> e = context.getInputMap().entrySet().iterator().next();
        File f = new File((String) context.getConfigParameters().get("tempDir"),
                context.getConfigParameters().get("outPrefix") + e.getKey());
        e.getValue().copyToFile(f);
        context.setResult(f.getName(), new Document(f, true));
    }
}
```

### Utilisation de scripts pour traiter les fichiers d’un dossier de contrôle {#using-scripts-to-process-files-of-a-watched-folder}

Les scripts sont le code personnalisé de plainte ECMAScript écrit dans les documents de processus placés dans le dossier de contrôle. Un script est représenté sous la forme d’un noeud JCR. Outre les variables ECMAScript standard (log, sling, etc.), le script comporte une variable processorContext. La variable est de type ProcessorContext. ProcessorContext dispose des API suivants :

* **getWatchFolderId** : renvoie l’ID du dossier de contrôle.
* **getInputMap**: renvoie un mappage de type Map. Les clés de la carte sont le nom du fichier d’entrée et un objet document contenant le contenu du fichier. Utilisez l’API getinputMap pour lire les fichiers d’entrée.
* **getConfigParameters**: renvoie un mappage inaltérable de type Map. La carte contient les paramètres de configuration d’un dossier de contrôle.
* **setResult** : l’implémentation de ContentProcessor utilise l’API pour transmettre le document de sortie au dossier de résultats. Vous pouvez attribuer un nom au fichier de sortie à l’API setResult. L’API peut choisir d’utiliser ou d’ignorer le fichier fourni en fonction du dossier de sortie ou du modèle de fichier spécifié. Si un modèle de dossier est spécifié, les fichiers de sortie portent des noms comme décrit dans les workflows. Si un modèle de fichier est spécifié, les fichiers de sortie portent des noms comme décrit dans le modèle de fichier.

Le code suivant est un exemple ECMAScript. Il accepte les fichiers d’entrée, copie les fichiers à un emplacement temporaire et renvoie un objet document avec le contenu du fichier. Le contenu de l’objet document est enregistré dans le dossier result. Le chemin d’accès physique du dossier de résultats est configuré dans la variable [Noeud de configuration du dossier de contrôle](../../forms/using/watched-folder-in-aem-forms.md#p-create-watched-folder-configuration-node-p).

>[!NOTE]
>
>Le dossier de sortie et le préfixe du nom de fichier sont définis en fonction des paramètres de configuration du dossier de contrôle.

```java
var inputMap = processorContext.getInputMap();
var params = processorContext.getConfigParameters();
var entry = inputMap.entrySet().iterator().next();
var tempFile = new Packages.java.io.File(params.get("tempDir"), params.get("outPrefix") + entry.getKey());
entry.getValue().copyToFile(tempFile);
processorContext.setResult(tempFile.getName(), new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true));
```

#### Emplacement des scripts et considérations de sécurité {#location-of-scripts-and-security-considerations}

Par défaut, un dossier conteneur (/etc/fd/watchfolder/scripts) est fourni, dans lequel les clients peuvent placer leurs scripts, et l’utilisateur du service par défaut utilisé par la structure du dossier de contrôle dispose des autorisations nécessaires pour lire les scripts à partir de cet emplacement.

Si vous souhaitez placer des scripts à un emplacement personnalisé, il est probable que l’utilisateur du service par défaut ne dispose pas des autorisations de lecture pour l’emplacement personnalisé. Pour ce type de scénario, procédez aux étapes suivantes pour fournir les autorisations nécessaires pour l’emplacement personnalisé :

1. Créez un utilisateur système par programmation ou par l’intermédiaire de la console https://&#39;[server]:[port]&#39;/crx/explorer. Vous pouvez également utiliser un utilisateur système existant. Il est important de travailler ici avec les utilisateurs système plutôt qu’avec les utilisateurs normaux.
1. Accordez des autorisations de lecture à l’utilisateur système existant ou nouvellement créé sur l’emplacement personnalisé où les scripts sont stockés. Vous pouvez avoir plusieurs emplacements personnalisés. Indiquez au moins des autorisations de lecture pour tous les emplacements personnalisés.
1. Dans la console de configuration Felix (/system/console/configMgr), recherchez le mappage utilisateur du service pour les dossiers de contrôle. Ce mappage ressemble à &#39;Mapping: adobe-aemds-core-watch-folder=..&#39;.
1. Cliquez sur le mappage. Pour l’entrée « adobe-aemds-core-watch-folder:scripts=fd-service », remplacez fd-service par l’ID de l’utilisateur système personnalisé. Cliquez sur Enregistrer.

Vous pouvez désormais utiliser l’emplacement personnalisé configuré pour enregistrer les scripts.

### Utilisation d’un workflow pour traiter les fichiers d’un dossier de contrôle {#using-a-workflow-to-process-files-of-a-watched-folder}

Les workflows permettent d&#39;automatiser les activités des Experience Manager. Les workflows se composent d’une série d’étapes exécutées dans un ordre spécifique. Chaque étape effectue une activité distincte, telle que l’activation d’une page ou l’envoi d’un message électronique. Les workflows peuvent interagir avec des ressources dans le référentiel, les comptes d’utilisateurs et les services de Experience Manager. Par conséquent, les workflows peuvent coordonner de manière complexe.

* Avant de créer un workflow, tenez compte des points suivants :
* La sortie d’une étape doit être disponible pour toutes les étapes suivantes.
Les étapes doivent pouvoir mettre à jour (ou même supprimer) des sorties existantes générées par les étapes précédentes.
* Les variables mutables sont utilisées pour transmettre les données dynamiques personnalisées entre les étapes.

Effectuez les étapes suivantes pour traiter des fichiers à l’aide des workflows : 

1. Créez une implémentation de l’interface de `com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextProcessor`. Cette fonction est similaire à l’implémentation créée pour un service.

   >[!NOTE]
   >
   >Vous pouvez créer l’implémentation complète entièrement dans ECMAScript.

1. Dans une étape du processus, recherchez le service OSGi de type com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService, puis appelez la méthode execute() du service avec les arguments suivants.

   * Votre implémentation personnalisée de l’interface de WorkflowContextProcessor
   * workItem
   * workflowSession
   * metadata

Si vous utilisez le langage de programmation Java pour implémenter le workflow, le moteur de workflow d’AEM fournit la valeur pour les variables workItem, workflowSession et metadata. Ces variables sont transmises en tant qu’arguments à la méthode execute () de votre implémentation personnalisée WorkflowProcess.

Si vous utilisez ECMAScript pour implémenter le workflow, le moteur de workflow d’AEM fournit la valeur des variables graniteWorkItem, graniteWorkflowSession et metadata. Ces variables sont transmises en tant qu’arguments à la méthode WorkflowContextService.execute () .

L’argument de processWorkflowContext() est un objet de type com.adobe.aemfd.watchfolder.workflow.api.WorkflowContext. L’interface WorkflowContext dispose des API suivantes pour faciliter les remarques spécifiques au workflow mentionnées ci-dessus :

* getWorkItem : renvoie la valeur de la variable WorkItem . Les variables sont transmises à la méthode WorkflowContextService.execute ().
* getWorkflowSession : renvoie la valeur de la variable WorkflowSession. Les variables sont transmises à la méthode WorkflowContextService.execute ().
* getMetadata : renvoie la valeur de la variable de métadonnées. Les variables sont transmises à la méthode WorkflowContextService.execute ().
* getCommittedVariables : renvoie un mappage d’objet en lecture seule représentant les variables définies par des étapes précédentes. Si une variable n’est modifiée dans aucune des étapes précédentes, la valeur par défaut spécifiée lors de la configuration du dossier de contrôle est renvoyée.
* getCommittedResults : renvoie un mappage en lecture seule du document. La carte représente les fichiers de sortie générés par les étapes précédentes.
* setVariable : l’implémentation de WorkflowContextProcessor utilise la variable pour manipuler les variables qui représentent les données dynamiques personnalisées qui circulent entre les étapes. Le nom et le type des variables sont identiques au nom des variables spécifié pendant la [configuration du dossier de contrôle](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p). Pour modifier la valeur d’une variable, appelez l’API setVariable avec une valeur non nulle. Pour supprimer une variable, appelez setVariable() avec une valeur null.

Les API ProcessorContext suivants sont également disponibles :

* getWatchFolderId : renvoie l’ID du dossier de contrôle.
* getInputMap : renvoie un mappage de type Map&lt;string document=&quot;&quot;>. Les clés de la carte sont le nom du fichier d’entrée et un objet document contenant le contenu du fichier. Utilisez l’API getinputMap pour lire les fichiers d’entrée.
* getConfigParameters : renvoie un mappage inaltérable de type Map&lt;string object=&quot;&quot;>. La carte contient les paramètres de configuration d’un dossier de contrôle.
* setResult : l’implémentation de ContentProcessor utilise l’API pour écrire le document de sortie dans le dossier result. Vous pouvez attribuer un nom au fichier de sortie à l’API setResult. L’API peut choisir d’utiliser ou d’ignorer le fichier fourni en fonction du dossier de sortie ou du modèle de fichier spécifié. Si un modèle de dossier est spécifié, les fichiers de sortie portent des noms comme décrit dans les workflows. Si un modèle de fichier est spécifié, les fichiers de sortie portent des noms comme décrit dans le modèle de fichier.

Remarque concernant l’API setResult, lorsqu’elle est utilisée dans les workflows :

* Pour ajouter un nouveau document de sortie qui contribue à la sortie globale du workflow, appelez l’API setResult avec un nom de fichier qui n’a été utilisé comme nom de fichier de sortie par une étape précédente.
* Pour mettre à jour un résultat généré par une étape précédente, appelez l’API setResult avec un nom de fichier déjà utilisé par une étape précédente.
* Pour supprimer un résultat généré par une étape précédente, appelez setResult avec un nom de fichier déjà utilisé par une étape précédente et ayant « null » comme contenu.

>[!NOTE]
>
>L’appel de l’API setResult avec le contenu « null » dans tout autre scénario peut entraîner une erreur.

L’exemple suivant est implémenté comme étape du workflow. Dans cet exemple, ECMAscript utilise un stepCount variable pour suivre le nombre de fois qu’une étape est appelée dans l’instance active du workflow.
Le nom du dossier de sortie est une combinaison de l’étape actuelle, du nom de fichier original et du préfixe spécifié dans le paramètre outPrefix.

ECMAScript obtient une référence du service de contexte de workflow et crée une implémentation de l’interface WorkflowContextProcessor. L’implémentation de WorkflowContextProcessor accepte les fichiers d’entrée, copie le fichier vers un emplacement temporaire, puis renvoie un document représentant le fichier copié. En fonction de la valeur de la variable booléenne purgePrevious, l’étape actuelle supprime la sortie générée la dernière fois par la même étape lorsque l’étape a été lancée dans l’instance de workflow actuelle. En fin de compte, la méthode wfSvc.execute est appelée pour l’implémentation de WorkflowContextProcessor. Le contenu du document de sortie est enregistré dans le dossier result à l’emplacement physique mentionné dans le noeud de configuration du dossier de contrôle.

```javascript
log.error("Watch-folder workflow script called for step: " + graniteWorkItem.getNode().getTitle());
var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
// Custom WorkflowContextProcessor implementation which defines the processWorkflowContext() method purely in JS
var impl = { processWorkflowContext: function (wfContext) {
    var wfId = wfContext.getWatchFolderId();
    var inputMap = wfContext.getInputMap();
    var paramMap = wfContext.getConfigParameters();
    var preResults = wfContext.getCommittedResults();
    var preVars = wfContext.getCommittedVariables();
    log.info("WF ID: " + wfId); // workflowId of type String
    log.info("Inputs: " + inputMap); // Input map of type Map<String, Document>
    log.info("Params: " + paramMap); // Config params of type Map<String, Object>
    log.info("Old results: " + preResults);
    log.info("Old variables: " + preVars);
    var currStepNumber = new Packages.java.lang.Long(new Packages.java.lang.Long(preVars.get("stepCount")).longValue() + 1);
    log.info("Current step number: " + currStepNumber);
    wfContext.setVariable("stepCount", currStepNumber);
    var entry = inputMap.entrySet().iterator().next();
    var tempFile = new Packages.java.io.File(paramMap.get("tempDir"), paramMap.get("outPrefix") + "STEP-" + currStepNumber + "-" + entry.getKey());
    entry.getValue().copyToFile(tempFile);
    var fName = tempFile.getName();
    var outDoc = new Packages.com.adobe.aemfd.docmanager.Document(tempFile, true);
    wfContext.setResult(tempFile.getName(), outDoc);
    var prevStepOutName = paramMap.get("outPrefix") + "STEP-" + (currStepNumber - 1) + "-" + entry.getKey();
    if (preResults.containsKey(prevStepOutName) && paramMap.get("purgePrevious").booleanValue()) {
        log.info("Purging previous step output " + prevStepOutName);
        wfContext.setResult(prevStepOutName, null);
    }
} }
wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
log.info("Exiting workflow script!")
```

### Créer un filtre de mappeur de charge pour mapper la structure d’un dossier de contrôle à la charge utile d’un workflow {#create-payload-mapper-filter-to-map-structure-of-a-watched-folder-to-the-payload-of-a-workflow}

Lorsque vous créez un dossier de contrôle, il crée une structure de dossiers dans le dossier contrôlé. La structure de dossiers comporte des dossiers stage, result, preserve, input et failure. La structure de dossiers peut servir de charge utile d’entrée au workflow et accepter la sortie d’un workflow. Il peut également répertorier les points d’échec, le cas échéant.

Si la structure d’une payload est différente de celle du dossier de contrôle, vous pouvez écrire des scripts personnalisés pour mapper la structure du dossier de contrôle à la payload. Un tel script est appelé filtre du mappeur de charge utile. AEM Forms fournit un filtre de mappeur de charge prêt à l’emploi pour mapper la structure du dossier de contrôle à une charge utile.

#### Création d’un filtre de mappage de charge personnalisé {#creating-a-custom-payload-mapper-filter}

1. Télécharger [Adobe du SDK client](https://repo1.maven.org/maven2/com/adobe/aemfd/aemfd-client-sdk/).
1. Configurez le SDK client dans le chemin de création du projet Maven. Pour commencer, vous pouvez télécharger et ouvrir le projet maven suivant dans l’IDE de votre choix.
1. Modifiez le code de filtre du mappeur de charge disponible dans l’exemple de lot en fonction de vos besoins.
1. Utilisez maven pour créer un lot du filtre de mappeur de charge personnalisé.
1. Utilisation [AEM console des lots](https://localhost:4502/system/console/bundles) pour installer le lot.

   Désormais, le filtre personnalisé de mappeur de charge est répertorié dans l’interface utilisateur AEM dossier de contrôle. Vous pouvez l’utiliser avec votre workflow.

   L’exemple de code suivant met en oeuvre un mappeur basé sur un fichier simple pour les fichiers enregistrés par rapport à une charge utile. Vous pouvez l’utiliser pour commencer.

   ```java
   package com.adobe.aemfd.watchfolder.workflow;
   import com.adobe.aemfd.docmanager.Document;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.PayloadMapper;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowExecutionContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowInitializationContext;
   import com.adobe.aemfd.watchfolder.workflow.api.payload.WorkflowVariable;
   import com.adobe.granite.workflow.exec.Workflow;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.ResourceResolver;
   import javax.jcr.Binary;
   import javax.jcr.Node;
   import java.util.Collection;
   import java.util.HashMap;
   import java.util.Map;
   @Component(immediate = true)
   @Service(value = PayloadMapper.class)
   public class SimpleFileBasedPayloadMapper implements PayloadMapper {
   @Override
   public Node createPayload(WorkflowInitializationContext wfInitCtxt, Node stagingFolder, String uniquePayloadName,
   Map<String, Binary> inputs, Collection<WorkflowVariable> variableDefs) throws Exception {
   Node dirNode = stagingFolder.addNode(uniquePayloadName, "sling:Folder");
   for (Map.Entry<String, Binary> bins: inputs.entrySet()) {
   Node fileNode = dirNode.addNode(bins.getKey(), "nt:file");
   Node resNode = fileNode.addNode ("jcr:content", "nt:resource");
   resNode.setProperty("jcr:data", bins.getValue());
   }
   return dirNode;
   }
   @Override
   public Map<String, Document> getInputs(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload, ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public void setOutput(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   String fileName, Binary contents, int outputMode) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getIntermediateOutputs(WorkflowInitializationContext wfInitCtxt,
   WorkflowExecutionContext wfExecCtxt, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Document> getFinalOutputs(WorkflowInitializationContext wfInitCtxt, Workflow workflow, Node payload,
   ResourceResolver resourceResolver) throws Exception {
   Map<String, Object> params = wfInitCtxt.getConfigParameters();
   Map<String, Document> result = new HashMap<String, Document>();
   for (Map.Entry<String, Object> me: params.entrySet()) {
   String key = me.getKey();
   if (key.startsWith("pm.outfile.")) {
   String fName = (String) me.getValue();
   Document d = new Document(payload.getPath() + "/" + fName, resourceResolver);
   result.put(fName, d);
   }
   }
   return result;
   }
   @Override
   public void setVariable(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt, Node payload,
   WorkflowVariable variable) throws Exception {
   //To change body of implemented methods use File | Settings | File Templates.
   }
   @Override
   public Map<String, Object> getVariables(WorkflowInitializationContext wfInitCtxt, WorkflowExecutionContext wfExecCtxt,
   Node payload) throws Exception {
   return null; //To change body of implemented methods use File | Settings | File Templates.
   }
   }
   ```

## Comment les utilisateurs interagissent avec un dossier de contrôle {#how-users-interact-with-a-watched-folder}

Pour un point de fin Watched Folder, les utilisateurs peuvent lancer des opérations de traitement de fichiers en copiant ou en faisant glisser des fichiers ou des dossiers d’entrée depuis leur bureau vers un dossier de contrôle. Les fichiers sont traités dans l&#39;ordre de leur arrivée.

Pour les points de fin Watched Folder, si une tâche ne nécessite qu’un seul fichier d’entrée, l’utilisateur peut le copier à la racine du dossier de contrôle.

Si la tâche contient plusieurs fichiers d’entrée, l’utilisateur doit créer, en dehors de la hiérarchie du dossier de contrôle, un dossier contenant tous les fichiers requis. Ce nouveau dossier doit inclure les fichiers d’entrée (et éventuellement un fichier DDX s’il est requis par le processus). Une fois le dossier de tâches créé, l’utilisateur le copie dans le dossier d’entrée du dossier de contrôle.

>[!NOTE]
>
>Vérifiez que le serveur d’applications a révoqué l’accès aux fichiers dans le dossier de contrôle. Si AEM Forms ne peut pas supprimer les fichiers du dossier d’entrée après leur analyse, le processus associé est lancé indéfiniment.

## Informations supplémentaires sur les dossiers de contrôle {#additional-information-about-the-watched-folders}

### A propos du ralentissement {#about-throttling}

Lorsque le ralentissement est activé pour un point de fin de dossier de contrôle, il limite le nombre de tâches du dossier de contrôle qui sont traitées à un moment donné. Le nombre maximal de tâches est déterminé par la valeur Taille du lot, également configurable dans le point de fin Watched Folder. Lorsque la limite de ralentissement est atteinte, les documents entrants dans le répertoire d’entrée du dossier de contrôle ne sont pas interrogés. Ces documents resteront dans le répertoire des entrées jusqu’à ce que d’autres tâches du dossier de contrôle soient terminées et qu’une autre demande d’interrogation soit effectuée. Pour le traitement synchrone, toutes les tâches traitées dans un seul sondage sont comptabilisées dans la limite de ralentissement, même si les tâches sont traitées consécutivement dans un seul thread.

>[!NOTE]
>
>Le ralentissement ne se met pas à l’échelle avec une grappe. Lorsque le ralentissement est activé, la grappe dans son ensemble ne traite pas plus de tâches que le nombre spécifié dans la taille du lot à un moment donné. Cette limite s’applique à l’ensemble de la grappe et n’est pas spécifique à chaque noeud de la grappe. Par exemple, avec une taille de lot de 2, la limite de ralentissement peut être atteinte avec un seul noeud qui traite deux tâches, et aucun autre noeud n’interroge le répertoire d’entrée tant que l’une des tâches n’est pas terminée.

#### Fonctionnement du ralentissement {#how-throttling-works}

Watched Folder analyse le dossier input à chaque intervalle de répétition, sélectionne le nombre de fichiers spécifié dans la taille du lot et appelle le service cible pour chacun de ces fichiers. Par exemple, si la taille du lot est de quatre, Watched Folder sélectionne quatre fichiers à chaque analyse, crée quatre demandes d’appel et appelle le service cible. Avant que ces requêtes ne soient terminées, si Watched Folder est appelé, il démarre à nouveau quatre tâches, que les quatre tâches précédentes soient terminées ou non.

L’option de ralentissement empêche Watched Folder d’appeler de nouvelles tâches avant que les tâches précédentes ne soient terminées. Watched Folder détectera les tâches en cours et traitera les nouvelles tâches en fonction de l’attribut Taille du lot défini, moins les tâches en cours. Par exemple, dans le second appel, si le nombre de tâches terminées est de trois seulement et qu’une tâche est toujours en cours, Watched Folder appelle uniquement trois autres tâches.

* Watched Folder s’appuie sur le nombre de fichiers présents dans le dossier stage pour déterminer le nombre de tâches en cours. Si les fichiers restent non traités dans le dossier stage, Watched Folder n’appelle plus aucune tâche. Par exemple, si la taille du lot est de quatre et que trois tâches sont bloquées, Watched Folder appelle une seule tâche dans les appels suivants. Il existe plusieurs scénarios qui peuvent empêcher le traitement des fichiers dans le dossier stage. Lorsque les tâches sont bloquées, l’administrateur peut arrêter le processus sur la page d’administration de Process Management, de sorte que Watched Folder déplace les fichiers hors du dossier stage.
* Si le serveur AEM Forms tombe en panne avant que le dossier de contrôle ne puisse appeler les tâches, l’administrateur peut sortir les fichiers du dossier stage. Pour plus d’informations, voir [Points d’échec et récupération](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).
* Si le serveur AEM Forms est en cours d’exécution mais que Watched Folder ne s’exécute pas lorsque le service Job Manager rappelle, ce qui se produit lorsque les services ne démarrent pas dans l’ordre, l’administrateur peut sortir les fichiers du dossier stage. Pour plus d’informations, voir [Points d’échec et récupération](../../forms/using/watched-folder-in-aem-forms.md#p-failure-points-and-recoveryfailure-points-and-recovery-p).

### Points d’échec et points recoveryFailure et récupération {#failure-points-and-recoveryfailure-points-and-recovery}

À chaque événement d’interrogation, Watched Folder verrouille le dossier input, déplace dans le dossier stage les fichiers correspondant au modèle de fichier d’inclusion, puis déverrouille le dossier input. Le verrouillage est nécessaire afin que deux threads ne sélectionnent pas le même ensemble de fichiers et ne les traitent pas deux fois. La probabilité d’un traitement en double augmente lorsque l’intervalle de répétition est faible et que la taille du lot est importante. Une fois les fichiers déplacés dans le dossier stage, le dossier input est déverrouillé afin que d’autres threads puissent analyser le dossier. Cette étape permet d’obtenir un débit élevé, car d’autres threads peuvent analyser pendant qu’un thread traite les fichiers.

Une fois les fichiers déplacés dans le dossier stage, les demandes d’appel sont créées pour chaque fichier et le service cible est appelé. Dans certains cas, Watched Folder ne peut pas récupérer les fichiers du dossier stage :

* Si le serveur tombe en panne avant que Watched Folder ne puisse créer la demande d’appel, les fichiers du dossier stage restent dans ce dossier et ne sont pas récupérés.

* Si Watched Folder a réussi à créer la demande d’appel pour chacun des fichiers du dossier stage et que le serveur se bloque, deux comportements sont possibles en fonction du type d’appel :

   * **Synchrone**: si Watched Folder est configuré pour appeler le service de manière synchrone, tous les fichiers du dossier stage restent dans ce dossier sans être traités.
   * **Asynchrone**: dans ce cas, Watched Folder s’appuie sur le service Job Manager. Si le service Job Manager rappelle Watched Folder, les fichiers du dossier stage sont déplacés vers le dossier preserve ou le dossier failure en fonction des résultats de l’appel. Si le service Job Manager ne rappelle pas Watched Folder, les fichiers ne seront pas traités dans le dossier stage. Cette situation se produit lorsque Watched Folder ne s’exécute pas lorsque Job Manager rappelle.

#### Récupération des fichiers source non traités dans le dossier stage {#recover-unprocessed-source-files-in-the-stage-folder}

Lorsque Watched Folder ne peut pas traiter les fichiers source dans le dossier stage, vous pouvez récupérer les fichiers non traités.

1. Redémarrez le serveur d’applications ou le noeud.

1. Arrêtez Watched Folder de traiter de nouveaux fichiers d’entrée. Si vous ignorez cette étape, il sera beaucoup plus difficile de déterminer les fichiers qui ne sont pas traités dans le dossier stage. Pour empêcher Watched Folder de traiter de nouveaux fichiers d’entrée, effectuez l’une des tâches suivantes :

   * Remplacez la propriété includeFilePattern du dossier de contrôle par un élément qui ne correspond à aucun nouveau fichier d’entrée (par exemple, saisissez NOMATCH).
   * Suspendre le processus de création de nouveaux fichiers d’entrée.

   Patientez jusqu’à ce qu’AEM Forms récupère et traite tous les fichiers. La majorité des fichiers doit être récupérée et tous les nouveaux fichiers d’entrée traités correctement. La durée d’attente de la récupération et du traitement des fichiers par Watched Folder dépend de la durée de l’opération à appeler et du nombre de fichiers à récupérer.

1. Déterminez les fichiers qui ne peuvent pas être traités. Si vous avez attendu un certain temps et que vous avez terminé l’étape précédente et que des fichiers non traités sont toujours présents dans le dossier stage, passez à l’étape suivante.

   >[!NOTE]
   >
   >Vous pouvez consulter la date et l’horodatage des fichiers dans le répertoire des fichiers traités. Selon le nombre de fichiers et le temps de traitement normal, vous pouvez déterminer les fichiers suffisamment anciens pour être considérés comme bloqués.

1. Copiez les fichiers non traités du répertoire des fichiers traités dans le répertoire des entrées.

1. Si vous avez empêché Watched Folder de traiter de nouveaux fichiers d’entrée à l’étape 2, remplacez le paramètre Inclure le modèle de fichier par sa valeur précédente ou réactivez le processus que vous avez désactivé.

### Assemblage de dossiers de contrôle en chaînes {#chain-watched-folders-together}

Les dossiers de contrôle peuvent être assemblés en chaînes de sorte qu’un document de résultats d’un dossier de contrôle corresponde au document d’entrée du dossier de contrôle suivant. Chaque dossier de contrôle peut appeler un service différent. En configurant les dossiers de contrôle de la sorte, plusieurs services peuvent être appelés. Par exemple, un dossier de contrôle peut convertir des fichiers de PDF au format Adobe PostScript® et un autre dossier de contrôle peut convertir les fichiers PostScript au format PDF/A. Pour ce faire, il vous suffit de définir le dossier de résultats du dossier de contrôle défini par votre premier point de fin afin qu’il pointe vers le dossier d’entrée du dossier de contrôle défini par votre second point de fin.

La sortie de la première conversion serait placée dans le dossier \path\result. Et le dossier d’entrée de la seconde conversion serait \chemin\result et le dossier de sortie de la seconde conversion serait \chemin\result\result (ou le dossier défini dans la zone du dossier de résultats pour la seconde conversion).

### Modèles de fichier et de dossier {#file-and-folder-patterns}

Les administrateurs peuvent indiquer le type du fichier servant à appeler un service. Il est possible d’établir plusieurs modèles de fichier pour chaque dossier de contrôle. Un modèle de fichier peut être l’une des propriétés de fichier suivantes :

* Fichiers possédant des extensions de nom de fichier particulières, par exemple &#42;.dat, &#42;.xml, .pdf, &#42;.&#42;
* Fichiers portant des noms spécifiques, par exemple data.&#42;
* Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

   * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &#42;.[dD][Aa]&#39;port&#39;
   * &#42;.[Xx][Mm][Ll]

* L’administrateur peut définir le modèle de fichier du dossier de sortie dans lequel stocker les résultats. Pour les dossiers de sortie (result, preserve et failure), l’administrateur peut spécifier l’un de ces modèles de fichiers :
* %Y = année (complète)
* %y = année (deux derniers chiffres)
* %M = mois,
* %D = jour du mois,
* %d = jour de l’année,
* %h = heure,
* %m = minute,
* %s = seconde,
* %R = nombre aléatoire entre 0 et 9
* %J = nom de la tâche

Par exemple, le chemin d’accès au dossier de résultats peut être C:\Adobe\Adobe LiveCycle ES4\BarcodedForms\%y\%m\%d.

Les mappages des paramètres de sortie peuvent également spécifier des modèles supplémentaires, tels que :

* %F = nom du fichier source
* %E = extension du nom du fichier source

Si le modèle de mappage des paramètres de sortie se termine par &quot;File.separator&quot; (qui est le séparateur de chemin), un dossier est créé et le contenu est copié dans ce dossier. Si le motif ne se termine pas par « File.separator », le contenu (fichier ou dossier résultant) est créé avec ce nom.

## Utilisation d’un PDF Generator avec un dossier de contrôle {#using-pdf-generator-with-a-watched-folder}

Vous pouvez configurer un dossier de contrôle pour lancer un workflow, un service ou un script destiné à traiter les fichiers d’entrée. Dans la section suivante, nous allons configurer un dossier de contrôle pour lancer ECMAScript. ECMAScript utilise PDF Generator pour convertir des documents Microsoft Word (.docx) en documents PDF.

Effectuez les étapes suivantes pour configurer un dossier de contrôle avec PDF Generator :

1. [Créer un ECMAScript](../../forms/using/watched-folder-in-aem-forms.md#p-create-an-ecmascript-p)
1. [Créer un workflow](../../forms/using/watched-folder-in-aem-forms.md#p-create-a-workflow-p)
1. [Configuration du dossier de contrôle](../../forms/using/watched-folder-in-aem-forms.md#p-configure-the-watched-folder-p)

### Créer un ECMAScript {#create-an-ecmascript}

ECMAScript utilise l’API createPDF du PDF Generator pour convertir des documents Microsoft Word (.docx) en documents du PDF. Effectuez les étapes suivantes pour créer le script :

1. Ouvrez CRXDE Lite dans une fenêtre de navigateur. L’URL est https://&#39;[server]:[port]&#39;/crx/de.

1. Accédez à /etc/workflow/scripts et créez un dossier nommé PDFG.

1. Dans le dossier PDFG, créez un fichier nommé pdfg-openOffice-sample.ecma, et ajoutez le code suivant dans le fichier : 

   ```javascript
   var wfSvc = sling.getService(Packages.com.adobe.aemfd.watchfolder.workflow.api.WorkflowContextService);
   // Custom ContentProcessor implementation which defines the processInputs() method purely in JS
   var impl = { processWorkflowContext: function (wrkfContext) {
   
     //  var logger = Packages.org.slf4j.LoggerFactory.getLogger("cmb-mergeandprint-sample.ecma");
                   var inputMap=wrkfContext.getInputMap();
   
                   var distiller = sling.getService(com.adobe.pdfg.service.api.DistillerService);
                   var generatePDF = sling.getService(com.adobe.pdfg.service.api.GeneratePDFService);
                   var pdfgConfig = sling.getService(com.adobe.pdfg.service.api.PDFGConfigService);
       var result = new Packages.java.util.HashMap();
       var entry = inputMap.entrySet().iterator().next();
       var pdfgOut = generatePDF.createPDF(entry.getValue(), ".docx", "Standard OpenOffice", "Standard", "No Security", null, null);
                   var convertedDoc = pdfgOut.get("ConvertedDoc");
   //   logger.info("SuccessFully saved the document to Ouput Node");
       wrkfContext.setResult(entry.getKey().substring(0, entry.getKey().lastIndexOf('.'))+".pdf",convertedDoc); // Ownership flag set to true for auto temp-file deletion.
   
   } }
   
   wfSvc.execute(impl, graniteWorkItem, graniteWorkflowSession, metaData);
   ```

1. Enregistrez et fermez le fichier.

### Créer un workflow {#create-a-workflow}

1. Ouvrez le workflow AEM UI dans une fenêtre du navigateur.
   <https://[servername>]:&#39;port&#39;/workflow

1. Dans la vue Modèles, cliquez sur **Nouveau**. Dans la boîte de dialogue Nouveau processus, spécifiez **Titre**, puis cliquez sur **OK**.

   ![create-a-workflow-pdf](assets/create-a-workflow-pdf.png)

1. Sélectionnez le workflow nouvellement créé et cliquez sur **Modifier**. Le workflow s’ouvre dans une nouvelle fenêtre.

1. Supprimez l’étape de workflow par défaut. Faites glisser l’étape du processus du Sidekick vers le workflow.

   ![create-a-workflow-pdf2](assets/create-a-workflow-pdf2.png)

1. Cliquez avec le bouton droit de la souris sur l’étape du processus et sélectionnez **Modifier**. La fenêtre Propriétés des étapes s’affiche.

1. Dans l’onglet Traitement, sélectionnez le script ECMAScript. Par exemple, le script pdfg-openOffice-sample.ecma créé dans [Créer un ECMAScript](#p-create-an-ecmascript-p). Activez l’option **Avance du gestionnaire** et cliquez sur **OK**.

   ![create-a-workflow3-pdf](assets/create-a-workflow3-pdf.png)

### Configurer le dossier de contrôle {#configure-the-watched-folder}

1. Ouvrez CRXDE Lite dans une fenêtre de navigateur. https://&#39;[server]:[port]&#39;/crx/de/

1. Accédez au dossier /etc/fd/watchfolder/config/ et créez un nœud de type nt:unstructured.

   ![configure-the-watched-folder-pdf](assets/configure-the-watched-folder-pdf.png)

1. Ajoutez les propriétés suivantes au nœud :

   * folderPath (chaîne) : le chemin du dossier à analyser à des intervalles de temps définis. Ce dossier doit être un emplacement partagé avec tous les serveurs disposant d’un accès complet au serveur.
inputProcessorType (chaîne) : le type du processus à démarrer. Dans ce didacticiel, spécifiez le workflow.

   * inputProcessorId (chaîne) : le comportement de la propriété inputProcessorId repose sur la valeur spécifiée pour la propriété inputProcessorType. Dans cet exemple, la valeur de la propriété inputProcessorType est un workflow. Ainsi, pour la propriété inputProcessorId, spécifiez le chemin suivant du flux de travaux PDFG : /etc/workflow/models/pdfg/jcr:content/model

   * outputFilePattern (chaîne) : motif du fichier de sortie. Vous pouvez spécifier un modèle de dossier ou de fichier. Si un modèle de dossier est spécifié, les fichiers de sortie portent des noms comme décrit dans les workflows. Si un modèle de fichier est spécifié, les fichiers de sortie portent des noms comme décrit dans le modèle de fichier.

   Outre les propriétés obligatoires mentionnées ci-dessus, les dossiers de contrôle prennent également en charge quelques propriétés facultatives. Pour obtenir la liste complète et la description des propriétés facultatives, voir [Propriétés Watched Folder](#watchedfolderproperties).

## Problèmes connus {#watched-folder-known-issues}

Au démarrage d’AEM 6.5 Forms on JEE, les fichiers commencent à être traités avant que JBoss ne démarre complètement et que les fichiers ne soient pas traités. Pour éviter cela, effacez tous les dossiers de contrôle avant de démarrer JBoss.
