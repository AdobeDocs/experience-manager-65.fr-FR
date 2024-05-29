---
title: Configuration du balisage des ressources à l’aide du service de contenu dynamique
description: Découvrez comment configurer le balisage intelligent et le balisage intelligent amélioré dans  [!DNL Adobe Experience Manager] à l’aide du service de contenu dynamique.
role: Admin
feature: Tagging,Smart Tags
solution: Experience Manager, Experience Manager Assets
source-git-commit: 109a608db0724050f6e505394da9138855ba992e
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 52%

---

# Dépannage des balises intelligentes pour les informations d’identification OAuth {#oauth-config}

Une configuration d’autorisation ouverte est requise pour adopter le consentement de la variable [!DNL Adobe Experience Manager] pour interagir avec les services de contenu dynamique de manière sécurisée.

>[!NOTE]
>
> Vous ne pouvez pas créer de nouvelles informations d’identification JWT à partir de juin 2024. Dorénavant, seules les informations d’identification OAuth serveur à serveur sont créées.
> L’intégration JWT continue de fonctionner jusqu’en janvier 2025 uniquement pour les utilisateurs AMS et on-premise existants.

## Configuration OAuth pour les nouveaux utilisateurs AMS {#oauth-config-existing-ams-users}

Voir [configuration des services de contenu dynamique](#integrate-adobe-io) pour la configuration des services OAuth pour un nouvel utilisateur. Une fois cette opération terminée, suivez ces [étapes](#prereqs-config-oauth-onprem).

>[!NOTE]
>
>Si nécessaire, vous pouvez envoyer un ticket d’assistance à la suite de la [processus de prise en charge](https://experienceleague.adobe.com/?lang=fr&amp;support-tab=home#support).

## Configuration OAuth pour les utilisateurs AMS existants {#oauth-config-new-ams-users}

Avant d’exécuter l’une des étapes de cette méthodologie, vous devez mettre en oeuvre les éléments suivants :

### Conditions préalables {#prereqs-config-oauth-onprem}

Une configuration OAuth requiert les prérequis suivants :

* Créez une nouvelle intégration OAuth dans le [Developer Console](https://developer.adobe.com/console/user/servicesandapis). Utilisez la variable `ClientID`, `ClientSecret`, `OrgID`, ainsi que d’autres propriétés dans les étapes ci-dessous :
* Les fichiers suivants se trouvent à ce chemin d’accès : `/apps/system/config in crx/de`:
   * `com.**adobe**.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`
   * `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`

### Configuration d’OAuth pour les utilisateurs on-premise {#steps-config-oauth-onprem}

1. Ajoutez ou mettez à jour les propriétés ci-dessous dans `com.adobe.granite.auth.oauth.accesstoken.provider.<randomnumbers>.config`:

   * `auth.token.provider.authorization.grants="client_credentials"`
   * `auth.token.provider.orgId="<OrgID>"`
   * `auth.token.provider.default.claims=("\"iss\"\ :\ \"<OrgID>\"")`
   * `auth.token.provider.scope="read_pc.dma_smart_content,\ openid,\ AdobeID,\ additional_info.projectedProductContext"`
     `auth.token.validator.type="adobe-ims-similaritysearch"`
   * Mettez à jour le `auth.token.provider.client.id` avec l’identifiant client de la nouvelle configuration OAuth.
   * Mettre à jour `auth.access.token.request` to `"https://ims-na1.adobelogin.com/ims/token/v3"`
2. Renommez le fichier en `com.adobe.granite.auth.oauth.accesstoken.provider-<randomnumber>.config`.
3. Suivez les étapes ci-dessous dans `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl.<randomnumber>.config`:
   * Mettez à jour la propriété auth.ims.client.secret avec le secret client de la nouvelle intégration OAuth.
   * Renommez le fichier en `com.adobe.granite.auth.ims.impl.IMSAccessTokenRequestCustomizerImpl-<randomnumber>.config`
4. Enregistrez toutes les modifications dans la console de développement du référentiel de contenu, par exemple, CRXDE.
5. Accédez à `/system/console/configMgr` et remplacez la configuration OSGi de `.<randomnumber>` to `-<randomnumber>`.
6. Suppression de l’ancienne configuration OSGi pour `"Access Token provider name: adobe-ims-similaritysearch"` in `/system/console/configMgr`.
7. Redémarrez la console.

## Validation de la configuration {#validate-the-configuration}

Une fois la configuration terminée, vous pouvez utiliser un MBean JMX pour valider la configuration. Pour procéder à la validation, suivez ces étapes.

1. Accédez à votre serveur [!DNL Experience Manager] sur `https://[aem_server]:[port]`.

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]** pour ouvrir la console OSGi. Cliquez sur **[!UICONTROL Principal] > [!UICONTROL JMX]**.

1. Cliquez sur `com.day.cq.dam.similaritysearch.internal.impl`. Les **[!UICONTROL tâches relatives à SimilaritySearch]** s’ouvrent alors.

1. Cliquez sur `validateConfigs()`. Dans la boîte de dialogue **[!UICONTROL Valider les configurations]**, cliquez sur **[!UICONTROL Invoquer]**.

Le résultat de la validation s’affiche dans la même boîte de dialogue.

## Intégration à la console Adobe Developer {#integrate-adobe-io}

En tant que nouvel utilisateur, lorsque vous intégrez à Adobe Developer Console, l’événement [!DNL Experience Manager] Le serveur authentifie vos informations d’identification de service auprès de la passerelle de la console Adobe Developer avant de transférer votre demande au service de contenu dynamique. Pour l’intégration, vous avez besoin d’un compte Adobe ID disposant de droits d’administrateur pour l’organisation et d’une licence Smart Content Service achetée et activée pour votre organisation.

Pour configurer le service de contenu dynamique, procédez comme suit :

1. Pour générer une clé publique, [créer un service de contenu dynamique ;](#obtain-public-certificate) configuration dans [!DNL Experience Manager]. [Téléchargement d’un certificat public](#obtain-public-certificate) pour l’intégration OAuth.

1. *[Non applicable si vous utilisez déjà]* [création d’une intégration dans Adobe Developer Console](#create-adobe-i-o-integration).

1. [Configurez votre déploiement](#configure-smart-content-service) en utilisant la clé API et d’autres informations d’identification de la console Adobe Developer.

1. [Testez la configuration](#validate-the-configuration).

## Téléchargement d’un certificat public en créant une configuration Smart Content Service {#download-public-certificate}

Un certificat public permet d’authentifier votre profil sur la console Adobe Developer.

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

   ![Boîte de dialogue Service de contenu dynamique Experience Manager pour fournir une URL de service de contenu](assets/aem_scs12.png)

   *Image : boîte de dialogue Service de contenu dynamique pour fournir une URL de service de contenu*

   >[!NOTE]
   >
   >L’URL fournie sous la forme [!UICONTROL URL du service] n’est pas accessible par le biais du navigateur et génère une erreur 404. La configuration fonctionne correctement avec la même valeur que le paramètre [!UICONTROL URL de service]. Pour connaître le statut général du service et le planning de maintenance, consultez [https://status.adobe.com](https://status.adobe.com).

1. Cliquez sur **[!UICONTROL Télécharger le certificat public pour l’intégration OAuth]** et télécharger le fichier de certificat public `AEM-SmartTags.crt`. De plus, vous n’êtes plus tenu de télécharger ce certificat dans la console de développement Adobe.

   ![Représentation des paramètres créés pour le service de balisage intelligent](assets/smart-tags-download-public-cert1.png)

   *Image : paramètres du service de balisage intelligent.*

## Création de l’intégration de la console Adobe Developer {#create-adobe-i-o-integration}

Pour utiliser les API de service de contenu dynamique, créez une intégration dans la console Adobe Developer afin d’obtenir la [!UICONTROL Clé API] (générée dans le champ [!UICONTROL ID CLIENT] de l’intégration de la console Adobe Developer), [!UICONTROL ID DE COMPTE TECHNIQUE], [!UICONTROL ID D’ORGANISATION] et [!UICONTROL SECRET CLIENT] pour les [!UICONTROL Paramètres du service de balisage intelligent des ressources] de la configuration cloud dans [!DNL Experience Manager].

1. Accès [https://developer.adobe.com/console/](https://developer.adobe.com/console/) dans un navigateur. Sélectionnez le compte approprié et vérifiez que le rôle d’organisation associé est administrateur système.

1. Créez un projet portant le nom de votre choix. Cliquez sur **[!UICONTROL Add API]** (Ajouter une API).

1. Sur la page **[!UICONTROL Add API]**, sélectionnez **[!UICONTROL Experience Cloud]** puis **[!UICONTROL Smart Content]** (Contenu dynamique). Cliquez sur **[!UICONTROL Next]** (Suivant).

1. Choisissez la **[!UICONTROL OAuth serveur à serveur]** méthode d’authentification.

1. Ajoutez/modifiez la variable **[!UICONTROL Nom d’identification]** selon les besoins. Cliquez sur **[!UICONTROL Suivant]**.

1. Sélection du profil de produits **[!UICONTROL Smart Content Services]**. Cliquez sur **[!UICONTROL Enregistrer l’API configurée]**. L’API OAuth est ajoutée sous les informations d’identification connectées pour une utilisation ultérieure. Vous pouvez copier la variable [!UICONTROL Clé API (ID client)] ou [!UICONTROL Générer un jeton d’accès] à partir de celle-ci.
<!--
1. On the **[!UICONTROL Select product profiles]** page, select **[!UICONTROL Smart Content Services]**. Click **[!UICONTROL Save configured API]**.

   A page displays more information about the configuration. Keep this page open to copy and add these values in [!UICONTROL Assets Smart Tagging Service Settings] of cloud configuration in [!DNL Experience Manager] to configure smart tags.

   ![In the Overview tab, you can review the information provided for integration.](assets/integration_details.png)


   *Figure: Details of integration in Adobe Developer Console*
-->

![configuration oauth](assets/oauth-config.png)
*Figure : Configuration d’OAuth serveur à serveur dans la console Adobe Developer*

## Configuration du service de contenu dynamique {#configure-smart-content-service}

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

>[!MORELIKETHIS]
>
>* [Présentation et entraînement des balises intelligentes](enhanced-smart-tags.md)
>* [Configuration du balisage intelligent](config-smart-tagging.md)
>* [Tutoriel vidéo sur les balises intelligentes](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html?lang=fr)
