---
title: Définir les options de configuration XCI.
description: Découvrez comment spécifier les options de configuration XCI. Vous pouvez spécifier des valeurs de fichier XCI personnalisées pour le formulaire adaptatif, de sorte qu’il puisse être utilisé lors du rendu du formulaire.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 81%

---

# Définir les options de configuration XCI. {#specify-xci-configuration-options}

Le service Output vous permet de spécifier un fichier XCI personnalisé à utiliser pour le rendu. Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Par défaut, le service Output remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Le service Output utilisera alors les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans la console d’administration, cliquer sur Services > Output. ****
1. Cochez ou désélectionnez la case Utiliser les options XCI par défaut du système. Lorsque cette option est sélectionnée, le service Output utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream. Lorsque cette option est désélectionnée, le service Output utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur **Enregistrer**.
