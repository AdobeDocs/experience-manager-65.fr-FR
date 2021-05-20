---
title: Rendre les polices disponibles
seo-title: Rendre les polices disponibles
description: Assurez-vous que les polices utilisées dans un formulaire sont bien disponibles sur le serveur d’applications J2EE hébergeant AEM forms.
seo-description: Assurez-vous que les polices utilisées dans un formulaire sont bien disponibles sur le serveur d’applications J2EE hébergeant AEM forms.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 100%

---

# Rendre les polices disponibles {#make-fonts-available}

Assurez-vous que les polices utilisées dans un formulaire sont bien disponibles sur le serveur d’applications J2EE hébergeant AEM forms. Prenons l’exemple suivant. Un concepteur de formulaire ajoute une police dans le répertoire de polices utilisé par Designer et crée un formulaire utilisant cette police sur un autre ordinateur. Placez cette police dans le répertoire des polices du client pour que le service Output puisse l’utiliser. Si ce répertoire n’existe pas, créez-le sur le serveur d’applications J2EE hébergeant AEM forms.

Pour plus d’informations sur les paramètres de police supplémentaires, consultez la section [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Spécification de l’emplacement du répertoire des polices du client**

1. Dans Administration Console, cliquez sur Paramètres > Paramètres de Core System > Configurations.
1. Dans la zone Emplacement du répertoire des polices système, saisissez le chemin du répertoire des polices du client. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**
1. Cliquez sur OK.
1. Redémarrez le système sur lequel AEM forms est installé.

>[!NOTE]
>
>Les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM forms est installé.
