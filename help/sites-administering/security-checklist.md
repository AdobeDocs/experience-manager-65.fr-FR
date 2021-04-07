---
title: Liste de contrôle de sécurité
seo-title: Liste de contrôle de sécurité
description: Découvrez les différents aspects de la sécurité lors de la configuration et du déploiement d’AEM.
seo-description: Découvrez les différents aspects de la sécurité lors de la configuration et du déploiement d’AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Sécurité
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '2842'
ht-degree: 86%

---

# Liste de contrôle de sécurité {#security-checklist}

Cette section traite des différentes étapes à suivre pour s’assurer que votre installation AEM est sécurisée une fois déployée. La liste de contrôle doit être appliquée de haut en bas.

>[!NOTE]
>
>Vous trouverez des informations supplémentaires [sur les menaces de sécurité les plus dangereuses, publiées par l’OWASP (Open Web Application Security Project)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project)

>[!NOTE]
>
>D’autres [considérations relatives à la sécurité](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) s’appliquent à la phase de développement.

## Principales mesures de sécurité {#main-security-measures}

### Exécution d’AEM en mode prêt pour la production {#run-aem-in-production-ready-mode}

Pour plus d’informations, voir [Exécution d’AEM en mode prêt pour la production](/help/sites-administering/production-ready.md).

### Activation du protocole HTTPS pour la sécurité des couches de transfert {#enable-https-for-transport-layer-security}

Pour une instance sécurisée, il est obligatoire d’activer la couche de transfert HTTPS sur les instances de création et de publication.

>[!NOTE]
>
>Pour plus d’informations, voir la section [Activation de HTTP Over SSL](/help/sites-administering/ssl-by-default.md).

### Installation des correctifs de sécurité {#install-security-hotfixes}

Assurez-vous d’avoir installé les derniers [correctifs de sécurité fournis par Adobe](https://helpx.adobe.com/fr/experience-manager/kb/aem63-available-hotfixes.html).

### Modification des mots de passe par défaut pour les comptes administrateur d’AEM et de la console OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

L&#39;Adobe recommande vivement, après l&#39;installation, de modifier le mot de passe des comptes [**AEM** `admin` privilégiés ](#changing-the-aem-admin-password) (sur toutes les instances).

Ces comptes sont les suivants :

* Le compte AEM `admin`

   Une fois que vous avez modifié le mot de passe du compte d’administration AEM, vous devez utiliser le nouveau mot de passe lors de l’accès à CRX.

* Mot de passe `admin` pour la console Web OSGi

   Cette modification sera également appliquée au compte d&#39;administration utilisé pour accéder à la console Web. Vous devrez donc utiliser le même mot de passe pour y accéder.

Ces deux comptes utilisent des informations d’identification distinctes. Il est essentiel d’utiliser des mots de passe sécurisés distincts pour un déploiement sécurisé.

#### Modification du mot de passe administrateur d’AEM {#changing-the-aem-admin-password}

Le mot de passe du compte administrateur d’AEM peut être modifié par le biais de la console [Opérations Granite – Users](/help/sites-administering/granite-user-group-admin.md).

Vous pouvez ici modifier le compte `admin` et [modifier le mot de passe](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>La modification du compte administrateur modifie également le compte de la console web OSGi. Après avoir modifié le compte administrateur, vous devez remplacer le compte OSGi par une autre valeur.

#### Importance la modification du mot de passe de la console web OSGi {#importance-of-changing-the-osgi-web-console-password}

Outre le compte d&#39;AEM `admin`, le fait de ne pas modifier le mot de passe par défaut du mot de passe de la console Web OSGi peut conduire à :

* l’affichage du serveur avec un mot de passe par défaut au démarrage et à l’arrêt (opération qui peut prendre quelques minutes sur les serveurs importants) ;
* l’exposition du serveur lorsque le référentiel est en panne/redémarre un lot (et qu’OSGI est en cours d’exécution).

Pour plus d’informations sur la modification du mot de passe de la console web, voir [Modification du mot de passe administrateur de la console web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) ci-dessous.

#### Modification du mot de passe administrateur de la console web OSGi  {#changing-the-osgi-web-console-admin-password}

Vous devez également modifier le mot de passe utilisé pour accéder à la console web. Pour ce faire, configurez les propriétés suivantes de la [console de gestion Apache Felix OSGi ](/help/sites-deploying/osgi-configuration-settings.md) :

**Nom d’utilisateur** et **mot de passe**, les informations d’identification pour accéder à la console de gestion web Apache Felix.
Le mot de passe doit être modifié après l’installation initiale pour garantir la sécurité de votre instance. 

Pour ce faire :

1. Accédez à la console Web à l’adresse `<server>:<port>/system/console/configMgr`.
1. Accédez à la **console de gestion OSGi Apache Felix** et remplacez le **nom d’utilisateur** et le **mot de passe**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Cliquez sur **Enregistrer**.

### Mise en œuvre d’un gestionnaire d’erreur personnalisé  {#implement-custom-error-handler}

Adobe recommande de définir des pages de gestionnaire d’erreur personnalisé, en particulier pour les codes de réponse HTTP 404 et 500, afin d’empêcher la divulgation d’informations.

>[!NOTE]
>
>Pour plus d’informations, voir l’article de la base de connaissances [Comment créer des scripts ou des gestionnaires d’erreur personnalisés](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html).

### Liste de contrôle de sécurité de Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher est un élément essentiel de votre infrastructure. Adobe recommande vivement de compléter la [liste de contrôle de sécurité de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=fr#getting-started).

>[!CAUTION]
>
>À l’aide de Dispatcher, vous devez désactiver le sélecteur « .form ».

## Étapes de vérification  {#verification-steps}

### Configuration des utilisateurs de réplication et de transfert {#configure-replication-and-transport-users}

L’installation AEM standard spécifie `admin` comme utilisateur des informations d’identifications de transfert dans les [agents de réplication](/help/sites-deploying/replication.md) par défaut. De même, l’administrateur est utilisé pour déterminer la source de la réplication sur le système de création.

Pour les aspects liés à la sécurité, les deux doivent être modifiés de manière à refléter le cas d’utilisation particulier en question, avec les deux aspects ci-dessous à l’esprit :

* L’**utilisateur du transfert** ne doit pas être administrateur. Au lieu de cela, configurez un utilisateur sur le système de publication, qui ne dispose de droits d’accès que sur les parties pertinentes du système de publication et utilise ces informations d’identification pour le transfert.

   Vous pouvez partir de l’utilisateur de réception de la réplication en lot et configurer les droits d’accès de cet utilisateur afin qu’ils correspondent à votre situation

* L’**utilisateur de la réplication** ou l’**ID utilisateur de l’agent** ne doit pas être non plus un administrateur, mais un utilisateur qui ne peut afficher que le contenu qui est censé être répliqué. L’utilisateur de la réplication permet de collecter le contenu à répliquer sur le système de création avant de l’envoyer au système de publication.

### Vérification des contrôles d’intégrité de la sécurité du tableau de bord des opérations {#check-the-operations-dashboard-security-health-checks}

AEM 6 introduit un nouveau tableau de bord des opérations, visant à aider les opérateurs système à résoudre les incidents et à contrôler l’intégrité d’une instance.

Le tableau de bord est accompagné également d’une série de contrôles de l’intégrité de la sécurité. Il est recommandé de contrôler le statut de tous les contrôles d’intégrité de la sécurité avant de les publier grâce à votre instance de production. Pour plus d’informations, consultez la [documentation du tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

### Contrôle de la présence des exemples de contenu {#check-if-example-content-is-present}

Tous les exemples de contenu et d’utilisateurs (par exemple, le projet Geometrixx et ses composants) doivent être désinstallés et totalement supprimés sur le système en production avant de les rendre accessibles publiquement.

>[!NOTE]
>
>Les exemples d’applications We.Retail sont supprimés si cette instance est en cours d’exécution en [mode Prêt pour la production](/help/sites-administering/production-ready.md). Si, pour une raison quelconque, ce n&#39;est pas le cas, vous pouvez désinstaller l&#39;exemple de contenu en accédant à Package Manager, puis en recherchant et désinstallant tous les packages We.Retail. Pour plus d’informations, voir [Utilisation de packages](package-manager.md).

### Contrôle de la présence des lots de développement CRX {#check-if-the-crx-development-bundles-are-present}

Ces lots OSGi de développement doivent être désinstallés sur les systèmes de création et de publication en production avant de les rendre accessibles.

* Prise en charge d’Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Contrôle de la présence des lots de développement Sling  {#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) déploie l’installation de la prise en charge des outils Apache Sling (org.apache.sling.tooling.support.install).

Ce lot OSGi doit être désinstallé sur les systèmes de création et de publication en production avant de les rendre accessibles.

### Protection contre les attaques CSRF  {#protect-against-cross-site-request-forgery}

#### Le framework de protection CSRF {#the-csrf-protection-framework}

AEM 6.1 est fourni avec un mécanisme qui offre une protection contre les attaques par usurpation des demandes intersites, appelé « **Infrastructure de protection CSRF Framework** ». Pour plus d’informations sur l’utilisation, consulter la [documentation](/help/sites-developing/csrf-protection.md).

#### Filtre de référents Sling {#the-sling-referrer-filter}

Pour prendre en compte les problèmes de sécurité connus concernant Cross-Site Request Forgery (CSRF) dans CRX WebDAV et Apache Sling, vous devez ajouter des configurations pour le filtre de référent pour pouvoir l’utiliser.

Le service de filtre de référent est un service OSGi qui permet de configurer :

* les méthodes HTTP à filtrer ;
* si un en-tête de référent vide est permis ;
* et une liste de serveurs à autoriser en plus de l’hôte du serveur.

   Par défaut, toutes les variations de localhost et les noms d’hôte actuels auxquels le serveur est lié se trouvent dans la liste.

Pour configurer le service de filtrage de référent :

1. Ouvrez la console Apache Felix (**Configurations**) à l’adresse :

   `https://<server>:<port_number>/system/console/configMgr`

1. Connectez-vous en tant que `admin`.
1. Dans le menu **Configurations**, sélectionnez :

   `Apache Sling Referrer Filter`

1. Dans le champ `Allow Hosts`, saisissez tous les hôtes autorisés en tant que parrain. Chaque entrée doit se trouver dans le formulaire

   &lt;protocol>://&lt;server>:&lt;port>

   Par exemple :

   * `https://allowed.server:80` autorise toutes les demandes émanant de ce serveur avec le port indiqué.
   * Si vous souhaitez également autoriser les demandes https, vous devez saisir une seconde ligne.
   * Si vous autorisez tous les ports de ce serveur, vous pouvez utiliser `0` comme numéro de port.

1. Cochez le champ `Allow Empty` si vous souhaitez autoriser les en-têtes de parrain vides/manquants.

   >[!CAUTION]
   >
   >Il est recommandé de fournir un référent lors de l’utilisation des outils de ligne de commande, comme `cURL` au lieu d’autoriser une valeur vide, car cela peut exposer votre système à des attaques CSRF.

1. Modifiez les méthodes que ce filtre doit utiliser pour les vérifications avec le champ `Filter Methods`.

1. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

### Paramètres OSGI {#osgi-settings}

Certains paramètres OSGI sont définis par défaut de manière à faciliter le débogage de l’application. Ils doivent être modifiés sur vos instances de publication et de création en production afin d’éviter des fuites d’informations internes vers le public.

>[!NOTE]
>
>Tous les paramètres ci-dessous, à l’exception de **Filtre de débogage WCM Day CQ** sont couverts automatiquement par le [mode prêt pour la production](/help/sites-administering/production-ready.md). Ainsi, il est recommandé de vérifier tous les paramètres avant de déployer votre instance dans un environnement de production.

Pour chacun des services ci-dessous, les paramètres spécifiés doivent être modifiés :

* [Gestionnaire de bibliothèque HTML Adobe Granite](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * Activez l’option **Réduire** (pour supprimer retours chariot et les espaces).
   * Activez l’option **Gzip** (pour permettre de compresser les fichiers et d’y accéder dans une demande).
   * Désactivez l’option **Déboguer**.
   * Désactivez l’option **Synchronisation**.

* [Filtre de débogage WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) :

   * Désactivez l’option **Activer**.

* [Filtre WCM Day CQ](/help/sites-deploying/osgi-configuration-settings.md) :

   * Lors de la publication uniquement, définissez **Mode WCM** sur Désactivé.

* [Gestionnaire de scripts Sling Java Apache](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * Désactivez l’option **Générer les informations de débogage**

* [Gestionnaire de scripts Apache Sling JSP](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * Désactivez **Generate Debug Info (Générer les informations de débogage)**
   * Désactivez **Mapped Content (Contenu mappé)**

Pour plus d’informations, voir [Paramètres de configuration d’OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Voir [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour plus de détails et connaître les pratiques recommandées.

## Autres ressources à lire  {#further-readings}

### Atténuation des attaques par déni de service (DoS){#mitigate-denial-of-service-dos-attacks}

Une attaque par déni de service (DoS) est une tentative de rendre une ressource informatique indisponible à ses utilisateurs ciblés. Ce type d’attaque prend souvent la forme d’une ressource surchargée, par exemple :

* Multitude de demandes provenant d’une source externe
* Demande de plus d’informations que le système n’est capable de traiter

   Par exemple, une représentation JSON de l’intégralité du référentiel.

* Lors de la demande d’une page de contenu avec un nombre illimité d’adresses URL, l’adresse URL peut inclure un nom en ligne, certains sélecteurs, une extension et un suffixe, qui peuvent tous être modifiés.

   Par exemple, `.../en.html` peut également être demandé comme suit :

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Toutes les variantes possibles (par exemple, renvoi d’une réponse `200`, configurée pour être mise en cache) seront mises en cache par Dispatcher, ce qui entraîne la saturation du système de fichiers et l’indisponibilité du service pour d’autres demandes.

De nombreux points de configuration permettent de prévenir ce type d’attaque. Nous n’abordons que ceux liés directement à AEM.

**Configuration de Sling pour prévenir les attaques par déni de service**

Sling est *centré sur le contenu*. Cela signifie que le traitement est centré sur le contenu, car chaque demande (HTTP) est mise en correspondance avec le contenu sous forme de ressource JCR (un nœud du référentiel) :

* La première cible est la ressource (nœud JCR) qui contient le contenu.
* Deuxièmement, l’outil de rendu, ou le script, se trouve dans les propriétés des ressources en combinaison avec certaines parties de la demande (sélecteurs et/ou extension, par exemple).

>[!NOTE]
>
>La section [Traitement des demandes Sling](/help/sites-developing/the-basics.md#sling-request-processing) en parle plus en détail.

Cette approche rend Sling très puissant et très flexible, mais, comme toujours, c’est la flexibilité qui doit être gérée attentivement.

Pour vous aider à prévenir toute utilisation abusive en raison d’une attaque par déni de service, vous pouvez prendre les mesures suivantes :

1. Incorporer des contrôles au niveau de l’application. En raison du nombre de variantes possibles, une configuration par défaut n’est pas envisageable.

   Dans votre application, vous devez :

   * Contrôler les sélecteurs dans votre application afin de ne proposer *que* les sélecteurs explicites nécessaires et de renvoyer un message `404` pour tous les autres.
   * Empêcher la sortie d’un nombre illimité de nœuds de contenu.

1. Contrôlez la configuration des outils de rendu par défaut, ce qui peut poser un problème.

   * Notamment, l’outil de rendu JSON, qui peut traverser l’arborescence sur plusieurs des niveaux.

      Par exemple, la demande :

      `http://localhost:4502/.json`

      peut vider l’ensemble du référentiel dans une représentation JSON. Cela entraînerait des problèmes importants au niveau du serveur. Ainsi, Sling définit une limite de nombre maximal de résultats. Pour limiter la profondeur du rendu JSON, vous pouvez définir la valeur pour :

      **Résultats**  max JSON(  `json.maximumresults`)

      dans la configuration du [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Lorsque cette limite est dépassée, le rendu est réduit. La valeur par défaut pour Sling dans AEM est `200`.

   * À titre de mesure préventive, désactivez les autres outils de rendu par défaut (HTML, texte brut, XML). Là encore, en configurant le [servlet Sling GET d’Apache](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Ne désactivez pas l’outil de rendu JSON. Il est nécessaire au fonctionnement normal d’AEM.

1. Utilisez un pare-feu pour filtrer l’accès à votre instance.

   * L’utilisation d’un pare-feu au niveau du système d’exploitation est nécessaire pour filtrer l’accès aux points de votre instance susceptibles de subir des attaques par déni de service si elle n’est pas protégée.

**Atténuer les attaques par déni de service (DoS) provoquées par l’utilisation des sélecteurs de formulaire**

>[!NOTE]
>
>Cette réduction ne doit être effectuée que sur les environnements AEM qui n’utilisent pas Forms.

Comme AEM ne fournit pas d’index prêts à l’emploi pour `FormChooserServlet`, l’utilisation de sélecteurs de formulaire dans les requêtes déclenche une traversée coûteuse du référentiel, ce qui entraîne généralement l’arrêt de l’instance AEM. Les sélecteurs de formulaire peuvent être détectés par la présence de **&amp;ast;.form.&amp;ast;** chaîne dans les requêtes.

Pour atténuer ce problème, veuillez procéder comme suit :

1. Accédez à la console Web en pointant votre navigateur vers *https://&lt;adresse du serveur>:&lt;serverport>/system/console/configMgr*.

1. Recherchez **Day CQ WCM Form Chooser Servlet**
1. Après avoir cliqué sur l’entrée, désactivez la **Recherche avancée requise** dans la fenêtre suivante.

1. Cliquez sur **Enregistrer**.

**Atténuer les attaques par déni de service (DoS) provoquées par l’utilisation du servlet de téléchargement de ressources**

Le servlet de téléchargement de ressources par défaut d’AEM permet aux utilisateurs authentifiés d’émettre des demandes de téléchargement simultanées de grande taille pour créer des fichiers ZIP de ressources visibles, susceptibles de surcharger le serveur et/ou le réseau.

Pour atténuer les risques d’attaques par déni de service, le composant OSGi `AssetDownloadServlet` est désactivé par défaut pour les instances de publication sur les dernières versions d’AEM.

Si votre configuration nécessite l’activation du serveur de téléchargement de ressources, veuillez consulter [cet article](/help/assets/download-assets-from-aem.md) pour plus d’informations.

### Désactivation de WebDAV {#disable-webdav}

WebDAV doit être désactivé dans les environnements de création et de publication. Vous pouvez le faire en arrêtant les lots OSGi appropriés.

1. Connectez-vous à la **console de gestion Felix**, exécutée sur :

   `https://<*host*>:<*port*>/system/console`

   Par exemple, `http://localhost:4503/system/console/bundles`.

1. Dans la liste des lots, recherchez le lot nommé :

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Cliquez sur le bouton Arrêter (colonne Actions) pour arrêter ce lot.

1. Là encore, dans la liste des lots, recherchez le lot nommé :

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Cliquez sur le bouton Arrêter pour arrêter ce lot.

   >[!NOTE]
   >
   >Il n’est pas nécessaire de redémarrer AEM.

### Vérification de toute absence de divulgation d’informations d’identification personnelles dans le chemin d’accès au répertoire principal des utilisateurs {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

Il est important de protéger vos utilisateurs en veillant à ne pas exposer d’informations d’identification personnelles dans le chemin d’accès au répertoire principal des utilisateurs du référentiel.

Depuis AEM 6.1, la façon dont les noms de nœud d’ID utilisateur (également appelé « ID autorisable ») sont stockés est modifiée par une nouvelle mise en œuvre de l’interface `AuthorizableNodeName`. La nouvelle interface n’expose plus l’ID utilisateur dans le nom du nœud, mais génère un nom aléatoire à la place.

Aucune configuration ne doit être effectuée pour l’activer, car il s’agit désormais de la méthode par défaut pour générer des ID autorisables dans AEM.

Même si cela n’est pas recommandé, vous pouvez la désactiver au cas où vous auriez besoin de l’ancienne mise en œuvre pour des raisons de rétrocompatibilité avec vos applications existantes. À cet effet, vous devez effectuer les opérations suivantes :

1. Accédez à la console Web et supprimez l’entrée ** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName*** de la propriété **requiredServicePids** dans **Apache Jackrabbit Oak SecurityProvider**.

   Vous pouvez également trouver Oak Security Provider en cherchant le PID **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** dans les configurations OSGi.

1. Supprimez la configuration OSGi **Apache Jackrabbit Oak Random Authorizable Node Name** dans la console web.

   Pour faciliter la recherche, notez que le PID pour cette configuration est **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Pour plus d’informations, voir la documentation Oak dans la section [Génération de noms de nœud autorisables](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Prévention du détournement de clic {#prevent-clickjacking}

Pour empêcher le détournement de clic, il est conseillé de configurer le serveur web afin que l’en-tête HTTP `X-FRAME-OPTIONS` soit défini sur `SAMEORIGIN`.

Pour plus [d’informations sur le détournement de clic, voir le site OWASP](https://www.owasp.org/index.php/Clickjacking).

### Veillez à répliquer correctement les clés de chiffrement lorsque cela est nécessaire {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Certaines fonctionnalités d’AEM et certains schémas d’authentification exigent que vous répliquiez vos clés de chiffrement sur toutes les instances AEM.

Avant d’effectuer cette opération, notez que la réplication des clés est effectuée différemment entre les versions, car le mode de stockage des clés diffère entre la version 6.3 et les versions antérieures.

Pour plus d’informations, voir ci-dessous.

#### Réplication des clés pour AEM 6.3  {#replicating-keys-for-aem}

Alors que dans les anciennes versions, les clés de réplication étaient stockées dans le référentiel, à compter d’AEM 6.3, elles sont stockées dans le système de fichiers.

Par conséquent, pour reproduire les clés entre les instances, vous devez les copier de l’instance source vers l’emplacement des instances cibles dans le système de fichiers.

Plus spécifiquement, vous devez effectuer les opérations suivantes :

1. Accédez à l’instance AEM, généralement une instance de création, et qui contient le matériel des clés à copier.
1. Cherchez le lot com.adobe.granite.crypto.file dans le système de fichiers local. Par exemple, sous ce chemin d’accès :

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   Le fichier `bundle.info` à l’intérieur de chaque dossier identifie le nom du lot.

1. Accédez au dossier des données. Par exemple :

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copiez les fichiers HMAC et les fichiers principaux.
1. Ensuite, accédez à l’instance cible sur laquelle vous souhaitez dupliquer la clé HMAC, puis accédez au dossier des données. Par exemple :

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Collez les deux fichiers copiés précédemment.
1. [Actualisez le lot de chiffrement](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) si l’instance cible est déjà en cours d’exécution.
1. Répétez les étapes ci-dessus pour toutes les instances sur lesquelles vous souhaitez répliquer la clé.

>[!NOTE]
>
>Vous pouvez rétablir la méthode 6.3 de stockage des clés en ajoutant le paramètre ci-dessous lorsque vous installez AEM pour la première fois :
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Réplication des clés pour AEM 6.2 et versions antérieures {#replicating-keys-for-aem-and-older-versions}

Dans AEM 6.2 et les versions antérieures, les clés sont stockées dans le référentiel sous le noeud `/etc/key`.

La méthode recommandée pour répliquer en toute sécurité les clés sur toutes les instances est de ne répliquer que ce nœud. Vous pouvez répliquer les nœuds de façon sélective à l’aide de CRXDE Lite :

1. Ouvrez le CRXDE Lite en accédant à *https://&lt;adresse du serveur>:4502/crx/de/index.jsp*
1. Sélectionnez le noeud `/etc/key`.
1. Cliquez sur l’onglet **Réplication**.
1. Appuyez sur le bouton **Réplication**.

### Test de pénétration {#perform-a-penetration-test}

Adobe recommande vivement d’effectuer un test de pénétration de l’infrastructure AEM avant la mise en production.

### Meilleures pratiques de développement {#development-best-practices}

Il est essentiel que les nouveaux développements respectent les [meilleures pratiques de sécurité](/help/sites-developing/security.md) afin de vous assurer de la sécurité de votre environnement AEM.
