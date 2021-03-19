---
title: Content Services
seo-title: Content Services
description: Content Services
seo-description: 'null'
uuid: 7bd09c91-3931-400b-bdfc-b064b9ca9668
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 6a7e5472-cb57-4c78-b183-7c6dcac11a4e
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 10%

---


# Content Services{#content-services}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>La fonctionnalité Content Services est uniquement documentée à des fins de prévisualisation.
>
>Il peut être modifié avec la version 6.3 GA Service Pack 1.

AEM Mobile Content Services est une fonctionnalité légère qui permet de demander du contenu géré par AEM. Ainsi, tous les développeurs d’applications disposent d’un moyen très performant de récupérer du contenu sans avoir à connaître AEM référentiel de contenu (JCR) et la structure Web (Sling). Il permet de découpler les applications qui demandent du référentiel de contenu.

Content Services introduit plusieurs nouveaux concepts d’AEM qui permettent à un développeur d’accéder AEM contenu géré sans connaître la structure de référentiel de ce contenu.

Ces éléments sont nécessaires pour conserver une certaine flexibilité et pour permettre une extension future en fournissant une couche d’abstraction entre le contenu géré AEM et les applications mobiles qui consomment le contenu. Cela permet à AEM Content Services de fonctionner comme une couche d’abstraction entre les exigences de contenu de l’application native et le référentiel de contenu AEM.

Content Services peut diffuser le contenu sous la forme de ressources, de code HTML compressé (HTML/CSS/JS) ou de contenu indépendant du canal.

>[!CAUTION]
>
>**Conditions préalables:**
>
>Avant de commencer à utiliser Content Services, veillez à activer l’indicateur Content Services. Pour activer la création et la gestion de modèles dans votre application, vous devez activer les modèles de données dans l’explorateur de configuration.
>
>Voir **[Administration de Content Services](/help/mobile/developing-content-services.md)** et la documentation [Navigateur de configuration](/help/sites-administering/configurations.md) pour plus d’informations.

![chlimage_1-143](assets/chlimage_1-143.png)

Une fois que vous avez défini l’indicateur Content Services et activé les modèles de données dans Configuration Browser, consultez les ressources ci-dessous pour commencer à utiliser AEM Mobile Content Services, familiarisez-vous avec les Concepts de Content Services tels que la gestion des modèles, la gestion des entités, suivie de la diffusion/rendu de contenu pour AEM Mobile Content Services.

* Modèles dans le référentiel
* Rendu et Diffusion
