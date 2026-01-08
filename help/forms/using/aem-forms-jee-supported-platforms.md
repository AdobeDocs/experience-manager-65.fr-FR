---
title: Plateformes prises en charge pour AEM Forms on JEE
description: Liste des composants d’infrastructure requis et pris en charge pour installer AEM Forms on JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: b2ef2498976ffb46238c4dee75df32a214c82300
workflow-type: tm+mt
source-wordcount: '3708'
ht-degree: 99%

---



# Plateformes prises en charge pour AEM Forms on JEE {#supported-platforms-for-aem-forms-on-jee}


## Plateformes prises en charge {#supported-platforms}


<div class="preview">

Adobe a publié un [programme d’installation complet](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) avec le pack de services 23 d’AEM 6.5.23.0 Forms (6.5.23.0) on JEE, ainsi que les programmes d’installation de correctifs. Le programme d’installation complet prend en charge les nouvelles plateformes, tandis que le programme d’installation de correctifs ne comprend que des correctifs.

Si vous effectuez une nouvelle installation ou prévoyez d’utiliser la version la plus récente du logiciel pour votre environnement AEM 6.5.23.0 Forms on JEE, Adobe recommande d’utiliser l’installateur complet [AEM 6.5.23.0Forms sur JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr), version publiée le 6 juin 2025, plutôt que l’installateur AEM 6.5.18 Forms publié le 31 août 2023 ou l’installateur AEM 6.5.12 Forms publié le 8 avril 2019.


</div>


### Niveaux de prise en charge {#support-levels}


Le serveur AEM Forms on JEE peut être installé sur toute combinaison de systèmes d’exploitation, de serveurs d’applications, de bases de données, de pilotes de base de données, de JDK, de serveurs LDAP et de serveurs de messagerie électronique pris en charge.


Ce document répertorie les plateformes client et serveur prises en charge pour AEM Forms on JEE. Adobe fournit plusieurs niveaux de prise en charge pour les configurations recommandées par Adobe et pour d’autres configurations. Ce document dresse également la liste des autres logiciels et versions pris en charge, des exceptions, des définitions de correctif et des règles de prise en charge des correctifs logiciels de fournisseurs tiers.


>[!NOTE]
>
>- Pour une liste complète des exceptions concernant les plateformes de serveur prises en charge, consultez [Exceptions aux plateformes de serveur prises en charge](#exceptions-to-supported-server-platforms).
>- AEM Forms on JEE ne prend en charge que les versions allemande, anglaise, française et japonaise des systèmes d’exploitation et des applications pris en charge.

### Politique de mise à niveau et de prise en charge

#### Programme d’installation complet

- **Prise en charge de la mise à niveau pour les programmes d’installation complets** : un programme d’installation complet est publié tous les 6 Packs de services AEM. Par exemple, un programme d’installation complet a été publié avec les versions des packs de services 6.5.12.0 et 6.5.18.0. AEM Forms permet des mises à niveau directes exclusivement à partir des deux derniers programmes d’installation complets. Par exemple, AEM Forms facilite les mises à niveau directes vers la version 6.5.23.0 uniquement à partir des deux derniers programmes d’installation complets, à savoir 6.5.18.0 et 6.5.12.0. Si vous devez effectuer une mise à niveau à partir d’une mise à niveau antérieure, vous pouvez utiliser une mise à niveau en plusieurs étapes pour accéder d’abord à une version complète du programme d’installation prise en charge, puis à la dernière version.

- **Obsolescence** : la prise en charge des plateformes est mise à jour avec chaque version du programme d’installation complet. Tout logiciel marqué comme obsolète dans la matrice de plateforme peut être supprimé des plateformes prises en charge dans les versions ultérieures ou lorsque le logiciel atteint la fin de support.

#### Packs de services


- **Couverture des Packs de services** : Adobe fournit une assistance technique pour les environnements AEM Forms utilisant un des six derniers Packs de services. Si votre version actuelle est antérieure aux six derniers Packs de services, Adobe recommande vivement d’effectuer une mise à niveau vers la dernière version afin d’optimiser les performances, la sécurité et la continuité de la prise en charge.

- **Instructions sur la mise à jour de correctifs** : lors de l’utilisation des programmes d’installation de correctifs pour la mise à jour, il est essentiel de vérifier que l’ancienneté de la version du programme d’installation complet sous-jacent ne dépasse pas deux versions. Par exemple, lors de l’installation du pack de services 6.5.23.0, vérifiez que la version du programme d’installation complet sous-jacent est 6.5.18.0 ou 6.5.12.0.

<!--
- **Patch Upgrade Support**: You can upgrade from an older service pack to a newer one (for example, from 6.5.18.0 to 6.5.23.0) using the patch installer, as long as the destination platform (OS, JDK, application server, etc.) is supported by the newer service pack.-->

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
  <td>Adobe fournit une prise en charge et une maintenance complètes de cette configuration. Cette configuration est couverte par le processus d’assurance qualité d’Adobe.</td>
 </tr>
 <tr>
  <td>R : Prise en charge limitée </td>
  <td>Adobe fournit une prise en charge complète pour cette configuration si certaines conditions préalables sont remplies. Contactez l’assistance aux entreprises d’Adobe pour connaître les conditions et demander une prise en charge.</td>
 </tr>
 <tr>
  <td>L : prise en charge limitée</td>
  <td>Adobe fournit une prise en charge complète et une maintenance pour cette configuration si certaines conditions préalables sont remplies. Toutes les fonctionnalités ne sont pas disponibles sur la configuration. Contactez l’assistance aux entreprises d’Adobe pour connaître les conditions et demander une prise en charge.<br /> </td>
 </tr>
</tbody>
</table>


### Configurations non prises en charge {#unsupported-configurations}


| Niveau de prise en charge | Description |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E : Fonctionnement supposé | Il est prévu que la configuration fonctionne normalement et nous n’avons reçu aucun rapport faisant état de problèmes. |
| Z : non pris en charge | La configuration n’est pas prise en charge. Adobe ne fait aucune déclaration indiquant si la configuration fonctionne et ne la prend pas en charge. |


>[!NOTE]
>
>Pour aider les clients d’AEM Forms à réduire le coût de possession, à simplifier l’architecture de déploiement et à moderniser la pile de développement, la plateforme d’entreprise Adobe Experience Manager délaisse les déploiements sur serveur d’applications au profit de déploiements OSGi autonomes. Adobe continue de prendre en charge la pile AEM Forms JEE avec une matrice réduite de composants d’infrastructure.
><br>
>Avec la version 6.5, les composants d’infrastructure les moins utilisés par nos clientes et clients Adobe ne sont plus pris en charge :
>
> - Base de données IBM® DB2®
> - Systèmes d’exploitation IBM® AIX® et Sun Solaris™
>
>
>Pour les nouvelles installations, il est recommandé, dans la mesure du possible, de déployer AEM Forms sur la pile OSGi moderne afin d’utiliser les dernières innovations en matière de formulaires adaptatifs réactifs pour les communications mobiles et interactives multicanaux, ainsi que des intégrations de données backend utilisant le modèle de données de formulaire.
>
>Adobe reconnaît que les utilisateurs et utilisatrices actuels doivent continuer à déployer la pile AEM Forms on JEE. Dans ce cas de figure, Adobe nécessite le déploiement d’AEM Forms JEE sur une infrastructure prise en charge, comme décrit dans cette documentation. Si vous effectuez une mise à niveau vers AEM 6.5 Forms et que vous utilisez une plateforme non prise en charge sur la version précédente d’AEM Forms, vous pouvez contacter l’assistance technique d’Adobe pour obtenir de l’aide sur la mise à niveau vers une plateforme prise en charge.

### Machines virtuelles Java™ (JVM) {#java-virtual-machines-jvm}


Adobe Experience Manager Forms nécessite l’exécution d’une machine virtuelle Java™, laquelle est fournie par la distribution JDK (Java™ Development Kit). Adobe Experience Manager fonctionne avec les versions suivantes des machines virtuelles Java™ :


<table>
<tbody>
 <tr>
  <th><p><strong>Plateforme</strong></p> </th>
  <th><p><strong>Niveau de prise en charge</strong></p> </th>
  <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
 </tr>
 <tr>
  <td><p>Oracle Java™ SE 11 (64 bits) <sup> [8] </sup> </p>  </td>
  <td><p>A : pris en charge</p> </td>
  <td><p>Versions et mises à jour mineures </p> </td>
 </tr>
 <tr>
  <td>Azul Zulu OpenJDK 11 64 bits</td>
  <td>Z : non pris en charge</td>
  <td><p> </p> </td>
 </tr>
 <tr>
  <td>Azul Zulu OpenJDK 8 64 bits</td>
  <td>Z : non pris en charge</td>
  <td><p> </p> </td>
 </tr>
 <tr>
  <td>Oracle Java™ SE 8 (64 bits)</td>
  <td>A : pris en charge</td>
  <td>Versions et mises à jour mineures</td>
 </tr>
 <tr>
  <td>IBM® J9 Virtual Machine (version 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
  <td>A : pris en charge</td>
  <td>Versions et mises à jour mineures</td>
 </tr>
 <tr>
  <td>IBM® JAVA1.8.0_291(version 8.0.6.30)<br /> </td>
  <td>A : pris en charge</td>
  <td>Versions et mises à jour mineures</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>- Consultez les bulletins de sécurité publiés par l’éditeur Java™ afin de garantir la sécurité des environnements de production et d’installer les mises à jour Java™ les plus récentes.
>- AEM Forms on JEE ne prend en charge que les JVM 64 bits pour les environnements de production.

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
  <td><p> MongoDB Enterprise 6.0 (obsolète) </p> </td>
  <td><p>Référentiel Microkernel</p> </td>
  <td><p>Pris en charge</p> </td>
 </tr>
 <tr>
  <td><p> MongoDB Enterprise 7.0 </p> </td>
  <td><p>Référentiel Microkernel</p> </td>
  <td><p>Pris en charge</p> </td>
 </tr>
  <tr>
  <td>Oracle Database 19c (éditions Standard, Real Application Clusters (RAC) et Enterprise) </td>
  <td>Référentiel Microkernel </td>
  <td>Pris en charge</td>
 </tr>
 <tr>
  <td><p>Référentiel Microkernel</p> </td>
  <td><p>Pris en charge</p> </td>
  <td></td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2019 (obsolète) </p> </td>
  <td><p>Référentiel Microkernel</p> </td>
  <td><p>Pris en charge</p> </td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2022 </p> </td>
  <td><p>Référentiel Microkernel</p> </td>
  <td><p>Pris en charge</p> </td>
 </tr>
 <tr>
  <td>IBM® DB2® 11.1 (obsolète)</td>
  <td>Référentiel Microkernel</td>
  <td>R : Prise en charge limitée</td>
 </tr>
 <tr>
 <tr>
  <td>MySQL 8.0.27 (obsolète) </td>
  <td>-</td>
  <td>R : Prise en charge limitée </td>
 </tr>
 <tr>
 <tr>
  <td>MySQL 8.4</td>
  <td>-</td>
  <td>R : Prise en charge limitée </td>
 </tr>
</tbody>
</table>


- IBM® DB2® n’est pas pris en charge pour les nouvelles installations. Il n’est pris en charge que pour les clients et clientes existants qui effectuent une mise à niveau vers AEM Forms 6.5.
- MongoDB est un logiciel tiers non inclus dans le package de licence d’AEM. Pour plus d’informations, voir la [Politique de licence de MongoDB](https://www.mongodb.org/about/licensing/).
- Pour tirer pleinement parti de votre déploiement AEM, Adobe conseille d’utiliser la version MongoDB Enterprise sous licence afin de bénéficier d’une assistance professionnelle.
@@ -242,187 +206,150 @@ Adobe Experience Manager Forms nécessite une machine virtuelle Java™ pour fonctionner,
- Le module Document Security n’utilise pas le référentiel de contenu. Cela signifie que si vous utilisez uniquement Document Security et que vous ne prévoyez pas d’utiliser HTML Workspace, HTML5 Forms ou des formulaires adaptatifs, n’installez pas le référentiel de contenu.
- AEM Forms on JEE ne prend pas en charge l’utilisation de MySQL pour la conservation du référentiel AEM (référentiel CRX).


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
  <td><p>MySQL Connector/J 5.7 (obsolète)</p> </td>
  <td><p>Fourni avec l’installation d’AEM Forms on JEE.</p> </td>
 </tr>
 <tr>
  <td>MySQL</td>
  <td><p>MySQL Connector/J 8.4</p> </td>
  <td><p>Fourni avec l’installation d’AEM Forms on JEE.</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server <br /> </td>
  <td><p>Pilote Microsoft® SQL Server JDBC 8.2.2 <br /> </p> <p>sqljdbc8.jar (obsolète) </p> </td>
  <td><p>À télécharger depuis le site web de Microsoft®.</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server <br /> </td>
  <td><p>Pilote Microsoft® SQL Server JDBC 12.10.0 <br /> </p> <p>sqljdbc12.10.0.jar</p> </td>
  <td><p>À télécharger depuis le site web de Microsoft®.</p> </td>
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
  <td>Oracle WebLogic Server 12.2.1 (12c R2) (obsolète) <sup>[9]</sup></td>
  <td>A : pris en charge</td>
  <td>Pack de services et mises à jour critiques</td>
 </tr>
 <tr>
  <td>Oracle WebLogic Server 14c <sup>[9]</sup></td>
  <td>A : pris en charge</td>
  <td>Pack de services et mises à jour critiques</td>
 </tr>
 <tr>
  <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
  <td>A : pris en charge</td>
  <td>Pack de services et mises à jour critiques</td>
 </tr>
 <tr>
  <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
  <td><p>A : pris en charge</p> </td>
  <td><p>Correctifs et correctifs cumulatifs pour la version EAP prise en charge</p> </td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>Les clusters IBM® WebSphere® ne sont pris en charge que dans les éditions Network Deployment.

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
  <td>Microsoft® Windows Server 2019 (64 bits) (obsolète)</td>
  <td>A : pris en charge</td>
  <td>Service Packs et mises à jour critiques</td>
 </tr>
    <tr>
  <td>Microsoft® Windows Server 2022 (64 bits)</td>
  <td>A : pris en charge</td>
  <td>Service Packs et mises à jour critiques</td>
 </tr>
 <tr>
  <td>Ubuntu 20.04</td>
  <td>A : pris en charge</td>
  <td>Service Packs et mises à jour critiques</td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bits) (obsolète)</p> </td>
  <td><p>A : pris en charge</p> </td>
  <td><p>Révisions mineures, mises à jour cumulatives et mises à jour critiques</p> </td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 9 (Kernel 4.x) (64 bits)</p> </td>
  <td><p>A : pris en charge</p> </td>
  <td><p>Révisions mineures, mises à jour cumulatives et mises à jour critiques</p> </td>
 </tr>
 <tr>
  <td><p>SUSE® Linux® Enterprise Server 15 SP6 (64-bit) </p> </td>
  <td><p>A : pris en charge</p> </td>
  <td><p>Packs de services, correctifs cumulatifs et mises à jour de sécurité critiques</p> </td>
 </tr>
 <tr>
  <td>Oracle Linux® 7 Mise à jour 3 (64 bits)</td>
  <td>A : pris en charge</td>
  <td>Packs de services, correctifs cumulatifs et mises à jour de sécurité critiques</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
> Pour les serveurs basés sur Linux®, les dépendances d’exécution requises sont les suivantes :
>
> - glibc.x86_64 (2.17-196)
> - libX11.x86_64 (1.6.7-4)
> - zlib.x86-64 (1.2.7-17)
> - libxcb.x86_64 (1.13-1.el7)
> - libXau.x86_64 (1.0.8-2.1.el7)
> - glibc-locale.x86_64 (2.17 ou version ultérieure)
> - OpenSSL 3 (requis à l’emplacement par défaut sur le système d’exploitation).

Pour l’installation d’OpenSSL 3 : les bibliothèques libcrypto.so.3 et libssl.so.3 doivent être disponibles dans le chemin d’accès par défaut à la bibliothèque, représenté par la variable d’environnement LD_LIBRARY_PATH. Si elles sont installées dans un emplacement non standard, assurez-vous que ce chemin est ajouté à LD_LIBRARY_PATH avant de démarrer le serveur.

#### Environnement virtualisé {#virtualized-environment}


Vous pouvez exécuter AEM Forms on JEE sur un ordinateur physique ou un environnement virtuel. Toutefois, si vous rencontrez un problème avec AEM Forms sur un environnement virtuel, essayez de reproduire le problème sur un ordinateur physique. Si le problème persiste sur l’ordinateur physique, contactez l’assistance technique d’Adobe pour le résoudre. Pour les problèmes qu’il n’est pas possible de reproduire sur un ordinateur physique, contactez le fournisseur de votre environnement virtuel.


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
  <td><p>Pack de services et mises à jour critiques</p> </td>
 </tr>
</tbody>
</table>

### Exceptions aux plateformes de serveur prises en charge {#exceptions-to-supported-server-platforms}


Tenez compte des exceptions suivantes lorsque vous choisissez la plateforme de configuration d’AEM Forms on JEE.


1. AEM Forms on JEE ne prend pas en charge IBM® WebSphere® avec MySQL.
1. AEM Forms on JEE ne prend pas en charge JBoss® sur SUSE® Linux® Enterprise Server 12. Seul IBM® WebSphere® est pris en charge sur SUSE® Linux® Enterprise Server 12.
1. AEM Forms on JEE ne prend en charge aucun autre JDK avec JBoss® qu’Oracle Java™ SE.
1. AEM Forms on JEE ne prend en charge aucun autre JDK avec IBM® WebSphere® que le JDK IBM®.
1. Le référentiel CRX prend en charge la persistance de type TarMK, MongoDB et les bases de données relationnelles (RDBMK). Vous ne pouvez pas avoir deux systèmes de bases de données différents entre le serveur d’applications et le référentiel CRX. Cependant, dans un environnement AEM Forms on JEE, vous pouvez utiliser MongoMK avec le référentiel CRX et une base de données relationnelle prise en charge avec le serveur d’applications.
@@ -432,12 +359,12 @@ Tenez compte des exceptions suivantes lorsque vous choisissez une plateforme pour configurer votre AEM F
1. Les versions de JDK supérieures à 1.8.0_281 ne sont pas prises en charge pour le serveur WebLogic. (FORMS-8498)
1. JDK 11.0.20 n’est pas pris en charge pour installer le programme d’installation AEM Forms on JEE. Seules la version JDK 11.0.19 ou les versions antérieures sont prises en charge pour installer le programme d’installation AEM Forms on JEE.

1. [!DNL Microsoft® Windows Server 2019] ne prend pas en charge [!DNL MySQL 5.7] et [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] ne prend donc pas en charge les installations clé en main pour [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312)


Tenez également compte des points suivants lors de votre choix de logiciels pour le déploiement d’Adobe AEM Forms on JEE :


- AEM Forms on JEE prend en charge les mises à jour, les correctifs et les packs de correctifs en plus des versions majeures et mineures spécifiées du logiciel pris en charge. Toutefois, la mise à jour à la version majeure ou mineure suivante n’est pas prise en charge sauf indication contraire.
- Les installations en cluster ne prennent pas en charge la persistance de TarMK. Pour plus d’informations sur la persistance prise en charge, voir [Choix d’un type de persistance pour une installation AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- AEM Forms on JEE prend en charge divers logiciels tiers, conformément à la [Politique de prise en charge des logiciels tiers](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p) d’Adobe.
@@ -449,274 +376,219 @@ En outre, tenez compte des points suivants lors du choix du logiciel pour Adobe AEM

### Serveurs LDAP (facultatifs) {#ldap-servers-optional}


<table>
<tbody>
 <tr>
  <th><p><strong>Produit (version de base)</strong></p> </th>
  <th><p><strong>Définitions de correctif prises en charge</strong></p> </th>
 </tr>
 <tr>
  <td>Microsoft® Active Directory 2016 (obsolète)</td>
  <td>Versions de maintenance et packs de correctifs</td>
 </tr>
 <tr>
  <td>Microsoft® Active Directory 2022</td>
  <td>Versions de maintenance et packs de correctifs</td>
 </tr>
 <tr>
  <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
  <td><p>Packages de fonctionnalités et correctifs intermédiaires</p> </td>
 </tr>
</tbody>
</table>


### Serveurs de messagerie (facultatifs) {#email-servers-optional}


| Produit |
| ----------------------- |
| Microsoft® Exchange 2013 |
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
  <td>IBM® Filenet</td>
  <td>5.5.2</td>
 </tr>
 <tr>
  <td>IBM® Content Manager Server (obsolète) </td>
  <td>8.5 Fix pack 2</td>
 </tr>
  <tr>
  <td> IBM® Content Manager Client (obsolète)</td>
  <td>8.5 </td>
 </tr>
  <td>Microsoft® Sharepoint </td>
  <td>2019<br /> </td>
 </tr>
</tbody>
</table>


### Prise en charge de Cordova {#support-for-cordova}


L’application AEM Forms prend désormais en charge Apache Cordova. Voici les versions Cordova prises en charge pour chaque plateforme :


- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

### Conditions requises pour PDF Generator

<table>
 <tbody>
  <tr>
   <th><p><strong>Produit</strong></p> </th>
   <th><p><strong>Formats pris en charge pour la conversion en PDF</strong></p> </th>
  </tr>
  <tr>
   <td>Dernière version d’<a href="https://helpx.adobe.com/fr/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a></td>
   <td>XPS, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML et HTM</td>
  </tr>

<tr>
   <td>Licences Microsoft® Office 2021 Professional Plus, licences au détail et en volume</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF et TXT</td>
  </tr>
  <tr>
   <td>
    <strong>OpenOffice 4.1.15</strong>   </td>
   <td>
    ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formats d’image (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF et TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- PDF Generator ne prend en charge que les versions allemande, anglaise, française et japonaise des systèmes d’exploitation et des applications pris en charge.
>- PDF Generator nécessite Adobe Acrobat Pro DC (32 bits) pour effectuer la conversion.
>- PDF Generator prend uniquement en charge la version 32 bits de Microsoft® Office Professional Plus et d’autres logiciels requis pour la conversion.
>- Si une installation Microsoft® Office est désactivée ou n’a pas de licence pour une raison quelconque, par exemple si une installation sous licence en volume ne parvient pas à localiser un hôte KMS dans un délai spécifié, les conversions peuvent échouer jusqu’à ce que l’installation reçoive une nouvelle licence et soit réactivée.
>- PDF Generator ne prend pas en charge Microsoft® Office 365.
>- Les conversions PDF Generator pour OpenOffice sont prises en charge sous Windows et Linux®.
>- Les fonctionnalités OCR PDF, Optimize PDF et Export PDF sont uniquement prises en charge sous Windows.
>- Le service PDF Generator ne prend pas en charge Microsoft® Windows 11.


PDF Generator prend uniquement en charge la version 32 bits de Microsoft® Office Professional Plus et d’autres logiciels requis pour la conversion.


L’installation de Microsoft® Office Professional Plus peut utiliser des licences en volume Retail ou MAK/KMS/AD.


Si une installation Microsoft® Office est désactivée ou n’a pas de licence pour une raison quelconque, par exemple si une installation sous licence en volume ne parvient pas à localiser un hôte KMS dans un délai spécifié, les conversions peuvent échouer jusqu’à ce que l’installation reçoive une nouvelle licence et soit réactivée.

<!-- Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.-->


### Exceptions de la prise en charge de l’accessibilité {#exceptions-to-accessibility-support}


Les sous-systèmes suivants d’AEM Forms ne sont pas conformes à la section [508](https://www.section508.gov/) :


- Interface utilisateur de création des formulaires adaptatifs
- Interface utilisateur de création de Forms Manager
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
  <td>Processeur Intel® Xeon® E5-2680, 2,4 GHz ou équivalent<br /> VMWare ESX 5.1 ou version ultérieure<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque libre : 15 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE</td>
 </tr>
 <tr>
  <td>SUSE® Linux® Enterprise Server</td>
  <td>Processeur Intel® Xeon E5-2670v2, 1 processeur virtuel, 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque disponible : 6 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE</td>
 </tr>
 <tr>
  <td>Red Hat® Enterprise Linux®</td>
  <td>Processeur Intel® Xeon E5-2670v2, 1 processeur virtuel, 2,5 GHz<br /> AWS m3.medium (3 ECU)<br /> RAM : 6 Go (système d’exploitation 64 bits avec JVM 64 bits)<br /> Espace disque disponible : 6 Go d’espace temporaire plus 22 Go<br /> pour AEM Forms on JEE<br /> </td>
 </tr>
 <tr>
  <td>Configuration matérielle requise pour un petit environnement de production</td>
  <td>
   <ul>
    <li><strong>Environnement Intel®</strong> : Intel Xeon® E5-2680, 2,4 GHz ou plus. L’utilisation d’un processeur à double cœur améliore encore les performances</li>
    <li><strong>Mémoire : </strong>4 Go <br /> </li>
   </ul> </td>
 </tr>
</tbody>
</table>


Pour des conditions requises supplémentaires, voir :

- [Configuration requise pour le déploiement sur serveur unique d’AEM Forms on JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_fr)
- [Configuration requise pour le déploiement en grappe d’AEM Forms on JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_fr)


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
 </tbody>
</table>


>[!NOTE]
>
>La famille de produits Acrobat DC présente deux suivis pour Acrobat et Reader qui sont des produits différents : « Classique » et « Continu ». Pour plus d’informations et une comparaison des deux suivis, voir [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

## Clients pris en charge pour AEM Forms on JEE {#supported-clients-for-aem-forms-on-jee}


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
  <td>Microsoft® Windows® 2019 Server (obsolète)</td>
  <td>Packs de services et mises à jour critiques</td>
 </tr>
 <tr>
  <td>Microsoft® Windows® 2022 Server</td>
  <td>Packs de services et mises à jour critiques</td>
 </tr>
</tbody>
</table>


- Espace disque pour l’installation : 1,7 Go pour Workbench uniquement, 2,7 Go sur un seul lecteur pour une installation complète de Workbench, Designer et des exemples d’assemblage, 400 Mo pour installer les répertoires temporaires (200 Mo dans le répertoire utilisateur temporaire et 200 Mo dans le répertoire temporaire Windows). si l’ensemble de ces emplacements se trouve sur un seul disque, vous devez allouer un total de 1,5 Go lors de l’installation. Les fichiers copiés dans les répertoires temporaires sont supprimés à la fin de l’installation.


- Mémoire pour l’exécution de Workbench : 2 Go de mémoire vive.
- Configuration matérielle requise : processeur Intel® Pentium® 4 ou AMD® équivalent, processeur cadencé à 1 GHz.
- Résolution d’affichage de 1024 X 768 pixels au minimum, écran couleur de 16 bits minimum.
- La connexion réseau via le protocole TCP/IPv4 ou TCP/IPv6 au serveur AEM Forms on JEE
- vous devez disposer des droits d’administration pour pouvoir installer Workbench sous Windows. Si vous effectuez l’installation à partir d’un compte non administrateur, le programme d’installation vous demande les informations d’identification d’un compte approprié.


### Concepteur {#designer}


- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft Windows 10 ou Windows® 11
- Processeur d’1 GHz ou plus avec prise en charge de PAE, NX et SSE2.
- 1 Go de RAM pour un système d’exploitation 32 bits ou 2 Go de RAM pour un système d’exploitation 64 bits
@@ -729,49 +601,45 @@ Pour plus d’informations, voir :
- Droits d’administration pour l’installation de Designer
- Microsoft® Visual C++ 2019 (VC 14.28 ou version ultérieure) Runtime 32 bits


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
  <td><p>A : pris en charge</p> </td>
  <td><p>Packs de services et mises à jour critiques</p> </td>
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
  <td><p>A : pris en charge</p> </td>
  <td>Toutes les mises à jour</td>
 </tr>
 <tr>
  <td>Apple Safari sous macOS</td>
  <td>A : pris en charge</td>
  <td>Toutes les mises à jour</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>Voici quelques exceptions liées au navigateur pour les ordinateurs de bureau :
>
>- Correspondence Management ne prend pas en charge Windows® Internet Explorer 9.0 pour les formulaires AEM 6.1.
>- Le portail Formulaires prend en charge le logiciel de lecteur d’écran JAWS 14.0 sur Internet Explorer 11 pour une meilleure accessibilité.

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
  <td>Safari sur iOS 15.1 et versions ultérieures</td>
  <td>Toutes les mises à jour</td>
 </tr>
 <tr>
  <td>Microsoft® Edge<br /> </td>
  <td>Toutes les mises à jour<br /> </td>
 </tr>
 <tr>
  <td>Navigateur Android™ natif sous Android™ 4.4 et versions ultérieures</td>
  <td>Toutes les mises à jour</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>- Le Portail Formulaires est pris en charge sur Safari sur iPad uniquement.

### Application AEM Forms {#aem-forms-workspace-app}


#### Prise en charge des appareils mobiles {#mobile-device-support}


L’application AEM Forms est disponible sur les plateformes suivantes :


| **Plateforme** | **Appareils pris en charge** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS  | Apple iPhone, iPad, iPad Air et iPad mini exécutant iOS 15.1 et versions ultérieures. |
| Google Android™ | Android™ 5.1 et versions ultérieures. L’application AEM Forms est certifiée sur les tablettes Samsung Galaxy de 7 et 10 pouces, ainsi que sur les smartphones les plus populaires. |
| Microsoft® Windows | Appareils Microsoft® Surface, tablettes, ordinateurs portables et ordinateurs de bureau exécutant le système d’exploitation Microsoft® Windows 10. |


### Extension d’Adobe Document Security for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}


Cliquez [ici](https://www.adobe.com/fr/products/livecycle/rightsmanagement/extension/downloads.html) afin de voir la configuration requise par Adobe Document Security Extension for Microsoft® Office.


### Exceptions de prise en charge de clients {#exceptions-to-client-support}


AEM Forms on JEE prend en charge les mises à jour, les correctifs et les packs de correctifs en plus des versions majeures et mineures spécifiées du logiciel pris en charge. Toutefois, la mise à jour à la version majeure ou mineure suivante n’est pas prise en charge sauf indication contraire.


## Règles de prise en charge des correctifs de fournisseurs tiers {#third-party-patch-support-policy}


La configuration requise pour l’installation de logiciels tiers pour AEM Forms on JEE est disponible dans la section « Configuration requise » de la documentation des produits concernés. Accédez à toute la documentation depuis [https://adobe.com/go/learn_aemforms_documentation_65_fr](https://adobe.com/go/learn_aemforms_documentation_65_fr).


Les plateformes de référence de fournisseurs tiers d’AEM Forms on JEE indiquent le niveau de correctif de l’infrastructure de fournisseur tiers en cours au moment du développement et de la publication d’AEM Forms on JEE, et forment le niveau minimum de correctif/pack de services de l’infrastructure prise en charge par cette version d’AEM Forms on JEE.


Adobe prend en charge les correctifs urgents ou recommandés publiés par des fournisseurs tiers lors de leur publication, en supposant que les fournisseurs tiers garantissent une compatibilité ascendante avec les versions qu’AEM Forms on JEE prend en charge. Adobe ne prend en charge que les correctifs publiés après le niveau minimum de correctif indiqué dans la documentation d’AEM Forms on JEE.


Dans certains cas, Adobe ne prend pas en charge les mises à jour de fournisseurs tiers qui modifient des fonctionnalités importantes, et ne permettent donc pas une compatibilité ascendante totale. Pour plus d’informations sur les mises à jour prises en charge, consultez la section [Définitions de correctif prises en charge](https://helpx.adobe.com/fr/aem-forms/aem-forms-third-party-software-patch.html) pour les produits de fournisseurs donnés et les types de correctifs qu’Adobe prend en charge.


Dans des circonstances échappant au contrôle d’Adobe, des correctifs tiers revendiquant une compatibilité ascendante peuvent avoir un impact négatif sur les produits ou les environnements clients Adobe. Dans ce cas, Adobe recommande aux clients et clientes d’évaluer l’impact de tout correctif urgent provenant d’un fournisseur tiers avant de l’appliquer aux systèmes critiques. Adobe collabore avec des tierces parties et engage des efforts commerciaux raisonnables pour résoudre ce genre de problèmes, soit par le biais de programmes d’assistance Adobe normaux, soit par l’intermédiaire de tiers qui rectifient le problème dans un correctif. Cela ne garantit pas qu’un correctif tiers récemment publié, pris en charge par Adobe, fonctionne tel que le documente le fournisseur ou avec AEM Forms on JEE.


Adobe se réserve le droit de modifier à tout moment les plateformes de fournisseurs tiers de référence prises en charge par une version d’AEM Forms on JEE et les définitions de correctif prises en charge.


Vous trouverez plus d’informations sur les correctifs de fournisseurs tiers en recherchant sur le site de support aux entreprises d’Adobe les articles de la base de connaissances relatifs à votre produit.

Pour toute question relative aux formats ou aux versions de plateforme pris en charge, contactez l’assistance technique d’[AEM Forms](https://business.adobe.com/in/support/main.html)

<!--

## Platform updates {#platform-updates}
The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:
- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016
The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016
The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:
- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit)
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2
-->




## Historique des révisions {#revision-history}


<!--
- 6.5.18.0 (Aug 31, 2023)
 - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
   - MongoDB Enterprise 4.4
   - Oracle WebLogic Server 14c
   - My SQL JDBC connector 8
   - Active Directory 2022
   - Microsoft&reg; Windows Server 2022 (64-bit)
 - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
   - Windows Server 2016 (64-bit)
   - MongoDB Enterprise 4.0
   - Oracle Database 12c Release 2 (12.2.0.1.0)
   - MySQL 5.7.35
   - Microsoft&reg; SQL Server 2016
   - JBoss&reg; EAP 7.1.4
   - My SQL JDBC connector 5.1.44
   - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
   - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
   - Microsoft&reg; JDBC Driver 8.x for SQL Server
   The release has also removed support for the following platforms for PDF Generator and in-general:
   - Microsoft&reg; Sharepoint 2016
   - Microsoft&reg; Office 2016
   - Microsoft&reg; Office Visio 2016
   - Microsoft&reg; Publisher 2016
   - Microsoft&reg; Project 2016
   - OpenOffice 4.1.2
   - Acrobat 2017 (Classic track) Version 17.011.30078 or later
 - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
   - Microsoft&reg; Windows Server 2019 (64-bit)
   - Microsoft&reg; Active Directory 2016
  
- 6.5.13.0 (June 2, 2022)
 The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 - Microsoft&reg; SharePoint 2016
- 6.5.12.0 (March 3, 2022)
   - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
     - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
     - Oracle Database 12c Release 1
     - Oracle Database 18c
     - Oracle Unified Directory (OUD) 11g Release 2
     - IBM&reg; Lotus Domino 9.0
     - IBM&reg; FileNet 5.2
     - Adobe Flash Player
   - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
     - MongoDB Enterprise 4.0
     - MongoDB Enterprise 4.2
     - IBM&reg; DB2&reg; 11.1
     - Oracle Database 12c Release 2
     - MySQL 5.7.35
     - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
     - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
     - IBM&reg; Content Manager Server 8.5 Fix pack 2
     - IBM&reg; Content Manager Client 8.5
     - Microsoft&reg; SQL Server 2016
- 6.5.10.0 (Sep 01, 2022)
 - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
 - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
   - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/fr/support/programs/eol-matrix.html).
   - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
   - Microsoft&reg; Windows Server 2016 (64-bit)
   - Microsoft&reg; Office 2016
   - OpenOffice 4.1.2
### Release 6.5.23.0 (June 06, 2025)
| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 |    MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 |SUSE&reg; Linux&reg; Enterprise Server 12 (64-bit) | MYSQL 8.0.27 |
| Microsoft&reg; SQL Server 2022 | |Microsoft&reg; SQL Server 2019 |
| Microsoft&reg; SQL Server JDBC driver 12.8 | | Microsoft&reg; SQL Server JDBC driver 8.2 |
| Microsoft&reg; Office 2021 | | Microsoft&reg; Office 2019 |
| Red Hat&reg; Enterprise Linux&reg; 9 (Kernel 4.x) (64-bit) | |Red Hat&reg; Enterprise Linux&reg; 8 (Kernel 4.x) (64-bit)  |
-->

### Version 6.5.23.0 (6 juin 2025)

| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 | MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 | SUSE® Linux® Enterprise Server 12 (64 bits) | MYSQL 8.0.27 |
| Microsoft® SQL Server 2022 | Centos 7 | Microsoft® SQL Server 2019 |
| Pilote Microsoft® SQL Server JDBC 12.10.0 | Red Hat® Enterprise Linux® 7 (Kernel 4.x) (64 bits) | Pilote Microsoft® SQL Server JDBC 8.2 |
| Red Hat® Enterprise Linux® 9 (Kernel 4.x) (64 bits) | | Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bits) |

### Version 6.5.22.0 (29 Novembre 2024)


| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
| SUSE® Linux® Enterprise Server 15 SP6 (64-bit) | |  |

### Version 6.5.21.0 (13 juin 2024)

| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
| Microsoft® Office 2021 |  |  |

### Version 6.5.19.1 (15 décembre 2023)


| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 | MongoDB Enterprise 4.4 |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |

### Version 6.5.18.0 (31 août 2023)


| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016 (64 bits) | Microsoft® Windows Server 2019 (64 bits) |
|  | Acrobat 2017 (Suivi classique) version 17.011.30078 ou ultérieure |  |

### Version 6.5.13.0 (2 juin 2022)


| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft® SharePoint 2016 |

### Version 6.5.12.0 (3 mars 2022)


| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
|  | IBM® J9 Virtual Machine (version 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | | Microsoft® SQL Server 2016 |
|  | | Microsoft® Windows Server 2016 |

### Version 6.5.10.0 (1er septembre 2022)


| Ajout de la prise en charge | Suppression de la prise en charge | Abandon de la prise en charge |
| -------------- | --------------- | ------------------- |
| SDK Oracle Java™ SE 11 (64 bits) pour le serveur d’applications JBoss® EAP 7.4. | | [Adobe Acrobat 2017 - La prise en charge principale d’Adobe Acrobat 2017 prend fin le 6 juin 2022](https://helpx.adobe.com/fr/support/programs/eol-matrix.html). |
|  | | OpenOffice 4.1.2 |

>[!NOTE]
>
> Une plateforme obsolète continue à bénéficier d’une prise en charge jusqu’à la prochaine version du programme d’installation complet ou jusqu’à ce que la prise en charge d’un fournisseur tiers pour la plateforme atteigne sa fin de vie, selon la première éventualité.

<!--
- Oct 10, 2021
 - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.
- Sep 07, 2021
 - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
   - [!DNL Adobe Acrobat 2020]
   - [!DNL Ubuntu 20.04]
   - [!DNL Open Office 4.1.10]
   - [!DNL Microsoft&reg;&reg; Office 2016]
   - [!DNL Microsoft&reg;&reg; Windows Server 2016]
   - [!DNL RHEL8]
- Dec 03, 2020
 - Support added with AEM Forms 6.5.7.0 or later for the following platform:
   - [!DNL Microsoft&reg;&reg; SQL Server 2019]
- Sep 09, 2020
   - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.
   -->