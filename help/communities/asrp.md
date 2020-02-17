---
title: ASRP - Fournisseur de ressources de stockage Adobe
seo-title: ASRP - Fournisseur de ressources de stockage Adobe
description: Configuration des communautés AEM pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configuration des communautés AEM pour utiliser une base de données relationnelle comme magasin commun
uuid: abe47ad9-9f72-4dad-a5e9-6d621a9722d4
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 3e81b519-57ca-4ee1-94bd-7adac4605407
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# ASRP - Fournisseur de ressources de stockage Adobe{#asrp-adobe-storage-resource-provider}

## A propos d’ASRP {#about-asrp}

Lorsque les communautés AEM sont configurées pour utiliser ASRP comme magasin commun, le contenu généré par l’utilisateur (UGC) est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options](/help/communities/working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](/help/communities/topologies.md)recommandées.

## Conditions requises {#requirements}

Une licence supplémentaire est requise pour l&#39;utilisation de ASRP.

Pour configurer votre site AEM Communities afin d’utiliser ASRP pour UGC, contactez votre gestionnaire de compte pour :

* URL du centre de données (adresse du point de terminaison ASRP)
* Clé du client
* Clé secrète
* Identifiants de Report Suite

Les clés secrètes et de consommateur sont partagées dans toutes les suites de rapports d’une entreprise. Il existe une suite de rapports par client.

## Configuration{#configuration}

### Sélectionner ASRP {#select-asrp}

La console [Configuration du](/help/communities/srp-config.md) stockage permet de sélectionner la configuration de stockage par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

**Sur l’instance d’auteur AEM :**

* Dans la navigation globale (Outils, Communautés, Configuration du stockage), sélectionnez** Adobe Storage Resource Provider (ASRP).**

![chlimage_1-30](assets/chlimage_1-30.png)

Les informations suivantes proviennent du processus de mise en service :

* **URL du centre de données. **Menu déroulant pour sélectionner le centre de données de production identifié par votre gestionnaire de compte.
* **Suite de rapports par défaut. **Entrez le nom de la suite de rapports par défaut.
* **Clé du client**. Entrez la clé du client.
* **Secret. **Entrez le secret.
* Sélectionnez **Envoyer.**

Préparez les instances de publication :

* [répliquer la clé de chiffrement](#replicate-the-crypto-key)
* [répliquer la configuration](#publishing-the-configuration)

Après avoir envoyé la configuration, testez la connexion :

* Sélectionnez **Test Config**. Pour chaque instance d’auteur et de publication, testez la connexion au centre de données à partir de la console Configuration du stockage.

* Assurez-vous que les URL du site pour les données de profil sont routables à partir du centre de données en [externalisant les liens](#externalize-links).

### Répliquer la clé Crypto {#replicate-the-crypto-key}

La clé de consommation et la clé secrète sont chiffrées. Pour que les clés soient chiffrées/déchiffrées correctement, la clé Granite Crypto maître doit être la même sur toutes les instances AEM.

Suivez les instructions de la section [Répliquer la clé](/help/communities/deploy-communities.md#replicate-the-crypto-key)Crypto.

### Externaliser les liens {#externalize-links}

Pour des liens d’image de profil et de profil corrects, veillez à [configurer correctement l’Externalisateur de liens](/help/sites-developing/externalizer.md).

Veillez à définir les domaines comme des URL routables à partir de l’URL du centre de données (point de terminaison ASRP).

### Synchronisation du temps {#time-synchronization}

Pour que l’authentification avec le point de terminaison ASRP réussisse, les machines qui exécutent vos communautés AEM hébergées doivent être synchronisées dans le temps, comme avec le protocole NTP ( [Network Time Protocol)](https://www.ntp.org/).

### Publication de la configuration {#publishing-the-configuration}

ASRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication :

Sur l’instance d’auteur AEM :

* Naviguer du menu principal vers `Tools > Operations > Replication.`
* Sélectionnez **Activer l’arborescence.**
* **Chemin de début :
**accédez à /etc/socialconfig/srpc/
* Désélectionnez **Uniquement Modifié.**
* Sélectionnez **Activer.**

## Mise à niveau à partir d’AEM 6.0 {#upgrading-from-aem}

>[!CAUTION]
>
>Si vous activez ASRP sur un site de communauté publié, les fichiers UGC déjà stockés dans [](/help/communities/jsrp.md)JCR ne sont plus visibles, car il n’existe aucune synchronisation des données entre le stockage sur site et le stockage en mode cloud.

**`AEM Communities Extension`**a été précédemment introduit dans les communautés sociales AEM 6.0 en tant que service cloud. Depuis les communautés AEM 6.1, aucune configuration de cloud n’est nécessaire, il vous suffit de sélectionner ASRP dans la console [de configuration du](/help/communities/srp-config.md)stockage.

En raison de la nouvelle structure de stockage, il est nécessaire de suivre les instructions de [mise à niveau](/help/communities/upgrade.md#adobe-cloud-storage) lors de la mise à niveau des communautés sociales vers les communautés.

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les profils ** utilisateur et les groupes *d’* utilisateurs, souvent entrés dans l’environnement de publication, consultez la page

* [Synchronisation des utilisateurs](/help/communities/sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](/help/communities/users.md)

## Résolution des incidents {#troubleshooting}

### UGC disparaît après la mise à niveau {#ugc-disappears-after-upgrade}

Si une mise à niveau est effectuée à partir d’un site de communauté sociale AEM 6.0 existant, veillez à suivre les instructions [](/help/communities/upgrade.md#adobe-cloud-storage)de mise à niveau, sinon l’UGC semble être perdu.

### Erreurs d’authentification {#authentication-errors}

Si vous recevez des erreurs d’authentification par rapport à l’URL du centre de données et que le fichier error.log d’AEM contient des messages sur les horodatages obsolètes, vérifiez que la synchronisation de l’heure est en cours.

Utilisez un outil tel que le protocole NTP ( [Network Time Protocol)](https://www.ntp.org/) pour synchroniser tous les serveurs d’auteur et de publication AEM.

### Le nouveau contenu n’apparaît pas dans les recherches {#new-content-does-not-appear-in-searches}

L’infrastructure de stockage en mode cloud d’Adobe utilise une cohérence ** éventuelle pour atteindre ses objectifs de mise à l’échelle et de performances. Pour cette raison, le nouveau contenu n’est pas immédiatement disponible et il faut plusieurs secondes pour qu’il apparaisse dans les résultats de la recherche.

Bien que l’intervalle affectant la cohérence éventuelle soit surveillé, contactez votre gestionnaire de compte si l’affichage du nouveau contenu dans les recherches prend plus de quelques secondes.

### UGC invisible dans ASRP {#ugc-not-visible-in-asrp}

Vérifiez que l&#39;ASRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l&#39;option de stockage. Par défaut, le fournisseur de ressources de stockage est JSRP et non ASRP.

Sur toutes les instances d’auteur et de publication AEM, consultez de nouveau la console de configuration du stockage ou consultez le référentiel AEM.

Dans JCR, if [/etc/socialconfig](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/):

* ne contient pas de noeud [srpc](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , cela signifie que le fournisseur de stockage est JSRP.
* Si le noeud srpc existe et contient la configuration [par](https://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut définissent ASRP comme fournisseur par défaut.

