---
title: Exigences techniques
seo-title: Technical Requirements
description: Une liste de plateformes serveur et client prises en charge pour AEM.
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 72ed4ceee560839c6573461cb5d4d6cbccfd696f
workflow-type: tm+mt
source-wordcount: '3525'
ht-degree: 94%

---

# Exigences techniques{#technical-requirements}

Adobe prend en charge Adobe Experience Manager (AEM) sur les plateformes indiquées dans les informations suivantes de ce document.

Pour tout problème relatif à la plateforme proprement dite, contactez directement le fournisseur de la plateforme.

>[!NOTE]
>
>Selon le plateforme sur lequel vous avez installé AEM, il peut exister différents ensembles de critères d’exigences pour la gestion des utilisateurs. 

## Prérequis {#prerequisites}

Configuration minimale requise pour installer Adobe Experience Manager :

* Installation de la plateforme Java, du JDK standard ou d’autres [machines virtuelles Java](#java-virtual-machines) prises en charge
* Fichier de démarrage rapide d’Experience Manager (JAR autonome ou WAR de déploiement de l’application web)

### Configuration minimale requise en matière d’espace disque et de mémoire {#minimum-sizing-requirements}

Configuration minimale requise pour exécuter Adobe Experience Manager :

* 5 Go d’espace disque disponible dans le répertoire d’installation
* Mémoire de 2 Go

>[!NOTE]
>
>* Les cas d’utilisation des ressources numériques nécessitent plus de mémoire de base. Voir [Deploiement et maintenance](/help/sites-deploying/deploy.md#default-local-install) pour plus de détails.
>* [Le module complémentaire AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) nécessite 15 Go d’espace temporaire.
>


Pour plus d’informations, consultez [Consignes de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md).

### Niveaux de prise en charge {#support-levels}

Ce document répertorie les plateformes client et serveur compatibles avec Adobe Experience Manager. Adobe fournit plusieurs niveaux de prise en charge, tant pour les configurations recommandées que pour les autres.

### Configurations prises en charge {#supported-configurations}

Adobe recommande ces configurations et assure un support complet dans le cadre du contrat de maintenance logicielle standard.

<table>
 <tbody>
  <tr>
   <td>Niveau de prise en charge</td>
   <td>Description<br /> </td>
  </tr>
  <tr>
   <td><strong>A : pris en charge</strong></td>
   <td>Adobe fournit une prise en charge et une maintenance complètes pour cette configuration. Cette configuration est couverte par le processus d’assurance qualité d’Adobe.</td>
  </tr>
  <tr>
   <td><strong>R : Prise en charge limitée </strong></td>
   <td>Pour garantir la réussite des projets de ses clients, Adobe fournit une prise en charge complète dans le cadre d’un programme de prise en charge limitée, ce qui exige le respect de conditions spécifiques. Une prise en charge de niveau R exige une demande formelle de la part du client et la confirmation d’Adobe. Pour plus d’informations, contactez le service à la clientèle Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurations non prises en charge {#unsupported-configurations}

| Niveau de prise en charge | Description |
|---|---|
| **Z : non pris en charge** | La configuration n’est pas prise en charge. Adobe ne fait aucune déclaration quant au fonctionnement de la configuration et n’en assure pas la prise en charge. |

## Plateformes prises en charge {#supported-platforms}

### Machines virtuelles Java (JVM) {#java-virtual-machines}

L’application nécessite l’exécution d’une machine virtuelle Java, laquelle est fournie par la distribution JDK (Java Development Kit).

Adobe Experience Manager fonctionne avec les versions suivantes des machines virtuelles Java :

>[!CAUTION]
>
>Il est conseillé de consulter les bulletins de sécurité publiés par l’éditeur Java afin de garantir la sécurité des environnements de production et d’installer les mises à jour Java les plus récentes.

| **Plateforme** | **Niveau de prise en charge** | **Lien** |
|---|---|---|
| Oracle Java SE 11 JDK - 64 bits | A : pris en charge `[1]` | [Télécharger](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| Oracle Java SE 10 JDK | Z : non pris en charge `[1]` |
| Oracle Java SE 9 JDK | Z : Non pris en charge `[1]` |
| Oracle Java SE 8 JDK - 64 bits | A : pris en charge `[1]` | [Télécharger](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| Machine virtuelle IBM J9 – Version 2.9, JRE 1.8.0 | A : pris en charge `[2]` |
| Machine virtuelle IBM J9 – Version 2.8, JRE 1.8.0 | A : pris en charge `[2]` |
| Azul Zulu OpenJDK 11 - 64 bits | A : pris en charge `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 bits | A : pris en charge `[3]` |  |

1. Oracle est passé à un modèle de support à long terme (LTS) pour les produits Oracle Java SE. Java 9, Java 10 et Java 12 sont des versions non-LTS fournies par Oracle (voir la [feuille de route de la prise en charge d’Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Pour déployer AEM dans un environnement d’exploitation, Adobe assure uniquement la prise en charge des versions LTS de Java. La prise en charge et la distribution du JDK Oracle Java SE, y compris toutes les mises à jour de maintenance des versions LTS après la fin des mises à niveau publiques, seront directement prises en charge par Adobe pour tous les clients AEM utilisant la technologie Oracle Java SE. Consultez la section [Stratégie de prise en charge Java pour Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) pour plus d’informations.


1. IBM JRE est pris en charge uniquement avec le serveur d’applications WebSphere.

1. Les versions LTS OpenJDK Azul Zulu sont prises en charge pour les déploiements d’AEM sur site commençant par la version 6.5 SP9. La prise en charge et la distribution des versions du JDK LTS Azul Zulu doivent être autorisées directement depuis Azul par nos clients.


### Stockage et persistance {#storage-persistence}

Plusieurs options sont disponibles pour déployer le référentiel d’Adobe Experience Manager. Consultez la liste suivante pour connaître les options de stockage et les technologies prises en charge.

| **Plateforme** | **Description** | **Niveau de prise en charge** |
|---|---|---|
| **Système de fichiers avec fichiers TAR** `[1]` | Référentiel | A : pris en charge |
| **Système de fichiers avec le magasin de données** `[1]` | Binaires | A : pris en charge |
| Stockage de binaires dans des fichiers TAR sur le système de fichiers `[1]` | Binaires | Z : Non pris en charge pour la production |
| Amazon S3 | Binaires | A : pris en charge |
| Stockage Microsoft Azure Blob | Binaires | A : pris en charge |
| MongoDB Enterprise 4.2  | Référentiel | A : pris en charge `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Référentiel | Z : non pris en charge |
| MongoDB Enterprise 3.6 | Référentiel | Z : non pris en charge |
| MongoDB Enterprise 3.4 | Référentiel | Z : non pris en charge |
| IBM DB2 10.5 | Base de données de formulaires et de référentiels | R : prise en charge limitée `[5]` |
| Oracle Database 12c (12.1.x) | Base de données de formulaires et de référentiels | R : prise en charge limitée  |
| Microsoft SQL Server 2016 | Base de données de formulaires | A : pris en charge |
| **Apache Lucene (démarrage rapide intégré)** | Service de recherche | A : pris en charge |
| Apache Solr | Service de recherche | A : pris en charge |

1. Le système de fichiers comprend le stockage de bloc compatible avec POSIX. Cela inclut la technologie de stockage réseau. Notez que les performances du système de fichiers sont variables et ont une incidence sur les performances globales. Il est conseillé d’effectuer un test de charge d’AEM avec le système de fichiers distant/réseau.
1. MongoDB Enterprise 4.2 nécessite AEM 6.5 SP9 au minimum.
1. La fragmentation MongoDB n’est pas prise en charge dans AEM. 
1. Seule le moteur de stockage MongoDB WiredTiger est prise en charge. 
1. Pris en charge pour les clients de mise à niveau d’AEM Forms. Non pris en charge pour les nouvelles installations.

>[!NOTE]
>
>Consultez la section [Déploiement de Communities](/help/communities/deploy-communities.md) pour plus d’informations sur les fonctionnalités d’AEM Communities.

>[!NOTE]
>
>MongoDB est un logiciel tiers qui n’est pas inclus dans le pack de licences AEM. Pour plus d’informations, consultez la page relative à la stratégie de gestion des licences MongoDB ([MongoDB licensing policy](https://www.mongodb.org/about/licensing/)).
>
>Pour tirer pleinement parti de votre déploiement AEM avec MongoDB, Adobe conseille d’utiliser la version MongoDB Enterprise sous licence afin de bénéficier d’une assistance professionnelle. Consultez la section [Déploiements recommandées](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) pour plus d’informations.
>
>La licence comprend un ensemble de répliques, composé d’une instance principale et de deux instances secondaires qui peuvent être utilisées pour les déploiements de création ou de publication.
>
>Si vous souhaitez créer des déploiements de création et de publication sur MongoDB, vous devez acheter deux licences distinctes.
>
>Vous obtiendrez auprès de l’assistance clientèle d’Adobe une aide adaptée aux problèmes admissibles relatifs à l’utilisation de MongoDB avec AEM.
>
>Pour plus d’informations, consultez la page [MongoDB pour Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>Les bases de données relationnelles prises en charge, telles qu’elles sont répertoriées ci-dessus, sont des logiciels tiers qui ne sont pas inclus dans le pack de licences AEM.
>
>Pour exécuter AEM 6.5 avec une base de données relationnelle prise en charge, un contrat d’assistance distinct auprès d’un fournisseur de base de données est requis. Vous obtiendrez auprès de l’assistance clientèle d’Adobe une aide adaptée aux problèmes admissibles relatifs à l’utilisation des bases de données relationnelles avec AEM 6.5.
>
>**La plupart des bases de données relationnelles bénéficient du niveau de prise en charge R sur AEM 6.5. Cette version s’accompagne des critères et d’un programme de prise en charge, comme indiqué dans la description du niveau R ci-dessus.**

### Moteurs de servlet / Serveurs d’applications {#servlet-engines-application-servers}

Adobe Experience Manager peut s’exécuter comme serveur autonome (fichier JAR de démarrage rapide) ou comme application web avec un serveur d’applications tiers (fichier WAR).

La version d’API de servlet minimum requise est 3.1.

| Plateforme | Niveau de prise en charge |
|---|---|
| **Moteur de servlet intégré au fichier de démarrage rapide (Jetty 9.4)** | A : pris en charge |
| Oracle WebLogic Server 12.2 (12cR2) | Z : non pris en charge |
| Serveur d’applications IBM WebSphere en livraison continue (LibertyProfile) avec Web Profile 7.0 et IBM JRE 1.8 | R : prise en charge restreinte des nouveaux contrats `[2]` |
| Serveur d’applications IBM 9.0 et IBM JRE 1.8 | R : prise en charge restreinte des nouveaux contrats `[1]` `[2]` |
| Apache Tomcat 8.5.x | R : prise en charge restreinte des nouveaux contrats `[2]` |
| JBoss EAP 7.2.x avec le serveur d’applications JBoss | Z : non pris en charge |
| JBoss EAP 7.1.4 avec le serveur d’applications JBoss | R : prise en charge restreinte des nouveaux contrats `[1]` `[2]` |
| JBoss EAP 7.0.x avec le serveur d’applications JBoss | Z : non pris en charge |

1. Recommandé pour les déploiements avec AEM Forms.
1. Démarrer des déploiements d’AEM 6.5 sur les serveurs d’applications entraîne le passage à la prise en charge restreinte. Les clients existants peuvent effectuer une mise à niveau vers AEM 6.5 et continuer à utiliser les serveurs d’applications. Pour les nouveaux clients, AEM 6.5 s’accompagne des critères et d’un programme de prise en charge, comme indiqué dans la description du niveau R ci-dessus.

### Systèmes d’exploitation serveur {#server-operating-systems}

Pour les environnements de production, Adobe Experience Manager fonctionne avec les plateformes de serveur suivantes :

| **Plateforme** | **Niveau de prise en charge** |
|---|---|
| **Linux, en fonction de la distribution Red Hat**  | A : pris en charge `[1]` `[3]` |
| Linux, en fonction de la distribution Debian, y compris Ubuntu  | A : pris en charge `[1]` `[2]` |
| Linux, en fonction de la distribution SUSE | A : pris en charge `[1]` |
| Microsoft Windows Server 2019 `[4]` | R : prise en charge restreinte des nouveaux contrats `[5]` |
| Microsoft Windows Server 2016 `[4]` | R : prise en charge restreinte des nouveaux contrats `[5]` |
| Microsoft Windows Server 2012 R2 | Z : non pris en charge |
| Oracle Solaris 11 | Z : non pris en charge |
| IBM AIX 7.2 | Z : non pris en charge |

1. Linux Kernel 2.6, 3.x, 4.x et 5.x comprend les dérivés de la distribution Red Hat, notamment Red Hat Enterprise Linux, CentOS, Oracle Linux et Amazon Linux. Les fonctions de module complémentaire AEM Forms sont uniquement prises en charge sur CentOS 7, Red Hat Enterprise Linux 7 et Red Hat Enterprise Linux 8.
1. AEM Forms est pris en charge sur Ubuntu 20.04 LTS.
1. Distribution Linux prise en charge par Adobe Managed Services.
1. Les déploiements en exploitation Microsoft Windows sont pris en charge pour les clients effectuant une mise à niveau vers la version 6.5 et pour une utilisation en dehors de l’environnement d’exploitation. Les nouveaux déploiements sont à la demande pour AEM Sites et Assets.
1. AEM Forms est pris en charge sous Microsoft Windows Server sans les restrictions du niveau d’assistance R.

>[!NOTE]
>
>Si vous installez AEM Forms 6.5, assurez-vous d’avoir installé les redistribuables Microsoft Visual C++ 32 bits suivants.
>
>* Redistribuable Microsoft Visual C++ 2008
>* Redistribuable Microsoft Visual C++ 2010
>* Redistribuable Microsoft Visual C++ 2012
>* Redistribuable Microsoft Visual C++ 2013 (à partir de la version 6.5)



### Environnements virtuels et de cloud computing {#virtual-cloud-computing-environments}

Adobe Experience Manager exécuté sur une machine virtuelle sur des environnements de cloud computing, tels que Microsoft Azure et Amazon Web Services (AWS), est pris en charge conformément aux exigences techniques répertoriées sur cette page, et d’après les conditions de prise en charge standard d’Adobe.

Pour un environnement natif dans le cloud, passez en revue la dernière offre de la gamme de produits AEM : Adobe Experience Manager as a Cloud Service. Consultez la [Documentation d’Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=fr) pour plus d’informations.

Adobe propose également l’utilisation d’Adobe Managed Services pour déployer AEM sur Azure ou AWS. Adobe Managed Services fournit aux experts les compétences nécessaires pour déployer et utiliser AEM dans ces environnements de cloud computing. Consultez notre [documentation complémentaire sur Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

Dans tous les autres cas, lorsqu’AEM est déployé sur Azure ou AWS, ou tout autre environnement de cloud computing, la prise en charge d’Adobe sera limitée à l’environnement informatique virtuel, conformément aux caractéristiques techniques répertoriées sur cette page. Tout problème signalé lié à l’exécution d’AEM dans ces environnements cloud devra être reproductible indépendamment de tout service cloud spécifique à l’environnement de cloud computing, à moins que le service cloud ne soit spécifiquement pris en charge dans le cadre des exigences techniques répertoriées sur cette page, par exemple le stockage Azure Blob ou AWS S3.

Pour des recommandations sur le déploiement d’AEM sur Azure ou AWS, en dehors d’Adobe Managed Services, Adobe recommande vivement de travailler directement avec votre fournisseur cloud ou avec l’un des partenaires Adobe prenant en charge le déploiement d’AEM dans l’environnement de cloud de votre choix. Le partenaire ou fournisseur cloud que vous choisissez est responsable du dimensionnement, de la conception et de l’implémentation de l’architecture, et ce, pour répondre à vos besoins spécifiques en matière de performance, de chargement, d’évolutivité et de sécurité.

### Plateformes Dispatcher (serveurs web) {#dispatcher-platforms-web-servers}

Le Dispatcher est le composant de mise en cache et d’équilibrage de charge. [Téléchargez la dernière version de Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). Experience Manager 6.5 nécessite la version 4.3.2 ou une version ultérieure du Dispatcher.

L’utilisation des serveurs web ci-dessous est prise en charge avec Dispatcher version 4.3.2 :

| Plateforme | Niveau de prise en charge |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A : pris en charge |
| Microsoft IIS 10 (Internet Information Server) | A : pris en charge |
| Microsoft IIS 8.5 (Internet Information Server) | Z : non pris en charge |

1. Les serveurs web développés sur la base du code source Apache httpd bénéficieront du même niveau de prise en charge que la version de httpd sur laquelle ils sont basés : En cas de doute, demandez à Adobe de confirmer le niveau de prise en charge relatif au produit serveur correspondant. Différents cas de figure :

   1. le serveur HTTP a été développé en utilisant uniquement les distributions source Apache officielles; ou
   1. le serveur HTTP a été distribué comme composant du système d’exploitation sur lequel il est exécuté. Exemples : Serveur IBM HTTP, Serveur Oracle HTTP 

1. Dispatcher n’est pas disponible pour Apache 2.4.x sur les systèmes d’exploitation Windows.

## Plateformes clientes prises en charge {#supported-client-platforms}

### Navigateurs pris en charge pour l’interface utilisateur de création {#supported-browsers-for-authoring-user-interface}

L’interface utilisateur d’Adobe Experience Manager fonctionne avec les plates-formes clientes suivantes : Tous les navigateurs sont testés avec l’ensemble par défaut de modules complémentaires et externes.

L’interface utilisateur d’AEM est optimisée en vue d’une utilisation sur des grands écrans (ordinateurs portables et de bureau) et sur des tablettes (du type Apple iPad ou Microsoft Surface). Le format « téléphone » n’est pas pris en charge.

>[!NOTE]
>
>**Prise en charge des navigateurs mis à jour fréquemment :**
>
>Mozilla Firefox, Google Chrome and Microsoft Edge publient des mises à jour tous les quelques mois. Adobe s’engage à fournir des mises à jour pour Adobe Experience Manager afin de conserver le niveau de prise en charge indiqué ci-dessous avec les versions à venir de ces navigateurs.

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
   <td>Microsoft Edge (Evergreen)</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z : non pris en charge</td>
   <td>Z : non pris en charge</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Mozilla Firefox, dernière version Extended Support Release (ESR) [1]</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Apple Safari on macOS (Evergreen)</td>
   <td>A : pris en charge</td>
   <td>A : pris en charge</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x sur macOS</td>
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

1. Version ESR (Extended Support Release) de Firefox. [Plus d’informations à ce sujet sur mozilla.org](https://www.mozilla.org/fr-FR/firefox/organizations/faq/)
1. Prise en charge pour Apple iPad

### Navigateurs pris en charge pour les sites web {#supported-browsers-for-websites}

En règle générale, la prise en charge du navigateur pour les sites web rendus par AEM Sites dépend de la mise en œuvre des modèles de pages AEM, de la conception et de la sortie des composants. Par conséquent, la responsabilité en revient à celui qui met en œuvre ces composants.

### Clients WebDAV {#webdav-clients}

**Microsoft Windows 7+**

Pour se connecter avec Microsoft Windows 7 et versions ultérieures à une instance AEM qui n’est pas sécurisée avec SSL, il faut qu’une authentification de base sur un réseau non sécurisé soit activée dans Windows. Pour ce faire, une modification est nécessaire dans le Registre Windows de WebClient :

1. Localisez la sous-clé du Registre :

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Ajoutez l’entrée de Registre BasicAuthLevel à cette sous-clé en lui attribuant une valeur de 2 (ou plus élevée).

Pour améliorer la réactivité du client WebDav sous Windows, consultez l’article [2445570 de la Base de connaissances d’assistance Microsoft](https://support.microsoft.com/kb/2445570).

## Autres remarques relatives aux plates-formes {#additional-platform-notes}

Vous trouverez dans cette section des remarques et des informations plus détaillées concernant l’exécution d’Adobe Experience Manager et de ses modules complémentaires.

### IPv4 et IPv6 {#ipv-and-ipv}

Tous les éléments d’Adobe Experience Manager (Instance, Dispatcher) peuvent être installés sur des réseaux IPv4 et IPv6.

Tout fonctionne sans problème, dans la mesure où aucune configuration particulière n’est requise. Si nécessaire, vous pouvez simplement indiquer une adresse IP suivant le format approprié au type de réseau.

Cela signifie que lorsqu’une adresse IP doit être indiquée, vous avez le choix entre les éléments suivants (suivant les besoins) :

* Une adresse IPv6
Par exemple : `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Une adresse IPv4
Par exemple : `https://123.1.1.4:4502`

* Un nom de serveur
Par exemple : `https://www.yourserver.com:4502`

* Le scénario par défaut de `localhost` sera interprété à la fois pour les installations réseau IPv4 et IPv6.
Par exemple : `https://localhost:4502`

### Configuration requise pour le module complémentaire AEM Dynamic Media  {#requirements-for-aem-dynamic-media-add-on}

Par défaut, AEM Dynamic Media est désactivé. Rendez-vous ici pour [activer Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Lorsque Dynamic Media est activé, des exigences techniques supplémentaires sont d’application.

>[!NOTE]
>
>Ces configurations système s’appliquent **uniquement** si vous utilisez Dynamic Media en mode hybride ; ce mode comprend un serveur d’images intégré qui n’est certifié que sur certains systèmes d’exploitation.
>
>Pour les clients Dynamic Media qui exécutent Dynamic Media en mode Scene7 (mode d’exécution **dynamicmedia_scene7**), il n’existe aucune exigence système supplémentaire spécifique ; la configuration requise est donc la même que pour AEM. L’architecture du mode Dynamic Media – Scene7 utilise le service d’images basé sur le cloud, et non celui intégré dans AEM.

#### Matériel {#hardware}

La configuration matérielle minimale requise s’applique à la fois à Linux et à Windows :

* Processeur Intel Xeon ou AMD Opteron avec au moins 4 cœurs
* Au moins 16 Go de RAM

#### Linux {#linux}

Si vous utilisez Dynamic Media sous Linux, les conditions préalables ci-dessous doivent être remplies :

* Red Hat Enterprise 7 ou CentOS 7 et versions ultérieures avec les derniers correctifs
* Système d’exploitation 64 bits
* Échange désactivé (recommandé)
* SELinux désactivé (voir la remarque ci-dessous)

>[!NOTE]
>
>Si les paramètres régionaux sont définis de sorte que LC_CTYPE n’est pas égal à `en_US.UTF-8`, cela empêchera Dynamic Media de fonctionner. Pour connaître sa valeur, saisissez &quot;locale&quot; à l’invite de commande. Si la configuration est différente, définissez la variable d’environnement LC_CTYPE sur la chaîne vide en saisissant &quot;export LC_CTYPE=&quot; avant d’exécuter AEM.

>[!NOTE]
>
>**Disabling SELinux (Désactiver SELinux) :** La diffusion d’images ne fonctionne pas lorsque SELinux est activé. Cette option est activée par défaut. Pour remédier à ce problème, modifiez le fichier **/etc/selinux/config** et définissez la valeur SELinux comme suit :
>
>`SELINUX=enforcing` **vers** `SELINUX=disabled`

>[!NOTE]
>
>**Architecture NUMA :** Les systèmes équipés de processeurs à architecture AMD64 et Intel EM64T sont généralement configurés comme des plates-formes NUMA (Non Uniform Memory Architecture). Cela signifie que le noyau construit plusieurs nœuds de mémoire lors du démarrage, plutôt que d’en construire un seul.
>
>Cette construction à plusieurs nœuds peut entraîner un épuisement de la mémoire sur un ou plusieurs des nœuds avant l’épuisement des autres. Lorsqu’un épuisement de la mémoire se produit, le noyau peut décider de terminer des processus (Image Server ou Platform Server, par exemple), bien que de la mémoire soit disponible.
>
>Si vous utilisez un système de ce type, Adobe vous conseille donc de désactiver l’architecture NUMA à l’aide de l’option de démarrage **numa=off** afin d’éviter que le noyau termine ces processus.

>[!NOTE]
>
>**Le nom d’hôte du serveur doit être résolvable :** veillez à ce que le nom de hôte du serveur soit résolvable sur une adresse IP. Si cela s’avère impossible, ajoutez le nom d’hôte complet et l’adresse IP à **/etc/hosts** :
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Espace d’échange égal à au moins deux fois la quantité de mémoire physique (RAM).

Pour utiliser Dynamic Media sous Windows, les redistribuables Microsoft Visual Studio 2010, 2013 et 2015 pour x64 et x86 doivent être installés.

Pour Windows x64 :

* Procurez-vous le redistribuable Microsoft Visual Studio 2010 à l’adresse [https://www.microsoft.com/fr-fr/download/details.aspx?id=13523](https://www.microsoft.com/fr-fr/download/details.aspx?id=13523).
* Procurez-vous le redistribuable Microsoft Visual Studio 2013 à l’adresse [https://www.microsoft.com/fr-fr/download/details.aspx?id=40784](https://www.microsoft.com/fr-fr/download/details.aspx?id=40784).
* Procurez-vous le redistribuable Microsoft Visual Studio 2015 à l’adresse [https://www.microsoft.com/fr-fr/download/details.aspx?id=48145](https://www.microsoft.com/fr-fr/download/details.aspx?id=48145).

Pour Windows x86 :

* Procurez-vous le redistribuable Microsoft Visual Studio 2010 à l’adresse [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555).
* Procurez-vous le redistribuable Microsoft Visual Studio 2013 à l’adresse [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769).
* Procurez-vous le redistribuable Microsoft Visual Studio 2015 à l’adresse [https://www.microsoft.com/fr-fr/download/details.aspx?id=52685](https://www.microsoft.com/fr-fr/download/details.aspx?id=52685).

#### Mac OS {#macos}

* Versions 10.9.x et ultérieures
* Pris en charge uniquement à des fins d’évaluation et de démonstration

### Exigences pour le générateur de PDF AEM Forms {#requirements-for-aem-forms-pdf-generator}

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
>
>PDF Generator prend en charge uniquement les versions en anglais, français, allemand et japonais des applications et des systèmes d’exploitation pris en charge.
>
>En outre :
>
>* PDF Generator requiert la version 32 bits d’[Acrobat 2020 (suivi Classic) version 20.004.30006](https://helpx.adobe.com/fr/acrobat/release-note/release-notes-acrobat-reader.html) ou d’Acrobat 2017 version 17.011.30078 pour effectuer la conversion.
>* Les conversions de PDF Generator pour OpenOffice sont uniquement prises en charge sous Windows et Linux.
>* PDF Generator ne prend en charge que la version commerciale 32 bits de Microsoft Office Professional Plus et d’autres logiciels requis pour la conversion sur le système d’exploitation Windows.
>* PDF Generator prend en charge les versions 32 et 64 bits d’OpenOffice sous Linux.
>* PDF Generator ne prend pas en charge Microsoft Office 365.
>* Les fonctionnalités OCR PDF, Optimize PDF et Export PDF sont prises en charge uniquement sous Windows.
>* Une version d’Acrobat est fournie avec AEM Forms pour permettre la fonctionnalité PDF Generator. La version groupée ne doit être accessible que par programmation et uniquement avec AEM Forms, pendant le terme de la licence AEM Forms pour l’utilisation avec AEM Forms PDF Generator. Pour plus d’informations, reportez-vous à la description du produit AEM Forms selon votre déploiement ([On-Premise](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-managed-services.html))
>* Le service PDF Generator ne prend pas en charge Microsoft Windows 10.
>* PDF Generator ne parvient pas à convertir les fichiers dans Microsoft Visio 2019. Vous pouvez continuer à utiliser Microsoft Visio 2016 pour convertir des fichiers .VSD et .VSDX.
>* PDF Generator ne parvient pas à convertir les fichiers à l’aide de Microsoft Project 2019. Vous pouvez continuer à utiliser Microsoft Project 2016 pour convertir les fichiers .VSD et .VSDX.
>


### Conditions requises pour AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server ou Microsoft Windows 10
* Processeur de 1 GHz ou plus avec prise en charge de PAE, NX et SSE2.
* Systèmes d’exploitation 32 bits : 1 Go de RAM ; systèmes d’exploitation 64 bits : 2 Go de RAM.
* Systèmes d’exploitation 32 bits : 16 Go d’espace disque ; systèmes d’exploitation 64 bits : 20 Go d’espace disque.
* Mémoire graphique – 128 Mo de GPU (256 Mo recommandé)
* 2,35 Go d’espace disponible sur le disque dur
* Résolution d’écran 1 024 X 768 pixels ou plus
* Accélération matérielle de la vidéo (en option)
* Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC.
* Droits d’administrateur pour l’installation de Designer.

### Exigences pour l’écriture en différée des métadonnées XMP AEM Assets {#requirements-for-aem-assets-xmp-metadata-write-back}

L’écriture différée XMP est prise en charge et activée pour les plateformes et formats de fichier suivants :

* **Systèmes d’exploitation :**

   * Linux (32 bits, prise en charge des applications 32 bits sur les systèmes 64 bits). Pour les étapes d’installation des bibliothèques clientes 32 bits, consultez la section [Activation de l’écriture différée et de l’extraction XMP sous RedHat Linux 64 bits](https://helpx.adobe.com/fr/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X (64 bits)

* **Formats de fichier :** JPEG, PNG, TIFF, PDF, INDD, AI et EPS.

### Conditions requises pour qu’AEM Assets traite les ressources lourdes en métadonnées sous Linux {#assetsonlinux}

Le processus XMPFilesProcessor nécessite le fonctionnement de la bibliothèque GLIBC_2.14. Utilisez un noyau Linux contenant GLIBC_2.14, par exemple un noyau Linux version 3.1.x. Cela améliore les performances de traitement des ressources qui contiennent un grand nombre de métadonnées, comme les fichiers PSD. L’utilisation d’une version précédente de GLIBC entraîne une erreur dans les journaux commençant par `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
