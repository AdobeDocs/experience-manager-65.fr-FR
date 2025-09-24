---
title: Assistant IA dans AEM 6.5
description: Utilisez l’Assistant IA pour vous aider à trouver des réponses et à résoudre les problèmes liés aux solutions disponibles dans Adobe Experience Manager.
solution: Experience Manager, Experience Manager 6.5
feature: Authoring, AI Assistant, AI Tools
role: Admin, Architect, Developer, User
exl-id: 3b4a484e-55b5-4924-82dd-56735f6ed46d
source-git-commit: 4ec42cee96cbedfc70db8a5272ceff64658a22a3
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 5%

---

# Assistant IA dans AEM 6.5 {#about-ai-assistant-in-aem}

>[!IMPORTANT]
>
>Les clients LTS AEM 6.5 et AEM 6.5 qui n’utilisent pas Cloud Manager/Experience Hub doivent contacter leur ingénieur du succès client Adobe pour demander l’accès à l’assistant AI.

L’assistant AI d’AEM 6.5/AEM 6.5 LTS offre une interface de conversation conçue pour rationaliser la recherche de réponses à vos requêtes liées à Adobe Experience Manager. Il vous permet d’obtenir des réponses instantanées à vos questions sur les produits AEM (*disponible pour tous les utilisateurs*) et d’automatiser la création de tickets d’assistance (*disponible pour les administrateurs de l’assistance*).

L’assistant AI prend en charge AEM as a Cloud Service, notamment les solutions suivantes :

* Page d’aperçu d’Experience Hub
* Edge Delivery Services
* Sites
* Assets
* Forms
* Dynamic Media
* Cloud Manager


Il est directement incorporé à AEM et accessible à partir de l’interface d’utilisation d’AEM Experience Hub, de Cloud Manager et de l’instance de création.

La vidéo de 3 minutes et 39 secondes qui suit présente une présentation détaillée de l’assistant AI dans AEM.

>[!VIDEO](https://video.tv.adobe.com/v/3470354?learn=on)

## Accéder à l’assistant AI dans AEM{#get-access}

Pour accéder à l’assistant AI dans AEM, les clients doivent disposer des éléments suivants :

* Autorisation d’utiliser l’assistant AI dans AEM pour la connaissance des produits. Cette autorisation vous permet de poser des questions relatives aux produits dans la conversation de l’assistant AI. Cette autorisation doit être activée.
* Autorisation d’ouvrir les tickets d’assistance, qui nécessite le rôle **Administrateur de l’assistance**.

>[!NOTE]
>
>Les requêtes des assistants d’IA dans AEM sont authentifiées via les services Adobe Identity Management (IMS). Pour plus d’informations, consultez la présentation des services Adobe Identity Management [](https://www.adobe.com/content/dam/cc/en/trust-center/ungated/whitepapers/corporate/adobe-identity-management-services-security-overview.pdf).

**Pour accéder à l’assistant AI dans AEM, procédez comme suit**

1. Les clients doivent avoir un accord supplémentaire en place pour accéder à la plupart des fonctionnalités d’IA et d’agent dans Adobe Experience Manager. Contactez votre représentant Adobe pour plus d’informations.

1. Pour utiliser l’assistant AI dans AEM, l’autorisation d’accéder à la connaissance des produits par l’intermédiaire de l’assistant AI est obligatoire. Cette autorisation est activée par défaut.

   Si vous souhaitez contrôler qui peut accéder à la connaissance des produits, envoyez un e-mail à [aemaiassistant@adobe.com](mailto:aemaiassistant@adobe.com) à partir de l’adresse e-mail associée à votre Adobe ID. Adobe peut activer le contrôle d’accès au niveau de l’utilisateur. Lorsqu’il est activé, votre administrateur peut accorder l’accès au niveau de l’utilisateur en suivant les étapes décrites dans [Configurer l’assistant AI dans AEM](/help/ai-assistant-in-aem-admin.md).


## Portée {#scope}

Le périmètre actuel de l’assistant AI dans AEM se concentre sur les questions de connaissance des produits pour AEMr. as a Cloud Service. Ce champ d’application inclut une prise en charge complète des domaines clés. <!--, such as Sites, Assets, Forms, Edge Delivery Services, Dynamic Media, and Cloud Manager. -->

* **Surfaces** : disponible dans AEM Experience Hub, l’interface utilisateur de création, Cloud Manager.
* **Fonctionnalités** : connaissance du produit et première étape pour le dépannage et les conseils, la création automatisée de tickets d’assistance et la recherche.
* **Valeur** : permet de gagner du temps, d’accélérer l’apprentissage et la valorisation, de réduire la nécessité de créer manuellement des tickets d’assistance et d’améliorer l’efficacité de la création de tickets d’assistance.

## Confidentialité, sécurité et gouvernance{#privacy-security-governance}

L’assistant AI d’AEM est conçu et met l’accent sur la confidentialité, la sécurité et la gouvernance.

Cet article décrit les fonctionnalités centrées sur la confiance que vous pouvez attendre de l’assistant AI dans AEM :

* Aucune donnée personnelle n’est utilisée par l’assistant AI dans AEM, y compris à des fins de formation.
* L’assistant AI dans AEM n’a pas accès aux données des clients.
* Une autorisation explicite est requise pour interagir avec l’assistant AI dans AEM.
* Les invites fournies par l&#39;utilisateur (questions, requêtes, etc.) ne sont pas partagées avec d&#39;autres clients.

<!-- See also [Security at Adobe whitepaper](). NEED ACTIVE LINK FROM ADRIAN NICOLAE TANASE. CURRENTLY 404. -->

## Découvrez l’assistant AI dans AEM pour la connaissance des produits et la création automatisée de tickets d’assistance {#ai-prod-insights}

La connaissance des produits englobe les concepts et les sujets dérivés de la documentation d’Adobe Experience League. Ces questions peuvent être classées dans les sous-groupes suivants :


| Connaissances du produit | Disponible pour tous les utilisateurs<br>Exemples |
| :--- | :--- |
| Apprentissage par points | <ul><li>Qu’est-ce que l’éditeur universel ?</li><li>Comment créer un programme dans Cloud Manager ?</li></ul> |
| Ouvrir la découverte | <ul><li>Comment utiliser l’éditeur universel ?</li><li>Existe-t-il un moyen de copier du contenu d’un environnement à un autre ?</li></ul> |
| Résolution des problèmes | <ul><li>Pourquoi ne puis-je pas accéder à l’éditeur universel ?</li><li>Pourquoi mon pipeline échoue-t-il ?</li></ul> |
| **Création de ticket d’assistance** | **Disponible uniquement pour les administrateurs **<br>**exemples** |
| Création automatisée de tickets d’assistance capturant l’historique et le contexte de la conversation de l’assistant AI | <ul><li>Créez un ticket d’assistance pour moi.</li></ul> |
| Récupération du statut du ticket d’assistance | <ul><li>Montrez-moi tous les tickets d&#39;assistance que j&#39;ai ouverts.</li><li>Me montrer le statut du ticket « E----------- »</li></ul> |

{style="table-layout:auto"}


## Comment concevoir des questions efficaces {#ai-craft-questions}

Pour recevoir les réponses les plus précises de la part de l’assistant AI dans AEM, il est important de formuler vos questions avec clarté et contexte. Suivez les conseils suivants pour vous assurer que vos requêtes sont claires et bien structurées :

* Exposez clairement votre tâche ou votre question de façon concise.
* Évitez les termes ambigus ou les syntaxes trop complexes pour améliorer la compréhension.
* Fournissez un contexte pertinent sur votre tâche ou votre question, car cette approche aide l’assistant d’IA d’AEM à fournir des réponses plus précises et plus pertinentes.
Par exemple, dans votre invite, il est utile de nommer la solution AEM dans laquelle vous travaillez : Sites, Assets, Dynamic Media, Edge Delivery Services, Cloud Manager ou Forms.

### Exemples de questions non prises en charge {#ai-unsupported-questions}

| Aire | Exemples |
| --- | --- |
| Informations opérationnelles | <ul><li>Combien y a-t-il d’environnements de développement dans mon client ?</li><li>Qui a lancé le dernier pipeline de production ?</li></ul> |
| Résolution des problèmes | <ul><li>Pourquoi mon pipeline de production échoue-t-il ?</li></ul> |
| Tâche et automatisation | <ul><li>Configurez un pipeline de qualité du code à partir d’une branche de développement.</li></ul> |


## Utilisation de l’assistant AI dans AEM {#ai-use}

<!-- UNHIDE AFTER BETA or at GA
### Enable AI Assistant in AEM access through Admin Console 

To use AI Assistant in AEM, your organization must opt in at the Admin Console level. A product administrator creates (or chooses) a user group and grants it the new "AI Assistant" permission. Anyone added to that group instantly gains access to the Assistant across AEM. If the goal is company-wide availability, the admin simply assigns all users to that group.

![AI Assistant in AEM in the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console.png)

From an employee's perspective, the process is straightforward: identify the product administrator for Adobe Experience Manager in your organization and request to be added to the AI-enabled user group. Once you appear in that group, the Assistant icon shows up automatically the next time you sign in.

Administrators should keep normal Cloud Manager governance in mind. Hold product administrator rights in the Admin Console to create profiles, manage user groups, or edit permissions. If users also need the Assistant's built-in **Create Support Ticket** feature, add the standard **Support Admin** role (standard Admin Console role) to the same individuals or group.

![Technical support ticket creation in AI Assistant in AEM of the Admin Console](/help/implementing/cloud-manager/assets/ai-assistant-admin-console-support-ticket.png)

For a guided walkthrough of setting up users and groups in AEM as a Cloud Service, see [Configuring access to AEM as a Cloud Service ](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview). 

See also [Custom Permissions](/help/implementing/cloud-manager/custom-permissions.md). -->


### Démarrer une conversation avec un assistant d’IA dans AEM

Vous pouvez réinitialiser l’assistant d’IA dans AEM et démarrer une nouvelle conversation lorsque vous souhaitez changer de sujet. Cette fonctionnalité est particulièrement utile lors de la résolution des problèmes liés aux requêtes qui échouent ou fournissent des informations incorrectes.

**Pour démarrer un assistant AI dans une conversation AEM, procédez comme suit**

1. Dans le coin supérieur droit de l’interface utilisateur d’AEM (à partir des pages Cloud Manager ou de l’instance d’auteur des environnements AEM), cliquez sur l’icône **Assistant IA**.

   ![Icône Assistant IA de la barre d’outils](/help/assets/assets-ai/ai-assistant-icon.png)

1. Dans la zone de texte du panneau **Assistant AI** située en bas, saisissez votre question ou votre invite, puis appuyez sur `Enter` ou cliquez sur ![Icône Envoyer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Send_18_N.svg).

   >[!NOTE]
   >
   >Les données personnelles ne doivent pas être incluses dans vos données, car elles ne sont pas nécessaires pour utiliser cet outil.

   ![Zone de texte au bas du panneau de l’assistant AI](/help/assets/assets-ai/ai-assistant-prompt-text-box.png)

1. Pour démarrer une nouvelle conversation (un nouveau sujet ou une modification du sujet), cliquez sur ![icône Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) > **Démarrer une nouvelle conversation**.

   ![Démarrez une nouvelle conversation dans l’assistant AI à partir de l’icône représentant des points de suspension](/help/assets/assets-ai/ai-assistant-start-new-conversation.png)

### Découvrir les invites par catégorie

L’assistant AI d’AEM comprend une fonction de capacité de découverte pour vous aider à explorer les rubriques et catégories prises en charge.

**Pour découvrir des invites par catégorie :**

1. Dans le panneau de l’assistant d’IA, cliquez sur ![Icône Apprendre](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg) pour activer le panneau de découverte d’invite.

   ![Panneau qui vous permet d’explorer les invites par catégorie dans l’assistant AI](/help/assets/assets-ai/ai-assistant-discover-prompts.png)
   *Panneau affichant les catégories d’invite dans l’assistant AI.*

1. Sélectionnez une catégorie pour afficher la liste des invites associées.
1. Sélectionnez une invite pour afficher des exemples des types de questions auxquelles l’assistant AI peut répondre.

1. Pour masquer le panneau de détection d’invite, cliquez de nouveau sur ![Icône Apprendre](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Learn_18_N.svg).

### Partagez vos commentaires sur l’assistant AI dans AEM

Vos commentaires aident Adobe à améliorer l’assistant d’IA pour de meilleures performances et précision.

Partagez vos commentaires sur votre expérience avec l’assistant AI dans AEM à l’aide des options suivantes :

![Pouces vers le haut, pouces vers le bas et icônes d’indicateur](/help/assets/assets-ai/ai-assistant-feedback-icons.png)

| Cliquer | Description |
| --- | --- |
| ![Icône pouce vers le haut](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbUpOutline_18_N.svg) | Indiquez ce qui s’est bien passé et partagez des commentaires positifs. |
| ![Icône pouce vers le bas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ThumbDownOutline_18_N.svg) | Fournir des suggestions d’amélioration. Ajoutez des commentaires spécifiques sur votre expérience, qui sont examinés quotidiennement. |
| ![Icône Indicateur](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Flag_18_N.svg) | Signalez tout problème ou fournissez des commentaires détaillés sur votre interaction avec l’assistant AI dans AEM. |

## Questions fréquentes sur l’assistant AI dans AEM {#ai-faq}

Voici les réponses à certaines questions courantes sur l’assistant d’IA :

* **Les informations fournies par l’assistant AI dans AEM sont-elles en temps réel ?**\
  Non. L’assistant AI puise son contenu dans la documentation d’Adobe Experience League. Les mises à jour apportées au contenu peuvent prendre un certain temps à se refléter dans ses réponses.
* **Quelles applications Adobe l’assistant AI dans AEM prend-il en charge ?**\
  Actuellement, l’assistant AI prend en charge les demandes d’informations sur les produits dans AEM as a Cloud Service, notamment Sites, Assets, Dynamic Media, Cloud Manager et Forms.
* **Quelles sont les fonctionnalités de l’assistant AI dans AEM ?**\
  L’assistant AI d’AEM est conçu pour répondre aux requêtes liées à la connaissance du produit Adobe.
* **L’assistant AI d’AEM utilise-t-il des informations personnelles pour les données d’identification ?**\
  Non. AI Assistant dans AEM n’utilise pas d’informations personnelles à des fins de formation. Évitez de partager des informations personnelles vous concernant ou concernant d’autres personnes, y compris des noms ou des coordonnées, avec l’assistant AI dans AEM.

<!-- IS THE DOCUMENTATION BELOW STILL NEEDED? IF SO, GO AHEAD AND DELETE THE COMMENT TAGS!!

## AEM Forms AI Assistant (Forms Experience Builder) {#ai-forms-builder}

In addition to the general AI Assistant in AEM for product knowledge, AEM offers a specialized **[AEM Forms AI Assistant (Forms Experience Builder)](/help/edge/docs/forms/forms-ai-assistant.md)**. This enhanced assistant can actively help you create and configure forms through natural language prompts and answer questions specific to forms.

### Key capabilities

The AEM Forms AI Assistant provides:

* **Form Creation**: Create new forms from scratch using natural language descriptions.
* **Design Import**: Convert existing designs (PDF, Figma, images) into functional AEM Forms. 
* **Form Configuration**: Add fields, panels, validation rules, and conditional logic.
* **Layout Management**: Organize form structure and optimize for different devices.
* **Integration Setup**: Configure form submissions and data handling.
* **Product Knowledge**: Answer questions about AEM Forms features and best practices.

### Where to access

The AEM Forms AI Assistant is available in the following:

* **Universal Editor**: For Edge Delivery Services forms with visual editing capabilities.
* **Adaptive Forms Editor**: For detailed form configuration and advanced features.
* **Forms Management UI**: For high-level form creation and management tasks.

### Getting started

>[!NOTE]
>
> The AEM Forms AI Assistant (Forms Experience Builder) is available under the private beta program. Send an email from your work address to [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) to request access.

To learn more about using the AEM Forms AI Assistant , see the [AEM Forms AI Assistant](/help/edge/docs/forms/forms-ai-assistant.md) documentation.

### Example Use Cases

* **"Create a customer feedback form with name, email, rating, and comments fields"**
* **"Convert this uploaded PDF application form into a digital adaptive form"**  
* **"Add conditional logic to show spouse information only when marital status is 'Married'"**
* **"Configure this form to submit data to the Customer Relationship Management system"**

This specialized AEM Forms AI Assistant represents the next evolution in form building, combining the power of AI with AEM's robust forms capabilities to streamline your form creation workflow.
-->
