---
title: Développement sur AEM – Conseils et bonnes pratiques
description: Conseils et bonnes pratiques pour le développement sur AEM
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: 8eef7e4d-a6f2-4b87-a995-0761447283c6
source-git-commit: 4e2ee7da5424ac6677eaa2392de7803e7543d13c
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 13%

---

# Développement sur AEM – Conseils et bonnes pratiques{#aem-development-guidelines-and-best-practices}

## Consignes relatives à l’utilisation des modèles et des composants {#guidelines-for-using-templates-and-components}

Les composants et les modèles Adobe Experience Manager (AEM) se composent d’une boîte à outils puissante. Ils peuvent être utilisés par les développeurs pour offrir aux utilisateurs, éditeurs et administrateurs de sites web la possibilité d’adapter leurs sites web aux besoins changeants de l’entreprise (agilité du contenu). Tout cela tout en conservant la disposition uniforme des sites (protection de la marque).

Un défi classique pour une personne responsable d’un site web, ou d’un ensemble de sites web (par exemple dans une succursale d’une entreprise globale), est d’introduire un nouveau type de présentation de contenu sur leurs sites web.

Supposons qu’il soit nécessaire d’ajouter une page de liste de discussion aux sites web, qui répertorie des extraits d’autres articles déjà publiés. La page doit avoir la même conception et la même structure que le reste du site web.

La méthode recommandée pour résoudre un tel problème serait la suivante :

* Réutiliser un modèle existant pour créer un nouveau type de page. Le modèle définit en gros la structure de la page (éléments de navigation, panneaux, etc.), qui est affinée par sa conception (CSS, graphiques).
* Utilisez le système de paragraphes (parsys/iparsys) sur les nouvelles pages.
* Définissez le droit d’accès au mode Conception des systèmes de paragraphes, de sorte que seules les personnes autorisées (généralement l’administrateur) puissent les modifier.
* Définissez les composants autorisés dans le système de paragraphes donné afin que les éditeurs puissent ensuite placer les composants requis sur la page. Dans ce cas, il peut s’agir d’un composant de liste, qui peut parcourir une sous-arborescence de pages et extraire les informations en fonction de règles prédéfinies.
* Les éditeurs ajoutent et configurent les composants autorisés sur les pages dont ils sont responsables, afin de fournir les fonctionnalités (informations) demandées à l’entreprise.

Cela illustre la manière dont cette approche permet aux utilisateurs et aux administrateurs du site web de répondre rapidement aux besoins de l’entreprise, sans avoir à faire appel aux équipes de développement. Les autres méthodes, comme la création d’un modèle, sont généralement un exercice coûteux qui nécessite un processus de gestion du changement et la participation de l’équipe de développement. Cela rend le processus entier plus long et coûteux.

Les développeurs de systèmes basés sur AEM doivent donc utiliser :

* modèles et contrôle d’accès à la conception de système de paragraphes pour l’uniformité et la protection de la marque
* système de paragraphes, y compris ses options de configuration pour plus de flexibilité.

Dans la plupart des projets courants, les règles générales suivantes s’appliquent aux développeurs :

* Maintenez le nombre de modèles bas, aussi bas que le nombre de structures de pages fondamentalement différentes sur les sites web.
* Fournissez la flexibilité et les fonctionnalités de configuration nécessaires à vos composants personnalisés.
* Optimisez l’utilisation de la puissance et de la flexibilité du système de paragraphes AEM : les composants parsys et iparsys.

### Personnalisation des composants et autres éléments {#customizing-components-and-other-elements}

Lors de la création de vos propres composants ou de la personnalisation d’un composant existant, il est souvent plus facile (et plus sûr) de réutiliser des définitions existantes. Les mêmes principes s’appliquent également à d’autres éléments d’AEM, par exemple le gestionnaire d’erreurs.

Cela peut être effectué en copiant et en remplaçant la définition existante. En d’autres termes, en copiant la définition de `/libs` vers `/apps/<your-project>`. Cette nouvelle définition, dans `/apps`, peut être mise à jour en fonction de vos besoins.

>[!NOTE]
>
>Voir [Utilisation des recouvrements](/help/sites-developing/overlays.md) pour plus d’informations.

Par exemple :

* [Personnalisation d’un composant](/help/sites-developing/components.md)

  Cette procédure suppose de superposer une définition de composant :

   * Création d’un dossier de composants dans `/apps/<website-name>/components/<MyComponent>` en copiant un composant existant :

      * Par exemple, pour personnaliser le composant Texte, copiez :

         * de `/libs/foundation/components/text`
         * vers `/apps/myProject/components/text`

* [Personnalisation des pages affichées par le gestionnaire d’erreurs](/help/sites-developing/customizing-errorhandler-pages.md#how-to-customize-pages-shown-by-the-error-handler)

  Ce cas implique le recouvrement d’un servlet :

   * Dans le référentiel, copiez un ou plusieurs scripts par défaut :

      * de `/libs/sling/servlet/errorhandler/`
      * vers `/apps/sling/servlet/errorhandler/`

>[!CAUTION]
>
>**** Ne modifiez rien dans le chemin d’accès `/libs`. 
>
>La raison en est que le contenu de `/libs` est remplacé la prochaine fois que vous mettez à niveau votre instance (et peut être remplacé lorsque vous appliquez un correctif ou un Feature Pack).
>
>Pour la configuration et les autres modifications :
>
>1. copiez l’élément de `/libs` vers `/apps` ;
>1. apportez les modifications désirées dans `/apps`.

## Quand utiliser les requêtes JCR et quand ne pas les utiliser {#when-to-use-jcr-queries-and-when-not-to-use-them}

Lorsqu’elles sont utilisées correctement, les requêtes JCR sont un puissant outil. Elles sont adaptées aux éléments suivants :

* requêtes réelles de l’utilisateur final, telles que les recherches de texte intégral sur le contenu.
* les cas où du contenu structuré doit être trouvé dans l’ensemble du référentiel.

  Dans ce cas, assurez-vous que les requêtes ne s’exécutent que si nécessaire. Par exemple, lors de l’activation des composants ou de l’invalidation du cache (par opposition, par exemple, aux étapes des workflows, aux gestionnaires d’événements qui se déclenchent lors des modifications de contenu et aux filtres).

N’utilisez jamais de requêtes JCR pour les requêtes de rendu pures. Par exemple, les requêtes JCR ne sont pas appropriées pour les éléments suivants :

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

Utilisez la session utilisateur, et non la session d’administration. Cela signifie que vous devez utiliser :

```java
slingRequest.getResourceResolver().adaptTo(Session.class);
```

### Protect contre les scripts intersites (XSS) {#protect-against-cross-site-scripting-xss}

Les scripts de site à site (XSS) permettent aux pirates d’injecter du code dans des pages web consultées par d’autres utilisateurs. Cette vulnérabilité de sécurité peut être exploitée par des utilisateurs web malveillants pour contourner les contrôles d’accès.

AEM applique le principe de filtrage de tout le contenu fourni par l’utilisateur en sortie. La prévention de XSS se voit accorder la priorité la plus élevée lors des phases de développement et de test.

En outre, un pare-feu d’application web, tel que [mod_security pour Apache](https://modsecurity.org), peut fournir un contrôle central et fiable sur la sécurité de l’environnement de déploiement et se protéger contre les attaques de script intersite qui n’avaient pas été détectées auparavant.

>[!CAUTION]
>
>L’exemple de code fourni avec AEM peut ne pas être protégé contre de telles attaques et repose généralement sur le filtrage des requêtes par un pare-feu d’application web.

La fiche de contrôle de l’API XSS contient des informations que vous devez connaître pour utiliser l’API XSS et rendre une application AEM plus sécurisée. Vous pouvez le télécharger ici :

Aide-mémoire de XSSAPI.

[Obtenir le fichier](assets/xss_cheat_sheet_2016.pdf)

### Sécurisation de la communication pour des informations confidentielles {#securing-communication-for-confidential-information}

Pour toute application Internet, assurez-vous que lors du transport d’informations confidentielles

* le trafic est sécurisé via SSL
* POST HTTP, le cas échéant

Cela s’applique aux informations confidentielles sur le système (telles que la configuration ou l’accès administratif) et confidentielles sur ses utilisateurs (comme leurs informations personnelles).

## Tâches de développement distinctes {#distinct-development-tasks}

### Personnalisation des pages d’erreur {#customizing-error-pages}

Les pages d’erreur peuvent être personnalisées pour AEM. Ceci est recommandé afin que l’instance ne révèle pas de traces sling sur les erreurs du serveur interne.

Voir [Personnalisation des pages d’erreur affichées par le gestionnaire d’erreurs](/help/sites-developing/customizing-errorhandler-pages.md) pour plus d’informations.

### Ouvrir les fichiers dans le processus Java™ {#open-files-in-the-java-process}

Comme AEM peut accéder à de nombreux fichiers, il est recommandé que la variable [Ouvrir des fichiers pour un processus Java™](/help/sites-deploying/configuring.md#open-files-in-the-java-process) être explicitement configuré pour AEM.

Pour minimiser ce problème, le développement doit s’assurer que tout fichier ouvert est correctement fermé lorsque (de manière significative) possible.
