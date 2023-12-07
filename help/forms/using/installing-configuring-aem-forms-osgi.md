---
title: Installer et configurer les fonctionnalités de capture de données
description: Installez et configurez les formulaires adaptatifs, les PDF forms et HTML5 Forms. Configurez Adobe Analytics et Adobe Target pour les formulaires adaptatifs afin d’analyser l’utilisation des formulaires et de cibler les utilisateurs en fonction de leur profil.
topic-tags: installing
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
role: Admin
exl-id: 19b5765e-50bc-4fed-8af5-f6bb464516c8
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 67%

---

# Installation et configuration des fonctionnalités de capture de données{#install-and-configure-data-capture-capabilities}

## Présentation {#introduction}

AEM Forms fournit un ensemble de formulaires pour obtenir des données de l’utilisateur final : formulaires adaptatifs, Forms HTML5 et PDF forms. Il fournit également des outils pour répertorier tous les formulaires disponibles sur une page web, analyser l’utilisation des formulaires et cibler les utilisateurs en fonction de leur profil. Ces fonctionnalités sont incluses dans le module complémentaire AEM Forms. Le module complémentaire est déployé sur une instance de création ou de publication d’AEM.

**Formulaires adaptatifs :** Ces formulaires changent l’aspect en fonction de la taille d’écran de l’appareil, sont attrayants et interactifs par nature. Adaptive Forms peut également s’intégrer à Adobe Analytics, Adobe Sign et Adobe Target. Il vous permet de fournir aux utilisateurs des formulaires personnalisés et des expériences orientées processus en fonction de leur démographie et d’autres fonctionnalités. Vous pouvez également intégrer des formulaires adaptatifs à Adobe Sign.

**PDF forms** sont adaptées à l’impression au pixel près et à la capture d’informations numériques dans un document PDF. Dans l’avatar numérique, vous pouvez utiliser Adobe Acrobat ou Acrobat Reader pour remplir ces formulaires. Vous pouvez héberger ces formulaires sur votre site web ou utiliser le portail de formulaires pour répertorier ces formulaires sur un site AEM. Vous pouvez également envoyer ces formulaires par courrier électronique à d’autres personnes en tant que pièces jointes. Ces formulaires sont mieux adaptés aux environnements de bureau.

**HTML5 Forms** sont la version de PDF forms compatible avec les navigateurs. HTML5 Forms convient aux environnements qui ne prennent pas en charge les modules externes de PDF. Les formulaires HTML5 permettent le rendu des formulaires basés sur XFA sur les appareils mobiles et les navigateurs de bureau ne prenant pas en charge les documents XFA en PDF. Ces formulaires sont mieux adaptés aux tablettes et aux environnements de bureau.

AEM Forms est une puissante plateforme de classe d’entreprise et la capture de données (formulaires adaptatifs, PDF forms et Forms HTML5) n’est qu’une des fonctionnalités d’AEM Forms. Pour obtenir la liste complète des fonctionnalités, voir [Présentation d’AEM Forms](/help/forms/using/introduction-aem-forms.md).

## Topologie de déploiement {#deployment-topology}

Le module complémentaire AEM Forms est une application déployée sur AEM. Vous n’avez besoin que d’un minimum d’une instance d’auteur AEM et d’AEM de publication pour exécuter les fonctionnalités de capture de données AEM Forms. La topologie suivante est suggérée pour exécuter les fonctionnalités de capture de données AEM Forms AEM Forms. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![recommened-topology](assets/recommended-topology.png)

## Configuration requise {#system-requirements}

Avant de commencer à installer et configurer la fonctionnalité de capture de données d’AEM Forms, assurez-vous que :

* Le matériel et l’infrastructure logicielle sont en place. Pour obtenir une liste détaillée des matériels et logiciels pris en charge, voir [Conditions techniques applicables](/help/sites-deploying/technical-requirements.md).

* Le chemin d’installation de l’instance AEM ne contient pas d’espaces.
* Une instance AEM est en cours d’exécution. Pour les utilisateurs de Windows, installez l’instance AEM en mode élevé. Dans la terminologie AEM, une « instance » est une copie d’AEM s’exécutant sur un serveur en mode de création ou de publication. Vous avez besoin d’au moins deux instances [AEM (une instance de création et une instance de publication)](/help/sites-deploying/deploy.md) pour exécuter les fonctionnalités de capture de données AEM Forms :

   * **Création** : instance AEM utilisée pour créer, télécharger et modifier du contenu et assurer l’administration du site web. Une fois que le contenu est publié, il est répliqué sur l’instance de publication.
   * **Publier**: instance d’AEM qui diffuse le contenu publié au public sur Internet ou sur un réseau interne.

* Les exigences de mémoire sont respectées. Le package complémentaire AEM Forms nécessite :

   * 15 Go d’espace temporaire pour les installations basées sur Microsoft Windows.
   * 6 Go d’espace temporaire pour les installations Unix.

* La réplication et la réplication inverse pour les instances de création et de publication sont définies. Pour plus d’informations, voir [Réplication](/help/sites-deploying/replication.md).
* Pour les systèmes UNIX :

   * Installez les packages 32 bits suivants à partir du support d’installation :

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>fontconfig</td>
   <td>freetype</td>
   <td>glibc</td>
  </tr>
  <tr>
   <td>libcurl</td>
   <td>libICE</td>
   <td>libicu</td>
   <td>libSM</td>
  </tr>
  <tr>
   <td>libuuid</td>
   <td>libX11</td>
   <td><p>libXau</p> </td>
   <td>libxcb</td>
  </tr>
  <tr>
   <td>libXext</td>
   <td>libXinerama</td>
   <td>libXrandr</td>
   <td>libXrender</td>
  </tr>
  <tr>
   <td>nss-softokn-freebl</td>
   <td>OpenSSL</td>
   <td>zlib</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Si OpenSSL est déjà installé sur le serveur, mettez-le à niveau vers la dernière version.
>* Créez les liens symboliques libcurl.so, libcrypto.so et libssl.so pointant vers la dernière version respective des bibliothèques libcurl, libcrypto et libssl.
>

* Installez le package 64 bits suivant à partir du support d’installation :

   * libicu

* Installez le [Package redistribuable Microsoft Visual Studio 2019 32 bits](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170).


## Installation du package complémentaire AEM Forms {#install-aem-forms-add-on-package}

Le module complémentaire AEM Forms est une application déployée sur AEM. Le package contient la capture de données AEM Forms et d’autres fonctionnalités. Suivez les étapes ci-après pour installer le package du module complémentaire :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Sélectionner **[!UICONTROL Adobe Experience Manager]** disponibles dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Sélectionnez le nom du package correspondant à votre système d’exploitation, puis sélectionnez **[!UICONTROL Accepter les termes du contrat de licence de l’utilisateur]**, puis sélectionnez **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

   Vous pouvez également télécharger le package via le lien direct répertorié dans l’article [Version d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
1. Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **Ne redémarrez pas immédiatement le serveur.** Avant de quitter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED cessent d’apparaître dans le fichier `[AEM-Installation-Directory]/crx-quickstart/logs/error.log` et que le journal soit stable.
1. Répétez les étapes 1 à 7 sur toutes les instances de création et de publication.

### (Windows uniquement) Installation automatique des redistribuables Visual Studio {#automatic-installation-visual-studio-redistributables}

Si vous installez une instance AEM en mode élevé, les packages redistribuables Visual Studio 32 bits sont installés automatiquement lors de l’installation du module complémentaire AEM Forms.

Pour évaluer si les redistribuables de Visual Studio sont installés automatiquement, ouvrez le fichier `error.log` accessible depuis le répertoire `/crx-repository/logs/`. Les journaux contiennent le message suivant :

`Redist <service name> already installed on system, will not attempt re-installation`

Si l’installation des redistributables échoue, les journaux contiennent le message suivant :

`Current user does not have elevated privileges, aborting installation of redist <service name>`

Pour résoudre ce problème, redémarrez le serveur AEM, installez AEM en mode élevé, puis installez le package complémentaire AEM Forms.

Si la vérification des privilèges échoue, les journaux contiennent le message suivant :

`Privilege escalation check failed with error: <error message>`

## Configurations post-installation {#post-installation-configurations}

AEM Forms comporte des configurations obligatoires et facultatives. Les configurations obligatoires incluent la configuration des bibliothèques BouncyCastle et de l’agent de sérialisation. Les configurations facultatives incluent la configuration du répartiteur, du portail de formulaires, d’Adobe Sign, d’Adobe Analytics et d’Adobe Target.

### Configurations post-installation obligatoires {#mandatory-post-installation-configurations}

#### Configuration des bibliothèques RSA et BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Pour déléguer le démarrage des bibliothèques, procédez comme suit sur toutes les instances dʼauteur et de publication :

1. Arrêtez l’instance AEM sous-jacente.
1. Ouvrez le fichier `[AEM installation directory]\crx-quickstart\conf\sling.properties` en mode d’édition.

   Si vous utilisez `[AEM installation directory]\crx-quickstart\bin\start.bat` pour démarrer AEM, modifiez le fichier sling.properties situé à l’emplacement `[AEM_root]\crx-quickstart\`.

1. Ajoutez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Enregistrez et fermez le fichier, puis démarrez l’instance AEM.
1. Répétez les étapes 1 à 4 sur toutes les instances de création et de publication.

#### Configurer l’agent de sérialisation {#configure-the-serialization-agent}

Pour autoriser le package, procédez comme suit sur toutes les instances dʼauteur et de publication :

1. Ouvrez AEM Configuration Manager dans une fenêtre de navigateur. L’URL par défaut est `https://'[server]:[port]'/system/console/configMgr`.
1. Recherchez **com.adobe.cq.deserfw.impl.DeserializationFirewallImpl.name** et ouvrez la configuration.
1. Ajoutez le package **sun.util.calendar** au champ **Placer sur la liste autorisée**. Cliquez sur **Enregistrer**.
1. Répétez les étapes 1 à 3 sur toutes les instances de création et de publication.

### Configurations facultatives après l’installation {#optional-post-installation-configurations}

#### La configuration de Dispatcher {#configure-dispatcher}

Dispatcher est l’outil de mise en cache et/ou d’équilibrage de charge d’Adobe Experience Manager, qui peut être utilisé conjointement avec un serveur web de niveau élevé. Si vous utilisez [Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html), effectuez les configurations suivantes pour AEM Forms :

1. Configurez l’accès à AEM Forms:

   Ouvrez le fichier dispatcher.any en mode d’édition. Accédez à la section des filtres et ajoutez le filtre suivant à la section des filtres :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Enregistrez et fermez le fichier. Pour plus d’informations sur les filtres, consultez la [documentation relative à Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Pour configurer le service de filtrage de référent, procédez comme suit :

   Connectez-vous au gestionnaire de configuration Apache Felix en tant qu’administrateur ou administratrice. L’URL par défaut du gestionnaire de configuration est `https://[server]:[port_number]/system/console/configMgr`. Dans le menu **Configurations**, sélectionnez l’option **Apache Sling Referrer Filter.** Dans le champ Allow Hosts, saisissez le nom d’hôte du répartiteur afin de l’activer comme référent et cliquez sur **Enregistrer**. Le format de l’entrée est `https://[server]:[port]`.

#### Configuration du cache {#configure-cache}

La mise en cache est un mécanisme qui permet de raccourcir les temps d’accès aux données, de réduire la latence et d’améliorer les vitesses d’entrée/sortie (E/S). Le cache de formulaires adaptatifs stocke uniquement le contenu de HTML et la structure JSON d’un formulaire adaptatif sans enregistrer de données préremplies. Cela permet de réduire le temps nécessaire au rendu d’un formulaire adaptatif.

* Lors de l’utilisation du cache de formulaires adaptatifs, utilisez la variable [AEM Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html) pour mettre en cache les bibliothèques clientes (CSS et JavaScript) d’un formulaire adaptatif.
* Lors du développement de composants personnalisés, gardez le cache de formulaires adaptatifs désactivé sur le serveur utilisé pour le développement.

Pour configurer la mise en cache des formulaires adaptatifs, procédez comme suit :

1. Accédez au gestionnaire de configuration de la console web AEM à l’adresse https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Cliquez sur la **configuration de canal web de communication interactive de formulaire adaptatif** pour éditer ses valeurs de configuration. Dans la boîte de dialogue Modifier les valeurs de configuration, spécifiez le nombre maximal de formulaires ou de documents qu’une instance du serveur AEM Forms peut mettre en cache le champ **Nombre de formulaires adaptatifs**. La valeur par défaut est 100. Cliquez sur **Enregistrer**.

   >[!NOTE]
   >
   >Pour désactiver le cache, définissez la valeur du champ Nombre de formulaires adaptatifs sur **0**. Le cache est réinitialisé, et tous les formulaires et documents sont supprimés du cache lorsque vous désactivez ou modifiez la configuration du cache.

#### Configuration de la communication SSL pour le modèle de données de formulaire {#configure-ssl-communcation-for-form-data-model}

Vous pouvez activer la communication SSL pour le modèle de données de formulaire. Pour activer la communication SSL pour le modèle de données de formulaire, avant de démarrer une instance AEM Forms, ajoutez des certificats au Trust Store Java de toutes les instances. Vous pouvez exécuter la commande ci-dessous pour ajouter les certificats :

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

#### Configuration d’Adobe Sign {#configure-adobe-sign}

Adobe Sign active les processus de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commercial, des ressources humaines, et bien d’autres domaines.

Dans un scénario Adobe Sign et de formulaires adaptatifs standard, un utilisateur remplit un formulaire adaptatif pour effectuer une **demande de service**. Par exemple, un formulaire de demande de carte bancaire et d’allocation. Lorsqu’un utilisateur ou une utilisatrice remplit, envoie et signe le formulaire de demande, le formulaire est envoyé au fournisseur de services pour qu’il effectue d’autres actions. Le fournisseur de services examine la demande et utilise Adobe Sign pour marquer la demande approuvée. Pour activer les processus de signature électronique similaires, vous pouvez intégrer Adobe Sign à AEM Forms.

Pour utiliser Adobe Sign avec AEM Forms, [Intégration d’Adobe Sign à AEM Forms](/help/forms/using/adobe-sign-integration-adaptive-forms.md).

#### Configuration d’Adobe Analytics {#configure-adobe-analytics}

AEM Forms s’intègre à Adobe Analytics qui vous permet de capturer et de suivre les mesures de performances des formulaires et documents que vous avez publiés. L’analyse de ces mesures contribue à une prise de décisions éclairée fondée sur les données, eu égard aux modifications requises pour concevoir des formulaires ou des documents plus faciles à utiliser.

Pour utiliser Adobe Analytics avec AEM Forms, voir [Configuration des analyses et des rapports](/help/forms/using/configure-analytics-forms-documents.md).

#### Intégrer Adobe Target {#integrate-adobe-target}

Vos clientes et clients sont susceptibles d’abandonner un formulaire si l’expérience qui en résulte n’est pas satisfaisante. Si elle est frustrante pour les clientes et clients, elle peut aussi bouleverser le volume et les coûts d’assistance de votre organisation. Il est essentiel et difficile d’identifier et de fournir l’expérience client appropriée qui augmente le taux de conversion. AEM Forms est la solution à ce problème.

AEM forms s’intègre à Adobe Target, une solution Adobe Marketing Cloud, pour offrir des expériences client personnalisées et attrayantes sur plusieurs canaux numériques. Pour utiliser Adobe Target avec des formulaires adaptatifs de test A/B, [intégrez Adobe Target à AEM Forms](/help/forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

## Étapes suivantes {#next-steps}

Vous avez configuré un environnement pour utiliser les fonctionnalités de capture de données AEM Forms. Les prochaines étapes pour utiliser cette fonctionnalité sont les suivantes :

* [Création de votre premier formulaire adaptatif](/help/forms/using/create-your-first-adaptive-form.md)
* [Création de votre premier formulaire PDF](https://www.adobe.com/go/learn_aemforms_designer_quick_start_65_fr)
* [Présentation des formulaires HTML5](/help/forms/using/introduction.md)
