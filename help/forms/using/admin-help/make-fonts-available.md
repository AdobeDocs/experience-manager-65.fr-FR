---
title: Rendre les polices disponibles
description: Assurez-vous que les polices utilisées dans un formulaire peuvent être utilisées sur le serveur d’applications J2EE hébergeant AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 100%

---

# Rendre les polices disponibles {#make-fonts-available}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Assurez-vous que les polices utilisées dans un formulaire peuvent être utilisées sur le serveur d’applications J2EE hébergeant AEM Forms. Prenons l’exemple suivant. Un concepteur ou une conceptrice de formulaires ajoute une police au répertoire de polices utilisé et crée un formulaire qui utilise cette police sur un ordinateur distinct. Pour que le service Output utilise la police, placez-la dans le répertoire des polices client. Si le répertoire des polices client n’existe pas, créez un répertoire sur le serveur d’applications J2EE hébergeant AEM Forms.

Pour plus d’informations sur les paramètres de police supplémentaires, voir [Configurer les paramètres généraux d’AEM Forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Spécification de l’emplacement du répertoire des polices client**

1. Dans la console d’administration, cliquez sur Paramètres > Paramètres de Core System > Configurations.
1. Dans la zone Emplacement du répertoire des polices système, tapez le chemin d’accès au répertoire des polices client. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**
1. Cliquez sur OK.
1. Redémarrez le système sur lequel AEM Forms est installé.

>[!NOTE]
>
>Les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM Forms est installé.
