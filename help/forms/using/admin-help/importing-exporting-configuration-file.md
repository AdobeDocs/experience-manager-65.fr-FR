---
title: Importer et exporter le fichier de configuration
description: Découvrez comment importer et exporter le fichier de configuration pour modifier les préférences du serveur ou configurer une autre instance de produit d’AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---

# Importer et exporter le fichier de configuration {#importing-and-exporting-the-configuration-file}

Utilisez la page Configuration manuelle pour télécharger une copie des paramètres de configuration au format XML. Les paramètres de ce fichier contrôlent toutes les préférences du serveur. Vous pouvez ensuite modifier le fichier et le charger à nouveau sur le serveur. Vous pouvez également utiliser ce fichier pour configurer une autre instance AEM produit forms.

Pour éviter tout risque de sécurité, la valeur du mot de passe de liaison du serveur d’annuaire n’est pas incluse dans un fichier de configuration exporté. Mettez à jour le mot de passe dans le fichier XML avant d’importer le fichier dans un nouveau système.

>[!NOTE]
>
>L’importation du fichier de configuration reconfigure AEM formulaires en fonction des informations contenues dans le fichier. Seul un administrateur système ou un consultant en services professionnels qui connaît le produit AEM forms et le code XML doit envisager de modifier le fichier de configuration. Il peut être nécessaire de modifier le fichier de configuration, par exemple, pour reconfigurer un paramètre corrompu.

**Exportation des informations de configuration**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Exporter. Si vous utilisez Microsoft Internet Explorer, vous êtes invité à spécifier l’emplacement d’enregistrement du fichier. Si vous utilisez Firefox, le fichier est enregistré sur votre bureau.

**Importation des informations de configuration**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Parcourir pour rechercher le fichier de configuration, sur Importer, puis sur OK.
