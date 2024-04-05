---
title: Comment intégrer AEM Forms à Adobe Analytics ?
description: AEM Forms s’intègre à Adobe Analytics, ce qui permet la capture et le suivi des mesures de performances des formulaires que vous avez publiés.
docset: aem65
exl-id: 030fe9f2-cd41-4290-b8a6-2f9ade6b5789
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1762'
ht-degree: 100%

---

# Analytics avec [!DNL Adobe Launch]. {#analyticsusingadobelaunch}

AEM Forms s’intègre à [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=fr), ce qui permet la capture et le suivi des mesures de performances des formulaires que vous avez publiés. L’analyse de ces mesures a pour objectif de permettre aux utilisateurs professionnels d’obtenir des informations sur le comportement des utilisateurs finaux et d’optimiser l’expérience de capture des données. Vous pouvez capturer et suivre le comportement des utilisateurs connectés et non connectés (anonymes) à l’aide d’Adobe Analytics pour formulaires adaptatifs.

Vous pouvez également effectuer des analyses à l’aide de Cloud Service Framework. Pour plus d’informations sur l’intégration d’AEM Forms à Cloud Service Framework, voir [Analytics à l’aide de Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md). L’avantage principal de l’utilisation d’Adobe Launch par rapport à Analytics avec Cloud Service Framework est que vous pouvez également définir des événements personnalisés, en plus de ces événements prêts à l’emploi. Les événements personnalisés sont définis à l’aide de l’éditeur de règles ou de bibliothèques clientes et sont mappés aux événements dans [!DNL Adobe Analytics].

Après avoir exécuté les actions mentionnées dans cet article, vous pouvez configurer et afficher des rapports dans [!DNL Adobe Analytics], comme illustré dans la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Utilisez [!DNL Adobe Analytics] pour identifier les schémas d’interaction et les problèmes auxquels sont confrontés les utilisateurs lorsqu’ils utilisent des formulaires adaptatifs. La version prête à l’emploi d’[!DNL Adobe Analytics] permet de réaliser le suivi et d’enregistrer les informations sur les évènements suivants :

* **Rendus** : nombre de fois qu’un formulaire est ouvert.

* **Envois** : nombre de fois qu’un formulaire est envoyé.

* **Abandons** : nombre de fois que les utilisateurs ont quitté le site sans remplir le formulaire.

* **Erreur** : nombre d’erreurs survenues sur le panneau et sur les champs du panneau.

* **Aide** : nombre de fois qu’un utilisateur ouvre l’aide d’un panneau et des champs du panneau.

* **Visites de champ** : nombre de visites d’un utilisateur dans un champ du formulaire.

* **Enregistrements** : nombre de fois où les utilisateurs enregistrent un formulaire sur le Portail Formulaires.

Outre ces événements prêts à l’emploi, vous pouvez également définir des événements personnalisés.

La figure suivante illustre les actions que vous devez effectuer avant d’afficher des rapports dans [!DNL Adobe Analytics] :

![Présentation d’Analytics](/help/forms/using/assets/analyticsworkflow.png)

## 1. Configuration d’[!DNL Adobe Analytics] {#Configure-adobe-analytics}

Avant de configurer [!DNL Adobe Analytics], créez :

* un Adobe ID pour vous connecter à [Adobe Experience Cloud](https://experience.adobe.com/#/home) ;
* une [suite de rapports](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=fr).


### Installation d’extensions AEM Forms et [!DNL Adobe Analytics] {#install-extensions}

Suivez les étapes suivantes pour configurer les extensions AEM Forms et [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=fr) :

1. Connectez-vous à Adobe Experience Cloud et sélectionnez un nom approprié pour l’entreprise.

1. Sélectionnez **[!UICONTROL Launch/Collecte de données]** et **[!UICONTROL Accéder à Launch/Collecte de données]**.

1. Sélectionnez **[!UICONTROL Nouvelle propriété]** et spécifiez un nom pour la configuration.

1. Indiquez un nom de domaine et sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la propriété.

1. Sélectionnez le nom de configuration disponible dans la liste des propriétés de balise.

1. Dans la section **[!UICONTROL Création]**, sélectionnez **[!UICONTROL Extensions]**.

1. Sélectionnez **[!UICONTROL Catalogue]** puis **[!UICONTROL Installer]** pour l’extension **[!UICONTROL Adobe Experience Manager Forms]**. **[!UICONTROL Adobe Experience Manager Forms]** s’affiche dans la liste des extensions installées disponibles dans l’onglet **Installé**.

1. Sélectionnez **[!UICONTROL Installer]** pour l’extension **[!UICONTROL Adobe Analytics]**.
1. Sélectionnez le nom de la suite de rapports dans les listes déroulantes **[!UICONTROL Suites de rapports de développement]**, **[!UICONTROL Suites de rapports d’évaluation]** et **[!UICONTROL Suites de rapports produit]** et sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer l’extension.

### Configuration d’éléments de données {#configure-data-elements}

Vous pouvez sélectionner l’un de ces éléments de données configurés dans une règle créée pour un événement. Lorsqu’un événement se produit sur un formulaire adaptatif, AEM Forms envoie ces éléments de données à [!DNL Adobe Analytics].

Après avoir installé l’extension **[!UICONTROL Adobe Experience Manager Forms]**, vous pouvez créer les éléments de données suivants :

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Procédez comme suit pour configurer les élément de données :

1. Dans la section **[!UICONTROL Création]**, sélectionnez **[!UICONTROL Éléments de données]**.

1. Sélectionnez **[!UICONTROL Créer un élément de données]**.

1. Spécifiez un nom pour l’élément de données. Par exemple, « Titre du formulaire » pour le type d’élément de données FormTitle.

1. Spécifiez **[!UICONTROL Adobe Experience Manager Forms]** comme nom d’extension.

1. Sélectionnez le **[!UICONTROL Type d’élément de données]**.

1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer l’élément de données.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configuration de règles {#configure-rules}

Suivez les étapes suivantes pour créer des règles basées sur l’extension **[!UICONTROL Adobe Experience Manager Forms]** :

1. Dans la section **[!UICONTROL Création]**, sélectionnez **[!UICONTROL Règles]**.

1. Sélectionnez **[!UICONTROL Créer une règle]**.

1. Spécifiez un nom pour la règle. Par exemple, Envoi de formulaire pour enregistrer les envois de formulaire.

1. Dans la section **[!UICONTROL Événements]**, sélectionnez **[!UICONTROL Ajouter]**.

1. Spécifiez **[!UICONTROL Adobe Experience Manager Forms]** comme nom d’extension.

1. Sélectionnez le type d’événement. L’entrée du champ **[!UICONTROL Nom]** est renseignée automatiquement en fonction du type d’événement sélectionné.

1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour enregistrer l’événement.

1. Dans la section **[!UICONTROL Actions]**, sélectionnez **[!UICONTROL Ajouter]**.

1. Spécifiez **[!UICONTROL Adobe Analytics]** comme nom d’extension.

1. Sélectionnez **[!UICONTROL Définir les variables]** comme type d’action. Les options disponibles dans la liste déroulante sont les suivantes :

   * **[!UICONTROL Définir les variables]** : utilisez ce type d’action pour définir le type d’événement pour lequel les éléments de données sélectionnés sont envoyés d’AEM Forms vers [!DNL Adobe Analytics].

   * **[!UICONTROL Envoyer la balise]** : utilisez ce type d’action pour envoyer des données d’AEM Forms vers [!DNL Adobe Analytics].

   * **[!UICONTROL Effacer les variables]** : utilisez ce type d’action pour effacer le journal de données afin que l’événement ne s’enregistre qu’une seule fois dans [!DNL Adobe Analytics].

     L’approche recommandée consiste à utiliser le type d’action **[!UICONTROL Définir les variables]** pour configurer l’événement et les éléments de données, puis à utiliser **[!UICONTROL Envoyer la balise]** pour envoyer des données, et **[!UICONTROL Effacer les variables]** pour effacer le suivi des données.

1. Dans la section **[!UICONTROL Props]**, mappez les options de suite de rapports disponibles dans la liste déroulante avec les éléments de données définis à l’aide de la commande [Configurer les éléments de données](#configure-data-elements).

   Par exemple, pour envoyer l’élément de données **Titre du formulaire** d’AEM Forms à [!DNL Adobe Analytics] lorsque vous envoyez un formulaire suivez les étapes suivantes :
   1. Dans la section **[!UICONTROL Props]**, sélectionnez une prop pour le titre du formulaire disponible dans la suite de rapports, puis sélectionnez ![Icône de la base de données](/help/forms/using/assets/database-icon.svg) pour la mapper au titre du formulaire créé dans [Configuration des éléments de données](#configure-data-elements).

      ![define-props](/help/forms/using/assets/define-props.png)

   1. Sélectionnez **[!UICONTROL Ajouter]** pour ajouter d’autres éléments de données à la liste.

1. Dans la section **[!UICONTROL Événements]**, sélectionnez un événement parmi les options disponibles dans la suite de rapports, puis cliquez sur **[!UICONTROL Conserver les modifications]**.

1. Dans la section **[!UICONTROL Actions]**, sélectionnez + et indiquez **[!UICONTROL Adobe Analytics]** comme nom d’extension.

1. Sélectionnez **[!UICONTROL Envoyer la balise]** comme type d’action. Dans le volet de droite, sélectionnez **[!UICONTROL s.t()]** pour envoyer des données à [!DNL Adobe Analytics] et les traiter comme une page vue ou **[!UICONTROL s.tl()]** pour envoyer des données à [!DNL Adobe Analytics] et ne pas les traiter comme une page vue. Sélectionnez **[!UICONTROL Conserver les modifications]**.

1. Dans la section **[!UICONTROL Actions]**, sélectionnez + et indiquez **[!UICONTROL Adobe Analytics]** comme nom d’extension.

1. Sélectionnez **[!UICONTROL Effacer les variables]** comme type d’action. Sélectionnez **[!UICONTROL Conserver les modifications]**. Après avoir effectué ces étapes, la section **[!UICONTROL Actions]** s’affiche comme suit :
   ![Configuration des actions](/help/forms/using/assets/actions-config.png)

   Personnalisez la section **[!UICONTROL Actions]** en fonction de vos besoins. Par exemple, vous pouvez définir deux étapes **Envoyer la balise** dans un flux Actions pour envoyer des données à [!DNL Adobe Analytics] et les traiter comme une page vue en une seule étape et envoyer des données à [!DNL Adobe Analytics] sans les traiter comme une page vue lors de la seconde étape.

   ![Configuration des actions](/help/forms/using/assets/actions-config-2.png)

1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle.

   Vous pouvez créer des règles pour tous les types d’événements, tels que : Abandons, Erreurs, Visites de champ, Aide, Rendus, Enregistrements et Envois.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flux de publication {#publish-flow}

Après avoir créé les éléments de données et les avoir utilisés dans des règles, publiez la configuration pour collecter les données de formulaire dans [!DNL Adobe Analytics].

Pour publier la configuration, procédez comme suit :

1. Dans la section **[!UICONTROL Publication]**, sélectionnez **[!UICONTROL Flux de publication]**.

1. Sélectionnez **[!UICONTROL Ajouter la bibliothèque]**, spécifiez un nom et sélectionnez l’environnement de la bibliothèque.

1. Sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**, puis **[!UICONTROL Enregistrer et créer dans le développement]**.

1. Dans la section **[!UICONTROL Développement]**, sélectionnez ![Autres options](/help/forms/using/assets/more-options-icon.svg), puis **[!UICONTROL Approuver et publier dans la production]**.

1. Confirmez les modifications et le flux de publication s’affiche bientôt dans la section **[!UICONTROL Publié]**.

![Flux de publication](/help/forms/using/assets/publish-flow.png)

## 2. Configuration d’AEM Forms {#configure-aem-forms}

Avant de créer une configuration Adobe Launch, créez une [configuration Adobe IMS à l’aide d’Adobe Launch en tant que solution cloud](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=fr).

### Création d’une configuration Adobe Launch {#create-adobe-launch-configuration}

Pour créer une configuration Adobe Launch, procédez comme suit :

1. Dans l’instance d’auteur AEM Forms, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Configurations d’Adobe Launch]**.

1. Sélectionnez un dossier pour créer la configuration et sélectionnez **[!UICONTROL Créer]**.

1. Indiquez un titre pour la configuration dans le champ **[!UICONTROL Titre]**.

1. Sélectionnez la [configuration Adobe IMS associée](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=fr).

1. Sélectionnez le nom de la société utilisée lors de la [configuration d’Adobe Analytics](#Configure-adobe-analytics).

1. Sélectionnez le nom de la propriété créée lors de la [configuration d’Adobe Analytics](#install-extensions).

1. Sélectionnez **[!UICONTROL Enregistrer et fermer]**.

1. Publiez la configuration.

### Activation d’[!DNL Adobe Analytics] pour un formulaire adaptatif {#enable-analytics-adaptive-form}

Pour utiliser la configuration [!DNL Adobe Launch] dans un formulaire adaptatif existant, suivez les étapes suivantes :

1. Dans l’instance d’auteur AEM Forms, accédez à **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formulaires]** > **[!UICONTROL Formulaires et documents]**.
1. Sélectionnez le formulaire adaptatif, puis sélectionnez **[!UICONTROL Propriétés]**.
1. Dans l’onglet **[!UICONTROL De base]**, sélectionnez le [conteneur de configuration](#create-adobe-launch-configuration) utilisé lors de la création de la configuration Adobe Launch.
1. Sélectionnez **[!UICONTROL Enregistrer et fermer]**. Le formulaire adaptatif est activé pour [!DNL Adobe Analytics].
1. Publication du formulaire.

Après avoir activé [!DNL Adobe Analytics] pour un formulaire adaptatif, vous pouvez [valider](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=fr#validate-the-page-view-beacon) s’il existe un flux approprié d’événement de données entre AEM Forms et [!DNL Adobe Analytics]. L’intégration d’AEM Forms avec Adobe Analytics est terminée. Vous pouvez désormais [configurer et afficher des rapports dans Adobe Analytics](#view-reports-adobe-analytics).

>[!NOTE]
>Dans le cas contraire, si les fonctionnalités [Analytics à l’aide de Cloud Service Framework](/help/forms/using/configure-analytics-forms-documents.md) et **Analytics avec Adobe Launch** sont activées simultanément, **Analytics avec Adobe Launch** est prioritaire.
> 

### Création de règles pour la capture d’événements personnalisés (facultatif) {#capture-custom-events}

Créez des règles sur des champs spécifiques d’un formulaire adaptatif à l’aide de l’éditeur de règles pour envoyer des données Analytics d’un formulaire adaptatif à [!DNL Adobe Analytics].

Dans un processus en deux étapes, vous définissez une règle sur un champ d’un formulaire adaptatif. La règle distribue un événement. Le nom de l’événement est mappé à un événement de capture personnalisé dans Adobe Launch.

Pour créer des règles à l’aide de l’éditeur de règles dans un formulaire adaptatif :

1. Sélectionnez le champ et sélectionnez ![Éditeur de règles](/help/forms/using/assets/rule-editor-icon.svg) pour ouvrir la page de l’éditeur de règles.
1. Définissez une condition dans la section [!UICONTROL Lorsque] de la règle.
1. Dans la section [!UICONTROL Alors] de la règle, sélectionnez **[!UICONTROL Distribuer l’événement]** dans la liste déroulante **[!UICONTROL Sélectionner une action]**.
1. Indiquez le nom de l’événement dans le champ **[!UICONTROL Saisir le nom de l’événement]**.

Par exemple, si la date de naissance est antérieure à une certaine date, AEM Forms distribue l’événement **Sécurité**.

![Distribuer l’événement](/help/forms/using/assets/security-event.png)

Pour mapper l’événement à un événement de capture personnalisé dans [!DNL Adobe Analytics] :

1. [Créez une règle](#configure-rules).

1. Dans la section **[!UICONTROL Événements]**, sélectionnez **[!UICONTROL Ajouter]**.

1. Spécifiez **[!UICONTROL Adobe Experience Manager Forms]** comme nom d’extension.

1. Sélectionnez **[!UICONTROL Capturer un événement personnalisé]** dans la liste déroulante **[!UICONTROL Type d’événement]**.

1. Indiquez le nom de l’événement que vous avez spécifié à l’étape 4 lors de la création d’une règle à l’aide de l’éditeur de règles.

1. Sélectionnez **Conserver les modifications** et effectuez le reste des actions spécifiées dans [Configurer les règles](#configure-rules).

## 3. Configuration et affichage de rapports dans [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Après avoir configuré un formulaire adaptatif pour envoyer des données d’événement dans [!DNL Adobe Analytics], vous pouvez commencer à afficher les rapports dans [!DNL Adobe Analytics] :

1. Sélectionnez ![Sélectionner le produit](/help/forms/using/assets/select-analytics.png) et **[!UICONTROL Analytics]**.

1. Sélectionnez **[!UICONTROL Créer un projet]** et **[!UICONTROL Projet vierge]**.

1. Sélectionnez le nom de la suite de rapports dans la liste déroulante en haut à droite de la forme libre.

1. Spécifiez **Titre du formulaire** dans le texte **[!UICONTROL Rechercher des éléments de dimensions]** pour afficher tous les titres du formulaire.

1. Déposez le titre du formulaire adaptatif dans la zone de texte **[!UICONTROL Déposez un segment ici (ou tout autre composant)]**.

1. Dans la section **[!UICONTROL Mesures]**, déposez les événements à suivre dans la zone de texte **[!UICONTROL Déposez une mesure ici (ou tout autre composant)]**.

1. Sélectionnez ![Visualisations](/help/forms/using/assets/visualization-icon.svg) et déposez un type de graphique dans la section Structure libre. De même, vous pouvez ajouter plusieurs types de graphique à la section Structure libre.

1. Appuyez sur les touches Ctrl+S et spécifiez un nom pour enregistrer le projet.

Pour obtenir des informations détaillées sur l’affichage des rapports d’analyse Forms, voir [Affichage et compréhension des rapports d’analyse d’AEM Forms](../../forms/using/view-understand-aem-forms-analytics-reports.md).
