---
title: Configuration des points d’entrée des dossiers de contrôle
description: Découvrez comment configurer les points de fin Watched Folder.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: ec169a01-a113-47eb-8803-bd783ea2c943
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '7163'
ht-degree: 27%

---

# Configuration des points d’entrée des dossiers de contrôle {#configuring-watched-folder-endpoints}

Un administrateur peut configurer un dossier réseau, appelé *dossier de contrôle*, de sorte que lorsqu’un utilisateur place un fichier (un fichier de PDF, par exemple) dans le dossier de contrôle, une opération de service configurée est appelée et manipule le fichier. Après que le service a effectué l’opération spécifiée, il enregistre le fichier modifié dans un dossier de sortie spécifié.

## Configuration du service Watched Folder {#configuring-the-watched-folder-service}

Avant de configurer un point de fin Watched Folder, configurez le service Watched Folder. Les paramètres de configuration du service Watched Folder ont deux objectifs :

* Pour configurer les attributs communs à tous les points de fin Watched Folder
* Pour fournir des valeurs par défaut à tous les points de fin Watched Folder

Après avoir configuré le service Watched Folder, vous ajoutez un point de fin Watched Folder au service cible. Lors de l’ajout du point de fin, vous définissez des valeurs, telles que le nom du service et le nom de l’opération, à appeler lorsque des fichiers ou des dossiers sont placés dans le dossier input du service Watched Folder configuré. Pour plus d’informations sur la configuration du service Watched Folder, voir [Paramètres du service Watched Folder](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Création d’un dossier de contrôle {#creating-a-watched-folder}

Vous pouvez créer un dossier de contrôle de deux manières :

* Lors de la configuration des paramètres d’un point de fin Watched Folder, saisissez le chemin d’accès complet au répertoire parent dans la zone Chemin d’accès et ajoutez le nom du dossier de contrôle à créer, comme indiqué dans l’exemple suivant :
  `  C:\MyPDFs\MyWatchedFolder`Comme le dossier MyWatchedFolder n’existe pas encore, AEM Forms tente de le créer à cet emplacement.

* Créez un dossier sur le système de fichiers avant de configurer un point de fin Watched Folder, puis saisissez le chemin d’accès complet dans la zone Chemin d’accès.

Dans un environnement organisé en grappe, le dossier qui sera utilisé comme dossier de contrôle doit être accessible, modifiable et partagé sur le système de fichiers ou le réseau. Dans ce scénario, chaque instance de serveur d’applications de la grappe doit avoir accès au même dossier partagé.

Sous Windows, si le serveur d’applications s’exécute en tant que service, il doit être démarré avec un accès approprié au dossier partagé de l’une des manières suivantes :

* Configurez le paramètre **Ouvrir une session en tant que du service du serveur d’applications** pour qu’il démarre avec un utilisateur disposant des droits d’accès appropriés sur le dossier de contrôle partagé.
* Sélectionnez Autoriser le service à interagir avec le bureau dans le champ Exécuter en tant que système local. Cette option nécessite que le dossier de contrôle partagé soit accessible et modifiable par tous.

## Association des dossiers de contrôle {#chaining-together-watched-folders}

Les dossiers de contrôle peuvent être assemblés en chaîne de sorte qu’un document de résultat d’un dossier de contrôle soit le document d’entrée du dossier de contrôle suivant. Chaque dossier de contrôle peut appeler un service différent. En configurant les dossiers de contrôle de cette manière, plusieurs services peuvent être appelés. Par exemple, un dossier de contrôle peut convertir des fichiers de PDF au format Adobe PostScript® et un autre dossier de contrôle, des fichiers PostScript au format PDF/A. Pour ce faire, définissez simplement la variable *result* du dossier de contrôle défini par votre premier point de fin pour pointer vers le *input* dossier du dossier de contrôle défini par votre second point de fin.

La sortie de la première conversion serait placée dans le dossier \path\result. Et le dossier d’entrée de la seconde conversion serait \chemin\result et le dossier de sortie de la seconde conversion serait \chemin\result\result (ou le dossier défini dans la zone du dossier de résultats pour la seconde conversion).

## Comment les utilisateurs interagissent avec les dossiers de contrôle {#how-users-interact-with-watched-folders}

Pour un point de fin Watched Folder, les utilisateurs peuvent appeler en copiant ou en faisant glisser des fichiers ou des dossiers d’entrée depuis leur bureau vers un dossier de contrôle. Les fichiers seront traités dans l’ordre dans lequel ils arrivent.

Pour les points de fin Watched Folder, si la tâche ne nécessite qu’un seul fichier d’entrée, l’utilisateur peut le copier à la racine du dossier de contrôle.

Si la tâche contient plusieurs fichiers d’entrée, l’utilisateur doit créer, en dehors de la hiérarchie des dossiers de contrôle, un dossier contenant tous les fichiers requis. Ce nouveau dossier doit inclure les fichiers d’entrée (et éventuellement un fichier DDX s’il est requis par le processus). Une fois le dossier de tâche créé, l’utilisateur le copie dans le dossier input du dossier de contrôle.

>[!NOTE]
>
>Assurez-vous que le serveur d’applications a supprimé l’accès aux fichiers du dossier de contrôle. Si AEM forms ne peut pas supprimer les fichiers du dossier d’entrée après leur analyse, le processus associé est appelé indéfiniment.

## Sortie du dossier de contrôle {#watched-folder-output}

Lorsque l’entrée est un dossier et que la sortie est composée de plusieurs fichiers, AEM forms crée un dossier de sortie portant le même nom que le dossier input et copie les fichiers de sortie dans ce dossier. Lorsque la sortie est composée d’un document map contenant une paire clé-valeur, telle que la sortie d’un processus Output, la clé est utilisée comme nom de fichier de sortie.

Les noms de fichiers de sortie issus d’un processus de point de fin ne peuvent pas contenir de caractères autres que des lettres, des chiffres et un point (.) avant l’extension de fichier. AEM forms convertit les autres caractères en valeurs hexadécimales.

Les applications clientes récupèrent les documents de résultat dans le dossier result du dossier de contrôle. Les erreurs de traitement sont consignées dans le dossier des échecs du dossier de contrôle.

## Fonctionnement de Watched Folder {#how-watched-folder-works}

Le module Watched Folder contient les services suivants :

* Service Watched Folder
* provider.file_scan_service
* provider.file_write_results_service

Outre les services répertoriés ci-dessus, Watched Folder dépend également d’autres services, notamment le service Planificateur pour la planification des tâches et le service Job Manager pour la prise en charge de l’appel asynchrone des services cibles.

### Traitement d’une demande d’appel par Watched Folder {#how-watched-folder-processes-an-invocation-request}

Le service Watched Folder gère la création, la mise à jour et la suppression des points de fin. Une fois les points de fin créés par l’administrateur, ils sont programmés pour être déclenchés par le service de programmation en fonction de l’intervalle de répétition spécifié ou de l’expression cron.

Ce diagramme illustre comment Watched Folder traite une demande d’appel.

![en_watchedfolder](assets/en_watchedfolder.png)

Le processus d’appel d’un service à l’aide de dossiers de contrôle est le suivant :

1. Une application client place des fichiers ou des dossiers dans le dossier input du dossier de contrôle.
1. Lorsque l’intervalle d’analyse de tâche se produit, le service de programmation appelle provider.file_scan_service pour traiter les fichiers ou les dossiers dans le dossier input.
1. provider.file_scan_service effectue les tâches suivantes :


   * Analyse le dossier input à la recherche de fichiers ou de dossiers correspondant au modèle de fichier d’inclusion et exclut les fichiers ou les dossiers pour le modèle de fichier d’exclusion spécifié. Les fichiers ou dossiers les plus anciens sont sélectionnés en premier. Les fichiers et les dossiers antérieurs à la durée d’attente sont également sélectionnés. Au cours d’une analyse, le nombre de fichiers ou de dossiers traités dépend de la taille du lot. Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](configuring-watched-folder-endpoints.md#about-file-patterns). Pour plus d’informations sur la définition de la taille du lot, voir [Paramètres du service Watched Folder](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Récupère les fichiers ou les dossiers à traiter. Si les fichiers ou les dossiers ne sont pas entièrement téléchargés, ils sont sélectionnés lors de l’analyse suivante. Pour s’assurer que les dossiers sont entièrement téléchargés, les administrateurs doivent créer un dossier avec un nom en utilisant le modèle de fichier d’exclusion. Une fois que le dossier contient tous les fichiers, il doit être renommé selon le modèle spécifié dans le modèle de fichier d’inclusion. Cette étape permet de s’assurer que le dossier contient tous les fichiers nécessaires pour appeler le service. Pour plus d’informations sur le téléchargement complet des dossiers, voir [Conseils et astuces pour les dossiers de contrôle](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Déplace les fichiers ou les dossiers vers le dossier stage après les avoir sélectionnés pour traitement.
   * Convertit les fichiers ou les dossiers du dossier stage en entrée appropriée en fonction des mappages des paramètres d’entrée du point de fin. Pour obtenir des exemples de mappages des paramètres d’entrée, voir [Conseils et astuces pour les dossiers de contrôle](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. Le service cible configuré pour le point de terminaison est appelé de manière synchrone ou asynchrone. Le service cible est appelé à l’aide du nom d’utilisateur et du mot de passe configurés pour le point de terminaison .

   * Un appel synchrone appelle directement le service cible et traite immédiatement la réponse.
   * Pour un appel asynchrone, le service cible est appelé par le biais du service Job Manager, qui place la demande dans une file d’attente. Le service Job Manager, à son tour, appelle provider.file_write_results_service pour gérer les résultats.

1. provider.file_write_results_service gère la réponse ou l’échec de l’appel du service cible. En cas de réussite, la sortie est enregistrée dans le dossier result en fonction de la configuration du point de fin. provider.file_write_results_service conserve également la source si le point de terminaison est configuré pour conserver les résultats une fois l’opération terminée.

   Lorsque l’appel du service cible entraîne un échec, provider.file_write_results_service consigne la raison de l’échec dans un fichier failure.log et place ce fichier dans le dossier failure. Le dossier failure est créé en fonction des paramètres de configuration spécifiés pour le point de terminaison . Lorsque l’administrateur définit l’option Conserver en cas d’échec pour la configuration du point de terminaison, provider.file_write_results_service copie également les fichiers source dans le dossier failure. Pour plus d’informations sur la récupération des fichiers du dossier failure, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Paramètres des points d’entrée d’un dossier de contrôle {#watched-folder-endpoint-settings}

Utilisez les paramètres suivants pour configurer un point de fin Watched Folder.

**Nom :**(obligatoire) identifie le point d’entrée. N’incluez pas de caractère « &lt; », car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL comme nom de point de terminaison, assurez-vous qu’elle est conforme aux règles de syntaxe spécifiées dans la norme RFC1738.

**Description :** fournit une description du point d’entrée. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**Chemin d’accès :** (obligatoire) indique l’emplacement du dossier de contrôle. Dans un environnement organisé en grappe, ce paramètre doit pointer vers un dossier réseau partagé accessible à tous les ordinateurs de la grappe.

**Asynchrone :** identifie le type d’appel comme étant asynchrone ou synchrone. La valeur par défaut est asynchrone. Le mode asynchrone est recommandé pour les processus de longue durée, tandis que le mode synchrone est recommandé pour les processus transitoires ou de courte durée.

**Expression Cron :** saisissez une expression cron si le dossier de contrôle doit être programmé en utilisant une expression de ce type. Si ce paramètre est configuré, l’intervalle de répétition est ignoré.

**Intervalle de répétition :** intervalle (en secondes) entre les analyses du dossier de contrôle d’entrée. À moins que le paramètre Ralentissement ne soit activé, l’intervalle de répétition doit être supérieur au temps nécessaire au traitement d’une tâche moyenne ; dans le cas contraire, le système risque d’être surchargé. La valeur par défaut est 5. Pour plus d’informations, voir la description de la taille du lot .

**Nombre de répétitions :** nombre d’analyses du dossier ou du répertoire par le dossier de contrôle. La valeur -1 indique une analyse indéfinie. La valeur par défaut est -1.

**Ralentissement :** lorsque cette option est sélectionnée, elle permet de limiter le nombre de tâches du dossier de contrôle quʼAEM Forms peut traiter à un moment donné. La valeur Taille du lot détermine le nombre maximal de tâches. Voir A propos du ralentissement .

**Nom d’utilisateur :** (obligatoire) nom d’utilisateur utilisé lors de l’appel d’un service cible à partir du dossier de contrôle. La valeur par défaut est SuperAdmin.

**Nom de domaine :** (obligatoire) domaine de l’utilisateur. La valeur par défaut est DefaultDom.

**Taille du lot :** le nombre de fichiers ou de dossiers à sélectionner par analyse. Utilisez pour éviter une surcharge du système ; l’analyse simultanée d’un trop grand nombre de fichiers peut entraîner un blocage. La valeur par défaut est 2.

Les paramètres Intervalle de répétition et Taille du lot déterminent le nombre de fichiers sélectionnés par Watched Folder à chaque analyse. Watched Folder utilise un pool de threads Quartz pour analyser le dossier input. Le pool de threads est partagé avec d’autres services. Si l’intervalle d’analyse est court, les threads analysent souvent le dossier input. Si des fichiers sont déposés fréquemment dans le dossier de contrôle, vous devez limiter l’intervalle d’analyse. Si les fichiers sont déposés peu fréquemment, utilisez un intervalle d’analyse plus long afin que les autres services puissent utiliser les threads.

Si un volume important de fichiers est déposé, définissez une grande taille de lot. Par exemple, si le service appelé par le point de fin Watched Folder peut traiter 700 fichiers par minute et que les utilisateurs déposent les fichiers dans le dossier input au même rythme, la définition de la taille du lot sur 350 et de l’intervalle de répétition sur 30 secondes permettra d’améliorer les performances de Watched Folder sans avoir à analyser trop souvent le dossier de contrôle.

Lorsque des fichiers sont déposés dans le dossier de contrôle, il les répertorie dans l’entrée, ce qui peut réduire les performances si l’analyse est effectuée toutes les secondes. L’allongement de l’intervalle d’analyse permet d’améliorer les performances. Si le volume de fichiers déposés est faible, ajustez la taille du lot et l’intervalle de répétition en conséquence. Par exemple, si 10 fichiers sont déposés toutes les secondes, essayez de définir l’intervalle de répétition sur 1 seconde et la taille du lot sur 10.

**Durée d’attente :** durée d’attente (en millisecondes) entre la création d’un dossier ou d’un fichier et son analyse. Par exemple, si la durée d’attente est de 3 600 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce dernier sera sélectionné à l’issue d’un laps de temps de 59 minutes ou plus. La valeur par défaut est 0.

Ce paramètre est utile pour garantir qu’un fichier ou un dossier est entièrement copié dans le dossier input. Par exemple, si vous devez traiter un fichier volumineux dont le téléchargement dure dix minutes, définissez une durée d’attente de 10&amp;ast;60 &amp;ast;1000 millisecondes. ce qui évite que le dossier de contrôle analyse le fichier tant que ce dernier a une existence inférieure à dix minutes.

**Exclure le modèle de fichier :** liste délimitée par des points-virgules **;** des modèles utilisés par un dossier de contrôle pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Aucun fichier ou dossier avec ce modèle ne sera analysé en vue du traitement.

Ce paramètre est utile lorsque l’entrée est un dossier contenant plusieurs fichiers. Le contenu du dossier peut être copié dans un dossier dont le nom sera choisi par le dossier de contrôle. Cela empêche le dossier de contrôle de sélectionner un dossier à traiter avant que le dossier ne soit complètement copié dans le dossier input.

Vous pouvez utiliser des modèles de fichiers pour exclure les types de fichiers suivants :

* Fichiers dotés d’extensions de nom de fichier spécifiques ; par exemple, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Fichiers portant des noms spécifiques, par exemple data.&amp;ast; exclut les fichiers et dossiers nommés *data1*, *data2*, etc.
* Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

   * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](configuring-watched-folder-endpoints.md#about-file-patterns).

**Inclure le modèle de fichier** : liste délimitée par des points-virgules **;** des modèles utilisés par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Ainsi, si le paramètre Inclure le modèle de fichier a pour valeur input&amp;ast;, tous les fichiers et dossiers correspondant à input&amp;ast; sont sélectionnés. Cela concerne les fichiers et les dossiers nommés input1, input2, etc.

La valeur par défaut est &amp;ast; et renvoie à tous les fichiers et dossiers.

Vous pouvez utiliser des modèles de fichiers pour inclure les types de fichiers suivants :

* Fichiers dotés d’extensions de nom de fichier spécifiques ; par exemple, &amp;ast;.dat, &amp;ast;.xml, &amp;ast;.pdf.
* Fichiers portant des noms spécifiques, par exemple data.&amp;ast; inclut les fichiers et dossiers nommés *data1*, *data2*, etc.
* Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

   * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](configuring-watched-folder-endpoints.md#about-file-patterns).


**Dossier result :** dossier dans lequel les résultats enregistrés sont stockés. Si les résultats ne s’affichent pas dans ce dossier, vérifiez le dossier des échecs. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier des échecs. Cette valeur peut être un chemin d’accès absolu ou relatif avec les modèles de fichiers suivants :

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

Par exemple, si nous sommes le 17 juillet 2009 à 20 h et que vous définissez `C:/Test/WF0/failure/%Y/%M/%D/%H/`, le dossier de résultat est alors `C:/Test/WF0/failure/2009/07/17/20`.

Si le chemin d’accès n’est pas absolu mais relatif, le dossier est créé dans le dossier de contrôle. La valeur par défaut est result/%Y/%M/%D/, qui correspond au dossier Result dans le dossier de contrôle. Pour plus d’informations sur les modèles de fichiers, voir [À propos des modèles de fichier](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Plus les dossiers de résultats sont petits, plus les performances de Watched Folder augmentent. Par exemple, si la charge estimée pour le dossier de contrôle est de 1 000 fichiers par heure, utilisez un modèle de type `result/%Y%M%D%H`, afin qu’un nouveau sous-dossier soit créé toutes les heures. Si la charge est moindre (par exemple, 1 000 fichiers par jour), vous pouvez utiliser un modèle de type `result/%Y%M%D`.

**Dossier preserve :** dossier dans lequel les fichiers sont stockés après avoir été analysés et sélectionnés. Le chemin d’accès peut être absolu, relatif ou nul. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier result. La valeur par défaut est preserve/%Y/%M/%D/.

**Dossier failure :** dossier dans lequel les fichiers en échec sont enregistrés. Cet emplacement dépend toujours du dossier de contrôle. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier Résultat.

Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier des échecs.

La valeur par défaut est failure/%Y/%M/%D/.

**Conserver en cas d’échec :** conservation des fichiers d’entrée en cas d’échec de l’exécution de l’opération dans un service. La valeur par défaut est true.

**Remplacer les noms de fichier en double :** lorsque cet attribut est défini sur « true », les fichiers du dossier obtenu et du dossier conservé sont remplacés. Lorsque la valeur est False, les fichiers et les dossiers comportant un suffixe d’index numérique sont utilisés pour le nom. La valeur par défaut est False.

**Durée de la purge :** (obligatoire) les fichiers et les sous-dossiers du dossier result sont vidés lorsqu’ils sont plus anciens que cette valeur. Cette valeur est mesurée en jours. Ce paramètre s’avère utile pour s’assurer que le dossier de résultats n’est pas plein.

Une valeur de -1 jour indique de ne jamais supprimer le dossier de résultats. La valeur par défaut est -1.

**Nom de l’opération :** (obligatoire) liste des opérations pouvant être attribuées au point d’entrée Watched Folder.

**Mappages des paramètres d’entrée :** permet de configurer l’entrée requise pour traiter le service et l’opération. Les paramètres disponibles dépendent du service qui utilise le point de fin Watched Folder. Voici les deux types d’entrées :

**Littéral :** le dossier de contrôle utilise la valeur saisie dans le champ telle qu’elle est affichée. Tous les types Java de base sont pris en charge. Par exemple, si une interface API utilise une entrée de type chaîne, long, nombre entier ou valeur booléenne, cette entrée est convertie en type approprié, puis le service est appelé.

**Variable :** la valeur saisie est un modèle de fichier que le dossier de contrôle utilise pour sélectionner l’entrée. Par exemple, dans le cas du service de mot de passe chiffré où le document d’entrée doit être un fichier PDF, l’utilisateur peut utiliser &amp;ast;.pdf comme modèle de fichier. Le dossier de contrôle récupère tous les fichiers du dossier de contrôle correspondant à ce modèle et appelle le service pour chaque fichier. Lorsqu’une variable est utilisée, tous les fichiers d’entrée sont convertis en documents. Seules les API qui utilisent le type d’entrée Document sont prises en charge.

**Mappages des paramètres de sortie :** permet de configurer les sorties du service et de l’opération. Les paramètres disponibles dépendent du service qui utilise le point de fin Watched Folder.

La sortie Watched Folder peut être un document unique, une liste de documents ou une carte de documents. Ces documents de sortie sont ensuite enregistrés dans le dossier result, à l’aide du modèle spécifié dans le mappage des paramètres de sortie.

>[!NOTE]
>
>La définition de noms de fichier de sortie uniques améliore les performances. Imaginez, par exemple, le cas où un service renvoie un document de sortie que le mappage des paramètres de sortie associe à `%F.%E` (le nom et l’extension du fichier d’entrée). Dans ce cas, si des utilisateurs déposent chaque minute des fichiers dont le nom est identique, que le dossier result est défini sur `result/%Y/%M/%D` et que le paramètre Remplacer les noms de fichier en double est inactif, Watched Folder tente de résoudre les noms de fichiers en double. Le processus impliqué dans la résolution des noms de fichiers en double peut affecter les performances. Si vous vous trouvez dans cette situation, définissez le mappage des paramètres de sortie sur `%F_%h_%m_%s_%l` pour ajouter les heures, les minutes, les secondes et les millisecondes au nom du fichier, ou assurez-vous que les fichiers déposés possèdent des noms uniques afin d’améliorer les performances.

## A propos des modèles de fichier {#about-file-patterns}

Les administrateurs peuvent indiquer le type du fichier servant à appeler un service. Plusieurs modèles de fichiers peuvent être définis pour chaque dossier de contrôle. Un modèle de fichier peut être l’une des propriétés de fichier suivantes :

* Fichiers dotés d’extensions de nom de fichier spécifiques ; par exemple, &amp;ast;.dat, &amp;ast;.xml et &amp;ast;.pdf,;
* Fichiers portant des noms spécifiques, par exemple data.&amp;ast;
* Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

   * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

L’administrateur peut définir le modèle de fichier du dossier de sortie dans lequel stocker les résultats. Pour les dossiers de sortie (result, preserve et failure), l’administrateur peut spécifier l’un de ces modèles de fichiers :

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

Par exemple, le chemin d’accès au dossier de résultats peut être `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Les mappages des paramètres de sortie peuvent également spécifier des modèles supplémentaires, tels que :

* %F = nom du fichier source
* %E = extension du nom du fichier source

Si le modèle de mappage des paramètres de sortie se termine par &quot;File.separator&quot; (qui est le séparateur de chemin), un dossier est créé et le contenu est copié dans ce dossier. Si le modèle ne se termine pas par « File.separator », le contenu (fichier ou dossier des résultats) est créé et utilise ce nom. Pour plus d’informations sur les mappages des paramètres de sortie, voir [Conseils et astuces pour les dossiers de contrôle](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## A propos du ralentissement {#about-throttling}

Lorsque le ralentissement est activé pour un point de fin de dossier de contrôle, il limite le nombre de tâches du dossier de contrôle pouvant être traitées à un moment donné. Le nombre maximal de tâches est déterminé par la valeur Taille du lot, également configurable dans le point de fin Watched Folder. Les documents entrants dans le répertoire d’entrée du dossier de contrôle ne seront pas interrogés lorsque la limite de ralentissement aura été atteinte. Les documents resteront également dans le répertoire des entrées jusqu’à ce que d’autres tâches du dossier de contrôle soient terminées et qu’une autre tentative d’interrogation soit effectuée. Dans le cas d’un traitement synchrone, toutes les tâches traitées dans un seul sondage sont comptabilisées dans la limite de ralentissement, même si les tâches sont traitées consécutivement dans un seul thread.

>[!NOTE]
>
>Le ralentissement ne se met pas à l’échelle avec une grappe. Lorsque le ralentissement est activé, la grappe dans son ensemble ne traite pas plus de tâches que le nombre spécifié dans la taille du lot à un moment donné. Cette limite s’applique à l’ensemble de la grappe et n’est pas spécifique à chaque noeud de la grappe. Par exemple, avec une taille de lot de 2, la limite de ralentissement peut être atteinte avec un seul noeud qui traite deux tâches, et aucun autre noeud n’interroge le répertoire d’entrée tant que l’une des tâches n’est pas terminée.

### Fonctionnement du ralentissement {#how-throttling-works}

Watched Folder analyse le dossier input à chaque intervalle de répétition, sélectionne le nombre de fichiers spécifié dans la taille du lot et appelle le service cible pour chacun de ces fichiers. Par exemple, si la taille du lot est de quatre, Watched Folder sélectionnera quatre fichiers à chaque analyse, créera quatre demandes d’appel et appellera le service cible. Avant que ces requêtes ne soient terminées, si Watched Folder est appelé, il démarrera à nouveau quatre tâches, que les quatre tâches précédentes soient terminées ou non.

L’option de ralentissement empêche le dossier de contrôle d’appeler de nouvelles tâches avant que les tâches précédentes ne soient terminées. Watched Folder détectera les tâches en cours et traitera les nouvelles tâches en fonction de la taille du lot moins les tâches en cours. Par exemple, dans le second appel, si le nombre de tâches terminées est de trois seulement et qu’une tâche est toujours en cours, Watched Folder appelle uniquement trois autres tâches.

* Watched Folder s’appuie sur le nombre de fichiers présents dans le dossier stage pour déterminer le nombre de tâches en cours. Si les fichiers restent non traités dans le dossier stage, Watched Folder n’appelle plus aucune tâche. Par exemple, si la taille du lot est de quatre et que trois tâches sont bloquées, Watched Folder appellera une seule tâche dans les appels suivants. Il existe plusieurs scénarios qui peuvent empêcher le traitement des fichiers dans le dossier stage. Si les tâches sont bloquées, l’administrateur peut mettre un terme au traitement dans la page d’administration du processus des formulaires et Watched Folder sortira alors les fichiers du dossier d’étape.
* Si le serveur Forms tombe en panne avant que Watched Folder puisse appeler les tâches, l’administrateur peut sortir les fichiers du dossier d’étape. Pour plus d’informations, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Si le serveur Forms fonctionne mais que Watched Folder ne fonctionne pas lorsque le service Job Manager appelle de nouveau, ce qui arrive lorsque les services ne sont pas exécutés dans la séquence définie, l’administrateur peut sortir les fichiers du dossier d’étape. Pour plus d’informations, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Performances et évolutivité {#performance-and-scalability}

Watched Folder peut traiter 100 dossiers au total sur un seul noeud. Les performances de Watched Folder dépendent des performances du serveur Forms. Pour les appels asynchrones, les performances dépendent davantage de la charge du système et des tâches qui se trouvent dans la file d’attente de Job Manager.

Les performances de Watched Folder peuvent être améliorées en ajoutant des noeuds à la grappe. Les tâches de Watched Folder sont distribuées sur les noeuds de la grappe en vertu du planificateur Quartz et, dans le cas de requêtes asynchrones, par le service Job Manager. Toutes les tâches sont conservées dans la base de données.

Watched Folder dépend du service Planificateur pour la planification, la désplanification et la replanification des tâches. D’autres services, tels que le service de gestion des événements, le service User Manager et le service Email Provider, sont disponibles et partagent le pool de threads du service de programmation. Cela peut avoir une incidence sur les performances de Watched Folder. Le réglage du pool de threads du service de programmation sera nécessaire lorsque tous les services commenceront à l’utiliser.

## Dossiers de contrôle dans une grappe {#watched-folders-in-a-cluster}

Dans une grappe, Watched Folder dépend du planificateur Quartz et du service Job Manager pour l’équilibrage de charge et le basculement. Pour plus d’informations sur le comportement de la grappe Quartz, voir [Documentation Quartz](https://www.quartz-scheduler.org/documentation).

Watched Folder effectue les trois tâches principales suivantes à chaque sondage :

* Analyser le dossier
* Appeler le service cible
* Gérer les résultats

Le comportement de l’équilibrage de charge et du basculement varie selon que le dossier de contrôle est configuré pour un appel synchrone ou asynchrone.

### Dossier de contrôle synchrone dans une grappe {#synchronous-watched-folder-in-a-cluster}

Pour les appels synchrones, l’équilibreur de charge Quartz décide quel noeud va obtenir l’événement d’interrogation. Le noeud qui reçoit l’événement d’interrogation effectue toutes les tâches : analyse du dossier, appel du service cible et gestion des résultats.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Pour les appels synchrones, lorsqu’un noeud échoue, le planificateur Quartz envoie de nouveaux événements d’interrogation aux autres noeuds. Les appels démarrés sur le noeud en échec seront perdus. Pour plus d’informations sur la manière de récupérer les fichiers associés à la tâche en échec, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Dossier de contrôle asynchrone dans une grappe {#asynchronous-watched-folder-in-a-cluster}

Pour les appels asynchrones, l’équilibreur de charge Quartz décide quel noeud recevra l’événement d’interrogation. Le noeud qui obtient l’événement d’interrogation analyse le dossier input et appelle le service cible en plaçant la demande dans la file d’attente du service Job Manager. L’équilibreur de charge du service Job Manager est quant à lui chargé de décider quel noeud traitera la demande d’appel. Il est possible que même si le noeud A a créé la demande d’appel, le noeud B termine le traitement de la demande. Ou le noeud qui a démarré la demande d’appel peut également terminer le traitement de la demande.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Pour les appels asynchrones, lorsqu’un noeud échoue, le planificateur Quartz envoie de nouveaux événements d’interrogation aux autres noeuds. Les demandes d’appel créées sur le noeud en échec se trouvent dans la file d’attente du service Job Manager et sont envoyées à d’autres noeuds en vue du traitement. Les fichiers pour lesquels des demandes d’appel ne sont pas créées resteront dans le dossier stage. Pour plus d’informations sur la manière de récupérer les fichiers associés à la tâche en échec, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Points d’échec et récupération {#failure-points-and-recovery}

À chaque événement d’interrogation, Watched Folder verrouille le dossier input, déplace dans le dossier stage les fichiers correspondant au modèle de fichier d’inclusion, puis déverrouille le dossier input. Le verrouillage est nécessaire afin que deux threads ne sélectionnent pas le même ensemble de fichiers et ne les traitent pas deux fois. Les chances que cela se produise augmentent avec un petit intervalle de répétition et une grande taille de lot. Une fois les fichiers déplacés dans le dossier stage, le dossier input est déverrouillé afin que d’autres threads puissent analyser le dossier. Cette étape permet d’obtenir un débit élevé, car d’autres threads peuvent analyser pendant qu’un thread traite les fichiers.

Une fois les fichiers déplacés dans le dossier stage, les demandes d’appel sont créées pour chaque fichier et le service cible est appelé. Dans certains cas, Watched Folder ne peut pas récupérer les fichiers du dossier stage :

* Si le serveur tombe en panne avant que Watched Folder ne puisse créer la demande d’appel, les fichiers du dossier stage restent dans ce dossier et ne sont pas récupérés.
* Si Watched Folder a réussi à créer la demande d’appel pour chacun des fichiers du dossier stage et que le serveur se bloque, deux comportements sont possibles en fonction du type d’appel :

**Synchrone :** Si Watched Folder est configuré pour appeler le service de manière synchrone, tous les fichiers du dossier stage restent dans ce dossier et ne subissent aucun traitement.

**Asynchrone :** Dans ce cas, Watched Folder s’appuie sur le service Job Manager. Si le service Job Manager rappelle Watched Folder, les fichiers du dossier stage sont déplacés vers le dossier preserve ou le dossier failure en fonction des résultats de l’appel. Si le service Job Manager ne rappelle pas Watched Folder, les fichiers ne seront pas traités dans le dossier stage. Cette situation se produit lorsque Watched Folder ne s’exécute pas lorsque Job Manager rappelle.

### Récupération des fichiers source non traités dans le dossier stage {#recovering-unprocessed-source-files-in-the-stage-folder}

Lorsque Watched Folder ne peut pas traiter les fichiers source dans le dossier stage, vous pouvez récupérer les fichiers non traités.

1. Redémarrez le serveur d’applications ou le noeud.
1. (Facultatif) Arrêtez Watched Folder de traiter les nouveaux fichiers d’entrée. Si vous ignorez cette étape, il sera beaucoup plus difficile de déterminer les fichiers qui ne sont pas traités dans le dossier stage. Pour empêcher Watched Folder de traiter de nouveaux fichiers d’entrée, effectuez l’une des tâches suivantes :

   * Dans Applications et services, modifiez le paramètre Inclure le modèle de fichier pour le point d’entrée du dossier de contrôle et donnez-lui une valeur qui ne correspond à aucun nouveau fichier d’entrée (par exemple, saisissez `NOMATCH`).
   * Suspendre le processus de création de nouveaux fichiers d’entrée.

   Patientez jusqu’à ce que AEM forms récupère et traite tous les fichiers. La majorité des fichiers doit être récupérée et tous les nouveaux fichiers d’entrée traités correctement. La durée d’attente de la récupération et du traitement des fichiers par Watched Folder dépend de la durée de l’opération à appeler et du nombre de fichiers à récupérer.

1. Déterminez les fichiers qui ne peuvent pas être traités. Si vous avez attendu un certain temps et que vous avez terminé l’étape précédente et que des fichiers non traités sont toujours présents dans le dossier stage, passez à l’étape suivante.

   >[!NOTE]
   >
   >Vous pouvez consulter la date et l’horodatage des fichiers dans le répertoire des fichiers traités. Selon le nombre de fichiers et le temps de traitement normal, vous pouvez déterminer les fichiers suffisamment anciens pour être considérés comme bloqués.

1. Copiez les fichiers non traités du répertoire des fichiers traités dans le répertoire des entrées.
1. Si vous avez empêché Watched Folder de traiter de nouveaux fichiers d’entrée à l’étape 2, remplacez le paramètre Inclure le modèle de fichier par sa valeur précédente ou réactivez le processus que vous avez désactivé.

## Considérations relatives à la sécurité des dossiers de contrôle {#security-considerations-for-watched-folders}

Chaque dossier de contrôle est configuré avec un nom d’utilisateur et un mot de passe. Ces informations d’identification sont utilisées lors de l’appel des services. Watched Folder s’appuie sur le fait que le dossier partagé est protégé par le système de fichiers de sécurité sous-jacent afin que seul le propriétaire du dossier de contrôle puisse accéder au dossier partagé.

## Conseils et astuces pour les dossiers de contrôle {#tips-and-tricks-for-watched-folders}

Voici quelques conseils et astuces lors de la configuration du point de fin Watched Folder :

* Si, sous Windows, un dossier de contrôle traite des fichiers image, spécifiez des valeurs pour l’option Inclure le modèle de fichier ou Exclure le modèle de fichier afin d’empêcher que le fichier Thumbs.db généré automatiquement par Windows ne soit interrogé par le dossier de contrôle.
* Si une expression cron est spécifiée, l’intervalle de répétition est ignoré. L’utilisation de l’expression cron est basée sur le système de planification des tâches Open Source Quartz, version 1.4.0.
* La taille du lot correspond au nombre de fichiers ou de dossiers qui seront sélectionnés dans chaque analyse du dossier de contrôle. Si la taille du lot est définie sur deux et que dix fichiers ou dossiers sont déposés dans le dossier input du dossier de contrôle, seuls deux sont sélectionnés dans chaque analyse. Lors de l’analyse suivante, qui se produira après la durée spécifiée dans l’intervalle de répétition, les deux fichiers suivants seront sélectionnés.
* Pour les modèles de fichiers, les administrateurs peuvent spécifier des expressions régulières avec la prise en charge de modèles génériques pour spécifier des modèles de fichiers. Watched Folder modifie l’expression régulière pour prendre en charge les modèles de caractère joker tels que &amp;ast;.&amp;ast; ou &amp;ast;.pdf. Ces modèles de caractères génériques ne sont pas pris en charge par les expressions régulières.
* Watched Folder analyse le dossier input à la recherche de l’entrée et ne sait pas si le fichier ou le dossier source est complètement copié dans le dossier input avant de commencer le traitement du fichier ou du dossier. Pour vous assurer que le fichier ou le dossier source est entièrement copié dans le dossier input du dossier de contrôle avant que le fichier ou le dossier ne soit sélectionné, procédez comme suit :

   * Utilisez l’attribut Temps d’attente , qui correspond au temps d’attente en millisecondes de Watched Folder de l’heure de dernière modification. Utilisez cette fonction si vous avez des fichiers volumineux à traiter. Par exemple, si le téléchargement d’un fichier prend 10 minutes, indiquez le temps d’attente sous la forme 10&amp;ast;60 &amp;ast;1 000 millisecondes. Cela empêchera Watched Folder de récupérer le fichier s’il n’est pas plus vieux que 10 minutes.
   * Utilisez exclure le modèle de fichier et inclure le modèle de fichier. Par exemple, si le modèle de fichiers d’exclusion est `ex*` et le modèle de fichiers d’inclusion `in*`, Watched Folder sélectionne les fichiers commençant par « in » et non ceux commençant par « ex ». Pour copier des fichiers ou des dossiers volumineux, renommez tout d’abord le fichier ou le dossier de sorte que leur nom commence par « ex ». Une fois le fichier ou le dossier nommé « ex » entièrement copié dans le dossier de contrôle, renommez-le en le faisant débuter par « in&amp;ast; ».

* Utilisez la durée de purge pour nettoyer le dossier result. Watched Folder nettoie tous les fichiers qui sont plus anciens que la durée mentionnée dans la durée de la purge. La durée est exprimée en jours.
* Lors de l’ajout d’un point de fin Watched Folder, après avoir sélectionné le nom de l’opération, le mappage des paramètres d’entrée est renseigné. Pour chaque entrée de l’opération, un champ de mappage des paramètres d’entrée est généré. Voici des exemples de mappages de paramètres d’entrée :

   * Pour une entrée `com.adobe.idp.Document` : si l’opération de service dispose d’une entrée du type `Document`, l’administrateur peut définir le type de mappage sur `Variable`. Watched Folder sélectionnera l’entrée du dossier input du dossier de contrôle en fonction du modèle de fichier spécifié pour le paramètre d’entrée. Si l’administrateur définit `*.pdf` comme paramètre, les fichiers possédant l’extension .pdf sont sélectionnés et convertis en `com.adobe.idp.Document`, puis le service est appelé.
   * Pour une entrée `java.util.Map` : si l’opération de service dispose d’une entrée du type `Map`, l’administrateur peut définir le type de mappage sur `Variable` et saisir une valeur de mappage avec un modèle du type `*.pdf`. Par exemple, un service a besoin d’un mappage de deux objets `com.adobe.idp.Document`, ce qui représente deux fichiers dans le dossier input, du type 1.pdf et 2.pdf. Watched Folder créera alors une mappe avec pour clé le nom du fichier et pour valeur `com.adobe.idp.Document`.
   * Pour une entrée `java.util.List` : si l’opération de service dispose d’une entrée du type List, l’administrateur peut définir le type de mappage sur `Variable` et saisir une valeur de mappage avec un modèle du type `*.pdf`. Lorsque les fichiers PDF seront déposés dans le dossier input, Watched Folder créera une liste des objets `com.adobe.idp.Document` représentant ces fichiers et appellera le service cible.
   * Pour `java.lang.String` : l’administrateur dispose de deux options. Tout d’abord, l’administrateur peut spécifier le type de mappage comme étant `Literal` et saisir une valeur de mappage sous la forme d’une chaîne, telle que `hello.` et Watched Folder appelle le service avec la chaîne `hello`. Deuxième option : l’administrateur peut définir le type de mappage sur `Variable`, puis saisir une valeur de mappage avec un modèle du type `*.txt`. Dans le deuxième cas, les fichiers ayant pour extension .txt seront lus comme un document converti sous forme de chaîne pour appeler le service.
   * Type primitif Java : l’administrateur peut définir le type de mappage sur `Literal` et fournir la valeur. Watched Folder appellera le service avec la valeur spécifiée.

* Watched Folder est destiné à fonctionner avec des documents. Les sorties prises en charge sont `com.adobe.idp.Document`, `org.w3c.Document` et `org.w3c.Node`, de même qu’une liste et un mappage de ces types. Tout autre type entraîne un échec de la sortie dans le dossier failure.
* Si les résultats ne se trouvent pas dans le dossier result, vérifiez le dossier failure pour voir si un échec s’est produit.
* Watched Folder fonctionne mieux s’il est utilisé en mode asynchrone. Dans ce mode, Watched Folder place la demande d’appel dans la file d’attente et rappelle. La file d’attente est ensuite traitée de manière asynchrone. Lorsque l’option Asynchrone n’est pas définie, Watched Folder appelle le service cible de manière synchrone et Process Engine attend que le service soit terminé avec la requête et que les résultats soient générés. Si le service cible prend beaucoup de temps pour traiter la demande, Watched Folder peut générer des erreurs de délai d’expiration.
* La création de dossiers de contrôle pour les opérations d’importation et d’exportation ne permet pas l’abstraction de l’extension de nom de fichier. Lors de l’appel du service Form Data Integration à l’aide de dossiers de contrôle, le type d’extension du nom du fichier de sortie peut ne pas correspondre au format de sortie prévu pour le type d’objet de document. Par exemple, si le fichier d’entrée vers un dossier de contrôle appelant l’opération d’exportation est un formulaire XFA contenant des données, la sortie doit être un fichier de données XDP. Pour obtenir un fichier de sortie avec l’extension de nom de fichier correcte, vous pouvez le spécifier dans le mapping des paramètres de sortie. Dans cet exemple, vous pouvez utiliser %F.xdp pour le mappage des paramètres de sortie.
* Watched Folder peut traiter les fichiers d’entrée avant qu’ils ne soient complètement copiés dans le dossier. Le verrouillage de fichier n’est pas obligatoire sous UNIX, contrairement à Windows. C’est pourquoi, lorsqu’un fichier est copié dans un dossier de contrôle, ce dernier peut le déplacer vers l’environnement intermédiaire sans attendre la fin de la copie du fichier. Ce comportement entraîne le traitement d’une partie seulement du fichier d’entrée. Il existe actuellement deux solutions :

   * Solution 1

      1. Spécifiez un modèle pour l’option Modèles de fichier d’exclusion, tel que temp&amp;ast;.ps.
      1. Copiez les fichiers dont le nom commence par temp (par exemple, temp1.ps) dans le dossier de contrôle.
      1. Une fois le fichier intégralement copié dans le dossier de contrôle, renommez-le pour le faire correspondre au modèle spécifié dans Modèle de fichier d’inclusion. Watched Folder déplace ensuite le fichier terminé vers l’étape.

   * Solution 2

     Si vous connaissez la durée maximale nécessaire pour copier vos fichiers dans un dossier de contrôle, indiquez le temps d’attente en secondes. Watched Folder attend ensuite le temps spécifié avant de déplacer le fichier vers l’environnement intermédiaire.

     Ce n’est pas un problème pour les fichiers sous Windows, car Windows verrouille un fichier lorsqu’un thread est en train d’écrire. Cependant, il s’agit d’un problème pour les dossiers sous Windows. Pour les dossiers, vous devez suivre les étapes de la solution 1.

* Si l’attribut Preserve Folder Name endpoint pour Watched Folder est défini sur un chemin d’accès de répertoire nul, le répertoire d’évaluation n’est pas nettoyé comme il le devrait. Le répertoire contient toujours le fichier traité et le dossier temporaire.

## Recommandations spécifiques au service pour les dossiers de contrôle {#service-specific-recommendations-for-watched-folders}

Pour tous les services, vous devez ajuster la taille du lot et l’intervalle de répétition du dossier de contrôle de sorte que le rythme auquel Watched Folder sélectionne de nouveaux fichiers et dossiers en vue du traitement ne dépasse pas le nombre de tâches pouvant être traitées par le serveur d’AEM forms. Les paramètres réels à utiliser peuvent varier en fonction du nombre de dossiers de contrôle configurés, des services utilisant des dossiers de contrôle et de l’intensité des tâches sur le processeur.

### Recommandations relatives au service Generate PDF {#generate-pdf-service-recommendations}

* Le service Generate PDF peut convertir un seul fichier à la fois pour les types de fichiers suivants : Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® et le PageMaker d’Adobe®. Il s’agit de tâches de longue durée. Par conséquent, assurez-vous que la taille du lot reste basse. Augmentez également l’intervalle de répétition si la grappe contient plus de noeuds.
* Pour les types de fichiers PostScript (PS), Encapsulated PostScript (EPS) et Image, le service Generate PDF peut traiter plusieurs fichiers en parallèle. Vous devez soigneusement régler la taille du pool bean session (qui détermine le nombre de conversions qui seront effectuées en parallèle) en fonction de la capacité de votre serveur et du nombre de noeuds dans la grappe. Augmentez ensuite la taille du lot à un nombre égal à la taille du pool bean session pour les types de fichiers que vous essayez de convertir. La fréquence d’interrogation doit être dictée par le nombre de noeuds de la grappe. Cependant, comme le service Generate PDF traite ce type de tâches assez rapidement, vous pouvez configurer l’intervalle de répétition sur une valeur basse, 5 ou 10, par exemple.
* Même si le service Generate PDF ne peut convertir qu’un seul fichier OpenOffice à la fois, la conversion est assez rapide. La logique ci-dessus pour les conversions PS, EPS et image s’applique également aux conversions OpenOffice.
* Pour permettre une distribution uniforme de la charge dans la grappe, conservez une taille de lot réduite et augmentez l’intervalle de répétition.

### recommandations relatives au service barcoded forms {#barcoded-forms-service-recommendations}

* Pour obtenir de meilleures performances dans le traitement des formulaires à codes-barres (fichiers de petite taille), saisissez `10` pour la taille du lot et `2` pour l’intervalle de répétition.
* Lorsque le nombre de fichiers du dossier input est important, il n’est pas impossible que des erreurs avec des fichiers masqués appelés *thumbs.db* surviennent. Il est dès lors recommandé de définir le modèle de fichier d’inclusion pour les fichiers d’inclusion sur la même valeur que celle indiquée pour la variable d’entrée (par exemple, `*.tiff`). Cela empêche ainsi Watched Folder de traiter les fichiers DB.
* Une taille du lot de `5` et un intervalle de répétition de `2` suffisent normalement car Barcoded Forms traite habituellement un code-barres en 0,5 seconde.
* Watched Folder n’attend pas que le moteur de processus termine la tâche avant de sélectionner de nouveaux fichiers ou dossiers. Il continue à analyser le dossier de contrôle et à appeler le service cible. Ce comportement peut surcharger le moteur, ce qui entraîne des problèmes de ressources et des dépassements de délai. Veillez à utiliser l’intervalle de répétition et la taille du lot pour limiter l’entrée du dossier de contrôle. Vous pouvez augmenter l’intervalle de répétition et réduire la taille du lot s’il existe d’autres dossiers de contrôle ou activer le ralentissement sur le point de terminaison . Pour plus d’informations sur le ralentissement, voir [A propos du ralentissement](configuring-watched-folder-endpoints.md#about-throttling).
* Watched Folder emprunte l’identité de l’utilisateur spécifié dans le nom d’utilisateur et le nom de domaine. Watched Folder appelle le service en tant que cet utilisateur s’il est appelé directement ou si le processus est de courte durée. Pour un processus de longue durée, le processus est appelé avec le contexte système. Les administrateurs peuvent définir des stratégies de système d’exploitation pour Watched Folder afin de déterminer à quel utilisateur autoriser ou refuser l’accès.
* Utilisez les modèles de fichiers pour organiser les dossiers result, failure et preserve. (Voir [A propos des modèles de fichier](configuring-watched-folder-endpoints.md#about-file-patterns).)

* Watched Folder s’appuie sur le planificateur Quartz pour analyser les dossiers de contrôle. Le planificateur Quartz dispose d’un pool de threads pour les analyser. Si l’intervalle de répétition du dossier de contrôle est très faible (&lt; 5 secondes) et que la taille du lot est élevée (> 2), une condition de concurrence peut se produire. Lorsque cette condition se produit, un fichier est sélectionné par deux threads Quartz :

   * L’un des threads réussit à trouver le fichier et à appeler le service cible avec le fichier .
   * Le deuxième thread voit le fichier mais échoue lorsqu’il tente de déterminer si le fichier est valide (fichier en lecture ou en écriture), ce qui entraîne de faux échecs indiquant que le fichier ne peut pas être traité car il est en lecture seule. Cela se produit uniquement avec un intervalle de répétition faible et une taille de lot élevée.
