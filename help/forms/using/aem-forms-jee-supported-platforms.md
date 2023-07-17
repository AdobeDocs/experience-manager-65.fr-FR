---
title: Plateformes prises en charge pour AEM Forms on JEE
description: Liste des composants d’infrastructure requis et pris en charge pour l’installation d’AEM Forms on JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 3d80ea6a6fbad05afcdd1f41f4b9de70921ab765
workflow-type: tm+mt
source-wordcount: '3685'
ht-degree: 55%

---


# Plateformes prises en charge pour AEM Forms on JEE {#supported-platforms-for-aem-forms-on-jee}

## Plateformes prises en charge {#supported-platforms}

<div class="preview">

Adobe a publié un [programme d’installation complet](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) avec AEM 6.5 Forms Service Pack 12 (6.5.12.0) on JEE, ainsi que les programmes d’installation de correctifs. Le programme d’installation complet prend en charge les nouvelles plateformes, tandis que le programme d’installation de correctif ne comprend que des correctifs.

Si vous effectuez une nouvelle installation ou envisagez d’utiliser les derniers logiciels pour votre environnement AEM Forms 6.5 on JEE, Adobe recommande d’utiliser le [programme d’installation complet d’AEM 6.5.12.0 Forms on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) sorti le 3 mars 2022 au lieu du programme d’installation d’AEM 6.5 Forms, sorti le 8 avril 2019.

</div>

### Niveaux de prise en charge {#support-levels}

Le serveur AEM Forms on JEE peut être configuré à l’aide de n’importe quelle combinaison de systèmes d’exploitation, de serveurs d’applications, de bases de données, de pilotes de base de données, de JDK, de serveurs LDAP et de serveurs de messagerie pris en charge.

Ce document répertorie les plateformes client et serveur prises en charge pour AEM Forms on JEE. Adobe offre plusieurs niveaux de prise en charge, à la fois pour les configurations recommandées par l’Adobe et pour d’autres configurations. Le document répertorie également d’autres logiciels pris en charge et leur version, les exceptions, les définitions de correctif et les règles de prise en charge des correctifs logiciels tiers.

>[!NOTE]
>
>- Pour obtenir une liste complète des exceptions concernant les plateformes de serveur prises en charge, voir [Exceptions aux plateformes de serveur prises en charge](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- AEM Forms on JEE ne prend en charge que les versions allemande, anglaise, française et japonaise des systèmes d’exploitation et des applications pris en charge.

### Configurations recommandées {#recommendedconfigurations}

Adobe recommande ces configurations et fournit une prise en charge complète ou limitée dans le cadre du contrat de maintenance logicielle standard :

<table>
 <tbody>
  <tr>
   <th>Niveau de prise en charge</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>A : Pris en charge<br /> </td>
   <td>Adobe fournit une prise en charge et une maintenance complètes de cette configuration. Cette configuration est couverte par le processus d’assurance qualité d’Adobe.</td>
  </tr>
  <tr>
   <td>R : Prise en charge limitée </td>
   <td>Adobe fournit une prise en charge complète de cette configuration une fois certaines conditions préalables remplies. Contactez le support d’Adobe aux entreprises pour en savoir plus sur les conditions préalables et envoyer une demande d’assistance.</td>
  </tr>
  <tr>
   <td>L : Prise en charge limitée</td>
   <td>Adobe fournit une prise en charge et une maintenance complètes de cette configuration une fois certaines conditions préalables remplies. Toutes les fonctionnalités ne sont pas disponibles dans la configuration. Contactez le support d’Adobe aux entreprises pour en savoir plus sur les conditions préalables et envoyer une demande d’assistance.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurations non prises en charge {#unsupported-configurations}

| Niveau de prise en charge | Description |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E : Fonctionnement supposé | Il est prévu que la configuration fonctionne normalement et nous n’avons reçu aucun rapport faisant état de problèmes. |
| Z : Non pris en charge | La configuration n’est pas prise en charge. Adobe ne fait aucune déclaration indiquant si la configuration fonctionne et ne la prend pas en charge. |

>[!NOTE]
>
>Pour aider les clients d’AEM Forms à réduire le coût de possession, à simplifier l’architecture de déploiement et à moderniser la pile de développement, la plateforme d’entreprise Adobe Experience Manager délaisse les déploiements sur serveur d’applications au profit de déploiements OSGi autonomes. Adobe continue de prendre en charge la pile AEM Forms JEE avec une matrice réduite de composants d’infrastructure.
>
>Avec la version 6.5, les composants d’infrastructure qui sont les moins utilisés parmi les clients Adobe ne sont plus pris en charge, comme suit :
>
>- Base de données IBM® DB2®
- Systèmes d’exploitation IBM® AIX® et Sun Solaris™
>
Pour les nouvelles installations, dans la mesure du possible, il est recommandé de déployer AEM Forms sur la pile OSGi moderne afin d’utiliser les dernières innovations en matière de Forms adaptatif réactif pour les communications interactives mobiles multicanaux et les intégrations de données principales à l’aide du modèle de données de formulaire.
>
Adobe reconnaît que les utilisateurs existants doivent continuer à déployer la pile AEM Forms on JEE. Dans ce cas de figure, Adobe nécessite le déploiement d’AEM Forms JEE sur une infrastructure prise en charge, comme décrit dans cette documentation. Si vous effectuez une mise à niveau vers AEM 6.5 Forms et que vous utilisez une plateforme non prise en charge sur la version précédente d’AEM Forms, vous pouvez contacter l’assistance technique d’Adobe pour obtenir de l’aide sur la mise à niveau vers une plateforme prise en charge.

### Machines virtuelles Java™ (JVM) {#java-virtual-machines-jvm}

Adobe Experience Manager Forms nécessite l’exécution d’une machine virtuelle Java™, fournie par la distribution Java™ Development Kit (JDK). Adobe Experience Manager fonctionne avec les versions suivantes des machines virtuelles Java™ :

<table>
 <tbody>
  <tr>
   <th><p><strong>Plateforme</strong></p> </th>
   <th><p><strong>Niveau de prise en charge</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 11 (64 bits) <sup> [8] </sup> </p>  </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Versions et mises à jour mineures </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 64 bits</td>
   <td>Z : Non pris en charge</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 64 bits</td>
   <td>Z : Non pris en charge</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bits)</td>
   <td>A : Pris en charge</td>
   <td>Versions et mises à jour mineures</td>
  </tr>
  <tr>
   <td>IBM® J9 Virtual Machine (version 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
   <td>A : Pris en charge</td>
   <td>Versions et mises à jour mineures</td>
  </tr>
  <tr>
   <td>IBM® JAVA1.8.0_291(version 8.0.6.30)<br /> </td>
   <td>A : Pris en charge</td>
   <td>Versions et mises à jour mineures</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Suivez les bulletins de sécurité publiés par le fournisseur Java™ afin de garantir la sécurité des environnements de production et d’installer les dernières mises à jour Java™.
- AEM Forms on JEE ne prend en charge que les JVM 64 bits pour les environnements de production.

### Bases de données et persistance de CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Plateforme</strong></p> </td>
   <td><p><strong> Description</strong></p> </td>
   <td><p><strong>Niveau de prise en charge</strong></p> </td>
  </tr>
  <tr>
   <td><p>Système de fichiers</p> </td>
   <td><p>Micronoyau de référentiel (fichiers TAR MK)</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 4.0  (Obsolète) </p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.2 </p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12c Release 2 (12.2.0.1.0) (Obsolète)</p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c (éditions Standard, Real Application Clusters (RAC) et Enterprise) </td>
   <td>Référentiel Microkernel </td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016 (obsolète)</p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2019</p> </td>
   <td><p>Référentiel Microkernel</p> </td>
   <td><p>Pris en charge</p> </td>
  </tr>
  <tr>
   <td>IBM® DB2® 11.1 (obsolète)</td>
   <td>Référentiel Microkernel</td>
   <td>R : Prise en charge limitée</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35 (Obsolète) </td>
   <td>-</td>
   <td>R : Prise en charge limitée </td>
  </tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R : Prise en charge limitée </td>
  </tr>
 </tbody>
</table>

- IBM® DB2® n’est pas pris en charge pour les nouvelles installations. Elle est prise en charge uniquement pour les clients existants effectuant une mise à niveau vers AEM 6.5 Forms.
- MongoDB est un logiciel tiers non inclus dans le package de licence d’AEM. Pour plus d’informations, voir [Politique de licence MongoDB](https://www.mongodb.org/about/licensing/).
- Pour tirer le meilleur parti de votre déploiement AEM, Adobe recommande d’obtenir une licence de la version MongoDB Enterprise afin de bénéficier d’une assistance professionnelle.
- Vous obtiendrez auprès de l’assistance clientèle d’Adobe une aide adaptée aux problèmes admissibles relatifs à l’utilisation de MongoDB avec AEM. Pour plus d’informations, consultez la page [MongoDB pour Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- Le système de fichiers comprend le stockage de bloc compatible avec POSIX. Cela inclut la technologie de stockage réseau. Gardez à l’esprit que les performances du système de fichiers peuvent varier et avoir une incidence sur les performances globales. Il est recommandé de charger les AEM de test avec le système de fichiers réseau/distant.
- Seul le moteur de stockage WiredTiger de MongoDB est pris en charge.
- La fragmentation MongoDB n’est pas pris en charge dans AEM. 
- AEM Forms on JEE ne prend pas en charge MySQL pour la persistance RDBMK.
- Le module Document Security n’utilise pas Content Repository. Cela signifie que si vous utilisez uniquement Document Security et que vous ne prévoyez pas d’utiliser HTML Workspace, HTML5 Forms ou des formulaires adaptatifs, n’installez pas Content Repository.
- AEM Forms on JEE ne prend pas en charge l’utilisation de MySQL pour la conservation du référentiel AEM (référentiel CRX).

### Pilotes de base de données {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Base de données </th>
   <th><p><strong>Plateforme</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar (version 5.1.44)</p> </td>
   <td><p>Fourni avec l’installation d’AEM Forms on JEE.</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server <br /> </td>
   <td><p>Pilote Microsoft® SQL Server JDBC 6.2.1.0 (Obsolète) <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fourni avec l’installation d’AEM Forms on JEE.</p> </td>
  </tr>
    <tr>
   <td>Microsoft® SQL Server <br /> </td>
   <td><p>Pilote Microsoft® SQL Server JDBC 6.2.2.0 <br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fourni avec l’installation d’AEM Forms on JEE.</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server <br /> </td>
   <td><p>Pilote Microsoft® SQL Server JDBC 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Téléchargez-le sur le site Web de Microsoft®.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Pilote JDBC pour Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (version 19.3.0.0.0)<br /> </p> </td>
   <td><p>Télécharger à partir du <a href="https://www.oracle.com/fr/database/technologies/appdev/jdbc-ucp-19c-downloads.html">site web d’Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Serveurs d’applications {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Plateforme</strong></p> </td>
   <td><p><strong>Niveau de prise en charge</strong></p> </td>
   <td><p><strong>Définitions de correctif prises en charge</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1 (12c R2)</td>
   <td>A : Pris en charge</td>
   <td>Service Pack et mises à jour critiques</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A : Pris en charge</td>
   <td>Service Pack et mises à jour critiques</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.1.4 <sup>[2] [3] [7]</sup> (Obsolète) </p> </td>
   <td><p>A : pris en charge</p> </td>
   <td><p>Correctifs et correctifs cumulatifs pour la version EAP prise en charge</p> </td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A : pris en charge</p> </td>
   <td><p>Correctifs et correctifs cumulatifs pour la version EAP prise en charge</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Les grappes IBM® WebSphere® ne sont prises en charge que dans les éditions Network Deployment.

### Systèmes d’exploitation de serveur {#server-operating-systems}

#### Environnements de production {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Plateforme</strong></p> </th>
   <th><p><strong>Niveau de prise en charge</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft® Windows Server 2019 (64 bits)</td>
   <td>A : Pris en charge</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A : Pris en charge</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td> Microsoft® Windows Server 2016 (64 bits) (obsolète)</td>
   <td>A : Pris en charge</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bits)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Versions mineures, mises à jour cumulatives et mises à jour critiques</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bits) (obsolète)</td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Versions mineures, mises à jour cumulatives et mises à jour critiques</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bits)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Service Packs, correctifs cumulatifs et mises à jour de sécurité critiques</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Mise à jour 3 (64 bits)</td>
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

Vous pouvez exécuter AEM Forms on JEE sur une machine physique ou un environnement virtuel. Cependant, si vous rencontrez un problème avec AEM Forms dans un environnement virtuel, essayez de le répliquer sur un ordinateur physique. Si le problème persiste sur l’ordinateur physique, contactez l’assistance technique d’Adobe pour le résoudre. Pour les problèmes qu’il n’est pas possible de reproduire sur un ordinateur physique, contactez le fournisseur de votre environnement virtuel.

#### Environnements de développement {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plateforme (version de base)</strong></p> </th>
   <th>Niveau de prise en charge</th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64 bits</p> </td>
   <td>E : Fonctionnement supposé</td>
   <td><p>Service Pack et mises à jour critiques</p> </td>
  </tr>
 </tbody>
</table>

### Exceptions aux plateformes de serveur prises en charge {#exceptions-to-supported-server-platforms}

Tenez compte des exceptions suivantes lors du choix d’une plateforme pour configurer votre serveur AEM Forms on JEE.

1. AEM Forms on JEE ne prend pas en charge IBM® WebSphere® avec MySQL.
1. AEM Forms on JEE ne prend pas en charge et JBoss® sous SUSE® Linux® Enterprise Server 12. Seul IBM® WebSphere® est pris en charge sur SUSE® Linux® Enterprise Server 12.
1. AEM Forms on JEE ne prend en charge aucun autre JDK avec JBoss® qu’Oracle Java™ SE.
1. AEM Forms on JEE ne prend en charge aucun autre JDK avec IBM® WebSphere® que le JDK IBM®.
1. Le référentiel CRX prend en charge la persistance de type TarMK, MongoDB et les bases de données relationnelles (RDBMK). Vous ne pouvez pas avoir deux systèmes de bases de données différents entre le serveur d’applications et le référentiel CRX. Cependant, dans un environnement AEM Forms on JEE, vous pouvez utiliser MongoMK avec le référentiel CRX et une base de données relationnelle prise en charge avec le serveur d’applications.
1. AEM Forms on JEE ne prend pas en charge le serveur d’applications WebSphere® sur CentOS.
1. AEM Forms on JEE ne prend pas en charge le contrôle d’accès basé sur les rôles JBoss® (RBAC).
1. AEM Forms on JEE prend uniquement en charge le SDK Oracle Java™ SE 11 (64 bits) pour le serveur d’applications JBoss® EAP 7.4.

Tenez également compte des points suivants lors du choix de logiciels pour les déploiements d’Adobe AEM Forms on JEE :

- AEM Forms on JEE prend en charge les mises à jour, les correctifs et les packs de correctifs en plus des versions majeures et mineures spécifiées des logiciels pris en charge. Toutefois, la mise à jour vers la version majeure ou mineure suivante n’est pas prise en charge, sauf indication contraire.
- Les installations en grappe ne prennent pas en charge la persistance de TarMK. Pour plus d’informations sur la persistance prise en charge, voir [Choix d’un type de persistance pour une installation AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms on JEE prend en charge divers logiciels tiers selon l’Adobe [Règles de prise en charge des logiciels tiers](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- Les plateformes de prise en charge d’AEM Forms on JEE sont prises en charge par les fournisseurs tiers. Certaines combinaisons peuvent ne pas être autorisées par les fournisseurs tiers. Par exemple, de nombreux fournisseurs n’ont pas certifié leurs serveurs d’applications avec Oracle. Par conséquent, AEM Forms on JEE ne prend pas en charge ces combinaisons non plus. Pour vous assurer de choisir les versions prises en charge des logiciels, vérifiez également le tableau de prise en charge des fournisseurs tiers.
- AEM Forms on JEE ne prend pas en charge TarMK Cold Secondaire.
- AEM Forms on JEE ne prend pas en charge la mise en grappe verticale.
- AEM Forms on JEE ne prend pas en charge la base de données MySQL sur un environnement organisé en clusters.
- Pour obtenir la liste des plateformes supprimées ou mises à jour, voir le document [Résumé des nouvelles fonctionnalités d’AEM 6.5 Forms](../../forms/using/whats-new.md).

### Serveurs LDAP (facultatifs) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produit (version de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Principal Directory 2016</td>
   <td>Versions de maintenance et Fix Packs</td>
  </tr>
  <tr>
   <td><p>IBM® Serveur d’annuaire Tivoli 6.4</p> </td>
   <td><p>Feature Packs et correctifs intermédiaires</p> </td>
  </tr>
 </tbody>
</table>

### Serveurs de messagerie électronique (facultatifs) {#email-servers-optional}

| Produit |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### Gestionnaires de contenu et connecteurs correspondants {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Produit<br /> </strong></td>
   <td><strong>Version</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM® FileNet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server (obsolète) </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> Client IBM® Content Manager (obsolète)</td>
   <td>8.5 </td>
  </tr>
  <tr>
   <td>Microsoft® SharePoint </td>
   <td>2016 (obsolète)<br /> </td>
  </tr>
  <tr>
   <td>Microsoft® SharePoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Prise en charge de Cordova {#support-for-cordova}

L’application AEM Forms prend désormais en charge Apache Cordova. Voici les versions Cordova prises en charge pour chaque plateforme :

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

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
PDF Generator ne prend en charge que les versions allemande, anglaise, française et japonaise des systèmes d’exploitation et des applications pris en charge.
>
En outre :
>
- PDF Generator requiert la version 32 bits d’[Acrobat 2020 (suivi Classic) version 20.004.30006](https://helpx.adobe.com/fr/acrobat/release-note/release-notes-acrobat-reader.html) ou d’Acrobat 2017 version 17.011.30078 pour effectuer la conversion.
- PDF Generator ne prend en charge que la version commerciale 32 bits de Microsoft® Office Professional Plus et d’autres logiciels requis pour la conversion.
- PDF Generator ne prend pas en charge Microsoft® Office 365.
- Les conversions de PDF Generator pour OpenOffice sont uniquement prises en charge sous Windows et Linux®.
- Les fonctionnalités OCR PDF, Optimize PDF et Export PDF sont uniquement prises en charge sous Windows.
- Une version d’Acrobat est fournie avec AEM Forms pour activer la fonctionnalité PDF Generator. La version groupée ne doit être accessible par programmation qu’avec AEM Forms, pendant la durée de la licence AEM Forms, pour une utilisation avec AEM Forms PDF Generator. Pour plus d’informations, voir la description du produit AEM Forms en fonction de votre déploiement ([On-Premise](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-manager-managed-services.html)).
>
- Le service PDF Generator ne prend pas en charge Microsoft® Windows 10.
- PDF Generator ne parvient pas à convertir les fichiers à l’aide de Microsoft® Visio 2019. Vous pouvez continuer à utiliser Microsoft® Visio 2016 pour convertir des fichiers .VSD et .VSDX.
- PDF Generator ne parvient pas à convertir les fichiers à l’aide de Microsoft® Project 2019. Vous pouvez continuer à utiliser Microsoft® Project 2016 pour convertir des fichiers .MPP.
>

### Exceptions de la prise en charge de l’accessibilité {#exceptions-to-accessibility-support}

Les sous-systèmes suivants d’AEM Forms ne sont pas [508](https://www.section508.gov/) compatible :

- Interface utilisateur de création de Forms adaptative
- Interface utilisateur de création de Forms Manager
- Interface de création de Correspondence Management
- Interface utilisateur d’administration (interface utilisateur de la console d’administration)

## Configuration requise pour AEM Forms on JEE {#system-requirements-for-aem-forms-on-jee}

### Configuration matérielle requise {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Plateforme</td>
   <td>Configuration matérielle requise</td>
  </tr>
  <tr>
   <td>Microsoft® Windows Server </td>
   <td>Processeur Intel Xeon® E5-2680, 2,4 GHz ou équivalent<br /> VMware ESX 5.1 ou version ultérieure<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque disponible : 15 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE</td>
  </tr>
  <tr>
   <td>SUSE® Linux® Enterprise Server</td>
   <td>Processeur Intel Xeon® E5-2670v2, 1 processeur virtuel, 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque disponible : 6 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Processeur Intel Xeon® E5-2670v2, 1 processeur virtuel, 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque disponible : 6 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE<br /> </td>
  </tr>
  <tr>
   <td>Configuration matérielle requise pour un environnement de production de petite taille</td>
   <td>
    <ul>
     <li><strong>Environnement Intel®</strong>: Intel Xeon® E5-2680, 2,4 GHz ou plus. L’utilisation d’un processeur à double coeur améliore encore les performances</li>
     <li><strong>Mémoire : </strong>4 Go <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Pour des conditions requises supplémentaires, voir :

- [Configuration requise pour le déploiement sur serveur unique d’AEM Forms on JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_fr)
- [Configuration requise pour le déploiement en grappe d’AEM Forms on JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_fr)

## Clients pris en charge pour AEM Forms on JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plateforme</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Entreprise, Professionnel, Basic)</p> <p>Version 32 bits ou 64 bits</p> <p> </p> </td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
  <tr>
   <td>Serveur Microsoft® Windows® 2016</td>
   <td>Service Packs et mises à jour critiques</td>
  </tr>
 </tbody>
</table>

- Espace disque pour l’installation : 1,7 Go pour Workbench uniquement, 2,7 Go sur un seul lecteur pour une installation complète de Workbench, Designer et des exemples d’assemblage, 400 Mo pour les répertoires d’installation temporaires : 200 Mo dans le répertoire temporaire de l’utilisateur et 200 Mo dans le répertoire temporaire Windows. Si tous ces emplacements se trouvent sur un seul lecteur, 1,5 Go d’espace doit être disponible pendant l’installation. Les fichiers copiés dans les répertoires temporaires sont supprimés à la fin de l’installation.

- Mémoire pour l’exécution de Workbench : 2 Go de mémoire vive
- Configuration matérielle requise : processeur Intel® Pentium® 4 ou AMD® équivalent, cadencé à 1 GHz
- Résolution d’affichage de 1024 X 768 pixels au minimum, écran couleur de 16 bits minimum.
- Connexion réseau TCP/IPv4 ou TCP/IPv6 au serveur AEM Forms on JEE
- Vous devez disposer des droits d’administrateur pour installer Workbench sous Windows. Si vous effectuez l’installation à partir d’un compte non administrateur, le programme d’installation vous demande les informations d’identification d’un compte approprié.

### Designer {#designer}

- Microsoft® Windows® 2016 Server , Microsoft® Windows® 2019 Server ou Microsoft Windows 10
- Processeur de 1 GHz ou plus avec prise en charge de PAE, NX et SSE2.
- Systèmes d’exploitation 32 bits : 1 Go de RAM ; systèmes d’exploitation 64 bits : 2 Go de RAM.
- Systèmes d’exploitation 32 bits : 16 Go d’espace disque ; systèmes d’exploitation 64 bits : 20 Go d’espace disque.
- Mémoire graphique – 128 Mo de GPU (256 Mo recommandé)
- 2,35 Go d’espace disponible sur le disque dur
- Résolution d’écran de 1 024 x 768 pixels ou plus
- Accélération matérielle de la vidéo (facultatif)
- Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC.
- Droits d’administrateur pour l’installation de Designer.

### Adobe Acrobat et Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat et Adobe Reader (version de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (Suivi classique)</td>
   <td>Version 20.004.30006 ou ultérieure<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017 (Suivi classique) (obsolète)</td>
   <td>Version 17.011.30078 ou ultérieure<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
La famille de produits Acrobat DC introduit deux suivis pour Acrobat et Reader, qui sont des produits différents : &quot;Classic&quot; et &quot;Continuous&quot;. Pour plus d’informations et une comparaison des deux suivis, voir [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

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
   <td><p>Microsoft® Edge (Evergreen)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td><p>Service Packs et mises à jour</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A : pris en charge</p> </td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E : Fonctionnement supposé</td>
   <td> Toutes les mises à jour</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A : Pris en charge</p> </td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Apple Safari sous macOS</td>
   <td>A : Pris en charge</td>
   <td>Toutes les mises à jour</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Voici quelques exceptions liées au navigateur pour les ordinateurs de bureau :
>
- Safari est pris en charge uniquement sous Macintosh OS X.
- Workspace prend en charge Safari 5.1 sous Macintosh OS X 10.6 et 10.7 avec Acrobat DC ou versions ultérieures. Pour plus d’informations sur la compatibilité de Safari 5.1 avec Adobe Reader, Acrobat, voir [https://helpx.adobe.com/fr/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/fr/x-productkb/multi/safari-5-1-incompatible-reader.html).
- Administration Console n’est pas prise en charge sur Safari.
- Correspondence Management ne prend pas en charge Windows® Internet Explorer 9.0 pour les formulaires AEM 6.1.
- Forms Portal prend en charge le logiciel de lecteur d’écran JAWS 14.0 sur Internet Explorer 11 pour une meilleure accessibilité.

#### Clients mobiles {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Navigateur (de base)</strong></p> </th>
   <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome sur Android™ 4.1.2 et versions ultérieures</p> </td>
   <td><p>Toutes les mises à jour</p> </td>
  </tr>
  <tr>
   <td>Safari sur iOS 15.1 et versions ultérieures</td>
   <td>Toutes les mises à jour</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>Toutes les mises à jour<br /> </td>
  </tr>
  <tr>
   <td>Navigateur Android™ natif sur Android™ 4.4 et versions ultérieures</td>
   <td>Toutes les mises à jour</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Le Portail Formulaires est pris en charge sur Safari sur iPad uniquement.

### Application AEM Forms {#aem-forms-workspace-app}

#### Prise en charge des périphériques mobiles {#mobile-device-support}

L’application AEM Forms est disponible sur les plateformes suivantes :

| **Plateforme** | **Périphériques pris en charge** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS  | Apple iPhone, iPad, iPad Air et iPad mini exécutant iOS 15.1 et versions ultérieures. |
| Google Android™ | Android™ 5.1 et versions ultérieures. L’application AEM Forms est certifiée sur les tablettes Samsung Galaxy de 7 et 10 pouces ainsi que sur les smartphones les plus populaires. |
| Microsoft® Windows  et versions ultérieures | Microsoft® Périphériques de surface, tablettes, ordinateurs portables et ordinateurs de bureau exécutant Microsoft® système d’exploitation Windows 10. |

### Adobe Document Security Extension for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}

Cliquez [ici](https://www.adobe.com/fr/products/livecycle/rightsmanagement/extension/downloads.html) afin de voir la configuration requise par Adobe Document Security Extension for Microsoft® Office.

### Exceptions de prise en charge de clients {#exceptions-to-client-support}

AEM Forms on JEE prend en charge les mises à jour, les correctifs et les packs de correctifs en plus des versions majeures et mineures spécifiées des logiciels pris en charge. Toutefois, la mise à jour vers la version majeure ou mineure suivante n’est pas prise en charge, sauf indication contraire.

## Règles de prise en charge des correctifs tiers {#third-party-patch-support-policy}

La configuration requise pour l’installation de logiciels tiers pour AEM Forms on JEE est disponible dans la section « Configuration requise » de la documentation des produits concernés. Accès à toute la documentation depuis [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65_fr) .

Les plateformes de référence tierces d’AEM Forms on JEE indiquent le niveau de correctif de l’infrastructure tierce en cours au moment du développement et de la publication d’AEM Forms on JEE, et à partir du niveau minimum de correctif ou pack de services de l’infrastructure prise en charge par cette version d’AEM Forms on JEE.

Adobe prend en charge les correctifs urgents ou recommandés publiés par des fournisseurs tiers à leur publication, en supposant que les fournisseurs tiers garantissent une compatibilité ascendante avec les versions qu’AEM Forms on JEE prend en charge. Adobe ne prend en charge que les correctifs publiés après le niveau minimum de correctif indiqué dans la documentation d’AEM Forms on JEE.

Parfois, Adobe ne prend pas en charge les mises à jour tierces qui modifient des fonctionnalités majeures et ne prennent donc pas en charge la compatibilité ascendante totale. Pour plus d’informations sur les mises à jour prises en charge, consultez la section [Définitions de correctif prises en charge](https://helpx.adobe.com/fr/aem-forms/aem-forms-third-party-software-patch.html) pour les produits de fournisseurs donnés et les types de correctifs qu’Adobe prend en charge.

Dans des circonstances échappant au contrôle d’Adobe, des correctifs tiers revendiquant une compatibilité ascendante peuvent avoir un impact négatif sur les produits ou les environnements clients Adobe. Dans ce cas, Adobe recommande aux clients d’évaluer l’impact de tout correctif urgent provenant d’un tiers avant de l’appliquer aux systèmes critiques. Adobe travaille avec des tiers en utilisant des efforts raisonnables de l’entreprise pour résoudre ces problèmes, soit par le biais de programmes d’assistance à l’Adobe normaux, soit par des tiers rectifiant le problème dans leur correctif. Cela ne garantit pas qu’un nouveau correctif tiers qui sera pris en charge par Adobe fonctionne comme documenté par le fournisseur ou avec AEM Forms on JEE.

Adobe se réserve le droit de modifier les plateformes de référence tierces prises en charge par une version d’AEM Forms on JEE et les définitions de correctif prises en charge à tout moment.

Vous trouverez plus d’informations sur les correctifs tiers en recherchant sur le site d’assistance aux entreprises Adobe les articles de la base de connaissances relatifs à votre produit.

## Mises à jour de Platform {#platform-updates}

Les plateformes suivantes sont marquées comme obsolètes dans la version AEM Forms 6.5.13.0 du 2 juin 2022 :

- Microsoft® SharePoint 2016

Les plateformes suivantes sont marquées comme obsolètes dans la version AEM Forms 6.5.12.0 du 3 mars 2022 :

- MongoDB Enterprise 4.0
- IBM® DB2® 11.1
- Oracle Database 12c Version 2
- MySQL 5.7.35
- Pilote Microsoft® SQL Server JDBC 6.2.1.0
- JBoss® Enterprise Application Platform (EAP) 7.1.4
- IBM® Content Manager Server 8.5 Fix Pack 2
- IBM® Content Manager Client 8.5
- Microsoft® SQL Server 2016

Les plateformes suivantes sont marquées comme obsolètes dans la version AEM Forms 6.5.10.0 du 7 septembre 2021 :

- Adobe Acrobat 2017 - [La prise en charge principale d’Adobe Acrobat 2017 prend fin le 6 juin 2022](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).
- Microsoft® Windows Server 2016 (64 bits)
- Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bits)
- Microsoft® Office 2016
- OpenOffice 4.1.2

>[!NOTE]
>
Les plateformes marquées comme [obsolètes sur AEM Forms 6.5.12.0 et 6.5.10.0 restent prises en charge jusqu’à la version AEM Forms 6.5 Service Pack 18 (6.5.18.0)](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).

## Historique des révisions {#revision-history}

- 1 septembre 2022

   - Ajout de la prise en charge du SDK Oracle Java™ SE 11 (64 bits) pour le serveur d’applications JBoss® EAP 7.4.

- 3 mars 2022

   - Suppression de la prise en charge des éléments suivants :
      - IBM® J9 Virtual Machine (version 2.8, JRE 1.8.0)
      - Oracle Database 12c Version 1
      - Oracle Database 18c
      - Oracle Unified Directory (OUD) 11g Version 2
      - IBM® Lotus Domino 9.0
      - IBM® FileNet 5.2
      - Adobe Flash Player

- 10 octobre 2021

   - Modification de la version prise en charge d’iOS pour l’application AEM Forms en iOS 15.1. La version précédente était iOS 12.

- 7 septembre 2021
   - **Mises à jour de Platform** : [!DNL Adobe Experience Manager Forms] on JEE a ajouté la prise en charge des plateformes suivantes :
      - [!DNL Adobe Acrobat 2020]
      - [!DNL Ubuntu 20.04]
      - [!DNL Open Office 4.1.10]
      - [!DNL Microsoft® Office 2019]
      - [!DNL Microsoft® Windows Server 2019]
      - [!DNL RHEL8]

- 3 décembre 2020
   - Ajout de la prise en charge d’AEM Forms 6.5.7.0 ou version ultérieure pour la plateforme suivante :
      - [!DNL Microsoft® SQL Server 2019]

- 9 septembre 2020

   - Modification de la version prise en charge d’iOS pour l’application AEM Forms en iOS 12. La version précédente était iOS 11.

