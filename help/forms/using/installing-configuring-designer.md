---
title: Installer et configurer Designer
description: Designer est disponible sous la forme d’un programme autonome et est également fourni avec Workbench. Découvrez comment installer Designer autonome.
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
feature: Forms Designer
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 78%

---

# Installation et configuration de Designer{#installing-and-configuring-designer}

## Prérequis {#pre-requisites}

+++ Pour AEM Forms Designer 64 bits (recommandé)

* Installation de la version 64 bits de  [Redistribuable Visual C++ 2019 (x64)](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation.
* Un utilisateur ou une utilisatrice disposant des droits d’administration pour installer ou désinstaller AEM Forms Designer.

+++

+++ Pour AEM Forms Designer 32 bits

* Installation de la version 32 bits de  [Redistribuable Visual C++ 2019 (x64)](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation.
* Un utilisateur ou une utilisatrice disposant des droits d’administration pour installer ou désinstaller AEM Forms Designer.

+++

>[!NOTE]
>
> La version 64 bits du concepteur a été introduite avec AEM 6.5 Forms Service Pack 19 (6.5.19.0).



## Installer AEM Forms Designer {#install-designer}

Designer est disponible sous la forme d’un programme autonome et est également fourni avec Workbench. Si vous utilisez un programme d’installation autonome pour AEM Forms Designer, procédez comme suit :

1. Désinstallez la version précédente d’AEM Forms Designer, si elle est déjà installée.
1. Téléchargez AEM Forms Designer 64 bits (recommandé) ou AEM Forms Designer 32 bits selon vos besoins.

   >[!NOTE]
   > 
   >* Forms Designer 32 bits doit être abandonné avec la version 6.5 Forms Service Packs 20 (6.5.20.0) d’AEM. Adobe recommande d’effectuer la mise à niveau vers le concepteur Forms 64 bits.
   >* Forms Designer 64 bits est disponible uniquement pour les Service Packs 19 (6.5.19.0) d’AEM 6.5 Forms ou versions ultérieures.
   >* À compter de la version d’Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0), la version Forms Designer inclut également la version du Service Pack. Par exemple, pour le Service Pack 15, le numéro de version est 6.5.15.20221112.1.0. Dans cet exemple, 6.5.15 est la version du Service Pack.

1. Lancez le programme d’installation d’AEM Forms Designer en cliquant deux fois sur setup.exe.
1. Continuez et fournissez vos détails ainsi que le numéro de série sur l’écran Personnalisation.

   >[!NOTE]
   >
   >* Obtenez votre clé de licence Forms Designer à partir de [Adobe Licensing Website](https://licensing.adobe.com/).

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
1. Installez la dernière version d’AEM Forms Designer en double-cliquant sur le fichier d’installation téléchargé.

+++