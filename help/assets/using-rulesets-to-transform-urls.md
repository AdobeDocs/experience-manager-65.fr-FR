---
title: Utilisation de jeux de règles de transformation d’URL
description: Vous pouvez déployer des ensembles de règles dans Dynamic Media pour transformer les URL. Les ensembles de règles sont des ensembles d’instructions écrites dans un langage de scripts (comme JavaScript) qui évaluent des données XML et déclenchent certaines actions si ces données remplissent des conditions spécifiques.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: Business Practitioner, Administrator,Developer
exl-id: b0ac587b-8592-4d37-9ce0-98a0859c367f
feature: Configuration,Rulesets
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 98%

---

# Utilisation d’ensembles de règles pour transformer des URL {#using-rulesets-to-transform-urls}

Vous pouvez déployer des ensembles de règles dans Dynamic Media pour transformer les URL. Les ensembles de règles sont des ensembles d’instructions écrites dans un langage de scripts (comme JavaScript) qui évaluent des données XML et déclenchent certaines actions si ces données remplissent des conditions spécifiques. Chaque règle définit au moins une condition et une action. Une règle évalue si les données XML remplissent les conditions et, si tel est le cas, déclenche les actions appropriées. Les exemples d’ensembles de règles comprennent les éléments suivants :

* Ajout d’un suffixe de type MIME. De nombreux services et sites web ont besoin de suffixes d’image, comme l’ajout de `.jpg` à une URL.
* Création d’un chemin de dossier vers l’URL pour le SEO (Search Engine Optimization, ou optimisation du moteur de recherche).

   Consultez [Comment Adobe Dynamic Media Classic prend en charge le SEO](/help/assets/assets/s7_seo.pdf).

* Ajout de métadonnées vers l’URL pour le SEO (Search Engine Optimization ou optimisation du moteur de recherche).

   Consultez [Comment Adobe Dynamic Media Classic prend en charge le SEO](/help/assets/assets/s7_seo.pdf).

* Définition de la mise en page du contenu pour déclencher le téléchargement.
* Simplifiez le service d’images pour la création de modèles d’URL pour la personnalisation. Par exemple, transformez `rgb{XX,YY,ZZ}` en `\redXX\greenYY\blueZZ` qui est conforme RTF.

* Effectuez la demande de certains caractères à coder tels que `$`, `{` et `}`, et certains caractères à décoder vers ImageServer. Par exemple, Facebook ne fonctionne pas bien avec les URL contenant des caractères spéciaux.

   Voir la section [Suppression des caractères spéciaux des URL](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

Dans le cadre de Dynamic Media, les sites web qui utilisent un système XML pour gérer les informations de ressources peuvent charger des fichiers XML sur Dynamic Media. Vous pouvez désigner l’un de ces fichiers comme fichier d’ensemble de règles de prétraitement pour le service des ressources Dynamic Media. Ce fichier restructure le format du protocole URL standard pour répondre à la logique métier des systèmes intégrés avec Dynamic Media. Vous spécifiez un fichier XML pour servir de chemin d’accès au fichier des définitions d’ensembles de règles.

>[!CAUTION]
>
>Utilisez les ensembles de règles avec prudence ; ceux-ci peuvent empêcher l’affichage du contenu Dynamic Media sur votre site.

Il existe des exemples d’ensembles de règles disponibles afin de vous aider à créer votre propre ensemble de règles.
Voir la section [Référence d’ensemble de règles](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/rule-set-reference/c-rule-set-reference.html?lang=fr).

À l’instar de la création de tous les ensembles de règles, assurez-vous que votre fichier XML est valide avant de le charger à l’aide d’un programme de validation XML tel que xmlvalid.
Voir également la section [Résolution des problèmes liés aux ensembles de règles](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

En outre, assurez-vous d’abord de tester votre ensemble de règles dans un environnement intermédiaire qui n’affecte pas votre environnement de production.
Les environnements de production et les environnements intermédiaires nécessitent en général des identifiants différents.

Consultez l’[application de bureau Adobe Dynamic Media Classic pour obtenir des informations de connexion](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#sign-in-dmc-app).

<!-- OBSOLETE INFORMATION * **NA staging environment** login page: [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **EMEA staging environment** login page: [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **JAPAC staging environment** login page: [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/) -->

Consultez également la section [Utilisation de « ressource » au lieu d’une image « is » dans un ensemble de règles](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Pour déployer des ensembles de règles XML :**

1. Connectez-vous à votre [application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#sign-in-dmc-app).

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

1. Téléchargez votre fichier d’ensemble de règles en procédant comme suit :

   * Sur la barre de Navigation générale, cliquez sur **[!UICONTROL Charger]**.
   * Sur la page **[!UICONTROL Charger]**, près du coin supérieur gauche, cliquez sur **[!UICONTROL Parcourir]**.
   * Dans la boîte de dialogue **[!UICONTROL Ouvrir]**, naviguez jusqu’à votre fichier d’ensemble de règles (XML).
   * Sélectionnez le fichier, puis cliquez sur **[!UICONTROL Ouvrir]**.
   * Sur le côté droit de la page **[!UICONTROL Charger]**, sélectionnez un dossier de destination pour le fichier d’ensemble de règles.
   * Près du bas de la page, assurez-vous que l’option **[!UICONTROL Publier après le chargement]** est cochée.
   * Dans le coin inférieur droit de la page, cliquez sur **[!UICONTROL Soumettre le chargement]**.
   * Sur la barre de Navigation générale, cliquez sur **[!UICONTROL Tâches]** afin de vérifier le statut de la tâche de chargement. Lorsque la colonne **[!UICONTROL État]** sur la page de la **[!UICONTROL Tâche]** indique Chargement terminé, passez aux étapes suivantes.

1. Sur la barre de navigation située en haut de la page, cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Configuration de la publication > Serveur d’images]**.
1. Sur la page du **[!UICONTROL Publication du serveur d’images]**, sous le groupe **[!UICONTROL Gestion de catalogue]**, localisez le **[!UICONTROL Chemin d’accès au fichier des définitions d’ensembles de règles]**, puis cliquez sur **[!UICONTROL Sélectionner]**.
1. Sur la page **[!UICONTROL Sélectionner le fichier de définition de l’ensemble de règles (XML)]**, accédez à votre fichier d’ensemble de règles, puis dans le coin inférieur droit de la page, cliquez sur **[!UICONTROL Sélectionner]**.
1. Dans le coin inférieur droit de la page Configuration, cliquez sur **[!UICONTROL Fermer]**.
1. Exécutez une tâche de Publication de serveur d’images.

   Les conditions d’ensemble de règles sont appliquées aux demandes aux serveurs d’images Dynamic Media en ligne.

   Si vous apportez des modifications au fichier d’ensemble de règles, celles-ci sont immédiatement appliquées lorsque vous rechargez et publiez à nouveau le fichier d’ensemble de règles mis à jour.
