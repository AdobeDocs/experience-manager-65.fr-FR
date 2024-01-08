---
title: Réplication
description: Découvrez comment configurer et surveiller les agents de réplication dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: 09943de5-8d62-4354-a37f-0521a66b4c49
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '3363'
ht-degree: 25%

---

# Réplication{#replication}

Les agents de réplication sont au coeur de Adobe Experience Manager (AEM) comme mécanisme utilisé pour :

* [Publier (activer)](/help/sites-authoring/publishing-pages.md#activatingcontent) contenu d’un environnement de création vers un environnement de publication.
* purger explicitement du contenu du cache de Dispatcher ;
* Renvoyer les entrées utilisateur (par exemple, les entrées de formulaire) de l’environnement de publication vers l’environnement de création (sous le contrôle de l’environnement de création).

Les requêtes [en file d&#39;attente](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjobeventhandler) à l’agent approprié pour le traitement.

>[!NOTE]
>
>Les données utilisateur (utilisateurs, groupes d’utilisateurs et profils utilisateur) ne sont pas répliquées entre les instances d’auteur et de publication.
>
>Pour plusieurs instances de publication, les données utilisateur sont distribuées par Sling lors de la [Synchronisation des utilisateurs](/help/sites-administering/sync.md) est activée.

## Réplication de l’auteur à la publication {#replicating-from-author-to-publish}

La réplication vers une instance de publication ou Dispatcher se fait en plusieurs étapes :

* L’auteur demande que certains contenus soient publiés (activés) ; cela peut être déclenché par une requête manuelle ou par des déclencheurs automatiques préconfigurés.
* la requête est transmise à l’agent de réplication par défaut approprié ; un environnement peut avoir plusieurs agents par défaut qui sont toujours sélectionnés pour de telles actions.
* l’agent de réplication &quot;regroupe&quot; le contenu et le place dans la file d’attente de réplication.
* dans l’onglet Sites web , [indicateur d’état coloré](/help/sites-authoring/publishing-pages.md#determiningpagepublicationstatus) est définie pour les pages individuelles.
* le contenu est extrait de la file d’attente et transporté vers l’environnement de publication à l’aide du protocole configuré ; il s’agit généralement du protocole HTTP.
* un servlet de l’environnement de publication reçoit la demande et publie le contenu reçu ; le servlet par défaut est `https://localhost:4503/bin/receive`.

* plusieurs environnements de création et de publication peuvent être configurés.

![chlimage_1-21](assets/chlimage_1-21.png)

### Réplication de la publication vers l’auteur {#replicating-from-publish-to-author}

Certaines fonctionnalités permettent aux utilisateurs de saisir des données sur une instance de publication.

Parfois, un type de réplication appelé réplication inverse est nécessaire pour renvoyer ces données à l’environnement de création à partir duquel elles sont redistribuées vers d’autres environnements de publication. Pour des raisons de sécurité, tout trafic de l’environnement de publication vers l’environnement de création doit être strictement contrôlé.

La réplication inverse utilise un agent dans l’environnement de publication qui fait référence à l’environnement de création. Cet agent place les données dans une boîte d’envoi. Cette boîte d’envoi est mise en correspondance avec les écouteurs de réplication dans l’environnement de création. Les écouteurs interrogent les boîtes d’envoi pour collecter toutes les données saisies, puis les distribuer selon les besoins. Cela garantit que l’environnement de création contrôle tout le trafic.

Dans d’autres cas, comme pour les fonctionnalités de communauté (par exemple, les forums, les blogs, les commentaires et les révisions), la quantité de contenu généré par l’utilisateur (UGC) entré dans l’environnement de publication est difficile à synchroniser efficacement entre les instances AEM à l’aide de la réplication.

AEM [Communities](/help/communities/overview.md) n’utilise jamais la réplication pour le contenu créé par l’utilisateur. Au lieu de cela, le déploiement de Communities nécessite un stock commun pour le contenu créé par l’utilisateur (voir [Stockage de contenu des communautés](/help/communities/working-with-srp.md)).

### Réplication prête à l’emploi {#replication-out-of-the-box}

Le site web we-retail, inclus dans une installation AEM standard, peut être utilisé pour illustrer la réplication.

Pour suivre cet exemple et utiliser les agents de réplication par défaut, [installer AEM](/help/sites-deploying/deploy.md) par :

* l’environnement de création sur le port `4502`
* l’environnement de publication sur le port ; `4503`

>[!NOTE]
>
>Activé par défaut :
>
>* Agents sur l’auteur : agent par défaut (publication)
>
>Efficacement désactivé par défaut (à partir de AEM 6.1) :
>
>* Agents sur l’auteur : agent de réplication inverse (publish_reverse)
>* Agents sur la publication : réplication inverse (boîte d’envoi)
>
>Pour vérifier l’état de l’agent ou de la file d’attente, utilisez la variable **Outils** console.
>Consultez la section [Surveillance de vos agents de réplication](#monitoring-your-replication-agents).

#### Réplication (auteur à publication) {#replication-author-to-publish}

1. Accédez à la page d’assistance dans l’environnement de création.
   **https://localhost:4502/content/we-retail/us/en/experience.html** `<pi>`
1. Modifiez la page afin de pouvoir ajouter du nouveau texte.
1. **Activer la page** pour que vous puissiez publier les modifications.
1. Ouvrez la page d’assistance dans l’environnement de publication :
   **https://localhost:4503/content/we-retail/us/en/experience.html**
1. Vous pouvez maintenant voir les modifications que vous avez entrées sur l’auteur.

Cette réplication est effectuée à partir de l’environnement de création par :

* **Agent par défaut (publication)**
Cet agent réplique le contenu sur l’instance de publication par défaut.
Les détails de cette opération (configuration et journaux) sont accessibles à partir de la console Outils de l’environnement de création ; ou :
  `https://localhost:4502/etc/replication/agents.author/publish.html`.

#### Agents de réplication prêts à l’emploi {#replication-agents-out-of-the-box}

Les agents suivants sont disponibles dans une installation AEM standard :

* [Agent par défaut](#replication-author-to-publish)
Utilisé pour la réplication de l’auteur à la publication.

* Le Dispatcher Flush
Utilisé pour gérer le cache du Dispatcher. Consultez la section [Invalidation du cache du Dispatcher depuis l’environnement de création](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html#invalidating-dispatcher-cache-from-the-authoring-environment) et [Invalidation du cache du Dispatcher depuis l’instance de publication](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=fr#invalidating-dispatcher-cache-from-a-publishing-instance) pour plus d’informations.

* [Réplication inverse](#reverse-replication-publish-to-author)
Utilisé pour la réplication de la publication vers l’auteur. La réplication inverse n’est pas utilisée pour les fonctionnalités de communautés, telles que les forums, les blogs et les commentaires. Elle est désactivée, puisque la boîte d’envoi n’est pas activée. L’utilisation de la réplication inverse nécessite une configuration personnalisée.

* L’agent statique
Il s’agit d’un agent qui stocke une représentation statique d’un nœud dans le système de fichiers.
Par exemple, avec les paramètres par défaut, les pages de contenu et les ressources dam sont stockées sous `/tmp`, soit comme HTML, soit comme format de ressource approprié. Consultez les onglets `Settings` et `Rules` pour la configuration.
Cette demande a été faite pour que lorsque la page est demandée directement depuis le serveur d’application, le contenu devienne visible. Il s’agit d’un agent spécialisé qui n’est (probablement) pas nécessaire pour la plupart des instances.

## Agents de réplication - Paramètres de configuration {#replication-agents-configuration-parameters}

Lors de la configuration d’un agent de réplication à partir de la console Outils, quatre onglets sont disponibles dans la boîte de dialogue :

### Paramètres {#settings}

* **Nom**

  Nom unique de l’agent de réplication.

* **Description**

  Description de l’objectif de cet agent de réplication.

* **Activé**

  Indique si l’agent de réplication est activé.

  Lorsque l’agent est **enabled**, la file d’attente s’affiche comme suit :

   * **Actif** lorsque des éléments sont en cours de traitement.
   * **Inactif** lorsque la file d’attente est vide.
   * **Bloqué** lorsque les éléments sont dans la file d’attente, mais ne peuvent pas être traités ; par exemple, lorsque la file d’attente de réception est désactivée.

* **Type de sérialisation**

  Type de sérialisation :

   * **Par défaut**: défini si l’agent doit être automatiquement sélectionné.
   * **Purge du Dispatcher**: sélectionnez cette option si l’agent doit être utilisé pour vider le cache de Dispatcher.

* **Délai de reprise**

  Délai (délai d’attente en millisecondes) entre deux reprises en cas de problème.

  Valeur par défaut : `60000`

* **Agent User Id**

  Selon l’environnement, l’agent utilise ce compte utilisateur pour :

   * collecter et regrouper le contenu à partir de l’environnement de création ;
   * créer et écrire le contenu dans l’environnement de publication ;

  Laissez ce champ vide pour utiliser le compte d’utilisateur du système (compte défini dans le sling en tant qu’utilisateur administrateur, `admin` par défaut).

  >[!CAUTION]
  >
  >Pour un agent dans l’environnement de création, ce compte *must* disposer d’un accès en lecture à tous les chemins que vous souhaitez répliquer.

  >[!CAUTION]
  >
  >Pour un agent dans l’environnement de publication, ce compte *must* disposer de l’accès en création/écriture nécessaire pour répliquer le contenu.

  >[!NOTE]
  >
  >Il peut servir de mécanisme pour sélectionner du contenu spécifique à des fins de réplication.

* **Niveau de journal**

  Indique le niveau de détail à utiliser pour les messages du journal.

   * `Error`: seules les erreurs sont consignées
   * `Info`: les erreurs, les avertissements et autres messages d’information sont consignés
   * `Debug`: un haut niveau de détail est utilisé dans les messages, principalement à des fins de débogage

  Valeur par défaut : `Info`

* **Utilisation pour la réplication inverse**

  Indique si cet agent est utilisé pour la réplication inverse ; renvoie l’entrée utilisateur de l’environnement Publier sur l’auteur .

* **Mise à jour des alias**

  La sélection de cette option active les demandes d’invalidation de chemin d’alias ou de redirection vers un microsite à Dispatcher. En outre, consultez la section [Configuration d’un agent Dispatcher Flush](/help/sites-deploying/replication.md#configuring-a-dispatcher-flush-agent).

#### Transfert {#transport}

* **URI**

  Cela spécifie le servlet de réception à l’emplacement cible. En particulier, vous pouvez spécifier ici le nom d’hôte (ou alias) et le chemin d’accès au contexte de l’instance cible.

  Par exemple :

   * Un agent par défaut peut effectuer une réplication sur `https://localhost:4503/bin/receive`.
   * Un agent Dispatcher Flush peut effectuer une réplication sur `https://localhost:8000/dispatcher/invalidate.cache`.

  Le protocole spécifié ici (HTTP ou HTTPS) détermine la méthode de transport.

  Pour les agents Dispatcher Flush, la propriété URI est utilisée uniquement si vous utilisez les entrées de l’hôte virtuel en fonction du chemin pour différencier les fermes. Vous utilisez ce champ pour cibler la ferme à invalider. Par exemple, la ferme de serveurs n°1 dispose d’un hôte virtuel de `www.mysite.com/path1/*` et la ferme de serveurs n°2 d’un hôte virtuel de `www.mysite.com/path2/*`. Vous pouvez utiliser l’URL `/path1/invalidate.cache` pour cibler la première ferme de serveurs et `/path2/invalidate.cache` pour cibler la seconde ferme de serveurs.

* **Utilisateur**

  Nom d’utilisateur du compte à utiliser pour accéder à la cible.

* **Mot de passe**

  Mot de passe du compte à utiliser pour accéder à la cible.

* **Domaine NTLM**

  Domain pour l’authentification NTLM.

* **Hôte NTLM**

  Hôte pour l’authentification NTLM.

* **Activer le protocole SSL décontracté**

  Activez cette option si vous souhaitez que les certificats SSL auto-certifiés soient acceptés.

* **Autoriser les certificats expirés**

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

  Pour un agent de purge de Dispatcher, cette valeur est presque toujours GET et ne doit pas être modifiée (POST serait une autre valeur possible).

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

  Activez cette option afin que vous puissiez fermer la connexion après chaque requête.

* **Délai de connexion**

  Timeout (en millisecondes) à appliquer lors de la tentative d’établissement d’une connexion.

* **Dépassement de délai du socket**

  Timeout (en millisecondes) à appliquer lors de l’attente du trafic après l’établissement d’une connexion.

* **Version du protocole**

  Version du protocole. Par exemple : `1.0` pour HTTP/1.0.

#### Déclencheurs {#triggers}

Ces paramètres permettent de définir des déclencheurs pour la réplication automatisée :

* **Ignorer la valeur par défaut**

  Si cette case est cochée, l’agent est exclu de la réplication par défaut ; cela signifie qu’il n’est pas utilisé si un auteur de contenu émet une action de réplication.

* **En cas de modification**

  Ici, une réplication par cet agent est automatiquement déclenchée lorsqu’une page est modifiée. Utilisé pour les agents de purge de Dispatcher, mais également pour la réplication inverse.

* **À la distribution**

  Si cette case est cochée, l’agent réplique automatiquement tout contenu marqué pour distribution lors de sa modification.

* **Heure d’activation/de désactivation atteinte**

  Cela déclenche la réplication automatique (pour activer ou désactiver une page selon le cas) lorsque les heures d’activation ou de désactivation définies pour une page se produisent. Il est principalement utilisé pour les agents de purge de Dispatcher.

* **À réception**

  Si cette case est cochée, les chaînes d’agent se répliquent lors de la réception d’événements de réplication.

* **Aucune mise à jour d’état**

  Lorsque cette case est cochée, l’agent ne force pas la mise à jour de l’état de réplication.

* **Aucun contrôle de version**

  Lorsque cette case est cochée, l’agent ne force pas le contrôle de version des pages activées.

## Configuration de vos agents de réplication {#configuring-your-replication-agents}

Pour plus d’informations sur la connexion des agents de réplication à l’instance de publication à l’aide de MSSL, voir [Réplication à l’aide de SSL mutuel](/help/sites-deploying/mssl-replication.md).

### Configuration des agents de réplication à partir de l’environnement de création {#configuring-your-replication-agents-from-the-author-environment}

Dans l’onglet Outils de l’environnement de création, vous pouvez configurer les agents de réplication qui résident dans l’environnement de création (**Agents sur l’auteur**) ou l’environnement de publication (**Agents sur la publication**). Les procédures suivantes illustrent la configuration d’un agent pour l’environnement de création, mais elles peuvent être utilisées pour les deux.

>[!NOTE]
>
>Lorsqu’un Dispatcher gère les requêtes HTTP pour les instances d’auteur ou de publication, la requête HTTP de l’agent de réplication doit inclure l’en-tête PATH. Outre la procédure suivante, vous devez ajouter l’en-tête PATH à la liste des en-têtes de client de Dispatcher. Voir [/clientheaders (en-têtes client)](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr#specifying-the-http-headers-to-pass-through-clientheaders).
>

1. Accédez à l’onglet **Outils** dans AEM.
1. Cliquez sur **Réplication** (volet de gauche pour ouvrir le dossier).
1. Double-cliquez **Agents sur l’auteur** (le volet gauche ou droit).
1. Cliquez sur le nom de l’agent approprié (qui est un lien) pour afficher des informations détaillées sur cet agent.
1. Cliquez sur **Modifier** la boîte de dialogue de configuration s’ouvre alors :

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. Les valeurs fournies doivent être suffisantes pour une installation par défaut. Si vous apportez des modifications, cliquez sur **OK** pour les enregistrer (voir [Agents de réplication - Paramètres de configuration](#replication-agents-configuration-parameters) pour plus d’informations sur les paramètres individuels).

>[!NOTE]
>
>L’installation AEM standard spécifie `admin` comme utilisateur des informations d’identifications de transfert dans les agents de réplication par défaut.
>
>Cela doit être modifié en compte d’utilisateur de réplication spécifique au site avec les privilèges pour répliquer les chemins requis.

### Configuration de la réplication inverse {#configuring-reverse-replication}

La réplication inverse est utilisée pour renvoyer le contenu utilisateur généré sur une instance de publication vers une instance d’auteur. Il est généralement utilisé pour des fonctionnalités telles que les enquêtes et les formulaires d’enregistrement.

Pour des raisons de sécurité, la plupart des topologies de réseau n’autorisent pas les connexions *de* la &quot;zone démilitarisée&quot; (un sous-réseau qui expose les services externes à un réseau non fiable comme Internet).

Comme l’environnement de publication se trouve généralement dans la zone démilitarisée, la connexion doit être lancée à partir de l’instance d’auteur pour que le contenu soit récupéré dans l’environnement d’auteur. Pour ce faire, procédez comme suit :

* an *outbox* dans l’environnement de publication où le contenu est placé.
* un agent (publication) dans l’environnement de création qui interroge régulièrement la boîte d’envoi pour trouver du nouveau contenu.

>[!NOTE]
>
>Pour les AEM [Communautés](/help/communities/overview.md), la réplication n’est pas utilisée pour le contenu généré par l’utilisateur sur une instance de publication. Consultez la section [Stockage de contenu de la communauté](/help/communities/working-with-srp.md).

Pour ce faire, vous devez :

**Un agent de réplication inverse dans l’environnement de création** - Agit comme composant actif pour collecter des informations à partir de la boîte d’envoi dans l’environnement de publication :

Si vous souhaitez utiliser la réplication inverse, assurez-vous que cet agent est activé.

![chlimage_1-23](assets/chlimage_1-23.png)

**Un agent de réplication inverse dans l’environnement de publication (boîte d’envoi)** - L’élément passif comme il agit comme une &quot;boîte d’envoi&quot;. L’entrée utilisateur est placée ici, d’où elle est collectée par l’agent dans l’environnement de création.

![chlimage_1-1](assets/chlimage_1-1.jpeg)

### Configuration de la réplication pour plusieurs instances de publication {#configuring-replication-for-multiple-publish-instances}

>[!NOTE]
>
>Seul le contenu est répliqué : les données utilisateur ne le sont pas (utilisateurs, groupes d’utilisateurs et profils utilisateur).
>
>Pour synchroniser les données utilisateur sur plusieurs instances de publication, activez [Synchronisation des utilisateurs](/help/sites-administering/sync.md).

Après l’installation, un agent par défaut est déjà configuré pour la réplication du contenu vers une instance de publication s’exécutant sur le port 4503 de l’hôte local.

Pour configurer la réplication du contenu pour une instance de publication supplémentaire, créez et configurez un nouvel agent de réplication :

1. Ouvrez le **Outils** dans AEM.
1. Sélectionner **Réplication**, puis **Agents sur l’auteur** dans le panneau de gauche.
1. Sélectionnez **Nouveau...**.
1. Définissez la variable **Titre** et **Nom**, puis sélectionnez **Agent de réplication**.
1. Cliquez sur **Créer** pour pouvoir créer l’agent.
1. Double-cliquez sur le nouvel élément de l’agent pour ouvrir le panneau de configuration.
1. Cliquez sur **Modifier** - le **Paramètres de l’agent** la boîte de dialogue s’ouvre. **Type de sérialisation** est déjà défini comme valeur par défaut. Il doit le rester.

   * Dans le **Paramètres** tab :

      * Activer **Activé**.
      * Saisissez un **Description**.
      * Définissez l’**intervalle entre deux tentatives** sur `60000`.

      * Gardez le **type de sérialisation** par `Default`.

   * Dans l’onglet **Transfert** :

      * Saisissez l’URI requise pour la nouvelle instance de publication ; par exemple,
        `https://localhost:4504/bin/receive`.

      * Saisissez le compte utilisateur spécifique au site utilisé pour la réplication.
      * Vous pouvez configurer d’autres paramètres selon vos besoins.

1. Cliquez sur **OK**.

Vous pouvez ensuite tester l’opération en mettant à jour, puis en publiant une page dans l’environnement de création.

Les mises à jour s’affichent sur toutes les instances de publication qui ont été configurées comme ci-dessus.

Si vous rencontrez des problèmes, vous pouvez vérifier les journaux sur l’instance d’auteur. Selon le niveau de détail nécessaire, vous pouvez également définir le **niveau de journal** sur `Debug` à l’aide de la boîte de dialogue **Paramètres de l’agent**, tel que décrit ci-dessus.

>[!NOTE]
>
>Cela peut être combiné avec l’utilisation de la fonction [Agent User Id](#agentuserid) pour sélectionner un contenu différent à répliquer dans les environnements de publication individuels. Pour chaque environnement de publication :
>
>1. Configurez un agent de réplication pour répliquer dans cet environnement de publication.
>1. Configurez un compte utilisateur, avec les droits d’accès nécessaires pour lire le contenu répliqué dans cet environnement de publication spécifique.
>1. Attribuez le compte d’utilisateur comme **Agent User Id** pour l’agent de réplication.
>

### Configuration d’un agent de vidage de Dispatcher {#configuring-a-dispatcher-flush-agent}

Les agents par défaut sont inclus dans l’installation. Toutefois, une configuration spécifique est toujours nécessaire et la même s’applique si vous définissez un nouvel agent :

1. Ouvrez le **Outils** dans AEM.
1. Cliquez sur **Déploiement**.
1. Sélectionner **Réplication** puis **Agents sur la publication**.
1. Double-cliquez sur le **Purge du Dispatcher** pour ouvrir la présentation.
1. Cliquez sur **Modifier** - le **Paramètres de l’agent** s’ouvre :

   * Dans le **Paramètres** tab :

      * Activer **Activé**.
      * Saisissez un **Description**.
      * Laissez le champ **Type de sérialisation** as `Dispatcher Flush`ou définissez-le comme tel lors de la création d’un agent.

      * (Facultatif) Sélectionnez **Mise à jour des alias** pour activer les demandes d’invalidation de chemin alias ou de redirection vers le Dispatcher.

   * Dans l’onglet **Transfert** :

      * Saisissez l’URI requise pour la nouvelle instance de publication ; par exemple,
        `https://localhost:80/dispatcher/invalidate.cache`.

      * Saisissez le compte utilisateur spécifique au site utilisé pour la réplication.
      * Vous pouvez configurer d’autres paramètres selon vos besoins.

   Pour les agents Dispatcher Flush, la propriété URI est utilisée uniquement si vous utilisez les entrées de l’hôte virtuel en fonction du chemin pour différencier les fermes. Vous utilisez ce champ pour cibler la ferme à invalider. Par exemple, la ferme de serveurs n°1 dispose d’un hôte virtuel de `www.mysite.com/path1/*` et la ferme de serveurs n°2 d’un hôte virtuel de `www.mysite.com/path2/*`. Vous pouvez utiliser l’URL `/path1/invalidate.cache` pour cibler la première ferme de serveurs et `/path2/invalidate.cache` pour cibler la seconde ferme de serveurs.

   >[!NOTE]
   >
   >Si vous avez installé AEM dans un contexte autre que le contexte par défaut recommandé, configurez la variable [En-têtes HTTP](#extended) dans le **Étendu** .

1. Cliquez sur **OK**.
1. Revenez au **Outils** , d’ici vous pouvez **Activer** la valeur **Purge du Dispatcher** agent (**Agents sur la publication**).

La variable **Purge du Dispatcher** l’agent de réplication n’est pas actif sur l’auteur. Vous pouvez accéder à la même page dans l’environnement de publication à l’aide de l’URI équivalent, par exemple : `https://localhost:4503/etc/replication/agents.publish/flush.html`.

### Contrôle de l’accès aux agents de réplication {#controlling-access-to-replication-agents}

L’accès aux pages utilisées pour configurer les agents de réplication peut être contrôlé à l’aide des droits d’utilisateur et de page de groupe sur le nœud `etc/replication`.

>[!NOTE]
>
>La définition de telles autorisations n’a aucune incidence sur la réplication du contenu par les utilisateurs (par exemple, à partir de la console Sites web ou de l’option du sidekick). La structure de réplication n’utilise pas la « session utilisateur » ou l’utilisateur actuel pour accéder aux agents de réplication lors de la réplication des pages. 

### Configuration de vos agents de réplication depuis CRXDE Lite {#configuring-your-replication-agents-from-crxde-lite}

>[!NOTE]
>
>La création d’agents de réplication n’est prise en charge que dans l’emplacement `/etc/replication` du référentiel. Cela est nécessaire pour que les listes de contrôle d’accès associées soient correctement gérées. La création d’un agent de réplication à un autre emplacement de l’arborescence peut entraîner un accès non autorisé.

Divers paramètres de vos agents de réplication peuvent être configurés à l’aide de CRXDE Lite.

Si vous accédez à `/etc/replication`, vous pouvez voir les trois noeuds suivants :

* `agents.author`
* `agents.publish`
* `treeactivation`

Les deux `agents` contiennent des informations de configuration concernant l’environnement approprié et ne sont actifs que lorsque cet environnement est en cours d’exécution. Par exemple : `agents.publish` n’est utilisé que dans l’environnement de publication. La capture d’écran suivante montre l’agent de publication dans l’environnement de création, comme inclus avec AEM WCM :

![chlimage_1-24](assets/chlimage_1-24.png)

## Surveillance de vos agents de réplication {#monitoring-your-replication-agents}

Pour surveiller un agent de réplication :

1. Accédez à l’onglet **Outils** dans AEM.
1. Cliquez sur **Réplication**.
1. Double-cliquez sur le lien vers les agents pour l’environnement approprié (volet gauche ou droit). Par exemple : **Agents sur l’auteur**.

   La fenêtre qui s’affiche affiche un aperçu de tous vos agents de réplication pour l’environnement de création, y compris leur cible et leur état.

1. Cliquez sur le nom de l’agent approprié (qui est un lien) pour afficher des informations détaillées sur cet agent :

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

   Vous pouvez y effectuer les opérations suivantes :

   * Vérifiez si l’agent est activé.
   * Regardez la cible de toutes les réplications.
   * Vérifiez si la file d’attente de réplication est active (activée).
   * Vérifiez s’il existe des éléments dans la file d’attente.
   * **Actualisez** ou **effacez** pour mettre à jour l’affichage des entrées de file d’attente. Cela vous permet de voir que les éléments entrent et sortent de la file d’attente.

   * **Affichez le journal** pour accéder au journal de toutes les actions de l’agent de réplication.
   * **Testez la connexion** à l’instance cible.
   * **Forcez une nouvelle tentative** sur les éléments de la file d’attente, le cas échéant.

   >[!CAUTION]
   >
   >N’utilisez pas le lien &quot;Tester la connexion&quot; pour la boîte d’envoi de réplication inverse sur une instance de publication.
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

Il regroupe ensuite tous les éléments de réplication dans un package, qui est ensuite répliqué en tant que fichier unique dans l’éditeur.

L’ Éditeur décompresse tous les éléments, les enregistre et renvoie le rapport à l’auteur.

### Configuration de la réplication par lots {#configuring-batch-replication}

1. Accédez à `http://serveraddress:serverport/siteadmin`.
1. Appuyez sur la touche **[!UICONTROL Outils]** dans la partie supérieure de l’écran
1. Dans le rail de navigation de gauche, accédez à **[!UICONTROL Réplication - Agents sur l’auteur]** et double-cliquez **[!UICONTROL Agent par défaut]**.
   * Vous pouvez également accéder à l’agent de réplication de publication par défaut en accédant directement à `http://serveraddress:serverport/etc/replication/agents.author/publish.html`
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
