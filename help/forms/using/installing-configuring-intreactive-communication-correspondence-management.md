---
title: Installation et configuration des communications interactives
seo-title: Install and configure Interactive Communications
description: Installez et configurez les communications interactives AEM Forms pour créer des correspondances commerciales, des documents, des déclarations, des avis de prestations, des courriers marketing, des factures et des kits de bienvenue.
seo-description: Install and configure AEM Forms Interactive Communications to create business correspondences, documents, statements, benefit notices, marketing mails, bills, and welcome kits.
uuid: 8acb7f68-0b52-4acd-97e2-af31c9408e8d
topic-tags: installing
discoiquuid: 225f2bc1-6842-4c79-a66d-8024a29325c0
docset: aem65
role: Admin
exl-id: 37fcfad9-2f84-4f0c-aed8-e4a5a3303a06
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 96%

---

# Installation et configuration des communications interactives{#install-and-configure-interactive-communications}

## Présentation {#introduction}

AEM Forms permet de centraliser la création, l’assemblage, la gestion et la diffusion de documents sécurisés et interactifs tels que des correspondances commerciales, des documents, des récapitulatifs, des avis de prestations, des courriers marketing, des factures et des kits de bienvenue. Cette fonctionnalité est appelée communication interactive. Cette fonctionnalité est incluse dans le package du module complémentaire AEM Forms. Le module complémentaire est déployé sur une instance de création ou de publication d’AEM.

Vous pouvez utiliser la fonctionnalité de communication interactive pour produire une communication dans plusieurs formats. Par exemple, les formats web et PDF. Vous pouvez intégrer la communication interactive au workflow d’AEM Workflow pour traiter et diffuser la communication assemblée aux clients et clientes sur le canal de leur choix. Par exemple, envoyer une communication à l’utilisateur final ou l’utilisatrice finale par e-mail.

Si vous effectuez une mise à niveau depuis une version précédente et que vous avez déjà investi dans la gestion des correspondances, vous pouvez installer le [package de compatibilité](../../forms/using/installing-configuring-intreactive-communication-correspondence-management.md#install-compatibility-package) pour continuer à utiliser la gestion des correspondances. Pour plus d’informations sur les différences entre la communication interactive et la gestion des correspondances, voir [Présentation de la communication interactive](/help/forms/using/interactive-communications-overview.md#interactive-communications-vs-correspondence-management).

AEM Forms est une plateforme d’entreprise performante. La communication interactive ne constitue que l’une des nombreuses fonctionnalités d’AEM Forms. Pour obtenir la liste complète des fonctionnalités, voir [Présentation d’AEM Forms](../../forms/using/introduction-aem-forms.md).

## Topologie de déploiement {#deployment-topology}

Le module complémentaire AEM Forms est une application déployée sur AEM. Vous avez juste besoin d’au moins une instance de création et de traitement AEM pour exécuter la fonctionnalité de communications interactives. La topologie suivante est fournie à titre indicatif pour exécuter les fonctionnalités de communications interactives AEM Forms, Correspondence Management, capture de données AEM Forms et des workflows basés sur des formulaires sur OSGi. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![recommended-topology](assets/recommended-topology.png)

Les communications interactives AEM Forms exécutent des interfaces utilisateur d’administration, de création et d’agent sur les instances de création AEM Forms. Les instances de publication hébergent la version finale des communications interactives prêtes à être utilisées par les utilisateurs finaux et les utilisatrices finales.

## Configuration requise {#system-requirements}

Avant de commencer à installer et à configurer les fonctionnalités de communication interactive et de gestion des correspondances d’AEM Forms, assurez-vous que :

* Le matériel et l’infrastructure logicielle sont en place. Pour obtenir une liste détaillée des matériels et logiciels pris en charge, voir [Conditions techniques applicables](/help/sites-deploying/technical-requirements.md).

* Le chemin d’installation de l’instance AEM ne contient pas d’espaces.
* Une instance AEM est en cours d’exécution. Dans la terminologie AEM, une « instance » est une copie d’AEM s’exécutant sur un serveur en mode de création ou de publication. Vous avez besoin d’au moins une instance d’AEM (auteur ou de traitement) pour exécuter les fonctionnalités de communication interactive et de gestion des correspondances d’AEM Forms :

   * **Création** : instance AEM utilisée pour créer, télécharger et modifier du contenu et assurer l’administration du site web. Une fois que le contenu est publié, il est répliqué sur l’instance de publication.
   * **Traitement :** une instance de [création AEM renforcée](/help/forms/using/hardening-securing-aem-forms-environment.md). Vous pouvez configurer une instance de création et renforcer sa sécurité après avoir effectué l’installation.

   * **Publication** : une instance AEM qui diffuse le contenu publié au public sur Internet ou sur un réseau interne.

* Les exigences de mémoire sont respectées. Le package complémentaire AEM Forms nécessite :

   * 15 Go d’espace temporaire pour les installations Microsoft® Windows.
   * 6 Go d’espace temporaire pour les installations Unix.

* Configuration requise supplémentaire pour les systèmes UNIX : si vous utilisez un système d’exploitation UNIX, installez les packages suivants à partir du support d’installation du système d’exploitation correspondant.

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

## Installation du package complémentaire AEM Forms {#install-aem-forms-add-on-package}

Le module complémentaire AEM Forms est une application déployée sur AEM. Le package contient la communication interactive AEM Forms, la gestion des correspondances et d’autres fonctionnalités. Suivez les étapes ci-après pour installer le package du module complémentaire :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Sélectionner **[!UICONTROL Adobe Experience Manager]** disponibles dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Forms]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Rechercher des téléchargements]** pour filtrer les résultats.
1. Sélectionnez le nom du package correspondant à votre système d’exploitation, puis sélectionnez **[!UICONTROL Accepter les termes du contrat de licence de l’utilisateur]**, puis sélectionnez **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

   Vous pouvez également télécharger le package via le lien direct répertorié dans l’article [Version d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

1. Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **Ne redémarrez pas immédiatement le serveur.** Avant d’arrêter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED and ServiceEvent UNREGISTERED cessent d’apparaître dans le fichier [AEM-Installation-Directory]/crx-quickstart/logs/error.log et que le journal soit stable.
1. Répétez les étapes 1 à 7 sur toutes les instances de création et de publication.

## Configurations post-installation {#post-installation-configurations}

AEM Forms comporte des configurations obligatoires et facultatives. Les configurations obligatoires incluent la configuration des bibliothèques BouncyCastle et de l’agent de sérialisation. Les configurations facultatives incluent la configuration de Dispatcher et d’Adobe Target.

### Configurations post-installation obligatoires {#mandatory-post-installation-configurations}

#### Configuration des bibliothèques RSA et BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Pour déléguer le démarrage des bibliothèques, procédez comme suit sur toutes les instances dʼauteur et de publication :

1. Arrêtez l’instance AEM sous-jacente.
1. Ouvrez le fichier [répertoire d’installation AEM]\crx-quickstart\conf\sling.properties pour le modifier.

   Si vous utilisiez [AEM installation directory]\crx-quickstart\bin\start.bat pour démarrer AEM, modifiez le fichier sling.properties à [AEM_root]\crx-quickstart\.

1. Ajoutez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*
   ```

1. Enregistrez et fermez le fichier, puis démarrez l’instance AEM.
1. Répétez les étapes 1 à 4 sur toutes les instances de création et de publication.

#### Configurer l’agent de sérialisation {#configure-the-serialization-agent}

Pour autoriser le package, procédez comme suit sur toutes les instances dʼauteur et de publication :

1. Ouvrez AEM Configuration Manager dans une fenêtre de navigateur. L’URL par défaut est https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez la **configuration du pare-feu de désérialisation**.
1. Ajoutez le package **sun.util.calendar** au champ **Placer sur la liste autorisée**. Cliquez sur Enregistrer.
1. Répétez les étapes 1 à 3 sur toutes les instances de création et de publication.

### Configurations facultatives après l’installation {#optional-post-installation-configurations}

#### Installer le package de compatibilité {#install-compatibility-package}

La communication interactive est l’approche par défaut et recommandée pour créer des communications client dans AEM 6.5 Forms. Si vous avez mis à niveau ou migré depuis une version précédente et envisagez de continuer à utiliser des lettres (gestion des correspondances), installez le [package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-65/forms/upgrade-aem-forms/aem-forms-osgi-upgrade/compatibility-package.html?lang=fr).

Le package de compatibilité AEMFD vous permet d’utiliser les ressources suivantes d’AEM 6.4 Forms, AEM 6.3 Forms et d’Forms 6.2 d’6.5 Forms :

* Fragments de document
* Lettres
* Dictionnaires de données
* Modèles et pages obsolètes de formulaires adaptatifs

#### La configuration de Dispatcher {#configure-dispatcher}

Le Dispatcher est l’outil de mise en cache et d’équilibrage de charge d’Adobe Experience Manager, qui peut être utilisé conjointement avec un serveur web d’entreprise. Si vous utilisez [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr), effectuez les configurations suivantes pour AEM Forms :

1. Configurez l’accès à AEM Forms:

   Ouvrez le fichier dispatcher.any en mode d’édition. Accédez à la section des filtres et ajoutez le filtre suivant à la section des filtres :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Enregistrez et fermez le fichier. Pour plus d’informations sur les filtres, consultez la [documentation relative à Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=fr).

1. Pour configurer le service de filtrage de référent, procédez comme suit :

   Connectez-vous au gestionnaire de configuration Apache Felix en tant qu’administrateur ou administratrice. L’URL par défaut du gestionnaire de configuration est https://&#39;server&#39;:[port_number]/system/console/configMgr. Dans le menu **Configurations**, sélectionnez l’option **Apache Sling Referrer Filter.** Dans le champ Autoriser des hôtes, saisissez le nom d’hôte du Dispatcher afin de l’activer comme référent, puis cliquez sur **Enregistrer**. Le format de l’entrée est https://&#39;[server]:[port]&#39;.

#### Intégrer Adobe Target {#integrate-adobe-target}

Vos clients et clientes pourraient abandonner une communication interactive si l’expérience qu’elle offre n’est pas captivante. En plus d’être frustrante pour les clients et les clientes, cette situation augmente également le volume et le coût de l’assistance pour votre entreprise. Il est essentiel et difficile d’identifier et de fournir l’expérience client appropriée qui augmente le taux de conversion. AEM Forms est la solution à ce problème.

AEM Forms s’intègre à Adobe Target, une solution Adobe Experience Cloud, pour offrir des expériences client personnalisées et attrayantes sur plusieurs canaux numériques. Pour utiliser Adobe Target avec une communication interactive, [intégrez Adobe Target à AEM Forms](../../forms/using/ab-testing-adaptive-forms.md#setupandintegratetargetinaemforms).

#### Configurer la communication SSL pour le modèle de données de formulaire  {#configure-ssl-communcation-for-form-data-model}

Vous pouvez activer la communication SSL pour le modèle de données de formulaire. Pour activer la communication SSL pour le modèle de données de formulaire, avant de démarrer une instance AEM Forms, ajoutez des certificats au Trust Store Java™ de toutes les instances. Vous pouvez exécuter la commande ci-dessous pour ajouter les certificats :

`keytool -import -alias <alias-name> -file <pathTo .cer certificate file> -keystore <<pathToJRE>\lib\security\cacerts>`

## Étapes suivantes {#next-steps}

Vous avez configuré un environnement pour utiliser les fonctionnalités de communication interactive et de gestion de la correspondance. Maintenant, les prochaines étapes pour utiliser cette fonctionnalité sont les suivantes :

* [Présentation de la gestion des correspondances](/help/forms/using/interactive-communications-overview.md)

* [Création d’une communication interactive](../../forms/using/create-interactive-communication.md)

* [Création d’une lettre de gestion de correspondances](../../forms/using/create-letter.md)
