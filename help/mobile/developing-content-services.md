---
title: Content Services
description: Découvrez comment utiliser AEM Mobile Content Services pour demander du contenu géré par AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: 955ffb1c-4fa9-43bb-8e5b-2df7f2d17951
solution: Experience Manager
feature: Mobile
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 2%
---
# Content Services{#content-services}

{{ue-over-mobile}}

>[!CAUTION]
>
>La fonctionnalité Content Services n’est documentée qu’à des fins de prévisualisation.
>
>Elle peut faire l’objet de modifications avec la version 6.3 Service Pack 1.

AEM Mobile Content Services est une fonctionnalité allégée permettant de demander du contenu géré par AEM. Tous les développeurs d’applications peuvent ainsi récupérer du contenu de manière extrêmement performante, sans avoir à posséder de connaissances approfondies du référentiel de contenu AEM (JCR) et du framework web (Sling). Il permet de découpler les applications qui le demandent du référentiel de contenu.

Content Services introduit plusieurs nouveaux éléments AEM qui permettent à un développeur d’accéder au contenu géré par AEM sans connaître la structure de référentiel de ce contenu.

Ces éléments sont nécessaires pour conserver la flexibilité et permettre une expansion future en fournissant une couche d’abstraction entre le contenu géré par AEM et les applications mobiles qui consomment le contenu. Cela permet à AEM Content Services de fonctionner en tant que couche d’abstraction entre les exigences en matière de contenu de l’application native et le référentiel de contenu AEM.

Content Services peut diffuser le contenu sous forme de ressources, d’HTML empaqueté (HTML/CSS/JS) ou de contenu indépendant du canal.

>[!CAUTION]
>
>**Conditions préalables :**
>
>Avant de commencer à utiliser Content Services, assurez-vous d’activer l’indicateur Content Services . Pour activer la création et la gestion de modèles dans votre application, activez les modèles de données dans l’explorateur de configurations.
>
>Pour plus d’informations [&#128279;](/help/mobile/developing-content-services.md)**consultez la documentation** Administration de Content Services et l’[Explorateur de configurations](/help/sites-administering/configurations.md).

![chlimage_1-143](assets/chlimage_1-143.png)

Après avoir défini l’indicateur Content Services et activé les modèles de données dans l’explorateur de configurations, consultez les ressources ci-dessous pour commencer à utiliser AEM Mobile Content Services. Familiarisez-vous avec les concepts de Content Services tels que la gestion des modèles, la gestion des entités suivie de la diffusion/du rendu du contenu pour AEM Mobile Content Services.

* Modèles dans le référentiel
* Rendu et diffusion
