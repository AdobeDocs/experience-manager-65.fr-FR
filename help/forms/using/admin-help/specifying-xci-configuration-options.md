---
title: Définir les options de configuration XCI
description: Découvrez comment spécifier des options de configuration XCI.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 21%

---

# Définir les options de configuration XCI {#specifying-xci-configuration-options}

Forms vous permet de spécifier un fichier XCI personnalisé à utiliser pour le rendu. (Voir [Configuration des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Par défaut, Forms remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Dans ce cas, Forms utilise les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans Administration Console, cliquez sur **Services** > **Forms**.
1. Cochez ou désélectionnez la case Utiliser les options XCI par défaut du système. Lorsque cette option est sélectionnée, Forms utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream . Si cette option est désélectionnée, Forms utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur **Enregistrer**.
