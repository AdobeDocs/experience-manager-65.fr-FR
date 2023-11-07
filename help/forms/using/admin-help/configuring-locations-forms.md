---
title: Configurer les emplacements pour Forms
description: Découvrez comment configurer l’emplacement d’AEM Forms. Vous pouvez spécifier les emplacements de fichier de l’attribut, l’emplacement du formulaire, le fichier du PDF de contrôle et l’emplacement du cache.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
exl-id: 0d9eb7fe-28a6-444e-957d-023687158c61
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 44%

---

# Configurer les emplacements pour Forms {#configuring-locations-for-forms}

Vous pouvez spécifier les emplacements URL, URI et fichier des attributs, tels que la racine web, l’emplacement des formulaires à récupérer, le fichier du PDF de contrôle utilisé dans les transformations PDFForm et l’emplacement du cache.

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Emplacements, spécifiez les options appropriées. Les options sont décrites ci-dessous.
1. Cliquez sur Enregistrer.

## Paramètres des emplacements {#locations-settings}

**URL de base :** URL de base où se trouvent les ressources de formulaires telles que les images et les scripts. Cette valeur est requise pour les transformations de HTML qui incluent des références HREF à des dépendances externes, telles que des images ou des scripts. xfasubset.js est l’un de ces scripts, nécessaire pour que les formulaires de HTML puissent effectuer des opérations d’intelligence XFA. Cette valeur doit être l’équivalent HTTP de l’URI racine du contenu.

>[!NOTE]
>
>L’URL de base ne prend en charge que les protocoles HTTP ou de référentiel. Il ne prend pas en charge les protocoles tels que file:///. Si vous devez accéder à une ressource telle qu’un CSS personnalisé ou un URI de signature numérique, utilisez la valeur de paramètre d’API appropriée pour spécifier l’emplacement absolu.

Lorsqu’un chemin de dépendance est absolu, la valeur de l’URL de base est ignorée. Dans le cas contraire, le chemin d’accès à la dépendance est combiné à l’URL de base.

La valeur par défaut est une chaîne vide.

L’exemple suivant pointe vers le même contenu (à l’aide de l’URI racine du contenu et de l’URL de base) :

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI racine web FS :** URL de l’application web de Forms. Vous pouvez laisser ce champ vide si l’application web Forms et l’application cliente sont déployées sur le même serveur d’applications ; l’URL racine Web de l’API Forms est utilisée.

Si l’application web Forms et l’application cliente ne sont pas déployées sur le même serveur d’applications, indiquez l’URL de l’application web Forms dans cette zone, comme indiqué dans l’exemple suivant :

`https://<host name>:<port>/FormServer`

Où `host name` et `port` correspondent au nom du serveur et au numéro de port du serveur hébergeant l’application web de Forms.

La valeur par défaut est une chaîne vide.

**URI racine web :** racine web de l’application. Cette valeur est combinée avec le paramètre sTargetURL (lorsque sTargetURL est fourni en tant que valeur relative), indiqué via le SDK d’AEM forms, pour construire une URL absolue et accéder ainsi au contenu Web spécifique de l’application.

La valeur par défaut est une chaîne vide.

**URI racine du contenu :** URI ou emplacement absolu pour la récupération des formulaires. Cette valeur est combinée avec le paramètre sFormQuery, indiqué via l’API, pour construire l’URL absolue vers le formulaire à récupérer. Cette valeur peut référencer un répertoire ou un emplacement web accessible via HTTP.

La valeur par défaut est une chaîne vide.

**URI de configuration XCI :** emplacement relatif ou absolu du fichier XCI utilisé pour le rendu. Si la valeur est relative, il est supposé que le fichier XCI réside dans le fichier EAR déployable d’AEM forms.

La valeur par défaut est `com/adobe/formServer/PA/pa.xci`.

**URI de mappage de polices :** emplacement relatif ou absolu du fichier de mappage de polices. Pour une valeur relative, il est supposé que ce fichier réside dans le fichier EAR déployable d’AEM forms.

Le fichier de mappage des polices est utilisé pour créer des mappages de polices personnalisés pour les transformations de HTML dans les formulaires. Vous pouvez ainsi spécifier la police qui sera remplacée lorsqu’une police n’est pas disponible sur l’ordinateur du client.

La valeur par défaut est `com/adobe/formServer/client-font-map.properties`.

L’exemple suivant présente une entrée dans le fichier de mappage de polices :

`Arial=Arial,Helvetica,sans-serif`

**Fichier PDF initial :** fichier PDF initial utilisé dans une transformation PDFForm pour un envoi optimisé. Le fichier du PDF de départ spécifie un fichier de PDF personnalisé (contenant uniquement des ressources de flux XFA, d’image et de police) qui est ajouté à la conception de formulaire et aux données. Le formulaire est rendu par Acrobat 7 ou une version ultérieure et s’applique à la transformation PDFForm.

La valeur par défaut est une chaîne vide.

**Emplacement du cache :** détermine l’emplacement du cache disque de Forms. Lorsque vous modifiez ce paramètre, toutes les informations de cache existantes de l’emplacement actuel sont réinitialisées et un nouveau cache est créé au nouvel emplacement. Sélectionnez l’une des options suivantes :

**Emplacement par défaut :** il s’agit de la sélection par défaut. Lorsque cette option est sélectionnée, le cache est créé à un emplacement différent selon le serveur d’applications utilisé :

* **JBoss :** [JBoss Home]\server\[install type]\svcdata\FormServer\Cache
* **WebLogic :** [Répertoire racine WebLogic]\user_projects\domains\[nom de domaine aem-forms]\adobe\[nom du serveur forms]\FormServer\Cache
* **WebSphere :** [Répertoire racine IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Répertoire temporaire LC :** le cache est créé dans le sous-répertoire du répertoire temporaire dʼAEM Forms, qui est spécifié dans la console dʼadministration sous Paramètres > Paramètres de Core System > Configurations > Emplacement du répertoire temporaire. Le sous-répertoire se nomme adobeform_[nom_serveur].

>[!NOTE]
>
>Si vous utilisez un utilitaire de nettoyage des répertoires temporaires, sachez que si la suppression de ces répertoires n’affecte pas les fonctionnalités, elle peut affecter considérablement les performances pendant une courte période jusqu’à la création du nouveau cache. Pour éviter ce problème, ne supprimez pas ces répertoires lors de l’effacement du répertoire temporaire d’AEM forms.
