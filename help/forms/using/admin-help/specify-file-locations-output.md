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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%
---
# Définir les emplacements de fichiers pour Output {#specify-file-locations-for-output}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Vous pouvez spécifier les emplacements dans lesquels Output recherche certains types de fichiers requis.

1. Dans la console d’administration, cliquez sur Services > sortie.
1. Sous Emplacements, spécifiez les options appropriées.
1. Cliquez sur Enregistrer.

## Paramètres des emplacements {#locations-settings}

**URI racine du contenu :** URI ou emplacement absolu du répertoire de récupération des formulaires. Cette valeur est combinée avec le paramètre sForm, indiqué via l’API, pour construire le chemin d’accès absolu vers le formulaire à récupérer. Cette valeur peut référencer un répertoire ou un emplacement web accessible via HTTP.

La valeur par défaut est une chaîne vide.

**Fichier de configuration XCI :** emplacement relatif ou absolu du fichier de configuration XCI utilisé par le service Output pour les opérations de rendu. Si la valeur est relative, il est supposé que le fichier XCI réside dans le fichier EAR déployable d’AEM Forms.

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
