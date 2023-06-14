---
title: Définir les options de configuration XCI
description: Découvrez comment spécifier des options de configuration XCI.
uuid: cf9e544d-63cd-4fad-8f89-bdb46eeef409
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f38ebd69-8d1c-49b6-824f-4bf0ec8a8953
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 12%

---

# Définir les options de configuration XCI {#specify-xci-configuration-options}

Output vous permet de spécifier un fichier XCI personnalisé qu’il utilise pour le rendu. (Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).) Par défaut, Output remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Dans ce cas, Output utilise les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans Administration Console, cliquez sur Services > Output.
1. Cochez ou désélectionnez la case Utiliser les options XCI par défaut du système . Lorsque cette option est sélectionnée, Output utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream. Si cette option est désélectionnée, Output utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur Enregistrer.
