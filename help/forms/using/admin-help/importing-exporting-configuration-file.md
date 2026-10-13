---
title: Importer et exporter le fichier de configuration
description: Découvrez comment importer et exporter le fichier de configuration pour modifier les préférences du serveur ou configurer une autre instance de produit AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 100%
---
# Importer et exporter le fichier de configuration {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

La page Configuration manuelle permet de télécharger une copie des paramètres de configuration au format XML. Les paramètres de ce fichier contrôlent toutes les préférences du serveur. Vous pouvez ensuite modifier le fichier et le charger à nouveau sur le serveur. Vous pouvez également utiliser ce fichier pour configurer une autre instance de produit AEM Forms.

Pour éviter tout risque de sécurité, la valeur du mot de passe de liaison du serveur d’annuaire n’est pas incluse dans un fichier de configuration exporté. Mettez à jour le mot de passe dans le fichier XML avant d’importer le fichier dans un nouveau système.

>[!NOTE]
>
>L’importation du fichier de configuration reconfigure AEM Forms en fonction des informations contenues dans le fichier. Seule une personnes chargée de l’administration système ou qui donne des conseils en services professionnels et qui connaît bien le produit AEM Forms et le code XML peut envisager de modifier le fichier de configuration. Il peut être nécessaire de modifier le fichier de configuration, par exemple, pour reconfigurer un paramètre corrompu.

**Exportation des informations de configuration**

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Exporter. Si vous utilisez Microsoft Internet Explorer, vous devez spécifier l’emplacement d’enregistrement du fichier. Si vous utilisez Firefox, le fichier est enregistré sur votre bureau.

**Importation des informations de configuration**

1. Dans la console d’administration, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration.
1. Cliquez sur Parcourir pour trouver le fichier de configuration, sur Importer, puis sur OK.
