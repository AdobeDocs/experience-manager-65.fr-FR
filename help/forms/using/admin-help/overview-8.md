---
title: Présentation du service de sortie
seo-title: Présentation du service de sortie
description: Output vous permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer pour produire un flux de sortie de documents dans différents formats.
seo-description: Output vous permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer pour produire un flux de sortie de documents dans différents formats.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Présentation du service de sortie {#overview-of-output-service}

Output vous permet de fusionner des données de formulaire XML dans une conception de formulaire créée dans Designer pour produire un flux de sortie de documents dans différents formats. Le flux de sortie peut être envoyé vers une imprimante réseau, une imprimante locale ou un fichier de disque.

Vous pouvez utiliser la page Output d’Administration Console pour administrer le service Output. Les paramètres que vous configurez sont utilisés lors de l’exécution, lorsque les paramètres équivalents n’ont pas été indiqués via l’API d’AEM Forms. Si la configuration a été effectuée via le SDK d’AEM Forms, les paramètres configurés avec Administration Console sont remplacés.

Pour plus d’informations sur le service Output, voir le [Guide de référence des services](https://www.adobe.com/go/learn_aemforms_services_61).

Vous pouvez exécuter plusieurs tâches à partir des pages Output d’Administration Console :

* indiquer des jeux de caractères à des fins d’internationalisation (voir [Modification du jeu de caractères](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)) ;
* indiquer des chemins d’accès absolus et relatifs pour les emplacements d’URL, d’URI, de XCI et de fichiers (voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)) ;
* configurer la taille de la mémoire cache et la stratégie de mise en cache (voir [Définition du mode de cache](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) et [Configuration des paramètres du cache](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)) ;
* rendre les polices disponibles sur le serveur d’applications (voir [Rendre les polices disponibles](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)) ;
* définir les polices à incorporer (voir [Définition des polices à incorporer](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)) ;
* définir des options de configuration XCI (voir [Définition des options de configuration XCI](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)) ;
* définir les paramètres de protection (voir [Définition des paramètres de protection](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)).

Une fois les paramètres modifiés, cliquez sur Enregistrer pour les appliquer à Output. Vous n’avez pas besoin de redémarrer le serveur pour que les modifications soient appliquées, mais vous devez redémarrer le service Output lors de la configuration des paramètres du cache.
