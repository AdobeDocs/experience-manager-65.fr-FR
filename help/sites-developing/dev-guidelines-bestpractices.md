---
title: Développement sur AEM – Conseils et bonnes pratiques
description: Conseils et bonnes pratiques pour le développement sur AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 100%

---

# Développement sur AEM – Conseils et bonnes pratiques{#aem-development-guidelines-and-best-practices}

## Consignes relatives à l’utilisation des modèles et des composants {#guidelines-for-using-templates-and-components}

Les composants et les modèles Adobe Experience Manager (AEM) se composent d’une boîte à outils puissante. Ils peuvent être utilisés par les développeurs et développeuses pour offrir aux utilisateurs et utilisatrices, aux éditeurs et éditrices, ainsi qu’aux administrateurs et administratrices de sites web la possibilité d’adapter leurs sites web aux besoins changeants de l’entreprise (agilité du contenu). Ils permettent en outre de conserver la disposition uniforme des sites (protection de la marque).

Il arrive souvent que la personne responsable d’un site web ou d’un ensemble de sites web (par exemple au niveau de la succursale d’une entreprise internationale) ait pour mission d’introduire un nouveau type de présentation de contenu dans les sites web.

Supposons qu’il soit nécessaire d’ajouter aux sites web une page de liste d’actualités, qui répertorie des extraits d’autres articles déjà publiés. La page doit avoir la même conception et la même structure que le reste du site web.

La méthode recommandée dans ces cas est la suivante :

* Réutilisez un modèle existant pour créer un type de page. Le modèle définit grossièrement la structure de la page (éléments de navigation, panneaux, etc.), qui est affinée par sa conception (CSS, graphiques).
* Utilisez le système de paragraphes (parsys/iparsys) sur les nouvelles pages.
* Définissez le droit d’accès au mode Conception des systèmes de paragraphes, de sorte que seules les personnes autorisées (généralement l’administrateur ou l’administratrice) puissent les modifier.
* Définissez les composants autorisés dans le système de paragraphes donné afin que les éditeurs et éditrices puissent ensuite placer les composants requis sur la page. Dans ce cas, il peut s’agir d’un composant de liste, qui peut parcourir une sous-arborescence de pages et extraire les informations en fonction de règles prédéfinies.
* Les éditeurs et éditrices ajoutent et configurent les composants autorisés sur les pages dont ils ou elles sont responsables, afin de fournir les fonctionnalités (informations) demandées à l’entreprise.

Cette méthode illustre la manière dont cette approche permet aux utilisateurs et utilisatrices, ainsi qu’aux administrateurs et administratrices du site web de répondre rapidement aux besoins de l’entreprise, sans avoir à faire appel aux équipes de développement. Les autres méthodes, comme la création d’un modèle, sont généralement un exercice coûteux qui nécessite un processus de gestion du changement et la participation de l’équipe de développement. Dans ce cas, le processus entier est plus long et coûteux.

Les développeurs et développeuses de systèmes basés sur AEM doivent donc utiliser :

* des modèles et contrôle d’accès à la conception de système de paragraphes pour l’uniformité et la protection de la marque ;
* un système de paragraphes, y compris ses options de configuration, pour plus de flexibilité.

Dans la plupart des projets courants, les règles générales suivantes s’appliquent aux développeurs et développeuses :

* Optez pour un nombre de modèles peu élevé, aussi peu élevé que le nombre de structures de pages fondamentalement différentes sur les sites web.
* Fournissez la flexibilité et les fonctionnalités de configuration nécessaires à vos composants personnalisés.
* Optimisez l’utilisation de la puissance et de la flexibilité du système de paragraphes AEM grâce aux composants parsys et iparsys.

### Personnalisation des composants et autres éléments {#customizing-components-and-other-elements}

Lors de la création de vos propres composants ou de la personnalisation d’un composant existant, il est souvent plus facile (et plus sûr) de réutiliser des définitions existantes. Ces principes s’appliquent également à d’autres éléments dans AEM, par exemple le gestionnaire d’erreurs.

Cela peut être effectué en copiant et en remplaçant la définition existante. En d’autres termes, en copiant la définition de `/libs` vers `/apps/<your-project>`. Cette nouvelle définition, dans `/apps`, peut être mise à jour en fonction de vos besoins.

>[!NOTE]
>
>Voir [Utilisation des incrustations](/help/sites-developing/overlays.md) pour plus d’informations.

Par exemple :

* [Personnalisation d’un composant](/help/sites-developing/components.md)

  Cette procédure suppose de superposer une définition de composant :

   * Créez un dossier de composants dans `/apps/<website-name>/components/<MyComponent>` en copiant un composant existant :

      * Par exemple, pour personnaliser le composant Texte, copiez :

         * de `/libs/foundation/components/text`
         * vers `/apps/myProject/components/text`

* [Personnalisation des pages affichées par le gestionnaire d’erreurs](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Ce cas implique le recouvrement d’un servlet :

   * Dans le référentiel, copiez un ou plusieurs scripts par défaut :

      * de `/libs/sling/servlet/errorhandler/`
      * vers `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**Ne modifiez rien** dans le chemin d’accès `/libs`.
>
>Cela est dû au fait que le contenu du `/libs` sera remplacé lors de la prochaine mise à niveau de votre instance (et peut être remplacé lorsque vous appliquez un correctif ou un pack de fonctionnalités).
>
>Pour la configuration et les autres modifications :
>
>1. copiez l’élément de `/libs` vers `/apps` ;
>1. apportez les modifications désirées dans `/apps`.

## Quand utiliser les requêtes JCR et quand ne pas les utiliser {#when-to-use-jcr-queries-and-when-not-to-use-them}

Lorsqu’elles sont utilisées correctement, les requêtes JCR sont un puissant outil. Elles sont adaptées pour :

* les requêtes réelles de l’utilisateur final ou de l’utilisatrice finale, telles que les recherches de texte intégral sur le contenu ;
* les cas où du contenu structuré est recherché dans l’ensemble du référentiel.

  Dans ce cas, assurez-vous que les requêtes ne s’exécutent que si nécessaire. Par exemple, lors de l’activation des composants ou de l’invalidation du cache (par opposition, par exemple, aux étapes des workflows, aux gestionnaires d’événements qui se déclenchent lors des modifications de contenu et aux filtres).

N’utilisez jamais de requêtes JCR pour les requêtes de rendu pures. Par exemple, les requêtes JCR ne sont pas adaptées pour :

* le rendu de navigation ;
* la création d’une présentation des « 10 derniers éléments d’actualité les plus récents » ;
* l’affichage des nombres d’éléments de contenu.

Pour le rendu du contenu, utilisez l’accès de navigation à l’arborescence de contenu au lieu d’effectuer une requête JCR.

>[!NOTE]
>
>Si vous utilisez le [Query Builder](/help/sites-developing/querybuilder-api.md), vous utilisez des requêtes JCR, car le Query Builder génère des requêtes JCR en arrière-plan.
>

## Considérations relatives à la sécurité {#security-considerations}

>[!NOTE]
>
>Il est également recommandé de se reporter à la [liste de contrôle de sécurité](/help/sites-administering/security-checklist.md).

### Sessions JCR (référentiel) {#jcr-repository-sessions}

Utilisez la session utilisateur, et non la session d’administration. Cela signifie que vous devez utiliser :

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### la fonctionnalité Protection contre les failles cross-site scripting (XSS) {#protect-against-cross-site-scripting-xss}

Les scripts de site à site (XSS) permettent aux pirates d’injecter du code dans des pages web consultées par d’autres utilisateurs. Cette vulnérabilité de sécurité peut être exploitée par des utilisateurs et utilisatrices web malveillants pour contourner les contrôles d’accès.

AEM applique le principe de filtrage de tout le contenu fourni par l’utilisateur ou l’utilisatrice en sortie. La prévention contre les failles XSS se voit accorder la priorité la plus élevée lors des phases de développement et de test.

En outre, un pare-feu d’application web, tel que le [mod_security pour Apache](https://modsecurity.org), peut fournir un contrôle centralisé fiable sur la sécurité de l’environnement de déploiement, ainsi qu’une protection contre les attaques XSS qui n’étaient pas détectées précédemment.

>[!CAUTION]
>
>L’exemple de code fourni avec AEM peut ne pas protéger contre de telles attaques et repose généralement sur le filtrage des requêtes par un pare-feu d’application web.

L’aide-mémoire de l’API XSS contient les informations que vous devez connaître pour utiliser l’API XSS et renforcer la sécurité d’une application AEM. Vous pouvez la télécharger ici :

Aide-mémoire de l’API XSS.

[Obtenir le fichier](assets/xss_cheat_sheet_2016.pdf)

### Sécurisation de la communication pour des informations confidentielles {#securing-communication-for-confidential-information}

Pour toute application Internet, assurez-vous que lors de la transmission d’informations confidentielles :

* le trafic est sécurisé via SSL ;
* HTTP POST est utilisé, le cas échéant.

Cela s’applique aux informations confidentielles sur le système (telles que la configuration ou l’accès administratif) et aux informations confidentielles pour ses utilisateurs et utilisatrices (comme leurs informations personnelles).

## Tâches de développement distinctes {#distinct-development-tasks}

### Personnalisation des pages d’erreur {#customizing-error-pages}

Les pages d’erreur peuvent être personnalisées pour AEM. La personnalisation est recommandée afin que l’instance ne révèle pas de traces sling sur les erreurs du serveur interne.

Pour plus d’informations, consultez [Personnalisation des pages d’erreur affichées par le gestionnaire d’erreurs](/help/sites-developing/customizing-errorhandler-pages.md).

### Ouvrir les fichiers dans le processus Java™ {#open-files-in-the-java-process}

Étant donné qu’AEM peut accéder à de nombreux fichiers, il est recommandé que le nombre de [fichiers ouverts pour un processus Java™](/help/sites-deploying/configuring.md#open-files-in-the-java-process) soit configuré explicitement pour AEM.

Pour minimiser ce problème, vous devriez vous assurer lors du développement que tout fichier ouvert est correctement fermé dès que possible (de manière raisonnable).
