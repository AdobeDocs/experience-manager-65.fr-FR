---
title: Ressources multilingues et traduction des ressources
description: Découvrez comment automatiser les workflows afin de traduire des ressources, y compris des fichiers binaires, des métadonnées et des balises dans plusieurs langues.
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 44%

---

# Ressources multilingues {#multilingual-assets}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/multilingual-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] vous permet d’automatiser les workflows de traduction des ressources (y compris les fichiers binaires, les métadonnées et les balises) pour générer des ressources dans d’autres langues à utiliser dans des projets multilingues.

Pour automatiser les processus de traduction, vous intégrez des fournisseurs de services de traduction à [!DNL Experience Manager] et créer des projets pour traduire des ressources dans plusieurs langues. [!DNL Experience Manager] prend en charge les workflows de traduction humaine et automatique.

Traduction humaine : les ressources traduites sont renvoyées et importées dans [!DNL Experience Manager]. Lorsque votre fournisseur de traduction est intégré à [!DNL Experience Manager], les ressources sont automatiquement envoyées entre [!DNL Experience Manager] et le fournisseur de traduction.

Traduction automatique : le service de traduction automatique traduit instantanément les métadonnées et les balises des ressources.

La traduction des ressources inclut les éléments suivants :

1. [Connexion du Experience Manager au fournisseur de services de traduction](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Création de configurations de structure d’intégration de traduction](/help/sites-administering/tc-tic.md)
1. [Préparation des ressources pour la traduction](preparing-assets-for-translation.md)
1. [Application de services cloud de traduction à des dossiers](transition-cloud-services.md)
1. [Création de projets de traduction](translation-projects.md)

Si votre fournisseur de services de traduction ne fournit pas de connecteur à intégrer à [!DNL Experience Manager], utilisez une [processus alternatif](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Voir aussi [Création de projets de traduction pour des fragments de contenu](creating-translation-projects-for-content-fragments.md).
