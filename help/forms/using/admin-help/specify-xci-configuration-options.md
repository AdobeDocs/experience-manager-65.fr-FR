---
title: Définir les options de configuration XCI
description: Découvrez comment spécifier des options de configuration XCI.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 7%

---

# Définir les options de configuration XCI {#specify-xci-configuration-options}

Output vous permet de spécifier un fichier XCI personnalisé qu’il utilise pour le rendu. Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Par défaut, Output remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Dans ce cas, Output utilise les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans Administration Console, cliquez sur **Services** > sortie.
1. Cochez ou désélectionnez la case Utiliser les options XCI par défaut du système . Lorsque cette option est sélectionnée, Output utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream. Si cette option est désélectionnée, Output utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur **Enregistrer**.
