---
title: Définition des options de configuration XCI
seo-title: Définition des options de configuration XCI
description: Découvrez comment définir les options de configuration XCI.
seo-description: Découvrez comment définir les options de configuration XCI.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 100%

---

# Définition des options de configuration XCI {#specifying-xci-configuration-options}

Le service Forms vous permet de spécifier un fichier XCI personnalisé à utiliser pour le rendu (voir [Configuration des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)). Par défaut, le service Forms remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Le service Forms utilisera alors les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans Administration Console, cliquez sur Services > Forms.
1. Cochez ou désélectionnez la case Utiliser les options XCI par défaut du système. Lorsque cette option est sélectionnée, le service Forms utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream. Lorsque cette option est désélectionnée, le service Forms utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur Enregistrer.
