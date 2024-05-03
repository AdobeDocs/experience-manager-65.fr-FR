---
title: Créer ou ajouter un formulaire adaptatif à une page AEM Sites
description: Découvrez comment créer ou ajouter facilement et sans effort un formulaire adaptatif à votre page AEM Sites. Découvrez les bonnes pratiques et les techniques étape par étape pour intégrer des formulaires dynamiques et personnalisables à votre site web, en optimisant vos expériences numériques pour un impact maximum.
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms, Foundation Components
exl-id: dcf023a1-8735-48cb-b3ea-d17357eeedaf
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 100%

---

# Créer ou ajouter un formulaire adaptatif à une page AEM Sites {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM 6.5 | Cet article |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page) |

Avec AEM Forms, vous pouvez facilement incorporer des formulaires adaptatifs dans vos pages web. Vos visiteurs et visiteuses peuvent ainsi remplir et envoyer facilement des formulaires sans jamais quitter la page sur laquelle ils se trouvent. Ce faisant, ils ou elles peuvent continuer à utiliser sans effort d’autres éléments du site web tout en interagissant activement avec le formulaire.

Vous pouvez utiliser l’éditeur de page d’AEM pour créer et ajouter rapidement plusieurs formulaires à vos pages AEM Sites. L’utilisation de l’éditeur de page d’AEM permet aux auteurs et autrices de contenu de créer des expériences de capture de données en toute transparence dans une page Sites à l’aide de la puissance des composants des formulaires adaptatifs, notamment le comportement dynamique, les validations, l’intégration de données, la génération d’un document d’enregistrement et l’automatisation de la gestion commerciale. L’éditeur de page permet également d’utiliser différentes fonctionnalités des pages d’AEM Sites, telles que le contrôle de version, le ciblage, la traduction et le gestionnaire de sites multiples.

AEM Forms fournit un conteneur de formulaires adaptatifs et des composants Formulaires adaptatifs - Incorporer. Vous pouvez utiliser le conteneur de formulaires adaptatifs pour créer un formulaire dans un fragment d’expérience ou une page AEM Sites, tandis que le composant Formulaire adaptatif – Incorporer permet d’ajouter un formulaire adaptatif existant ou de créer un formulaire à l’aide de l’éditeur de formulaire adaptatif.

![Formulaire adaptatif dans la page Sites](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## Avantages de l’utilisation du composant Conteneur de formulaires adaptatifs dans l’éditeur de page d’AEM ou dans un fragment d’expérience

L’utilisation du conteneur de formulaires adaptatifs dans l’éditeur de page d’AEM vous permet de créer des expériences de capture de données transparentes dans une page Sites à l’aide de toute la puissance des composants des formulaires adaptatifs, notamment le comportement dynamique, les validations et l’intégration de données, ainsi que de générer un document d’enregistrement et d’automatiser la gestion commerciale. Le conteneur de formulaires adaptatifs vous permet également d’utiliser les différentes fonctionnalités des pages AEM Sites, telles que le contrôle de version, le ciblage, la traduction et le gestionnaire de sites multiples, améliorant ainsi l’expérience globale de création et de gestion de formulaires. Examinons quelques-unes de ces fonctionnalités :

* **Contrôle de version :** les pages AEM Sites vous offrent des [fonctionnalités de contrôle de version fiables](/help/sites-authoring/working-with-page-versions.md), ce qui vous permet de suivre et de gérer différentes versions de vos formulaires. Vous pouvez ainsi apporter des modifications et des améliorations aux formulaires tout en conservant la possibilité de restaurer des versions précédentes si nécessaire. Le contrôle de version garantit une approche contrôlée et organisée du développement et de l’évolution des formulaires.
* **Ciblage (intégration à Adobe Target) :** avec les fonctionnalités de ciblage des pages AEM Sites, vous pouvez également [personnaliser l’expérience du formulaire pour différentes audiences](/help/sites-administering/target.md). En exploitant les segments d’utilisateurs et d’utilisatrices et les critères de ciblage, vous pouvez personnaliser le contenu, la conception ou le comportement du formulaire en fonction de groupes d’utilisateurs et d’utilisatrices spécifiques. Vous pouvez ainsi offrir une expérience de formulaire personnalisée et pertinente, ce qui augmente l’engagement et les taux de conversion.
* **Traduction :** intégration transparente d’AEM Sites [à des services de traduction](/help/sites-administering/translation.md), ce qui vous permet de traduire facilement des formulaires en plusieurs langues. Cette fonctionnalité simplifie le processus de localisation, en veillant à ce que vos formulaires soient accessibles à une audience globale. Vous pouvez gérer efficacement les traductions dans les projets de traduction d’AEM, ce qui réduit le temps et les efforts requis pour la prise en charge des formulaires multilingues. Pour plus d’informations sur la traduction, reportez-vous à la section Remarques.
* **Gestion multisite et Live Copy :** AEM Sites vous offre une fonctionnalité fiable [de gestion multisite et de Live Copy](/help/sites-administering/msm.md), vous permettant de créer et de gérer plusieurs sites web au sein d’un seul environnement. Cette fonctionnalité vous permet désormais de réutiliser des formulaires sur différents sites, assurant ainsi la cohérence et réduisant les efforts de duplication. Grâce à un contrôle et une gestion centralisés, vous pouvez gérer et mettre à jour efficacement les formulaires sur plusieurs sites web.
* **Thèmes :** les pages AEM Sites vous fournissent un cadre pour la conception et la gestion de styles visuels cohérents sur plusieurs pages web. Elles définissent les couleurs, les polices, les feuilles de style et d’autres éléments visuels qui contribuent à l’aspect général du site web. [Vous pouvez utiliser les thèmes conçus pour une page AEM Sites pour un formulaire adaptatif afin de gagner du temps.](/help/sites-authoring/style-system.md).
* **Balisage :** les pages AEM Sites vous permettent d’[affecter des balises ou des étiquettes à une page, à une ressource ou à un autre contenu](/help/sites-authoring/tags.md). Les balises sont des mots-clés ou des étiquettes de métadonnées qui permettent de classer et d’organiser du contenu selon des critères spécifiques. Vous pouvez affecter une ou plusieurs balises aux pages, aux ressources ou à tout autre élément de contenu dans AEM afin d’améliorer la recherche et de classer les ressources.
* **Verrouillage et déverrouillage de contenu :** AEM Sites permet à ses utilisateurs et utilisatrices de [contrôler l’accès aux pages et leurs modifications](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page) dans l’environnement AEM Sites. Lorsqu’une page est verrouillée, cela signifie qu’elle est protégée contre les changements ou modifications non autorisés par d’autres utilisateurs et utilisatrices. Seule la personne qui a verrouillé le contenu ou l’équipe d’administration désignée peut le déverrouiller pour autoriser les modifications.


## Il existe plusieurs possibilités pour ajouter un formulaire adaptatif dans l’éditeur de page d’AEM.

Vous pouvez tirer pleinement parti de cette fonctionnalité en utilisant les options suivantes :

* **[Ajouter un formulaire adaptatif personnalisé à une page AEM Sites :](#create-an-adaptive-form-in-sites-editor)** créez entièrement un nouveau formulaire en l’adaptant spécifiquement à vos besoins et préférences de conception.

* **[Ajouter un formulaire adaptatif personnalisé à un fragment d’expérience :](#create-an-adaptive-form-in-experience-fragment)** étendez la portée de vos formulaires en les ajoutant aux fragments d’expérience AEM, ce qui permet une réutilisation transparente sur plusieurs pages ou sites.

* **[Convertir un formulaire adaptatif en fragment d’expérience :](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** convertissez un formulaire adaptatif ajouté à une page AEM Sites en un fragment d’expérience pour réutiliser le formulaire sur plusieurs pages AEM Sites.

* **Créer et ajouter des formulaires basés sur des modèles approuvés dans une page AEM Sites :** tirez parti des modèles prévalidés pour créer rapidement des formulaires conformes aux directives de marque et aux normes de conception de votre entreprise. Cette option est disponible uniquement pour les formulaires adaptatifs créés avec l’éditeur de formulaires adaptatifs ou le composant Formulaires adaptatifs - Incorporer.

* **Ajouter des formulaires existants à une page AEM Sites :** intégrez facilement des formulaires que vous avez déjà créés dans vos sites web, ce qui permet aux visiteurs et visiteuses d’interagir directement avec eux. Cette option est disponible uniquement pour les formulaires adaptatifs créés avec l’éditeur de formulaires adaptatifs ou le composant Formulaires adaptatifs - Incorporer.

* **Ajouter plusieurs formulaires à une page AEM Sites ou à un fragment d’expérience :** ajoutez plusieurs formulaires à une page afin de proposer aux utilisateurs et utilisatrices plusieurs choix en fonction de leurs préférences et de leurs besoins. Il peut s’agir d’une combinaison de nouveaux formulaires et de formulaires existants.

## Remarques {#consideration}

* Lorsque vous utilisez le conteneur de formulaires adaptatifs pour créer ou ajouter un formulaire, les formulaires sont traduits et localisés par le biais du flux de traduction AEM Sites. Pour chaque langue, une copie distincte (copie de langue) de la page du site et des formulaires correspondants est générée. Lorsqu’un auteur ou une autrice de contenu modifie une règle dans un formulaire sur la page parente, les mêmes modifications doivent être effectuées dans toutes les copies de langue du formulaire. Le conteneur de formulaires adaptatifs vous permet également d’utiliser diverses fonctionnalités des pages AEM Sites telles que le contrôle de version, le ciblage, la traduction et le gestionnaire de sites multiples.

* Lorsque vous créez ou ajoutez un formulaire à l’aide du composant Formulaire adaptatif - Incorporer, les formulaires sont traduits et localisés à l’aide du flux de traduction AEM Forms. Dans ce cas, un seul formulaire est conservé et référencé dans toutes les copies de langue des pages Sites. Le composant Formulaire adaptatif - Incorporer ne permet pas d’accéder aux différentes fonctionnalités des pages AEM Sites telles que le contrôle de version, le ciblage, la traduction et le gestionnaire de sites multiples.


## Avant de commencer {#before-you-start}

+++  Activation des composants principaux des formulaires adaptatifs pour votre environnement

Assurez-vous que les [composants principaux des formulaires adaptatifs sont activés pour votre environnement](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=fr).

+++

+++  Ajout de bibliothèques clientes de formulaires adaptatifs à la page AEM Sites et aux composants de page de fragment d’expérience

Pour activer la fonctionnalité complète du composant Conteneur de formulaires adaptatifs, ajoutez les bibliothèques clientes Customheaderlibs et Customfooterlibs à votre page AEM Sites à l’aide du pipeline de déploiement. Pour ajouter les bibliothèques :

1. Connectez-vous à votre instance de création AEM et ouvrez CRX DE. L’URL par défaut d’une instance de création s’exécutant localement est `http://localhost:4502/crx/de`.

1. Ouvrez le fichier `/apps/[your-sites-project]/components/page/customheaderlibs.html` et ajoutez le code suivant au fichier :

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Ouvrez le fichier `/apps/[your-sites-project]/components/page/customfooterlibs.html` et ajoutez le code suivant au fichier :

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Ouvrez le fichier `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` et ajoutez le code suivant au fichier :

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Ouvrez le fichier `/apps/[your-sites-project]/components/customfooterlibs.html` et ajoutez le code suivant au fichier :

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Répétez les étapes ci-dessus pour toutes les instances de création et de publication dans votre environnement.

+++

+++ Activation du Conteneur de formulaires adaptatifs

Pour activer le composant [!UICONTROL Conteneur de formulaires adaptatifs] dans la politique du modèle, procédez comme suit :

1. Ouvrez la page AEM Sites ou le fragment d’expérience pour modification. Pour ouvrir la page à modifier, sélectionnez-la, puis cliquez sur Modifier.
1. Ouvrez le modèle de votre page Sites ou Fragment d’expérience. Pour ouvrir le modèle, accédez aux [!UICONTROL Informations sur la page] ![Informations sur la page](/help/forms/using/assets/Smock_Properties_18_N.svg) > [!UICONTROL Modifier le modèle]. Le modèle correspondant s’ouvre dans l’éditeur de modèles.
1. Dans la vue Structure, cliquez sur l’icône **[!UICONTROL Politique]** ![Politique](/help/forms/using/assets/Smock_FeedManagement_18_N.svg) dans la barre de menus. Dans la liste **[!UICONTROL Composants autorisés]**, cochez la case **[!UICONTROL Conteneur de formulaires adaptatifs]** sous **[Nom du projet Archetype AEM] - Formulaire adaptatif**.
1. Cliquez sur **[!UICONTROL Terminé]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Créer un formulaire adaptatif {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Vous pouvez créer un nouveau formulaire à partir de zéro, en l’adaptant spécifiquement à vos besoins et à vos préférences en matière de conception, directement dans une page AEM Sites ou dans un fragment d’expérience. Pour les formulaires à usage unique, il est recommandé d’effectuer une création directe sur une page AEM Sites, tandis que les fragments d’expérience sont parfaits pour les formulaires qui doivent être réutilisés sur plusieurs pages de votre site web.

* [Créer un formulaire dans une page AEM Sites](#create-an-adaptive-form-in-sites-editor)
* [Créer un formulaire dans un fragment d’expérience](#create-an-adaptive-form-in-experience-fragment)
* [Convertir un formulaire adaptatif dans une page AEM Sites en fragment d’expérience](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Créer un formulaire dans une page AEM Sites {#create-an-adaptive-form-in-sites-editor}

Vous pouvez utiliser le composant Conteneur de formulaires adaptatifs dans l’éditeur de page d’AEM pour créer un formulaire personnalisé. Le composant vous permet de créer un formulaire en faisant glisser et en déposant les composants du formulaire. Les composants de formulaire sont basés sur les composants principaux. Vous pouvez facilement les personnaliser en fonction des besoins de votre entreprise.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Pour créer un formulaire adaptatif dans une page Sites :

1. Ouvrez la page AEM Sites en mode d’édition.
1. Faites glisser et déposez le composant **[!UICONTROL Conteneur de formulaires adaptatifs]** du navigateur de composants vers la page Sites. Un espace est alors créé sur la page pour le formulaire. Vous pouvez modifier la taille de l’espace conteneur à l’aide du mode Disposition.
1. Faites glisser et déposez les composants principaux de formulaire adaptatif dans l’espace conteneur pour créer le formulaire.
1. Ajoutez le bouton Soumettre.

Ensuite, vous [définissez l’action Soumettre](#configure-submit-action-for-form) et les propriétés avancées.

### Créer un formulaire dans un fragment d’expérience {#create-an-adaptive-form-in-experience-fragment}

Vous pouvez étendre la portée de vos formulaires en les ajoutant aux fragments d’expérience AEM, ce qui permet une réutilisation directe sur plusieurs pages ou sites. Par exemple, vous pouvez inclure un formulaire d’inscription à une newsletter dans un fragment d’expérience. Vous pouvez ainsi réutiliser facilement le fragment sur plusieurs pages de votre site web, ce qui évite d’avoir à recréer le formulaire à plusieurs reprises. Toutes les mises à jour ou modifications apportées au formulaire d’inscription à la newsletter dans le fragment d’expérience sont automatiquement propagées à toutes les pages sur lesquelles elles sont utilisées. Cela simplifie le processus et garantit une expérience utilisateur fluide tout en simplifiant la gestion des formulaires de votre site web.

Pour créer un formulaire adaptatif dans un fragment d’expérience :

1. Ouvrez un fragment d’expérience.
1. Faites glisser et déposez le composant de **[!UICONTROL conteneur de formulaires adaptatifs]** du navigateur de composants sur le fragment d’expérience.
1. Faites glisser et déposez les composants principaux de formulaire adaptatif dans l’espace conteneur du fragment d’expérience pour créer le formulaire.
1. Ajoutez le bouton Soumettre.

Ensuite, vous [définissez l’action de soumission](#configure-submit-action-for-form) et les propriétés avancées.

### Convertir un formulaire adaptatif dans une page AEM Sites en fragment d’expérience {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Vous pouvez convertir un formulaire adaptatif existant dans un éditeur de page d’AEM Sites en fragment d’expérience afin de réutiliser le formulaire sur plusieurs pages ou sites.

Pour convertir un formulaire adaptatif dans une page AEM Sites en fragment d’expérience :

1. Ouvrez la page AEM Sites contenant le formulaire adaptatif (dans le composant de conteneur de formulaires adaptatifs) en mode d’édition.
1. Ouvrez l’arborescence de contenu, puis sélectionnez le **[!UICONTROL conteneur de formulaires adaptatifs]** qui héberge votre formulaire adaptatif. Une page AEM Sites peut héberger plusieurs formulaires adaptatifs. Sélectionnez donc avec soin le conteneur de formulaires adaptatifs approprié.
1. Dans la barre de menu, sélectionnez l’![icône Convertir en variation de fragment d’expérience](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg)icône Convertir en variation de frangment d’expérience.
   ![Convertir un formulaire adaptatif dans une page Sites en fragment d’expérience](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   Une boîte de dialogue pour convertir le conteneur de formulaires adaptatifs en un nouveau fragment d’expérience ou l’ajouter à un fragment d’expérience existant s’affiche
1. Dans la boîte de dialogue Convertir en variation de fragment d’expérience, définissez les valeurs des options suivantes :

   * **Action :** vous pouvez sélectionner pour créer un fragment d’expérience ou ajouter à un fragment d’expérience existant.
   * **Chemin d’accès parent :** spécifiez le chemin du dossier dans lequel héberger le fragment d’expérience. Cette option est disponible uniquement pour créer un fragment d’expérience.
   * **Modèle :** spécifiez le chemin du modèle de fragment d’expérience. Si vous ne disposez pas d’un modèle de fragment d’expérience, [créez-le](/help/sites-developing/experience-fragments.md). Cette option est disponible uniquement pour l’ajout d’un formulaire adaptatif à un fragment d’expérience existant.
   * **Titre du fragment :** spécifiez le titre du fragment d’expérience. Le titre identifie de manière unique un fragment d’expérience.


## Configuration de l’action de soumission pour le formulaire {#configure-submit-action-for-form}

L’action Envoyer vous permet de choisir la destination des données capturées via un formulaire adaptatif. Elle est déclenchée lorsqu’un utilisateur ou une utilisatrice clique sur le bouton Soumettre d’un formulaire adaptatif. Les formulaires adaptatifs incluent certaines actions de soumission prêtes à l’emploi. Vous pouvez également étendre les actions de soumission par défaut pour créer votre propre action de soumission. Pour configurer une action de soumission pour votre formulaire :

1. Ouvrez l’éditeur de page AEM ou le fragment d’expérience contenant le formulaire adaptatif.
1. Ouvrez l’arborescence de contenu, puis sélectionnez le **[!UICONTROL conteneur de formulaires adaptatifs]** qui héberge votre formulaire adaptatif. Une page AEM Sites peut héberger plusieurs formulaires adaptatifs. Sélectionnez donc avec soin le conteneur de formulaires adaptatifs approprié.
1. Cliquez sur l’icône de propriétés de conteneur de formulaires adaptatifs ![propriétés de conteneur de formulaires adaptatifs](/help/forms/using/assets/configure-icon.svg). La boîte de dialogue du conteneur de formulaires adaptatifs pour configurer les actions de soumission s’ouvre.
   ![Conteneur de formulaires adaptatifs](/help/forms/using/assets/adaptive-forms-container.png)
1. Sélectionnez et configurez une action de soumission en fonction de vos besoins. Pour plus d’informations sur les actions de soumission, voir [Action de soumission de formulaire adaptatif](configuring-submit-actions.md)


## Configuration d’un schéma ou d’un modèle de données de formulaire pour un formulaire {#configure-schema-or-data-model-for-form}

Vous pouvez utiliser le modèle de données de formulaire pour connecter un formulaire à une source de données afin d’envoyer et de recevoir des données en fonction des actions de l’utilisateur ou de l’utilisatrice. Vous pouvez également connecter un formulaire à un schéma JSON pour recevoir les données envoyées dans un format prédéfini.

Avant de connecter un formulaire à un schéma ou à un modèle de données de formulaire

* [Créer un schéma JSON et le charger dans votre environnement](adaptive-form-json-schema-form-model.md)
* [Créer un modèle de données de formulaire](create-form-data-models.md)

Pour configurer un schéma JSON ou un modèle de données de formulaire pour votre formulaire :

1. Ouvrez l’éditeur de page AEM ou le fragment d’expérience contenant le formulaire adaptatif.
1. Ouvrez l’arborescence de contenu, puis sélectionnez le **[!UICONTROL conteneur de formulaires adaptatifs]** qui héberge votre formulaire adaptatif. Une page AEM Sites peut héberger plusieurs formulaires adaptatifs. Sélectionnez donc avec soin le conteneur de formulaires adaptatifs approprié.
1. Cliquez sur l’icône de propriétés de conteneur de formulaires adaptatifs ![propriétés de conteneur de formulaires adaptatifs](/help/forms/using/assets/configure-icon.svg). La boîte de dialogue Conteneur de formulaires adaptatifs pour configurer les modèles de données s’ouvre.
   ![Conteneur de formulaires adaptatifs de modèle de données de formulaire](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. Sélectionnez et configurez un schéma JSON ou un modèle de données de formulaire, en fonction de vos besoins. Pour plus d’informations sur les actions de soumission, voir [Action de soumission de formulaire adaptatif](configuring-submit-actions.md).

   * Lorsque vous sélectionnez l’option **[!UICONTROL Modèle de formulaire]**, utilisez l’option **[!UICONTROL Sélectionner un modèle de données de formulaire]** pour sélectionner un modèle de données de formulaire préconfiguré.
   * Lorsque vous sélectionnez l’option **[!UICONTROL Schéma]**, utilisez l’option **[!UICONTROL Schéma]** pour sélectionner un schéma JSON pour votre formulaire.

1. Cliquez sur **[!UICONTROL Terminé]**.

## Configurer un service de préremplissage pour un formulaire {#configure-prefill-service-for-form}

Vous pouvez utiliser le service de préremplissage pour remplir automatiquement les champs d’un formulaire adaptatif à l’aide de données existantes. Lorsqu’un utilisateur ou une utilisatrice ouvre un formulaire, les valeurs de ces champs sont préremplies. Vous pouvez effectuer les actions suivantes :

* [Créer un service de préremplissage personnalisé](prepopulate-adaptive-form-fields.md)
* [Utiliser le service de préremplissage de de modèle de données de formulaire](#fdm-prefill-service)

### Utiliser le service de préremplissage de modèle de données de formulaire {#fdm-prefill-service}

Vous pouvez utiliser le service de préremplissage de modèle de données de formulaire pour préremplir les champs d’un formulaire à l’aide d’un modèle de données de formulaire configuré. Le service de préremplissage de modèle de données de formulaire utilise la méthode [Obtenir le service du modèle de données de formulaire configuré](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) pour récupérer des données. Pour utiliser le service de préremplissage de modèle de données de formulaire pour un formulaire adaptatif :

1. Ouvrez l’éditeur de page AEM ou le fragment d’expérience contenant le formulaire adaptatif.
1. Ouvrez l’arborescence de contenu, puis sélectionnez le **[!UICONTROL conteneur de formulaires adaptatifs]** qui héberge votre formulaire adaptatif. Une page AEM Sites peut héberger plusieurs formulaires adaptatifs. Sélectionnez donc avec soin le conteneur de formulaires adaptatifs approprié.
1. Cliquez sur l’icône de propriétés de conteneur de formulaires adaptatifs ![propriétés de conteneur de formulaires adaptatifs](/help/forms/using/assets/configure-icon.svg). La boîte de dialogue Conteneur de formulaires adaptatifs pour configurer les modèles de données s’ouvre.
   ![Service de préremplissage de formulaire de l’éditeur de page aem sites](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. Sélectionnez un modèle de données de formulaire. Ouvrez l’onglet **[!UICONTROL De base]**. Dans le service de préremplissage, sélectionnez **[!UICONTROL Service de préremplissage de brouillon du Portail Formulaires]**.
1. Cliquez sur **[!UICONTROL Terminé]**.

## Rediriger la personne utilisatrice vers une nouvelle personne utilisatrice lors de l’envoi du formulaire ou afficher un message de remerciement

Lors de l’envoi d’un formulaire, vous pouvez rediriger la personne utilisatrice vers une autre page web ou vers un message. Pour rediriger la personne utilisatrice ou configurer le message de remerciement :

1. Ouvrez l’éditeur de page AEM ou le fragment d’expérience contenant le formulaire adaptatif.
1. Ouvrez l’arborescence de contenu, puis sélectionnez le **[!UICONTROL conteneur de formulaires adaptatifs]** qui héberge votre formulaire adaptatif. Une page AEM Sites peut héberger plusieurs formulaires adaptatifs. Sélectionnez donc avec soin le conteneur de formulaires adaptatifs approprié.
1. Cliquez sur l’icône de propriétés de conteneur de formulaires adaptatifs ![propriétés de conteneur de formulaires adaptatifs](/help/forms/using/assets/configure-icon.svg). La boîte de dialogue Conteneur de formulaires adaptatifs pour configurer les modèles de données s’ouvre.
1. Ouvrez l’onglet **[!UICONTROL Soumission]**.

   * Pour configurer une URL de redirection, pour l’option Lors de l’envoi, sélectionnez l’option Rediriger vers l’URL, puis fournissez une adresse absolue, une URL de redirection ou le chemin relatif d’une page AEM Sites.

   * Pour configurer un message de remerciement ou personnalisé, sélectionnez l’option Afficher le message et écrivez un message dans la zone Contenu du message pour l’option Lors de l’envoi. Il s’agit d’une zone de texte enrichi. Vous pouvez utiliser l’option Plein écran pour afficher tous les éléments de texte enrichi disponibles.

## Voir également {#see-also}

* [Création d’un formulaire adaptatif autonome basé sur des composants principaux](/help/forms/using/create-an-adaptive-form-core-components.md)
* [Créer un style ou des thèmes pour vos formulaires](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
