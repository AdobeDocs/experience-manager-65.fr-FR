---
title: ASRP - Fournisseur de ressources de stockage d’Adobe
seo-title: ASRP - Fournisseur de ressources de stockage d’Adobe
description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
role: Administrator
exl-id: 6430ed96-5d96-41b6-866f-90b34ff84f7a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 1%

---

# ASRP - Fournisseur de ressources de stockage d’Adobe {#asrp-adobe-storage-resource-provider}

## À propos d’ASRP {#about-asrp}

Lorsqu’AEM Communities est configuré pour utiliser ASRP comme magasin commun, le contenu généré par l’utilisateur est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options SRP](/help/communities/working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](/help/communities/topologies.md).

## Conditions requises {#requirements}

Une licence supplémentaire est requise pour l’utilisation d’ASRP.

Pour configurer votre site AEM Communities afin d’utiliser ASRP pour le contenu généré par l’utilisateur, contactez votre gestionnaire de compte pour :

* URL du centre de données (adresse du point de terminaison ASRP)
* Clé du client
* Clé secrète
* Identifiants de suite de rapports

Les clés client et secrète sont partagées dans toutes les suites de rapports d’une société. Il existe une suite de rapports par client.

## Configuration {#configuration}

### Sélectionnez ASRP {#select-asrp}

La [console Configuration du stockage](/help/communities/srp-config.md) permet de sélectionner la configuration du stockage par défaut, qui identifie l’implémentation de la SRP à utiliser.

**Sur l’instance d’auteur AEM :**

* Dans la navigation globale, accédez à **[!UICONTROL Outils > Communautés > Configuration du stockage]** et sélectionnez **[!UICONTROL Fournisseur de ressources de stockage d’Adobe (ASRP)]**.

![asrp-default](assets/asrp-default.png)

Les informations suivantes proviennent du processus de mise en service :

* **URL** du centre de données : Menu déroulant permettant de sélectionner le centre de données de production identifié par le représentant de votre compte.
* **Suite de rapports par défaut** : Saisissez le nom de la suite de rapports par défaut.
* **Consumer Key** : Entrez la clé du consommateur.
* **Secret** : Saisissez le secret.
* Sélectionnez **Envoyer**.

Préparez les instances de publication :

* [Réplication de la clé de cryptage](#replicate-the-crypto-key)
* [Réplication de la configuration](#publishing-the-configuration)

Après avoir soumis la configuration, testez la connexion :

* Sélectionnez **Configuration du test**.

   Pour chaque instance de création et de publication, testez la connexion au centre de données à partir de la console Configuration de stockage .

* Assurez-vous que les URL de site pour les données de profil sont routables à partir du centre de données en [externalisant les liens](#externalize-links).

### Répliquer la clé de chiffrement {#replicate-the-crypto-key}

La clé du client et la clé secrète sont chiffrées. Pour que les clés soient chiffrées/déchiffrées correctement, la Principale clé Crypto Granite doit être la même sur toutes les instances AEM.

Suivez les instructions de la section [Répliquer la clé de chiffrement](/help/communities/deploy-communities.md#replicate-the-crypto-key).

### Externaliser les liens {#externalize-links}

Pour des liens d’image de profil et de profil corrects, veillez à [configurer correctement l’externaliseur de liens](/help/sites-developing/externalizer.md).

Veillez à définir les domaines comme des URL routables à partir de l’URL du centre de données (point de terminaison ASRP).

### Synchronisation des heures {#time-synchronization}

Pour que l’authentification avec le point de terminaison ASRP réussisse, les machines exécutant votre AEM Communities hébergé doivent être synchronisées, par exemple avec le [protocole NTP (Network Time Protocol)](https://www.ntp.org/).

### Publication de la configuration {#publishing-the-configuration}

ASRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication :

Sur l’instance d’auteur AEM :

* Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]** dans le menu principal.
* Sélectionnez **Activer l’arborescence**
* **Chemin de début** : accédez à  `/conf/global/settings/communities/srpc/`
* Désélectionner **Uniquement Modifié**
* Sélectionnez **Activer**

## Mise à niveau à partir d’AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Si vous activez ASRP sur un site de communauté publié, tout contenu créé par l’utilisateur déjà stocké dans [JCR](/help/communities/jsrp.md) n’est plus visible, car il n’existe aucune synchronisation des données entre l’espace de stockage on-premise et l’espace de stockage dans le cloud.

**`AEM Communities Extension`** a été précédemment introduit dans les communautés sociales d’AEM 6.0 en tant que service cloud. Depuis AEM 6.1 Communities, aucune configuration de cloud n’est nécessaire, il vous suffit de sélectionner ASRP dans la [console de configuration de stockage](/help/communities/srp-config.md).

En raison de la nouvelle structure de stockage, il est nécessaire de suivre les instructions [upgrade](/help/communities/upgrade.md#adobe-cloud-storage) lors de la mise à niveau des communautés de réseaux sociaux vers Communities.

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les *profils utilisateur* et les *groupes d’utilisateurs*, souvent renseignés dans l’environnement de publication, consultez la page

* [Synchronisation des utilisateurs](/help/communities/sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md)

## Résolution des problèmes {#troubleshooting}

### Le contenu généré par l’utilisateur disparaît après la mise à niveau {#ugc-disappears-after-upgrade}

Si vous effectuez une mise à niveau à partir d’un site de communauté sociale AEM 6.0 existant, veillez à suivre les [instructions de mise à niveau](/help/communities/upgrade.md#adobe-cloud-storage), sinon le contenu généré par l’utilisateur semble être perdu.

### Erreurs d’authentification {#authentication-errors}

Si vous recevez des erreurs d’authentification par rapport à l’URL du centre de données et que le fichier error.log AEM contient des messages sur les horodatages obsolètes, vérifiez que la synchronisation est en cours.

Utilisez un outil tel que le [protocole NTP (Network Time Protocol)](https://www.ntp.org/) pour synchroniser tous les serveurs de création et de publication d’AEM.

### Le nouveau contenu n’apparaît pas dans les recherches {#new-content-does-not-appear-in-searches}

L’infrastructure de stockage dans le cloud d’Adobe utilise *la cohérence éventuelle* pour atteindre ses objectifs de mise à l’échelle et de performances. Pour cette raison, le nouveau contenu n’est pas immédiatement disponible et il faut plusieurs secondes pour qu’il apparaisse dans les résultats de recherche.

Bien que l’intervalle qui affecte la cohérence éventuelle soit surveillé, contactez votre gestionnaire de compte si l’affichage du nouveau contenu dans les recherches prend plus de quelques secondes.

### UGC non visible dans ASRP {#ugc-not-visible-in-asrp}

Assurez-vous que l&#39;ASRP a été configuré pour être le fournisseur par défaut en vérifiant la configuration de l&#39;option de stockage. Par défaut, le fournisseur de ressources de stockage est JSRP, et non ASRP.

Sur toutes les instances d’AEM de création et de publication, consultez à nouveau la console Configuration de stockage ou vérifiez le référentiel AEM.

Dans JCR, si [/conf/global/settings/communities](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) :

* Ne contient pas de noeud [srpc](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp), cela signifie que le fournisseur de stockage est JSRP.
* Si le noeud srpc existe et contient le noeud [defaultconfiguration](https://localhost:4502/crx/de/index.jsp#/conf/global/settings/communities/srp/defaultconfiguration) , les propriétés de la configuration par défaut définissent ASRP comme fournisseur par défaut.
