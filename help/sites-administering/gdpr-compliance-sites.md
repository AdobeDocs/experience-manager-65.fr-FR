---
title: AEM Sites – Préparation pour le RGPD
seo-title: AEM Sites – Préparation pour le RGPD
description: Découvrez les détails de la préparation d’AEM Sites pour le RGPD.
seo-description: Découvrez les détails de la préparation d’AEM Sites pour le RGPD.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 91%

---


# AEM Sites – Préparation pour le RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations relatives à la protection des données et à la protection de la vie privée ; comme le RGPD, l&#39;ACCP, etc.

Le règlement général sur la protection des données (RGPD) de l’Union européenne sur les droits de confidentialité des données entre en vigueur en mai 2018.

AEM Sites est prêt à aider les clients avec les obligations de conformité au RGPD. Cette page guide les clients à travers les procédures de gestion des demandes RGPD dans AEM Sites. Elle décrit l’emplacement des données privées stockées et la procédure pour les supprimer manuellement ou à l’aide de code.

Pour plus d’informations, voir la [page RGPD du centre de traitement des données personnelles d’Adobe](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Voir [Préparation d’AEM pour le RGPD](/help/managing/data-protection-and-privacy.md) pour plus de détails.

## Serveur de création {#author-server}

Les comptes utilisateur et le contenu généré par les utilisateurs sur le serveur de création sont abordés dans la [documentation de la plate-forme relative au RGPD](/help/managing/data-protection-and-privacy.md).

## Serveur de publication {#publish-server}

Les comptes utilisateur utilisés pour authentifier les visiteurs sur le site et le contenu généré par les utilisateurs sur le serveur de publication sont abordés dans la [documentation de la plate-forme relative au RGPD](/help/managing/data-protection-and-privacy.md).

Par défaut, les composants AEM Sites ne stockent pas les données de formulaires saisies par les visiteurs sur le   serveur de publication. Il est recommandé de transférer les données vers un système tiers ou vers Adobe Campaign pour traitement ultérieur.

## Souscription/exclusion {#opt-in-opt-out}

AEM dispose d’un [service d’exclusion des cookies](/help/sites-developing/cookie-optout.md) qui peut être utilisé pour gérer l’inclusion/exclusion des utilisateurs.

## Enhanced Insights by Analytics {#enhanced-insights-by-analytics}

AEM Sites comprend une intégration facultative à Enhanced Insights by Analytics utilisant la fonctionnalité incluse dans le service On-demand Adobe Analytics.

Pour plus d’informations sur la gestion des requêtes RGPD des personnes titulaires de ces données liées à Adobe Analytics, voir [Adobe Analytics et RGPD](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html).

## Enhanced Personalization by Target {#enhanced-personalization-by-target}

AEM Sites comprend une intégration facultative à Enhanced Personalization by Target utilisant la fonctionnalité incluse dans le service On-demand Adobe Target.

Pour plus d’informations sur la gestion des requêtes RGPD des personnes titulaires de ces données liées à Adobe Target, voir [Adobe Target : Confidentialité et règlement général sur la protection des données (RGPD)](https://docs.adobe.com/content/help/en/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html).

## ContextHub {#contexthub}

AEM fournit une couche de données facultative avec [ContextHub](/help/sites-developing/contexthub.md). Cette option conserve les données spécifiques aux visiteurs dans le navigateur, afin qu’elles soient utilisées pour la personnalisation basée sur des règles.

Par défaut, ces données sur les visiteurs ne sont pas stockées dans AEM ; AEM envoie des règles à la couche de données de façon à prendre des décisions de personnalisation dans le navigateur.

>[!NOTE]
>
>Avant Adobe CQ 5.6, ClientContext (une version antérieure de ContextHub) envoyait les données au serveur, mais ne les stockait pas.
>
>Les versions 5.5 et antérieures d’Adobe CQ sont désormais en fin de vie et ne sont pas abordées dans cette documentation.

### Mise en œuvre de la souscription/l’exclusion  {#implementing-opt-in-opt-out}

Le propriétaire du site doit mettre en œuvre un composant d’exclusion en suivant les instructions ci-après.

Ces instructions mettent en œuvre la souscription comme valeur par défaut. Ainsi, un visiteur du site web doit clairement donner son accord avant que toute donnée personnelle soit stockée dans la persistance du navigateur (côté client).

* Le composant d’exclusion doit être inclus à chaque fois que le composant ContextHub est inclus.
* Les conditions qui renvoient au RGPD pour le site web doivent être présentées à ce visiteur du site web, afin de lui permettre :

   * d’accepter ;
   * de refuser ;
   * de modifier son choix précédent.

* Si un visiteur du site accepte les conditions du site, le cookie d’exclusion ContextHub doit être supprimé :

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Si un visiteur du site n’accepte pas les conditions du site, le cookie d’exclusion ContextHub doit être défini :

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Pour vérifier si ContextHub s’exécute en mode d’exclusion, l’appel suivant doit être effectué dans la console du navigateur :

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Aperçu de la persistance de ContextHub  {#previewing-persistence-of-contexthub}

Pour afficher un aperçu de la persistance utilisée par ContextHub, l’utilisateur peut :

* utiliser la console du navigateur, par exemple :

   * Chrome:

      * Ouvrez Outils de développement > Application > Stockage :

         * Stockage local > (site web) > ContextHubPersistence
         * Stockage de session > (site web) > ContextHubPersistence
         * Cookies > (site web) > SessionPersistence
   * Firefox:

      * Ouvrez Outils de développement > Stockage :

         * Stockage local > (site web) > ContextHubPersistence
         * Stockage de session > (site web) > ContextHubPersistence
         * Cookies > (site web) > SessionPersistence
   * Safari:

      * Ouvrez Préférences > Avancé > Afficher le menu Développement dans la barre de menus
      * Ouvrez Développement > Afficher la console JavaScript

         * Console > Stockage > Stockage local > (site web) > ContextHubPersistence
         * Console > Stockage > Stockage de session > (site web) > ContextHubPersistence
         * Console > Stockage > Cookies > (site web) > ContextHubPersistence
   * Internet Explorer:

      * Ouvrez Outils de développement > Console :

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* utiliser l’API ContextHub dans la console du navigateur :

   * ContextHub fournit les couches de persistance des données suivantes :

      * ContextHub.Utils.Persistence.Modes.LOCAL (par défaut)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      Le magasin ContextHub définit la couche de persistance utilisée pour afficher l’état actuel de la persistance. Toutes les couches devraient être cochées.


Par exemple, pour afficher les données enregistrées dans le stockage local :

Pour afficher un aperçu de la persistance utilisée par ContextHub, l’utilisateur peut :

* utiliser la console du navigateur :

   * Dans Chrome : ouvrez Outils de développement > Application > Stockage :

      * Stockage local > (site web) > ContextHubPersistence
      * Stockage de session > (site web) > ContextHubPersistence
      * Cookies > (site web) > SessionPersistence
   * Dans Firefox : ouvrez Outils de développement > Stockage :

      * Stockage local > (site web) > ContextHubPersistence
      * Stockage de session > (site web) > ContextHubPersistence
      * Cookies > (site web) > SessionPersistence


* utiliser l’API ContextHub dans la console du navigateur :

   * ContextHub fournit les couches de persistance des données suivantes :

      * ContextHub.Utils.Persistence.Modes.LOCAL (par défaut)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      Le magasin ContextHub définit la couche de persistance utilisée pour afficher l’état actuel de la persistance. Toutes les couches devraient être cochées.


Par exemple, pour afficher les données enregistrées dans le stockage local :

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Effacement de la persistance de ContextHub  {#clearing-persistence-of-contexthub}

Pour effacer la persistance de ContextHub :

* Pour effacer la persistance des magasins actuellement chargés :

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Pour effacer une couche spécifique de persistance, par exemple, sessionStorage :

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Pour effacer toutes les couches de persistance ContextHub, le code approprié doit être appelé pour l’ensemble des couches :

   * ContextHub.Utils.Persistence.Modes.LOCAL (par défaut)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW

