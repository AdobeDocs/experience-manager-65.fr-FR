---
title: Installation et configuration des communications interactives
seo-title: Installation et configuration des communications interactives
description: Installez et configurez les communications interactives AEM Forms pour créer les correspondances commerciales, les documents, les déclarations, les avis, les courriers marketing, les factures et les kits de bienvenue.
seo-description: Installez et configurez les communications interactives AEM Forms pour créer les correspondances commerciales, les documents, les déclarations, les avis, les courriers marketing, les factures et les kits de bienvenue.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 78%

---


# Installation et configuration des communications interactives{#install-and-configure-interactive-communications}

## Présentation {#introduction}

AEM Form permet de centraliser la création, l’assemblage, la gestion et la diffusion de documents sécurisés et interactifs tels que les correspondances d’entreprise, les documents, les relevés, les avis d’avantages, les courriers marketing, les factures et les kits de bienvenue. Cette fonctionnalité est appelée communication interactive. Cette fonctionnalité est incluse dans le package du module complémentaire AEM Forms. Le package du module complémentaire est déployé sur une instance de création ou de publication d’AEM.

Vous pouvez utiliser la fonctionnalité de communication interactive pour produire une communication dans plusieurs formats, par exemple, Web et PDF. Vous pouvez intégrer la communication interactive au processus AEM pour traiter et fournir la communication assemblée aux clients sur le canal de leur choix. Par exemple, l’envoi d’une communication à l’utilisateur final par email.

If you are upgrading from a previous version and have already invested in correspondence management, you can install the [compatibility package](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) to continue using correspondence management. Pour plus d’informations sur les différences entre la communication interactive et la gestion des correspondances, voir [Présentation de la communication interactive](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms est une plate-forme d’entreprise performante. La communication interactive n’est que l’une des fonctionnalités d’AEM Forms. Pour obtenir la liste complète des fonctionnalités, voir [Présentation d’AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologie de déploiement {#deployment-topology}

Le package du module complémentaire AEM Forms est une application déployée sur AEM. Vous n’avez besoin que d’un minimum d’une instance AEM de création et de traitement pour exécuter la fonctionnalité de communication interactive. La topologie suivante est une topologie indicative permettant d’exécuter les communications interactives AEM Forms, la gestion des correspondances, la capture de données AEM Forms et les fonctionnalités du processus basé sur l’utilisation de Forms sur OSGi. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![topologie recommandée](assets/recommended-topology.png)

Les communications interactives AEM Forms exécutent les interfaces utilisateur d’administration, de création et d’agent sur les instances de création AEM Forms. Les instances de publication hébergent la version finale des communications interactives prêtes à être utilisées par les utilisateurs finaux.

## Configuration requise {#system-requirements}

Avant de commencer à installer et à configurer les capacités interactives de gestion des communications et de la correspondance des AEM Forms, assurez-vous que :

* Le matériel et l’infrastructure logicielle sont en place. Pour obtenir une liste détaillée des matériels et logiciels pris en charge, voir [Conditions techniques applicables](/help/sites-deploying/technical-requirements.md).

* Le chemin d’installation de l’instance AEM ne contient aucun espace blanc.
* Une instance AEM est en cours d’utilisation. Dans la terminologie AEM, une « instance » est une copie d’AEM s’exécutant sur un serveur en mode de création ou de publication. Vous avez besoin d’au moins une instance AEM (Auteur ou Traitement) pour exécuter les fonctionnalités AEM Forms de communication interactive et de gestion de correspondance :

   * **Création** : instance AEM utilisée pour créer, télécharger et modifier du contenu et assurer l’administration du site Web. Une fois que le contenu est publié, il est répliqué sur l’instance de publication.
   * **Traitement :** une instance de traitement est une instance [de création AEM sécurisée de manière renforcée](/help/forms/using/hardening-securing-aem-forms-environment.md). Vous pouvez configurer une instance de création et renforcer sa sécurité après avoir effectué l’installation.

   * **Publication** : instance AEM qui diffuse le contenu publié au public sur Internet ou sur un réseau interne.

* Les besoins en mémoire sont satisfaits. Le module complémentaire AEM Forms  nécessite :

   * 15 Go d’espace temporaire pour les installations Microsoft Windows.
   * 6 Go d’espace temporaire pour les installations Unix.

* Conditions supplémentaires pour les systèmes UNIX : si vous utilisez un système d’exploitation UNIX, installez les packages suivants des supports d’installation du système d’exploitation correspondant.

<table>
 <tbody>
  <tr>
   <td>expat</td>
   <td>libxcb</td>
   <td>freetype</td>
   <td>libXau</td>
  </tr>
  <tr>
   <td>libSM</td>
   <td>zlib</td>
   <td>libICE</td>
   <td>libuuid</td>
  </tr>
  <tr>
   <td>glibc</td>
   <td>libXext</td>
   <td><p>nss-softokn-freebl</p> </td>
   <td>fontconfig</td>
  </tr>
  <tr>
   <td>libX11</td>
   <td>libXrender</td>
   <td>libXrandr</td>
   <td>libXinerama</td>
  </tr>
 </tbody>
</table>

## Installation du module complémentaire AEM Forms {#install-aem-forms-add-on-package}

Le package du module complémentaire AEM Forms est une application déployée sur AEM. Le package contient des fonctionnalités AEM Forms de communication interactive, de gestion de la correspondance et d’autres fonctionnalités. Suivez les étapes ci-après pour installer le package du module complémentaire :

1. Connectez-vous au [serveur AEM](https://localhost:4502) en tant qu’administrateur, puis ouvrez le [partage de package](https://localhost:4502/crx/packageshare). Vous avez besoin d’un Adobe ID pour vous connecter au partage de package.
1. Dans le [partage de package AEM](https://localhost:4502/crx/packageshare/login.html), recherchez les **packages de modules complémentaires AEM 6.5 Forms** ou **les derniers Service Packs**, cliquez sur le package correspondant à votre système d’exploitation, puis sur **Télécharger**. Lisez et acceptez l’accord de licence, puis cliquez sur **OK**. Le téléchargement démarre. Une fois le téléchargement effectué, le mot **Téléchargé** apparaît en regard du package.

   Vous pouvez également utiliser le numéro de version pour rechercher un package de module complémentaire. Pour obtenir le numéro de version du dernier package, voir l’article [Versions AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html).

1. Une fois le téléchargement terminé, cliquez sur **Téléchargé**. Vous êtes redirigé vers le gestionnaire de package. Dans le gestionnaire de packages, recherchez le package téléchargé, puis cliquez sur **Installer**.

   Si vous téléchargez manuellement le package à l’aide du lien direct répertorié dans l’article [Versions AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html), connectez-vous au gestionnaire de package, cliquez sur **Télécharger le package**, sélectionnez le package téléchargé et cliquez sur Télécharger. Une fois le package téléchargé, cliquez sur son nom, puis sur **Installer**. 

1. Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **Ne redémarrez pas immédiatement le serveur.** Avant d’arrêter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED ne s’affichent plus dans le fichier [AEM-Installation-Directory]/crx-quickstart/logs/error.log et que le journal soit stable.
1. Répétez les étapes 1 à 4 sur toutes les instances de création et de publication.

## Configurations post-installation {#post-installation-configurations}

AEM Forms comporte quelques configurations obligatoires et facultatives. Les configurations obligatoires incluent la configuration des bibliothèques BouncyCastle et de l’agent de sérialisation. Les configurations facultatives incluent la configuration du répartiteur et d’Adobe Target.

### Configurations post-installation obligatoires {#mandatory-post-installation-configurations}

#### Configuration des bibliothèques RSA et BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Effectuez les étapes suivantes sur toutes les instances d’auteur et de publication pour démarrer et déléguer les bibliothèques :

1. Arrêtez l’instance AEM sous-jacente.
1. Open the [AEM installation directory]\crx-quickstart\conf\sling.properties file for editing.

   If you used [AEM installation directory]\crx-quickstart\bin\start.bat to start AEM, then edit the sling.properties located at [AEM_root]\crx-quickstart\.

1. Ajoutez les propriétés suivantes au fichier sling.properties :

   ```
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   sling.bootdelegation.class.org.bouncycastle.jce.provider.BouncyCastleProvider=org.bouncycastle.*
   ```

1. Enregistrez et fermez le fichier, puis démarrez l’instance AEM.
1. Répétez les étapes 1 à 4 sur toutes les instances de création et de publication.

#### Configurer l’agent de sérialisation {#configure-the-serialization-agent}

Effectuez les étapes suivantes sur toutes les instances d’auteur et de publication pour ajouter le package à la liste autorisée :

1. Ouvrez AEM Configuration Manager dans une fenêtre de navigateur. The default URL is https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez la **configuration du pare-feu de désérialisation**.
1. Add the **sun.util.calendar** package to the **allowlist** field. Cliquez sur Enregistrer.
1. Répétez les étapes 1 à 3 sur toutes les instances de création et de publication.

### Configurations post-installation facultatives {#optional-post-installation-configurations}

#### Installation du package de compatibilité {#install-compatibility-package}

La communication interactive est l’approche par défaut et recommandée pour créer des communications client dans AEM 6.5 Forms. Si vous avez mis à niveau ou migré depuis une version précédente et envisagez de continuer à utiliser des lettres (gestion des correspondances), installez le [package de compatibilité AEMFD](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/fd/AEM-FORMS-6.4-COMPAT).

Le package de compatibilité AEMFD vous permet d’utiliser les ressources suivantes d’AEM Forms 6.4, AEM Forms 6.3 et AEM Forms 6.2 sur AEM Forms 6.5 :

* Fragments de document
* Lettres
* Dictionnaires de données
* Modèles et pages des formulaires adaptatifs obsolètes

#### La configuration de Dispatcher {#configure-dispatcher}

Le répartiteur est l’outil de mise en cache et d’équilibrage de charge pour AEM. Le répartiteur AEM aide également à protéger le serveur AEM des attaques.  Vous pouvez augmenter la sécurité de votre instance AEM en utilisant le répartiteur conjointement avec un serveur Web de niveau élevé. If you use [Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html), then perform the following configurations for AEM Forms:

1. Configurez l’accès à AEM Forms:

   Ouvrez le fichier dispatcher.any en mode d’édition. Accédez à la section des filtres et ajoutez le filtre suivant à la section des filtres :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Enregistrez et fermez le fichier. Pour des informations détaillées sur les filtres, voir la [documentation du répartiteur](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configurez le service de filtrage des référents :

   Connectez-vous à Configuration Manager d’Apache Felix en tant qu’administrateur. The Default URL of the configuration manager is https://&#39;server&#39;:[port_number]/system/console/configMgr. Dans le menu **Configurations**, sélectionnez l’option **Apache Sling Referrer Filter.** Dans le champ Allow Hosts, saisissez le nom d’hôte du répartiteur afin de l’activer comme référent et cliquez sur **Enregistrer**. The format of the entry is https://&#39;[server]:[port]&#39;.

#### Intégration d’Adobe Target {#integrate-adobe-target}

Vos clients sont susceptibles d’abandonner une communication interactive si l’expérience qu’ils en font n’est pas satisfaisante. Si elle est frustrante pour les clients, elle peut aussi bouleverser le volume et les coûts d’assistance de votre entreprise. Il est difficile mais primordial d’identifier et d’offrir une bonne expérience client qui augmente le taux de conversion. AEM Forms détient la clé de ce problème.

AEM Forms s’intègre à Adobe Target, une solution Adobe Marketing Cloud, afin de fournir des expériences client personnalisées et attrayantes par le biais de plusieurs canaux numériques. Pour utiliser Adobe Target avec une communication interactive, [intégrez Adobe Target à AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configuration de la communication SSL pour le modèle de données de formulaire  {#configure-ssl-communcation-for-form-data-model}

Vous pouvez activer la communication SSL pour le modèle de données de formulaire. Pour activer la communication SSL pour le modèle de données de formulaire, avant de démarrer une instance AEM Forms, ajoutez des certificats au Trust Store Java de toutes les instances. Vous pouvez exécuter la commande suivante pour ajouter les certificats :

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Étapes suivantes {#next-steps}

Vous avez configuré un environnement pour qu’il utilise des fonctionnalités interactives de communication et de gestion de la correspondance. Maintenant, les prochaines étapes pour utiliser cette fonctionnalité sont les suivantes :

* [Présentation de la gestion des correspondances](/help/forms/using/interactive-communications-overview.md)

* [Créer une communication interactive](../../forms/using/create-interactive-communication.md)

* [Création d’une lettre de gestion de correspondances](../../forms/using/create-letter.md)

