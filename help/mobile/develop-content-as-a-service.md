---
title: Remise de contenu
seo-title: Remise de contenu
description: 'null'
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Remise de contenu{#content-delivery}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les applications mobiles doivent pouvoir utiliser tout le contenu d’AEM en fonction des besoins pour diffuser l’expérience d’application ciblée.

Cela inclut l’utilisation des ressources, du contenu du site, du contenu CaaS (en direct) et du contenu personnalisé pouvant avoir sa propre structure.

>[!NOTE]
>
>**Le contenu** en direct peut provenir de l’une des fonctions ci-dessus via les gestionnaires ContentSync. Il peut être utilisé pour le traitement par lots du package et de la remise via zips, ainsi que pour la maintenance des mises à jour ou de ces packages.

Content Services fournit trois types principaux de documents :

1. **Assets**
1. **Contenu HTML compressé (HTML/CSS/JS)**
1. **Contenu indépendant du canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Assets {#assets}

Les collections de ressources sont des éléments AEM qui contiennent des références à d’autres collections.

Une collection de ressources peut être exposée via Content Services. L’appel d’une collection de ressources dans une requête renvoie un objet qui est une liste des ressources, y compris leurs URL. Les ressources sont accessibles via une URL. L’URL est fournie dans un objet. Par exemple :

* Une entité de page renvoie JSON (objet de page) qui inclut une référence à l’image. La référence d’image est une URL utilisée pour obtenir le binaire de ressources de l’image.
* Une demande de liste de ressources d’un dossier renvoie JSON avec des détails sur toutes les entités de ce dossier. Cette liste est un objet. Le fichier JSON contient des références URL qui sont utilisées pour obtenir le fichier binaire de chaque fichier de ce dossier.

### Optimisation des ressources {#asset-optimization}

L’une des principales valeurs de Content Services est la possibilité de renvoyer des fichiers optimisés pour le périphérique. Cela réduit les besoins de stockage local des périphériques et améliore les performances de l’application.

L’optimisation des ressources sera une fonction côté serveur, basée sur les informations fournies dans la demande d’API. Dans la mesure du possible, les rendus de ressource doivent être mis en cache de sorte que des requêtes similaires ne nécessitent pas une nouvelle génération du rendu de ressource.

### Workflow des ressources {#assets-workflow}

Le flux de travaux des ressources est le suivant :

1. Référence des ressources disponible dans AEM prêt à l’emploi
1. Créer une entité de référence d’élément à partir de son modèle
1. Modifier l&#39;entité

   1. Sélectionner un fichier ou une collection de fichiers
   1. Personnalisation du rendu JSON

Le diagramme suivant illustre le processus **de référence des** ressources :

![chlimage_1-155](assets/chlimage_1-155.png)

### Gestion des ressources {#managing-assets}

Content Services permet d’accéder aux ressources gérées AEM qui ne peuvent pas être référencées par d’autres contenus AEM.

#### Ressources gérées existantes {#existing-managed-assets}

Un utilisateur existant des sites et des ressources AEM utilise les ressources AEM pour gérer l’ensemble de son matériel numérique pour tous les canaux. Ils développent une application mobile native et doivent utiliser plusieurs ressources gérées par AEM Assets. Par exemple, logos, images d’arrière-plan, icônes de bouton, etc.

Actuellement, elles sont réparties dans le référentiel Ressources. Les fichiers que l’application doit référencer sont les suivants :

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Accès aux entités de ressources CS {#accessing-cs-asset-entities}

Mettons de côté les étapes de la façon dont la page est rendue disponible via l’API pour l’instant (elle sera couverte par la description de l’interface utilisateur d’AEM) et supposons qu’elle a été effectuée. Les entités de ressources ont été créées et ajoutées à l’espace &quot;appImages&quot;. D’autres dossiers ont été créés sous l’espace à des fins d’organisation. Les entités de ressources sont donc stockées dans le JCR AEM sous la forme suivante :

* /content/entités/appImages/logos/logo_light
* /content/entités/appImages/logos/logo_dark
* /content/entités/appImages/bkgnd/grey_blue
* /content/entités/appImages/icons/cart
* /content/entités/appImages/icons/home

#### Obtention d’une liste des entités de ressources disponibles {#getting-a-list-of-available-asset-entities}

Un développeur d’applications peut obtenir une liste des ressources disponibles en récupérant les entités de ressources. Le point de terminaison de l’espace Content Services peut fournir ces informations via le SDK de l’API du service Web.

Le résultat serait un objet au format JSON qui fournirait une liste des ressources du dossier &quot;icons&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obtention d’une image {#getting-an-image}

Le fichier JSON fournit une URL pour chaque image, générée par Content Services à l’image.

Pour obtenir le binaire de l’image &quot;panier&quot;, la bibliothèque cliente est de nouveau utilisée.

## Contenu HTML compressé {#packaged-html-content}

Le contenu HTML est nécessaire pour les clients qui doivent conserver la disposition du contenu. Cela s&#39;avère utile pour les applications natives qui utilisent un conteneur Web (comme une vue Web Cordova) pour afficher le contenu.

AEM Content Services pourra fournir du contenu HTML à l’application mobile via l’API. Les clients qui souhaitent exposer du contenu AEM au format HTML créeront une entité de page HTML pointant vers la source de contenu AEM.

Les options suivantes sont prises en compte :

* **** Fichier zip : Pour avoir les meilleures chances de s’afficher correctement sur le périphérique, tous les éléments référencés de la page - css, JavaScript, ressources, etc. - sera inclus dans un seul fichier compressé avec la réponse. Les références dans la page HTML seront ajustées pour utiliser un chemin relatif vers ces fichiers.
* **** Diffusion en continu : Obtention d’un manifeste des fichiers requis auprès d’AEM. Utilisez ensuite ce manifeste pour demander tous les fichiers (HTML, CSS, JS, etc.) avec les requêtes suivantes.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenu indépendant du canal {#channel-independent-content}

Le contenu indépendant du canal est un moyen d’exposer les éléments de contenu AEM - tels que les pages - sans se soucier de la disposition, des composants ou d’autres informations spécifiques au canal.

Ces entités de contenu sont générées à l’aide d’un modèle de contenu pour traduire les structures AEM au format JSON. Les données JSON résultantes contiennent des informations sur les données du contenu, qui sont découplées du référentiel AEM. Cela inclut le renvoi des métadonnées et des liens de référence AEM aux ressources, ainsi que les relations entre les structures de contenu - y compris la hiérarchie des entités.

### Gestion du contenu indépendant du canal {#managing-channel-independent-content}

Le contenu peut accéder à l’application de plusieurs manières.

1. Obtention de contenu ZIPS via AEM en direct

   * Les gestionnaires de synchronisation de contenu peuvent mettre à jour le package zip directement ou en appelant les rendus de contenu existants

      * Gestionnaires de plateformes
      * Gestionnaires AEMM
      * Gestionnaires personnalisés

1. Obtention de contenu directement via les rendus de contenu

   * Rendus Sling par défaut prêts à l’emploi
   * Rendu de contenu AEM Mobile/Content Services
   * Restiers personnalisés

