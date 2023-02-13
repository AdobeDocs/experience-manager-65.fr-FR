---
title: Authentification unique et gestionnaires de temporisation
seo-title: Single Sign On and timeout handlers
description: Comment définir la valeur du délai d’expiration de la session pour l’espace de travail AEM Forms.
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '189'
ht-degree: 100%

---

# Authentification unique et gestionnaires de temporisation {#single-sign-on-and-timeout-handlers}

L’authentification unique est activée sur l’espace de travail AEM Forms. Si un utilisateur s’est connecté à une application AEM Forms telle que Forms Manager ou l’interface utilisateur de PDF Generator, puis accède à l’espace de travail AEM Forms dans la même session de navigateur, alors il est connecté à l’espace de travail AEM Forms et vice versa.

## Gestion des délais du serveur dans l’espace de travail AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Le délai d’expiration d’une session utilisateur peut être configuré dans Administration Console.

Pour définir le délai d’expiration, connectez-vous à `https://'[server]:[port]'/adminui`, accédez à **Paramètres > User Management > Configuration > Configurer les attributs système avancés**, puis sélectionnez les paramètres souhaités.

Dans l’espace de travail AEM Forms, le délai d’expiration correspond à :

* la durée de disponibilité d’une session utilisateur en réponse à l’appel de commande `initialize` qui initialise la session utilisateur.
* Une boîte de dialogue contextuelle informe l’utilisateur que la session va expirer, 15 secondes avant qu’elle n’expire

Dans cette boîte de dialogue contextuelle :

* Cliquez sur OK pour fermer la session utilisateur.
* Cliquez sur Annuler pour réinitialiser la session utilisateur.

>[!NOTE]
>
>Si l’utilisateur ne réagit pas, il est automatiquement déconnecté de l’espace de travail AEM Forms trois secondes avant expiration de la session.
