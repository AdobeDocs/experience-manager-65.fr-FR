---
title: Installation et configuration d’un workflow basé sur l’utilisation de Forms sur OSGi
seo-title: Installation et configuration d’un workflow basé sur l’utilisation de Forms sur OSGi
description: Installez et configurez les communications interactives AEM Forms pour créer les correspondances commerciales, les documents, les déclarations, les avis, les courriers marketing, les factures et les kits de bienvenue.
seo-description: Installez et configurez les communications interactives AEM Forms pour créer les correspondances commerciales, les documents, les déclarations, les avis, les courriers marketing, les factures et les kits de bienvenue.
uuid: 1ceae822-215a-4b83-a562-4609a09c3a54
topic-tags: installing
discoiquuid: de292a19-07db-4ed3-b13a-7a2f1cd9e0dd
docset: aem65
role: Admin
exl-id: 4b24a38a-c1f0-4c81-bb3a-39ce2c4892b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 57%

---

# Installation et configuration d’un workflow basé sur l’utilisation de Forms sur OSGi{#installing-and-configuring-forms-centric-workflow-on-osgi}

## Présentation {#introduction}

Les entreprises collectent et traitent des données à partir de plusieurs formulaires, systèmes principaux et autres sources de données. Le traitement des données implique des procédures de révision et d’approbation, des tâches répétitives et l’archivage des données. Par exemple, la révision d’un formulaire et sa conversion en document PDF. Une fois cette opération effectuée manuellement, les tâches répétitives peuvent nécessiter beaucoup de temps et de ressources.

Vous pouvez utiliser [le processus basé sur Forms sur OSGi](../../forms/using/aem-forms-workflow.md) pour créer rapidement des processus basés sur des formulaires adaptatifs. Ces workflows peuvent vous aider à automatiser les workflows de révision et d’approbation, les workflows de processus d’entreprise et d’autres tâches répétitives. Ces processus permettent également de traiter des documents (créer, assembler, distribuer et archiver des documents PDF, ajouter des signatures numériques pour limiter l’accès aux documents, décoder des formulaires à code-barres, etc.) et utiliser le processus de signature Adobe Sign avec des formulaires et des documents.

Une fois configurés, ces processus peuvent être déclenchés manuellement pour terminer un processus défini ou s’exécuter par programmation lorsque les utilisateurs envoient un formulaire ou une communication interactive. Cette fonctionnalité est incluse dans le package du module complémentaire AEM Forms.

AEM Forms est une plate-forme d’entreprise performante. Le processus Forms sur OSGi n’est qu’une des fonctionnalités d’AEM Forms. Pour obtenir la liste complète des fonctionnalités, voir [Présentation d’AEM Forms](introduction-aem-forms.md).

>[!NOTE]
>
>Avec le processus basé sur l’utilisation de Forms sur OSGi, vous pouvez rapidement créer et déployer des processus pour différentes tâches sur la pile OSGi, sans avoir à installer la fonctionnalité Process Management complète sur la pile JEE. Voir une [comparaison](capabilities-osgi-jee-workflows.md) des processus d’AEM centrés sur Forms sur OSGi et de la gestion des processus sur JEE pour découvrir la différence et les similitudes dans les fonctionnalités.
>
>Après la comparaison, si vous choisissez d’installer la fonctionnalité Process Management sur la pile JEE, voir [Installation ou mise à niveau d’AEM Forms on JEE](/help/forms/home.md) pour plus d’informations sur l’installation et la configuration de la pile JEE et les fonctionnalités de Process Management.

## Topologie de déploiement {#deployment-topology}

Le package du module complémentaire AEM Forms est une application déployée sur AEM. Vous n’avez besoin que d’un minimum d’une instance de création ou de traitement AEM (auteur de production) pour exécuter la fonctionnalité de flux de travail Forms sur OSGi. Une instance de traitement est une instance [AEM Author](/help/forms/using/hardening-securing-aem-forms-environment.md) renforcée. N’effectuez aucune création réelle, comme la création de processus ou de formulaires adaptatifs, sur l’auteur de production.

La topologie suivante est une topologie indicative permettant d’exécuter les communications interactives AEM Forms, la gestion des correspondances, la capture de données AEM Forms et les fonctionnalités du processus basé sur l’utilisation de Forms sur OSGi. Pour plus d’informations sur la topologie, voir [Topologies d’architecture et de déploiement pour AEM Forms](/help/forms/using/aem-forms-architecture-deployment.md).

![recommandé-topology](assets/recommended-topology.png)

Le workflow Forms d’AEM Forms sur OSGi s’exécute AEM boîte de réception et AEM l’interface utilisateur de création de modèles de processus sur les instances d’auteur d’AEM Forms.

## Configuration requise {#system-requirements}

>[!NOTE]
>
>Passez à la section [Étapes suivantes](../../forms/using/installing-configuring-forms-centric-workflow-on-osgi.md#next-steps) du document, si vous avez déjà installé AEM Forms sur OSGi comme expliqué dans l’article [Installation et configuration des fonctionnalités de capture de données](../../forms/using/installing-configuring-aem-forms-osgi.md) .

Avant de commencer à installer et configurer le processus basé sur l’utilisation de Forms sur OSGi, assurez-vous que :

* Le matériel et l’infrastructure logicielle sont en place. Pour obtenir une liste détaillée des matériels et logiciels pris en charge, voir [Conditions techniques applicables](/help/sites-deploying/technical-requirements.md).

* Le chemin d’installation de l’instance AEM ne contient aucun espace blanc.
* Une instance AEM est en cours d’utilisation. Dans la terminologie AEM, une « instance » est une copie d’AEM s’exécutant sur un serveur en mode de création ou de publication. Vous avez besoin d’au moins une instance d’AEM (auteur ou traitement) pour exécuter le workflow Forms sur OSGi :

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

Le package du module complémentaire AEM Forms est une application déployée sur AEM. Le module contient un workflow centré sur Forms sur OSGi et d’autres fonctionnalités. Suivez les étapes ci-après pour installer le package du module complémentaire :

1. Ouvrez la [Distribution de logiciels](https://experience.adobe.com/downloads). Vous avez besoin d’un Adobe ID pour vous connecter à la Distribution de logiciels.
1. Appuyez sur **[!UICONTROL Adobe Experience Manager]** disponible dans le menu d’en-tête.
1. Dans la section **[!UICONTROL Filtres]** :
   1. Sélectionnez **[!UICONTROL Formulaires]** dans la liste déroulante **[!UICONTROL Solution]**.
   2. Sélectionnez la version et le type du package. Vous pouvez également utiliser l’option **[!UICONTROL Téléchargements de recherche]** pour filtrer les résultats.
1. Appuyez sur le nom du module approprié à votre système d’exploitation, sélectionnez **[!UICONTROL Accepter les termes du contrat de licence de l’utilisateur (EULA)]**, puis appuyez sur **[!UICONTROL Télécharger]**.
1. Ouvrez [Package Manager](https://docs.adobe.com/content/help/fr/experience-manager-65/administering/contentmanagement/package-manager.html) et cliquez sur **[!UICONTROL Télécharger le package]** pour télécharger le package.
1. Sélectionnez le package et cliquez sur **[!UICONTROL Installer]**.

   Vous pouvez également télécharger le package via le lien direct répertorié dans l’article [Versions d’AEM Forms](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html).

1. Une fois le package installé, vous êtes invité à redémarrer l’instance AEM. **Ne redémarrez pas immédiatement le serveur.** Avant d’arrêter le serveur AEM Forms, attendez que les messages ServiceEvent REGISTERED et ServiceEvent UNREGISTERED cessent d’apparaître dans le fichier  [AEM-Installation-Directory]/crx-quickstart/logs/error.log et que le journal soit stable.
1. Répétez les étapes 1 à 7 sur toutes les instances de création et de publication.

## Configurations post-installation {#post-installation-configurations}

AEM Forms comporte quelques configurations obligatoires et facultatives. Les configurations obligatoires incluent la configuration des bibliothèques BouncyCastle et de l’agent de sérialisation. Les configurations facultatives incluent la configuration du répartiteur et d’Adobe Target.

### Configurations post-installation obligatoires {#mandatory-post-installation-configurations}

#### Configuration des bibliothèques RSA et BouncyCastle  {#configure-rsa-and-bouncycastle-libraries}

Effectuez les étapes suivantes sur toutes les instances de création et de publication pour déléguer le démarrage des bibliothèques :

1. Arrêtez l’instance AEM sous-jacente.
1. Ouvrez le fichier [AEM répertoire d’installation]\crx-quickstart\conf\sling.properties pour le modifier.

   Si vous avez utilisé [AEM répertoire d’installation]\crx-quickstart\bin\start.bat pour démarrer AEM, modifiez le fichier sling.properties situé à l’adresse [racine_de_l’utilisateur ]\crx-quickstart\.

1. Ajoutez les propriétés suivantes au fichier sling.properties :

   ```shell
   sling.bootdelegation.class.com.rsa.jsafe.provider.JsafeJCE=com.rsa.*  
   ```

1. Enregistrez et fermez le fichier, puis démarrez l’instance AEM.
1. Répétez les étapes 1 à 4 sur toutes les instances de création et de publication.

#### Configurer l’agent de sérialisation {#configure-the-serialization-agent}

Effectuez les étapes suivantes sur toutes les instances de création et de publication pour ajouter le package à la liste autorisée :

1. Ouvrez AEM Configuration Manager dans une fenêtre de navigateur. L’URL par défaut est https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Recherchez et ouvrez la **configuration du pare-feu de désérialisation**.
1. Ajoutez le package **sun.util.calendar** au champ **liste autorisée**. Cliquez sur Enregistrer.
1. Répétez les étapes 1 à 3 sur toutes les instances de création et de publication.

### Configurations post-installation facultatives {#optional-post-installation-configurations}

#### La configuration de Dispatcher {#configure-dispatcher}

Le répartiteur est l’outil de mise en cache et d’équilibrage de charge pour AEM. Le répartiteur AEM aide également à protéger le serveur AEM des attaques.  Vous pouvez augmenter la sécurité de votre instance AEM en utilisant le répartiteur conjointement avec un serveur Web de niveau élevé. Si vous utilisez [Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher-configuration.html), effectuez les configurations suivantes pour AEM Forms :

1. Configurez l’accès à AEM Forms:

   Ouvrez le fichier dispatcher.any en mode d’édition. Accédez à la section des filtres et ajoutez le filtre suivant à la section des filtres :

   `/0025 { /type "allow" /glob "* /bin/xfaforms/submitaction*" } # to enable AEM Forms submission`

   Enregistrez et fermez le fichier. Pour des informations détaillées sur les filtres, voir la [documentation du répartiteur](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html).

1. Configurez le service de filtrage des référents :

   Connectez-vous à Configuration Manager d’Apache Felix en tant qu’administrateur. L’URL par défaut du gestionnaire de configuration est https://&#39;server&#39;:[port_number]/system/console/configMgr. Dans le menu **Configurations**, sélectionnez l’option **Apache Sling Referrer Filter.** Dans le champ Allow Hosts, saisissez le nom d’hôte du répartiteur afin de l’activer comme référent et cliquez sur **Enregistrer**. Le format de l’entrée est `https://'[server]:[port]'`.

#### Configuration du cache {#configure-cache}

La mise en cache est un mécanisme qui permet de raccourcir les temps d’accès aux données, réduire le temps de réponse et améliorer les vitesses d’entrée/sortie (E/S). Le cache de formulaires adaptatifs stocke uniquement le contenu HTML et la structure JSON d’un formulaire adaptatif sans enregistrer les données pré-renseignées. Cela permet de réduire le temps nécessaire pour effectuer le rendu d’un formulaire adaptatif.

* Lorsque vous utilisez le cache de formulaires adaptatifs, utilisez le [répartiteur AEM](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) pour mettre en cache les bibliothèques client (CSS et Javascript) d’un formulaire adaptatif. 
* Lors du développement des composants personnalisés, sur le serveur utilisé pour le développement, gardez le cache de formulaires adaptatifs désactivé.

Effectuez les étapes suivantes pour configurer le cache de formulaires adaptatifs :

1. Accédez à la page de configuration de la console web AEM à l’adresse `https://'[server]:[port]'/system/console/configMgr`.
1. Cliquez sur la **[!UICONTROL configuration de canal web de communication interactive de formulaire adaptatif]** pour éditer ses valeurs de configuration. Dans la boîte de dialogue Modifier les valeurs de configuration, indiquez le nombre maximal de formulaires ou documents qu’une instance du serveur AEM Forms peut mettre en cache dans le champ **Nombre de Forms adaptatives**. La valeur par défaut est 100. Cliquez sur **Enregistrer**.

   >[!NOTE]
   >
   >Pour désactiver le cache, définissez la valeur du champ Nombre de formulaires adaptatifs sur **0**. Le cache est réinitialisé, et tous les formulaires et documents sont supprimés du cache lorsque vous désactivez ou modifiez la configuration du cache.

#### Configuration d’Adobe Sign {#configure-adobe-sign}

Adobe Sign autorise les processus de signature électronique pour les formulaires adaptatifs. Les signatures électroniques améliorent les processus de traitement des documents pour les services juridiques, commercial, des ressources humaines, et bien d’autres domaines.

Dans un scénario standard de processus Adobe Sign et Forms sur OSGi, un utilisateur remplit un formulaire adaptatif à **demander un service**. Par exemple, un formulaire de demande de carte de paiement et d’allocation. Lorsqu’un utilisateur remplit, envoie et signe le formulaire de demande, un processus d’approbation/rejet est démarré. Le fournisseur de services examine la demande dans AEM boîte de réception et utilise Adobe Sign pour la signer électroniquement. Pour activer les processus de signature électronique similaires, vous pouvez intégrer Adobe Sign à AEM Forms.

Pour utiliser Adobe Sign avec AEM Forms, [intégrez Adobe Sign à AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

## Étapes suivantes {#next-steps}

Vous avez configuré un environnement pour utiliser le processus Forms sur les fonctionnalités OSGi. Les étapes d&#39;utilisation de cette fonctionnalité sont désormais les suivantes :

* [Utilisation d’un workflow basé sur l’utilisation de Forms sur OSGi](../../forms/using/aem-forms-workflow.md)
* [Référence sur les étapes de workflow](/help/sites-developing/workflows-step-ref.md)
* [Post-traitement des lettres et communications interactives](../../forms/using/submit-letter-topostprocess.md)
