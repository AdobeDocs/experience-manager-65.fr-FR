---
title: Réplication
seo-title: Replication
description: Découvrez comment configurer et surveiller les agents de réplication dans AEM.
seo-description: Learn how to configure and monitor replication agents in AEM.
uuid: 6c0bc2fe-523a-401f-8d93-e5795f2e88b9
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 3cae081e-93e3-4317-b307-1316283c307a
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '3425'
ht-degree: 46%

---

# Réplication{#replication}

Les agents de réplication sont essentiels à Adobe Experience Manager (AEM) comme mécanisme utilisé pour :

* [Publier (activer)](/help/sites-authoring/publishing-pages.md#activatingcontent) contenu d’un auteur vers un environnement de publication.
* Purge explicite du contenu du cache de Dispatcher.
* Renvoyer les entrées utilisateur (par exemple, les entrées de formulaire) de l’environnement de publication vers l’environnement de création (sous le contrôle de l’environnement de création).

Les requêtes [en file d&#39;attente](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) à l’agent approprié pour le traitement.

>[!NOTE]
>
>Les données utilisateur (utilisateurs, groupes d’utilisateurs et profils utilisateur) ne sont pas répliquées entre les instances de création et de publication.
>
>Pour plusieurs instances de publication, les données utilisateur sont distribuées par Sling lors de la [Synchronisation des utilisateurs](/help/sites-administering/sync.md) est activée.

## Réplication de l’auteur à la publication {#replicating-from-author-to-publish}

La réplication, vers une instance de publication ou Dispatcher, se fait en plusieurs étapes :

* l’auteur demande que certains contenus soient publiés (activés) ; cela peut être déclenché par une requête manuelle ou par des déclencheurs automatiques préconfigurés.
* la requête est transmise à l’agent de réplication par défaut approprié ; un environnement peut avoir plusieurs agents par défaut qui seront toujours sélectionnés pour de telles actions.
* l’agent de réplication &quot;regroupe&quot; le contenu et le place dans la file d’attente de réplication.
* dans l’onglet Sites web , [indicateur d’état coloré](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) est définie pour les pages individuelles.
* le contenu est extrait de la file d’attente et transporté vers l’environnement de publication à l’aide du protocole configuré ; il s’agit généralement de HTTP.
* Un servlet dans l’environnement de publication reçoit la demande et publie le contenu reçu ; le servlet par défaut est `https://localhost:4503/bin/receive`.

* Plusieurs environnement de création et de publication peuvent être configurés.

![chlimage_1-21](assets/chlimage_1-21.png)

### Réplication de la publication vers l’auteur {#replicating-from-publish-to-author}

Certaines fonctionnalités permettent aux utilisateurs de saisir des données sur une instance de publication.

Dans certains cas, un type de réplication appelé réplication inverse est nécessaire pour renvoyer ces données à l’environnement de création à partir duquel elles sont redistribuées vers d’autres environnements de publication. En raison de contraintes de sécurité, tout trafic à partir de la publication vers l’environnement de création doit être strictement contrôlé.

La réplication inverse utilise un agent dans l’environnement de publication qui fait référence à l’environnement de création. Cet agent place les données dans une boîte d’envoi. Cette boîte d’envoi est mise en correspondance avec les écouteurs de réplication dans l’environnement de création. Les écouteurs interrogent les boîtes d’envoi pour collecter toutes les données saisies, puis les distribuer selon les besoins. Cela garantit que l’environnement de création contrôle tout le trafic.

Dans d’autres cas, comme pour les fonctionnalités de communauté (par exemple, les forums, les blogs, les commentaires et les révisions), la quantité de contenu généré par l’utilisateur (UGC) entré dans l’environnement de publication est difficile à synchroniser efficacement entre les instances d’AEM à l’aide de la réplication.

AEM [Communities](/help/communities/overview.md) n’utilise jamais la réplication pour le contenu créé par l’utilisateur. Au lieu de cela, le déploiement de Communities nécessite un stock commun pour le contenu créé par l’utilisateur (voir [Stockage de contenu des communautés](/help/communities/working-with-srp.md)).

### Réplication prête à l’emploi {#replication-out-of-the-box}

Le site web we-retail, inclus dans une installation AEM standard, peut être utilisé pour illustrer la réplication.

Pour suivre cet exemple et utiliser les agents de réplication par défaut, vous devez [installer AEM](/help/sites-deploying/deploy.md) avec :

* l’environnement de création sur le port `4502` ;
* l’environnement de publication sur le port `4503`.

>[!NOTE]
>
>Activé par défaut :
>
>* Agents sur l’auteur : Agent par défaut (publication)
>
>Efficacement désactivé par défaut (à partir de AEM 6.1) :
>
>* Agents sur l’auteur : agent de réplication inverse (publish_reverse)
>* Agents sur la publication : réplication inverse (boîte de sortie)
>
>Pour vérifier le statut de l’agent ou de la file d’attente, utilisez la console **Outils**.
>Consultez la section [Surveillance de vos agents de réplication](#monitoring-your-replication-agents).

#### Réplication (auteur à publication) {#replication-author-to-publish}

1. Accédez à la page d’assistance dans l’environnement de création.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Modifiez la page pour ajouter du nouveau texte.
1. **Activer la page** pour publier les modifications.
1. Ouvrez la page d’assistance dans l’environnement de publication :
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Vous pouvez maintenant voir les modifications que vous avez entrées sur l’auteur.

Cette réplication est effectuée à partir de l’environnement de création par :

* **Agent par défaut (publication)**
Cet agent reproduit le contenu vers l’instance de publication par défaut.
Les détails (configuration et journaux) sont accessibles à partir de la console Outils de l’environnement de création ; ou :
  `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agents de réplication prêts à l’emploi {#replication-agents-out-of-the-box}

Les agents suivants sont disponibles dans une installation AEM standard :

* [Agent par défaut](#replication-author-to-publish)
Utilisé pour effectuer une réplication de l’auteur à la publication.

* Le Dispatcher Flush
Utilisé pour gérer le cache du Dispatcher. Consultez la section [Invalidation du cache du Dispatcher depuis l’environnement de création](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) et [Invalidation du cache du Dispatcher depuis l’instance de publication](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/page-invalidate.html#invalidating-dispatcher-cache-from-a-publishing-instance) pour plus d’informations.

* [La réplication inverse](#reverse-replication-publish-to-author)
Utilisée pour effectuer une réplication de la publication à l’auteur. La réplication inverse n’est pas utilisée pour les fonctionnalités de communautés, telles que les forums, les blogs et les commentaires. Elle est désactivée, puisque la boîte d’envoi n’est pas activée. L’utilisation de la réplication inverse nécessite une configuration personnalisée.

* L’agent statique
Il s’agit d’un agent qui stocke une représentation statique d’un nœud dans le système de fichiers.
Par exemple, avec les paramètres par défaut, les pages de contenu et les ressources de gestion des ressources numériques sont stockées sous `/tmp`, au format HTML ou au format de ressource approprié. Consultez les onglets `Settings` et `Rules` pour la configuration.
Cette demande a été faite pour que lorsque la page est demandée directement depuis le serveur d’application, le contenu devienne visible. Il s’agit d’un agent spécialisé qui ne sera (probablement) pas nécessaire pour la plupart des instances.

## Agents de réplication - Paramètres de configuration {#replication-agents-configuration-parameters}

Lors de la configuration d’un agent de réplication à partir de la console Outils, quatre onglets sont disponibles dans la boîte de dialogue :

### Paramètres {#settings}

* **Nom**

  Nom unique de l’agent de réplication.

* **Description**

  Description de l’objectif de cet agent de réplication.

* **Activé**

  Indique si l’agent de réplication est actuellement activé.

  Lorsque l’agent est **enabled** la file d’attente s’affiche comme suit :

   * **Actif** lorsque des éléments sont en cours de traitement.
   * **Inactif** lorsque la file d’attente est vide.
   * **Bloqué** lorsque les éléments sont dans la file d’attente, mais ne peuvent pas être traités ; par exemple, lorsque la file d’attente de réception est désactivée.

* **Type de sérialisation**

  Type de sérialisation :

   * **Par défaut**: Défini si l’agent doit être automatiquement sélectionné.
   * **Purge du Dispatcher**: Sélectionnez cette option si l’agent doit être utilisé pour vider le cache du Dispatcher.

* **Intervalle entre deux tentatives**

  Délai (délai d’attente en millisecondes) entre deux reprises en cas de problème.

  Valeur par défaut : `60000`

* **ID utilisateur de l’agent**

  Selon l’environnement, l’agent utilisera ce compte utilisateur pour :

   * collecter et regrouper le contenu à partir de l’environnement de création ;
   * créer et écrire le contenu dans l’environnement de publication ;

  Laissez ce champ vide pour utiliser le compte d’utilisateur du système (compte défini dans le sling en tant qu’utilisateur administrateur, `admin` par défaut).

  >[!CAUTION]
  >
  >Pour un agent dans l’environnement de création, ce compte *doit* avoir un accès en lecture à tous les chemins que vous souhaitez dupliquer. 

  >[!CAUTION]
  >
  >Pour un agent sur l’environnement de publication, ce compte *doit* avoir l’accès en création/écriture requis pour dupliquer le contenu.

  >[!NOTE]
  >
  >Il peut servir de mécanisme pour sélectionner du contenu spécifique à des fins de réplication.

* **Niveau de journal**

  Indique le niveau de détail à utiliser pour les messages du journal.

   * `Error` : seules les erreurs seront enregistrées.
   * `Info` : les erreurs, les avertissements et autres messages informatifs y figureront.
   * `Debug` : un haut niveau de détail sera utilisé dans les messages, principalement à des fins de débogage.

  Valeur par défaut : `Info`

* **Utiliser pour une réplication inverse**

  Indique si cet agent sera utilisé pour la réplication inverse ; renvoie les entrées utilisateur de l’environnement de publication vers l’environnement de création.

* **Mise à jour de l’alias**

  La sélection de cette option active les demandes d’invalidation de chemin d’alias ou de redirection vers un microsite à Dispatcher. En outre, consultez la section [Configuration d’un agent Dispatcher Flush](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transfert {#transport}

* **URI**

  Cela spécifie le servlet de réception à l’emplacement cible. En particulier, vous pouvez spécifier ici le nom d’hôte (ou alias) et le chemin d’accès au contexte de l’instance cible.

  Par exemple :

   * Un agent par défaut peut effectuer une réplication sur `https://localhost:4503/bin/receive`.
   * Un agent Dispatcher Flush peut effectuer une réplication sur `https://localhost:8000/dispatcher/invalidate.cache`.

  Le protocole spécifié ici (HTTP ou HTTPS) détermine la méthode de transfert. 

  Pour les agents Dispatcher Flush, la propriété URI est utilisée uniquement si vous utilisez les entrées de l’hôte virtuel en fonction du chemin pour différencier les fermes. Vous utilisez ce champ pour cibler la ferme à invalider. Par exemple, la ferme de serveurs n°1 dispose d’un hôte virtuel de `www.mysite.com/path1/*` et la ferme de serveurs n°2 d’un hôte virtuel de `www.mysite.com/path2/*`. Vous pouvez utiliser l’URL `/path1/invalidate.cache` pour cibler la première ferme de serveurs et `/path2/invalidate.cache` pour cibler la seconde ferme de serveurs.

* **Utilisateur**

  Nom d’utilisateur du compte à utiliser pour accéder à la cible.

* **Mot de passe**

  Mot de passe du compte à utiliser pour accéder à la cible.

* **Domaine NTLM**

  Domain pour l’authentification NTLM.

* **Hôte NTLM**

  Hôte pour l’authentification NTLM.

* **Activer Relaxed SSL**

  Activez cette option si vous souhaitez que les certificats SSL auto-certifiés soient acceptés.

* **Autoriser les certificats ayant expiré**

  Activez cette option si vous souhaitez que les certificats SSL expirés soient acceptés.

#### Proxy {#proxy}

Les paramètres suivants ne sont nécessaires que si un proxy est nécessaire :

* **Hôte du proxy**

  Nom d’hôte du proxy utilisé pour le transport.

* **Port du proxy**

  Port du proxy.

* **Utilisateur du proxy**

  Nom d’utilisateur du compte à utiliser.

* **Mot de passe du proxy**

  Mot de passe du compte à utiliser.

* **Domaine NTLM du proxy**

  Domaine NTLM du proxy.

* **Hôte NTLM du proxy**

  Domaine NTLM du proxy.

#### Etendu {#extended}

* **Interface**

  Vous pouvez définir ici l’interface de socket à lier.

  Cela définit l’adresse locale à utiliser lors de la création de connexions. Si cette valeur n’est pas définie, l’adresse par défaut est utilisée. Cela s’avère utile pour spécifier l’interface à utiliser sur les systèmes à plusieurs hôtes ou en grappe.

* **Méthode HTTP**

  Méthode HTTP à utiliser.

  Pour un agent de purge de Dispatcher, cette opération est presque toujours GET et ne doit pas être modifiée (POST serait une autre valeur possible).

* **En-têtes HTTP**

  Ils sont utilisés pour les agents de purge de Dispatcher et spécifient les éléments qui doivent être vidés.

  Pour un agent de purge de Dispatcher, les trois entrées standard ne doivent pas avoir à être modifiées :

   * `CQ-Action:{action}`
   * `CQ-Handle:{path}`
   * `CQ-Path:{path}`

  Ils sont utilisés, le cas échéant, pour indiquer l’action à utiliser lors du vidage de la poignée ou du chemin. Les sous-paramètres sont dynamiques :

   * `{action}` indique une action de réplication.

   * `{path}` indique un chemin.

  Ils sont remplacés par le chemin/l’action correspondant à la requête et n’ont donc pas besoin d’être &quot;codés en dur&quot; :

  >[!NOTE]
  >
  >Si vous avez installé AEM dans un contexte autre que le contexte par défaut recommandé, vous devez enregistrer le contexte dans les en-têtes HTTP. Par exemple :
  >`CQ-Handle:/<*yourContext*>{path}`

* **Fermer la connexion**

  Activez cette option pour fermer la connexion après chaque requête.

* **Dépassement du délai de connexion**

  Délai d’expiration (en millisecondes) à appliquer lors de la tentative d’établissement d’une connexion.

* **Dépassement de délai du socket**

  Délai d’expiration (en millisecondes) à appliquer lors de l’attente du trafic après l’établissement d’une connexion.

* **Version du protocole**

  Version du protocole, par exemple, `1.0` pour HTTP/1.0.

#### Déclencheurs {#triggers}

Ces paramètres permettent de définir des déclencheurs pour la réplication automatisée :

* **Ignorer la valeur par défaut**

  Si cette case est cochée, l’agent est exclu de la réplication par défaut. cela signifie qu’il ne sera pas utilisé si un auteur de contenu émet une action de réplication.

* **En cas de modification**

  Ici, une réplication par cet agent sera automatiquement déclenchée lorsqu’une page est modifiée. Il est principalement utilisé pour les agents de purge de Dispatcher, mais également pour la réplication inverse.

* **En cas de distribution**

  Si cette case est cochée, l’agent réplique automatiquement tout contenu marqué pour distribution lors de sa modification.

* **Heure d’activation/de désactivation atteinte**

  Cela déclenche la réplication automatique (pour activer ou désactiver une page selon le cas) lorsque les heures d’activation ou de désactivation définies pour une page se produisent. Il est principalement utilisé pour les agents de purge de Dispatcher.

* **A réception**

  Si cette case est cochée, l’agent effectue une réplication en chaîne lors de la réception d’événements de réplication.

* **Aucune mise à jour d&#39;état**

  Lorsque cette option est cochée, l’agent ne force pas la mise à jour de l’état de réplication.

* **Aucune création de versions différentes**

  Lorsque cette case est cochée, l’agent ne force pas le contrôle de version des pages activées.

## Configuration de vos agents de réplication {#configuring-your-replication-agents}

Pour plus d’informations sur la connexion des agents de réplication à l’instance de publication à l’aide de MSSL, voir [Réplication à l’aide du protocole SSL mutuel](/help/sites-deploying/mssl-replication.md).

### Configuration des agents de réplication à partir de l’environnement de création {#configuring-your-replication-agents-from-the-author-environment}

Dans l’onglet Outils de l’environnement de création, vous pouvez configurer les agents de réplication qui résident dans l’environnement de création (**Agents sur l’auteur**) ou de l’environnement de publication (**Agents sur publication**). Les procédures suivantes illustrent la configuration d’un agent pour l’environnement de création, mais elles peuvent être utilisées pour les deux.

>[!NOTE]
>
>Lorsqu’un dispatcher gère les requêtes HTTP pour les instances d’auteur ou de publication, la requête HTTP de l’agent de réplication doit inclure l’en-tête PATH. En plus de la procédure suivante, vous devez ajouter l’en-tête PATH à la liste des en-têtes du Dispatcher. (Voir [/clientheaders (en-têtes client)](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).
>

1. Accédez à l’onglet **Outils** dans AEM.
1. Cliquez sur **Réplication** (volet de gauche pour ouvrir le dossier).
1. Double-cliquez **Agents sur l’auteur** (le volet gauche ou droit).
1. Cliquez sur le nom de l’agent approprié (qui est un lien) pour afficher des informations détaillées sur cet agent.
1. Cliquez sur **Modifier** pour ouvrir la boîte de dialogue de configuration :

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Les valeurs fournies doivent être suffisantes pour une installation par défaut. Si vous apportez des modifications, cliquez sur **OK** pour les enregistrer (consultez la section [Agents de réplication - Paramètres de configuration](#replication-agents-configuration-parameters) pour obtenir plus de détails sur chaque paramètre).

>[!NOTE]
>
>L’installation AEM standard spécifie `admin` comme utilisateur des informations d’identifications de transfert dans les agents de réplication par défaut.
>
>Cela doit être modifié en compte d’utilisateur de réplication spécifique au site avec les privilèges permettant de répliquer le ou les chemins d’accès requis.

### Configuration de la réplication inverse {#configuring-reverse-replication}

La réplication inverse est utilisée pour renvoyer le contenu utilisateur généré sur une instance de publication à une instance d’auteur. Il est généralement utilisé pour des fonctionnalités telles que les enquêtes et les formulaires d’enregistrement.

Pour des raisons de sécurité, la plupart des topologies de réseau n’autorisent pas les connexions *de* la &quot;zone démilitarisée&quot; (un sous-réseau qui expose les services externes à un réseau non fiable comme Internet).

Comme l’environnement de publication se trouve généralement dans la zone démilitarisée, la connexion doit être lancée à partir de l’instance d’auteur pour que le contenu soit récupéré dans l’environnement de création. Pour ce faire, procédez comme suit :

* an *outbox* dans l’environnement de publication où le contenu est placé.
* un agent (publication) dans l’environnement de création qui interroge régulièrement la boîte d’envoi pour trouver du nouveau contenu.

>[!NOTE]
>
>Pour AEM [Communities](/help/communities/overview.md), la réplication n’est pas utilisée pour le contenu généré par l’utilisateur sur l’instance de publication. Consultez la section [Stockage de contenu de la communauté](/help/communities/working-with-srp.md).

Pour cela vous aurez besoin des éléments suivants :

**Un agent de réplication inverse dans l’environnement de création** Il agit comme le composant principal pour collecter des informations à partir de la boîte d’envoi dans l’environnement de publication :

Si vous souhaitez utiliser la réplication inverse, vérifiez que cet agent est activé.

![chlimage_1-23](assets/chlimage_1-23.png)

**Un agent de réplication inverse dans l’environnement de publication (boîte d’envoi)** Il s’agit de l’élément passif, car il agit comme une « boîte d’envoi ». L’entrée de l’utilisateur est placée ici, d’où elle est collectée par l’agent dans l’environnement de création.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuration de la réplication pour plusieurs instances de publication {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Seul le contenu est répliqué : les données utilisateur ne le sont pas (utilisateurs, groupes d’utilisateurs et profils utilisateur).
>
>Pour synchroniser les données utilisateur sur plusieurs instances de publication, activez [la synchronisation des utilisateurs](/help/sites-administering/sync.md).

Lors de l’installation, un agent par défaut est déjà configuré pour la réplication du contenu vers une instance de publication s’exécutant sur le port 4503 de l’hôte local.

Pour configurer la réplication du contenu pour une instance de publication supplémentaire, vous devez créer et configurer un nouvel agent de réplication :

1. Ouvrez le **Outils** dans AEM.
1. Sélectionner **Réplication**, puis **Agents sur l’auteur** dans le panneau de gauche.
1. Sélectionnez **Nouveau...**.
1. Définissez la variable **Titre** et **Nom**, puis sélectionnez **Agent de réplication**.
1. Cliquez sur **Créer** pour créer l’agent.
1. Double-cliquez sur le nouvel élément de l’agent pour ouvrir le panneau de configuration.
1. Cliquez sur **Modifier** - le **Paramètres de l’agent** La boîte de dialogue s’ouvre ; **Type de sérialisation** est déjà défini comme valeur par défaut. Il doit le rester.

   * Dans le **Paramètres** tab :

      * Activer **Activé**.
      * Saisissez un **Description**.
      * Définissez l’**intervalle entre deux tentatives** sur `60000`.

      * Gardez le **type de sérialisation** par `Default`.

   * Dans l’onglet **Transfert** :

      * Saisissez l’URI requise pour la nouvelle instance de publication, par exemple,
        `https://localhost:4504/bin/receive`.

      * Saisissez le compte utilisateur spécifique au site utilisé pour la réplication.
      * Vous pouvez configurer d’autres paramètres selon vos besoins.

1. Cliquez sur **OK** pour enregistrer les paramètres.

Vous pouvez ensuite tester l’opération en mettant à jour, puis en publiant une page dans l’environnement de création.

Les mises à jour s’affichent sur toutes les instances de publication qui ont été configurées comme ci-dessus.

Si vous rencontrez des problèmes, vous pouvez vérifier les journaux sur l’instance d’auteur. Selon le niveau de détail nécessaire, vous pouvez également définir le **niveau de journal** sur `Debug` à l’aide de la boîte de dialogue **Paramètres de l’agent**, tel que décrit ci-dessus.

>[!NOTE]
>
>Cette méthode peut être utilisée en association avec l’[ID d’utilisateur de l’agent](#agentuserid) pour sélectionner un contenu différent pour répliquer les environnements de publication individuels. Pour chaque environnement de publication :
>
>1. Configurez un agent de réplication pour la réplication vers cet environnement de publication.
>1. Configuration d’un compte d’utilisateur ; avec les droits d’accès requis pour lire le contenu qui sera répliqué dans cet environnement de publication spécifique.
>1. Attribuez le compte utilisateur comme **Agent User Id** pour l’agent de réplication.
>

### Configuration d’un agent de vidage de Dispatcher {#configuring-a-dispatcher-flush-agent}

Les agents par défaut sont inclus dans l’installation. Toutefois, une configuration est toujours nécessaire et la même s’applique si vous définissez un nouvel agent :

1. Ouvrez le **Outils** dans AEM.
1. Cliquez sur **Déploiement**.
1. Sélectionnez **Réplication**, puis **Agents sur la publication**.
1. Double-cliquez sur le **Purge du Dispatcher** pour ouvrir la présentation.
1. Cliquez sur **Modifier** - le **Paramètres de l’agent** La boîte de dialogue s’ouvre :

   * Dans le **Paramètres** tab :

      * Activer **Activé**.
      * Saisissez un **Description**.
      * Gardez le **type de sérialisation** sur `Dispatcher Flush` ou définissez-le comme pour la création d’un agent.

      * (Facultatif) Sélectionnez **Mise à jour des alias** pour activer les demandes d’invalidation de chemin alias ou de redirection vers le Dispatcher.

   * Dans l’onglet **Transfert** :

      * Saisissez l’URI requise pour la nouvelle instance de publication, par exemple,
        `https://localhost:80/dispatcher/invalidate.cache`.

      * Saisissez le compte utilisateur spécifique au site utilisé pour la réplication.
      * Vous pouvez configurer d’autres paramètres selon vos besoins.

   Pour les agents Dispatcher Flush, la propriété URI est utilisée uniquement si vous utilisez les entrées de l’hôte virtuel en fonction du chemin pour différencier les fermes. Vous utilisez ce champ pour cibler la ferme à invalider. Par exemple, la ferme de serveurs n°1 dispose d’un hôte virtuel de `www.mysite.com/path1/*` et la ferme de serveurs n°2 d’un hôte virtuel de `www.mysite.com/path2/*`. Vous pouvez utiliser l’URL `/path1/invalidate.cache` pour cibler la première ferme de serveurs et `/path2/invalidate.cache` pour cibler la seconde ferme de serveurs.

   >[!NOTE]
   >
   >Si vous avez installé AEM dans un contexte autre que le contexte recommandé par défaut, vous devez configurer les [en-têtes HTTP](#extended) dans l’onglet **Étendu**.

1. Pour enregistrer les modifications, cliquez sur **OK**.
1. Revenez au **Outils** , d’ici vous pouvez **Activer** la valeur **Purge du Dispatcher** agent (**Agents sur publication**).

L’agent de réplication du **vidage du dispatcher** n’est pas actif sur l’auteur. Vous pouvez accéder à la même page dans l’environnement de publication en utilisant l’URI équivalente ; par exemple, `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Contrôle de l’accès aux agents de réplication {#controlling-access-to-replication-agents}

L’accès aux pages utilisées pour configurer les agents de réplication peut être contrôlé à l’aide des droits d’utilisateur et de page de groupe sur le nœud `etc/replication`.

>[!NOTE]
>
>La définition de telles autorisations n’affecte pas les utilisateurs qui répliquent du contenu (par exemple, à partir de la console Sites web ou de l’option du sidekick). La structure de réplication n’utilise pas la « session utilisateur » ou l’utilisateur actuel pour accéder aux agents de réplication lors de la réplication des pages. 

### Configuration de vos agents de réplication depuis CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La création d’agents de réplication n’est prise en charge que dans l’emplacement `/etc/replication` du référentiel. Cette restriction est nécessaire pour que les listes de contrôle d’accès associées soient correctement gérées. La création d’un agent de réplication à un autre emplacement de l’arborescence peut entraîner un accès non autorisé.

Divers paramètres de vos agents de réplication peuvent être configurés à l’aide de CRXDE Lite.

Si vous accédez à `/etc/replication`, vous pouvez voir les trois nœuds suivants :

* `agents.author`
* `agents.publish`
* `treeactivation`

Les deux `agents` contiennent des informations de configuration concernant l’environnement approprié et ne sont actifs que lorsque cet environnement est en cours d’exécution. Par exemple, `agents.publish` sera uniquement utilisé dans l’environnement de publication. La capture d’écran suivante montre l’agent de publication dans l’environnement de création, compris avec la gestion du contenu web d’AEM :

![chlimage_1-24](assets/chlimage_1-24.png)

## Surveillance de vos agents de réplication {#monitoring-your-replication-agents}

Pour surveiller un agent de réplication :

1. Accédez à l’onglet **Outils** dans AEM.
1. Cliquez sur **Réplication**.
1. Double-cliquez sur le lien vers les agents pour l’environnement approprié (volet gauche ou droit) ; par exemple **Agents sur l’auteur**.

   La fenêtre qui s’affiche donne un aperçu de tous vos agents de réplication pour l’environnement de création, y compris leur cible et leur état.

1. Cliquez sur le nom de l’agent approprié (qui est un lien) pour afficher des informations détaillées sur cet agent :

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Vous pouvez effectuer les opérations suivantes :

   * Vérifiez si l’agent est activé.
   * Regardez la cible de toutes les réplications.
   * Vérifiez si la file d’attente de réplication est actuellement principale (activée).
   * Vérifiez s’il existe des éléments dans la file d’attente.
   * **Actualiser** ou **Effacer** pour mettre à jour l’affichage des entrées de file d’attente ; vous pouvez ainsi voir les éléments entrer et quitter la file d’attente.

   * **Affichez le journal** pour accéder au journal de toutes les actions de l’agent de réplication.
   * **Testez la connexion** à l’instance cible.
   * **Forcer une nouvelle tentative** sur les éléments de la file d’attente, le cas échéant.

   >[!CAUTION]
   >
   >N’utilisez pas le lien « Tester la connexion » pour la boîte d’envoi de réplication inverse sur une instance de publication.
   >
   >
   >Si un test de réplication est effectué pour une file d’attente de la boîte d’envoi, les éléments qui sont plus anciens que la réplication de test sont retraités avec chaque réplication inverse.
   >
   >
   >Si de tels éléments existent déjà dans la file d’attente, ils peuvent être recherchés avec la requête XPath JCR suivante et doivent être supprimés.
   >
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

## Réplication par lots {#batch-replication}

La réplication par lots ne reproduit pas individuellement les pages ou les ressources, mais attend que le premier seuil des deux, qu’il s’agisse d’un seuil temporel ou de taille, soit déclenché.

Il regroupe ensuite tous les éléments de réplication dans un package, qui est ensuite répliqué en tant que fichier unique vers l’éditeur.

L’éditeur décompressera tous les éléments, les enregistrera et les renverra à l’auteur.

### Configuration de la réplication par lots {#configuring-batch-replication}

1. Accédez à `http://serveraddress:serverport/siteadmin`.
1. Appuyez sur l’icône **[!UICONTROL Outils]** dans la partie supérieure de l’écran.
1. Dans le rail de navigation de gauche, accédez à **[!UICONTROL Réplication - Agents sur l’auteur]** et double-cliquez **[!UICONTROL Agent par défaut]**.
   * Vous pouvez également accéder à l’agent de réplication de publication par défaut en accédant directement à `http://serveraddress:serverport/etc/replication/agents.author/publish.html`.
1. Appuyez sur le bouton **[!UICONTROL Modifier]** au-dessus de la file d’attente de réplication.
1. Dans la fenêtre suivante, accédez à l’onglet **[!UICONTROL Avancé]** :
   ![batchreplication](assets/batchreplication.png)
1. Configurez l’agent.

### Paramètres {#parameters}

* `[!UICONTROL Enable Batch Mode]` : active ou désactive le mode de réplication par lots.
* `[!UICONTROL Max Wait Time]` - Durée d’attente maximale avant le démarrage d’une requête par lots, en secondes. La valeur par défaut est de 2 secondes.
* `[!UICONTROL Trigger Size]` - Commence la réplication par lots lorsque cette taille limite est atteinte.

## Ressources supplémentaires {#additional-resources}

Pour plus d’informations sur la résolution des problèmes, vous pouvez lire le [Réplication de dépannage](/help/sites-deploying/troubleshoot-rep.md) page.
