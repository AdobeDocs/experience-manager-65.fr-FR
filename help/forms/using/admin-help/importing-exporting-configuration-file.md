---
title: Importation et exportation du fichier de configuration
seo-title: Importation et exportation du fichier de configuration
description: Découvrez comment importer et exporter le fichier de configuration afin de modifier les préférences du serveur ou de configurer une autre instance de produit de formulaire AEM.
seo-description: Découvrez comment importer et exporter le fichier de configuration afin de modifier les préférences du serveur ou de configurer une autre instance de produit de formulaire AEM.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 100%

---

# Importation et exportation du fichier de configuration {#importing-and-exporting-the-configuration-file}

La page Configuration manuelle permet de télécharger une copie des paramètres de configuration au format XML. Les paramètres contenus dans ce fichier contrôlent toutes les préférences du serveur. Vous pouvez modifier ce fichier et le télécharger à nouveau vers le serveur. Vous pouvez également utiliser ce fichier pour configurer une autre instance du produit AEM forms.

Pour éviter tout risque de sécurité, la valeur du mot de passe de liaison du serveur d’annuaire n’est jamais incluse dans un fichier de configuration exporté. Mettez le mot de passe à jour dans le fichier XML avant de l’importer dans un nouveau système.

>[!NOTE]
>
>En important le fichier de configuration, vous reconfigurez AEM forms en fonction des informations contenues dans le fichier. Seul un administrateur système ou un consultant spécialiste maîtrisant le produit AEM forms et le langage XML est habilité à modifier le fichier de configuration. Ces personnes peuvent être amenées à modifier le fichier de configuration, notamment pour reconfigurer un paramètre corrompu.

**Exportation des informations de configuration**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Exporter. Si vous utilisez Microsoft Internet Explorer, vous êtes invité à spécifier l’emplacement d’enregistrement du fichier. Si vous utilisez Firefox, le fichier est enregistré sur le bureau.

**Importation des informations de configuration**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Parcourir pour rechercher le fichier de configuration, sur Importer, puis sur OK.
