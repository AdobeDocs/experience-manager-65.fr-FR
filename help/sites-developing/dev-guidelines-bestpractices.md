---
title: Développement sur AEM – Conseils et bonnes pratiques
seo-title: AEM Development - Guidelines and Best Practices
description: Conseils et meilleures pratiques pour développer sur AEM.
seo-description: Guidelines and best practices for developing on AEM
uuid: a67de085-4441-4a1d-bec3-2f27892a67ff
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: b4cf0ffc-973a-473b-80c8-7f530d111435
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 100%

---

# Développement sur AEM – Conseils et bonnes pratiques{#aem-development-guidelines-and-best-practices}

## Conseils pour l’utilisation des modèles et des composants {#guidelines-for-using-templates-and-components}

Les composants et les modèles AEM représentent un ensemble d’outils très puissants. Ils peuvent être utilisés par les développeurs afin de fournir aux utilisateurs, éditeurs et administrateurs de sites web la capacité d’adapter leurs sites web en fonction de l’évolution des besoins de l’entreprise (agilité du contenu) tout en conservant la mise en page uniforme des sites (protection de la marque).

Pour une personne chargée d’un site web ou d’un ensemble de sites web (par exemple, dans une succursale d’une entreprise globale), il est souvent difficile d’introduire un nouveau type de présentation de contenu sur sess sites web.

Supposons qu’il soit nécessaire d’ajouter sur les sites web une page de liste d’actualités qui répertorie des extraits d’autres articles déjà publiés. La page doit avoir la même conception et structure que le reste du site web.

La méthode recommandée pour y arriver consiste à :

* réutiliser un modèle existant pour créer un type de page ; Le modèle définit la structure de page dans les grandes lignes (éléments de navigation, volets, etc.), qui est ensuite peaufinée par sa conception (CSS, graphismes).
* utiliser le système de paragraphe (parsys/iparsys) sur les nouvelles pages.
* Définissez le droit d’accès au mode Création des systèmes de paragraphe, afin que seules les personnes autorisées (généralement l’administrateur) puissent les modifier.
* Définissez les composants autorisés dans le système de paragraphe donné afin que les éditeurs puissent ensuite définir les composants requis sur la page. Dans notre exemple, il peut s’agir d’un composant de liste, qui peut parcourir une sous-arborescence de pages et extraire des informations selon des règles prédéfinies.
* Les éditeurs ajoutent et configurent les composants autorisés, sur les pages dont ils ont la charge, afin de fournir la fonctionnalité demandée (information) à l’entreprise.

Cela illustre comment cette approche permet aux administrateurs et aux utilisateurs contribuant au site web de répondre aux besoins de leur entreprise rapidement, sans impliquer les équipes de développement. Les méthodes alternatives, telles que la création d’un modèle, sont généralement coûteuses, car elles requièrent un processus de gestion de modification et la participation de l’équipe de développement. Cela rend le processus beaucoup plus long et coûteux.

Les développeurs des systèmes basés sur AEM doivent donc utiliser :

* des modèles et le contrôle d’accès à la conception de système de paragraphe pour assurer l’uniformité et protéger la marque ;
* le système de paragraphe, y compris ses options de configuration pour plus de souplesse.

Les règles générales suivantes sont pertinentes pour les développeurs dans la majorité des projets habituels :

* Garder un petit nombre de modèles, correspondant au nombre de structures de pages fondamentalement différentes sur les sites web.
* Fournir la souplesse et les capacités de configuration requises à vos composants personnalisés.
* Optimiser l’usage de la puissance et de la souplesse du système de paragraphe AEM : les composants parsys et iparsys.

### Personnalisation des composants et d’autres éléments {#customizing-components-and-other-elements}

Lors de la création de vos propres composants ou de la personnalisation d’un composant existant, il est souvent plus simple (et plus sûr) de recycler les définitions existantes. Les mêmes principes s’appliquent également à d’autres éléments dans AEM, par exemple le gestionnaire d’erreurs.

Cela peut être effectué en copiant et en remplaçant la définition existante. En d’autres termes, en copiant la définition de `/libs` vers `/apps/<your-project>`. Cette nouvelle définition, dans `/apps`, peut être mise à jour en fonction de vos besoins.

>[!NOTE]
>
>Voir [Utilisation des recouvrements](/help/sites-developing/overlays.md) pour plus de détails.

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


## Quand utiliser ou non les requêtes JCR {#when-to-use-jcr-queries-and-when-not-to-use-them}

Lorsqu’elles sont utilisées correctement, les requêtes JCR sont un puissant outil. Elles conviennent aux :

* requêtes des utilisateurs finaux, telles que les recherches en texte intégral sur le contenu ;
* les occasions où le contenu structuré doit pouvoir être recherché sur le référentiel entier.

   Dans de tels cas, assurez-vous que les requêtes ne s’exécutent que lorsqu’elles sont absolument nécessaires, par exemple, lors de l’activation d’un composant ou de l’invalidation du cache (par opposition, par exemple, aux étapes de workflows, aux gestionnaires d’événement qui se déclenchent lors des modifications de contenu, aux filtres, etc.).

Les requêtes JCR ne devraient jamais être employées pour des requêtes de rendu pures. Par exemple, les requêtes JCR ne sont pas utiles pour :

* le rendu de navigation ;
* la création d’un aperçu des dix actualités les plus récentes ;
* l’affichage des nombres d’éléments de contenu.

Pour effectuer le rendu du contenu, utilisez l’accès de navigation à l’arborescence de contenu au lieu d’effectuer une requête JCR.

>[!NOTE]
>
>Si vous utilisez [Query Builder](/help/sites-developing/querybuilder-api.md), vous utilisez des requêtes JCR, car Query Builder génère des requêtes JCR en interne.

## Considérations relatives à la sécurité {#security-considerations}

>[!NOTE]
>
>Il est également recommandé de se reporter à la [liste de contrôle de sécurité](/help/sites-administering/security-checklist.md).

### Sessions (de référentiel) JCR {#jcr-repository-sessions}

Vous devez utiliser la session utilisateur, et non la session administrative. Cela signifie que vous devriez utiliser :

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protection contre les scripts de site à site (XSS) {#protect-against-cross-site-scripting-xss}

Les scripts de site à site (XSS) permettent aux pirates d’injecter du code dans des pages web consultées par d’autres utilisateurs. Cette faille de sécurité peut être exploitée par des internautes malveillants pour contourner les contrôles d’accès.

AEM applique le principe de filtrage de l’ensemble du contenu fourni par l’utilisateur lors de la sortie. La prévention du script intersite (XSS) se voit accorder la priorité la plus élevée lors des phases de développement et de test.

En outre, un pare-feu d’application Web, tel que [mod_security pour Apache](https://modsecurity.org), peut fournir un contrôle centralisé fiable sur la sécurité de l’environnement de déploiement, ainsi qu’une protection contre les attaques XSS qui n’étaient pas détectées précédemment.

>[!CAUTION]
>
>L’exemple de code fourni avec AEM peut ne pas protéger contre de telles attaques et repose généralement sur le filtrage des requêtes par un pare-feu pour applications web.

L’aide-mémoire de l’API XSS contient les informations dont vous avez besoin pour utiliser l’API XSS et renforcer la sécurité d’une application AEM. Vous pouvez le télécharger ici :

L’aide-mémoire de l’API XSS.

[Obtenir le fichier](assets/xss_cheat_sheet_2016.pdf)

### Sécurisation de la communication pour des informations confidentielles {#securing-communication-for-confidential-information}

Comme pour toute application Internet, lors du transport d’informations confidentielles, vérifiez que :

* le trafic est sécurisé via SSL ;
* HTTP POST est utilisé, le cas échéant.

Cela s’applique aux informations confidentielles au sein du système (comme la configuration ou l’accès administrateur), ainsi qu’aux informations confidentielles pour ses utilisateurs (comme leurs détails personnels).

## Tâches distinctes de développement {#distinct-development-tasks}

### Personnalisation des pages d’erreur {#customizing-error-pages}

Les pages d’erreur peuvent être personnalisées pour AEM. Cela est recommandé de sorte que l’instance ne révèle pas de traces Sling sur les erreurs de serveur interne.

Voir [Personnalisation des pages d’erreur affichées par le gestionnaire d’erreur](/help/sites-developing/customizing-errorhandler-pages.md) pour plus de détails.

### Fichiers ouverts dans le processus Java {#open-files-in-the-java-process}

Étant donné qu’AEM peut accéder à un grand nombre de fichiers, il est recommandé que le nombre de [fichiers ouverts pour un processus Java](/help/sites-deploying/configuring.md#open-files-in-the-java-process) soit configuré explicitement pour AEM.

Pour minimiser ce problème, vous devriez vous assurer lors du développement que tout fichier ouvert est correctement fermé dès que possible (de manière raisonnable).
