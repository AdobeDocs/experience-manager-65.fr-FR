---
title: Programme d’installation du correctif JEE AEM Forms
description: Programme d’installation du correctif JEE AEM Forms pour résoudre les problèmes liés aux composants Forms d’AEM 6.5.
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 98%

---

# Programme d’installation du correctif JEE AEM Forms {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contactez l’assistance technique](https://www.adobe.com/account/sign-in.supportportal.html) pour plus d’informations ou pour obtenir le correctif.

## À propos du programme d’installation du correctif {#about-the-patch-installer}

Le programme d’installation du correctif JEE AEM 6.5 Forms comprend tous les problèmes résolus pour tous les composants JEE d’AEM 6.5 Forms disponibles jusqu’à la publication de ce correctif. Consultez les dernières [Notes de mise à jour du pack de services](release-notes.md) pour obtenir une liste complète des problèmes résolus.

## Prérequis pour installer le correctif {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installation et configuration du correctif {#installing-and-configuring-the-patch}

1. Effectuez une sauvegarde du dossier de déploiement &lt;*AEM_forms_root*>/. Cela est nécessaire si vous décidez de désinstaller le Quick Fix.
1. Arrêtez le serveur d’applications.
1. Extrayez le fichier d’archive du programme d’installation de correctif sur votre disque dur.
1. Dans le répertoire, dont le nom dépend du système d’exploitation que vous utilisez :

   * **Windows**


Accédez au répertoire approprié sur le support d’installation ou dans le dossier de votre disque dur dans lequel le programme d’installation a été copié, puis cliquez deux fois sur le fichier aemforms65_cfp_install.exe.

      * (Windows 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`

   * **Linux**
Accédez au répertoire approprié puis, dans l’invite de commande, saisissez `./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Vous lancez ainsi un assistant d’installation qui vous guide tout au long de l’installation.

1. Dans l’écran d’introduction, cliquez sur **[!UICONTROL Suivant]**.
1. Dans l’écran **Choisir le dossier d’installation**, vérifiez que l’emplacement par défaut affiché correspond à votre installation ou cliquez sur **[!UICONTROL Parcourir]** pour sélectionner le dossier dans lequel AEM Forms est actuellement installé, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé du correctif Quick Fix, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé relatif à la pré-installation, puis cliquez sur **[!UICONTROL Installer]**.
1. Lorsque l’installation est terminée, cliquez sur **[!UICONTROL Suivant]** pour appliquer les mises à jour du Quick Fix à vos fichiers installés.

1. **[Pour Windows uniquement] :** Effectuez l’une des étapes suivantes :
   * Désélectionnez l’option **Démarrer le gestionnaire de configuration** avant de cliquer sur **[!UICONTROL Terminé]**. Exécutez **Configuration Manager** en utilisant le fichier **ConfigurationManager.bat** situé dans `[aem-forms root]\configurationManager\bin`.

   * Vous pouvez aussi désélectionner l’option **Démarrer Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Avant d’exécuter **Configuration Manager** en utilisant **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, accédez au répertoire *`<AEMForms_Install_Dir>\configurationManager\bin`* et remplacez les fichiers [ConfigurationManager.lax](/help/assets/ConfigurationManager.lax) et [ConfigurationManager_IPV6.lax](/help/assets/ConfigurationManager_IPv6.lax).

   >>
   [!NOTE]
   >>
   L’utilisation du fichier **ConfigurationManager.bat** vous permet d’éviter de mettre à jour manuellement le nom des fichiers .lax.
   >

1. **[Pour les systèmes Unix uniquement] :**

   * La case à cocher **Démarrer Configuration Manager** est sélectionnée par défaut. Cliquez sur **[!UICONTROL Terminé]** pour exécuter Configuration Manager instantanément ou pour exécuter **Configuration Manager** plus tard, désélectionnez l’option **Démarrer Configuration Manager** avant de cliquer sur **[!UICONTROL Terminé]**. Vous pourrez démarrer **Configuration Manager** ultérieurement à l’aide du script approprié dans le répertoire `[AEM_forms_root]/configurationManager/bin`.

1. En fonction de votre serveur d’applications, sélectionnez l’un des documents suivants et suivez les instructions de la section *Configuration et déploiement d’AEM Forms*.

   * [Installation et déploiement d’AEM Forms pour JBoss](https://www.adobe.com/go/learn_aemforms_installJBoss_65_fr)
   * [Installation et déploiement d’AEM Forms pour WebSphere](https://www.adobe.com/go/learn_aemforms_installWebSphere_65_fr)

1. (JBoss uniquement) Après avoir installé le correctif et configuré le serveur, supprimez les répertoires tmp et work du serveur d’applications JBoss.

## Configurations après le déploiement {#post-deployment-configurations}

### Configurations SAML {#saml-configurations}

Si l’authentification SAML est configurée et que vous rencontrez des problèmes avec des métadonnées IDP volumineuses, procédez comme suit après l’installation du correctif :

1. Définissez la propriété système suivante dans votre serveur d’applications :\
   `um.saml.enable.large.xml=true`
1. Redémarrez le serveur.
1. Supprimez les fournisseurs d’authentification SAML existants et ajoutez-les à nouveau pour les domaines existants, comme décrit dans les paramètres SAML.

## Modules touchés {#impacted-modules}

* Document Services
* Document Security
* Foundation JEE

[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)
