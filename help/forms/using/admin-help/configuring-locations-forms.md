---
title: Configuration des emplacements pour Forms
description: Découvrez comment configurer l’emplacement d’AEM Forms. Vous pouvez spécifier les emplacements de fichier de l’attribut, l’emplacement du formulaire, le fichier du PDF de contrôle et l’emplacement du cache.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
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
source-wordcount: '838'
ht-degree: 100%
---
# Configuration des emplacements pour Forms {#configuring-locations-for-forms}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Vous pouvez spécifier les emplacements URL, URI et fichier des attributs, tels que la racine web, l’emplacement des formulaires à récupérer, le fichier PDF initial utilisé dans les transformations PDFForm et l’emplacement du cache.

1. Dans la console d’administration, cliquez sur Services > Forms.
1. Sous Emplacements, spécifiez les options appropriées. Les options sont décrites ci-dessous.
1. Cliquez sur Enregistrer.

## Paramètres des emplacements {#locations-settings}

**URL de base :** URL de base où se trouvent les ressources de formulaires telles que les images et les scripts. Cette valeur est requise pour les transformations HTML qui incluent des références HREF à des dépendances externes, telles que des images ou des scripts. xfasubset.js est l’un de ces scripts, nécessaire pour que les formulaires HTML puissent effectuer des opérations d’intelligence XFA. Cette valeur doit être l’équivalent HTTP de l’URI racine du contenu.

>[!NOTE]
>
>L’URL de base ne prend en charge que les protocoles HTTP ou de référentiel. Elle ne prend pas en charge les protocoles tels que file:///. Si vous devez accéder à une ressource telle qu’un CSS personnalisé ou un URI de signature numérique, utilisez la valeur de paramètre d’API appropriée pour spécifier l’emplacement absolu.

Lorsqu’un chemin de dépendance est absolu, la valeur de l’URL de base est ignorée. Dans le cas contraire, le chemin de dépendance est combiné à l’URL de base.

La valeur par défaut est une chaîne vide.

L’exemple suivant pointe vers le même contenu (à l’aide de l’URI racine du contenu et de l’URL de base) :

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI racine web FS :** URL de l’application web de Forms. Vous pouvez laisser ce champ vide si l’application web Forms et l’application cliente sont déployées sur le même serveur d’applications ; l’URL racine web de l’API Forms est utilisée.

Si l’application web Forms et l’application cliente ne sont pas déployées sur le même serveur d’applications, indiquez l’URL de l’application web Forms dans cette zone, comme indiqué dans l’exemple suivant :

`https://<host name>:<port>/FormServer`

Où `host name` et `port` correspondent au nom du serveur et au numéro de port du serveur hébergeant l’application web de Forms.

La valeur par défaut est une chaîne vide.

**URI racine web :** racine web de l’application. Cette valeur est combinée avec le paramètre sTargetURL (lorsque sTargetURL est fourni en tant que valeur relative), indiqué via le SDK d’AEM Forms, pour construire une URL absolue et accéder ainsi au contenu web spécifique de l’application.

La valeur par défaut est une chaîne vide.

**URI racine du contenu :** URI ou emplacement absolu pour la récupération des formulaires. Cette valeur est combinée avec le paramètre sFormQuery, indiqué via l’API, pour construire le chemin d’accès absolu vers le formulaire à récupérer. Cette valeur peut référencer un répertoire ou un emplacement web accessible via HTTP.

La valeur par défaut est une chaîne vide.

**URI de configuration XCI :** emplacement relatif ou absolu du fichier XCI utilisé pour le rendu. Si la valeur est relative, il est supposé que le fichier XCI réside dans le fichier EAR déployable d’AEM Forms.

La valeur par défaut est `com/adobe/formServer/PA/pa.xci`.

**URI de mappage de polices :** emplacement relatif ou absolu du fichier de mappage de polices. Pour une valeur relative, on suppose que ce fichier réside dans le fichier EAR déployable d’AEM Forms.

Le fichier de mappage des polices est utilisé pour créer des mappages de polices personnalisés pour les transformations de HTML dans les formulaires. Vous pouvez ainsi spécifier la police qui sera remplacée lorsqu’une police n’est pas disponible sur l’ordinateur du client ou de la cliente.

La valeur par défaut est `com/adobe/formServer/client-font-map.properties`.

L’exemple suivant présente une entrée dans le fichier de mappage de polices :

`Arial=Arial,Helvetica,sans-serif`

**Fichier PDF initial :** fichier PDF initial utilisé dans une transformation PDFForm pour un envoi optimisé. Le fichier PDF de départ spécifie un fichier PDF personnalisé (contenant uniquement des ressources de flux XFA, d’image et de police) auquel sont ajoutées la conception du formulaire et les données. Le formulaire est rendu par Acrobat 7 ou une version ultérieure et s’applique à la transformation PDFForm.

La valeur par défaut est une chaîne vide.

**Emplacement du cache :** détermine l’emplacement du cache disque de Forms. Lorsque vous modifiez ce paramètre, toutes les informations de cache existantes de l’emplacement actuel sont réinitialisées et un nouveau cache est créé au nouvel emplacement. Sélectionnez l’une des options suivantes :

**Emplacement par défaut :** il s’agit de la sélection par défaut. Lorsque cette option est sélectionnée, le cache est créé à un emplacement différent selon le serveur d’applications utilisé :

* **JBoss :** [JBoss Home]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic :** [WebLogic Home]\user_projects\domains\[aem-forms Domain Name]\adobe\[Forms Server name]\FormServer\Cache
* **WebSphere :** [Répertoire racine IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Répertoire temporaire LC :** le cache est créé dans le sous-répertoire du répertoire temporaire dʼAEM Forms, qui est spécifié dans la console dʼadministration sous Paramètres > Paramètres de Core System > Configurations > Emplacement du répertoire temporaire. Le sous-répertoire se nomme adobeform_[nom_serveur].

>[!NOTE]
>
>Si vous utilisez un utilitaire de nettoyage des répertoires temporaires, bien que la suppression de ces répertoires n’affecte pas les fonctionnalités, elle peut affecter considérablement les performances pendant une courte période jusqu’à la création du nouveau cache. Pour éviter ce problème, ne supprimez pas ces répertoires lors de l’effacement du répertoire temporaire d’AEM Forms.
