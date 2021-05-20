---
title: Balises intelligentes améliorées
description: Balises intelligentes améliorées
contentOwner: AG
feature: Balises intelligentes, Recherche
role: Business Practitioner
exl-id: 5eff4a0f-30b1-4753-ad0b-002656eed972
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1600'
ht-degree: 50%

---

# Présentation, application et traitement des balises intelligentes {#enhanced-smart-tags}

Les entreprises qui traitent des ressources numériques utilisent de plus en plus le vocabulaire contrôlé par taxonomie dans les métadonnées des ressources. Il comprend essentiellement une liste des mots-clés que les employés, les partenaires et les clients utilisent fréquemment pour mentionner et rechercher des ressources numériques d’une classe particulière. Le balisage des ressources avec un vocabulaire contrôlé par taxonomie permet de s’assurer que les ressources sont facilement identifiées et récupérées.

Comparé aux vocabulaires des langages naturels, le balisage des ressources numériques basé sur la taxonomie métier aide à les aligner avec les activités d’une entreprise et à assurer que les ressources les mieux adaptées apparaissent dans les recherches.

Par exemple, un constructeur de voitures peut baliser les images de voitures avec les noms de modèles afin d’afficher uniquement les images appropriées lors de recherches d’images de différents modèles pour concevoir une campagne de promotion.

Pour que le service de contenu dynamique applique les balises appropriées, entraînez-le à reconnaître votre taxonomie. Pour entraîner le service, regroupez tout d’abord un ensemble de ressources et de balises qui décrivent le mieux ces ressources. Pour faciliter l’apprentissage du service, appliquez ces balises aux ressources et exécutez un workflow d’entraînement.

Une fois une balise entraînée et prête, le service peut appliquer ces balises sur les ressources par un workflow de balisage.

En arrière-plan, le service de contenu dynamique utilise la structure Adobe Sensei AI pour entraîner son algorithme de reconnaissance d’image sur votre structure de balises et votre taxonomie métier. Cette intelligence de contenu est ensuite utilisée pour appliquer les balises pertinentes sur un ensemble de ressources différentes.

Le service de contenu dynamique est un service cloud hébergé sur [!DNL Adobe Developer Console]. Pour l’utiliser dans [!DNL Adobe Experience Manager], l’administrateur système doit intégrer votre déploiement [!DNL Experience Manager] à [!DNL Adobe Developer Console].

En résumé, voici les principales étapes pour utiliser le service de contenu dynamique :

* Intégration
* Passage en revue des ressources et des balises (définition de la taxonomie)
* Entraînement du service de contenu dynamique
* Balisage automatique

![Organigramme](assets/flowchart.gif)

## Conditions préalables et formats pris en charge {#prerequisites}

Avant de pouvoir utiliser le service de contenu dynamique, assurez-vous de respecter les conditions suivantes pour créer une intégration sur [!DNL Adobe Developer Console]:

* Compte Adobe ID pourvu de droits d’administrateur pour l’organisation.
* Activez le service de contenu dynamique pour votre organisation.
* Pour ajouter le package de base de services de contenu dynamique à un déploiement, attribuez une licence [!DNL Adobe Experience Manager Sites] au package de base et au module complémentaire [!DNL Assets].

Le service applique des balises intelligentes aux ressources des types MIME suivants :

* image/jpeg
* image/tiff
* image/png
* image/bmp
* image/gif
* image/pjpeg
* image/x-portable-anymap
* image/x-portable-bitmap
* image/x-portable-graymap
* image/x-portable-pixmap
* image/x-rgb
* image/x-xbitmap
* image/x-xpixmap
* image/x-icon
* image/photoshop
* image/x-photoshop
* image/psd
* image/vnd.adobe.photoshop

Le service applique des balises intelligentes aux rendus de ressources des types MIME suivants :

* image/jpeg
* image/pjpeg
* image/png

## Intégration {#onboarding}

Le service de contenu dynamique est disponible à l’achat sous la forme d’un module complémentaire de [!DNL Experience Manager]. Une fois l’achat effectué, un courrier électronique est envoyé à l’administrateur de votre entreprise avec un lien vers [!DNL Adobe I/O].

L’administrateur peut suivre le lien pour intégrer le service de contenu dynamique à [!DNL Experience Manager]. Pour intégrer le service à [!DNL Experience Manager Assets], voir [Configuration des balises intelligentes](config-smart-tagging.md).

Le processus d’intégration est terminé lorsque l’administrateur configure le service et ajoute des utilisateurs dans [!DNL Experience Manager].

>[!NOTE]
>
>Si vous utilisez la version [!DNL Experience Manager] 6.3 ou antérieure et avez besoin du service de balisage pour vos ressources, voir [Balises intelligentes](https://helpx.adobe.com/experience-manager/6-3/assets/using/touch-ui-smart-tags.html). Les balises intelligentes n’utilisent pas les dernières fonctionnalités d’IA et sont donc moins précises que le service de balisage intelligent amélioré.

## Vérification des ressources et des balises {#reviewing-assets-and-tags}

Une fois embarqué, la première chose à faire est d’identifier un ensemble de balises qui décrivent le mieux ces images dans le contexte de votre entreprise.

Ensuite, passez en revue les images de façon à identifier une série d’images qui représentent le mieux votre produit pour un besoin particulier de votre entreprise. Vérifiez que les ressources figurant dans la série sélectionnée sont conformes aux [instructions d’entraînement du service de contenu dynamique](/help/assets/config-smart-tagging.md#training-the-smart-content-service).

Ajoutez les ressources à un dossier, puis appliquez les balises à chaque ressource sur la page de propriétés. Exécutez ensuite le workflow d’entraînement sur ce dossier. La série de ressources sélectionnée permet au service de contenu dynamique d’entraîner efficacement plus de ressources avec vos définitions de taxonomie.

>[!NOTE]
>
>1. L’entraînement est un processus irrévocable. Adobe recommande de bien passer en revue les balises dans la série de ressources sélectionnée bien avant d’entraîner le service de contenu dynamique sur les balises.
>1. Avant l’entraînement d’une balise, voir [Instructions d’entraînement du service de contenu dynamique](/help/assets/config-smart-tagging.md#training-the-smart-content-service).
>1. Lorsque vous entraînez le service de contenu dynamique pour la première fois, Adobe recommande de réaliser l’entraînement sur au moins deux balises distinctes.


## Présentation des [!DNL Experience Manager] résultats de recherche avec des balises intelligentes {#understandsearch}

Par défaut, la recherche [!DNL Experience Manager] combine les termes de recherche avec une clause `AND`. L’utilisation de balises intelligentes ne modifie pas ce comportement par défaut. L’utilisation de balises intelligentes ajoute une clause `OR` supplémentaire pour rechercher les termes de recherche liés aux balises intelligentes. Par exemple, pour la recherche de `woman running`. Les ressources avec les mots-clés `woman` ou `running` uniquement dans les métadonnées n’apparaissent pas dans les résultats de recherche par défaut. Toutefois, une ressource balisée avec `woman` ou `running` à l’aide de balises intelligentes apparaît dans une telle requête de recherche. Les résultats de la recherche sont donc une combinaison de :

* Ressources avec des mots-clés `woman` et `running` dans les métadonnées.

* Ressources balisées intelligemment avec l’un des mots-clés.

Les résultats de recherche qui correspondent à tous les termes de recherche dans les champs de métadonnées s’affichent en premier, suivis des résultats de recherche correspondant à l’un des termes de recherche des balises dynamiques. Dans l’exemple ci-dessus, l’ordre approximatif de l’affichage des résultats de recherche est le suivant :

1. Correspondances de `woman running` dans les différents champs de métadonnées.
1. Correspondances de `woman running` dans les balises intelligentes.
1. Correspondances de `woman` ou de `running` dans les balises intelligentes.

>[!CAUTION]
>
>Si l’indexation Lucene est effectuée à partir de [!DNL Adobe Experience Manager], la recherche basée sur les balises intelligentes ne fonctionne pas comme prévu.

## Balisage automatique des ressources {#tagging-assets-automatically}

Après avoir entraîné le service de contenu dynamique, vous pouvez déclencher le workflow de balisage pour appliquer automatiquement les balises appropriées sur une autre série de ressources similaire.

Vous pouvez exécuter le workflow de balisage périodiquement ou au besoin.

>[!NOTE]
>
>Le workflow de balisage s’exécute sur les ressources et les dossiers.

### Balisage périodique {#periodic-tagging}

Vous pouvez activer le service de contenu dynamique de façon à ce qu’il balise périodiquement les ressources au sein d’un dossier. Ouvrez la page des propriétés de votre dossier de ressources, sélectionnez **[!UICONTROL Activer les balises intelligentes]** sous l’onglet **[!UICONTROL Détails]**, puis enregistrez les modifications.

Une fois cette option sélectionnée pour un dossier, le service de contenu dynamique balise automatiquement les ressources qu’il contient. Par défaut, le workflow de balisage s’exécute tous les jours à 00h00.

### Balisage à la demande {#on-demand-tagging}

Vous pouvez déclencher le workflow de balisage à partir de la console de workflow ou de la chronologie pour baliser instantanément vos ressources.

>[!NOTE]
>
>Si vous exécutez le workflow de balisage à partir de la chronologie, vous pouvez appliquer des balises sur un maximum de 15 ressources à la fois.

#### Balisage des ressources à l’aide de la console de workflow {#tagging-assets-from-the-workflow-console}

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la page **[!UICONTROL Modèles de processus]**, sélectionnez le workflow **[!UICONTROL Balisage intelligent des ressources (gestion des actifs numériques)]**, puis appuyez/cliquez sur **[!UICONTROL Démarrer le processus]** dans la barre d’outils.

   ![dam_smart_tag_workflow](assets/dam_smart_tag_workflow.png)

1. Dans la boîte de dialogue **[!UICONTROL Exécuter le processus]**, accédez au dossier de charge utile contenant les ressources sur lesquelles vous souhaitez appliquer vos balises automatiquement.
1. Indiquez un titre pour le workflow et un commentaire facultatif. Cliquez sur **[!UICONTROL Exécuter]**.

   ![tagging_dialog](assets/tagging_dialog.png)

   Pour vérifier si le service de contenu dynamique a correctement balisé vos ressources, accédez au dossier de ressources et passez en revue les balises.

#### Balisage des ressources à partir de la chronologie {#tagging-assets-from-the-timeline}

1. Dans l’interface utilisateur [!DNL Assets], sélectionnez le dossier contenant des ressources ou des ressources spécifiques auxquelles vous souhaitez appliquer des balises intelligentes.
1. Dans le coin supérieur gauche, ouvrez la **[!UICONTROL Chronologie]**.
1. Ouvrez les actions dans la partie inférieure de la barre latérale gauche et cliquez sur **[!UICONTROL Démarrer le processus]**.

   ![start_workflow](assets/start_workflow.png)

1. Sélectionnez le workflow **[!UICONTROL Balisage intelligent des ressources (gestion des actifs numériques)]** et spécifiez un titre pour le workflow.
1. Cliquez sur **[!UICONTROL Début]**. Le workflow applique des balises aux ressources. pour vérifier si le service de contenu dynamique a correctement balisé vos ressources, accédez au dossier de ressources et passez en revue les balises.

>[!NOTE]
>
>Lors des cycles de balisage suivants, seules les ressources modifiées sont à nouveau balisées avec des balises nouvellement entraînées. Toutefois, même les ressources non modifiées sont balisées si l’intervalle entre le dernier cycle de balisage et l’actuel pour le workflow de balisage dépasse 24 heures. Pour les workflows de balisage périodiques, les ressources inchangées sont balisées lorsque l’intervalle dépasse six mois.

## Traitez ou modérez les balises intelligentes appliquées {#manage-smart-tags}

Vous pouvez organiser les balises intelligentes pour supprimer les balises inexactes qui sont affectées à vos images de marque afin que seules les balises les plus pertinentes soient affichées.

La modération de balises intelligentes contribue également à affiner les résultats des recherches d’images basées sur des balises, en garantissant que votre image apparaisse dans les résultats de la recherche pour les balises les plus pertinentes. Essentiellement, cela réduit les risques que des images non pertinentes apparaissent dans les résultats de la recherche.

Vous pouvez également attribuer un rang supérieur à une balise afin d’accroître sa pertinence pour une image. La promotion d’une balise pour une image augmente les risques que l’image apparaisse dans les résultats de recherche lorsque la balise particulière est recherchée.

1. Dans la zone de recherche, recherchez des ressources à l’aide d’une balise comme mot-clé.
1. Pour identifier une image que vous ne trouvez pas pertinente pour votre recherche, passez en revue les résultats de la recherche.
1. Sélectionnez l’image, puis cliquez sur **[!UICONTROL Gérer les balises]** dans la barre d’outils.
1. Sur la page **[!UICONTROL Gérer les balises]** , passez en revue les balises. Si vous ne souhaitez pas que l’image soit recherchée sur la base d’une balise spécifique, sélectionnez la balise, puis cliquez sur **[!UICONTROL Supprimer]** dans la barre d’outils. Vous pouvez également cliquer sur le symbole `x` qui s’affiche en regard d’une balise.
1. Si vous le souhaitez, pour attribuer un rang supérieur à une balise, sélectionnez-la et cliquez sur **[!UICONTROL Convertir]** dans la barre d’outils. La balise objet d’une conversion est déplacée dans la section **[!UICONTROL Balises]**.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis sur **[!UICONTROL OK]**
1. Accédez à la page **[!UICONTROL Propriétés]** de l’image. Notez que la balise que vous avez promue se voit attribuer plus de pertinence et apparaît plus tôt dans les résultats de recherche.

## Conseils et restrictions {#tips-best-practices-limitations}

* L’utilisation des services de contenu dynamique est limitée à 2 millions d’images balisées par an. Toutes les images en double qui sont traitées et balisées sont chacune comptabilisées comme une image balisée.
* Si vous exécutez le workflow de balisage à partir de la chronologie, vous pouvez appliquer des balises sur un maximum de 15 ressources à la fois.
* Les balises intelligentes fonctionnent uniquement pour les formats d’image PNG et JPG. Ainsi, les ressources prises en charge pour lesquelles des rendus ont été créés dans ces deux formats sont balisées avec des balises intelligentes.
