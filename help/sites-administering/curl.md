---
title: Utiliser cURL avec AEM
description: Découvrez comment utiliser cURL pour les tâches courantes d’Adobe Experience Manager.
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 12b370e3041ff179cd249f3d4e6ef584c4339909
workflow-type: ht
source-wordcount: '1061'
ht-degree: 100%

---

# Utiliser cURL avec AEM{#using-curl-with-aem}

Les administrateurs ont souvent besoin d’automatiser ou de simplifier des tâches courantes sur un système. Dans AEM, par exemple, la gestion des utilisateurs et des utilisatrices, l’installation de packages et la gestion des bundles OSGi sont des tâches qui doivent être effectuées régulièrement.

En raison de la nature RESTful de le framework Sling sur laquelle repose AEM, pratiquement toutes les tâches peuvent se réduire à l’appel d’une adresse URL. cURL peut être utilisé pour exécuter des appels d’URL et peut s’avérer un outil utile pour les administrateurs et administratrices d’AEM.

## cURL, qu’est-ce que c’est ? {#what-is-curl}

cURL est un outil de ligne de commande Open Source utilisé pour manipuler des adresses URL. Il prend en charge de nombreux protocoles Internet, tels que HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP et RTSP.

Initialement publié en 1997, cURL est un outil bien établi et largement répandu pour obtenir ou envoyer des données en utilisant la syntaxe de l’adresse URL. Le nom cURL signifiait à l’origine « see URL&quot; » (« voir l’URL » en français).

Compte tenu de la nature RESTful de la structure Sling sur laquelle repose AEM, la plupart des tâches peuvent se réduire à l’appel d’une adresse URL, ce que cURL peut exécuter. Les [tâches de manipulation de contenu](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands), comme l’activation des pages et le démarrage de workflows, ainsi que les [tâches opérationnelles](/help/sites-administering/curl.md#common-operational-aem-curl-commands), comme la gestion de packages, d’utilisateurs et d’utilisatrices, peuvent être automatisées à l’aide de cURL. En outre, vous pouvez [créer vos propres commandes cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) pour la plupart des tâches dans AEM.

>[!NOTE]
>
>Toute commande AEM exécutée par le biais de cURL doit être autorisée, comme n’importe quel utilisateur, dans AEM. Toutes les listes de contrôle d’accès et tous les droits d’accès sont respectés lors de l’utilisation de cURL pour exécuter une commande AEM.

## Télécharger cURL {#downloading-curl}

cURL est une partie standard de Mac OS et de certaines distributions Linux. Cependant, il est disponible pour la plupart des systèmes d’exploitation. Vous trouverez les derniers téléchargements à l’adresse [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

Le référentiel source de cURL est également disponible sur GitHub.

## Créer une commande AEM compatible avec cURL {#building-a-curl-ready-aem-command}

Il est possible de créer des commandes cURL pour la plupart des opérations dans AEM telles que le déclenchement des workflows, la vérification des configurations OSGi, le déclenchement des commandes JMX, la création d’agents de réplication, etc.

Pour trouver la commande exacte dont vous avez besoin pour votre opération particulière, vous devez utiliser les outils de développement de votre navigateur pour capturer l’appel POST au serveur lorsque vous exécutez la commande AEM.

Les étapes suivantes décrivent comment effectuer cette opération en créant une page dans le navigateur Chrome, par exemple.

1. Préparez l’action à appeler dans AEM. Dans ce cas, nous sommes allés jusqu’à la fin de l’assistant de **création de page**, mais nous n’avons pas encore cliqué sur **Créer**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. Démarrez les outils de développement et sélectionnez l’onglet **Network**. Cliquez sur le bouton **Conserver le journal** avant d’effacer la console.

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. Cliquez sur **Créer** dans l’assistant **Créer une page** pour créer le workflow.
1. Cliquez avec le bouton droit de la souris sur l’action POST obtenue et sélectionnez **Copier** > **Copier en tant que cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. Copiez la commande cURL dans un éditeur de texte et supprimez tous les en-têtes de la commande, qui commencent par `-H` (soulignés en bleu dans l’illustration ci-dessous), puis ajoutez le paramètre d’authentification approprié, comme `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Exécutez la commande cURL à l’aide de la ligne de commande et affichez la réponse.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## Commandes cURL AEM opérationnelles courantes {#common-operational-aem-curl-commands}

Voici une liste des commandes cURL d’AEM pour les tâches administratives et opérationnelles courantes.

>[!NOTE]
>
>Les exemples ci-dessous considèrent qu’AEM est exécuté sur `localhost` sur le port `4502` et utilise le nom d’utilisateur `admin` avec le mot de passe `admin`. D’autres espaces réservés aux commandes sont définis entre crochets.

### Gérer les packages {#package-management}

#### Liste de tous les packages installés

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### Créer un package {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### Prévisualiser un package {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### Faire une liste du contenu du package {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### Compiler un package {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### Réencapsuler un package {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### Renommer un package {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### Charger un package {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### Installer un package {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Désinstaller un package {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Supprimer un package {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Télécharger un package {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### Réplication d’un module {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### User Management {#user-management}

#### Créer un utilisateur ou une utilisatrice {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### Créer un groupe {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### Ajouter une propriété à un utilisateur ou une utilisatrice existant {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### Créer un utilisateur ou une utilisatrice avec un profil {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### Créer un utilisateur ou une utilisatrice en tant que membre d’un groupe {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### Ajouter un utilisateur ou une utilisatrice à un groupe {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Supprimer un utilisateur ou une utilisatrice d’un groupe {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Définir l’appartenance d’un utilisateur ou d’une utilisatrice à un groupe {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### Supprimer un utilisateur ou une utilisatrice {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### Supprimer un groupe {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### Sauvegarde {#backup}

Pour plus d’informations, consultez [Sauvegarde et restauration](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup).

### OSGi {#osgi}

#### Démarrer un bundle {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### Arrêter un bundle {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### Invalider le cache {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### Expulser le cache {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### Agent de réplication {#replication-agent}

#### Consulter le statut d’un agent {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### Supprimer un agent {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### Créer un agent {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### Mettre un agent en pause {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### Effacer une file d’attente d’agents {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### Communities {#communities}

#### Affecter et révoquer des badges {#assign-and-revoke-badges}

Pour plus d’informations, consultez [Notation et attribution de badges de Communautés](/help/communities/implementing-scoring.md#assign-and-revoke-badges).

Pour plus d’informations, consultez [Notions fondamentales sur la notation et l’attribution de badges](/help/communities/configure-scoring.md#example-setup).

#### Réindexation de MSRP {#msrp-reindexing}

Pour plus d’informations, consultez [MSRP – Fournisseur de ressources de stockage MongoDB](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command).

### Sécurité {#security}

#### Activer et désactiver CRX DE Lite {#enabling-and-disabling-crx-de-lite}

Pour plus d’informations, consultez [Activation de CRXDE Lite dans AEM](/help/sites-administering/enabling-crxde-lite.md).

### Nettoyage de la mémoire du magasin de données {#data-store-garbage-collection}

Pour plus d’informations, consultez [Nettoyage de la mémoire de magasin de données](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection).

### Intégration d’Analytics à Target {#analytics-and-target-integration}

Pour plus d’informations, consultez [Souscription à Adobe Analytics et Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script).

### Connexion unique {#single-sign-on}

#### Envoyer un en-tête de test {#send-test-header}

Pour plus d’informations, consultez [Authentification unique](/help/sites-deploying/single-sign-on.md).

## Commandes cURL d’AEM pour la manipulation de contenu courant {#common-content-manipulation-aem-curl-commands}

Voici une liste des commandes cURL d’AEM pour la manipulation de contenu.

>[!NOTE]
>
>Les exemples ci-dessous considèrent qu’AEM est exécuté sur `localhost` sur le port `4502` et utilise le nom d’utilisateur `admin` avec le mot de passe `admin`. D’autres espaces réservés aux commandes sont définis entre crochets.

### Gestion des pages {#page-management}

#### Activation des pages {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### Désactivation des pages {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### Activation d’une arborescence {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### Verrouillage de la page {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Déverrouiller la page {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Copie de la page {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### Comment effectuer un déploiement superficiel {#shallow-rollout}

Lorsque vous utilisez AEM as a Cloud Service, certaines instances nécessitent de déployer une seule page spécifique sans propager ses sous-pages. Si elle n’est pas configurée correctement, la commande curl standard pour déployer des pages peut inclure des sous-pages par inadvertance. Cette section décrit comment ajuster la commande curl pour réaliser un déploiement superficiel d’une page spécifiée et exclure toute sous-page supplémentaire.

Pour effectuer un déploiement superficiel, procédez comme suit :

1. Modifiez la commande curl existante en faisant passer le paramètre de `type=deep` à `type=page`.
1. Utilisez la syntaxe suivante pour la commande curl :

```shell
curl -H "Authorization: Bearer <token>" "https://<instance-url>/bin/asynccommand" \
   -d type=page \
   -d operation=asyncRollout \
   -d cmd=rollout \
   -d path="/content/<your-path>"
```

Vérifiez également les points suivants :

1. Veillez à remplacer `<token>` avec votre jeton d’autorisation réel et `<instance-url>` avec l’URL de votre instance spécifique.
1. Remplacez `/content/<your-path>` par le chemin d’accès de la page spécifique que vous souhaitez déployer.

En définissant `type=page`, la commande cible uniquement la page spécifiée, à l’exclusion des sous-pages. Ainsi, cette configuration permet un contrôle précis du déploiement du contenu, en s’assurant que seules les modifications prévues sont propagées dans les environnements. En outre, ce réglage s’aligne également sur la manière dont les déploiements sont gérés via l’interface d’utilisation d’AEM lors de la sélection de pages individuelles.

### Workflows {#workflows}

Pour plus d’informations, consultez [Interaction avec des workflows par programmation](/help/sites-developing/workflows-program-interaction.md).

### Contenu Sling {#sling-content}

#### Créer un dossier {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### Supprimer un nœud {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### Déplacer un nœud {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Copier un nœud {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Charger des fichiers à l’aide de Sling PostServlet {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### Charger des fichiers à l’aide de Sling PostServlet et spécifier le nom du nœud {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### Charger des fichiers en spécifiant un type de contenu {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### Manipulation des ressources {#asset-manipulation}

Pour plus d’informations, consultez [API Assets HTPP](/help/assets/mac-api-assets.md).
