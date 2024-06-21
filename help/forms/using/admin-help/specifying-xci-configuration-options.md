---
title: Définir les options de configuration XCI
description: Découvrez comment définir les options de configuration XCI. Vous pouvez spécifier des valeurs de fichier XCI personnalisées pour le formulaire adaptatif, de sorte qu’il puisse être utilisé lors du rendu du formulaire.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 100%

---

# Définir les options de configuration XCI {#specifying-xci-configuration-options}

Le service Forms vous permet de spécifier un fichier XCI personnalisé à utiliser pour le rendu. (Voir [Configurer des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).) Par défaut, le service Forms remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Le service Forms utilisera alors les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans la console d’administration, cliquez sur **Services** > **>Forms**.
1. Cochez ou décochez la case Utiliser les options XCI par défaut du système. Lorsque cette option est sélectionnée, le service Forms utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream. Lorsque cette option est désélectionnée, le service Forms utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur **Enregistrer**.
