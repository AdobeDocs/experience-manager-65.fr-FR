---
title: Balises intelligentes améliorées
description: Balises intelligentes améliorées
contentOwner: AG
feature: Smart Tags, Search
role: User
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1567'
ht-degree: 85%

---

# Comprendre, appliquer et traiter des balises intelligentes {#enhanced-smart-tags}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/smart-tags.html?lang=fr) |
| AEM 6.5 | Cet article |

Les entreprises qui traitent des ressources numériques utilisent de plus en plus le vocabulaire contrôlé par taxonomie dans les métadonnées des ressources. Il s’agit essentiellement d’une liste de mots-clés que les employés, les partenaires et les clients utilisent couramment pour faire référence aux ressources numériques d’une classe particulière et les rechercher. Le balisage des ressources avec un vocabulaire contrôlé par taxonomie permet de s’assurer que les ressources sont facilement identifiées et récupérées.

Comparé aux vocabulaires des langages naturels, le balisage des ressources numériques basé sur la taxonomie métier aide à les aligner avec les activités d’une entreprise et à assurer que les ressources les mieux adaptées apparaissent dans les recherches.

Par exemple, un constructeur de voitures peut baliser les images de voitures avec les noms de modèles afin d’afficher uniquement les images appropriées lors de recherches d’images de différents modèles pour concevoir une campagne de promotion.

Pour que le service de contenu dynamique applique les balises adéquates, entraînez-le à reconnaître votre taxonomie. Pour entraîner le service, regroupez tout d’abord un ensemble de ressources et de balises qui décrivent le mieux ces ressources. Pour faciliter l’apprentissage du service, appliquez ces balises aux ressources et exécutez un workflow d’entraînement.

Une fois une balise entraînée et prête, le service peut appliquer ces balises sur les ressources par un workflow de balisage.

En arrière-plan, le service de contenu dynamique utilise le framework d’intelligence artificielle d’Adobe Sensei pour entraîner son algorithme de reconnaissance d’image sur votre framework de balises et votre taxonomie métier. Cette intelligence de contenu est ensuite utilisée pour appliquer les balises pertinentes sur un ensemble de ressources différentes.

Le service de contenu dynamique est un service cloud hébergé sur [!DNL Adobe Developer Console]. Pour l’utiliser dans [!DNL Adobe Experience Manager], l’administrateur système doit intégrer votre déploiement [!DNL Experience Manager] avec [!DNL Adobe Developer Console].

En résumé, voici les principales étapes pour utiliser le service de contenu dynamique :

* Intégration
* Vérification de ressources et de balises (définition de taxonomie)
* Entraînement du service de contenu dynamique
* Balisage automatique

![Organigramme](assets/flowchart.gif)

## Conditions préalables et formats pris en charge {#prerequisites}

Avant de pouvoir utiliser le service de contenu dynamique, assurez-vous de respecter les conditions suivantes pour créer une intégration sur [!DNL Adobe Developer Console] :

* L’organisation doit disposer d’un compte Adobe ID pourvu de droits d’administrateur.
* Activez le service de contenu dynamique pour votre organisation.
* Pour ajouter un module de base de services de contenu dynamique à un déploiement, une licence de package de base [!DNL Adobe Experience Manager Sites] et le module complémentaire [!DNL Assets].

Le service applique des balises intelligentes aux ressources des types MIME suivants :

* `image/jpeg`
* `image/tiff`
* `image/png`
* `image/bmp`
* `image/gif`
* `image/pjpeg`
* `image/x-portable-anymap`
* `image/x-portable-bitmap`
* `image/x-portable-graymap`
* `image/x-portable-pixmap`
* `image/x-rgb`
* `image/x-xbitmap`
* `image/x-xpixmap`
* `image/x-icon`
* `image/photoshop`
* `image/x-photoshop`
* `image/psd`
* `image/vnd.adobe.photoshop`

Le service applique des balises intelligentes aux rendus de ressources des types MIME suivants :

* `image/jpeg`
* `image/pjpeg`
* `image/png`

## Intégration {#onboarding}

Le service de contenu dynamique est disponible à l’achat sous forme de module complémentaire pour [!DNL Experience Manager]. Une fois que vous l’avez acheté, un e-mail est envoyé à l’administrateur de votre entreprise avec un lien vers [!DNL Adobe I/O].

L’administrateur peut suivre le lien pour intégrer le service de contenu dynamique à [!DNL Experience Manager]. Pour intégrer le service à [!DNL Experience Manager Assets], consultez [Configuration des balises intelligentes](config-smart-tagging.md).

Le processus d’intégration est terminé lorsque l’administrateur configure le service et ajoute des utilisateurs dans [!DNL Experience Manager].

## Révision des ressources et des balises {#reviewing-assets-and-tags}

Après l’intégration, commencez par identifier un ensemble de balises qui décrit le mieux ces images dans le contexte de votre entreprise.

Ensuite, passez en revue les images de façon à identifier une série d’images qui représentent le mieux votre produit pour un besoin particulier de votre entreprise. Vérifiez que les ressources figurant dans la série sélectionnée sont conformes aux [instructions d’entraînement du service de contenu dynamique](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Ajoutez les ressources à un dossier et appliquez les balises à chaque ressource à partir de la page des propriétés. Exécutez ensuite le workflow d’entraînement sur ce dossier. L’ensemble de ressources traité permet au service de contenu dynamique d’entraîner efficacement plus de ressources à l’aide de vos définitions de taxonomie.

>[!NOTE]
>
>1. La formation est un processus irrévocable. Adobe vous recommande de passer en revue les balises de l’ensemble de ressources traité bien avant d’entraîner le service de contenu dynamique sur les balises.
>1. Avant de vous entraîner pour une balise, reportez-vous à [Instructions de formation pour le service de contenu dynamique](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Lorsque vous entraînez le service de contenu dynamique pour la première fois, Adobe recommande de réaliser l’entraînement sur au moins deux balises distinctes.


## Comprendre les résultats de recherche [!DNL Experience Manager] avec les balises intelligentes {#understandsearch}

Par défaut, la recherche [!DNL Experience Manager] associe les termes de recherche avec une clause `AND`. L’utilisation de balises intelligentes ne modifie pas ce comportement par défaut. L’utilisation de balises intelligentes ajoute une clause `OR` supplémentaire pour trouver n’importe quel des termes de recherche liés aux balises intelligentes. Par exemple, pour la recherche de `woman running`. Les ressources avec les mots-clés `woman` ou `running` uniquement dans les métadonnées n’apparaissent pas dans les résultats de recherche par défaut. Toutefois, une ressource balisée avec `woman` ou `running` à l’aide de balises intelligentes apparaît dans une telle requête de recherche. Les résultats de la recherche sont donc une combinaison de :

* ressources avec les mots-clés `woman` et `running` dans les métadonnées ;

* ressources dotées de balises dynamiques avec l’un des mots-clés.

Les résultats de recherche qui correspondent à tous les termes de recherche des champs de métadonnées sont affichés en premier, suivis des résultats de recherche qui correspondent à l’un des termes de recherche des balises intelligentes. Dans l’exemple ci-dessus, l’ordre approximatif d’affichage des résultats de recherche est le suivant :

1. Correspondances de `woman running` dans les différents champs de métadonnées.
1. Correspondances de `woman running` dans les balises intelligentes.
1. Correspondances de `woman` ou de `running` dans les balises intelligentes.

>[!CAUTION]
>
>Si l’indexation Lucene est réalisée à partir d’[!DNL Adobe Experience Manager], la recherche basée sur les balises intelligentes ne fonctionne pas comme prévu.

## Balisage automatique de ressources {#tagging-assets-automatically}

Après avoir entraîné le service de contenu dynamique, vous pouvez déclencher le workflow de balisage pour appliquer automatiquement les balises appropriées à un autre ensemble de ressources similaires.

Vous pouvez exécuter le workflow de balisage périodiquement ou si nécessaire.

>[!NOTE]
>
>Le workflow de balisage s’exécute sur les ressources et les dossiers.

### Balisage périodique {#periodic-tagging}

Vous pouvez activer le service de contenu dynamique de façon à ce qu’il balise périodiquement les ressources au sein d’un dossier. Ouvrez la page de propriétés du dossier de ressources, sélectionnez **[!UICONTROL Activer les balises intelligentes]** sous l’onglet **[!UICONTROL Détails]** et enregistrez les modifications.

Lorsque cette option est sélectionnée pour un dossier, le service de contenu dynamique balise automatiquement les ressources au sein du dossier. Par défaut, le workflow de balisage s’exécute chaque jour à minuit.

### Balisage à la demande {#on-demand-tagging}

Vous pouvez déclencher le workflow de balisage à partir de la console de workflow ou de la chronologie pour baliser instantanément vos ressources.

>[!NOTE]
>
>Si vous exécutez le workflow de balisage à partir de la chronologie, vous pouvez appliquer des balises sur un maximum de 15 ressources à la fois.

#### Balisage des ressources à l’aide de la console de workflow {#tagging-assets-from-the-workflow-console}

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la page **[!UICONTROL Modèles de processus]**, sélectionnez le workflow **[!UICONTROL Balisage intelligent des ressources (gestion des actifs numériques (DAM))]**, puis appuyez/cliquez sur **[!UICONTROL Démarrer le processus]** dans la barre d’outils.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Dans la boîte de dialogue **[!UICONTROL Exécuter le processus]**, accédez au dossier de charge utile contenant les ressources sur lesquelles vous souhaitez appliquer vos balises automatiquement.
1. Indiquez un titre pour le workflow et un commentaire facultatif. Cliquez sur **[!UICONTROL Exécuter]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Pour vérifier si le service de contenu dynamique a correctement balisé vos ressources, accédez au dossier de ressources et passez en revue les balises.

#### Balisage des ressources à partir de la chronologie {#tagging-assets-from-the-timeline}

1. Depuis l’interface utilisateur [!DNL Assets], sélectionnez le dossier contenant les ressources ou des ressources spécifiques auxquelles vous souhaitez appliquer des balises intelligentes.
1. Dans le coin supérieur gauche, ouvrez la **[!UICONTROL Chronologie]**.
1. Ouvrez les actions dans la partie inférieure de la barre latérale gauche et cliquez sur **[!UICONTROL Démarrer le processus]**.

   ![start_workflow](assets/start_workflow.png)

1. Sélectionnez le workflow **[!UICONTROL Balisage intelligent des ressources (gestion des actifs numériques (DAM))]** et spécifiez un titre pour le workflow.
1. Cliquez sur **[!UICONTROL Début]**. Le workflow applique des balises aux ressources. Pour vérifier si le service de contenu dynamique a correctement balisé vos ressources, accédez au dossier de ressources et passez en revue les balises.

>[!NOTE]
>
>Dans les cycles de balisage suivants, seules les ressources modifiées sont balisées à nouveau avec les balises qui viennent d’être entraînées. Toutefois, même les ressources non modifiées sont balisées si l’intervalle entre le dernier cycle de balisage et l’actuel pour le workflow de balisage dépasse 24 heures. Pour les workflows de balisage périodiques, les ressources inchangées sont balisées lorsque l’intervalle dépasse six mois.

## Traitement ou modération des balises intelligentes appliquées {#manage-smart-tags}

Vous pouvez organiser les balises intelligentes pour supprimer toute balise non pertinente qui pourrait avoir été attribuée à vos ressources de marque, afin que seules les balises les plus pertinentes s’affichent.

La modération de balises intelligentes contribue également à affiner les résultats des recherches d’images basées sur des balises, en garantissant que votre image apparaisse dans les résultats de la recherche pour les balises les plus pertinentes. Essentiellement, cela permet d’éliminer les risques d’affichage d’images sans rapport dans les résultats de recherche.

Vous pouvez également attribuer un rang supérieur à une balise afin d’accroître son degré de pertinence par rapport à une image. La promotion d’une balise pour une image augmente la probabilité que cette image apparaisse dans les résultats de recherche lorsque cette balise spécifique est recherchée.

1. Dans la zone de recherche, recherchez des ressources à l’aide d’une balise comme mot-clé.
1. Pour identifier une image que vous ne trouvez pas pertinente pour votre recherche, examinez les résultats de la recherche.
1. Sélectionnez l’image, puis cliquez sur **[!UICONTROL Gérer les balises]** dans la barre d’outils.
1. Examinez les balises sur la page **[!UICONTROL Gérer les balises]**. Si vous ne souhaitez pas que l’image puisse être recherchée sur la base d’une balise spécifique, sélectionnez la balise, puis cliquez sur **[!UICONTROL Supprimer]** dans la barre d’outils. Vous pouvez également cliquer sur le symbole `x` qui s’affiche à côté d’une balise.
1. Pour attribuer un rang supérieur à une balise, vous pouvez aussi la sélectionner et cliquer sur **[!UICONTROL Promouvoir]** dans la barre d’outils. La balise objet d’une conversion est déplacée dans la section **[!UICONTROL Balises]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis sur **[!UICONTROL OK]**.
1. Accédez à la page **[!UICONTROL Propriétés]** de l’image. Remarquez que la balise que vous avez convertie se voit attribuer une pertinence plus élevée et apparaît plus tôt dans les résultats de la recherche.

## Conseils et restrictions {#tips-best-practices-limitations}

* Pour entraîner le modèle, utilisez les images les plus appropriées. L’entraînement ne peut pas être annulé ou le modèle d’entraînement ne peut pas être supprimé. La précision de votre balisage dépend de l’entraînement en cours. Il doit donc être effectué soigneusement.
* L’utilisation des services de contenu dynamique est limitée à 2 millions d’images balisées par an. Toutes les images en double qui sont traitées et balisées sont chacune comptabilisées comme une image balisée.
* Si vous exécutez le workflow de balisage à partir de la chronologie, vous pouvez appliquer des balises sur un maximum de 15 ressources à la fois.
* Les balises intelligentes fonctionnent uniquement pour les formats d’image PNG et JPG. Ainsi, les ressources prises en charge pour lesquelles des rendus ont été créés dans ces deux formats sont balisées avec des balises intelligentes.
