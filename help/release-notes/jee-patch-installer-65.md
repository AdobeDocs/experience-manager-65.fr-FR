---
title: Programme d’installation des correctifs d’AEM Forms JEE
description: Programme d’installation des correctifs d’AEM Forms JEE
uuid: 76662858-afca-4ba3-883b-9b9a61874f15
content-type: reference
discoiquuid: b0283feb-c3ec-4ef0-885c-46bc83a61e26
exl-id: 6b17472b-9226-4319-b305-4dba862d21af
source-git-commit: e54d8633aa3b8c1554df90d1b9650713246b95e8
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 51%

---

# Programme d’installation des correctifs d’AEM Forms JEE {#aem-forms-jee-patch-installer}

>[!NOTE]
>
>[Pour plus d’informations ou pour obtenir le correctif, contactez le ](https://www.adobe.com/account/sign-in.supportportal.html) support technique.

## A propos du programme d&#39;installation de correctif {#about-the-patch-installer}

Le programme d’installation du correctif Forms JEE d’AEM 6.5 comprend tous les problèmes résolus pour tous les composants d’AEM 6.5 Forms JEE disponibles jusqu’à la publication de ce correctif. Consultez les dernières [Notes de mise à jour du Service Pack](sp-release-notes.md) pour obtenir la liste complète des problèmes résolus.

## Prérequis pour installer le correctif {#prerequisites-to-installing-the-patch}

* AEM 6.5 Forms

## Installer et configurer le correctif {#installing-and-configuring-the-patch}

1. Effectuez une sauvegarde du dossier de déploiement &lt;*AEM_forms_root*>/. Il est nécessaire si vous décidez de désinstaller le Quick Fix.
1. Arrêtez le serveur d’applications.
1. Extrayez le fichier d’archive du programme d’installation de correctif sur votre disque dur.
1. Dans le répertoire, dont le nom dépend du système d’exploitation que vous utilisez :

   * **Windows**
Accédez au répertoire approprié sur le support d’installation ou dans le dossier de votre disque dur dans lequel vous avez copié le programme d’installation, puis double-cliquez sur le fichier aemforms65_cfp_install.exe .

      * (Windows 32 bits) `Windows\Disk1\InstData\VM`
      * (Windows 64 bits) `Windows_64Bit`\ `Disk1\InstData\VM`
   * ****
LinuxAccédez au répertoire approprié, puis, à l’invite de commande, saisissez 
`./aem65_cfp_install.bin`.

      * (Linux) `Linux/Disk1/InstData/NoVM`

   Un assistant s’ouvre alors et vous guide tout au long de l’installation.

1. Dans le panneau Introduction, cliquez sur **[!UICONTROL Suivant]**.
1. Dans l’écran Choisir le répertoire d’installation, vérifiez que l’emplacement par défaut affiché correspond à votre installation ou cliquez sur **[!UICONTROL Parcourir]** pour sélectionner le dossier dans lequel AEM Forms est actuellement installé, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé du correctif Quick Fix, puis cliquez sur **[!UICONTROL Suivant]**.
1. Lisez le résumé relatif à la pré-installation, puis cliquez sur **[!UICONTROL Installer]**.
1. Lorsque l’installation est terminée, cliquez sur **[!UICONTROL Suivant]** pour appliquer les mises à jour du Quick Fix à vos fichiers installés.

1. Désélectionnez l’option Démarrer Configuration Manager avant de cliquer sur Terminé. Avant d’exécuter Configuration Manager à l’aide de **ConfigurationManager.exe** ou **ConfigurationManager_IPv6.exe**, accédez au répertoire *&lt;AEMForms_Install_Dir>\configurationManager\bin* et mettez à jour les fichiers `ConfigurationManager.lax` et `ConfigurationManager_IPv6.lax` avec les opérations de changement de nom suivantes :

   * `axis.jar` vers `axis-1.4.1.1.jar`
   * `serializer-2.7.1.jar` vers `serializer-2.7.2.jar`
   * `xalan-2.7.1.jar` vers `xalan-2.7.2.jar`
   * `xercesImpl-2.9.1.jar` vers `xercesImpl-2.12.0.jar`
   * `xml-apis-2.7.1.jar` vers `xml-apis-2.7.2.jar`

1. La case à cocher Démarrer Configuration Manager est sélectionnée par défaut. Cliquez sur **[!UICONTROL Terminé]** pour exécuter Configuration Manager.

1. Pour exécuter Configuration Manager ultérieurement, désélectionnez l’option Démarrer Configuration Manager avant de cliquer sur Terminé. Vous pouvez lancer Configuration Manager ultérieurement à l’aide du script approprié dans le répertoire `[AEM_forms_root]/configurationManager/bin`.

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

## Modules touchés {#impacted-modules}

* Services de document
* Document Security
* Foundation JEE

[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)
