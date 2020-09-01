---
title: Programme d’installation des correctifs AEM Forms JEE
description: 'null'
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
translation-type: tm+mt
source-git-commit: c1af919d4c0fd984249e1a7009274c63b8ce9adb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 45%

---


# Programme d’installation des correctifs AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Contactez l&#39;assistance](https://www.adobe.com/fr/account/sign-in.supportportal.html) pour plus d&#39;informations ou pour obtenir le correctif.

## A propos du programme d’installation de correctif {#about-the-patch-installer}

Le programme d’installation de correctif Forms JEE 6.5 AEM comprend tous les problèmes corrigés pour tous les composants d’AEM 6.5 Forms JEE disponibles jusqu’à la sortie de ce correctif. Consultez les dernières Notes [de mise à jour du](sp-release-notes.md) Service Pack pour obtenir une liste complète des problèmes résolus.

## Conditions préalables à l&#39;installation du correctif {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installation et configuration du correctif {#installing-and-configuring-the-patch}

1. Effectuez une sauvegarde du dossier de déploiement &lt;*AEM_forms_root*>/. Il est nécessaire si vous décidez de désinstaller le Quick Fix.
1. Arrêtez le serveur d’applications.
1. Extrayez le fichier d&#39;archive du programme d&#39;installation du correctif sur votre disque dur.
1. Dans le répertoire, dont le nom dépend du système d’exploitation que vous utilisez :

   * **Windows** Accédez au répertoire approprié sur le support d’installation ou dans le dossier de votre disque dur où vous avez copié le programme d’installation, puis cliquez sur le fichier aemforms65_cfp_install.exe en appuyant sur le doublon.

      * (Windows 32-bit) `Windows\Disk1\InstData\VM`
      * (Windows 64-bit) `Windows_64Bit`\ `Disk1\InstData\VM`
   * **Linux** Accédez au répertoire approprié et, à partir d’une invite de commande, tapez 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Un assistant s’ouvre alors et vous guide tout au long de l’installation.

1. Dans le panneau Introduction, cliquez sur **[!UICONTROL Suivant]**.
1. Dans l’écran Choisir le répertoire d’installation, vérifiez que l’emplacement par défaut affiché correspond à votre installation ou cliquez sur **[!UICONTROL Parcourir]** pour sélectionner le dossier dans lequel AEM Forms est actuellement installé, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé du correctif Quick Fix, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé relatif à la pré-installation, puis cliquez sur **[!UICONTROL Installer]**. 
1. Lorsque l’installation est terminée, cliquez sur **[!UICONTROL Suivant]** pour appliquer les mises à jour du Quick Fix à vos fichiers installés.

1. Désélectionnez l’option Démarrer Configuration Manager avant de cliquer sur Terminé. Avant d’exécuter Configuration Manager à l’aide de **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, accédez au répertoire *&lt;AEMForms_Install_Dir>\configurationManager\bin* et mettez à jour **axis.jar vers axis-1.4.1.1.jar dans les fichiers suivants :******

   * ConfigurationManager.lax
   * ConfigurationManager_IPv6.lax

1. La case à cocher Début Configuration Manager est activée par défaut. Cliquez sur **[!UICONTROL Terminé]** pour exécuter Configuration Manager.

1. Pour exécuter Configuration Manager ultérieurement, désélectionnez l’option Démarrer Configuration Manager avant de cliquer sur Terminé. You can start Configuration Manager later using the appropriate script in the `[AEM_forms_root]/configurationManager/bin` directory.

1. En fonction de votre serveur d’applications, sélectionnez l’un des documents suivants et suivez les instructions de la section *Configuration et déploiement d’AEM Forms*.

   * [Installation et déploiement d’AEM Forms pour JBoss](http://www.adobe.com/go/learn_aemforms_installJBoss_65)
   * [Installation et déploiement d’AEM Forms pour WebSphere](http://www.adobe.com/go/learn_aemforms_installWebSphere_65)

1. (JBoss uniquement) Après avoir installé le correctif et configuré le serveur, supprimez les répertoires tmp et work du serveur d’applications JBoss.

## Configurations après le déploiement {#post-deployment-configurations}

### Configurations SAML {#saml-configurations}

Si l’authentification SAML est configurée et que vous rencontrez des problèmes avec les métadonnées IDP volumineuses, procédez comme suit après l’installation du correctif :

1. Définissez la propriété système suivante dans votre serveur d’applications :\
   `um.saml.enable.large.xml=true`
1. Redémarrez le serveur.
1. Supprimez les fournisseurs d’authentification SAML existants et ajoutez-les à nouveau pour les domaines existants, comme décrit dans les paramètres SAML.

## Modules affectés {#impacted-modules}

* Services de documents
* Protection des documents
* Foundation JEE

[Contacter le support technique](https://www.adobe.com/fr/account/sign-in.supportportal.html)
