---
title: Configuration du balisage des ressources à l’aide du service de contenu dynamique
description: Découvrez comment configurer le balisage intelligent et le balisage intelligent amélioré dans  [!DNL Adobe Experience Manager] à l’aide du service de contenu dynamique.
contentOwner: AG
role: Admin
feature: Tagging,Smart Tags
exl-id: 9f68804f-ba15-4f83-ab1b-c249424b1396
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '2227'
ht-degree: 100%

---

# Préparation de [!DNL Assets] pour le balisage intelligent {#configure-asset-tagging-using-the-smart-content-service}

Avant de commencer à baliser vos ressources à l’aide des services de contenu dynamique, intégrez [!DNL Experience Manager Assets] à l’Adobe Developer Console pour tirer parti du service dynamique d’[!DNL Adobe Sensei]. Une fois configuré, entraînez le service à l’aide de quelques images et d’une balise.

>[!NOTE]
>
>* Les services de contenu intelligent ne sont plus disponibles pour les nouveaux clients On-Premise [!DNL Experience Manager Assets]. Les clients On-Premise existants, pour lesquels cette fonctionnalité est déjà activée, peuvent continuer à utiliser les services de contenu intelligent.
>* Les services de contenu intelligent sont disponibles pour les clients Managed Services [!DNL Experience Manager Assets], pour lesquels cette fonctionnalité est déjà activée.
>* Les nouveaux clients Managed Services [!DNL Experience Manager Assets] peuvent suivre les instructions mentionnées dans cet article pour configurer les services de contenu intelligent.

Avant d’utiliser le service de contenu dynamique, vérifiez les points suivants :

* [Intégration à la console Adobe Developer](#integrate-adobe-io).
* [Entraînement du service de contenu dynamique](#training-the-smart-content-service)

* Installez le dernier pack de services [[!DNL Experience Manager] ](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=fr).

## Intégration à la console Adobe Developer {#integrate-adobe-io}

Lors de l’intégration à la console Adobe Developer, le serveur [!DNL Experience Manager] authentifie vos informations d’identification de service auprès de la passerelle de la console Adobe Developer avant de transférer votre demande au service de contenu dynamique. Pour l’intégration, vous avez besoin d’un compte Adobe ID disposant de droits d’administrateur pour l’organisation et d’une licence Smart Content Service achetée et activée pour votre organisation.

Pour configurer le service de contenu dynamique, procédez comme suit :

1. Pour générer une clé publique, [Créez une configuration de service de contenu dynamique](#obtain-public-certificate) dans [!DNL Experience Manager]. [Obtenez un certificat public](#obtain-public-certificate) pour l’intégration d’OAuth.

1. [Créez une intégration dans Adobe Developer Console](#create-adobe-i-o-integration) et chargez la clé publique générée.

1. [Configurez votre déploiement](#configure-smart-content-service) en utilisant la clé API et d’autres informations d’identification de la console Adobe Developer.

1. [Testez la configuration](#validate-the-configuration).

1. Facultativement, [activez le balisage automatique lors du chargement des ressources](#enable-smart-tagging-in-the-update-asset-workflow-optional).

### Obtention d’un certificat public en créant la configuration du service de contenu dynamique {#obtain-public-certificate}

Un certificat public permet d’authentifier votre profil sur Adobe Developer Console.

1. Dans l’interface utilisateur [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Services cloud hérités]**.

1. Dans la page Services cloud, cliquez sur **[!UICONTROL Configurer maintenant]** sous **[!UICONTROL Ressources – Balises intelligentes]**.

1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, spécifiez un titre et un nom pour la configuration de balises intelligentes. Cliquez sur **[!UICONTROL Créer]**.

1. Dans la boîte de dialogue **[!UICONTROL Service de contenu dynamique AEM]**, utilisez les valeurs suivantes :

   **[!UICONTROL URL du service]** : `https://smartcontent.adobe.io/<region where your Experience Manager author instance is hosted>`

   Par exemple, `https://smartcontent.adobe.io/apac`. Vous pouvez indiquer `na`, `emea`, ou `apac` comme les régions où votre instance d’auteur Experience Manager est hébergée.

   >[!NOTE]
   >
   >Si le service géré Experience Manager est mis en service avant le 1er septembre 2022, utilisez l’URL de service suivante :
   >`https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Serveur d’autorisation]** : `https://ims-na1.adobelogin.com`

   Laissez les autres champs vides pour l’instant (pour les remplir ultérieurement). Cliquez sur **[!UICONTROL OK]**.

   ![Boîte de dialogue Service de contenu dynamique Experience Manager pour fournir une URL de service de contenu](assets/aem_scs.png)


   *Image : boîte de dialogue Service de contenu dynamique pour fournir une URL de service de contenu*

   >[!NOTE]
   >
   >L’URL fournie en tant qu’[!UICONTROL URL de service] n’est pas accessible via le navigateur et génère un message d’erreur 404. La configuration fonctionne correctement avec la même valeur que le paramètre [!UICONTROL URL de service]. Pour connaître le statut général du service et le planning de maintenance, consultez [https://status.adobe.com](https://status.adobe.com).

1. Cliquez sur **[!UICONTROL Télécharger le certificat public pour l’intégration OAuth]** et téléchargez le fichier de certificat public `AEM-SmartTags.crt`.

   ![Représentation des paramètres créés pour le service de balisage intelligent](assets/smart-tags-download-public-cert.png)


   *Image : paramètres du service de balisage intelligent.*

#### Reconfiguration quand un certificat atteint sa date d’expiration {#certrenew}

Lorsque le certificat expire, il n’est plus approuvé. Vous ne pouvez pas renouveler un certificat ayant expiré. Pour ajouter un certificat, procédez comme suit.

1. Connectez-vous en tant qu’administrateur à votre déploiement [!DNL Experience Manager]. Cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.

1. Recherchez et cliquez sur l’utilisateur **[!UICONTROL dam-update-service]**. Cliquez sur l’onglet **[!UICONTROL Keystore]**.

1. Supprimez le fichier de stockage de clés **[!UICONTROL similaritysearch]** existant avec le certificat arrivé à expiration. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   ![Suppression d’une entrée de recherche de similarité existante dans le Keystore pour ajouter un nouveau certificat de sécurité](assets/smarttags_delete_similaritysearch_keystore.png)


   *Schéma : suppression d’une entrée `similaritysearch` existante dans le Keystore pour ajouter un certificat de sécurité.*

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Ancienne version de Cloud Services]**. Cliquez sur **[!UICONTROL Balises dynamiques de ressources]** > **[!UICONTROL Afficher la configuration]** > **[!UICONTROL Configurations disponibles]**. Cliquez sur la configuration requise.

1. Pour télécharger un certificat public, cliquez sur **[!UICONTROL Télécharger le certificat public pour l’intégration OAuth]**.

1. Accédez à [https://console.adobe.io](https://console.adobe.io) et naviguez vers les services de contenu dynamique existants sur la page **[!UICONTROL Intégrations]**. Téléchargez le nouveau certificat. Pour plus d’informations, consultez les instructions contenues dans [Création d’une intégration dans Adobe Developer Console](#create-adobe-i-o-integration).

### Création de l’intégration de la console Adobe Developer {#create-adobe-i-o-integration}

Pour utiliser les API de service de contenu dynamique, créez une intégration dans la console Adobe Developer afin d’obtenir la [!UICONTROL Clé API] (générée dans le champ [!UICONTROL ID CLIENT] de l’intégration de la console Adobe Developer), [!UICONTROL ID DE COMPTE TECHNIQUE], [!UICONTROL ID D’ORGANISATION] et [!UICONTROL SECRET CLIENT] pour les [!UICONTROL Paramètres du service de balisage intelligent des ressources] de la configuration cloud dans [!DNL Experience Manager].

1. Accédez à l’URL [https://console.adobe.io](https://console.adobe.io/) dans un navigateur. Sélectionnez le compte approprié et vérifiez que le rôle d’organisation associé est administrateur système.

1. Créez un projet portant le nom de votre choix. Cliquez sur **[!UICONTROL Add API]** (Ajouter une API).

1. Sur la page **[!UICONTROL Add API]**, sélectionnez **[!UICONTROL Experience Cloud]** puis **[!UICONTROL Smart Content]** (Contenu dynamique). Cliquez sur **[!UICONTROL Next]** (Suivant).

1. Sélectionnez **[!UICONTROL Upload your public key]** (Charger votre clé publique). Fournissez le fichier de certificat téléchargé depuis [!DNL Experience Manager]. Le message [!UICONTROL Public key(s) uploaded successfully] (La ou les clés publiques ont été chargées) s’affiche. Cliquez sur **[!UICONTROL Next]** (Suivant).

   La page [!UICONTROL Créer des informations d’identification de compte de service (JWT)] affiche la clé publique du compte de service.

1. Cliquez sur **[!UICONTROL Next]** (Suivant).

1. Dans la page **[!UICONTROL Select product profiles]** (Sélectionner les profils de produits), sélectionnez **[!UICONTROL Smart Content Services]** (Services de contenu dynamique). Cliquez sur **[!UICONTROL Enregistrer l’API configurée]**. 

   Une page affiche davantage d’informations sur la configuration. Laissez cette page ouverte pour copier et ajouter ces valeurs dans les [!UICONTROL Paramètres du service de balisage intelligent des ressources] de la configuration cloud dans [!DNL Experience Manager] pour configurer des balises intelligentes.

   ![Dans l’onglet Aperçu, vous pouvez consulter les informations fournies pour l’intégration.](assets/integration_details.png)


   *Image : détails de l’intégration dans la console Adobe Developer*

### Configuration du service de contenu dynamique {#configure-smart-content-service}

Pour configurer l’intégration, utilisez les valeurs d’[!UICONTROL ID DE COMPTE TECHNIQUE], d’[!UICONTROL ID D’ORGANISATION], de [!UICONTROL SECRET CLIENT] et d’[!UICONTROL ID CLIENT] à partir de l’intégration de la console Adobe Developer. La création d’une configuration cloud de balises intelligentes permet d’authentifier les demandes d’API provenant du déploiement [!DNL Experience Manager].

1. [!DNL Experience Manager]Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Services cloud hérités]** pour ouvrir la console [!UICONTROL Services cloud].

1. Sous les **[!UICONTROL balises intelligentes des ressources]**, ouvrez la configuration créée ci-dessus. Sur la page des paramètres du service, cliquez sur **[!UICONTROL Modifier]**.

1. Dans la boîte de dialogue **[!UICONTROL Service de contenu dynamique AEM]**, utilisez les valeurs préremplies pour les champs **[!UICONTROL URL de service]** et **[!UICONTROL Serveur d’autorisation]**.

1. Pour les champs [!UICONTROL Clé Api], [!UICONTROL Identifiant du compte technique], [!UICONTROL ID d’organisation] et [!UICONTROL Secret du client], copiez et utilisez les valeurs suivantes générées dans [Intégration de la console Adobe Developer](#create-adobe-i-o-integration).

   | [!UICONTROL Paramètres du service de balisage intelligent des ressources] | Champs d’intégration d’[!DNL Adobe Developer Console] |
   |--- |--- |
   | [!UICONTROL Clé API] | [!UICONTROL ID CLIENT] |
   | [!UICONTROL Identifiant de compte technique] | [!UICONTROL ID DE COMPTE TECHNIQUE] |
   | [!UICONTROL Identifiant d’organisation] | [!UICONTROL ID D’ORGANISATION] |
   | [!UICONTROL Secret client] | [!UICONTROL SECRET CLIENT] |

### Validation de la configuration {#validate-the-configuration}

Une fois la configuration terminée, vous pouvez utiliser un MBean JMX pour valider la configuration. Pour procéder à la validation, suivez ces étapes.

1. Accédez à votre serveur [!DNL Experience Manager] sur `https://[aem_server]:[port]`.

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]** pour ouvrir la console OSGi. Cliquez sur **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Cliquez sur `com.day.cq.dam.similaritysearch.internal.impl`. Les **[!UICONTROL tâches relatives à SimilaritySearch]** s’ouvrent alors.

1. Cliquez sur `validateConfigs()`. Dans la boîte de dialogue **[!UICONTROL Valider les configurations]**, cliquez sur **[!UICONTROL Invoquer]**.

Le résultat de la validation s’affiche dans la même boîte de dialogue.

### Activation du balisage intelligent dans le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques] (Facultatif) {#enable-smart-tagging-in-the-update-asset-workflow-optional}

1. Dans [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.

1. Sur la page **[!UICONTROL Modèles de processus]**, sélectionnez le modèle de processus **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques (DAM)]**.

1. Cliquez sur **[!UICONTROL Modifier]** dans la barre d’outils.

1. Développez le panneau latéral pour afficher les étapes. Faites glisser l’étape **[!UICONTROL Balisage intelligent de la ressource]** disponible dans la section Processus de DAM (gestion des actifs numériques) et placez-la après l’étape **[!UICONTROL Miniatures des processus]**.

   ![Ajout de l’étape Balisage intelligent de la ressource après l’étape Miniatures des processus dans le processus Ressources de mise à jour de gestion des actifs numériques (DAM)](assets/smart-tag-in-dam-update-asset-workflow.png)

   *Image : ajout de l’étape de balisage intelligent de la ressource après l’étape Miniatures des processus dans le workflow [!UICONTROL Ressources de mise à jour de la gestion des ressources numériques]*.

1. Ouvrez l’étape en mode édition. Dans **[!UICONTROL Paramètres avancés]**, vérifiez que l’option **[!UICONTROL Avance du gestionnaire]** est sélectionnée.

   ![Configuration du workflow de Ressource de mise à jour de la gestion des ressources numériques et ajout de l’étape de balisage intelligent](assets/smart-tag-step-properties-workflow1.png)


   *Image : configuration du workflow de Ressource de mise à jour de la gestion des ressources numériques et ajout de l’étape de balisage intelligent*

1. Dans l’onglet **[!UICONTROL Arguments]**, sélectionnez **[!UICONTROL Ignorer les erreurs]** si vous souhaitez que le workflow se termine même si l’étape de balisage automatique échoue.

   ![Configuration du workflow de Ressource de mise à jour de la gestion des ressources numériques pour ajouter l’étape de balisage intelligent et sélectionner l’avance du gestionnaire](assets/smart-tag-step-properties-workflow2.png)


   *Image : configuration du workflow de Ressource de mise à jour de la gestion des ressources numériques pour ajouter l’étape de balisage intelligent et sélectionner l’avance du gestionnaire*

   Pour baliser les ressources lors de leur chargement, et ce, que le balisage intelligent soit activé ou non dans les dossiers, cochez la case **[!UICONTROL Ignorer l’indicateur de balise intelligente]**.

   ![Configuration du workflow de Ressource de mise à jour de la gestion des ressources numériques pour ajouter l’étape de balisage intelligent et sélectionner l’indicateur de balisage intelligent](assets/smart-tag-step-properties-workflow3.png)


   *Image : configuration du workflow de Ressource de mise à jour de la gestion des ressources numériques pour ajouter l’étape de balisage intelligent et sélectionner l’indicateur de balisage intelligent*

1. Cliquez sur **[!UICONTROL OK]** pour fermer l’étape du workflow, puis enregistrez ce dernier.

## Entraînement du service de contenu dynamique {#training-the-smart-content-service}

Pour que le service de contenu dynamique reconnaisse votre taxonomie métier, exécutez-la sur une série de ressources qui incluent déjà des balises correspondant à votre entreprise. Pour baliser efficacement vos images de marque, le service de contenu dynamique requiert que les images d’entraînement respectent certaines instructions. Après l’entraînement, le service peut appliquer la même taxonomie à un ensemble de ressources similaire.

Vous pouvez entraîner le service plusieurs fois afin d’améliorer sa capacité à appliquer des balises pertinentes. Après chaque cycle d’entraînement, exécutez un workflow de balisage et vérifiez si vos ressources sont correctement balisées.

Vous pouvez entraîner le service de contenu intelligent périodiquement ou selon les besoins.

>[!NOTE]
>
>Le workflow d’entraînement s’exécute sur les dossiers uniquement.

### Instructions d’entraînement {#guidelines-for-training}

Pour un résultat optimal, les images de votre corpus d’entraînement respectent les instructions suivantes :

**Quantité et taille :** minimum 30 images par balise. Minimum 500 pixels sur le côté le plus long.

**Cohérence** : les images utilisées pour une balise spécifique sont visuellement similaires.

Par exemple, il est déconseillé d’incorporer une balise `my-party` pour toutes ces images (en situation d’entraînement), car elles ne sont pas similaires visuellement.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/coherence.png)

**Couverture** : les images d’entraînement doivent être suffisamment variées. L’idée est de fournir quelques exemples raisonnablement différents pour apprendre à Experience Manager à se concentrer sur les bons éléments. Si vous appliquez la même balise sur des images visuellement différentes, incluez au moins cinq exemples de chaque type.

Par exemple, pour la balise *mannequin-pose-tête-baissée*, incluez davantage d’images d’entraînement similaires à l’image mise en évidence ci-dessous pour que le service reconnaisse les images similaires avec plus de précision lors du balisage.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/coverage_1.png)

**Distraction/obstruction** : l’entraînement du service donne de meilleurs résultats sur les images qui ont moins de distractions (telles que des arrière-plans importants ou des objets/personnes sans lien avec le sujet principal).

Par exemple, pour la balise *chaussure-décontractée*, la seconde image n’est pas un bon candidat pour l’entraînement.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/distraction.png)

**Complétude :** si une image est admissible pour plusieurs balises, ajoutez toutes les balises applicables avant d’inclure l’image à des fins de formation. Par exemple, pour les balises telles que `raincoat` et `model-side-view`, ajoutez les deux balises sur la ressource éligible avant de l’inclure pour la formation.

![Images d’illustration donnant un exemple d’instructions d’entraînement](/help/assets/assets/do-not-localize/completeness.png)

>[!NOTE]
>
>La capacité du service de contenu dynamique à s’entraîner à partir de vos balises et à les appliquer à d’autres images dépend de la qualité des images que vous utilisez pour l’entraînement. Pour obtenir des résultats optimaux, Adobe recommande d’utiliser des images visuellement similaires afin d’entraîner le service pour chaque balise.

### Entraînement périodique {#periodic-training}

Vous pouvez activer le service de contenu dynamique afin qu’il s’entraîne périodiquement sur les ressources et les balises associées au sein d’un dossier. Ouvrez la page de [!UICONTROL Propriétés] de votre dossier de ressources, sélectionnez **[!UICONTROL Activer les balises intelligentes]** sous l’onglet **[!UICONTROL Détails]** et enregistrez les modifications.

![enable_smart_tags](assets/enable_smart_tags.png)

Lorsque cette option est sélectionnée pour un dossier, [!DNL Experience Manager] exécute automatiquement un workflow d’entraînement afin d’entraîner le service de contenu dynamique sur les ressources du dossier et leurs balises. Par défaut, le workflow d’entraînement s’exécute toutes les semaines à 00 h 30 le samedi.

### Entraînement à la demande {#on-demand-training}

Vous pouvez entraîner le service de contenu dynamique lorsque cela s’avère nécessaire à partir de la console de workflow.

1. Dans l’interface d’[!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la page **[!UICONTROL Modèles de workflow]**, sélectionnez le workflow **[!UICONTROL Entraînement des balises intelligentes]**, puis cliquez sur **[!UICONTROL Démarrer le workflow]** dans la barre d’outils.
1. Dans la boîte de dialogue **[!UICONTROL Exécuter le workflow]**, localisez le dossier de payload qui comprend les ressources balisées pour entraîner le service.
1. Indiquez le titre du workflow et ajoutez un commentaire. Cliquez ensuite sur **[!UICONTROL Exécuter]**. Les ressources et les balises sont soumises à l’entraînement.

   ![workflow_dialog](assets/workflow_dialog.png)

>[!NOTE]
>
>Une fois que les ressources figurant dans un dossier sont traitées pour l’entraînement, seules les ressources modifiées sont traitées au cours des cycles d’entraînement suivants.

### Affichage des rapports de formation {#viewing-training-reports}

Pour vérifier que le service de contenu dynamique est entraîné sur vos balises dans la série de ressources d’entraînement, examinez le rapport de workflow d’entraînement dans la console Rapports.

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rapports]**.
1. Dans la page **[!UICONTROL Rapports de ressources]**, cliquez sur **[!UICONTROL Créer]**.
1. Sélectionnez le rapport **[!UICONTROL Entraînement des balises intelligentes]**, puis cliquez sur **[!UICONTROL Suivant]** dans la barre d’outils.
1. Indiquez un titre et une description pour le rapport. Sous **[!UICONTROL Planifier le rapport]**, laissez l’option **[!UICONTROL Maintenant]** sélectionnée. Si vous souhaitez planifier le rapport pour une date ultérieure, sélectionnez **[!UICONTROL Plus tard]** et spécifiez une date et une heure. Ensuite, cliquez sur **[!UICONTROL Créer]** dans la barre d’outils.
1. Dans la page **[!UICONTROL Rapports de ressources]**, sélectionnez le rapport que vous avez généré. Pour afficher le rapport, cliquez sur **[!UICONTROL Afficher]** dans la barre d’outils.
1. Passez en revue les détails du rapport.

   Le rapport affiche le statut d’identification des balises que vous avez entraînées. La couleur verte de la colonne **[!UICONTROL État de l’entraînement]** indique que le service de contenu dynamique est entraîné pour la balise. La couleur jaune indique que le service n’est pas complètement entraîné pour une balise particulière. Dans ce cas, ajoutez d’autres images avec la balise particulière et exécutez le workflow d’entraînement pour l’entraînement complet du service sur la balise.

   Si vous ne voyez pas vos balises dans ce rapport, lancez à nouveau le workflow d’entraînement pour ces balises.

1. Pour télécharger le rapport, sélectionnez-le dans la liste, puis cliquez sur **[!UICONTROL Télécharger]** dans la barre d’outils. Le rapport est téléchargé sous la forme d’une feuille de calcul Microsoft Excel.

## Limites {#limitations}

* Le balisage intelligent amélioré est basé sur des modèles d’apprentissage d’images et de leurs balises. Ces modèles ne sont pas toujours parfaits pour identifier les balises. La version actuelle du service de contenu dynamique présente les limites suivantes :

   * Impossibilité d’identifier des différences subtiles dans les images. Par exemple, des chemises coupe droite ou ajustée.
   * Impossibilité d’identifier des balises basées sur des motifs ou des éléments minuscules d’une image. Par exemple, des logos sur des t-shirts.
   * Le balisage est pris en charge dans les paramètres régionaux gérés par [!DNL Experience Manager].

* Pour rechercher des ressources à l’aide de balises intelligentes (standard ou améliorées), utilisez la recherche de texte intégral d’[!DNL Assets]. Il n’y a aucun prédicat de recherche distinct pour les balises intelligentes.

>[!MORELIKETHIS]
>
>* [Présentation et entraînement des balises intelligentes](enhanced-smart-tags.md)
>* [Tutoriel vidéo sur les balises intelligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=fr)
