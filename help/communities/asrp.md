---
title: ASRP - Fournisseur de ressources d'Enregistrement d'Adobe
seo-title: ASRP - Fournisseur de ressources d'Enregistrement d'Adobe
description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 3202866bd38779a9784e44ab470152df61c585f5
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 1%

---


# ASRP - Fournisseur de ressources d&#39;Enregistrement d&#39;Adobe {#asrp-adobe-storage-resource-provider}

## À propos de l&#39;ASRP {#about-asrp}

Lorsque AEM Communities est configuré pour utiliser ASRP en tant que magasin commun, le contenu généré par l’utilisateur est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](/help/communities/topologies.md).

## Conditions préalables {#requirements}

Une licence supplémentaire est requise pour l&#39;utilisation de ASRP.

Pour configurer votre site AEM Communities de manière à utiliser ASRP pour UGC, contactez votre gestionnaire de compte pour :

* URL du centre de données (adresse du point de terminaison ASRP)
* Clé du client
* Clé secrète
* ID de suite de rapports

Les clés secrètes et de consommation sont partagées dans toutes les suites de rapports pour une société. Il existe une suite de rapports par client.

## Configuration {#configuration}

### Sélectionner ASRP {#select-asrp}

La [console de configuration d&#39;Enregistrement](/help/communities/srp-config.md) permet de sélectionner la configuration d&#39;enregistrement par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

**Sur l’instance d’auteur AEM :**

* Dans la navigation globale, accédez à **[!UICONTROL Outils > Communautés > Configuration de l&#39;Enregistrement]** et sélectionnez **[!UICONTROL Fournisseur de ressources d&#39;Enregistrement d&#39;Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

Les informations suivantes proviennent du processus de mise en service :

* **URL** du centre de données : Menu déroulant pour sélectionner le centre de données de production identifié par votre gestionnaire de compte.
* **Suite** de rapports par défaut : Entrez le nom de la Report Suite par défaut.
* **consumer key** : Entrez le consumer key.
* **Secret** : Entrez le secret.
* Sélectionnez **Envoyer**.

Préparez les instances de publication :

* [Répliquer la clé de chiffrement](#replicate-the-crypto-key)
* [Réplication de la configuration](#publishing-the-configuration)

Après avoir envoyé la configuration, testez la connexion :

* Sélectionnez **Test Config**.

   Pour chaque instance d’auteur et de publication, testez la connexion au centre de données à partir de la console de configuration de l’Enregistrement.

* Assurez-vous que les URL du site pour les données de profil sont routables à partir du centre de données en [externalisant les liens](#externalize-links).

### Répliquer la clé Crypto {#replicate-the-crypto-key}

Le Consumer key et la clé secrète sont chiffrés. Pour que les clés soient chiffrées/déchiffrées correctement, la Principale clé Crypto de granit doit être la même sur toutes les instances AEM.

Suivez les instructions à l&#39;adresse [Répliquer la clé Crypto](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Externaliser les liens {#externalize-links}

Pour des liens d’image de profil et de profil corrects, veillez à [configurer correctement l’Externalisateur de liens](/help/sites-developing/externalizer.md).

Veillez à définir les domaines comme des URL routables à partir de l’URL du centre de données (point de terminaison ASRP).

### Synchronisation de l&#39;heure {#time-synchronization}

Pour que l&#39;authentification avec le point de terminaison ASRP réussisse, les machines exécutant votre AEM Communities hébergée doivent être synchronisées avec le temps, par exemple avec le [protocole NTP (Network Time Protocol)](https://www.ntp.org/).

### Publication de la configuration {#publishing-the-configuration}

ASRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication :

Sur l’instance d’auteur AEM :

* Accédez au menu principal **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]**
* Sélectionnez **Activer l&#39;arborescence**
* **Chemin** du début : accéder à  `/conf/global/settings/communities/srpc/`
* Désélectionnez **Modifié uniquement**.
* Sélectionnez **Activer**

## Mise à niveau à partir de AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Si vous activez ASRP sur un site de communauté publié, tout UGC déjà stocké dans [JCR](/help/communities/jsrp.md) n’est plus visible, car il n’existe aucune synchronisation des données entre l’enregistrement sur site et l’enregistrement cloud.

**`AEM Communities Extension`** était auparavant introduit dans AEM 6.0 communautés sociales en tant que service cloud. À partir de AEM 6.1 communautés, aucune configuration de cloud n&#39;est nécessaire, il vous suffit de sélectionner ASRP dans la [console de configuration d&#39;enregistrement](/help/communities/srp-config.md).

En raison de la nouvelle structure d’enregistrement, il est nécessaire de suivre les instructions [upgrade](/help/communities/upgrade.md#adobe-cloud-storage) lors de la mise à niveau des communautés sociales vers les communautés.

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur *les utilisateurs*, *les profils utilisateur* et *les groupes d’utilisateurs*, souvent saisis dans l’environnement de publication, consultez

* [Synchronisation des utilisateurs](/help/communities/sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md)

## Résolution des incidents {#troubleshooting}

### UGC disparaît après la mise à niveau {#ugc-disappears-after-upgrade}

Si la mise à niveau à partir d’un site de communauté sociale AEM 6.0 existant, veillez à suivre les [instructions de mise à niveau](/help/communities/upgrade.md#adobe-cloud-storage), sinon l’UGC semble être perdu.

### Erreurs d’authentification {#authentication-errors}

Si vous recevez des erreurs d’authentification par rapport à l’URL du centre de données et que l’AEM error.log contient des messages sur les horodatages obsolètes, vérifiez que la synchronisation de l’heure est en cours.

Utilisez un outil tel que le [protocole NTP (Network Time Protocol)](https://www.ntp.org/) pour synchroniser tous les serveurs d’auteur et de publication d’AEM.

### Le nouveau contenu n&#39;apparaît pas dans les recherches {#new-content-does-not-appear-in-searches}

L&#39;infrastructure d&#39;enregistrement de cloud d&#39;Adobes utilise *une cohérence éventuelle* pour atteindre ses objectifs de mise à l&#39;échelle et de performance. Pour cette raison, le nouveau contenu n’est pas instantanément disponible et il faut plusieurs secondes pour qu’il s’affiche dans les résultats de la recherche.

Bien que l’intervalle affectant la cohérence éventuelle soit surveillé, contactez le représentant du compte si l’affichage du nouveau contenu dans les recherches prend plus de quelques secondes.

### UGC non visible dans ASRP {#ugc-not-visible-in-asrp}

Assurez-vous que l&#39;ASRP a été configuré pour être le fournisseur par défaut en vérifiant la configuration de l&#39;option d&#39;enregistrement. Par défaut, le fournisseur de ressources d’enregistrement est JSRP et non ASRP.

Sur toutes les instances d’AEM création et de publication, consultez à nouveau la console de configuration de l’Enregistrement ou vérifiez le référentiel AEM.

Dans JCR, si [/conf/global/settings/communautés](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) :

* Ne contient pas de noeud [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp), cela signifie que le fournisseur d’enregistrement est JSRP.
* Si le noeud srpc existe et contient [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) noeud, les propriétés de la configuration par défaut définissent ASRP comme fournisseur par défaut.

