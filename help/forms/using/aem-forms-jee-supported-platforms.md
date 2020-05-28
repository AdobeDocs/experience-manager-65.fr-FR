---
title: Plateformes prises en charge pour AEM Forms on JEE
seo-title: Plateformes prises en charge pour AEM Forms on JEE
description: Liste des composants d’infrastructure requis et pris en charge pour installer AEM Forms on JEE
seo-description: Liste des composants d’infrastructure requis et pris en charge pour installer AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
translation-type: tm+mt
source-git-commit: 18345e6519169cfceb01ab56821b596e284f3303
workflow-type: tm+mt
source-wordcount: '3202'
ht-degree: 77%

---


# Plateformes prises en charge pour AEM Forms sur JEE{#supported-platforms-for-aem-forms-on-jee}

## Plateformes prises en charge {#supported-platforms}

### Niveaux de prise en charge {#support-levels}

Le serveur AEM Forms on JEE peut être installé sur toute combinaison de systèmes d’exploitation, de serveurs d’applications, de bases de données, de pilotes de base de données, de JDK, de serveurs LDAP et de serveurs de messagerie électronique pris en charge.

Ce document répertorie les plateformes client et serveur prises en charge pour AEM Forms on JEE. Adobe fournit plusieurs niveaux de prise en charge, tant pour nos configurations recommandées que pour les autres. Ce document dresse également la liste des autres logiciels et versions pris en charge, des exceptions, des définitions de correctif et des règles de prise en charge des correctifs logiciels de fournisseurs tiers.

>[!NOTE]
>
>* Pour une liste complète des exceptions concernant les plateformes de serveur prises en charge, voir [Exceptions aux plateformes de serveur prises en charge](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>* AEM Forms on JEE ne prend en charge que les versions allemande, anglaise, française et japonaise des systèmes d’exploitation et des applications pris en charge.
>



### Configurations recommandées {#recommendedconfigurations}

Adobe recommande ces configurations et fournit une prise en charge totale ou restreinte en tant que partie intégrante du contrat de maintenance logicielles standard :

<table>
 <tbody>
  <tr>
   <th>Niveau de prise en charge</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>A : Pris en charge<br /> </td>
   <td>Adobe fournit une prise en charge et une maintenance complètes pour cette configuration. Cette configuration est couverte par le processus d’assurance qualité d’Adobe.</td>
  </tr>
  <tr>
   <td>R : Prise en charge limitée </td>
   <td>Adobe fournit une prise en charge complète pour cette configuration si certaines conditions préalables sont remplies. Contactez le support d’assistance aux entreprises d’Adobe pour connaître les conditions et demander une prise en charge.</td>
  </tr>
  <tr>
   <td>L : prise en charge limitée</td>
   <td>Adobe fournit une prise en charge complète et une maintenance pour ces configurations si certaines conditions préalables sont remplies. Toutes les fonctionnalités ne sont pas disponibles sur la configuration. Contactez le support d’assistance aux entreprises d’Adobe pour connaître les conditions et demander une prise en charge.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations non prises en charge {#unsupported-configurations}

| Niveau de prise en charge | Description |
|---|---|
| E : Fonctionnement supposé | Il est prévu que la configuration fonctionne normalement et nous n’avons reçu aucun rapport faisant état de problèmes. |
| Z : Non pris en charge | La configuration n’est pas prise en charge. Adobe ne fait aucune déclaration quant au fonctionnement de la configuration et n’en assure pas la prise en charge. |

>[!NOTE]
>
>Pour aider les clients d’AEM Forms à réduire le coût de propriété, à simplifier l’architecture de déploiement et à moderniser la pile de développement, Adobe Experience Manager Enterprise Platform s’éloigne des déploiements basés sur les serveurs d’applications pour privilégier les déploiements OSGi autonomes. Adobe continue à prendre en charge la pile AEM Forms JEE avec une matrice réduite de composants d’infrastructure.
>
>Avec la version 6.5, les composants d’infrastructure qui sont les moins utilisés par nos clients ne sont plus pris en charge, comme suit :
>・ Serveur d’applications Oracle WebLogic
>・ Base de données IBM DB2
>・ Systèmes d’exploitation IBM AIX et Sun Solaris
>
>Pour les nouvelles installations, lorsque cela est possible, il est recommandé de déployer AEM Forms sur la pile OSGi moderne afin d’exploiter les dernières innovations concernant les formulaires adaptatifs réactifs pour les communications interactives mobiles à canaux multiples et les intégrations de données d’arrière-plan à l’aide du modèle de données de formulaire.
>
>Nous reconnaissons que les utilisateurs existants doivent continuer à déployer la pile AEM Forms sur JEE. Dans ce cas de figure, Adobe nécessite le déploiement d’AEM Forms JEE sur l’infrastructure prise en charge, comme décrit dans cette documentation. Si vous effectuez une mise à niveau vers AEM Forms 6.5 et utilisez une plateforme non prise en charge dans la version précédente d’AEM Forms, vous pouvez contacter l’assistance Adobe pour obtenir de l’aide sur la mise à niveau vers une plateforme prise en charge.

### Machines virtuelles Java (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms nécessite l’exécution d’une machine virtuelle Java, laquelle est fournie par la distribution JDK (Java Development Kit). Adobe Experience Manager fonctionne avec les versions suivantes des machines virtuelles Java :

<table>
 <tbody>
  <tr>
   <th><p><strong>Plate-forme</strong></p> </th>
   <th><p><strong>Niveau de prise en charge</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11 (64 bits)</p> </td>
   <td><p>Z : Non pris en charge</p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bits)</td>
   <td>A : Pris en charge</td>
   <td>Versions et mises à jour mineures</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine (build 2.8 &amp; , JRE 1.8.0)</td>
   <td>A : Pris en charge</td>
   <td>Versions et mises à jour mineures</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine (build 2.9 &amp; , JRE 1.8.0)<br /> </td>
   <td>A : Pris en charge</td>
   <td>Versions et mises à jour mineures</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Il est conseillé de consulter les bulletins de sécurité publiés par l’éditeur Java afin de garantir la sécurité des environnements de production et d’installer les mises à jour Java les plus récentes.
>* AEM Forms on JEE ne prend en charge que les JVM 64 bits pour les environnements de production.


### Bases de données et persistance de CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Plate-forme</strong></p> </td>
   <td><p><strong> Description</strong></p> </td>
   <td><p><strong>Niveau de prise en charge</strong></p> </td>
  </tr>
  <tr>
   <td><p>Système de fichiers</p> </td>
   <td><p>Micronoyau de référentiel (fichiers TAR MK)</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0  </p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12c version 1</p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td>Oracle Database 18c </td>
   <td>Référentiel Microkernel</td>
   <td>Pris en charge</td>
  </tr> 
   <tr>
   <td>Oracle Database 19c </td>
   <td>Micronoyau de référentiel </td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>Référentiel Microkernel</td>
   <td>R : Prise en charge limitée</td>
  </tr>
    <tr>
   <td>MySQL 5.7.19 </td>
   <td>-</td>
   <td>R : Prise en charge limitée </td>
  </tr>
 </tbody>
</table>

* IBM DB2 n’est pas pris en charge pour les nouvelles installations. Elle est prise en charge uniquement pour les clients existants effectuant une mise à niveau vers AEM Forms 6.5.
* MongoDB est un logiciel tiers qui n’est pas inclus dans le pack de licences AEM. Pour plus d’informations, consultez la page relative à la stratégie de gestion des licences MongoDB ([MongoDB licensing policy](https://www.mongodb.org/about/licensing/)).
* Pour tirer pleinement parti de votre déploiement AEM, Adobe conseille d’utiliser la version MongoDB Enterprise sous licence afin de bénéficier d’une assistance professionnelle.
* Vous obtiendrez auprès de l’assistance clientèle d’Adobe une aide adaptée aux problèmes admissibles relatifs à l’utilisation de MongoDB avec AEM. Pour plus d’informations, consultez la page [MongoDB pour Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
* Le système de fichiers comprend le stockage de bloc compatible avec POSIX. Cela inclut la technologie de stockage réseau. Notez que les performances du système de fichiers sont variables et ont une incidence sur les performances globales. Il est conseillé d’effectuer un test de charge d’AEM avec le système de fichiers distant/réseau.
* Seul le moteur de stockage WiredTiger de MongoDB est pris en charge.
* La fragmentation MongoDB n’est pas pris en charge dans AEM. 
* AEM Forms on JEE ne prend pas en charge MySQL pour la persistance de RDBMK.
* Le module Document Security n’utilise pas Content Repository. Cela signifie que si vous utilisez uniquement Document Security et ne prévoyez pas d’utiliser Workspace HTML, les formulaires HTML5 ou les formulaires adaptatifs, vous n’avez pas besoin d’installer Content Repository.
* AEM Forms sur JEE ne prend pas en charge l’utilisation de MySQL pour le référentiel AEM persistant (CRX-Repository).


### Pilotes de base de données {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Base de données </th>
   <th><p><strong>Plate-forme</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar (version 5.1.44)</p> </td>
   <td><p>Fourni avec l’installation d’AEM Forms on JEE</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Pilote Microsoft® SQL Server JDBC 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fourni avec l’installation d’AEM Forms on JEE.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Pilote JDBC pour Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (version 19.3.0.0.0)<br /> </p> </td>
   <td><p>Télécharger à partir du site Web <a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html"></a>Oracle.</p> </td>
  </tr>
 </tbody>
</table>

### Serveurs d’applications {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Plate-forme</strong></p> </td>
   <td><p><strong>Niveau de prise en charge</strong></p> </td>
   <td><p><strong>Définitions de correctif prises en charge</strong></p> </td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A : Pris en charge</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Correctifs et correctifs cumulés pour la version prise en charge de EAP</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Les grappes IBM® WebSphere® sont uniquement prises en charge dans les éditions Network Deployment.

### Systèmes d’exploitation de serveur {#server-operating-systems}

#### Environnements de production {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Plate-forme</strong></p> </th>
   <th><p><strong>Niveau de prise en charge</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016 (64 bits)</td>
   <td>A : Pris en charge</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bits)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Révisions mineures, mises à jour cumulatives et mises à jour critiques</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bits)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Service Packs, correctifs cumulatifs et mises à jour de sécurité critiques</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3 (64 bits)</td>
   <td>A : Pris en charge</td>
   <td>Service Packs, correctifs cumulatifs et mises à jour de sécurité critiques</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bits)<sup> [6]</sup></td>
   <td>A : Pris en charge</td>
   <td>Service Packs, correctifs cumulatifs et mises à jour de sécurité critiques</td>
  </tr>
 </tbody>
</table>

#### Environnement virtualisé {#virtualized-environment}

Vous pouvez exécuter AEM Forms on JEE sur un ordinateur physique ou un environnement virtuel. Toutefois, si vous rencontrez un problème avec AEM Forms sur un environnement virtuel, essayez de reproduire le problème sur un ordinateur physique. Si le problème persiste sur l’ordinateur physique, contactez l’assistance Adobe pour obtenir une résolution. Pour les problèmes que vous ne pouvez pas reproduire sur un ordinateur physique, contactez votre fournisseur d&#39;environnement virtuel.

#### Environnements de développement {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plateforme (version de base)</strong></p> </th>
   <th>Niveau de prise en charge</th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64 bits</p> </td>
   <td>E : Fonctionnement supposé</td>
   <td><p>Service Packs et mises à jour critiques</p> </td>
  </tr>
 </tbody>
</table>

### Exceptions aux plateformes de serveur prises en charge {#exceptions-to-supported-server-platforms}

Tenez compte des exceptions suivantes lorsque vous choisissez la plateforme de configuration d’AEM Forms on JEE.

1. AEM Forms sur JEE ne prend pas en charge IBM® WebSphere® avec MySQL.
1. AEM Forms on JEE ne prend pas en charge et JBoss sur SUSE Linux Enterprise Server 12. Seul IBM WebSphere est pris en charge sur SUSE Linux Enterprise Server 12.
1. AEM Forms on JEE ne prend en charge aucun autre JDK avec JBoss® qu’Oracle Java™ SE.
1. AEM Forms on JEE ne prend en charge aucun autre JDK avec IBM® WebSphere® que le JDK IBM®.
1. CRX-repository prend en charge la persistance de type TarMK, MongoDB et les bases de données relationnelles (RDBMK). Vous ne pouvez pas avoir deux systèmes de base de données différents entre le serveur d’applications et le référentiel CRX. Cependant, sur un environnement AEM Forms sur JEE, vous pouvez utiliser MongoMK avec CRX-repository et une base de données relationnelle prise en charge avec le serveur d’applications.
1. AEM Forms on JEE ne prend pas en charge le serveur d’application WebSphere sur CentOS.
1. AEM Forms on JEE ne prend pas en charge le contrôle d’accès basé sur les rôles (RBAC) JBoss.

Tenez également compte des points suivants lors de votre choix de logiciels pour le déploiement d’Adobe AEM Forms on JEE :

* AEM Forms on JEE prend en charge les mises à jour, les correctifs et les packs de correctifs en plus des versions majeures et mineures spécifiées du logiciel pris en charge. Toutefois, la mise à jour à la version majeure ou mineure suivante n’est pas prise en charge sauf indication contraire.
* Les installations en grappe ne prennent pas en charge la persistance de TarMK. Pour plus d’informations sur la persistance prise en charge, voir [Choix d’un type de persistance pour une installation AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
* AEM Forms on JEE prend charge divers logiciels tiers, conformément à nos [Règles de prise en charge des logiciels de fournisseurs tiers](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
* AEM Forms on JEE prend en charge des plateformes en fonction de la prise en charge offerte par les fournisseurs tiers. Certaines combinaisons peuvent ne pas être autorisées par les fournisseurs tiers. Par exemple, de nombreux fournisseurs n’ont pas certifié leurs serveurs d’applications avec Oracle. Par conséquent, AEM Forms on JEE ne prend pas en charge ces combinaisons non plus. Pour vous assurer de choisir les versions prises en charge des logiciels, vérifiez également le tableau de prise en charge des fournisseurs tiers.
* AEM Forms on JEE ne prend pas en charge TarMK Cold Standby.
* AEM Forms on JEE ne prend pas en charge la mise en grappe verticale.
* AEM Forms on JEE ne prend pas en charge la base de données MySQL sur un environnement organisé en grappes.
* Pour la liste des plateformes supprimées ou mises à jour, voir document de résumé [des nouvelles fonctionnalités d’](../../forms/using/whats-new.md) AEM Forms 6.5.

### Serveurs LDAP (facultatifs) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produit (version de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle Unified Directory (OUD) 11g Version 2</td>
   <td>Service Packs</td>
  </tr>
  <tr>
   <td>Microsoft Active Directory 2016</td>
   <td>Versions de maintenance et Fix Packs</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>Packages de fonctionnalités et correctifs intermédiaires</p> </td>
  </tr>
 </tbody>
</table>

### Serveurs de messagerie électronique (facultatifs) {#email-servers-optional}

| Produit |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### Gestionnaires de contenu et connecteurs correspondants {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Produit<br /> </strong></td>
   <td><strong>Version</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM Filenet </td>
   <td>5.2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Server</td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td>IBM Content Manager Client</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft Sharepoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Prise en charge de Cordova {#support-for-cordova}

L’application AEM Forms prend désormais en charge Apache Cordova. Voici les versions spécifiques à la plate-forme de Cordova prises en charge :

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### Prise en charge logicielle de PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produit</strong></p> </th>
   <th><p><strong>Formats pris en charge pour la conversion en PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 Classic track</a> - Dernière version</td>
   <td>XPS, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF et DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF et TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC, HTML, HTM RTF et TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>PDF Generator prend en charge uniquement les versions en anglais, français, allemand et japonais des applications et des systèmes d’exploitation pris en charge.
>
>En outre :
>
>* PDF Generator requires 32-bit version of [Acrobat 2017 classic track version 17.011.30078 or later](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) to perform the conversion.
>* PDF Generator prend uniquement en charge la version commerciale 32 bits de Microsoft Office Professional Plus et d’autres logiciels requis pour la conversion.
>* PDF Generator ne prend pas en charge Microsoft Office 365.
>* Les conversions de PDF Generator pour OpenOffice sont uniquement prises en charge sous Windows et Linux.
>* Les fonctionnalités OCR PDF, Optimize PDF et Export PDF sont prises en charge uniquement sous Windows.
>* Une version d’Acrobat est fournie avec AEM Forms pour permettre la fonctionnalité PDF Generator. La version groupée ne doit être accessible que par programmation et uniquement avec AEM Forms, pendant le terme de la licence AEM Forms pour l’utilisation avec AEM Forms PDF Generator. For more information, refer to AEM Forms product description as per your deployment ([On-Premise](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) or [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))”
   >
   >
* Le service PDF Generator ne prend pas en charge Microsoft Windows 10.
>



### Exceptions de la prise en charge de l’accessibilité {#exceptions-to-accessibility-support}

Les sous-systèmes suivants d’AEM Forms ne sont pas conformes à la section [508](https://www.section508.gov/) :

* Interface utilisateur de création des formulaires adaptatifs
* Interface utilisateur de création de Forms Manager
* Interface de création de Correspondence Management
* Interface utilisateur d’administration (interface utilisateur de la console d’administration)

## Configuration requise pour AEM Forms sur JEE {#system-requirements-for-aem-forms-on-jee}

### Configuration matérielle requise {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Plate-forme</td>
   <td>Configuration matérielle requise</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server </td>
   <td>Processeur Intel® Xeon® E5-2680, 2,4 GHz ou équivalent<br /> VMWare ESX 5.1 ou version ultérieure<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque libre : 15 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server </td>
   <td>Processeur Intel Xeon E5-2670v2, 1 processeur virtuel, 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque disponible : 6 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Processeur Intel Xeon E5-2670v2, 1 processeur virtuel, 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits) <br /> Espace disque disponible : 6 Go d’espace temporaire + 22 Go<br /> pour AEM Forms on JEE<br /> </td>
  </tr>
  <tr>
   <td>Configuration matérielle requise pour un petit environnement de production</td>
   <td>
    <ul>
     <li><strong>Environnement Intel</strong> : Intel® Xeon® E5-2680, 2,4 GHz ou plus. L’utilisation d’un processeur à double noyau améliore encore les performances</li>
     <li><strong>Mémoire : </strong>4 Go <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Pour la configuration requise supplémentaire, voir :

* [Configuration requise pour le déploiement sur serveur unique d’AEM Forms sur JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [Configuration requise pour le déploiement en grappe d’AEM Forms on JEE
   ](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## Clients pris en charge pour AEM Forms sur JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plate-forme</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Version 32 bits ou 64 bits</p> <p> </p> </td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2016 Server</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
 </tbody>
</table>

* Espace disque pour l’installation : 1,7 Go pour Workbench uniquement, 2,7 Go sur un seul lecteur pour une installation complète de Workbench, Designer et des exemples d’assemblage, 400 Mo pour installer les répertoires temporaires (200 Mo dans le répertoire utilisateur temporaire et 200 Mo dans le répertoire temporaire Windows). si l’ensemble de ces emplacements se trouve sur un seul disque, vous devez allouer un total de 1,5 Go lors de l’installation. Les fichiers copiés dans les répertoires temporaires sont supprimés à la fin de l’installation.

* Mémoire pour l’exécution de Workbench : 2 Go de mémoire vive.
* Configuration matérielle requise : Processeur Intel® Pentium® 4 ou AMD équivalent, processeur cadencé à 1 GHz.
* Résolution d’affichage de 1024 X 768 pixels au minimum, écran couleur de 16 bits minimum
* La connexion réseau via le protocole TCP/IPv4 ou TCP/IPv6 au serveur AEM Forms on JEE
* vous devez disposer des droits d’administrateur pour pouvoir installer Workbench sous Windows. Si vous effectuez une installation à partir d’un compte non administrateur, le programme d’installation vous demandera les informations d’identification d’un compte administrateur.

### Designer {#designer}

>[!NOTE]
>
>Pour installer Designer sous Windows, exécutez le programme d’installation avec les droits d’administrateur.

* Microsoft® Windows® 2016 Server, Microsoft Windows 10

   * Processeur de 1 GHz ou plus avec prise en charge de PAE, NX et SSE2.
   * Systèmes d’exploitation 32 bits : 1 Go de RAM ; systèmes d’exploitation 64 bits : 2 Go de RAM.
   * Systèmes d’exploitation 32 bits : 16 Go d’espace disque ; systèmes d’exploitation 64 bits : 20 Go d’espace disque.

* Mémoire graphique - 128 Mo de GPU (256 Mo recommandé)
* 2,35 Go d’espace disponible sur le disque dur
* Lecteur de DVD-ROM
* Internet Explorer 10 ou 11 ; Firefox 45.x
* Résolution d’écran 1 024 X 768 pixels ou plus
* Accélération matérielle de la vidéo (en option)
* Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC.

### Adobe Acrobat et Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat et Acrobat Reader (version de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2017 (Suivi classique)</td>
   <td>Version 17.011.30078 ou ultérieure<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>La famille de produits Acrobat DC présente deux suivis pour Acrobat et Reader qui sont essentiellement des produits différents : « Classique » et « Continu ». For details and a comparison of the two tracks, see [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### Navigateurs {#browsers}

#### Ordinateurs de bureau {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Navigateur (de base)</strong></p> </th>
   <th><p><strong>Niveau de prise en charge</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge (Evergreen)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Service Packs et mises à jour critiques</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E : Fonctionnement supposé</td>
   <td> Toutes les mises à jour</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Google Chrome and Firefox sous MAC OS X</td>
   <td>A : Pris en charge<br /> <br /> </td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A : Pris en charge</td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>A : Pris en charge</td>
   <td>Toutes les mises à jour</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Voici quelques exceptions liées au navigateur pour les ordinateurs de bureau :
>
>* La plupart des navigateurs récents ne prennent plus en charge les modules externes basés sur NPAPI. For information about how it impacts AEM Forms applications and workflows, see [Discontinuation of NPAPI browser plugins and its impact](https://helpx.adobe.com/fr/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).
>* Safari est pris en charge uniquement sous Macintosh OS X.
>* Workspace prend en charge Safari 5.1 sous Macintosh OS X 10.6 et 10.7 avec Acrobat DC ou versions ultérieures. For more information about Safari 5.1 compatibility with Adobe Reader, Acrobat, see [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* Administration Console n’est pas prise en charge sur Safari.
>* Correspondence Management ne prend pas en charge Windows® Internet Explorer 9.0 pour AEM Forms 6.1.
>* Forms Portal prend en charge le logiciel de lecteur d’écran JAWS 14.0 sur Internet Explorer 11 pour une meilleure accessibilité.
>



#### Clients mobiles {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Navigateur (de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome sur Android™ 4.1.2 et versions ultérieures</p> </td>
   <td><p>Toutes les mises à jour</p> </td>
  </tr>
  <tr>
   <td>Safari sur iOS 11.0 et versions ultérieures</td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>Toutes les mises à jour<br /> </td>
  </tr>
  <tr>
   <td>Navigateur Android natif sur Android™ 4.4 et versions ultérieures</td>
   <td>Toutes les mises à jour</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Le Portail Formulaires est pris en charge sur Safari sur iPad uniquement.
>



### Application AEM Forms {#aem-forms-workspace-app}

#### Prise en charge de périphériques mobiles {#mobile-device-support}

L’application AEM Forms est disponible sur les plateformes suivantes :

| **Plate-forme** | **Appareils mobiles** |
|---|---|
| Apple iOS  | Apple iPhone, iPad, iPad Air et iPad mini exécutant iOS 11 et versions ultérieures. |
| Google Android | Android 5.1 et versions ultérieures. L’application AEM Forms est certifiée sur les tablettes Samsung Galaxy 7 et 10 pouces et les smartphones les plus courants. |
| Microsoft Windows | Périphériques Microsoft Surface, tablettes, ordinateurs portables et ordinateurs de bureau exécutant le système d&#39;exploitation Microsoft Windows 10. |

### Adobe Flash Player {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player (de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Dernière version de Flash Player</p> </td>
   <td><p>Versions et mises à jour mineures</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Adobe [cessera de mettre à jour et de distribuer Flash Player fin 2020](https://theblog.adobe.com/adobe-flash-update/).

### Extension d’Adobe Document Security for Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Cliquez [ici](https://www.adobe.com/fr/products/livecycle/rightsmanagement/extension/downloads.html) afin de voir la configuration requise par Adobe Document Security Extension for Microsoft® Office.

### Exceptions de prise en charge de clients {#exceptions-to-client-support}

AEM Forms on JEE prend en charge les mises à jour, les correctifs et les packs de correctifs en plus des versions majeures et mineures spécifiées du logiciel pris en charge. Toutefois, la mise à jour à la version majeure ou mineure suivante n’est pas prise en charge sauf indication contraire.

## Règles de prise en charge des correctifs de fournisseurs tiers {#third-party-patch-support-policy}

La configuration requise pour l’installation de logiciels de fournisseurs tiers pour AEM Forms on JEE est disponible dans la section « Configuration requise » de la documentation des produits concernés. All documentation can be accessed from [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

Les plateformes de référence de fournisseurs tiers d’AEM Forms on JEE indiquent le niveau de correctif de l’infrastructure de fournisseur tiers en cours au moment du développement et de la publication d’AEM Forms on JEE, et forment le niveau minimum de correctif/Service Pack de l’infrastructure prise en charge par cette version d’AEM Forms on JEE.

Adobe prend en charge les correctifs urgents ou recommandés publiés par des fournisseurs tiers à leur parution en supposant que les fournisseurs tiers garantissent une compatibilité ascendante avec les versions qu’AEM Forms on JEE prend en charge. Adobe ne prend en charge que les correctifs publiés après le niveau minimal de correctif indiqué dans la documentation d’AEM Forms on JEE.

Dans certains cas, Adobe ne prend pas en charge les mises à jour de fournisseurs tiers qui changent des fonctionnalités importantes, et ne permettent donc pas une compatibilité ascendante totale. For details on the supported updates, see [Supported patch definitions](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) for specific vendor products and the patch types Adobe supports.

Dans des circonstances échappant au contrôle d’Adobe, des correctifs de fournisseurs revendiquant une compatibilité ascendante peuvent avoir un impact négatif sur les produits ou les environnements clients Adobe. Dans ce cas, Adobe recommande que les clients évaluent l’impact de tout correctif urgent d’un fournisseur tiers avant de l’appliquer aux systèmes critiques. Adobe collabore avec des fournisseurs tiers afin de faire le nécessaire pour résoudre ces problèmes, que ce soit au travers des programmes de prise en charge standard d’Adobe ou de fournisseurs tiers rectifiant les problèmes de leurs correctifs. Ceci ne garantit toutefois pas qu’un nouveau correctif récemment publié par un fournisseur tiers et pris en charge par Adobe fonctionne comme documenté par le fournisseur ou avec AEM Forms on JEE.

Adobe se réserve le droit de modifier les plateformes de fournisseurs tiers de référence prises en charge par une version d’AEM Forms on JEE et les définitions de correctif prises en charge à tout moment.

Vous trouverez plus d’informations sur les correctifs de fournisseurs tiers en recherchant sur le site Support Adobe aux entreprises les articles de la base de connaissances relatifs à votre produit.
