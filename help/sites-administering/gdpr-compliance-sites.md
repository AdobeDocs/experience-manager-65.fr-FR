---
title: AEM Sites – Préparation pour le RGPD
seo-title: AEM Sites - GDPR Readiness
description: Découvrez les détails de la préparation au RGPD pour AEM Sites.
seo-description: Learn about the details of GDPR Readiness for AEM Sites.
uuid: 00d1fdce-ef9a-4902-a7a5-7225728e8ffc
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 772f6188-5e0b-4e66-b94a-65a0cc267ed3
exl-id: 8c1ea483-7319-4e5c-be4c-d43a2b67d316
source-git-commit: d8ae63edd71c7d27fe93d24b30fb00a29332658d
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 24%

---

# AEM Sites – Préparation pour le RGPD{#aem-sites-gdpr-readiness}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité, comme le RGPD, le CCPA, etc.

Le règlement général sur la protection des données (RGPD) de l’Union européenne sur les droits de confidentialité des données entre en vigueur en mai 2018.

AEM Sites est prêt à aider les clients avec les obligations de conformité au RGPD. Cette page guide les clients à travers les procédures de gestion des demandes RGPD dans AEM Sites. Elle décrit l’emplacement des données privées stockées et la procédure pour les supprimer manuellement ou à l’aide de code.

Pour plus d’informations, voir [Page RGPD du Centre de traitement des données personnelles des Adobes](https://www.adobe.com/fr/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Voir [AEM Préparation au RGPD](/help/managing/data-protection-and-privacy.md) pour plus de détails.

## Serveur de création {#author-server}

Les comptes utilisateur et le contenu généré par l’utilisateur sur le serveur de création sont abordés dans la section [Documentation relative au RGPD de Platform](/help/managing/data-protection-and-privacy.md).

## Serveur de publication {#publish-server}

Les comptes utilisateur utilisés pour authentifier les visiteurs sur le site et le contenu généré par l’utilisateur sur le serveur de publication sont couverts dans la variable [Documentation relative au RGPD de Platform](/help/managing/data-protection-and-privacy.md).

Par défaut, les composants AEM Sites ne stockent pas les données de formulaires saisies par les visiteurs sur le serveur de publication. Il est recommandé de transférer les données vers un système tiers ou vers Adobe Campaign pour traitement ultérieur.

## Souscription/exclusion {#opt-in-opt-out}

AEM dispose d’un [service d’exclusion des cookies](/help/sites-developing/cookie-optout.md) qui peut être utilisé pour gérer les souscriptions/exclusions des utilisateurs.

## Statistiques améliorées par Analytics {#enhanced-insights-by-analytics}

AEM Sites comprend une intégration facultative avec Enhanced Insights by Analytics qui utilise les fonctionnalités du service On-demand Adobe Analytics.

Pour plus d’informations sur la gestion des demandes des titulaires de données RGPD liées à Adobe Analytics, voir [Adobe Analytics et RGPD](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=fr).

## Personnalisation améliorée par Target {#enhanced-personalization-by-target}

AEM Sites comprend une intégration facultative à la personnalisation améliorée par Target, qui utilise les fonctionnalités du service à la demande Adobe Target.

Pour plus d’informations sur la gestion des demandes des titulaires de données RGPD liées à Adobe Target, voir [Adobe Target - Confidentialité et Règlement général sur la protection des données](https://developer.adobe.com/target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation/?lang=en).

## ContextHub {#contexthub}

AEM fournit une couche de données facultative avec [ContextHub](/help/sites-developing/contexthub.md). Cela permet de conserver les données spécifiques aux visiteurs dans le navigateur, à utiliser pour la personnalisation basée sur des règles.

Par défaut, ces données de visiteur ne sont pas stockées dans AEM ; AEM envoie des règles à la couche de données pour prendre des décisions de personnalisation dans le navigateur.

>[!NOTE]
>
>Avant la version 5.6 d’Adobe CQ, le ClientContext (une version antérieure de ContextHub) envoyait les données au serveur, mais ne les stockait pas.
>
>Adobe CQ 5.5 et versions antérieures sont désormais en fin de vie et ne sont pas couverts par cette documentation.

### Mise en œuvre de la souscription/l’exclusion {#implementing-opt-in-opt-out}

Le propriétaire du site doit mettre en oeuvre un composant d’exclusion conformément aux instructions suivantes.

Ces instructions implémentent l’inclusion comme valeur par défaut. Ainsi, un visiteur du site web doit clairement accepter, avant que toute donnée personnelle ne soit stockée dans la persistance (côté client) du navigateur.

* Le composant d’exclusion doit être inclus à chaque fois que le composant ContextHub est inclus.
* Les conditions générales relatives au RGPD pour le site web doivent être présentées au visiteur du site web, ce qui lui permet de :

   * d’accepter ;
   * de refuser ;
   * modifier leur choix précédent ;

* Si un visiteur du site accepte les conditions générales du site, le cookie d’exclusion ContextHub doit être supprimé :

   ```
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   ```

* Si un visiteur du site n’accepte pas les conditions générales du site, le cookie d’exclusion ContextHub doit être défini :

   ```
   ContextHub.Utils.Cookie.setItem('cq-opt-out', 1);
   ```

* Pour vérifier si ContextHub s’exécute en mode d’exclusion, l’appel suivant doit être effectué dans la console du navigateur :

   ```
   var isOptedOut = ContextHub.isOptedOut(true) === true;
   // if isOptedOut is true, ContextHub is running in opt-out mode
   ```

### Aperçu de la persistance de ContextHub {#previewing-persistence-of-contexthub}

Pour prévisualiser la persistance utilisée par ContextHub, un utilisateur peut :

* Utilisez la console du navigateur ; par exemple :

   * Chrome :

      * Ouvrez Outils de développement > Application > Stockage :

         * Stockage local > (site web) > ContextHubPersistence
         * Stockage de session > (site web) > ContextHubPersistence
         * Cookies > (site web) > SessionPersistence
   * Firefox :

      * Ouvrez Outils de développement > Stockage :

         * Stockage local > (site web) > ContextHubPersistence
         * Stockage de session > (site web) > ContextHubPersistence
         * Cookies > (site web) > SessionPersistence
   * Safari :

      * Ouvrez Préférences > Avancé > Afficher le menu Développer dans la barre de menus.
      * Ouvrez Développer > Afficher la console JavaScript .

         * Console > Stockage > Stockage local > (site web) > ContextHubPersistence
         * Console > Stockage > Stockage de session > (site web) > ContextHubPersistence
         * Console > Stockage > Cookies > (site web) > ContextHubPersistence
   * Internet Explorer :

      * Ouvrez Outils de développement > Console :

         * localStorage.getItem(&#39;ContextHubPersistence&#39;)
         * sessionStorage.getItem(&#39;ContextHubPersistence&#39;)
         * document.cookie




* Utilisez l’API ContextHub dans la console du navigateur :

   * ContextHub fournit les couches de persistance des données suivantes :

      * ContextHub.Utils.Persistence.Modes.LOCAL (par défaut)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      Le magasin ContextHub définit le calque de persistance à utiliser. De ce fait, pour afficher l’état actuel de la persistance, tous les calques doivent être vérifiés.


Par exemple, pour afficher les données stockées dans localStorage :

Pour prévisualiser la persistance utilisée par ContextHub, un utilisateur peut :

* Utilisez la console du navigateur :

   * Chrome - ouvrez Outils de développement > Application > Stockage :

      * Stockage local > (site web) > ContextHubPersistence
      * Stockage de session > (site web) > ContextHubPersistence
      * Cookies > (site web) > SessionPersistence
   * Firefox - ouvrez Outils de développement > Stockage :

      * Stockage local > (site web) > ContextHubPersistence
      * Stockage de session > (site web) > ContextHubPersistence
      * Cookies > (site web) > SessionPersistence


* Utilisez l’API ContextHub dans la console du navigateur :

   * ContextHub fournit les couches de persistance des données suivantes :

      * ContextHub.Utils.Persistence.Modes.LOCAL (par défaut)
      * ContextHub.Utils.Persistence.Modes.SESSION
      * ContextHub.Utils.Persistence.Modes.COOKIE
      * ContextHub.Utils.Persistence.Modes.WINDOW

      Le magasin ContextHub définit le calque de persistance à utiliser. De ce fait, pour afficher l’état actuel de la persistance, tous les calques doivent être vérifiés.


Par exemple, pour afficher les données stockées dans localStorage :

```
var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.LOCAL });
console.log(storage.getTree());
```

### Effacement de la persistance de ContextHub {#clearing-persistence-of-contexthub}

Pour effacer la persistance ContextHub :

* Pour effacer la persistance des magasins actuellement chargés :

   ```
   // in order to be able to fully access persistence layer, Opt-Out must be turned off
   ContextHub.Utils.Cookie.removeItem('cq-opt-out');
   
   // following call asks all currently loaded stores to clear their data
   ContextHub.cleanAllStores();
   
   // following call asks all currently loaded stores to set back default values (provided in their configs)
   ContextHub.resetAllStores();
   ```

* Pour effacer un calque de persistance spécifique ; par exemple, sessionStorage :

   ```
   var storage = new ContextHub.Utils.Persistence({ mode: ContextHub.Utils.Persistence.Modes.SESSION });
   storage.setItem('/store', null);
   storage.setItem('/_', null);
   
   // to confirm that nothing is stored:
   console.log(storage.getTree());
   ```

* Pour effacer tous les calques de persistance ContextHub, le code approprié doit être appelé pour tous les calques :

   * ContextHub.Utils.Persistence.Modes.LOCAL (par défaut)
   * ContextHub.Utils.Persistence.Modes.SESSION
   * ContextHub.Utils.Persistence.Modes.COOKIE
   * ContextHub.Utils.Persistence.Modes.WINDOW
