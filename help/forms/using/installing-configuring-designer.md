---
title: Installation et configuration de Designer
description: Designer est disponible sous la forme d’un programme autonome et est également fourni avec Workbench. Découvrez comment installer Designer autonome.
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin, User, Developer
feature: Forms Designer,Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 89f807e1d31c5588d86e50160b0149e00422b78c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 100%

---

# Installation et configuration de Designer{#installing-and-configuring-designer}

## Prérequis {#pre-requisites}

+++ Pour AEM Forms Designer 64 bits (recommandé)

* Installation de la version 64 bits de [Redistribuable Visual C++ 2019 (x64)](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation.
* Un utilisateur ou une utilisatrice disposant des droits d’administration pour installer ou désinstaller AEM Forms Designer.

+++

+++ Pour AEM Forms Designer 32 bits

* Installation de la version 32 bits de [Redistribuable Visual C++ 2019 (x64)](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation.
* Un utilisateur ou une utilisatrice disposant des droits d’administration pour installer ou désinstaller AEM Forms Designer.

+++

>[!NOTE]
>
>* La version 64 bits de Designer a été introduite avec le pack de services AEM 6.5 Forms 19 (6.5.19.0).
>* La version 32 bits de Designer est obsolète depuis la publication du [pack de services 21 d’AEM Forms (6.5.21.0)](https://experienceleague.adobe.com/fr/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases).
> * Les plateformes prises en charge pour Forms Designer s’alignent sur les plateformes prises en charge par AEM Forms. Pour en savoir plus sur les plateformes prises en charge pour Forms Designer, [cliquez ici](/help/forms/using/aem-forms-jee-supported-platforms.md).

Pour plus d’informations sur l’installation de Forms Designer, voir [Questions fréquentes](#fandq).

## Installer AEM Forms Designer {#install-designer}

Designer est disponible sous la forme d’un programme autonome et est également fourni avec Workbench. Si vous utilisez un programme d’installation autonome pour AEM Forms Designer, procédez comme suit :

1. Désinstallez la version précédente d’AEM Forms Designer, si elle est déjà installée.
1. Téléchargez AEM Forms Designer 64 bits (recommandé) ou AEM Forms Designer 32 bits en fonction de vos besoins.

   >[!NOTE]
   > 
   >* Forms Designer 32 bits devrait devenir obsolète avec la version 6.5 d’AEM Forms Service Packs 20 (6.5.20.0). Adobe recommande de passer à la version 64 bits de Forms Designer.
   >* Forms Designer 64 bits est disponible uniquement pour AEM Forms 6.5 Service Packs 19 (6.5.19.0) ou versions ultérieures.
   >* À compter de la version d’Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0), la version Forms Designer inclut également la version du Service Pack. Par exemple, pour le Service Pack 15, le numéro de version est 6.5.15.20221112.1.0. Dans cet exemple, 6.5.15 est la version du Service Pack.

1. Lancez le programme d’installation d’AEM Forms Designer en cliquant deux fois sur setup.exe.
1. Continuez et fournissez vos détails ainsi que le numéro de série sur l’écran Personnalisation.

   >[!NOTE]
   >
   >* Obtenez votre clé de licence Forms Designer sur [Adobe Licensing Website](https://licensing.adobe.com/).

1. Si vous acceptez les termes du contrat de licence, appuyez sur Suivant pour continuer.
1. (Facultatif) Modifiez le chemin d’installation par défaut, si vous voulez installer Designer à l’emplacement de votre choix. Cliquez sur Suivant.
1. Cliquez sur Précédent pour modifier les préférences. Pour installer Designer, cliquez sur Installer.
1. Cliquez sur Terminer à la fin de l’installation.

Vous pouvez également installer AEM Forms Designer via la ligne de commande en mode passif ou silencieux.

* Installation en ligne de commande passive : le programme d’installation affiche une barre de progression qui indique que l’installation est en cours mais aucun message d’erreur ou d’invite ne s’affiche. Une fois l’installation lancée, vous ne pouvez pas l’annuler.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Installation en ligne de commande silencieuse : le programme d’installation exécute l’installation sans afficher d’interface utilisateur. Aucun message, invite ou boîte de dialogue ne s’affiche. Une fois l’installation lancée, vous ne pouvez pas l’annuler.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```

## Mettre à jour AEM Forms Designer {#update-forms-designer}

Il existe deux cas lors de la mise à jour de la dernière version d’AEM Forms Designer 6.5.16.0 :

* **Cas 1** : lorsque l’utilisateur ou l’utilisatrice dispose d’une version d’AEM Forms Designer antérieure à la version 6.5.15.0.
* **Cas 2** : lorsque l’utilisateur ou l’utilisatrice dispose de la version 6.5.15.0 d’AEM Forms Designer.

+++**Lorsque l’utilisateur ou l’utilisatrice dispose d’une version d’AEM Forms Designer antérieure à la version 6.5.15.0.**

Si vous utilisez un programme d’installation autonome pour AEM Forms Designer, procédez comme suit :

1. Avant l’installation d’**AEM Forms Designer 6.5.16.0**, les utilisateurs et les utilisatrices doivent désinstaller toutes les versions précédentes.
1. Téléchargez et installez [AEM Forms Designer 6.5.15.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) à partir de la page Versions d’AEM Forms.
1. Après une installation réussie d’**AEM Forms Designer 6.5.15.0**, téléchargez et installez [AEM Forms Designer 6.5.16.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) en double-cliquant sur le fichier d’installation téléchargé.

+++

+++**Lorsque l’utilisateur ou l’utilisatrice dispose de la version 6.5.15.0 d’AEM Forms Designer**

Si vous utilisez un programme d’installation autonome pour AEM Forms Designer, procédez comme suit :
1. Téléchargez la dernière version d’AEM Forms Designer à partir du [Portail de distribution logicielle](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr).
1. Installez la dernière version d’AEM Forms Designer en double-cliquant sur le fichier d’installation téléchargé.

+++

## Questions fréquentes {#fandq}

* **Est-il possible pour un utilisateur ou une utilisatrice de mettre à niveau et d’installer directement Designer 64 bits ?**
   * Oui, les utilisateurs et utilisatrices peuvent directement mettre à niveau ou installer Designer 64 bits. Pour effectuer la mise à niveau, installez le programme d’installation complet de Designer [SP19](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/Designer-Patch/sp19_x64/aemforms_designer_6_5_0_wwe_win.zip) et appliquez la version de correctif de Designer qui a suivi.

     >[!NOTE]
     > Avant de procéder à la mise à niveau vers Designer 64 bits, désinstallez d’abord Designer 32 bits, le cas échéant.

* **Est-il possible pour les utilisateurs et utilisatrices de conserver les deux versions 32 et 64 bits installées sur leur système ?**
   * Non, les installations 32 bits et 64 bits ne fonctionneront pas sur le même ordinateur. L’utilisateur ou l’utilisatrice peut disposer soit de Designer 32 bits, soit de Designer 64 bits.

* **Comment vérifier si un utilisateur ou une utilisatrice dispose de Designer 64 bits ou de Designer 32 bits ?**
   * Il y a deux façons de vérifier la version de Forms Designer :

      1. Ouvrez Designer, accédez à l’aide, cliquez sur À propos de Designer et vous verrez les informations sur la version de Designer ainsi que les informations sur les bits. Par exemple, vous voyez qu’il est écrit 64 bits en bas de la version comme indiqué ici :
         `6.5.21.20240522.1.161 | 64 bit`
      1. Ouvrez Designer, une icône de marque s’affiche en haut à gauche et contient des informations 64 bits avec le nom du produit.

