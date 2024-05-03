---
title: Créer ou configurer un dossier de contrôle
description: Découvrez comment créer ou supprimer un dossier de contrôle ou modifier les propriétés d’un dossier de contrôle existant.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: b15d8d3b-5e47-4c33-95fe-440fcf96be83
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 99%

---

# Création ou configuration d’un dossier de contrôle {#create-or-configure-a-watched-folder}

Un administrateur ou une administratrice peut configurer un dossier réseau, appelé *dossier de contrôle*, de sorte que, lorsqu’une personne place un fichier (fichier PDF, par exemple) dans le dossier de contrôle, une opération préconfigurée est lancée pour manipuler le fichier. Une fois l’opération spécifiée réalisée, le fichier modifié est enregistré dans un dossier de sortie spécifié. Pour plus d’informations sur l’administration d’un dossier de contrôle, voir [Aide d’administration](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md).

Vous pouvez utiliser l’interface utilisateur du dossier de contrôle pour :

* Créer un dossier de contrôle
* Modifier les propriétés d’un dossier de contrôle existant
* Supprimer un dossier de contrôle

## Créer un dossier de contrôle {#create-a-watched-folder}

Avant de configurer un dossier de contrôle, vérifiez les éléments suivants :

* Les dossiers de contrôle sont une fonctionnalité avancée d’AEM Forms. Le module complémentaire AEM Forms est requis pour un bon fonctionnement. Assurez-vous que le module complémentaire approprié d’AEM Forms est installé et configuré.
* Vous pouvez créer le dossier de contrôle dans un espace de stockage partagé ou un espace de stockage local. Assurez-vous que la personne configurée dans AEM Forms pour exécuter le dossier de contrôle dispose des autorisations de lecture et d’écriture sur le dossier de contrôle.
* Vous pouvez utiliser un service, un workflow ou un script pour automatiser une opération avec un dossier de contrôle. Assurez-vous que le service, le workflow ou le script correspondant est créé et prêt à être exécuté. Pour des informations sur la création d’un service, workflow et script, voir [Diverses méthodes pour traiter les fichiers](/help/forms/using/watched-folder-in-aem-forms.md#various-methods-for-processing-files).
* Un dossier de contrôle possède plusieurs propriétés, voir [Propriétés des dossiers de contrôle](watched-folder-in-aem-forms.md#watchedfolderproperties).

Effectuez les étapes suivantes pour créer un dossier de contrôle :

1. Sélectionnez l’icône d’**Adobe Experience Manager** dans le coin supérieur gauche de l’écran.
1. Sélectionnez **Outils** > **Forms** > **Configurer le dossier de contrôle.** La liste des dossiers de contrôle déjà configurés s’affiche.
1. Sélectionnez **Nouveau**. La liste des champs nécessaires à la création du dossier de contrôle s’affiche :

   * **Nom** : identifie le dossier de contrôle. Utilisez uniquement des caractères alphanumériques pour le nom.
   * **Chemin** : indique l’emplacement du dossier de contrôle. Dans un environnement en cluster, ce paramètre doit pointer vers un dossier de réseau partagé, accessible pour chaque utilisateur et utilisatrice exécutant AEM sur des nœuds différents d’un cluster.
   * **Traiter les fichiers avec** : te type de processus à démarrer. Vous pouvez spécifier le workflow, le script, ou le service.
   * **Nom du service/Chemin du script/Chemin du workflow** : le comportement du champ est basé sur la valeur spécifiée pour le champ **Traiter les fichiers avec**. Vous pouvez spécifier les valeurs suivantes :

      * Pour un workflow, indiquez le modèle de workflow à exécuter. Par exemple, /etc/workflow/models/&lt;nom_workflow>/jcr:content/model.
      * Pour un script, précisez le chemin JCR du script à exécuter. Par exemple, /etc/watchfolder/test/testScript.ecma.
      * Pour le service, spécifiez le filtre utilisé pour localiser un service OSGi. Le service est enregistré comme une implémentation de l’interface de com.adobe.aemfd.watchfolder.service.api.ContentProcessor. Par exemple, le code suivant est une implémentation personnalisée de l’interface ContentProcessor avec une propriété personnalisée (foo=bar).

   >[!NOTE]
   >
   >Si vous avez sélectionné **Service** pour le champ **Traiter les fichiers à l’aide de**, la valeur du champ Nom du service (inputProcessorType) doit être mise entre parenthèses. Par exemple : (foo=bar).

   ```java
   @Component(metatype = true, immediate = true, label = "WF Test Service", description = "WF Test Service")
   @Service(value = {OutputWriter.class, ContentProcessor.class})
   @Property(name = "foo", value = "bar")
   public class OutputWriter implements ContentProcessor {
   ```

   * **Modèle de fichier de sortie** : spécifiez une liste délimitée par point-virgule (;) de modèles utilisés par un dossier de contrôle pour déterminer le nom et l’emplacement des dossiers et fichiers de sortie. Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

1. Sélectionnez **Avancé**. L’onglet Avancé contient d’autres champs. La plupart de ces champs contiennent une valeur par défaut.

   * **Filtre du mappeur de charge :** lorsque vous créez un dossier de contrôle, il crée une structure de dossiers dans le dossier contrôlé. La structure de dossiers est constituée de dossiers d’étapes, de résultats, de conservations, d’entrées et d’échecs. La structure de dossiers peut servir de charge utile d’entrée au workflow et accepte la sortie d’un workflow. Elle peut également répertorier les points d’échec, le cas échéant. La structure d’une charge utile est différente de celle d’un dossier de contrôle. Vous pouvez écrire des scripts personnalisés pour mapper la structure d’un dossier de contrôle à la charge utile. Un tel script est appelé le filtre du mappeur de charge. Deux implémentations de mappeur de charge prêtes à l’emploi sont disponibles. Si vous ne disposez pas d’[une implémentation personnalisée](/help/forms/using/watched-folder-in-aem-forms.md#creating-a-custom-payload-mapper-filter), utilisez l’une des implémentations prêtes à l’emploi :

      * **Mappeur par défaut :** utilisez le mappeur de charge par défaut pour conserver les contenus d’entrée et de sortie des dossiers de contrôle dans des dossiers d’entrée et de sortie distincts dans la charge utile.
      * **Mappeur de charge basé sur des fichiers simples :** utilisez le mappeur de charge basé sur des fichiers simples pour conserver les contenus d’entrée et de sortie directement dans le dossier de charge utile. Tout comme pour le mappeur par défaut, aucune hiérarchie supplémentaire n’est créée.

   * **Mode d’exécution** : spécifiez la liste séparée par des virgules de modes d’exécution autorisés pour l’exécution du workflow.
   * **Expiration des fichiers de scène toutes les** : indiquez le nombre de secondes à attendre pour qu’un fichier/dossier d’entrée ayant déjà été collecté pour traitement soit traité comme ayant expiré et défini comme étant un échec. Le mécanisme d’expiration s’active uniquement lorsque la valeur de cette propriété est un nombre positif.
   * **Supprimer les fichiers de scène expirés en cas de ralentissement** : si cette option est activée, le mécanisme **Expiration des fichiers de scène toutes les** est activé uniquement lorsque l’option de ralentissement est activé pour le dossier de contrôle.
   * **Analyser le dossier d’entrée toutes les :** spécifiez l’intervalle de temps, en secondes, entre les analyses du dossier de contrôle des entrées. À moins que le paramètre Ralentissement ne soit activé, l’attribut Intervalle de répétition doit être supérieur à la durée du traitement d’une tâche moyenne, faute de quoi le système risque d’être surchargé. La valeur de l’intervalle doit être supérieure ou égale à un.
   * **Exclure le modèle de fichier** : indiquez une liste délimitée par des points-virgules (;) de modèles utilisés par un dossier de contrôle pour déterminer les fichiers et les dossiers à analyser et à sélectionner. Les fichiers ou les dossiers pourvus de ce modèle spécifié ne sont pas analysés en vue d’être traités. Pour plus d’informations sur les modèles de fichiers, voir [A propos des modèles de fichier](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Inclure le modèle de fichier** : spécifiez une liste délimitée par des points-virgules (;) des modèles utilisés par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Ainsi, si le paramètre Inclure le modèle de fichier a pour valeur input&amp;ast;, tous les fichiers et dossiers correspondant à input&amp;ast; sont sélectionnés. La valeur par défaut, &amp;ast;, désigne tous les fichiers et les dossiers. Pour plus d’informations sur les modèles de fichiers, voir [À propos des modèles de fichier](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).
   * **Durée d’attente :** indiquez le temps, en millisecondes, à patienter avant l’analyse d’un dossier ou fichier après sa création. Par exemple, si la durée d’attente est de 3 600 000 millisecondes (une heure) et que le fichier a été créé il y a une minute, ce dernier sera sélectionné à l’issue d’un laps de temps de 59 minutes ou plus. La valeur par défaut est 0.

     Ce paramètre assure la copie intégrale d’un fichier ou d’un dossier dans le dossier d’entrée. Par exemple, si vous devez traiter un fichier volumineux dont le téléchargement dure dix minutes, définissez une durée d’attente de 10&amp;ast;60 &amp;ast;1000 millisecondes. Cet intervalle évite que le dossier de contrôle analyse le fichier tant que ce dernier a une existence inférieure à dix minutes.

   * **Supprimer les résultats antérieurs à :** indiquez l’heure, en fonction du nombre de jours, à attendre avant de supprimer les fichiers et dossiers antérieurs à la valeur spécifiée. Grâce à ce paramètre, le dossier obtenu n’est jamais plein. La valeur -1 jour indique de ne jamais supprimer le dossier de résultats. La valeur par défaut est -1.
   * **Nom du dossier de résultat :** spécifiez le nom du dossier dans lequel enregistrer les résultats. Si les résultats ne s’affichent pas dans ce dossier, vérifiez le dossier des échecs. Les fichiers en lecture seule ne sont pas traités ; ils sont enregistrés dans le dossier des échecs. Vous pouvez utiliser un chemin d’accès relatif ou absolu répondant aux modèles de fichiers suivants :

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
      * Par exemple, s’il est 20 h, que nous sommes le 17 juillet 2009 et que vous définissez C:/Test/WF0/failure/%Y/%M/%D/%H/, le dossier result est alors C:/Test/WF0/failure/2009/07/17/20.
      * Si le chemin d’accès n’est pas absolu, mais relatif, le dossier est créé dans le dossier de contrôle. La valeur par défaut est result/%Y/%M/%D/, qui correspond au dossier result dans le dossier de contrôle. Pour plus d’informations sur les modèles de fichiers, voir [À propos des modèles de fichier](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-file-patterns).

   * **Nom du dossier Échecs :** spécifiez le dossier dans lequel les fichiers en situation d’échec sont enregistrés. Cet emplacement dépend toujours du dossier de contrôle. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier result.
   * **Conserver le nom de dossier :** indiquez le dossier dans lequel les fichiers sont stockés après avoir été analysés et sélectionnés. Le chemin d’accès peut être absolu, relatif ou vide. Vous pouvez utiliser des modèles de fichiers, comme indiqué pour le dossier result. La valeur par défaut est preserve/%Y/%M/%D/.
   * **Taille du lot :** indiquez le nombre de fichiers ou de dossiers à sélectionner par analyse. Ce paramètre permet d’éviter une surcharge du système, car l’analyse simultanée d’un trop grand nombre de fichiers peut provoquer une panne. La valeur par défaut est 2.

     Si l’intervalle d’analyse est court, les threads analysent souvent le dossier d’entrée. Si des fichiers sont déposés régulièrement dans le dossier de contrôle, il est préférable que l’intervalle d’analyse soit court. Si les fichiers sont rarement déposés, choisissez un intervalle d’analyse plus long afin que les autres services puissent utiliser les threads.

   * **Ralentir sur :** lorsque cette option est sélectionnée, elle permet de limiter le nombre de tâches du dossier de contrôle qu’AEM Forms peut traiter en une seule fois. La valeur Taille du lot détermine le nombre maximal de tâches. Pour plus d’informations, voir [ralentissement](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#about-throttling)
   * **Écraser les fichiers existants portant le même nom :** lorsque ce paramètre est défini sur true, les fichiers du dossier obtenu et du dossier conservé sont remplacés. Lorsqu’il est défini sur False, les fichiers et les dossiers avec un suffixe d’index numérique sont utilisés pour le nom. La valeur par défaut est False.
   * **Conserver les fichiers en cas d’échec :** lorsque ce paramètre est défini sur True, les fichiers d’entrée sont conservés en cas d’échec. La valeur par défaut est true.
   * **Inclure les fichiers avec modèle :** spécifiez une liste délimitée par des points-virgules (;) des modèles utilisés par le dossier de contrôle pour déterminer les dossiers et les fichiers à analyser et à sélectionner. Ainsi, si le paramètre Inclure le modèle de fichier a pour valeur Entrée, tous les fichiers et les dossiers correspondant à Entrée sont sélectionnés. Pour plus d’informations, voir [Aide à l’administration](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md) 
   * **Appeler un dossier de contrôle de manière asynchrone :** identifie le type d’appel comme étant asynchrone ou synchrone. La valeur par défaut est asynchrone. Le mode asynchrone est recommandé pour les processus de longue durée, tandis que le mode synchrone est recommandé pour les processus transitoires ou de courte durée.
   * **Activer le dossier de contrôle :** lorsque cette option est activée, le dossier de contrôle est activé. La valeur par défaut est True.

## Modifier les propriétés d’un dossier de contrôle existant {#modify-properties-of-an-existing-watched-folder}

En plus de modifier le nom du dossier de contrôle, vous pouvez également modifier toutes les propriétés d’un dossier de contrôle existant. Effectuez les étapes suivantes pour modifier les propriétés d’un dossier de contrôle existant :

1. Sélectionnez l’icône **Adobe Experience Manager** dans le coin supérieur gauche de l’écran.
1. Sélectionnez **Outils** > **Forms** > **Configurer le dossier de contrôle.** La liste des dossiers de contrôle déjà configurés s’affiche.
1. Sur le côté gauche de l’écran du dossier de contrôle, sélectionnez le dossier de contrôle et **Modifier.** La liste des champs nécessaire à la création du dossier de contrôle s’affiche. Les champs répertoriés dans l’onglet **Réglages de base** sont obligatoires. L’onglet Avancé contient d’autres champs. La plupart de ces champs contiennent une valeur par défaut. Vous pouvez modifier ces propriétés selon vos besoins.
1. Après avoir modifié les propriétés, sélectionnez **Mettre à jour**. Les propriétés modifiées sont enregistrées.
