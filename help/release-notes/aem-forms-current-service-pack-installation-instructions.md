---
title: Instructions d’installation du correctif AEM Forms pour AEM Forms
description: Instructions d’installation du Service Pack AEM Forms pour l’environnement OSGi et JEE
exl-id: ae4c7e9d-9af8-4288-a6f9-e3bcbe7d153d
source-git-commit: b15581701aaff72db2fc0030b0062d2f12150d8f
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 50%

---

# Instructions d’installation d’AEM 6.5 Service Pack Forms {#aem-form-patch-installation-instructions}

## Informations sur la version

| Produit |  de Forms Adobe Experience Manager 6.5 |
|---|---|
| Version | 6.5.16.0 |
| Type | Mise à jour du pack de services |
| Date | 2 mars 2023 |
| URL de téléchargement | [Dernières versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) |

>[!NOTE]
>
>Consultez la dernière version [Notes de mise à jour d’AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr) pour obtenir une liste complète des problèmes résolus.

## Éléments inclus dans Experience Manager Forms 6.5

Le Service Pack d’Adobe Experience Manager (AEM) Forms comprend de nouvelles fonctionnalités et des fonctionnalités mises à niveau, telles que les améliorations importantes demandées par les clients, les performances, la stabilité et les améliorations de sécurité. Service Packs de mise à jour d’AEM Forms à intervalles réguliers, afin de fournir les dernières fonctionnalités et améliorations. Selon votre pile, sélectionnez l’un des chemins suivants pour télécharger et installer le Service Pack sur votre environnement :

* [Télécharger et installer le Service Pack dans un environnement AEM Form on JEE](#download-and-install-for-jee-service-pack)
* [Télécharger et installer le Service Pack dans un environnement AEM de formulaire sur OSGi](#download-and-install-for-osgi-service-pack)

>[!NOTE]
>
> Adobe publie un programme d’installation complet tous les 6e Service Pack. AEM 6.5 Forms Service Pack 12 (6.5.12.0) sur JEE était le dernier programme d’installation complet. Le programme d’installation complet prend en charge les nouvelles plateformes, tandis que le programme d’installation du Service Pack normal inclut de nouvelles fonctionnalités, des correctifs de bogues et des améliorations générales. Si vous effectuez une nouvelle installation ou envisagez d’utiliser les derniers logiciels pour votre environnement AEM Forms 6.5 on JEE, Adobe recommande d’utiliser le programme d’installation complet d’AEM 6.5.12.0 Forms on JEE sorti le 3 mars 2022 au lieu du programme d’installation d’AEM 6.5 Forms, sorti le 8 avril 2019. Après avoir utilisé le programme d’installation complet, installez le dernier Service Pack.

## Télécharger et installer le Service Pack dans un environnement AEM Form on JEE {#download-and-install-for-jee-service-pack}

![Installation de JEE](/help/forms/using/assets/jeeinstallation.png)

+++1. Effectuez une sauvegarde de votre environnement existant :

1. Sauvegardez vos [Référentiel CRX, schéma de base de données et répertoire de stockage global de documents](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).
1. Sauvegardez le &lt;*AEM_forms_root* dossier >/deploy.

>[!NOTE]
>
> Avant d’exécuter le programme d’installation d’AEM Service Pack, assurez-vous de disposer des droits d’accès en écriture sur AEM répertoire d’installation.

+++

+++2.Téléchargez le logiciel requis :

* [Service Pack d’AEM Forms on JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)
* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr)
* [Package de modules complémentaires Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)
* [Servlet de fragment](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffeaturepack%2Forg.apache.felix.http.servlet-api-1.2.0_fragment_full.jar)

+++

+++3. Installez le Service Pack d’AEM Forms on JEE :

1. Arrêtez le serveur d’applications.
1. Extrayez le **Archivage du programme d’installation d’AEM Forms on JEE Service Pack** sur votre disque dur :

   * **Windows**
Accédez au répertoire approprié sur le support d’installation ou dans le dossier de votre disque dur dans lequel vous avez copié le programme d’installation, puis double-cliquez sur le 
`aemforms65_cfp_install.exe` approuvé.

      * (Windows 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux®**
Accédez au répertoire approprié, puis à partir d’un shell et saisissez 
`./aem65_cfp_install.bin`.

      * (Linux®) `Linux/Disk1/InstData/NoVM`

   Un assistant s’ouvre alors et vous guide tout au long de l’installation.

1. Dans le panneau Introduction, cliquez sur **[!UICONTROL Suivant]**.
1. Dans l’écran **Choisir le dossier d’installation**, vérifiez que l’emplacement par défaut affiché correspond à votre installation ou cliquez sur **[!UICONTROL Parcourir]** pour sélectionner le dossier dans lequel AEM Forms est actuellement installé, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez les informations récapitulatives du Service Pack, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé relatif à la pré-installation, puis cliquez sur **[!UICONTROL Installer]**.
1. Lorsque l’installation est terminée, cliquez sur **[!UICONTROL Suivant]** pour appliquer les mises à jour du Quick Fix à vos fichiers installés.
1. **[Pour Windows uniquement] :** Effectuez l’une des étapes suivantes :

   * Désélectionnez l’option **Démarrer le gestionnaire de configuration** avant de cliquer sur **[!UICONTROL Terminé]**. Exécutez **Configuration Manager** en utilisant le fichier **ConfigurationManager.bat** situé dans `[aem-forms root]\configurationManager\bin`.

   * Vous pouvez aussi désélectionner l’option **Démarrer Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Avant d’exécuter **Configuration Manager** en utilisant **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, accédez au répertoire *`<AEMForms_Install_Dir>\configurationManager\bin`* et remplacez les fichiers [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) et [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax).

      >[!NOTE]
      >
      >* Mise à jour ou remplacement du **ConfigurationManager.bat** vous aide à éviter de mettre à jour les fichiers .lax manuellement.


1. **[Pour Unix uniquement]:** Le **Démarrez Configuration Manager** est sélectionnée par défaut. Cliquez sur **[!UICONTROL Terminé]** pour exécuter Configuration Manager instantanément ou pour exécuter **Configuration Manager** plus tard, désélectionnez l’option **Démarrer Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Vous pourrez démarrer **Configuration Manager** ultérieurement à l’aide du script approprié dans le répertoire `[AEM_forms_root]/configurationManager/bin`.

1. En fonction de votre serveur d’applications, sélectionnez l’un des documents suivants et suivez les instructions de la section *Configuration et déploiement d’AEM Forms*.

   * [Installation et déploiement d’AEM Forms pour JBoss®](https://www.adobe.com/go/learn_aemforms_installJBoss_65_fr)
   * [Installation et déploiement d’AEM Forms pour WebSphere®](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_fr)
   * [Installation et déploiement d’AEM Forms pour WebLogic](https://www.adobe.com/go/learn_aemforms_installWebLogic_65_fr)
   * [Installation et déploiement d’AEM forms pour la grappe JBoss®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-jboss.pdf)
   * [Installation et déploiement d’AEM forms pour la grappe WebSphere®](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-websphere.pdf)
   * [Installation et déploiement d’AEM Forms pour la grappe WebLogic](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/install-cluster-weblogic.pdf)


>[!NOTE]
>
> Après avoir installé le Service Pack d’AEM Forms on JEE, vous devez supprimer le module complémentaire Forms de `crx-repository\install` avant de redémarrer le serveur d’applications. Téléchargez le dernier module complémentaire Forms à partir du [Portail de distribution de logiciels](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

+++

+++4. Installation du fragment de servlet

>[!NOTE]
>
> * Si vous effectuez une mise à niveau à partir de **AEM Service Pack 6.5.15.0**, il n’est pas nécessaire d’installer le **fragment de servlet**. Si vous effectuez une mise à niveau à partir d’une version antérieure à **AEM Service Pack 6.5.15.0**, il est obligatoire d’installer la variable **fragment de servlet**.
> * Il est obligatoire d’installer la variable **fragment de servlet** pour tous les serveurs d’applications, à l’exception de ceux qui s’exécutent sur **JBoss® EAP 7.4.0**.



Pour télécharger et installer le fragment de servlet :

1. Si vous n’avez pas téléchargé le fragment, téléchargez-le à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar).

1. Démarrez le serveur d’applications, attendez que les journaux se stabilisent et vérifiez l’état du lot.

1. Ouvrez les lots de la console web. L’URL par défaut est `http://[Server]:[Port]/system/console/bundles`.

1. Cliquez sur Installer/Mettre à jour. Sélectionnez le fragment téléchargé, `org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar`. Cliquez sur **Install** (Installer) ou **Update** (Mettre à jour). Attendez que le serveur applicatif se stabilise

1. Arrêtez le serveur d’applications.

+++

+++5. Installez AEM  Service Pack 

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.
1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].
1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).
1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL ExperienceManager] Service pack.<!--       UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne.
Le package est automatiquement installé.

* Utilisez l’[API HTTP à partir du gestionnaire de packages](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

   >[!NOTE]
   >
   >Le Service Pack du Experience Manager ne prend pas en charge l’installation du Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (spversion)` sous [!UICONTROL Produits installés].<!-- UPDATE FOR EACH NEW RELEASE -->
1. Tous les lots OSGi sont : **[!UICONTROL PRINCIPAL]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (Utiliser la console web : `/system/console/bundles`).
1. Le lot OSGi `org.apache.jackrabbit.oak-core` est version 1.22.14 ou ultérieure (Utiliser WebConsole) : `/system/console/     bundles`).

+++

+++6. Installation du module complémentaire Experience Manager Forms AEM

1. Assurez-vous que vous avez installé le [!DNL Experience Manager] Service pack.
1. Téléchargez le package complémentaire Forms correspondant répertorié dans les [versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour votre système d’exploitation.
1. Installez le package complémentaire Forms comme décrit dans [Installation des packages complémentaires AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
1. Si vous utilisez des lettres dans Experience Manager 6.5 Forms, installez le [dernier package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

+++

## Télécharger et installer le Service Pack dans un environnement AEM de formulaire sur OSGi {#download-and-install-for-osgi-service-pack}

![Étapes d’installation OSGi](/help/forms/using/assets/osgiinstallation.png)


+++1. Effectuez une sauvegarde de votre environnement existant :

1. Sauvegardez vos [Référentiel CRX et schéma de base de données](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/aem-forms-backup-recovery/backing-aem-forms-data.html).

>[!NOTE]
>
> Si vous installez le Service Pack AEM Forms pour la base de données relationnelle, il est obligatoire de sauvegarder DB_schema.

+++

+++2.Téléchargez le logiciel requis :

* [AEM Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr)
* [Package de modules complémentaires Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr)

+++

+++3. Installez AEM  Service Pack 

1. Redémarrez l’instance avant l’installation si l’instance est en mode de mise à jour (lorsque l’instance a été mise à jour à partir d’une version antérieure). Adobe recommande un redémarrage si le temps de disponibilité actuel d’une instance est élevé.
1. Avant l’installation, prenez un instantané ou exécutez une sauvegarde récente de votre instance [!DNL Experience Manager].
1. Téléchargez le pack de services à partir de la [Distribution logicielle](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). <!-- UPDATE FOR EACH NEW RELEASE -->
1. Ouvrez le gestionnaire de modules et cliquez sur **[!UICONTROL Charger le module]** pour charger le module. Pour en savoir plus, consultez la section [Gestionnaire de modules](/help/sites-administering/package-manager.md).
1. Sélectionnez le module, puis sélectionnez **[!UICONTROL Installer]**.

**Installation automatique**

Vous pouvez utiliser deux méthodes différentes pour installer automatiquement [!DNL Experience Manager] Service pack.<!--  UPDATE FOR EACH NEW RELEASE -->

* Placez le package dans le dossier `../crx-quickstart/install` lorsque le serveur est disponible en ligne. Le package est automatiquement installé.
* Utilisez l’[API HTTP à partir du gestionnaire de packages](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=fr). Utilisez `cmd=install&recursive=true` afin que les packages imbriqués soient installés.

   >[!NOTE]
   >
   >Le Service Pack du Experience Manager ne prend pas en charge l’installation du Bootstrap. <!-- UPDATE FOR EACH NEW RELEASE -->

**Validation de l’installation**

Pour connaître les plateformes certifiées pour travailler avec cette version, reportez-vous à la section des [exigences techniques](/help/sites-deploying/technical-requirements.md).

1. La page d’informations sur les produits (`/system/console/productinfo`) affiche la chaîne de version mise à jour `Adobe Experience Manager (spversion)` sous [!UICONTROL Produits installés]. <!-- UPDATE FOR EACH NEW RELEASE -->

1. Tous les lots OSGi sont au statut **[!UICONTROL ACTIF]** ou **[!UICONTROL FRAGMENT]** dans la console OSGi (utilisez la console web : `/system/console/bundles`).

   1. Le lot OSGi `org.apache.jackrabbit.oak-core` est de la version 1.22.14 ou ultérieure (utiliser la console Web : `/system/console/bundles`). 

+++

+++4. Installation du module complémentaire Experience Manager Forms AEM

1. Assurez-vous que vous avez installé le [!DNL Experience Manager] Service pack.
1. Téléchargez le package complémentaire Forms correspondant répertorié dans les [versions d’AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) pour votre système d’exploitation.
1. Installez le package complémentaire Forms comme décrit dans [Installation des packages complémentaires AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
1. Si vous utilisez des lettres dans Experience Manager 6.5 Forms, installez le [dernier package de compatibilité AEMFD](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).

+++

## Résolution des problèmes

* If **Boîte de dialogue sur l’interface utilisateur du gestionnaire de modules** quitte le service pack pendant l’installation, attendez que les journaux d’erreurs se stabilisent avant d’accéder au déploiement. Attendez les logs spécifiques liés à la désinstallation du lot de mise à jour avant de vous assurer que les installations sont réussies. En règle générale, ce problème se produit dans le navigateur Safari, mais peut se produire par intermittence dans n’importe quel navigateur.

* Vérifiez les logs du moniteur (error.log) une fois l’installation terminée pour toute activité. Patientez quelques minutes jusqu’à ce qu’il n’y ait aucune activité dans les journaux. Redémarrez l’instance AEM.

* Au cas où vous obtiendriez une **erreur service-unavailable** après l’installation du Service Pack AEM Forms 6.5.15.0, [installation du fragment de servlet et du lot](/help/forms/using/aem-service-pack-installation-solution.md) pour corriger l’erreur.
