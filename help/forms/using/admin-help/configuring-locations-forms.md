---
title: Configuration des emplacements pour Forms
seo-title: Configuration des emplacements pour Forms
description: Découvrez comment configurer l’emplacement pour Forms.
seo-description: Découvrez comment configurer l’emplacement pour Forms.
uuid: ba35888b-492c-4678-890b-160b53e7d659
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3d2b7cfb-228c-4cc2-8fcd-d500f0010010
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Configuration des emplacements pour Forms {#configuring-locations-for-forms}

Vous pouvez indiquer les emplacements URL, URI et fichier des attributs, tels que la racine Web, l’emplacement des formulaires à récupérer et le fichier PDF initial utilisé dans les transformations PDFForm et l’emplacement du cache.

1. Dans Administration Console, cliquez sur Services > Forms.
1. Sous Emplacements, définissez les options appropriées. Les options sont décrites ci-dessous.
1. Cliquez sur Enregistrer.

## Paramètres des emplacements {#locations-settings}

**URL de base :** URL de base où se trouvent les ressources du formulaire, telles que les images et les scripts. Cette valeur est nécessaire pour les transformations HTML incluant des références HREF à des dépendances externes, telles que des images ou des scripts. Un tel script est xfasubset.js, requis pour que les formulaires HTML exécutent les fonctions intelligentes XFA. Cette valeur doit être l’équivalent HTTP de l’URI racine du contenu.

>[!NOTE]
>
>l’URL de base ne prend en charge que les protocoles HTTP ou référentiels. Elle ne prend pas en charge les protocoles tels que file:///. Si vous devez accéder à une ressource telle qu’une feuille de style en cascade personnalisée ou un URI de signature numérique, utilisez la valeur du paramètre API appropriée pour spécifier l’emplacement absolu.

Quand le chemin d’accès d’une dépendance est absolu, la valeur de l’URL de base est ignorée. Sinon, le chemin d’accès de la dépendance est combiné avec l’URL de base.

La valeur par défaut est une chaîne vide.

L’exemple suivant pointe vers le même contenu (en utilisant l’URI racine du contenu et l’URL de base) :

`(ContentRootURI)/subdir/image1.jpg`

`(BaseURL)/subdir/image1.jpg`

**URI racine Web FS :** URL de l’application Web Forms. Vous pouvez laisser ce champ vide si l’application Web de Forms et l’application cliente sont déployées sur le même serveur d’applications ; l’URL racine Web de l’API de Forms est utilisée.

Si l’application Web de Forms et l’application cliente ne sont pas déployées sur le même serveur d’applications, vous devez indiquer l’URL de l’application Web de Forms dans ce champ, comme indiqué dans l’exemple qui suit :

`https://<host name>:<port>/FormServer`

Where `host name`and `port` are the server name and port number of the server that is hosting the Forms web application.

La valeur par défaut est une chaîne vide.

**URI racine Web :** racine Web de l’application. Cette valeur est combinée avec le paramètre sTargetURL (lorsque sTargetURL est fourni en tant que valeur relative), indiqué via le SDK d’AEM forms, pour construire une URL absolue et accéder ainsi au contenu Web spécifique de l’application.

La valeur par défaut est une chaîne vide.

**URI racine du contenu :** URI ou emplacement absolu à partir duquel les formulaires sont récupérés. Cette valeur est combinée avec le paramètre sFormQuery, indiqué via l’API, pour construire l’URL absolue vers le formulaire à récupérer. Cette valeur peut faire référence à un répertoire ou à un emplacement Web accessible par HTTP.

La valeur par défaut est une chaîne vide.

**URI de configuration XCI :** Emplacement relatif ou absolu dans lequel le fichier XCI utilisé pour le rendu est trouvé. Si la valeur est relative, il est supposé que le fichier XCI réside dans le fichier EAR déployable d’AEM forms.

La valeur par défaut est `com/adobe/formServer/PA/pa.xci`.

**URI de mappage de polices :** Emplacement relatif ou absolu du fichier de mappage des polices. Si la valeur est relative, il est supposé que ce fichier réside dans le fichier EAR déployable d’AEM forms.

Le fichier de mappage de polices est utilisé pour créer des mappages de polices personnalisés pour les transformations HTML dans Forms, ce qui permet d’indiquer la police qui sera remplacée lorsqu’une police n’est pas disponible sur l’ordinateur du client.

La valeur par défaut est `com/adobe/formServer/client-font-map.properties`.

L’exemple suivant présente une entrée dans le fichier de mappage de polices :

`Arial=Arial,Helvetica,sans-serif`

**Fichier PDF initial :** Fichier PDF initial utilisé dans une transformation PDFForm pour optimiser les  de. Le fichier PDF initial indique un fichier PDF personnalisé (qui ne contient que des ressources de flux XFA, d’image et de police) qui est ajouté à la conception et aux données du formulaire. Le formulaire est rendu par Acrobat (version 7 ou ultérieure) et s’applique à la transformation PDFForm.

La valeur par défaut est une chaîne vide.

**Emplacement du cache :** Indique l’emplacement du cache disque de Forms. Lorsque ce paramètre est modifié, toutes les informations concernant le cache de l’emplacement courant sont réinitialisées et un nouveau cache est créé dans le nouveau répertoire. Sélectionnez l’une des options suivantes :

**Emplacement par défaut :** Il s’agit de la sélection par défaut. Lorsque cette option est sélectionnée, le cache est créé à un emplacement différent selon le serveur d’applications utilisé :

* **JBoss :** Accueil [JBoss]\server\[type d’installation]\svcdata\FormServer\Cache
* **WebLogic :** Accueil [WebLogic]\user_projects\domains\[nom de domaine aem-forms]\adobe\[nom du serveur de formulaires]\FormServer\Cache
* **WebSphere :** Accueil [IBM]\WebSphere\AppServer\installedApps\adobe\server1\FormServer\Cache

**Répertoire temporaire LC :** Le cache est créé dans un sous-répertoire du répertoire temporaire d’AEM forms, qui est spécifié dans Administration Console sous Paramètres > Paramètres de Core System > Configurations > Emplacement du répertoire temporaire. The subdirectory is named adobeform_[servername].

>[!NOTE]
>
>si vous utilisez un utilitaire de nettoyage des répertoires temporaires, sachez que si la suppression de ces répertoires n’affecte pas les fonctionnalités, elle réduit considérablement les performances pendant une courte période, jusqu’à ce que le nouveau cache soit reconstitué. Pour éviter ce problème, ne supprimez pas ces répertoires lorsque vous videz le répertoire temporaire d’AEM forms.

