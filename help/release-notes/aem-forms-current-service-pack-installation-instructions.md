---
title: Instructions d’installation du correctif AEM Forms pour AEM Forms
description: Instructions d’installation du Pack de services AEM Forms pour l’environnement OSGi et JEE
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: 2266f67d834341715b7300ff366f93d960110dac
workflow-type: ht
source-wordcount: '1734'
ht-degree: 100%

---

# Instructions d’installation pour le pack de services AEM Forms 6.5 {#aem-form-patch-installation-instructions}

## Informations sur la version

| Produit | Version |
|---|---|
| d’Adobe Experience Manager Forms 6.5 | 6.5.21.0 |
| Type | Mise à jour du pack de services |
| Date | 29 mai 2024 |
| URL de téléchargement | [Dernières versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) |

>[!NOTE]
>
>Consultez les dernières [notes de mise à jour du pack de services AEM](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr) pour obtenir une liste complète des problèmes résolus.

## Éléments inclus dans Experience Manager Forms 6.5

Le pack de services Adobe Experience Manager (AEM) Forms comprend de nouvelles fonctionnalités et des fonctionnalités mises à niveau, telles que les améliorations importantes demandées par les clientes et clients, ainsi que des performances, une stabilité et une sécurité renforcées. AEM Forms lance des packs de service à intervalles réguliers pour fournir les dernières fonctionnalités et améliorations. Selon votre pile technologique, sélectionnez l’un des chemins suivants pour télécharger et installer le Pack de services sur votre environnement :

* [Télécharger et installer le pack de services sur un environnement AEM Forms on JEE](#download-and-install-for-jee-service-pack)
* [Télécharger et installer le pack de services sur AEM Forms dans un environnement OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> * Adobe publie un programme d’installation complet tous les six Packs de services. Le pack de services 18 (6.5.12.0) d’AEM Forms 6.5 est le dernier programme d’installation complet. Le programme d’installation complet prend en charge les nouvelles plateformes, tandis que le programme d’installation du Pack de services normal inclut de nouvelles fonctionnalités, des correctifs de bug et des améliorations générales. Si vous effectuez une nouvelle installation ou si vous envisagez d’utiliser les derniers logiciels pour votre environnement AEM Forms 6.5 on JEE, Adobe recommande d’utiliser le programme d’installation complet d’AEM 6.5.18.0 Forms on JEE sorti le 31 août 2023 au lieu du programme d’installation d’AEM 6.5 Forms, sorti le 8 avril 2019 ou le programme d’installation d’AEM 6.5.12.0 sorti le 3 mars 2022. Après avoir utilisé le programme d’installation complet, installez le dernier pack de services.
> * Les fonctionnalités d’AEM Forms, telles que les formulaires adaptatifs, disponibles dans [AEM 6.5 QuickStart](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=fr), sont uniquement destinées à des fins d’exploration et d’évaluation. Pour une utilisation en production, il est essentiel d’obtenir une licence valide pour AEM Forms.

<!--

## Prerequisites {#prerequisites}

From AEM Service Pack 6.5.19.0 and onwards, XMLFM (XML output) will be available in 64-bit only, therefore you require the latest [Microsoft Visual C++ Redistributable (2015-2022) 64-bit](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) to be installed on Windows Server prior to JEE or OSGi installation.

>[!NOTE]
> This prerequisite is required in addition to the already existing Microsoft Visual C++ Redistributable 32-bit.

-->

## Télécharger et installer le pack de services sur un environnement AEM Forms on JEE {#download-and-install-for-jee-service-pack}

<!--
![JEE Installation](/help/forms/using/assets/jeeinstallation.png) -->

+++1. Effectuez une sauvegarde de votre environnement existant.

1. Sauvegardez votre [référentiel CRX, votre schéma de base de données et votre GDS (stockage global de documents)](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=fr).
1. Sauvegardez le dossier &lt;*AEM_forms_root*>/deploy.

>[!NOTE]
>
> Avant d’exécuter le programme d’installation du Pack de services d’AEM, assurez-vous de disposer des droits d’accès en écriture sur le répertoire d’installation AEM.

+++

+++2. Téléchargez le logiciel requis.

* [Service Pack AEM Forms on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)

* [Servlet de fragment](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr)
* [Package de modules complémentaires Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)


+++

+++3. Installez les packages redistribuables Microsoft Visual C++.

* Téléchargez et installez la [version 64 bits des packages Microsoft Visual C++ redistribuables pour Visual Studio 2015, 2017, 2019 et 2022](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sur l’ordinateur sur lequel AEM 6.5 Forms est installé.

>[!NOTE]
>
> Assurez-vous d’installer la version redistribuable, même si une version précédente est installée, afin de garantir la disponibilité de la dernière version.

+++

+++4. Installez le pack de services AEM Forms on JEE :

1. Arrêtez le serveur d’applications.
1. Extrayez l’**archive du programme d’installation du Service Pack AEM Forms on JEE** sur votre disque dur :

   * **Windows**
Accédez au répertoire approprié sur le support ou dossier d’installation de votre disque dur dans lequel le programme d’installation a été copié, puis double-cliquez sur le fichier `aemforms65_cfp_install.exe`.

      * (Windows 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux®**
Accédez au répertoire approprié puis, à partir du shell, saisissez `./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Vous lancez ainsi un assistant d’installation qui vous guide tout au long de l’installation.

1. Dans l’écran d’introduction, cliquez sur **[!UICONTROL Suivant]**.
1. Dans l’écran **Choisir le dossier d’installation**, vérifiez que l’emplacement par défaut affiché correspond à votre installation ou cliquez sur **[!UICONTROL Parcourir]** pour sélectionner le dossier dans lequel AEM Forms est actuellement installé, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez les informations récapitulatives du pack de services, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé relatif à la pré-installation, puis cliquez sur **[!UICONTROL Installer]**.
1. Lorsque l’installation est terminée, cliquez sur **[!UICONTROL Suivant]** pour appliquer les mises à jour du Quick Fix à vos fichiers installés.
1. **[Pour Windows uniquement] :** Effectuez l’une des étapes suivantes :

   * Désélectionnez l’option **Démarrer le Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Exécutez **Configuration Manager** en utilisant le fichier **ConfigurationManager.bat** situé dans `[aem-forms root]\configurationManager\bin`.

   * Vous pouvez aussi désélectionner l’option **Démarrer Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Avant d’exécuter **Configuration Manager** à l’aide de **ConfigurationManager.exe** ou de **ConfigurationManager_IPv6.exe**, accédez au répertoire *`<AEMForms_Install_Dir>\configurationManager\bin`* et remplacez **ConfigurationManager.lax** et **ConfigurationManager_IPV6.lax** par la dernière version des fichiers [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) et [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax), recherchez et remplacez **axis-1.4.1.1.jar** par **axis-1.4.1.2.jar** dans ces deux fichiers.

     >[!NOTE]
     >
     >* La mise à jour ou le remplacement du fichier **ConfigurationManager.bat** vous permet d’éviter de mettre à jour manuellement le nom des fichiers .lax.

1. **[Pour les systèmes Unix uniquement] :** la case **Démarrer Configuration Manager** est cochée par défaut. Cliquez sur **[!UICONTROL Terminé]** pour exécuter Configuration Manager instantanément ou pour exécuter **Configuration Manager** plus tard, désélectionnez l’option **Démarrer Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Vous pourrez démarrer **Configuration Manager** ultérieurement à l’aide du script approprié dans le répertoire `[AEM_forms_root]/configurationManager/bin`.

1. En fonction de votre serveur d’applications, sélectionnez l’un des documents suivants et suivez les instructions de la section *Configuration et déploiement d’AEM Forms*.

   * [Installation et déploiement d’AEM Forms pour JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_fr)
   * [Installation et déploiement d’AEM Forms pour WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_fr)
   * [Installation et déploiement d’AEM Forms pour WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_fr)
   * [Installation et déploiement d’AEM Forms pour le cluster JBoss®](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Installation et déploiement d’AEM Forms pour le cluster WebSphere®](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Installation et déploiement d’AEM Forms pour le cluster WebLogic](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
>* Après avoir installé le pack de services AEM Forms on JEE, vous devez supprimer le module complémentaire Forms du dossier `crx-repository\install` avant de redémarrer le serveur d’applications. Téléchargez le dernier pack de module complémentaire de Forms à partir du [Portail de distribution logicielle](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
>* Il est recommandé d’utiliser la commande « Ctrl + C » pour redémarrer le SDK. Le redémarrage du SDK AEM à l’aide de méthodes alternatives, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

+++

+++5. Installer le fragment de servlet (Pack de services AEM 6.5.14.0 ou version antérieure) (**Installation obligatoire**)

>[!NOTE]
>
> * Si vous effectuez une mise à niveau à partir du **Pack de services AEM 6.5.15.0**, l’installation du **fragment de servlet** n’est pas obligatoire. Pour les versions du **Pack de services AEM 6.5.14.0** ou antérieures, il est **obligatoire d’installer** le fragment de servlet.


Pour télécharger et installer le fragment de servlet :

1. Si vous n’avez pas téléchargé le fragment, téléchargez-le à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

2. Démarrez le serveur d’applications, attendez que les journaux se stabilisent et vérifiez l’état du lot.

3. Ouvrez les lots de la console web. L’URL par défaut est `http://[Server]:[Port]/system/console/bundles`.

4. Cliquez sur Installer/Mettre à jour. Sélectionnez le fragment téléchargé, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Cliquez sur **Install** (Installer) ou **Update** (Mettre à jour). Attendez que le serveur d’applications se stabilise.

5. Arrêtez le serveur d’applications.

+++

+++6. Installez AEM Service Pack 

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.
1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].
1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).
1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement le Service Pack [!DNL ExperienceManager].<!--       UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne.
Le package est automatiquement installé.

* Utilisez l’[API HTTP à partir du gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

  >[!NOTE]
  >
  >Le Service Pack Experience Manager ne prend pas en charge l’installation en Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validation de l’installation**

  Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

   1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (spversion)` sous [!UICONTROL Produits installés].<!-- UPDATE FOR EACH NEW RELEASE -->
   1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).
   1. Le bundle OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.14 ou ultérieure (utilisez la console web : `/system/console/bundles`).

+++

+++7. Installer le package du module complémentaire Adobe Experience Manager Forms d’AEM

1. Vérifiez que vous avez installé le pack de services [!DNL Experience Manager].
1. Téléchargez le package complémentaire Forms correspondant répertorié dans les [versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour votre système d’exploitation.
1. Installez le package complémentaire Forms comme décrit dans [Installation des packages complémentaires AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
1. Si vous utilisez des lettres dans Experience Manager 6.5 Forms, installez le [dernier package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

+++

## Télécharger et installer le pack de service sur un environnement AEM Forms on OSGi {#download-and-install-for-osgi-service-pack}


<!-- ![OSGi Installation Steps](/help/forms/using/assets/osgiinstallation.png)
-->

+++1. Effectuez une sauvegarde de votre environnement existant.

1. Sauvegardez vos [référentiel CRX et schéma de base de données](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html?lang=fr).

>[!NOTE]
>
> Si vous installez le pack de services AEM Forms pour la base de données relationnelle, il est obligatoire de sauvegarder DB_schema.

+++

+++2. Téléchargez le logiciel requis.

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr)
* [Package de modules complémentaires Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)

+++

+++ 3. Installez les packages redistribuables Microsoft Visual C++.

* Téléchargez et installez la [version 64 bits des packages Microsoft Visual C++ redistribuables pour Visual Studio 2015, 2017, 2019 et 2022](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022) sur l’ordinateur sur lequel AEM 6.5 Forms est installé.

>[!NOTE]
>
>
> Assurez-vous d’installer la version redistribuable, même si une version précédente est installée, afin de garantir la disponibilité de la dernière version.

+++

+++4. Installez AEM Service Pack 

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.
1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].
1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).
1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement le Service Pack [!DNL Experience Manager].<!--  UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de modules](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

  >[!NOTE]
  >
  >Le Service Pack Experience Manager ne prend pas en charge l’installation Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

  **Validation de l’installation**

  Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

   1. La page d’informations sur les produits (`/system/console/productinfo`) affiche le numéro de version mis à jour `Adobe Experience Manager (spversion)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->.

   1. Tous les bundles OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

      1. Le bundle OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.14 ou ultérieure (utiliser la console Web : `/system/console/bundles`).

+++

+++5. Installez le package complémentaire Adobe Experience Manager Forms (AEM).

1. Vérifiez que vous avez installé le pack de services [!DNL Experience Manager].
1. Téléchargez le package complémentaire Forms correspondant répertorié dans les [versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour votre système d’exploitation.
1. Installez le package complémentaire Forms comme décrit dans [Installation des packages complémentaires AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
1. Si vous utilisez des lettres dans Experience Manager 6.5 Forms, installez le [dernier package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

+++

## Résolution des problèmes

* Si la **boîte de dialogue sur l‘IU du gestionnaire de modules** se ferme pendant l’installation du pack de services, attendez que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez l’affichage des journaux spécifiques liés à la désinstallation du bundle de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans le navigateur Safari mais peut se produire par intermittence sur n’importe quel navigateur.

* Vérifiez toute activité dans les journaux du moniteur (error.log) une fois l’installation terminée quelle que soit l’activité. Patientez quelques minutes jusqu’à ce qu’il n’y ait plus aucune activité dans les journaux. Redémarrez l’instance AEM.

* Au cas où vous obtiendriez une **erreur service-unavailable** après l’installation du Pack de services AEM Forms 6.5.15.0 ou ultérieur, [installez le fragment de servlet et l’offre groupée](/help/forms/using/aem-service-pack-installation-solution.md) pour corriger l’erreur.
