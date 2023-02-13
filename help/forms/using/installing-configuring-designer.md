---
title: Installer et configurer Designer
seo-title: Installing and configuring Designer
description: Designer est disponible sous la forme d’un programme autonome et est également fourni avec Workbench. Découvrez comment installer la version autonome de Designer.
seo-description: Designer is available as a stand-alone installer and is also bundled with Workbench. Learn how to install stand-alone Designer.
uuid: c5b779d1-cb6a-48f4-87d6-48464753e516
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: designer
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f3a5b5ce-2262-4d5d-a8ae-d59a3a4229e7
docset: aem65
role: Admin
exl-id: 90503d29-e079-43f4-a5dc-ce90ed7844c6
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: ht
source-wordcount: '290'
ht-degree: 100%

---

# Installation et configuration de Designer{#installing-and-configuring-designer}

## Prérequis {#pre-requisites}

* Installation de la version 32 bits de [Redistribuable Visual C++ 2019 (x86)](https://learn.microsoft.com/fr-fr/cpp/windows/latest-supported-vc-redist?view=msvc-170). Assurez-vous que les packages d’exécution redistribuables susmentionnés sont installés avant de démarrer l’installation.
* Un utilisateur ou une utilisatrice disposant des droits d’administration pour installer ou désinstaller Designer.

## Installation de Designer {#install-designer}

Designer est disponible sous la forme d’un programme autonome et est également fourni avec Workbench. Si vous utilisez un programme d’installation autonome pour Designer, procédez comme suit :

1. Désinstallez la version précédente d’AEM Forms Designer, si elle est déjà installée.
1. Téléchargez Designer depuis [Adobe Licensing Website](https://licensing.adobe.com/).

   >[!NOTE]
   >
   > * À compter de la version d’Adobe Experience Manager 6.5 Forms Service Pack 15 (6.5.15.0), la version Forms Designer inclut également la version du Service Pack. Par exemple, pour le Service Pack 15, le numéro de version est 6.5.15.20221112.1.0. Dans cet exemple, 6.5.15 est la version du Service Pack.


1. Lancez le programme d’installation de Designer en cliquant deux fois sur setup.exe.
1. Continuez et fournissez vos détails ainsi que le numéro de série dans la boîte de dialogue Personnalisation.
1. Si vous acceptez les termes du contrat de licence, appuyez sur Suivant pour continuer.
1. (Facultatif) Modifiez le chemin d’installation par défaut, si vous voulez installer Designer à l’emplacement de votre choix. Cliquez sur Suivant.
1. Cliquez sur Précédent pour modifier les préférences. Pour installer Designer, cliquez sur Installer.
1. Cliquez sur Terminer à la fin de l’installation.

Vous pouvez également installer Designer via la ligne de commande en mode passif ou silencieux.

* Installation en ligne de commande passive : le programme d’installation affiche une barre de progression qui indique que l’installation est en cours mais aucun message d’erreur ou d’invite ne s’affiche. Une fois l’installation lancée, vous ne pouvez pas l’annuler.

```shell
msiexec /i "<absolute path>\Designer.msi" /passive SERIALNUMBER=****-****-****-****-****-****
```

* Installation en ligne de commande silencieuse : le programme d’installation exécute l’installation sans afficher d’interface utilisateur. Aucun message, invite ou boîte de dialogue ne s’affiche. Une fois l’installation lancée, vous ne pouvez pas l’annuler.

```shell
msiexec /i "<absolute path>\Designer.msi" /quiet SERIALNUMBER=****-****-****-****-****-****
```
