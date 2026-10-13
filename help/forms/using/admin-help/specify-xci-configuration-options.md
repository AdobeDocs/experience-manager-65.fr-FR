---
title: Définir les options de configuration XCI
description: Découvrez comment définir les options de configuration XCI. Vous pouvez spécifier des valeurs de fichier XCI personnalisées pour le formulaire adaptatif, de sorte qu’il puisse être utilisé lors du rendu du formulaire.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
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
source-wordcount: '161'
ht-degree: 100%
---
# Définir les options de configuration XCI {#specify-xci-configuration-options}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Le service Output vous permet de spécifier un fichier XCI personnalisé à utiliser pour le rendu. Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

Par défaut, le service Output remplace certaines des options spécifiées dans le fichier XCI, notamment :

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

Vous pouvez sélectionner des options qui annulent le remplacement des options répertoriées ci-dessus. Le service Output utilisera alors les valeurs spécifiées dans le fichier XCI personnalisé.

1. Dans la console d’administration, cliquer sur Services > Output. ****
1. Sélectionnez ou désélectionnez la case Utiliser les options XCI par défaut du système. Lorsque cette option est sélectionnée, le service Output utilise ses valeurs par défaut pour les paramètres paquets, créateur, producteur et compressObjectStream. Lorsque cette option est désélectionnée, le service Output utilise les valeurs spécifiées dans le fichier XCI personnalisé.
1. Cliquez sur **Enregistrer**.
