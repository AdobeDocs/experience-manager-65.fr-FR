---
title: Utilisation d’ensemble de règles pour transformer les URL
description: Vous pouvez déployer des ensembles de règles dans Dynamic Media pour transformer les URL. Les ensembles de règles sont des ensembles d’instructions écrites dans un langage de scripts (comme JavaScript) qui évaluent des données XML et déclenchent certaines actions si ces données remplissent des conditions spécifiques.
uuid: 9fed0c83-67b7-4483-a9b4-322e6a483449
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: abcff903-204b-4ab6-87d8-6f0ce63d7b41
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Utilisation de jeux de règles pour transformer des URL {#using-rulesets-to-transform-urls}

Vous pouvez déployer des ensembles de règles dans Dynamic Media pour transformer les URL. Les ensembles de règles sont des ensembles d’instructions écrites dans un langage de scripts (comme JavaScript) qui évaluent des données XML et déclenchent certaines actions si ces données remplissent des conditions spécifiques. Chaque règle définit au moins une condition et une action. Une règle évalue si les données XML remplissent les conditions et, si tel est le cas, déclenche les actions appropriées. Les exemples d’ensembles de règles comprennent les éléments suivants :

* Ajout d’un suffixe de type MIME. Many services and websites require image suffixes, such as adding `.jpg` to a URL.
* Création d’un chemin de dossier vers l’URL pour le SEO (Search Engine Optimization, optimisation du moteur de recherche).

   Voir la section [Comment le système de publication Adobe Scene7 prend en charge le SEO](/help/assets/assets/s7_seo.pdf).

* Ajout de métadonnées vers l’URL pour le SEO (Search Engine Optimization, optimisation du moteur de recherche).

   Voir la section [Comment le système de publication Adobe Scene7 prend en charge le SEO](/help/assets/assets/s7_seo.pdf).

* Définition de la mise en page du contenu pour déclencher le téléchargement.
* Simplifiez le service d’images pour la création de modèles d’URL pour la personnalisation. Par exemple, transformez `rgb{XX,YY,ZZ}` en RTF-ready `\redXX\greenYY\blueZZ`

* Request certain characters to be encoded such as `$`, `{`, and `}`, and certain characters to be decoded toward ImageServer. Par exemple, Facebook ne fonctionne pas bien avec les URL contenant des caractères spéciaux.

   Voir la section [Suppression des caractères spéciaux des URL](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/remove-special-characters-urls.html).

Dans le cadre de Dynamic Media, les sites Web qui utilisent un système XML pour gérer les informations de ressources peuvent charger des fichiers XML sur Dynamic Media. Vous pouvez désigner l’un de ces fichiers comme fichier d’ensemble de règles de prétraitement pour le service des ressources Dynamic Media. Ce fichier restructure le format du protocole URL standard pour répondre à la logique métier des systèmes intégrés avec Dynamic Media. Vous spécifiez un fichier XML pour servir de chemin d’accès au fichier des définitions d’ensembles de règles.

>[!CAUTION]
>
>Soyez prudent lorsque vous utilisez des jeux de règles ; ils peuvent empêcher l’affichage du contenu Contenu Contenu Contenu multimédia dynamique sur votre site Web.

Il existe des exemples d’ensembles de règles disponibles afin de vous aider à créer votre propre ensemble de règles.
Voir la section [Référence d’ensemble de règles](https://marketing.adobe.com/resources/help/en_US/s7/is_ir_api/is_api/image_catalog/c_rule_set_reference.html).

A l’instar de la création de tous les ensembles de règles, assurez-vous que votre fichier XML est valide avant de le charger à l’aide d’un programme de validation XML tel que xmlvalid.
Voir également la section [Résolution des problèmes liés aux ensembles de règles](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/scene7-ruleset-troubleshooting.html).

En outre, assurez-vous d’abord de tester votre ensemble de règles dans un environnement intermédiaire qui n’affecte pas votre environnement de production.
Les environnements de production et les environnements intermédiaires nécessitent en général des identifiants différents.

* **Page de connexion de l&#39;environnement** intermédiaire NA : [https://s7sps1-staging.scene7.com/IpsWeb/](https://s7sps1-staging.scene7.com/IpsWeb/)
* **Page de connexion de l&#39;environnement** intermédiaire EMEA : [https://s7sps3-staging.scene7.com/IpsWeb/](https://s7sps3-staging.scene7.com/IpsWeb/)
* **Page de connexion de l’environnement** d’évaluation JAPAC : [https://s7sps5-staging.scene7.com/IpsWeb/](https://s7sps5-staging.scene7.com/IpsWeb/)

Voir également la section [Utilisation de « ressource » au lieu d’une image « is » dans un ensemble de règles](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/ruleset-asset-instead-image.html).

**Pour déployer des ensembles de règles XML :**

1. Connectez-vous à votre compte Dynamic Media Classic :

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne connaissez pas ces informations, contactez le support technique.

1. Téléchargez votre fichier d’ensemble de règles en procédant comme suit :

   * Sur la barre de Navigation générale, cliquez sur **[!UICONTROL Charger]**.
   * On the **[!UICONTROL Upload]** page, near the upper-left corner, click **[!UICONTROL Browse]**.
   * In the **[!UICONTROL Open]** dialog box, browse to your rule set file (XML).
   * Sélectionnez le fichier, puis cliquez sur **[!UICONTROL Ouvrir]**.
   * On the right side of the **[!UICONTROL Upload]** page, select a destination folder for the rule set file.
   * Près du bas de la page, assurez-vous que l’option **[!UICONTROL Publier après le chargement]** est cochée.
   * Dans le coin inférieur droit de la page, cliquez sur **[!UICONTROL Soumettre le chargement]**.
   * Sur la barre de Navigation générale, cliquez sur **[!UICONTROL Tâches]** afin de vérifier le statut de la tâche de chargement. When the **[!UICONTROL Status]** column on the **[!UICONTROL Job]** page says Upload Done, continue to the next steps.

1. Sur la barre de navigation située en haut de la page, cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Configuration de la publication > Serveur d’images]**.
1. On the **[!UICONTROL Image Server Publish]** page, under the **[!UICONTROL Catalog Management]** group, locate **[!UICONTROL Rule Set Definition File Path]**, then click **[!UICONTROL Select]**.
1. On the **[!UICONTROL Select Rule Set Definition File (XML)]** page, browse to your rule set file, then in the lower-right corner of the page, click **[!UICONTROL Select]**.
1. Dans le coin inférieur droit de la page Configuration, cliquez sur **[!UICONTROL Fermer]**.
1. Exécutez une tâche de Publication de serveur d’images.

   Les conditions d’ensemble de règles sont appliquées aux demandes aux serveurs d’images Dynamic Media en ligne.

   Si vous apportez des modifications au fichier d’ensemble de règles, celles-ci sont immédiatement appliquées lorsque vous rechargez et publiez à nouveau le fichier d’ensemble de règles mis à jour.

