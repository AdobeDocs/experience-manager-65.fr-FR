---
title: Configurations et navigateur de configuration
description: Comprendre AEM configurations et comment elles gèrent les paramètres de l'espace de travail dans AEM.
translation-type: tm+mt
source-git-commit: 8f5159d92f64b218d9e2e72d119e6de9d3e01ce6
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 2%

---


# Configurations et navigateur de configuration {#configuration-browser}

Les configurations AEM permettent de gérer les paramètres dans AEM et servent d&#39;espaces de travail.

## Qu’est-ce qu’une configuration ? {#what-is-a-configuration}

Une configuration peut être considérée sous deux angles différents.

* [Un administrateur](#configurations-administrator) utilise des configurations en tant qu’espaces de travail dans AEM pour définir et gérer des groupes de paramètres.
* [Un développeur](#configurations-developer) utilise le mécanisme de configuration sous-jacent qui implémente les configurations pour conserver et rechercher les paramètres dans AEM.

En résumé : du point de vue d&#39;un administrateur, les configurations sont la façon dont vous créez des espaces de travail pour gérer les paramètres dans AEM, tandis que le développeur doit comprendre comment AEM utilise et gère ces configurations dans le référentiel.

Quelle que soit votre perspective, les configurations répondent à deux objectifs principaux en AEM :

* Les configurations activent certaines fonctionnalités pour certains groupes d’utilisateurs.
* Les configurations définissent les droits d’accès pour ces fonctionnalités.

## Configurations en tant qu’administrateur {#configurations-administrator}

L’administrateur AEM ainsi que les auteurs peuvent considérer les configurations comme des espaces de travail. Ces espaces de travail peuvent être utilisés pour rassembler des groupes de paramètres ainsi que leur contenu associé à des fins d’organisation en implémentant des droits d’accès pour ces fonctionnalités.

Des configurations peuvent être créées pour de nombreuses fonctionnalités différentes dans AEM.

* [Configurations de cloud](/help/sites-administering/configurations.md)
* [Segments Context Hub](/help/sites-administering/segmentation.md)
* [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)
* [Modèles modifiables](/help/sites-authoring/templates.md)

### Exemple {#administrator-example}

Par exemple, un administrateur peut créer deux configurations pour les modèles modifiables.

* WKND-General
* WKND-Magazine

L’administrateur peut alors créer des modèles de page généraux à l’aide de la configuration WKND-General, puis des modèles spécifiques au magazine sous WKND-Magazine.

L&#39;administrateur peut alors associer le WKND-General à tout le contenu du site WKND. Cependant, la configuration WKND-Magazine ne serait associée qu&#39;au site du magazine.

En procédant comme suit :

* Lorsqu’un auteur de contenu crée une nouvelle page pour le magazine, il peut choisir entre des modèles généraux (WKND-General) ou des modèles de magazine (WKND-Magazine).
* Lorsqu’un auteur de contenu crée une nouvelle page pour une autre partie du site qui n’est pas le magazine, il peut uniquement choisir parmi les modèles généraux (WKND-General).

Des configurations similaires sont possibles non seulement pour les modèles modifiables, mais également pour les configurations de cloud, les segments ContextHub et les modèles de fragments de contenu.

### Utilisation de l’explorateur de configurations {#using-configuration-browser}

Le navigateur de configuration permet à un administrateur de créer, gérer et configurer facilement des droits d’accès aux configurations dans AEM.

>[!NOTE]
>
>Il n’est possible de créer des configurations à l’aide de l’explorateur de configuration que si votre utilisateur dispose de `admin` droits. `admin` des droits sont également requis pour attribuer des droits d&#39;accès à la configuration ou pour modifier une configuration.

#### Creating a Configuration {#creating-a-configuration}

Il est très simple de créer une nouvelle configuration dans AEM en utilisant le navigateur de configuration.

1. Connectez-vous à AEM en tant que Cloud Service et dans le menu principal, sélectionnez **Outils** -> **Général** -> **Configuration Navigateur**.
1. Appuyez ou cliquez sur **Créer**.
1. Indiquez un **titre** et un **nom** pour votre configuration.

   ![Création d’une configuration](assets/configuration-create.png)

   * Le **titre** doit être descriptif.
   * Le **nom** deviendra le nom du noeud dans le référentiel.
      * Elle sera générée automatiquement en fonction du titre et ajustée en fonction des conventions de dénomination [AEM.](/help/sites-developing/naming-conventions.md)
      * Il peut être ajusté si nécessaire.
1. Vérifiez le type de configuration que vous souhaitez autoriser.
   * [Configurations de cloud](/help/sites-administering/configurations.md)
   * [Segments Context Hub](/help/sites-administering/segmentation.md)
   * [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)
   * [Modèles modifiables](/help/sites-authoring/templates.md)
1. Appuyez ou cliquez sur **Créer**.

>[!TIP]
>
>Les configurations peuvent être imbriquées.

#### Modification des configurations et de leurs droits d’accès {#access-rights}

Si vous considérez les configurations comme des espaces de travail, les droits d&#39;accès peuvent être définis sur ces configurations afin de forcer qui peut accéder à ces espaces de travail ou qui ne peut pas y accéder.

1. Connectez-vous à AEM en tant que Cloud Service et dans le menu principal, sélectionnez **Outils** -> **Général** -> **Configuration Navigateur**.
1. Sélectionnez la configuration à modifier, puis appuyez ou cliquez sur **Propriétés** dans la barre d&#39;outils.
1. Sélectionnez les fonctionnalités supplémentaires que vous souhaitez ajouter à la configuration.
   >[!NOTE]
   >
   >Il n&#39;est pas possible de désélectionner une fonction une fois la configuration créée.
1. Utilisez le bouton Autorisations **** effectives pour vue d&#39;une matrice de rôles et des autorisations qui leur sont actuellement attribuées pour les configurations.
   ![Fenêtre d&#39;autorisations efficaces](assets/configuration-effective-permissions.png)
1. Pour attribuer de nouvelles autorisations, saisissez le nom de l’utilisateur ou du groupe dans le champ **Sélectionner un utilisateur ou un groupe** de la section **Ajouter de nouvelles autorisations** .
   * Les offres de champ **Sélectionner un utilisateur ou un groupe** sont automatiquement renseignées en fonction des utilisateurs et rôles existants.
1. Sélectionnez l’utilisateur ou le rôle approprié dans les résultats de saisie semi-automatique.
   * Vous pouvez sélectionner plusieurs utilisateurs ou rôles.
1. Vérifiez les options d’accès que les utilisateurs ou rôles sélectionnés doivent avoir et cliquez sur **Ajouter**.
   ![Ajouter les droits d’accès à une configuration](assets/configuration-edit.png)
1. Répétez les étapes pour sélectionner des utilisateurs ou des rôles et attribuer des droits d’accès supplémentaires si nécessaire.
1. Appuyez ou cliquez sur **Enregistrer et fermer** lorsque vous avez terminé.

## Configurations en tant que développeur {#configurations-developer}

En tant que développeur, il est important de savoir comment AEM en tant que Cloud Service fonctionne avec les configurations et comment il traite la résolution de configuration.

### Séparation de la configuration et du contenu {#separation-of-config-and-content}

Bien que l’ [administrateur et les utilisateurs puissent considérer les configurations comme des lieux de travail](#configurations-administrator) pour gérer différents paramètres et contenus, il est important de comprendre que les configurations et le contenu sont stockés et gérés séparément par AEM dans le référentiel.

* `/content` est l’accueil de tout le contenu.
* `/conf` est la base de toutes les configurations.

Le contenu référence sa configuration associée par le biais d’une `cq:conf` propriété. aem effectue une recherche basée sur le contenu et sa `cq:conf` propriété contextuelle permet de trouver la configuration appropriée.

### Exemple {#developer-example}

Dans cet exemple, supposons que vous ayez un code d&#39;application qui s&#39;intéresse aux paramètres DAM.

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

Le point de départ de toute recherche de configuration est une ressource de contenu, généralement quelque part sous `/content`. Il peut s’agir d’une page, d’un composant au sein d’une page, d’un fichier ou d’un dossier DAM. Il s&#39;agit du contenu réel pour lequel nous recherchons la configuration appropriée qui s&#39;applique dans ce contexte.

Maintenant, avec l&#39; `Conf` objet en main, nous pouvons récupérer l&#39;élément de configuration spécifique qui nous intéresse. Dans ce cas, il s’agit `dam/imageserver`d’un ensemble de paramètres liés au `imageserver`. L&#39; `getItem` appel renvoie une `ValueMap`valeur. Nous lisons ensuite une propriété `bgkcolor` string et fournissons une valeur par défaut de &quot;FFFFF&quot; au cas où la propriété (ou l&#39;élément de configuration complet) n&#39;existerait pas.

Examinons maintenant le contenu JCR correspondant :

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wkns
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

Dans cet exemple, nous supposons ici un dossier DAM spécifique à WKND et une configuration correspondante. En commençant par ce dossier `/content/dam/wknd`, nous verrons qu&#39;il existe une propriété string nommée `cq:conf` qui fait référence à la configuration qui doit s&#39;appliquer à la sous-arborescence. La propriété est généralement définie sur un dossier `jcr:content` de ressources ou une page. Ces `conf` liens sont explicites, il est donc facile de les suivre en regardant simplement le contenu dans CRXDE.

En entrant `/conf`, nous suivons la référence et voyons qu&#39;il y a un `/conf/wknd` noeud. Il s&#39;agit d&#39;une configuration. Veuillez noter que sa recherche est totalement transparente par rapport au code de la demande. L&#39;exemple de code n&#39;a jamais de référence dédiée, il est caché derrière l&#39; `Conf` objet. La configuration qui s’applique est entièrement contrôlée par le contenu JCR.

Nous voyons que la configuration contient un noeud de nom fixe `settings` qui contient les éléments réels, y compris le `dam/imageserver` dont nous avons besoin dans notre cas. Un tel article peut être considéré comme un &quot;document de paramètres&quot; et est généralement représenté par un `cq:Page` contenant un `jcr:content` contenu réel.

Enfin, nous voyons la propriété `bgkcolor` dont notre exemple de code a besoin. Le `ValueMap` dont nous retirons `getItem` est basé sur le `jcr:content` noeud de la page.

### Résolution de configuration {#configuration-resolution}

L&#39;exemple de base ci-dessus montrait une configuration unique. Mais il existe de nombreux cas où vous souhaitez avoir différentes configurations, comme une configuration globale par défaut, une configuration différente pour chaque marque et peut-être une configuration spécifique pour vos sous-projets.

Pour ce faire, la recherche de configuration dans AEM dispose d’un mécanisme d’héritage et de secours dans l’ordre de préférence suivant :

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * Configuration spécifique référencée depuis `cq:conf` quelque part dans `/content`
   * La hiérarchie est arbitraire et peut être conçue tout comme la structure de votre site. Ce n&#39;est pas l&#39;activité du code de l&#39;application de le savoir.
   * Modifiable au moment de l’exécution par les utilisateurs disposant de privilèges de configuration
1. `/conf/<siteconfig>/<parentconfig>`
   * Parcourir les parents pour les configurations de secours
   * Modifiable au moment de l’exécution par les utilisateurs disposant de privilèges de configuration
1. `/conf/<siteconfig>`
   * Parcourir les parents pour les configurations de secours
   * Modifiable au moment de l’exécution par les utilisateurs disposant de privilèges de configuration
1. `/conf/global`
   * Paramètres globaux du système
   * Valeurs par défaut généralement globales pour votre installation
   * Défini par un `admin` rôle
   * Modifiable au moment de l’exécution par les utilisateurs disposant de privilèges de configuration
1. `/apps`
   * Valeurs par défaut de l’application
   * Corrigé par le déploiement des applications
   * Lecture seule au moment de l’exécution
1. `/libs`
   * Paramètres par défaut AEM produit
   * Uniquement modifiable par Adobe, accès au projet non autorisé
   * Corrigé par le déploiement des applications
   * Lecture seule au moment de l’exécution

### Utilisation des configurations {#using-configurations}

Les configurations dans AEM sont basées sur les configurations Sling de prise en compte du contexte. Les lots Sling fournissent une API de service qui peut être utilisée pour obtenir des configurations contextuelles. Les configurations sensibles au contexte sont des configurations qui sont liées à une ressource de contenu ou à une arborescence de ressources, comme [décrit dans l&#39;exemple précédent.](#developer-example)

Pour plus d’informations sur les configurations basées sur le contexte, des exemples et la manière de les utiliser, [consultez la documentation Sling.](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### Console Web ConfMgr {#confmgr-web-console}

À des fins de débogage et de test, il existe une console Web **ConfMgr** à `https://<host>:<port>/system/console/conf`l’emplacement, qui peut afficher des configurations pour un chemin/élément donné.

![ConfMgr](assets/configuration-confmgr.png)

Fournissez simplement :

* **Chemin d’accès au contenu**
* **Item**
* **User**

Cliquez sur **Résoudre** pour voir quelles configurations sont résolues et recevoir un exemple de code qui résoudra ces configurations.

### Console Web de configuration adaptée au contexte {#context-aware-web-console}

À des fins de débogage et de test, il existe une console Web de configuration **** contextuelle à `https://<host>:<port>/system/console/slingcaconfig`l’adresse, qui permet d’interroger des configurations contextuelles dans le référentiel et d’afficher leurs propriétés.

![Console Web de configuration prenant en compte le contexte](assets/configuration-context-aware-console.png)

Fournissez simplement :

* **Chemin d’accès au contenu**
* **Nom de configuration**

Cliquez sur **Résoudre** pour récupérer les chemins et propriétés de contexte associés pour la configuration sélectionnée.
