---
title: Exigences techniques
description: Liste des plateformes client et serveur prises en charge pour Adobe Experience Manager.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '3498'
ht-degree: 58%

---

# Exigences techniques {#technical-requirements}

Adobe prend en charge (AEM) Adobe Experience Manager sur les plateformes, comme décrit dans les informations suivantes de ce document.

Pour tout problème lié à la plateforme, contactez le fournisseur de la plateforme.

>[!NOTE]
>
>Selon la plateforme sur laquelle vous installez AEM, il peut y avoir différents ensembles d’exigences pour la gestion des utilisateurs et des utilisatrices.

## Prérequis {#prerequisites}

Configuration minimale requise pour installer Adobe Experience Manager :

* Installation de Java™ Platform, Standard Edition JDK ou autre prise en charge [Machines virtuelles Java™](#java-virtual-machines)
* Fichier de démarrage rapide d’Experience Manager (JAR autonome ou WAR de déploiement de l’application web)

### Configuration minimale requise en matière d’espace disque et de mémoire {#minimum-sizing-requirements}

Configuration minimale requise pour exécuter Adobe Experience Manager :

* 5 Go d’espace disque disponible dans le répertoire d’installation
* Mémoire de 2 Go

>[!NOTE]
>
>* Les cas d’utilisation des ressources numériques nécessitent davantage de mémoire de base. Voir [Déploiement et maintenance](/help/sites-deploying/deploy.md#default-local-install) pour plus d’informations.
>* [Le package complémentaire AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) nécessite 15 Go d’espace temporaire.
>


Pour plus d’informations, voir [Consignes de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md).

### Niveaux de prise en charge {#support-levels}

Ce document répertorie les plateformes clientes et serveur prises en charge pour Adobe Experience Manager. Adobe fournit plusieurs niveaux de prise en charge, tant pour les configurations recommandées que pour les autres.

### Configurations prises en charge {#supported-configurations}

Adobe recommande ces configurations et fournit une prise en charge complète dans le cadre du contrat de maintenance logicielle standard.

<table>
 <tbody>
  <tr>
   <td>Niveau de prise en charge</td>
   <td>Description<br /> </td>
  </tr>
  <tr>
   <td><strong>A : pris en charge</strong></td>
   <td>Adobe fournit une prise en charge et une maintenance complètes de cette configuration. Cette configuration est couverte par le processus d’assurance qualité d’Adobe.</td>
  </tr>
  <tr>
   <td><strong>R : Prise en charge limitée </strong></td>
   <td>Pour garantir la réussite des projets des clients, Adobe fournit une prise en charge complète dans le cadre d’un programme de prise en charge limité, qui nécessite que des conditions spécifiques soient remplies. La prise en charge au niveau R nécessite une requête formelle de la part du client ou de la cliente et une confirmation par Adobe. Pour plus d’informations, contactez l’assistance clientèle d’Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurations non prises en charge {#unsupported-configurations}

| Niveau de prise en charge | Description |
|---|---|
| **Z : non pris en charge** | La configuration n’est pas prise en charge. Adobe ne fait pas d’instructions indiquant si la configuration fonctionne et ne la prend pas en charge. |

## Plateformes prises en charge {#supported-platforms}

### Machines virtuelles Java™ {#java-virtual-machines}

L’application nécessite l’exécution d’une machine virtuelle Java™, fournie par la distribution Java™ Development Kit (JDK).

Adobe Experience Manager fonctionne avec les versions suivantes des machines virtuelles Java™ :

>[!CAUTION]
>
>Suivez les bulletins de sécurité publiés par le fournisseur Java™. Cela garantit la sécurité des environnements de production. Installez toujours les mises à jour Java™ les plus récentes.

| **Plateforme** | **Niveau de prise en charge** | **Lien** |
|---|---|---|
| Oracle Java™ SE 11 JDK - 64 bits | A : pris en charge `[1]` | [Télécharger](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java™ SE 10 JDK | Z : non pris en charge `[1]` |
| Oracle Java™ SE 9 JDK | Z : non pris en charge `[1]` |
| Oracle Java™ SE 8 JDK - 64 bits | A : pris en charge `[1]` | [Télécharger](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9 VM - build 2.9, JRE 1.8.0 | A : pris en charge de `[2]` |
| IBM® J9 VM - build 2.8, JRE 1.8.0 | A : pris en charge de `[2]` |
| Azul Zulu OpenJDK 11 - 64 bits | A : pris en charge de `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 bits | A : pris en charge de `[3]` |  |

1. Oracle est passé à un modèle &quot;Long Term Support&quot; (LTS) pour les produits Oracle Java™ SE. Java™ 9, Java™ 10 et Java™ 12 sont des versions non-LTS par Oracle (voir [Feuille de route du support Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Pour déployer AEM dans un environnement d’exploitation, Adobe assure uniquement la prise en charge des versions LTS de Java™. La prise en charge et la distribution du JDK Oracle Java™ SE, y compris toutes les mises à jour de maintenance des versions LTS au-delà de la fin des mises à jour publiques, sont directement prises en charge par Adobe pour tous les clients AEM qui utilisent la technologie Oracle Java™ SE. Voir [Stratégie de prise en charge de Java™ pour Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Important : Java™ 11 est pris en charge jusqu’en septembre 2026 au minimum.**

1. IBM® JRE est uniquement pris en charge avec WebSphere® Application Server.

1. Les versions LTS OpenJDK Azul Zulu sont prises en charge pour les déploiements d’AEM sur site commençant par la version 6.5 SP9. La prise en charge et la distribution des versions du JDK LTS Azul Zulu doivent être autorisées directement depuis Azul par les clients Adobe.


### Stockage et persistance {#storage-persistence}

Il existe différentes options pour déployer le référentiel d’Adobe Experience Manager. Consultez la liste suivante pour connaître les technologies et les options de stockage prises en charge.

| **Plateforme** | **Description** | **Niveau de prise en charge** |
|---|---|---|
| **Système de fichiers avec fichiers TAR** `[1]` | Référentiel | A : pris en charge |
| **Système de fichiers avec le magasin de données** `[1]` | Binaires | A : pris en charge |
| Stockage de binaires dans des fichiers TAR sur le système de fichiers `[1]` | Binaires | Z : Non pris en charge pour la production |
| Amazon S3 | Binaires | A : pris en charge |
| Stockage d’objets blob Microsoft® Azure. | Binaires | A : pris en charge |
| MongoDB Enterprise 4.4 | Référentiel | A : pris en charge `[2, 3, 4]` |
| MongoDB Enterprise 4.2  | Référentiel | A : pris en charge `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Référentiel | Z : non pris en charge |
| MongoDB Enterprise 3.6 | Référentiel | Z : non pris en charge |
| MongoDB Enterprise 3.4 | Référentiel | Z : non pris en charge |
| IBM® DB2® 10.5 | Référentiel et base de données Forms | R : prise en charge limitée `[5]` |
| Oracle Database 12c (12.1.x) | Référentiel et base de données Forms | R : prise en charge limitée  |
| Microsoft® SQL Server 2016 | Base de données Forms | A : pris en charge |
| **Apache Lucene (démarrage rapide intégré)** | Service de recherche | A : pris en charge |
| Apache Solr | Service de recherche | A : pris en charge |

1. Le système de fichiers comprend le stockage de bloc compatible avec POSIX. Inclut la technologie de stockage réseau. Gardez à l’esprit que les performances du système de fichiers peuvent varier et avoir une incidence sur les performances globales. Chargez l’AEM de test avec le système de fichiers réseau/distant.
1. MongoDB Enterprise versions 4.2 et 4.4 nécessitent AEM 6.5 SP9 au minimum.
1. La fragmentation MongoDB n’est pas prise en charge dans AEM.
1. Seul le moteur de stockage WiredTiger de MongoDB est pris en charge.
1. Pris en charge pour les clients et clientes de mise à niveau d’AEM Forms. Non pris en charge pour les nouvelles installations.

>[!NOTE]
Consultez la section [Déploiement de Communities](/help/communities/deploy-communities.md) pour plus d’informations sur les fonctionnalités d’AEM Communities.

>[!NOTE]
MongoDB est un logiciel tiers non inclus dans le package de licence d’AEM. Pour plus d’informations, voir [Politique de licence MongoDB](https://www.mongodb.com/community/licensing) page.
Pour tirer pleinement parti de votre déploiement AEM avec MongoDB, Adobe conseille d’utiliser la version MongoDB Enterprise sous licence afin de bénéficier d’une assistance professionnelle. Consultez la section [Déploiements recommandées](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) pour plus d’informations.
La licence comprend un ensemble de répliques, composé d’une instance principale et de deux instances secondaires qui peuvent être utilisées pour les déploiements de création ou de publication.
Si vous souhaitez exécuter les instances de création et de publication sur MongoDB, deux licences distinctes doivent être achetées.
L’assistance clientèle d’Adobe aide à résoudre les problèmes admissibles liés à l’utilisation de MongoDB avec AEM.
Pour plus d’informations, consultez la page [MongoDB pour Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
Les bases de données relationnelles prises en charge, telles que répertoriées ci-dessus, sont des logiciels tiers qui ne sont pas inclus dans le package de licence d’AEM.
Pour exécuter AEM 6.5 avec une base de données relationnelle prise en charge, un contrat d’assistance distinct auprès d’un fournisseur de base de données est requis. L’assistance clientèle d’Adobe aide à résoudre les problèmes admissibles liés à l’utilisation des bases de données relationnelles avec AEM 6.5.
**La plupart des bases de données relationnelles sont actuellement prises en charge au niveau R sur AEM 6.5, qui comprend des critères et un programme de prise en charge, comme indiqué dans la description du niveau R ci-dessus.**

### Moteurs de servlet/serveurs d’applications {#servlet-engines-application-servers}

Adobe Experience Manager peut s’exécuter en tant que serveur autonome (fichier JAR de démarrage rapide) ou en tant qu’application web dans un serveur d’applications tiers (fichier WAR).

La version minimale requise de l’API servlet est Servlet 3.1.

| Plateforme | Niveau de prise en charge |
|---|---|
| **Moteur de servlet intégré à démarrage rapide (Jetty 9.4)** | A : pris en charge |
| Oracle WebLogic Server 12.2 (12cR2) | Z : non pris en charge |
| IBM® WebSphere® Application Server (LibertyProfile) avec profil Web 7.0 et IBM® JRE 1.8 | R : prise en charge restreinte des nouveaux contrats `[2]` |
| IBM® WebSphere® Application Server 9.0 et IBM® JRE 1.8 | R : prise en charge restreinte des nouveaux contrats `[1]` `[2]` |
| Apache Tomcat 8.5.x | R : prise en charge restreinte des nouveaux contrats `[2]` |
| JBoss® EAP 7.2.x avec JBoss® Application Server | Z : non pris en charge |
| JBoss® EAP 7.1.4 avec JBoss® Application Server | R : prise en charge restreinte des nouveaux contrats `[1]` `[2]` |
| JBoss® EAP 7.0.x avec JBoss® Application Server | Z : non pris en charge |

1. Recommandé pour les déploiements avec AEM Forms.
1. Avec les déploiements d’AEM 6.5 sur les serveurs d’applications, la prise en charge limitée sera activée. Les clientes et clients existant(e)s peuvent effectuer une mise à niveau vers AEM 6.5 et continuer à utiliser des serveurs d’applications. Pour les nouveaux clients, il s’accompagne de critères de prise en charge et d’un programme de prise en charge, comme indiqué dans la description du niveau R ci-dessus.

### Systèmes d’exploitation de serveur {#server-operating-systems}

Adobe Experience Manager fonctionne avec les plateformes de serveur suivantes pour les environnements de production :

| **Plateforme** | **Niveau de prise en charge** |
|---|---|
| **Linux®, basé sur la distribution Red Hat®** | A : pris en charge `[1]` `[3]` |
| Linux®, selon la distribution Debian y compris. Ubuntu  | A : pris en charge `[1]` `[2]` |
| Linux®, selon la distribution SUSE® | A : pris en charge de `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R : prise en charge restreinte des nouveaux contrats `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R : prise en charge restreinte des nouveaux contrats `[5]` |
| Microsoft® Windows Server 2012 R2 | Z : non pris en charge |
| Oracle Solaris™ 11 | Z : non pris en charge |
| IBM® AIX® 7.2 | Z : non pris en charge |

1. Linux® Kernel 2.6, 3. x, 4. x, et 5. x comprend les dérivés de la distribution Red Hat®, notamment Red Hat® Enterprise Linux®, CentOS, Oracle Linux® et Amazon Linux®. Les fonctions de module complémentaire AEM Forms sont uniquement prises en charge sur CentOS 7, Red Hat® Enterprise Linux® 7, Red Hat® Enterprise Linux® 8 et Red Hat® Enterprise Linux® 9.
1. AEM Forms est pris en charge sur Ubuntu 20.04 LTS.
1. Distribution Linux® prise en charge par Adobe Managed Services.
1. Les déploiements de production Windows Microsoft® sont pris en charge pour les clients effectuant une mise à niveau vers la version 6.5 et pour les utilisateurs n’utilisant pas la production. Les nouveaux déploiements sont à la demande pour AEM Sites et Assets.
1. AEM Forms est pris en charge sur Microsoft® Window Server sans les restrictions de niveau de prise en charge R.

>[!NOTE]
Si vous installez AEM Forms 6.5, assurez-vous d’avoir installé le redistribuable Microsoft® Visual C++ 32 bits suivant.
* Redistribuable Microsoft® Visual C++ 2008
* Redistribuable Microsoft® Visual C++ 2010
* Redistribuable Microsoft® Visual C++ 2012
* Redistribuable Microsoft® Visual C++ 2013 (à partir de la version 6.5)



### Environnements virtuels et de cloud computing {#virtual-cloud-computing-environments}

Adobe Experience Manager est pris en charge dans le cadre d’une exécution sur une machine virtuelle dans des environnements de cloud computing. Ces environnements incluent en tant que Microsoft® Azure et Amazon Web Services (AWS), s’exécutant conformément aux exigences techniques répertoriées sur cette page et conformément aux conditions de prise en charge standard d’Adobe.

Pour un environnement natif dans le cloud, passez en revue la dernière offre de la gamme de produits AEM : Adobe Experience Manager as a Cloud Service. Consultez la [Documentation d’Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=fr) pour plus d’informations.

Adobe propose également l’utilisation d’Adobe Managed Services pour déployer AEM sur Azure ou AWS. Adobe Managed Services fournit aux experts les compétences nécessaires pour déployer et utiliser AEM dans ces environnements de cloud computing. Consultez les [documents complémentaires sur Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

Dans tous les autres cas de déploiement d’AEM sur Azure ou AWS, ou tout autre environnement de cloud computing, la prise en charge d’Adobe se limite à l’environnement informatique virtuel. Cet environnement virtuel doit être exécuté conformément aux spécifications techniques répertoriées sur cette page. Tout problème signalé relatif à l’AEM s’exécutant dans l’un de ces environnements cloud doit être reproductible indépendamment de tout service cloud spécifique à l’environnement de cloud computing. En d’autres termes, sauf si le service cloud est pris en charge dans le cadre des exigences techniques répertoriées sur cette page, par exemple le stockage Azure Blob ou AWS S3.

Pour obtenir des recommandations sur le déploiement d’AEM sur Azure ou AWS, en dehors d’Adobe Managed Services, Adobe recommande de travailler directement avec le fournisseur de cloud. Vous pouvez également travailler avec des partenaires d’Adobe pour prendre en charge le déploiement d’AEM dans l’environnement cloud de votre choix. Le fournisseur ou partenaire cloud sélectionné est responsable du dimensionnement, de la conception et de l’implémentation de l’architecture, afin de répondre à vos besoins spécifiques en termes de performances, de charge, d’évolutivité et de sécurité.

### Plateformes de Dispatcher (serveurs web) {#dispatcher-platforms-web-servers}

Dispatcher est le composant de mise en cache et d’équilibrage de charge. [Téléchargez la dernière version de Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=en). Experience Manager 6.5 nécessite la version 4.3.2 ou une version ultérieure du Dispatcher.

Les serveurs web suivants sont pris en charge pour une utilisation avec Dispatcher version 4.3.2 :

| Plateforme | Niveau de prise en charge |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A : pris en charge |
| Microsoft® IIS 10 (serveur d&#39;informations Internet) | A : pris en charge |
| Microsoft® IIS 8.5 (serveur d&#39;informations Internet) | Z : non pris en charge |

1. Les serveurs web créés à partir du code source Apache httpd prennent autant en charge que la version de httpd sur laquelle ils sont basés. En cas de doute, demandez à Adobe de confirmer le niveau de prise en charge relatif au produit serveur correspondant. Différents cas de figure :

   1. Le serveur HTTP a été créé en utilisant uniquement les distributions source Apache officielles, ou
   1. Le serveur HTTP a été livré dans le cadre du système d’exploitation sur lequel il est exécuté. Exemples : Serveur HTTP IBM®, serveur HTTP Oracle

1. Dispatcher n’est pas disponible pour Apache 2.4.x pour les systèmes d’exploitation Windows.

## Plateformes clientes prises en charge {#supported-client-platforms}

### Navigateurs pris en charge pour l’interface utilisateur de création {#supported-browsers-for-authoring-user-interface}

L’interface utilisateur d’Adobe Experience Manager fonctionne avec les plates-formes clientes suivantes : Tous les navigateurs sont testés avec l’ensemble par défaut de plug-ins et de modules complémentaires.

L’interface utilisateur d’AEM est optimisée pour les grands écrans (généralement les notebooks et les ordinateurs de bureau) et le format de tablette (par exemple Apple iPad ou Microsoft® Surface). Le format de téléphone n’est pas pris en charge.

>[!NOTE]
**Prise en charge des navigateurs avec des cycles de version rapides :**
La version Mozilla Firefox, Google Chrome et Microsoft® Edge est mise à jour tous les quelques mois. Adobe s’engage à fournir des mises à jour pour qu’Adobe Experience Manager conserve le niveau de prise en charge, comme indiqué ci-dessous avec les versions à venir de ces navigateurs.

<table>
 <tbody>
  <tr>
   <td><strong>Navigateur</strong></td>
   <td><strong>Prise en charge de l’interface utilisateur<br /> </strong></td>
   <td><strong>Prise en charge de l’interface utilisateur classique</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z : non pris en charge</td>
   <td>Z : non pris en charge</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Mozilla Firefox, dernier ESR [1]</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Apple Safari sous macOS (Evergreen)</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x sous macOS</td>
   <td>Z : non pris en charge</td>
   <td>Z : non pris en charge</td>
  </tr>
  <tr>
   <td>Apple Safari sur iOS 12.x</td>
   <td>A : pris en charge [2]</td>
   <td>Z : non pris en charge</td>
  </tr>
  <tr>
   <td>Apple Safari sur iOS 11.x</td>
   <td>Z : non pris en charge</td>
   <td>Z : non pris en charge</td>
  </tr>
 </tbody>
</table>

1. Version de prise en charge étendue de Firefox [En savoir plus sur mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. Prise en charge d’Apple iPad

### Navigateurs pris en charge pour les sites web {#supported-browsers-for-websites}

En règle générale, la prise en charge des navigateurs pour les sites web rendus par AEM Sites dépend de l’implémentation des modèles de page d’AEM, de la conception et de la sortie des composants, et relève donc de celui ou celle qui met en œuvre ces parties.

### Clients et clientes WebDAV {#webdav-clients}

**Microsoft® Windows 7+**

Lors de la connexion à Microsoft® Windows 7+ à une instance AEM non sécurisée avec SSL, l’authentification de base sur un réseau non sécurisé doit être activée sous Windows. Il nécessite une modification du registre Windows du WebClient :

1. Recherchez la sous-clé de registre :

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Ajoutez l’entrée de registre BasicAuthLevel à cette sous-clé à l’aide d’une valeur de 2 ou plus.

## Remarques supplémentaires sur Platform {#additional-platform-notes}

Cette section contient des notes spéciales et des informations plus détaillées sur l’exécution d’Adobe Experience Manager et de ses modules complémentaires.

### IPv4 et IPv6 {#ipv-and-ipv}

Vous pouvez installer tous les éléments d’Adobe Experience Manager (instance, Dispatcher) sur des réseaux IPv4 et IPv6.

Tout fonctionne sans problème, dans la mesure où aucune configuration particulière n’est requise. Si nécessaire, vous spécifiez une adresse IP au format approprié à votre type de réseau.

Lorsqu’une adresse IP doit être spécifiée, vous pouvez sélectionner (au besoin) parmi les options suivantes :

* Adresse IPv6. Par exemple : `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Adresse IPv4. Par exemple : `https://123.1.1.4:4502`

* Nom du serveur. Par exemple : `https://www.yourserver.com:4502`

* La casse par défaut de `localhost` est interprété pour les installations réseau IPv4 et IPv6. Par exemple, `https://localhost:4502`

### Exigences requises pour le module complémentaire AEM Dynamic Media {#requirements-for-aem-dynamic-media-add-on}

Par défaut, AEM Dynamic Media est désactivé. Rendez-vous ici pour [activer Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Lorsque Dynamic Media est activé, des exigences techniques supplémentaires sont d’application.

>[!NOTE]
Ces configurations système s’appliquent **uniquement** si vous utilisez Dynamic Media en mode hybride ; ce mode comprend un serveur d’images intégré qui n’est certifié que sur certains systèmes d’exploitation.
Pour les clients Dynamic Media qui exécutent le mode Dynamic Media - Scene7 (c’est-à-dire : **dynamicmedia_scene7** en mode d’exécution), aucune configuration système supplémentaire n’est requise ; configuration requise identique à celle d’AEM. L’architecture du mode Scene7 de Dynamic Media utilise le service d’images basé sur le cloud et non le service incorporé dans AEM.

#### Matériel {#hardware}

Les exigences matérielles suivantes s’appliquent à Linux® et Windows :

* Processeur Intel Xeon® ou AMD® Opteron avec au moins quatre coeurs
* Au moins 16 Go de RAM

#### Linux® {#linux}

Si vous utilisez Dynamic Media sous Linux®, les conditions préalables suivantes doivent être remplies :

* Red Hat® Enterprise 7 ou CentOS 7 et versions ultérieures avec les derniers correctifs
* Système d’exploitation 64 bits
* Permutation désactivée (recommandé)
* SELinux désactivé (voir la note ci-dessous)

>[!NOTE]
Si les paramètres régionaux sont définis de sorte que LC_CTYPE n’est pas égal à `en_US.UTF-8`, cela empêchera Dynamic Media de fonctionner. Pour connaître sa valeur, saisissez &quot;locale&quot; à l’invite de commande. S’il n’est pas correctement défini, définissez la variable d’environnement LC_CTYPE sur la chaîne vide en saisissant &quot;export LC_CTYPE=&quot; avant d’exécuter AEM.

>[!NOTE]
**Désactivation de SELinux :** la diffusion d’images ne fonctionne pas lorsque SELinux est activé. Cette option est activée par défaut. Pour résoudre ce problème, modifiez le fichier **/etc/selinux/config** et modifiez la valeur SELinux à partir de :
`SELINUX=enforcing` **vers** `SELINUX=disabled`

>[!NOTE]
**Architecture NUMA :** Les systèmes dotés de processeurs AMD64 et Intel® EM64T sont généralement configurés en tant que plates-formes NUMA (Non Uniform Memory Architecture). En d’autres termes, le noyau construit plusieurs noeuds de mémoire au moment du démarrage plutôt que de construire un seul noeud de mémoire.
La construction de plusieurs nœuds peut entraîner un épuisement de la mémoire sur un ou plusieurs nœuds avant que d’autres nœuds ne s’épuisent. Lorsque l’épuisement de la mémoire se produit, le noyau peut décider d’interrompre les processus (par exemple, la diffusion d’images ou le serveur de plateformes) même s’il existe de la mémoire disponible.
Par conséquent, si vous exécutez un tel système, Adobe recommande de désactiver NUMA à l’aide de l’option de démarrage **numa=off** pour éviter que le noyau n’arrête ces processus.

>[!NOTE]
**La résolution du nom d’hôte du serveur doit être effectuée :** assurez-vous que le nom d’hôte du serveur est résolvable sur une adresse IP. Si cela s’avère impossible, ajoutez le nom d’hôte complet et l’adresse IP à **/etc/hosts** :
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Espace de permutation égal à au moins deux fois la quantité de mémoire physique (RAM)

Pour utiliser Dynamic Media sous Windows, installez Microsoft® Visual Studio 2010, 2013 et 2015 redistribuable pour x64 et x86.

Pour Windows x64 :

* Obtenez le redistribuable Microsoft® Visual Studio 2010 à l’adresse [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/fr-fr/download/details.aspx?id=26999)
* Obtenez le redistribuable Microsoft® Visual Studio 2013 à l’adresse [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/fr-fr/download/details.aspx?id=40784)
* Obtenez le redistribuable Microsoft® Visual Studio 2015 à l’adresse [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/fr-fr/download/details.aspx?id=48145)

Pour Windows x86 :

* Obtenez le redistribuable Microsoft® Visual Studio 2010 à l’adresse [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/fr-fr/download/details.aspx?id=26999)
* Obtenez le redistribuable Microsoft® Visual Studio 2013 à l’adresse [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenez le redistribuable Microsoft® Visual Studio 2015 à l’adresse [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/fr-fr/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x et versions ultérieures
* Pris en charge uniquement à des fins d’évaluation et de démonstration

### Conditions requises pour AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

### Prise en charge logicielle de PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produit</strong></p> </th>
   <th><p><strong>Formats pris en charge pour la conversion en PDF</strong></p> </th>
  </tr>
  <tr>
   <td>Dernière version <a href="https://helpx.adobe.com/fr/acrobat/release-note/release-notes-acrobat-reader.html">Suivi classique Acrobat 2020</a></td>
   <td>XPS, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF et DWF</td>
  </tr>
  <tr>
   <td>Dernière version (obsolète) <a href="https://helpx.adobe.com/fr/acrobat/release-note/release-notes-acrobat-reader.html">Suivi classique Acrobat 2017</a></td>
   <td>XPS, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF et DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF et TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (obsolète)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF et TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (obsolète)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (obsolète)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016 (obsolète)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF et TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (obsolète)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF et TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
PDF Generator ne prend en charge que les versions allemande, anglaise, française et japonaise des systèmes d’exploitation et des applications pris en charge.
En outre,
* PDF Generator requiert la version 32 bits d’[Acrobat 2020 (suivi Classic) version 20.004.30006](https://helpx.adobe.com/fr/acrobat/release-note/release-notes-acrobat-reader.html) ou d’Acrobat 2017 version 17.011.30078 pour effectuer la conversion.
* Les conversions de PDF Generator pour OpenOffice sont uniquement prises en charge sous Windows et Linux®.
* PDF Generator ne prend en charge que la version commerciale 32 bits de Microsoft® Office Professional Plus et d’autres logiciels requis pour la conversion sur le système d’exploitation Windows.
* PDF Generator prend en charge les versions 32 et 64 bits d’OpenOffice sous Linux® système d’exploitation.
* PDF Generator ne prend pas en charge Microsoft® Office 365.
* Les fonctionnalités OCR PDF, Optimize PDF et Export PDF sont uniquement prises en charge sous Windows.
* Une version d’Acrobat est fournie avec AEM Forms pour activer la fonctionnalité PDF Generator. Accédez par programmation à la version groupée uniquement avec AEM Forms, pendant la durée de la licence AEM Forms, pour l’utiliser avec AEM Forms PDF Generator. Pour plus d’informations, voir la description du produit AEM Forms selon votre déploiement ([On-Premise](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* Le service PDF Generator ne prend pas en charge Microsoft® Windows 10.
* PDF Generator ne parvient pas à convertir les fichiers à l’aide de Microsoft® Visio 2019. Vous pouvez continuer à utiliser Microsoft® Visio 2016 pour la conversion. `.VSD` et `.VSDX` fichiers .
* PDF Generator ne parvient pas à convertir les fichiers à l’aide de Microsoft® Project 2019. Vous pouvez continuer à utiliser Microsoft® Project 2016 pour effectuer une conversion. `.VSD` et `.VSDX` fichiers .
>


### Conditions requises pour AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server ou Microsoft Windows 10
* Processeur de 1 GHz ou plus avec prise en charge de PAE, NX et SSE2.
* Systèmes d’exploitation 32 bits : 1 Go de RAM ; systèmes d’exploitation 64 bits : 2 Go de RAM.
* Systèmes d’exploitation 32 bits : 16 Go d’espace disque ; systèmes d’exploitation 64 bits : 20 Go d’espace disque.
* Mémoire graphique – 128 Mo de GPU (256 Mo recommandé)
* 2,35 Go d’espace disponible sur le disque dur
* Résolution d’écran de 1 024 x 768 pixels ou plus
* Accélération matérielle de la vidéo (facultatif)
* Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC.
* Droits d’administrateur pour l’installation de Designer.

### Conditions requises pour l’écriture différée des métadonnées AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

L’écriture différée XMP est prise en charge et activée pour les plateformes et formats de fichier suivants :

* **Systèmes d’exploitation :**

   * Linux® (Prise en charge des applications 32 bits et 32 bits sur les systèmes 64 bits). Pour connaître les étapes d’installation des bibliothèques clientes 32 bits, voir [Comment activer l’extraction XMP et la réécriture sur Red Hat® Linux 64 bits®](https://helpx.adobe.com/fr/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X (64 bits)

* **Formats de fichier :** JPEG, PNG, TIFF, PDF, INDD, AI et EPS.

### Conditions requises pour qu’AEM Assets traite les ressources lourdes en métadonnées sous Linux® {#assetsonlinux}

Le processus XMPFilesProcessor nécessite le fonctionnement de la bibliothèque GLIBC_2.14. Utilisez un noyau Linux® qui contient GLIBC_2.14, par exemple le noyau Linux® version 3.1.x. Cela améliore les performances de traitement des ressources qui contiennent un grand nombre de métadonnées, comme les fichiers de PSD. L’utilisation d’une version précédente de GLIBC entraîne une erreur dans les journaux commençant par `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
