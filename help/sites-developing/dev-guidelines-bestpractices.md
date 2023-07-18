---
title: Développement sur AEM – Conseils et bonnes pratiques
seo-title: AEM Development - Guidelines and Best Practices
description: Conseils et bonnes pratiques pour le développement sur AEM
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 30%

---

# Développement sur AEM – Conseils et bonnes pratiques{#aem-development-guidelines-and-best-practices}

## Instructions relatives à l’utilisation des modèles et des composants {#guidelines-for-using-templates-and-components}

Les composants et les modèles AEM représentent un ensemble d’outils très puissants. Ils peuvent être utilisés par les développeurs pour offrir aux utilisateurs, éditeurs et administrateurs de sites web la possibilité d’adapter leurs sites web aux besoins changeants de l’entreprise (agilité du contenu) tout en conservant la disposition uniforme des sites (protection de la marque).

Un défi classique pour une personne responsable d’un site web, ou d’un ensemble de sites web (par exemple dans une succursale d’une entreprise globale), est d’introduire un nouveau type de présentation de contenu sur leurs sites web.

Supposons qu’il soit nécessaire d’ajouter une page de liste de discussion aux sites web, qui répertorie des extraits d’autres articles déjà publiés. La page doit avoir la même conception et la même structure que le reste du site web.

La méthode recommandée pour résoudre un tel problème serait la suivante :

* réutiliser un modèle existant pour créer un type de page ; Le modèle définit en gros la structure de la page (éléments de navigation, panneaux, etc.), qui est affinée par sa conception (CSS, graphiques).
* Utilisez le système de paragraphes (parsys/iparsys) sur les nouvelles pages.
* Définissez le droit d’accès au mode Conception des systèmes de paragraphes, de sorte que seules les personnes autorisées (généralement l’administrateur) puissent les modifier.
* Définissez les composants autorisés dans le système de paragraphes donné afin que les éditeurs puissent ensuite placer les composants requis sur la page. Dans notre cas, il peut s’agir d’un composant de liste, qui peut parcourir une sous-arborescence de pages et extraire les informations en fonction de règles prédéfinies.
* Les éditeurs ajoutent et configurent les composants autorisés, sur les pages dont ils sont responsables, pour fournir les fonctionnalités (informations) demandées à l’entreprise.

Cela illustre la manière dont cette approche permet aux utilisateurs et aux administrateurs du site web de répondre rapidement aux besoins de l’entreprise, sans avoir à faire appel aux équipes de développement. Les autres méthodes, telles que la création d’un modèle, sont généralement coûteuses, car elles nécessitent un processus de gestion du changement et la participation de l’équipe de développement. Cela rend le processus entier beaucoup plus long et coûteux.

Les développeurs de systèmes basés sur AEM doivent donc utiliser :

* modèles et contrôle d’accès à la conception de système de paragraphes pour l’uniformité et la protection de la marque
* système de paragraphes, y compris ses options de configuration pour plus de flexibilité.

Les règles générales suivantes s’appliquent aux développeurs dans la plupart des projets habituels :

* Maintenez le nombre de modèles bas, aussi bas que le nombre de structures de pages fondamentalement différentes sur les sites web.
* Fournissez la flexibilité et les fonctionnalités de configuration nécessaires à vos composants personnalisés.
* Optimisez l’utilisation de la puissance et de la flexibilité du système de paragraphes d’AEM : les composants parsys et iparsys.

### Personnalisation des composants et autres éléments {#customizing-components-and-other-elements}

Lors de la création de vos propres composants ou de la personnalisation d’un composant existant, il est souvent plus facile (et plus sûr) de réutiliser des définitions existantes. Les mêmes principes s’appliquent également à d’autres éléments dans AEM, par exemple le gestionnaire d’erreurs.

Cela peut être effectué en copiant et en remplaçant la définition existante. En d’autres termes, en copiant la définition de `/libs` vers `/apps/<your-project>`. Cette nouvelle définition, dans `/apps`, peut être mise à jour en fonction de vos besoins.

>[!NOTE]
>
>Voir [Utilisation des recouvrements](/help/sites-developing/overlays.md) pour plus d’informations.

Par exemple :

* [Personnalisation d’un composant](/help/sites-developing/components.md)

  Cette procédure suppose de superposer une définition de composant :

   * Créez un dossier de composants dans `/apps/<website-name>/components/<MyComponent>` en copiant un composant existant :

      * Par exemple, pour personnaliser le composant Texte, copiez :

         * de `/libs/foundation/components/text`
         * vers `/apps/myProject/components/text`

* [Personnalisation des pages affichées par le gestionnaire d’erreurs](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Ce cas implique le recouvrement d’un servlet :

   * Dans le référentiel, copiez le ou les scripts par défaut :

      * de `/libs/sling/servlet/errorhandler/`
      * vers `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>Vous **ne devez rien** modifier dans le chemin `/libs`.
>
>En effet, le contenu de `/libs` est remplacé dès que vous mettez à niveau votre instance (et risque de l’être si vous appliquez un correctif ou un pack de fonctionnalités).
>
>Pour la configuration et les autres modifications :
>
>1. copiez l’élément de `/libs` vers `/apps` ;
>1. apportez les modifications désirées dans `/apps`.

## Quand utiliser les requêtes JCR et quand ne pas les utiliser {#when-to-use-jcr-queries-and-when-not-to-use-them}

Lorsqu’elles sont utilisées correctement, les requêtes JCR sont un puissant outil. Elles sont adaptées aux éléments suivants :

* requêtes réelles de l’utilisateur final, telles que les recherches de texte intégral sur le contenu.
* les cas où du contenu structuré doit être trouvé dans l’ensemble du référentiel.

  Dans ce cas, assurez-vous que les requêtes ne s’exécutent que lorsque cela est absolument nécessaire, par exemple lors de l’activation ou de l’invalidation du composant (contrairement à, par exemple, les étapes des workflows, les gestionnaires d’événements qui se déclenchent lors des modifications de contenu, des filtres, etc.).

Les requêtes JCR ne doivent jamais être utilisées pour les requêtes de rendu pures. Par exemple, les requêtes JCR ne sont pas appropriées pour

* navigation du rendu
* création d’une présentation des &quot;10 derniers éléments d’actualité les plus récents&quot;
* l’affichage des nombres d’éléments de contenu.

Pour le rendu du contenu, utilisez l’accès de navigation à l’arborescence de contenu au lieu d’effectuer une requête JCR.

>[!NOTE]
>
>Si vous utilisez la variable [Query Builder](/help/sites-developing/querybuilder-api.md), vous utilisez des requêtes JCR, car Query Builder génère des requêtes JCR en arrière-plan.
>

## Considérations relatives à la sécurité {#security-considerations}

>[!NOTE]
>
>Il est également recommandé de se reporter à la [liste de contrôle de sécurité](/help/sites-administering/security-checklist.md).

### Sessions JCR (Repository) {#jcr-repository-sessions}

Vous devez utiliser la session utilisateur, et non la session d’administration. Cela signifie que vous devez utiliser :

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contre les scripts intersites (XSS) {#protect-against-cross-site-scripting-xss}

Les scripts de site à site (XSS) permettent aux pirates d’injecter du code dans des pages web consultées par d’autres utilisateurs. Cette vulnérabilité de sécurité peut être exploitée par des utilisateurs web malveillants pour contourner les contrôles d’accès.

AEM applique le principe de filtrage de tout le contenu fourni par l’utilisateur en sortie. La prévention de XSS est prioritaire lors des phases de développement et de test.

En outre, un pare-feu d’application Web, tel que [mod_security pour Apache](https://modsecurity.org), peut fournir un contrôle centralisé fiable sur la sécurité de l’environnement de déploiement, ainsi qu’une protection contre les attaques XSS qui n’étaient pas détectées précédemment.

>[!CAUTION]
>
>L’exemple de code fourni avec AEM peut ne pas être protégé contre de telles attaques et repose généralement sur le filtrage des requêtes par un pare-feu d’application web.

L’aide-mémoire de l’API XSS contient les informations dont vous avez besoin pour utiliser l’API XSS et renforcer la sécurité d’une application AEM. Vous pouvez le télécharger ici :

Aide-mémoire de XSSAPI.

[Obtenir le fichier](assets/xss_cheat_sheet_2016.pdf)

### Sécurisation de la communication pour des informations confidentielles {#securing-communication-for-confidential-information}

Pour toute application Internet, assurez-vous que lors du transport d’informations confidentielles

* le trafic est sécurisé via SSL
* POST HTTP, le cas échéant

Cela s’applique aux informations confidentielles du système (telles que la configuration ou l’accès administratif) ainsi qu’aux informations confidentielles de ses utilisateurs (telles que leurs informations personnelles).

## Tâches de développement distinctes {#distinct-development-tasks}

### Personnalisation des pages d’erreur {#customizing-error-pages}

Les pages d’erreur peuvent être personnalisées pour AEM. Ceci est recommandé afin que l’instance ne révèle pas de traces sling sur les erreurs du serveur interne.

Voir [Personnalisation des pages d’erreur affichées par le gestionnaire d’erreurs](/help/sites-developing/customizing-errorhandler-pages.md) pour plus d’informations.

### Ouvrir les fichiers dans le processus Java {#open-files-in-the-java-process}

Étant donné qu’AEM peut accéder à un grand nombre de fichiers, il est recommandé que le nombre de [fichiers ouverts pour un processus Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) soit configuré explicitement pour AEM.

Pour minimiser ce problème, vous devriez vous assurer lors du développement que tout fichier ouvert est correctement fermé dès que possible (de manière raisonnable).
