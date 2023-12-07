---
title: Présentation du service de sortie
description: Output permet de fusionner des données de formulaire XML avec une conception de formulaire créée dans Designer pour créer un flux de sortie de document dans différents formats.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 7%

---

# Présentation du service de sortie {#overview-of-output-service}

Output permet de fusionner des données de formulaire XML avec une conception de formulaire créée dans Designer pour créer un flux de sortie de document dans différents formats. Le flux de sortie peut être envoyé vers une imprimante réseau, une imprimante locale ou un fichier de disque.

Vous pouvez utiliser la page Output d’Administration Console pour administrer le service Output. Les paramètres que vous configurez sont utilisés au moment de l’exécution lorsque les paramètres équivalents n’ont pas été spécifiés via l’API d’AEM forms. La configuration effectuée via le SDK d’AEM forms remplace les paramètres configurés à l’aide de la console d’administration.

Pour plus d’informations sur le service Output, voir [Référence des services](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

Dans les pages Output d’Administration Console, vous pouvez effectuer plusieurs tâches :

* Spécifiez des jeux de caractères pour l’internationalisation. (Voir [Modification du jeu de caractères](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* Spécifiez les chemins d’accès absolus et relatifs pour les URL, les URI, les XCI et les emplacements de fichiers. (Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* Configurez les tailles et les stratégies de cache. (Voir [Spécification du mode de cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) et [Configuration des paramètres du cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* Rendez les polices disponibles sur le serveur d’applications. (Voir [Rendre les polices disponibles](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* Définition des polices à incorporer. (Voir [Définition des polices à incorporer](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* Définition des options de configuration XCI. (Voir [Définition des options de configuration XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* Définition des paramètres de protection. (Voir [Définition des paramètres de protection](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

Après avoir modifié les paramètres, cliquez sur Enregistrer pour les appliquer à Output. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications prennent effet, mais vous devrez peut-être redémarrer le service Output lors de la configuration des paramètres du cache.
