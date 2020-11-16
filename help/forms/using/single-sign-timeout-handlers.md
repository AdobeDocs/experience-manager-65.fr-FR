---
title: Authentification unique et gestionnaires de temporisation
seo-title: Authentification unique et gestionnaires de temporisation
description: Comment définir la valeur du délai d’expiration de la session pour l’espace de travail AEM Forms.
seo-description: Comment définir la valeur du délai d’expiration de la session pour l’espace de travail AEM Forms.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 55%

---


# Authentification unique et gestionnaires de temporisation {#single-sign-on-and-timeout-handlers}

L’authentification unique est activée sur l’espace de travail AEM Forms. Si un utilisateur s’est connecté à une application AEM Forms telle que Forms Manager ou l’interface utilisateur de PDF Generator et accède à AEM Forms workspace dans la même session de navigateur, il est alors connecté à AEM Forms workspace et vice versa.

## Gestion des délais du serveur dans l’espace de travail AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

Le délai d’expiration d’une session utilisateur peut être configuré dans Administration Console.

To set the timeout, login to `https://'[server]:[port]'/adminui`, navigate to **Settings > User Management > Configuration > Configure Advanced System Attributes**, and make the desired settings.

En AEM Forms, le délai d’expiration de l’espace de travail est géré comme suit :

* la durée de disponibilité d’une session utilisateur en réponse à l’appel de commande `initialize` qui initialise la session utilisateur.
* Une boîte de dialogue contextuelle informe l’utilisateur que la session va expirer, 15 secondes avant qu’elle n’expire

Dans cette boîte de dialogue contextuelle :

* Cliquez sur OK pour fermer la session utilisateur.
* Cliquez sur Annuler pour réinitialiser la session utilisateur.

>[!NOTE]
>
>Si aucune action n’est entreprise, l’utilisateur est automatiquement déconnecté de l’espace de travail AEM Forms trois secondes avant l’expiration de la session.
