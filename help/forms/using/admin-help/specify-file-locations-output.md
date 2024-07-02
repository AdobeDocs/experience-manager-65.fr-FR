---
title: Définir les emplacements de fichiers pour Output
description: Découvrez comment spécifier des emplacements de fichiers pour Output pour certains types de fichiers, par exemple, URI racine du contenu, Fichier de configuration XCI, Cache et Par défaut.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 620c69d6-4fe1-46d6-b5d4-3b562142e547
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '327'
ht-degree: 100%

---

# Définir les emplacements de fichiers pour Output {#specify-file-locations-for-output}

Vous pouvez spécifier les emplacements dans lesquels Output recherche certains types de fichiers requis.

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Emplacements, spécifiez les options appropriées.
1. Cliquez sur Enregistrer.

## Paramètres des emplacements {#locations-settings}

**URI racine du contenu :** URI ou emplacement absolu du répertoire de récupération des formulaires. Cette valeur est combinée avec le paramètre sForm, indiqué via l’API, pour construire l’URL absolue vers le formulaire à récupérer. Cette valeur peut référencer un répertoire ou un emplacement web accessible via HTTP.

La valeur par défaut est une chaîne vide.

**Fichier de configuration XCI :** emplacement relatif ou absolu du fichier de configuration XCI utilisé par le service Output pour les opérations de rendu. Si la valeur est relative, il est supposé que le fichier XCI réside dans le fichier EAR déployable d’AEM forms.

La valeur par défaut est `com/adobe/formServer/PA/pa_output.xci`.

**Emplacement du cache :** détermine l’emplacement du cache disque d’Output. Lorsque vous modifiez ce paramètre, toutes les informations de cache existantes de l’emplacement actuel sont réinitialisées et un nouveau cache est créé au nouvel emplacement. Sélectionnez l’une des options suivantes :

**Emplacement par défaut :** il s’agit de la sélection par défaut. Lorsque cette option est sélectionnée, le cache est créé à un emplacement différent selon le serveur d’applications utilisé :

* **JBoss :**`[JBoss Home]\server\[install type]\svcdata\Output\Cache` 
* **WebLogic :**`[WebLogic Home]\user_projects\domains\[aem-forms domain Name]\adobe\[Forms Server name]\Output\Cache`
* **WebSphere :**`[IBM Home]\WebSphere\AppServer\installedApps\adobe\server1\Output\Cache`

**Répertoire temporaire LC :** le cache est créé dans le sous-répertoire du répertoire temporaire d’AEM Forms, qui est spécifié dans la console d’administration sous Paramètres > Paramètres de Core System > Configurations > Emplacement du répertoire temporaire. Le sous-répertoire est nommé `adobeoutput_[servername]`.

>[!NOTE]
>
>Si vous utilisez un utilitaire de nettoyage des répertoires temporaires, bien que la suppression de ces répertoires n’affecte pas les fonctionnalités, elle peut affecter considérablement les performances pendant une courte période jusqu’à la création du nouveau cache. Pour éviter ce problème, ne supprimez pas ces répertoires lors de l’effacement du répertoire temporaire d’AEM Forms.
