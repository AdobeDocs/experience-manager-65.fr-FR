---
title: Authentification unique et gestionnaires de temporisation
seo-title: Single Sign On and timeout handlers
description: Comment définir la valeur de délai d’expiration de session pour l’espace de travail AEM Forms.
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 40%

---

# Authentification unique et gestionnaires de temporisation {#single-sign-on-and-timeout-handlers}

L’espace de travail AEM Forms est SSO activé. Si un utilisateur s’est connecté à une application AEM Forms telle que Forms Manager ou l’interface utilisateur du PDF Generator et a accès à l’espace de travail AEM Forms dans la même session de navigateur, il est alors connecté à l’espace de travail AEM Forms et inversement.

## Gestion du délai d’expiration du serveur dans l’espace de travail AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Le délai d’expiration de la session d’un utilisateur peut être configuré dans Administration Console.

Pour définir le délai d’expiration, connectez-vous à `https://'[server]:[port]'/adminui`, accédez à **Paramètres > User Management > Configuration > Configurer les attributs système avancés**, puis sélectionnez les paramètres souhaités.

Dans l’espace de travail AEM Forms, le délai d’expiration correspond à :

* la durée de disponibilité d’une session utilisateur en réponse à l’appel de commande `initialize` qui initialise la session utilisateur.
* Une boîte de dialogue contextuelle avertit l’utilisateur que la session est sur le point d’expirer, 15 secondes avant l’expiration de la session.

Dans cette boîte de dialogue contextuelle :

* Cliquez sur OK pour terminer la session utilisateur.
* Cliquez sur Annuler pour réinitialiser la session utilisateur.

>[!NOTE]
>
>Si l’utilisateur ne réagit pas, il est automatiquement déconnecté de l’espace de travail AEM Forms trois secondes avant expiration de la session.
