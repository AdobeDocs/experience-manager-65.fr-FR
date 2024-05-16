---
title: Configuration des points d’entrée des dossiers de contrôle
description: Découvrez comment configurer des points d’entrée de dossiers de contrôle. Si un document est placé dans un dossier de contrôle, une opération de service configurée est appelée et manipule le fichier.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.4/FORMS
exl-id: ec169a01-a113-47eb-8803-bd783ea2c943
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '7192'
ht-degree: 100%

---

# Configuration des points d’entrée des dossiers de contrôle {#configuring-watched-folder-endpoints}

Un administrateur ou une administratrice peut configurer un dossier réseau, appelé *dossier de contrôle*, de sorte que lorsqu’un utilisateur ou une utilisatrice y place un fichier (par exemple un fichier PDF), une opération de service configurée est appelée et manipule le fichier. Après que le service a effectué l’opération spécifiée, il enregistre le fichier modifié dans un dossier de sortie spécifié.

## Configuration du service du dossier de contrôle {#configuring-the-watched-folder-service}

Avant de configurer un point d’entrée de dossier de contrôle, configurez le service du dossier de contrôle. Les paramètres de configuration du service du dossier de contrôle ont deux objectifs :

* Configurer les attributs communs à tous les points d’entrée du dossier de contrôle.
* Fournir des valeurs par défaut à tous les points d’entrée du dossier de contrôle.

Après avoir configuré le service du dossier de contrôle, ajoutez un point d’entrée du dossier de contrôle au service cible. Lors de l’ajout du point d’entrée, définissez des valeurs telles que le nom du service et le nom de l’opération à appeler lorsque des fichiers ou des dossiers sont placés dans le dossier d’entrée du service configuré du dossier de contrôle. Pour plus d’informations sur la configuration du service du dossier de contrôle, consultez [Paramètres du service du dossier de contrôle](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).

## Création d’un dossier de contrôle {#creating-a-watched-folder}

Vous pouvez créer un dossier de contrôle de deux manières :

* Lors de la configuration des paramètres d’un point d’entrée de dossier de contrôle, saisissez le chemin d’accès complet du répertoire parent dans le champ Chemin d’accès et ajoutez-y le nom du dossier de contrôle à créer, comme indiqué dans l’exemple suivant :
  `  C:\MyPDFs\MyWatchedFolder`Comme le dossier MyWatchedFolder n’existe pas encore, AEM Forms tente de le créer à cet emplacement.

* Créez un dossier dans le système de fichiers avant de configurer un point d’entrée de dossier de contrôle puis indiquez son chemin d’accès complet dans le champ Chemin d’accès.

Dans un environnement organisé en clusters, le dossier à utiliser comme dossier de contrôle doit être accessible, modifiable et partagé sur le système de fichiers ou le réseau. Dans ce cas, chaque instance du serveur d’applications dans le cluster doit avoir accès au même dossier partagé.

Sous Windows, si le serveur d’applications s’exécute en tant que service, il doit être démarré avec les droits d’accès au dossier partagé appropriés, de l’une des manières suivantes :

* Configurez le paramètre **Ouvrir une session en tant que du service du serveur d’applications** pour qu’il démarre avec un utilisateur disposant des droits d’accès appropriés sur le dossier de contrôle partagé.
* Sélectionnez Autoriser le service à interagir avec le bureau dans le champ Exécuter en tant que système local. Cette option nécessite que le dossier de contrôle partagé soit accessible et modifiable par tout le monde.

## Chaînage de dossiers de contrôle {#chaining-together-watched-folders}

Les dossiers de contrôle peuvent être assemblés en chaîne de sorte qu’un document de résultats d’un dossier de contrôle corresponde au document d’entrée du dossier de contrôle suivant. Chaque dossier de contrôle peut appeler un service différent. En configurant des dossiers de contrôle de la sorte, plusieurs services peuvent être appelés. Par exemple, un premier dossier de contrôle peut convertir des fichiers PDF au format Adobe PostScript®, et un second dossier de contrôle peut convertir des fichiers PostScript au format PDF/A. Pour ce faire, configurez le dossier *résultats* du dossier de contrôle défini par votre premier point d’entrée, afin qu’il pointe vers le dossier *entrée* du dossier de contrôle défini par votre second point d’entrée.

La sortie de la première conversion serait placée dans le dossier \path\result. Et le dossier d’entrée de la seconde conversion serait \chemin\result et le dossier de sortie de la seconde conversion serait \chemin\result\result (ou le dossier défini dans la zone du dossier de résultats pour la seconde conversion).

## Interaction des utilisateurs et des utilisatrices avec les dossiers de contrôle {#how-users-interact-with-watched-folders}

Avec un point d’entrée de dossier de contrôle, les utilisateurs et les utilisatrices peuvent lancer le processus en copiant ou en faisant glisser des fichiers ou des dossiers depuis le bureau vers un dossier de contrôle. Les fichiers sont traités selon leur ordre d’arrivée.

Avec plusieurs points d’entrée de dossier de contrôle, si la tâche ne requiert qu’un fichier d’entrée, l’utilisateur ou l’utilisatrice peut le copier à la racine du dossier de contrôle.

Si la tâche contient plusieurs fichiers d’entrée, l’utilisateur ou l’utilisatrice doit créer, hors de l’arborescence du dossier de contrôle, un dossier contenant tous les fichiers requis. Ce nouveau dossier doit inclure les fichiers d’entrée (et éventuellement un fichier DDX s’il est requis par le processus). Une fois le dossier de la tâche créé, l’utilisateur ou l’utilisatrice le copie dans le dossier d’entrée du dossier de contrôle.

>[!NOTE]
>
>Vérifiez que le serveur d’applications a révoqué l’accès aux fichiers dans le dossier de contrôle. Si AEM Forms ne peut pas supprimer les fichiers du dossier d’entrée après leur analyse, le processus associé est alors appelé indéfiniment.

## Sorties du dossier de contrôle {#watched-folder-output}

Lorsque l’entrée est un dossier et que la sortie compte plusieurs fichiers, AEM Forms crée un dossier de sortie portant le même nom que le dossier d’entrée, et copie les fichiers de sortie dans ce dossier. Lorsque la sortie est un mappage de documents contenant une paire clé/valeur, comme la sortie d’un processus de sortie, c’est la clé qui est utilisée comme nom du fichier de sortie.

Les noms des fichiers de sortie générés par un processus de point d’entrée ne peuvent pas comporter de caractères autres que des lettres, des chiffres et un point (.) avant l’extension du fichier. AEM forms remplace les autres caractères par leurs valeurs hexadécimales.

Les applications clientes sélectionnent les documents de résultats dans le dossier des résultats du dossier de contrôle. Les erreurs de traitement sont consignées dans le dossier des échecs du dossier de contrôle.

## Fonctionnement du dossier de contrôle {#how-watched-folder-works}

Le module de dossier de contrôle contient les services suivants :

* Service du dossier de contrôle
* provider.file_scan_service
* provider.file_write_results_service

Outre les services répertoriés ci-dessus, le dossier de contrôle dépend également d’autres services, notamment le service Planificateur pour la planification des traitements et le service de gestion des traitements pour la prise en charge de l’appel asynchrone des services cibles.

### Traitement d’une demande d’appel par le dossier de contrôle {#how-watched-folder-processes-an-invocation-request}

Le service de dossier de contrôle gère la création, la mise à jour et la suppression des points d’entrée. Une fois les points d’entrée créés par l’administrateur ou l’administratrice, ils sont programmés pour être déclenchés par le service de planification en fonction de l’intervalle de répétition spécifié ou de l’expression cron.

Ce diagramme illustre comment le dossier de contrôle traite une demande d’appel.

![en_watchedfolder](assets/en_watchedfolder.png)

Le processus d’appel d’un service à l’aide de dossiers de contrôle est le suivant :

1. Une application cliente place des fichiers ou des dossiers dans le dossier d’entrée du dossier de contrôle.
1. Lorsque l’intervalle d’analyse de traitement se produit, le service de planification appelle provider.file_scan_service pour traiter les fichiers ou les dossiers dans le dossier d’entrée.
1. provider.file_scan_service effectue les tâches suivantes :


   * Analyse le dossier d’entrée à la recherche de fichiers ou de dossiers correspondant au modèle de fichier d’inclusion et exclut les fichiers ou les dossiers pour le modèle de fichier d’exclusion spécifié. Les fichiers ou dossiers les plus anciens sont sélectionnés en premier. Les fichiers et les dossiers antérieurs à la durée d’attente sont également sélectionnés. Au cours d’une analyse, le nombre de fichiers ou de dossiers traités dépend de la taille du lot. Pour plus d’informations sur les modèles de fichiers, consultez [À propos des modèles de fichiers](configuring-watched-folder-endpoints.md#about-file-patterns). Pour plus d’informations sur la définition de la taille du lot, voir [Paramètres du service de dossier de contrôle](/help/forms/using/admin-help/configure-service-settings.md#watched-folder-service-settings).
   * Récupère les fichiers ou les dossiers à traiter. Si les fichiers ou les dossiers ne sont pas entièrement téléchargés, ils sont sélectionnés lors de l’analyse suivante. Pour s’assurer que les dossiers sont entièrement téléchargés, les administrateurs et administratrices doivent créer un dossier avec un nom en utilisant le modèle de fichier d’exclusion. Une fois que le dossier contient tous les fichiers, il doit être renommé selon le modèle spécifié dans le modèle de fichier d’inclusion. Cette étape permet de s’assurer que le dossier contient tous les fichiers nécessaires pour appeler le service. Pour plus d’informations sur le téléchargement complet des dossiers, voir [Conseils et astuces pour les dossiers de contrôle](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).
   * Déplace les fichiers ou les dossiers vers le dossier d’évaluation après les avoir sélectionnés pour traitement.
   * Convertit les fichiers ou les dossiers du dossier d’évaluation en entrée appropriée en fonction des mappages des paramètres d’entrée du point d’entrée. Pour obtenir des exemples de mappages des paramètres d’entrée, voir [Conseils et astuces pour les dossiers de contrôle](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).


1. Le service cible configuré pour le point d’entrée est appelé de manière synchrone ou asynchrone. Le service cible est appelé à l’aide du nom d’utilisateur ou d’utilisatrice et du mot de passe configurés pour le point d’entrée.

   * Un appel synchrone appelle directement le service cible et traite immédiatement la réponse.
   * Pour un appel asynchrone, le service cible est appelé par le biais du service de gestion des traitements, qui place la requête dans une file d’attente. Le service de gestion des traitements, à son tour, appelle provider.file_write_results_service pour traiter les résultats.

1. provider.file_write_results_service gère la réponse ou l’échec de l’appel du service cible. En cas de réussite, la sortie est enregistrée dans le dossier de résultat en fonction de la configuration du point d’entrée. provider.file_write_results_service conserve également la source si le point d’entrée est configuré pour conserver les résultats une fois l’opération terminée.

   Lorsque l’appel du service cible entraîne un échec, provider.file_write_results_service consigne la raison de l’échec dans un fichier failure.log et place ce fichier dans le dossier d’échec. Le dossier d’échec est créé en fonction des paramètres de configuration spécifiés pour le point d’entrée. Lorsque l’administrateur ou l’administratrice définit l’option Conserver en cas d’échec pour la configuration du point d’entrée, provider.file_write_results_service copie également les fichiers sources dans le dossier d’échec. Pour plus d’informations sur la récupération des fichiers dans le dossier d’échec, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Paramètres des points d’entrée d’un dossier de contrôle {#watched-folder-endpoint-settings}

Utilisez les paramètres suivants pour configurer un point d’entrée de dossier de contrôle.

**Nom :**(obligatoire) identifie le point d’entrée. N’incluez pas de caractère « &lt; », car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL comme nom du point d’entrée, assurez-vous qu’elle est conforme aux règles de syntaxe spécifiées dans la RFC1738.

**Description :** fournit une description du point d’entrée. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**Chemin d’accès :** (obligatoire) indique l’emplacement du dossier de contrôle. Dans un environnement organisé en grappe, ce paramètre doit pointer vers un dossier réseau partagé accessible à tous les ordinateurs de la grappe.

**Asynchrone :** identifie le type d’appel comme étant asynchrone ou synchrone. La valeur par défaut est asynchrone. Le mode asynchrone est recommandé pour les processus de longue durée, tandis que le mode synchrone est recommandé pour les processus transitoires ou de courte durée.

**Expression Cron :** saisissez une expression cron si le dossier de contrôle doit être programmé en utilisant une expression de ce type. Si ce paramètre est configuré, l’intervalle de répétition est ignoré.

**Intervalle de répétition :** intervalle (en secondes) entre les analyses du dossier de contrôle d’entrée. À moins que le paramètre Ralentissement ne soit activé, le paramètre Intervalle de répétition doit être supérieur à la durée d’exécution d’un traitement moyen, faute de quoi le système risque d’être surchargé. La valeur par défaut est 5. Pour plus d’informations, voir la description du paramètre Taille du lot.

**Nombre de répétitions :** nombre d’analyses du dossier ou du répertoire par le dossier de contrôle. La valeur -1 indique une analyse sans limite. La valeur par défaut est -1.

**Ralentissement :** lorsque cette option est sélectionnée, elle permet de limiter le nombre de tâches du dossier de contrôle quʼAEM Forms peut traiter à un moment donné. La valeur Taille du lot détermine le nombre maximal de tâches. Voir A propos du ralentissement .

**Nom d’utilisateur :** (obligatoire) nom d’utilisateur utilisé lors de l’appel d’un service cible à partir du dossier de contrôle. La valeur par défaut est SuperAdmin.

**Nom de domaine :** (obligatoire) domaine de l’utilisateur ou de l’utilisatrice. La valeur par défaut est DefaultDom.

**Taille du lot :** le nombre de fichiers ou de dossiers à sélectionner par analyse. Ce paramètre permet d’éviter une surcharge du système, car l’analyse simultanée d’un trop grand nombre de fichiers peut provoquer une panne. La valeur par défaut est 2.

Les paramètres Intervalle de répétition et Taille du lot permettent de déterminer le nombre de fichiers sélectionnés par le service Dossir de contrôle pour chaque analyse. Le service Dossier de contrôle utilise un pool de threads Quartz pour analyser le dossier input. Le pool de threads est partagé avec d’autres services. Si l’intervalle d’analyse est court, les threads analysent fréquemment le dossier d’entrée. Si des fichiers sont déposés régulièrement dans le dossier de contrôle, il est préférable que l’intervalle d’analyse soit court. Si les fichiers sont rarement déposés, choisissez un intervalle d’analyse plus long afin que les autres services puissent utiliser les threads.

Si un volume important de fichiers est déposé, définissez une grande taille de lot. Par exemple, si le service appelé par le point d’entrée du dossier de contrôle peut traiter 700 fichiers par minute et que les utilisateurs et les utilisatrices déposent des fichiers dans le dossier Entrée à la même fréquence, la définition de la Taille du lot sur 350 et de l’Intervalle de répétition sur 30 secondes permet de maintenir les performances du dossier de contrôle sans avoir à subir les conséquences d’une analyse trop fréquente du dossier de contrôle.

Lorsque des fichiers sont déposés dans le dossier de contrôle, ce dernier les répertorie dans le dossier Entrée, ce qui réduit parfois les performances si l’analyse s’effectue toutes les secondes. L’allongement de l’intervalle d’analyse permet d’améliorer les performances. Si le volume des fichiers déposés est réduit, ajustez la Taille du lot et l’Intervalle de répétition en conséquence. Par exemple, si 10 fichiers sont déposés toutes les secondes, essayez de définir l’Intervalle de répétition sur 1 seconde et la Taille du lot sur 10.

**Durée d’attente :** durée d’attente (en millisecondes) entre la création d’un dossier ou d’un fichier et son analyse. Par exemple, si la durée d’attente est de 3 600 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce dernier sera sélectionné à l’issue d’un laps de temps de 59 minutes ou plus. La valeur par défaut est 0.

Ce paramètre assure la copie intégrale d’un fichier ou d’un dossier dans le dossier d’entrée. Par exemple, si vous devez traiter un fichier volumineux dont le téléchargement dure dix minutes, définissez une durée d’attente de 10&amp;ast;60 &amp;ast;1000 millisecondes. ce qui évite que le dossier de contrôle analyse le fichier tant que ce dernier a une existence inférieure à dix minutes.

**Exclure le modèle de fichier :** liste délimitée par des points-virgules **;** des modèles utilisés par un dossier de contrôle pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Les fichiers ou les dossiers pourvus de ce modèle ne sont pas analysés pour traitement.

Ce paramètre est utile lorsque l’entrée est un dossier contenant plusieurs fichiers. Vous pouvez copier le contenu du dossier dans un dossier dont le nom sera choisi par le dossier de contrôle. Ceci empêche le dossier de contrôle de choisir un dossier à traiter avant qu’il ne soit complètement copié dans le dossier d’entrée.

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


**Dossier result :** dossier dans lequel les résultats enregistrés sont stockés. Si les résultats ne s’affichent pas dans ce dossier, vérifiez le dossier des échecs. Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier des échecs. Il peut s’agir d’un chemin d’accès relatif ou absolu avec les modèles de fichiers suivants :

* %F = préfixe du nom du fichier
* %E = extension du nom du fichier
* %Y = année (complète)
* %y = année (deux derniers chiffres)
* %M = mois
* %D = jour du mois
* %d = jour de l’année
* %H = heure (horloge 24 heures)
* %h = heure (horloge 12 heures)
* %m = minute
* %s = seconde
* %l = milliseconde
* %R = nombre aléatoire (entre 0 et 9)
* %P = ID de processus ou de tâche

Par exemple, si nous sommes le 17 juillet 2009 à 20 h et que vous définissez `C:/Test/WF0/failure/%Y/%M/%D/%H/`, le dossier de résultat est alors `C:/Test/WF0/failure/2009/07/17/20`.

Si le chemin d’accès n’est pas absolu, mais relatif, le dossier est créé dans le dossier de contrôle. La valeur par défaut est result/%Y/%M/%D/, qui correspond au dossier result dans le dossier de contrôle. Pour plus d’informations sur les modèles de fichiers, voir [À propos des modèles de fichier](configuring-watched-folder-endpoints.md#about-file-patterns).

>[!NOTE]
>
>Plus les dossiers de résultats sont petits, plus les performances du service Dossier de contrôle augmentent. Par exemple, si la charge estimée pour le dossier de contrôle est de 1 000 fichiers par heure, utilisez un modèle de type `result/%Y%M%D%H`, afin qu’un nouveau sous-dossier soit créé toutes les heures. Si la charge est moindre (par exemple, 1 000 fichiers par jour), vous pouvez utiliser un modèle de type `result/%Y%M%D`.

**Dossier preserve :** dossier dans lequel les fichiers sont stockés après avoir été analysés et sélectionnés. Le chemin d’accès de répertoire peut être absolu, relatif ou null. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier result. La valeur par défaut est preserve/%Y/%M/%D/.

**Dossier failure :** dossier dans lequel les fichiers en échec sont enregistrés. Cet emplacement dépend toujours du dossier de contrôle. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier Résultat.

Les fichiers en lecture seule ne sont pas traités et ils sont enregistrés dans le dossier des échecs.

La valeur par défaut est failure/%Y/%M/%D/.

**Conserver en cas d’échec :** conservation des fichiers d’entrée en cas d’échec de l’exécution de l’opération dans un service. La valeur par défaut est true.

**Remplacer les noms de fichier en double :** lorsque cet attribut est défini sur « true », les fichiers du dossier obtenu et du dossier conservé sont remplacés. Lorsqu’il est défini sur False, les fichiers et les dossiers avec un suffixe d’index numérique sont utilisés pour le nom. La valeur par défaut est False.

**Durée de la purge :** (obligatoire) les fichiers et les sous-dossiers du dossier result sont vidés lorsqu’ils sont plus anciens que cette valeur. Cette valeur est mesurée en jours. Grâce à ce paramètre, le dossier obtenu n’est jamais plein.

La valeur -1 jour indique de ne jamais supprimer le dossier de résultats. La valeur par défaut est -1.

**Nom de l’opération :** (obligatoire) liste des opérations pouvant être attribuées au point d’entrée Watched Folder.

**Mappages des paramètres d’entrée :** permet de configurer l’entrée requise pour traiter le service et l’opération. Les paramètres disponibles dépendent du service qui utilise le point d’entrée du dossier de contrôle. Voici les deux types d’entrées :

**Littéral :** le dossier de contrôle utilise la valeur saisie dans le champ telle qu’elle est affichée. Tous les types Java de base sont pris en charge. Par exemple, si une interface API utilise une entrée de type chaîne, long, nombre entier ou valeur booléenne, cette entrée est convertie en type approprié, puis le service est appelé.

**Variable :** la valeur saisie est un modèle de fichier que le dossier de contrôle utilise pour sélectionner l’entrée. Par exemple, dans le cas d’un service de mot de passe chiffré où le document d’entrée doit être un fichier PDF, l’utilisateur ou l’utilisatrice peut utiliser &amp;ast;.pdf comme modèle de fichier. Le dossier de contrôle récupère tous les fichiers du dossier de contrôle correspondant à ce modèle et appelle le service pour chaque fichier. Lorsqu’une variable est utilisée, tous les fichiers d’entrée sont convertis en documents. Seules les API qui utilisent le type d’entrée Document sont prises en charge.

**Mappages des paramètres de sortie :** permet de configurer les sorties du service et de l’opération. Les paramètres disponibles dépendent du service qui utilise le point d’entrée du dossier de contrôle.

Les sorties du dossier de contrôle peuvent être un document unique, une liste de documents ou une carte de documents. Ces documents de sortie sont ensuite enregistrés dans le dossier de résultat, à l’aide du modèle spécifié dans le mappage des paramètres de sortie.

>[!NOTE]
>
>La définition de noms qui produisent des noms de fichier de sortie uniques améliore les performances. Imaginez, par exemple, le cas où un service renvoie un document de sortie que le mappage des paramètres de sortie associe à `%F.%E` (le nom et l’extension du fichier d’entrée). Dans ce cas, si des utilisateurs déposent chaque minute des fichiers dont le nom est identique, que le dossier result est défini sur `result/%Y/%M/%D` et que le paramètre Remplacer les noms de fichier en double est inactif, Watched Folder tente de résoudre les noms de fichiers en double. Le processus impliqué dans la résolution des noms de fichiers en double peut affecter les performances. Si vous vous trouvez dans cette situation, définissez le mappage des paramètres de sortie sur `%F_%h_%m_%s_%l` pour ajouter les heures, les minutes, les secondes et les millisecondes au nom du fichier, ou assurez-vous que les fichiers déposés possèdent des noms uniques afin d’améliorer les performances.

## À propos des modèles de fichier {#about-file-patterns}

Les administrateurs peuvent indiquer le type du fichier servant à appeler un service. Il est possible d’établir plusieurs modèles de fichier pour chaque dossier de contrôle. Un modèle de fichier peut être du type suivant :

* Fichiers dotés d’extensions de nom de fichier spécifiques. Par exemple : &amp;ast;.dat, &amp;ast;.xml et &amp;ast;.pdf
* Fichiers portant des noms spécifiques. Par exemple : data.&amp;ast;
* Fichiers contenant des expressions composites dans leur nom et leur extension, comme dans les exemples suivants :

   * Données[0-9][0-9][0-9].[dD][aA]&#39;port&#39;
   * &amp;ast;.[dD][Aa]&#39;port&#39;
   * &amp;ast;.[Xx][Mm][Ll]

L’administrateur ou l’administratrice peut définir le modèle de fichier du dossier de sortie dans lequel enregistrer les résultats. Concernant les dossiers de sortie (résultats, conservation et échecs), il ou elle peut indiquer l’un des modèles de fichier suivants :

* %Y = année (complète)
* %y = année (deux derniers chiffres)
* %M = mois
* %D = jour du mois
* %d = jour de l’année
* %h = heure
* %m = minute
* %s = seconde
* %R = nombre aléatoire entre 0 et 9
* %J = nom de la tâche

Par exemple, le chemin d’accès au dossier de résultats peut être `C:\Adobe\Adobe_Experience_Manager_forms\BarcodedForms\%y\%m\%d`.

Les mappages des paramètres de sortie peuvent également spécifier des modèles supplémentaires, tels que :

* %F = nom du fichier source
* %E = extension du nom du fichier source

Si le modèle de mappage des paramètres de sortie se termine par « File.separator » (qui correspond au séparateur de chemin), un dossier est créé dans lequel le contenu est copié. Si le modèle ne se termine pas par « File.separator », le contenu (fichier ou dossier des résultats) est créé et utilise ce nom. Pour plus d’informations sur les mappages des paramètres de sortie, voir [Conseils et astuces pour les dossiers de contrôle](configuring-watched-folder-endpoints.md#tips-and-tricks-for-watched-folders).

## À propos de la limitation {#about-throttling}

Lorsque l’option de limitation est activée pour un point d’entrée de dossier de contrôle, elle limite le nombre de tâches de dossier de contrôle pouvant être traitées à un moment donné. La valeur Taille du lot détermine le nombre maximal de tâches, le tout pouvant être configuré dans le point d’entrée du dossier de contrôle. Les documents entrants dans le répertoire d’entrée du dossier de contrôle ne seront pas interrogés lorsque la limite de limitation aura été atteinte. Les documents resteront également dans le répertoire d’entrée jusqu’à ce que les autres tâches du dossier de contrôle soient terminées et qu’une autre tentative d’interrogation soit effectuée. En cas de traitement synchrone, toutes les tâches traitées dans une interrogation tiendront compte de la limite de limitation, même si les tâches sont traitées les unes après les autres, dans un seul thread.

>[!NOTE]
>
>Aucune mise à l’échelle du ralentissement n’est effectuée dans un cluster. Lorsque l’option de ralentissement est activée, le cluster dans son ensemble ne traite pas plus de tâches que le nombre indiqué dans l’attribut Taille du lot. Cette limite est fixée par le cluster et n’est pas spécifique à chacun de ses nœuds. Par exemple, si l’attribut Taille du lot a pour valeur 2, la limite du ralentissement peut être atteinte avec le traitement de deux tâches sur un seul nœud et aucun autre nœud n’interrogera alors le répertoire des entrées tant que l’une des tâches ne sera pas terminée.

### Fonctionnement du ralentissement {#how-throttling-works}

Watched Folder analyse le dossier input à chaque intervalle de répétition, récupère le nombre de fichiers spécifié dans la taille du lot et appelle le service cible pour chacun de ces fichiers. Par exemple, si la taille du lot est de quatre, à chaque analyse, le dossier de contrôle récupérera quatre fichiers, créera quatre requêtes d’appel et appellera le service cible. Avant que ces requêtes ne soient terminées, si Watched Folder est appelé, il démarrera à nouveau quatre tâches, indépendamment du fait que les quatre tâches précédentes sont ou non terminées.

L’option de ralentissement empêche le dossier de contrôle d’appeler de nouvelles tâches avant que les tâches précédentes ne soient terminées. Le dossier de contrôle détectera les tâches en cours et traitera les nouvelles tâches en fonction de la taille du lot, moins les tâches en cours. Par exemple, dans le second appel, si le nombre de tâches terminées est de trois seulement et qu’une tâche est toujours en cours, le dossier de contrôle appelle uniquement trois autres tâches.

* Le dossier de contrôle se base sur le nombre de fichiers présents dans le dossier stage pour connaître le nombre de tâches en cours. Si les fichiers restent dans le dossier stage sans être traités, Watched Folder n’appelle plus aucune tâche. Par exemple, si la taille du lot est de quatre et que trois tâches sont bloquées, Watched Folder n’appellera qu’une seule tâche lors des appels suivants. Il existe plusieurs scénarios qui peuvent empêcher le traitement des fichiers dans le dossier stage. Si les tâches sont bloquées, l’administrateur peut mettre un terme au traitement dans la page d’administration du processus des formulaires et Watched Folder sortira alors les fichiers du dossier d’étape.
* Si le serveur Forms Server tombe en panne avant que Watched Folder puisse appeler les tâches, l’administrateur ou l’administratrice peut sortir les fichiers du dossier stage. Pour plus d’informations, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).
* Si le serveur Forms Server fonctionne mais que Watched Folder ne s’exécute pas lorsque le service Job Manager rappelle, ce qui se produit lorsque les services ne démarrent pas dans l’ordre, l’administrateur ou l’administratrice peut sortir les fichiers du dossier stage. Pour plus d’informations, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Performances et évolutivité {#performance-and-scalability}

Watched Folder peut traiter 100 dossiers au total sur un seul nœud. Les performances de Watched Folder dépendent des performances du serveur Forms Server. Pour les appels asynchrones, les performances dépendent davantage de la charge du système et des tâches qui se trouvent dans la file d’attente de Job Manager.

Vous pouvez améliorer les performances du dossier de contrôle en ajoutant des nœuds au cluster. Les tâches de Watched Folder sont distribuées sur les nœuds du cluster en vertu du planificateur Quartz et, en cas de requêtes asynchrones, par le service Job Manager. Toutes les tâches sont conservées dans la base de données.

Le dossier de contrôle dépend du service Scheduler pour la planification, la déplanification et la replanification des tâches. D’autres services, tels que le service Event Management, le service User Manager et le service Email Provider, sont disponibles et partagent le pool de threads du service Scheduler. Cela peut avoir une incidence sur les performances de Watched Folder. Un réglage du pool de threads du service Scheduler sera nécessaire lorsque tous les services commenceront à l’utiliser.

## Dossiers de contrôle dans un cluster {#watched-folders-in-a-cluster}

Dans un cluster, le dossier de contrôle dépend du planificateur Quartz et du service Job Manager pour l’équilibrage de charge et le basculement. Pour plus d’informations sur le comportement du cluster Quartz, voir la [documentation Quartz](https://www.quartz-scheduler.org/documentation).

Watched Folder effectue les trois tâches principales suivantes à chaque interrogation :

* Analyser le dossier
* Appeler le service cible
* Gérer les résultats

Le comportement de l’équilibrage de la charge et du basculement varie en fonction de la configuration du dossier de contrôle (en mode synchrone ou asynchrone).

### Dossier de contrôle synchrone dans un cluster {#synchronous-watched-folder-in-a-cluster}

Pour les appels synchrones, l’équilibreur de charge Quartz décide du nœud recevant l’événement d’interrogation. Le nœud concerné exécutera l’ensemble des tâches suivantes : analyse du dossier, appel du service cible et gestion des résultats.

![en_synchwatchedfoldercluster](assets/en_synchwatchedfoldercluster.png)

Pour les appels synchrones, lorsqu’un nœud échoue, le planificateur Quartz envoie de nouveaux événements d’interrogation aux autres nœuds. Les appels lancés sur le nœud en échec sont perdus. Pour plus d’informations sur la récupération de fichiers associés à la tâche ayant échoué, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


### Dossier de contrôle asynchrone dans un cluster {#asynchronous-watched-folder-in-a-cluster}

Pour les appels asynchrones, l’équilibreur de charge Quartz décide du nœud recevant l’événement d’interrogation. Le nœud qui reçoit l’événement d’interrogation analyse le dossier input et appelle le service cible en plaçant la demande dans la file d’attente du service Job Manager. L’équilibreur de charge du service Job Manager est quant à lui chargé de décider quel nœud traite la demande d’appel. Il est possible que même si le nœud A a créé la demande d’appel, le nœud B termine le traitement de la demande. De même, il est possible que le nœud qui lance la demande d’appel termine le traitement de la demande.

![en_asynchwatchedfoldercluster](assets/en_asynchwatchedfoldercluster.png)

Pour les appels asynchrones, lorsqu’un nœud échoue, le planificateur Quartz envoie de nouveaux événements d’interrogation aux autres nœuds. Les demandes d’appel créées sur le nœud en échec seront placées dans la file d’attente du service Job Manager, puis envoyées vers d’autres nœuds en vue de leur traitement. Les fichiers pour lesquels des demandes d’appel ne sont pas créées resteront dans le dossier stage. Pour plus d’informations sur la récupération de fichiers associés à la tâche ayant échoué, voir [Points d’échec et récupération](configuring-watched-folder-endpoints.md#failure-points-and-recovery).


## Points d’échec et récupération {#failure-points-and-recovery}

À chaque événement d’interrogation, le dossier de contrôle verrouille le dossier d’entrée, déplace dans le dossier stage les fichiers correspondant au modèle de fichiers inclus, puis déverrouille le dossier d’entrée. Le verrouillage est nécessaire afin que deux threads ne sélectionnent pas le même ensemble de fichiers et ne les traitent pas deux fois. La probabilité d’un traitement en double augmente lorsque l’intervalle de répétition est court et que la taille du lot est importante. Une fois les fichiers déplacés dans le dossier stage, le dossier input est déverrouillé de sorte que d’autres threads puissent analyser le dossier. Cette étape offre un débit élevé du fait que d’autres threads peuvent effectuer une analyse pendant que l’un d’entre eux traite les fichiers.

Une fois les fichiers déplacés dans le dossier stage, les demandes d’appel sont créées pour chaque fichier et le service cible est appelé. Cependant, il arrive parfois que le dossier de contrôle ne puisse pas récupérer les fichiers dans le dossier stage :

* Si une panne du serveur survient avant que le dossier de contrôle n’ait eu le temps de créer la demande d’appel, les fichiers situés dans le dossier stage restent dans ce dossier et ne sont pas récupérés.
* Si le dossier de contrôle a réussi à créer la demande d’appel pour chacun des fichiers du dossier stage et qu’une panne du serveur survient, deux comportements sont à noter, en fonction du type d’appel :

**Synchrone** : si Watched Folder est configuré pour appeler le service de manière synchrone, tous les fichiers du dossier stage restent dans ce dossier et ne subissent aucun traitement.

**Asynchrone** : dans ce cas, Watched Folder s’appuie sur le service Job Manager. Si le service Job Manager rappelle le dossier de contrôle, les fichiers du dossier stage sont déplacés vers le dossier de conservation ou d’échecs, en fonction des résultats de l’appel. Si le service Job Manager ne rappelle pas le dossier de contrôle, les fichiers restent dans le dossier stage et ne subissent aucun traitement. Cette situation survient lorsque le dossier de contrôle n’est pas exécuté alors que Job Manager rappelle.

### Récupération des fichiers source non traités dans le dossier stage {#recovering-unprocessed-source-files-in-the-stage-folder}

Lorsque le dossier de contrôle ne peut pas traiter les fichiers source dans le dossier stage, vous avez la possibilité de récupérer les fichiers n’ayant fait l’objet d’aucun traitement.

1. Redémarrez le serveur d’applications ou le nœud.
1. (Facultatif) Faites en sorte que Watched Folder ne traite plus aucun nouveau fichier d’entrée. Si vous ignorez cette étape, il vous sera plus difficile de déterminer les fichiers non traités dans le dossier stage. Pour empêcher que le dossier de contrôle ne traite de nouveaux fichiers d’entrée, procédez comme suit :

   * Dans Applications et services, modifiez le paramètre Inclure le modèle de fichier pour le point d’entrée du dossier de contrôle et donnez-lui une valeur qui ne correspond à aucun nouveau fichier d’entrée (par exemple, saisissez `NOMATCH`).
   * Mettez un terme au processus de création de nouveaux fichiers d’entrée.

   Attendez qu’AEM Forms récupère et traite tous les fichiers. La majorité des fichiers devra être récupérée et tous les nouveaux fichiers d’entrée correctement traités. Le temps nécessaire au dossier de contrôle pour récupérer et traiter les fichiers dépendra de la durée de l’opération pour l’appel, ainsi que du nombre de fichiers à récupérer.

1. Déterminez les fichiers ne pouvant pas être traités. Si vous avez suffisamment attendu, que vous avez terminé l’étape précédente et qu’il reste encore des fichiers non traités dans le dossier stage, passez à l’étape suivante.

   >[!NOTE]
   >
   >Vous pouvez consulter la date et l’horodatage des fichiers dans le répertoire stage. En fonction du nombre de fichiers et du temps normal de traitement, vous pouvez déterminer les fichiers considérés comme étant bloqués.

1. Copiez les fichiers non traités du répertoire stage dans le répertoire des entrées.
1. Si vous avez empêché le dossier de contrôle de traiter de nouveaux fichiers d’entrée à l’étape 2, redonnez au paramètre Inclure le modèle de fichier son ancienne valeur ou réactivez le processus préalablement désactivé.

## Questions de sécurité pour les dossiers de contrôle {#security-considerations-for-watched-folders}

Chaque dossier de contrôle est configuré avec un nom d’utilisateur et un mot de passe. Ces informations d’identification sont utilisées lors de l’appel des services. Watched Folder repose sur le fait que le dossier partagé est protégé par le système de fichiers de sécurité sous-jacent afin que seul le ou la propriétaire du dossier de contrôle puisse accéder au dossier partagé.

## Conseils et astuces concernant les dossiers de contrôle {#tips-and-tricks-for-watched-folders}

Voici quelques trucs et astuces pour la configuration du point d’entrée de Watched Folder :

* Si vous disposez d’un dossier de contrôle sous Windows qui traite des fichiers image, spécifiez les valeurs pour l’option Inclure le modèle de fichier ou Exclure le modèle de fichier afin d’empêcher le fichier Thumbs.db généré automatiquement par Windows d’être interrogé par le dossier de contrôle.
* Si une expression cron est spécifiée, l’intervalle de répétition est ignoré. L’utilisation de l’expression cron est basée sur le système de planification des tâches open source Quartz, version 1.4.0.
* La taille du lot correspond au nombre de fichiers ou de dossiers qui seront récupérés lors de chaque analyse du dossier de contrôle. Si la taille du lot est définie sur deux et que dix fichiers ou dossiers sont déposés dans le dossier input du dossier de contrôle, seuls deux seront récupérés à chaque analyse. Lors de la prochaine analyse, qui aura lieu après le temps spécifié dans l’intervalle de répétition, les deux fichiers suivants seront récupérés.
* Pour les modèles de fichiers, les administrateurs et administratrices peuvent spécifier des expressions régulières avec une prise en charge supplémentaire des modèles de caractères joker pour spécifier des modèles de fichiers. Watched Folder modifie l’expression régulière pour prendre en charge les modèles de caractère joker tels que &amp;ast;.&amp;ast; ou &amp;ast;.pdf. Ces modèles de caractères joker ne sont pas pris en charge par les expressions régulières.
* Watched Folder analyse le dossier input à la recherche de l’entrée et ne sait pas si le fichier ou le dossier source est complètement copié dans le dossier input avant de commencer à traiter le fichier ou le dossier. Pour vous assurer que le fichier ou le dossier source est entièrement copié dans le dossier input du dossier de contrôle avant que le fichier ou le dossier ne soit récupéré, procédez comme suit :

   * Utilisez le temps d’attente, qui correspond au temps en millisecondes pendant lequel Watched Folder attend à partir de la dernière heure de modification. Utilisez cette fonctionnalité si vous avez des fichiers volumineux à traiter. Par exemple, si le téléchargement d’un fichier prend 10 minutes, indiquez le temps d’attente sous la forme 10&amp;ast;60 &amp;ast;1 000 millisecondes. Cela empêchera Watched Folder de récupérer le fichier s’il ne date pas d’au moins 10 minutes.
   * Utilisez le modèle de fichier d’exclusion et le modèle de fichier d’inclusion. Par exemple, si le modèle de fichiers d’exclusion est `ex*` et le modèle de fichiers d’inclusion `in*`, Watched Folder sélectionne les fichiers commençant par « in » et non ceux commençant par « ex ». Pour copier des fichiers ou des dossiers volumineux, renommez tout d’abord le fichier ou le dossier de sorte que leur nom commence par « ex ». Une fois le fichier ou le dossier nommé « ex » entièrement copié dans le dossier de contrôle, renommez-le en le faisant débuter par « in&amp;ast; ».

* Utilisez la durée de purge pour garder le dossier result propre. Watched Folder nettoie tous les fichiers antérieurs à la durée mentionnée dans la durée de purge. La durée est exprimée en jours.
* Lors de l’ajout d’un point d’entrée de Watched Folder, lorsque le nom de l’opération a été sélectionné, le mappage des paramètres d’entrée est renseigné. Pour chaque entrée de l’opération, un champ de mappage de paramètres d’entrée est généré. Voici des exemples de mappages de paramètres d’entrée :

   * Pour une entrée `com.adobe.idp.Document` : si l’opération de service dispose d’une entrée du type `Document`, l’administrateur peut définir le type de mappage sur `Variable`. Le dossier de contrôle va prélever l’entrée à partir du dossier d’entrée du dossier de contrôle sur la base du modèle de fichier spécifié pour le paramètre d’entrée. Si l’administrateur définit `*.pdf` comme paramètre, les fichiers possédant l’extension .pdf sont sélectionnés et convertis en `com.adobe.idp.Document`, puis le service est appelé.
   * Pour une entrée `java.util.Map` : si l’opération de service dispose d’une entrée du type `Map`, l’administrateur peut définir le type de mappage sur `Variable` et saisir une valeur de mappage avec un modèle du type `*.pdf`. Par exemple, un service a besoin d’un mappage de deux objets `com.adobe.idp.Document`, ce qui représente deux fichiers dans le dossier input, du type 1.pdf et 2.pdf. Watched Folder créera alors une mappe avec pour clé le nom du fichier et pour valeur `com.adobe.idp.Document`.
   * Pour une entrée `java.util.List` : si l’opération de service dispose d’une entrée du type List, l’administrateur peut définir le type de mappage sur `Variable` et saisir une valeur de mappage avec un modèle du type `*.pdf`. Lorsque les fichiers PDF seront déposés dans le dossier input, Watched Folder créera une liste des objets `com.adobe.idp.Document` représentant ces fichiers et appellera le service cible.
   * Pour `java.lang.String` : l’administrateur dispose de deux options. Tout d’abord, l’administrateur peut spécifier le type de mappage comme étant `Literal` et saisir une valeur de mappage sous la forme d’une chaîne, telle que `hello.` et Watched Folder appelle le service avec la chaîne `hello`. Deuxième option : l’administrateur peut définir le type de mappage sur `Variable`, puis saisir une valeur de mappage avec un modèle du type `*.txt`. Dans le deuxième cas, les fichiers ayant pour extension .txt seront lus comme un document converti sous forme de chaîne pour appeler le service.
   * Type primitif Java : l’administrateur peut définir le type de mappage sur `Literal` et fournir la valeur. Le dossier de contrôle appellera le service avec la valeur spécifiée.

* Le dossier de contrôle est destiné à fonctionner avec des documents. Les sorties prises en charge sont `com.adobe.idp.Document`, `org.w3c.Document` et `org.w3c.Node`, de même qu’une liste et un mappage de ces types. Tout autre type entraînera une sortie d’échec dans le dossier d’échec.
* Si les résultats ne se trouvent pas dans le dossier de résultats, vérifiez le dossier d’échec pour voir si un échec s’est produit.
* Le dossier de contrôle fonctionne mieux s’il est utilisé en mode asynchrone. Dans ce mode, le dossier de contrôle place la requête d’appel dans la file d’attente et effectue un nouvel appel. La file d’attente est ensuite traitée de manière asynchrone. Lorsque l’option Asynchrone n’est pas définie, le dossier de contrôle appelle le service cible de manière synchrone et Process Engine attend que le service ait terminé la requête et que les résultats soient produits. Si le service cible met beaucoup de temps à traiter la requête, le dossier de contrôle peut recevoir des erreurs d’expiration de délai.
* La création de dossiers de contrôle pour les opérations d’import et d’export ne permet pas l’abstraction des extensions de nom de fichier. Lors de l’appel du service Form Data Integration à l’aide de dossiers de contrôle, le type d’extension de nom du fichier de sortie peut ne pas correspondre au format de sortie prévu pour le type d’objet de document. Par exemple, si le fichier d’entrée d’un dossier de contrôle qui appelle l’opération d’export est un formulaire XFA contenant des données, la sortie doit être un fichier de données XDP. Pour obtenir un fichier de sortie avec l’extension de nom de fichier correcte, vous pouvez la spécifier dans le mappage des paramètres de sortie. Dans cet exemple, vous pouvez utiliser %F.xdp pour le mappage des paramètres de sortie.
* Le dossier de contrôle peut traiter les fichiers d’entrée avant qu’ils ne soient complètement copiés dans le dossier. Le verrouillage des fichiers n’est pas obligatoire sous UNIX comme sous Windows. Pour cette raison, lorsqu’un fichier est copié dans un dossier de contrôle, le dossier de contrôle peut déplacer le fichier vers l’évaluation sans attendre la fin de la copie du fichier. Ce comportement entraîne le traitement d’une seule partie du fichier d’entrée. Il existe actuellement deux solutions de contournement :

   * Solution de contournement 1

      1. Spécifiez un modèle pour l’option Modèles de fichier d’exclusion, tel que temp&amp;ast;.ps.
      1. Copiez les fichiers dont le nom commence par temp (par exemple, temp1.ps) dans le dossier de contrôle.
      1. Une fois le fichier intégralement copié dans le dossier de contrôle, renommez-le pour le faire correspondre au modèle spécifié dans Modèle de fichier d’inclusion. Le dossier de contrôle déplace ensuite le fichier terminé vers l’évaluation.

   * Solution de contournement 2

     Si vous connaissez la durée maximale nécessaire pour copier vos fichiers dans un dossier de contrôle, spécifiez la durée en secondes pour Temps d’attente. Le dossier de contrôle attend ensuite la durée spécifiée avant de déplacer le fichier vers l’évaluation.

     Ce n’est pas un problème pour les fichiers sous Windows, car Windows verrouille un fichier lorsqu’un thread est en cours d’écriture. Cependant, il s’agit d’un problème pour les dossiers sous Windows. Pour les dossiers, vous devez suivre les étapes de la solution de contournement 1.

* Si l’attribut de point d’entrée Preserve Folder Name pour le dossier de contrôle est défini sur un chemin de répertoire nul, le répertoire intermédiaire n’est pas nettoyé comme il devrait l’être. Le répertoire contient toujours le fichier traité et le dossier temporaire.

## Recommandations spécifiques au service pour les dossiers de contrôle {#service-specific-recommendations-for-watched-folders}

Pour tous les services, vous devez ajuster la taille du lot et l’intervalle de répétition du dossier de contrôle afin que la vitesse à laquelle le dossier de contrôle récupère les nouveaux fichiers et dossiers à traiter ne dépasse pas la vitesse des traitements pouvant être traités par le serveur AEM Forms. Les paramètres réels à utiliser peuvent varier en fonction du nombre de dossiers de contrôle configurés, des services qui utilisent les dossiers de contrôle et de l’intensité des traitements sur le processeur.

### Recommandations relatives au service Generate PDF {#generate-pdf-service-recommendations}

* Le service Generate PDF ne peut convertir qu’un seul fichier à la fois pour les types de fichiers suivants : Microsoft Word, Microsoft Excel, Microsoft PowerPoint, Microsoft Project, AutoCAD, Adobe Photoshop®, Adobe FrameMaker® et Adobe PageMaker®. Ce sont des traitements de longue durée ; par conséquent, assurez-vous de maintenir la taille du lot à un niveau faible. Augmentez également l’intervalle de répétition s’il y a plus de nœuds dans le cluster.
* Pour les types de fichiers PostScript (PS), Encapsulated PostScript (EPS) et image, le service Generate PDF peut traiter plusieurs fichiers en parallèle. Vous devez soigneusement ajuster la taille du pool de session bean (qui régit le nombre de conversions qui seront effectuées en parallèle) en fonction de la capacité de votre serveur et du nombre de nœuds dans le cluster. Augmentez ensuite la taille du lot jusqu’à un nombre égal à la taille du pool de session beans pour les types de fichiers que vous essayez de convertir. La fréquence d’interrogation doit être dictée par le nombre de nœuds dans le cluster. Toutefois, étant donné que le service Generate PDF traite ce type de traitements assez rapidement, vous pouvez configurer l’intervalle de répétition sur une valeur faible, telle que 5 ou 10.
* Même si le service Generate PDF ne peut convertir qu’un seul fichier OpenOffice à la fois, la conversion est assez rapide. La logique ci-dessus pour les conversions PS, EPS et d’images s’applique également aux conversions OpenOffice.
* Pour permettre une répartition uniforme de la charge dans le cluster, maintenez la taille du lot faible et augmentez l’intervalle de répétition.

### Recommandations relatives au service Barcoded Forms {#barcoded-forms-service-recommendations}

* Pour obtenir de meilleures performances dans le traitement des formulaires à codes-barres (fichiers de petite taille), saisissez `10` pour la taille du lot et `2` pour l’intervalle de répétition.
* Lorsque le nombre de fichiers du dossier input est important, il n’est pas impossible que des erreurs avec des fichiers masqués appelés *thumbs.db* surviennent. Il est dès lors recommandé de définir le modèle de fichier d’inclusion pour les fichiers d’inclusion sur la même valeur que celle indiquée pour la variable d’entrée (par exemple, `*.tiff`). Cela empêche ainsi Watched Folder de traiter les fichiers DB.
* Une taille du lot de `5` et un intervalle de répétition de `2` suffisent normalement car Barcoded Forms traite habituellement un code-barres en 0,5 seconde.
* Le dossier de contrôle n’attend pas que Process Engine termine la tâche avant de récupérer de nouveaux fichiers ou dossiers. Il continue d’analyser le dossier surveillé et d’appeler le service cible. Ce comportement peut surcharger le moteur, provoquant des problèmes de ressources et des délais d’attente. Assurez-vous d’utiliser l’intervalle de répétition et la taille du lot pour limiter l’entrée du dossier surveillé. Vous pouvez augmenter l’intervalle de répétition et réduire la taille du lot s’il existe davantage de dossiers surveillés ou activer la limitation sur le point de d’entrée. Pour plus d’informations sur la limitation, voir [À propos de la limitation](configuring-watched-folder-endpoints.md#about-throttling).
* Le dossier de contrôle emprunte l’identité de l’utilisateur ou l’utilisatrice spécifié dans le nom d’utilisateur et le nom de domaine. Il appelle le service en tant que cet utilisateur ou cette utilisatrice s’il est invoqué directement ou si le processus est de courte durée. Pour un processus de longue durée, le processus est invoqué avec le contexte système. Les administrateurs et administratrices peuvent définir des politiques de système d’exploitation pour le dossier de contrôle afin de déterminer à quel utilisateur ou utilisatrice autoriser ou refuser l’accès.
* Utilisez des modèles de fichiers pour organiser les résultats, les échecs et conserver les dossiers. (Voir [À propos des modèles de fichiers](configuring-watched-folder-endpoints.md#about-file-patterns).)

* Le dossier de contrôle s’appuie sur le planificateur Quartz pour analyser les dossiers surveillés. Le planificateur Quartz dispose d’un pool de threads qui les analyse. Si l’intervalle de répétition du dossier de contrôle est très faible (&lt; 5 secondes) et que la taille du lot est élevée (> 2 secondes), une situation de concurrence critique peut se produire. Lorsque cette condition se produit, un fichier est récupéré par deux threads Quartz :

   * L’un des threads trouve le fichier et appelle le service cible avec le fichier.
   * Le deuxième thread voit le fichier mais échoue lorsqu’il tente de savoir si le fichier est valide (fichier en lecture ou en écriture), ce qui provoque de faux échecs indiquant que le fichier ne peut pas être traité car il est en lecture seule. Cela se produit uniquement avec un faible intervalle de répétition et une taille de lot élevée.
