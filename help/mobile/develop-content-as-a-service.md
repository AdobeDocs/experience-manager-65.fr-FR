---
title: Diffusion de contenu
seo-title: Diffusion de contenu
description: 'null'
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 3%

---


# Diffusion de contenu{#content-delivery}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Les applications mobiles doivent pouvoir utiliser tout le contenu de l’AEM en fonction des besoins pour diffuser l’expérience d’application ciblée.

Cela inclut l’utilisation de ressources, de contenu du site, de contenu d’application de la loi (en direct) et de contenu personnalisé pouvant avoir sa propre structure.

>[!NOTE]
>
>**Le** contenu en vol peut provenir de n’importe lequel des éléments ci-dessus via les gestionnaires ContentSync. Il peut être utilisé pour le traitement par lots des packages et de la diffusion via zips, ainsi que pour la maintenance des mises à jour ou de ces packages.

Content Services fournit trois types de matériel principaux :

1. **Ressources**
1. **Contenu HTML compressé (HTML/CSS/JS)**
1. **Contenu indépendant du canal**

![chlimage_1-154](assets/chlimage_1-154.png)

## Ressources {#assets}

Les collections de ressources sont des constructions AEM qui contiennent des références à d’autres collections.

Une collection de ressources peut être exposée via Content Services. L’appel d’une collection de ressources dans une requête renvoie un objet qui est une liste des ressources, y compris leurs URL. Les ressources sont accessibles via une URL. L’URL est fournie dans un objet. Par exemple :

* Une entité de page renvoie un objet JSON (objet de page) qui inclut une référence d’image. La référence d’image est une URL utilisée pour obtenir le fichier binaire de l’image.
* Une demande de liste de ressources dans un dossier renvoie un fichier JSON contenant des informations détaillées sur toutes les entités contenues dans ce dossier. Cette liste est un objet. Le fichier JSON contient des références URL qui sont utilisées pour obtenir le binaire de chaque fichier de ce dossier.

### Optimisation des ressources {#asset-optimization}

L’une des valeurs clés de Content Services est la possibilité de renvoyer des ressources optimisées pour le périphérique. Cela réduit les besoins d’enregistrement de périphérique local et améliore les performances de l’application.

L’optimisation des ressources sera une fonction côté serveur, basée sur les informations fournies dans la demande d’API. Dans la mesure du possible, les rendus de ressource doivent être mis en cache de sorte que des requêtes similaires ne nécessitent pas une nouvelle génération du rendu de ressource.

### Workflow des ressources {#assets-workflow}

Le processus des ressources est le suivant :

1. Référence des ressources disponible dans AEM prêt à l’emploi
1. Créer une entité de référence d&#39;élément en fonction de son modèle
1. Modifier l&#39;entité

   1. Sélectionner un fichier ou une collection de ressources
   1. Personnalisation du rendu JSON

Le diagramme suivant présente le **Workflow de référence des ressources** :

![chlimage_1-155](assets/chlimage_1-155.png)

### Gestion des ressources {#managing-assets}

Content Services permet d’accéder à AEM ressources gérées qui ne peuvent pas être référencées par le biais d’un autre contenu AEM.

#### Ressources gérées existantes {#existing-managed-assets}

Un utilisateur AEM Sites et Assets existant utilise AEM Assets pour gérer l’ensemble de son matériel numérique pour tous les canaux. Ils développent une application mobile native et doivent utiliser plusieurs ressources gérées par AEM Assets. Par exemple, logos, images d’arrière-plan, icônes de bouton, etc.

Actuellement, elles sont réparties dans le référentiel Ressources. Les fichiers que l’application doit référencer se trouvent dans :

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/grey_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### Accès aux entités de ressources CS {#accessing-cs-asset-entities}

Mettons de côté les étapes de mise à disposition de la page par le biais de l’API pour l’instant (elle sera couverte par la description de l’interface utilisateur AEM) et supposons qu’elle ait été effectuée. Les entités de ressources ont été créées et ajoutées à l’espace &quot;appImages&quot;. D’autres dossiers ont été créés sous l’espace à des fins d’organisation. Ainsi, les entités d’actifs sont stockées dans le JCR AEM comme suit :

* /content/entités/appImages/logos/logo_light
* /content/entités/appImages/logos/logo_dark
* /content/entités/appImages/bkgnd/grey_blue
* /content/entités/appImages/icons/panier
* /content/entités/appImages/icons/home

#### Obtention d&#39;une liste d&#39;entités de ressources disponibles {#getting-a-list-of-available-asset-entities}

Un développeur d’applications peut obtenir une liste des ressources disponibles en récupérant les entités de ressources. Le point de terminaison de l’espace Content Services peut fournir ces informations par le biais du SDK de l’API du service Web.

Il en résulterait un objet au format JSON qui fournirait une liste des ressources du dossier &quot;icons&quot;.

![chlimage_1-156](assets/chlimage_1-156.png)

#### Obtention d’une image {#getting-an-image}

Le fichier JSON fournit une URL pour chaque image, générée par Content Services à l’image.

Pour obtenir le binaire de l’image &quot;panier&quot;, la bibliothèque cliente est de nouveau utilisée.

## Contenu HTML compressé {#packaged-html-content}

Le contenu HTML est nécessaire pour les clients qui doivent conserver la disposition du contenu. Cela s&#39;avère utile pour les applications natives qui utilisent un conteneur Web (tel qu&#39;une vue Web Cordova), pour afficher le contenu.

AEM Content Services pourra fournir du contenu HTML à l’application mobile via l’API. Les clients qui souhaitent exposer AEM contenu au format HTML créent une entité de page HTML pointant vers la source de contenu AEM.

Les options suivantes sont prises en compte :

* **Fichier zip :** pour avoir la meilleure chance de s’afficher correctement sur le périphérique, tous les éléments référencés de la page - css, JavaScript, ressources, etc. - sera inclus dans un seul fichier compressé avec la réponse. Les références dans la page HTML seront ajustées pour utiliser un chemin relatif vers ces fichiers.
* **Diffusion en continu :** Obtention d’un manifeste des fichiers requis à partir de l’AEM. Ensuite, utilisez ce manifeste pour demander tous les fichiers (HTML, CSS, JS, etc.) avec les requêtes suivantes.

![chlimage_1-157](assets/chlimage_1-157.png)

## Contenu indépendant du canal {#channel-independent-content}

Le contenu indépendant du canal est un moyen d&#39;exposer les éléments de contenu AEM (tels que les pages) sans se soucier de la disposition, des composants ou d&#39;autres informations spécifiques au canal.

Ces entités de contenu sont générées à l’aide d’un modèle de contenu pour traduire les structures AEM en un format JSON. Les données JSON résultantes contiennent des informations sur les données du contenu, qui sont découplées du référentiel AEM. Cela inclut le renvoi de métadonnées et de liens de référence AEM aux ressources, ainsi que les relations entre les structures de contenu - y compris la hiérarchie des entités.

### Gestion du contenu indépendant du Canal {#managing-channel-independent-content}

Le contenu peut accéder à l’application de plusieurs manières.

1. ZIPS de contenu GET via AEM en vol

   * Les gestionnaires de synchronisation de contenu peuvent mettre à jour le package zip directement ou en appelant les rendus de contenu existants

      * Gestionnaires de plateformes
      * Gestionnaires AEMM
      * Gestionnaires personnalisés

1. GET du contenu directement via les rendus de contenu

   * Rendu Sling par défaut prêt à l’emploi
   * Rendu de contenu AEM Mobile/Content Services
   * Rendu personnalisés

