---
title: Intégration à Adobe Dynamic Tag Management
seo-title: Integrating with Adobe Dynamic Tag Management
description: Découvrez l’intégration avec Adobe Dynamic Tag Management.
seo-description: Learn about integration with Adobe Dynamic Tag Management.
uuid: cbb9f942-44e3-4cd5-b07d-4298a7a08376
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: b8c7a20a-7694-4a49-b66a-060720f17dad
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 69%

---

# Intégration à Adobe Dynamic Tag Management {#integrating-with-adobe-dynamic-tag-management}

Intégrez la [gestion dynamique des balises Adobe](https://www.adobe.com/fr/solutions/digital-marketing/dynamic-tag-management.html) à AEM afin de pouvoir utiliser vos propriétés web de gestion dynamique des balises pour effectuer le suivi des sites AEM. La gestion dynamique des balises permet aux spécialistes du marketing de gérer les balises pour collecter des données et distribuer des données sur les systèmes de marketing numérique. Par exemple, utilisez la gestion dynamique des balises afin de collecter les données d’utilisation de votre site Web AEM et de distribuer les données à analyser dans Adobe Analytics ou Adobe Target.

Avant de procéder à l’intégration, vous devez créer la [propriété Web](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) de gestion dynamique des balises qui surveille le domaine de votre site AEM. Les [options d’hébergement](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) de la propriété Web doivent être configurées de façon à ce que vous puissiez configurer AEM pour accéder aux bibliothèques de gestion dynamique des balises.

Une fois que vous avez configuré l’intégration, les modifications apportées aux outils et aux règles de déploiement de gestion dynamique des balises ne nécessitent pas de modifier la configuration de gestion dynamique des balises dans AEM. Les modifications sont automatiquement disponibles pour AEM.

>[!NOTE]
>
>Si vous utilisez DTM avec une configuration de proxy personnalisée, vous devez configurer les deux configurations de proxy client HTTP, car certaines fonctionnalités d’AEM utilisent les API 3.x et d’autres les API 4.x :
>
>* La version 3.x est configurée avec [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient).
>* Les API 4.x sont configurées avec [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>

## Options de déploiement {#deployment-options}

Les options de déploiement suivantes affectent la configuration de l’intégration à Dynamic Tag Management.

### Hébergement Dynamic Tag Management {#dynamic-tag-management-hosting}

AEM prend en charge Dynamic Tag Management hébergé dans le cloud ou hébergé sur AEM.

* Hébergée dans le cloud : les bibliothèques JavaScript Dynamic Tag Management sont stockées dans le cloud et vos pages AEM y font directement référence.
* Hébergée dans AEM : la gestion dynamique des balises génère des bibliothèques JavaScript. AEM utilise un modèle de workflow pour obtenir et installer les bibliothèques.

Le type d’hébergement utilisé par votre implémentation détermine certaines des tâches de configuration et d’implémentation que vous effectuez. Pour plus d’informations sur les options d’hébergement, voir [Hébergement : onglet Incorporer](https://microsite.omniture.com/t2/help/en_US/dtm/#Hosting__Embed_Tab) dans l’aide de Dynamic Tag Management.

### Bibliothèque d’évaluation et de production {#staging-and-production-library}

Déterminez si votre instance d’auteur AEM utilise le code d’évaluation ou de production Dynamic Tag Management.

En général, votre instance de création utilise les bibliothèques intermédiaires de gestion dynamique des balises tandis que l’instance de production utilise les bibliothèques de production. Ce scénario vous permet d’utiliser l’instance d’auteur pour tester les configurations Dynamic Tag Management non approuvées.

Si vous le souhaitez, votre instance de création peut utiliser les bibliothèques de production. Des modules de navigateur Web sont disponibles et vous permettent de basculer entre l’utilisation des bibliothèques intermédiaires à des fins de test lorsque les bibliothèques sont hébergées dans le cloud.

### Utilisation du crochet de déploiement de Dynamic Tag Management {#using-the-dynamic-tag-management-deployment-hook}

Lorsqu’AEM héberge les bibliothèques de gestion dynamique des balises, vous pouvez utiliser le service de crochet de déploiement de gestion dynamique des balises pour pousser automatiquement les mises à jour de la bibliothèque vers AEM. Les mises à jour de la bibliothèque sont envoyées lorsque des modifications sont apportées aux bibliothèques (par exemple, lorsque les propriétés Web de gestion dynamique des balises sont modifiées).

Pour utiliser le crochet de déploiement, la gestion dynamique des balises doit pouvoir se connecter à l’instance AEM qui héberge les bibliothèques. Vous devez [autoriser l’accès à AEM](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) pour les serveurs de gestion dynamique des balises.

Dans certains cas, AEM peut être inaccessible (par exemple, lorsqu’il se trouve derrière un pare-feu). Dans ces cas, vous pouvez utiliser l’option d’importateur d’interrogations d’AEM pour récupérer régulièrement les bibliothèques. Une expression de tâche cron détermine la planification des téléchargements de bibliothèque.

## Activation de l’accès au service Hook de déploiement {#enabling-access-for-the-deployment-hook-service}

Autorisez le service de crochet de déploiement de gestion dynamique des balises à accéder à AEM afin qu’il puisse mettre à jour les bibliothèques hébergées dans AEM. Indiquez l’adresse IP des serveurs de gestion dynamique des balises qui mettent à jour les bibliothèques d’évaluation et d’exploitation en fonction des besoins :

* Évaluation : `107.21.99.31`
* Exploitation : `23.23.225.112` et `204.236.240.48`

Exécutez la configuration à l’aide de la [console Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou d’un nœud [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) :

* Dans la console Web, utilisez l’élément Configuration du crochet de déploiement de gestion dynamique des balises Adobe de la page Configuration.
* Pour une configuration OSGi, le PID du service est `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet`.

Le tableau suivant décrit les propriétés à configurer.

| Propriété de la console Web | Propriété OSGi | Description |
|---|---|---|
| Liste autorisée d’évaluation d’adresses IP de gestion dynamique des balises | `dtm.staging.ip.whitelist` | L’adresse IP du serveur de gestion dynamique des balises qui met à jour les bibliothèques intermédiaires. |
| Liste autorisée d’exploitation d’adresses IP de gestion dynamique des balises | `dtm.production.ip.whitelist` | L’adresse IP du serveur de gestion dynamique des balises qui met à jour les bibliothèques de production. |

## Création de la configuration Dynamic Tag Management {#creating-the-dynamic-tag-management-configuration}

Créez une configuration cloud de sorte que l’instance AEM puisse s’authentifier auprès de Dynamic Tag Management et interagir avec votre propriété web.

>[!NOTE]
>
>Évitez l’inclusion de deux codes de suivi Adobe Analytics sur vos pages lorsque votre propriété web de gestion dynamique des balises comprend l’outil Adobe Analytics et que vous utilisez également [Content Insight](/help/sites-authoring/content-insights.md). Dans votre [configuration cloud Adobe Analytics](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics), sélectionnez l’option Ne pas inclure le code de suivi.

### Paramètres généraux {#general-settings}

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>Jeton API</td>
   <td>La valeur de la propriété Jeton API de votre compte d’utilisateur de gestion dynamique des balises. AEM utilise cette propriété pour l’authentification auprès de la gestion dynamique des balises.</td>
  </tr>
  <tr>
   <td>Entreprise</td>
   <td>Société à laquelle votre identifiant de connexion est associé.</td>
  </tr>
  <tr>
   <td>Propriété</td>
   <td>Nom de la propriété Web que vous avez créée pour gérer les balises de votre site AEM.</td>
  </tr>
  <tr>
   <td>Inclure le code de production sur l’auteur</td>
   <td><p>Sélectionnez cette option pour que les instances de création et de publication d’AEM utilisent la version de production des bibliothèques de gestion dynamique des balises. </p> <p>Lorsque cette option n’est pas sélectionnée, les paramètres intermédiaires s’appliquent à l’instance de création et les paramètres de production à l’instance de publication.</p> </td>
  </tr>
 </tbody>
</table>

### Propriétés d’auto-hébergement - Évaluation et production {#self-hosting-properties-staging-and-production}

Les propriétés suivantes de la configuration de gestion dynamique des balises permettent à AEM d’héberger les bibliothèques gestion de dynamique des balises. Les propriétés permettent à AEM de télécharger et d’installer les bibliothèques. Vous pouvez éventuellement mettre à jour automatiquement les bibliothèques afin de vous assurer qu’elles reflètent les modifications apportées à l’application de gestion Dynamic Tag Management.

Certaines propriétés utilisent des valeurs obtenues à partir de la section Téléchargement de bibliothèque de l’onglet Incorporer de votre propriété web de gestion dynamique des balises. Pour plus d’informations, voir [Téléchargement de bibliothèque](https://microsite.omniture.com/t2/help/en_US/dtm/#Library_Download) dans l’aide de Dynamic Tag Management.

>[!NOTE]
>
>Lorsque vous hébergez le lot de gestion dynamique des balises sur AEM, le téléchargement de bibliothèque doit être activé dans Gestion dynamique des balises avant la création de la configuration. En outre, Akamai doit être activé, car Akamai fournit les bibliothèques pour le téléchargement.

Lorsque les bibliothèques de gestion dynamique des balises sont hébergées sur AEM, AEM configure automatiquement certaines propriétés de la propriété web en fonction de votre configuration. Consultez les descriptions du tableau suivant.

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>Utiliser l’auto-hébergement</td>
   <td>Sélectionnez cette option lorsque vous hébergez le fichier de bibliothèque de gestion dynamique des balises sur AEM. Sélectionnez cette option pour afficher les autres propriétés figurant dans ce tableau.</td>
  </tr>
  <tr>
   <td>URL du lot de gestion dynamique des balises</td>
   <td>URL à utiliser pour télécharger la bibliothèque de gestion dynamique des balises. Procurez-vous cette valeur à partir de la section des URL de téléchargement de la page de téléchargement des bibliothèques de la gestion dynamique des balises. Pour des raisons de sécurité, cette valeur doit être configurée manuellement.</td>
  </tr>
  <tr>
   <td>Processus de téléchargement</td>
   <td><p>Modèle de workflow à utiliser pour télécharger et installer la bibliothèque de gestion dynamique des balises. Le modèle par défaut est Téléchargement du lot de gestion dynamique des balises par défaut. Utilisez ce modèle, sauf si vous avez créé un modèle personnalisé.</p> <p>Le workflow de téléchargement par défaut active automatiquement les bibliothèques lorsqu’elles sont téléchargées.</p> </td>
  </tr>
  <tr>
   <td>Conseil du domaine</td>
   <td><p>(Facultatif) Domaine du serveur AEM qui héberge la bibliothèque de gestion dynamique des balises. Spécifiez une valeur pour remplacer le domaine par défaut configuré pour un <a href="/help/sites-developing/externalizer.md">service d’externaliseur de lien Day CQ</a>.</p> <p>Lorsqu’il est connecté à la gestion dynamique des balises, AEM utilise cette valeur pour configurer le chemin d’accès HTTP intermédiaire ou le chemin d’accès HTTP de production des propriétés Téléchargement de bibliothèque de la propriété Web de gestion dynamique des balises.</p> </td>
  </tr>
  <tr>
   <td>Conseil du domaine sécurisé</td>
   <td><p>(Facultatif) Domaine du serveur AEM qui héberge la bibliothèque de gestion dynamique des balises en HTTPS. Spécifiez une valeur pour remplacer le domaine par défaut configuré pour un <a href="/help/sites-developing/externalizer.md">service d’externaliseur de lien Day CQ</a>.</p> <p>Lorsqu’il est connecté à la gestion dynamique des balises, AEM utilise cette valeur pour configurer le chemin d’accès HTTPS intermédiaire ou le chemin d’accès HTTPS de production des propriétés Téléchargement de bibliothèque de la propriété Web de gestion dynamique des balises.</p> </td>
  </tr>
  <tr>
   <td>Secret partagé</td>
   <td><p>(Facultatif) Secret partagé à utiliser pour déchiffrer le téléchargement. Procurez-vous cette valeur à partir du champ Secret partagé de la page Téléchargement de bibliothèque de la gestion dynamique des balises.</p> <p><strong>Remarque :</strong> les bibliothèques <a href="https://www.openssl.org/docs/apps/openssl.html">OpenSSL</a> doivent être installées sur l’ordinateur où se trouve AEM afin que ce dernier puisse déchiffrer les bibliothèques téléchargées.</p> </td>
  </tr>
  <tr>
   <td>Activer l’importateur d’interrogations</td>
   <td><p>(Facultatif) Sélectionnez cette option pour télécharger et installer régulièrement la bibliothèque de gestion dynamique des balises afin de vous assurer que vous utilisez une version mise à jour. Lorsque cette option est sélectionnée, la gestion dynamique des balises n’envoie pas de requêtes HTTP POST à l’URL du crochet de déploiement.</p> <p>AEM configure automatiquement la propriété d’URL de crochet de déploiement des propriétés Téléchargement de bibliothèque pour la propriété Web de gestion dynamique des balises. Si cette option est sélectionnée, la propriété est configurée sans valeur. Si cette option n’est pas sélectionnée, la propriété est configurée avec l’URL de votre configuration de gestion dynamique des balises.</p> <p>Activez l’importateur d’interrogations lorsque le crochet de déploiement Dynamic Tag Management ne peut pas se connecter à AEM, par exemple, lorsque AEM se trouve derrière un pare-feu.</p> </td>
  </tr>
  <tr>
   <td>Énoncé de planification</td>
   <td>(Apparaît et est obligatoire lorsque l’option Activer l’importateur d’interrogations est sélectionnée.) Une expression cron qui contrôle à quel moment les bibliothèques de gestion dynamique des balises sont téléchargées.</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### Propriétés d’hébergement dans le cloud - Évaluation et production {#cloud-hosting-properties-staging-and-production}

Vous configurez les propriétés suivantes pour votre configuration de Tag Management dynamique lorsque la configuration de balise dynamique est hébergée dans le cloud.

<table>
 <tbody>
  <tr>
   <th>Propriété</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>Utiliser l’auto-hébergement</td>
   <td>Effacez cette option lorsque le fichier de bibliothèque de gestion dynamique des balises est hébergé dans le cloud.</td>
  </tr>
  <tr>
   <td>Code d’en-tête</td>
   <td><p>Le code d’en-tête de l’évaluation obtenu à partir de la gestion dynamique des balises pour votre hôte. Cette valeur est automatiquement renseignée lorsque vous vous connectez à la gestion dynamique des balises.</p> <p> Pour voir le code dans la gestion dynamique des balises, cliquez sur l’onglet Incorporer, puis sur le nom d’hôte. Développez la section Code d’en-tête et cliquez sur l’option Copier le code intégré de la zone Code intégré intermédiaire ou de la zone Code intégré de production selon les besoins.</p> </td>
  </tr>
  <tr>
   <td>Code de pied de page</td>
   <td><p>Le code de pied de page de l’évaluation obtenu à partir de la gestion dynamique des balises pour votre hôte. Cette valeur est automatiquement renseignée lorsque vous vous connectez à la gestion dynamique des balises.</p> <p>Pour voir le code dans la gestion dynamique des balises, cliquez sur l’onglet Incorporer, puis sur le nom d’hôte. Développez la section Code de pied de page et cliquez sur l’option Copier le code intégré de la zone Code intégré intermédiaire ou Code intégré de production selon les besoins.</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

La procédure suivante utilise l’IU optimisée pour les écrans tactiles pour configurer l’intégration à Dynamic Tag Management.

1. Sur le rail, cliquez sur Outils > Opérations > Cloud > Cloud Service.
1. Dans la zone Tag Management dynamique , l’un des liens suivants s’affiche pour ajouter une configuration :

   * Cliquez sur Configurer maintenant s’il s’agit de la première configuration que vous ajoutez.
   * Cliquez sur Afficher les configurations, puis sur le lien + en regard de Configurations disponibles si une ou plusieurs configurations ont été créées.

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. Saisissez le titre de la configuration, puis cliquez sur Créer.
1. Dans le champ Jeton API , saisissez la valeur de la propriété Jeton API de votre compte utilisateur Tag Management dynamique.

   Pour obtenir la valeur de votre jeton API, contactez le service client de gestion dynamique des balises.

   >[!NOTE]
   >
   >Le jeton API n’expire que lorsque l’utilisateur de la gestion dynamique des balises le demande explicitement.

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. Cliquez sur Connexion à la gestion dynamique des balises. AEM s’authentifie auprès de Dynamic Tag Management et récupère la liste des sociétés auxquelles votre compte est associé.
1. Sélectionnez la société, puis la propriété que vous utilisez pour effectuer le suivi de votre site AEM.
1. Si vous utilisez du code d’évaluation sur l’instance d’auteur, désélectionnez l’option Inclure le code de production sur l’auteur.
1. Si nécessaire, indiquez les valeurs des propriétés dans les onglets Paramètres d’évaluation et Paramètres de production, puis cliquez sur OK.

## Téléchargement manuel de la bibliothèque Dynamic Tag Management {#manually-downloading-the-dynamic-tag-management-library}

Téléchargez manuellement les bibliothèques de gestion dynamique des balises pour les mettre immédiatement à jour dans AEM. Par exemple, téléchargez manuellement une bibliothèque mise à jour avant que l’importateur d’interrogations ne soit programmé pour télécharger automatiquement la bibliothèque.

1. Sur le rail, cliquez sur Outils > Opérations > Cloud > Cloud Service.
1. Dans la zone Tag Management dynamique, cliquez sur Afficher les configurations, puis cliquez sur votre configuration.
1. Dans la zone Paramètres d’évaluation ou Paramètres de production, cliquez sur le bouton Déclencher le processus de téléchargement pour télécharger et déployer le lot de bibliothèques.

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>Les fichiers téléchargés sont stockés sous `/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`.
>
>Les valeurs suivantes sont directement issues de votre [configuration de gestion dynamique des balises](#creating-the-dynamic-tag-management-configuration).
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>

## Association d’une configuration Tag Management dynamique à votre site {#associating-a-dynamic-tag-management-configuration-with-your-site}

Associez votre configuration de gestion dynamique des balises aux pages de votre site web de sorte qu’AEM ajoute le script requis aux pages. Associez la page racine de votre site à la configuration. Tous les descendants de cette page héritent de l’association. Si nécessaire, vous pouvez remplacer l’association sur une page descendante.

Utilisez la procédure suivante pour associer une page et les descendants à une configuration de gestion dynamique des balises.

1. Ouvrez la page racine de votre site dans l’IU classique.
1. Utilisez Sidekick pour ouvrir les propriétés de la page.
1. Dans l’onglet Cloud Service, cliquez sur Ajouter un service, sélectionnez Tag Management dynamique, puis cliquez sur OK.

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. Utilisez le menu déroulant Tag Management dynamique pour sélectionner votre configuration, puis cliquez sur OK.

Utilisez la procédure suivante pour remplacer l’association de configuration héritée pour une page. Le remplacement affecte la page et tous ses descendants.

1. Ouvrez la page dans l’IU classique.
1. Utilisez Sidekick pour ouvrir les propriétés de la page.
1. Dans l’onglet Cloud Service, cliquez sur l’icône de cadenas en regard de la propriété Hérité de , puis cliquez sur Oui dans la boîte de dialogue de confirmation.

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Supprimez ou sélectionnez une autre configuration de gestion dynamique des balises, puis cliquez sur OK.
