---
title: Rendre les polices disponibles
description: Assurez-vous que les polices utilisées dans un formulaire sont disponibles sur le serveur d’applications J2EE hébergeant AEM forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 16%

---

# Rendre les polices disponibles {#make-fonts-available}

Assurez-vous que les polices utilisées dans un formulaire sont disponibles sur le serveur d’applications J2EE hébergeant AEM forms. Prenons l’exemple suivant. Un concepteur de formulaire ajoute une police dans le répertoire des polices utilisé par Designer et crée un formulaire qui l’utilise sur un ordinateur distinct. Pour que le service Output utilise la police, placez-la dans le répertoire des polices du client. Si le répertoire des polices du client n’existe pas, créez-en un sur le serveur d’applications J2EE hébergeant AEM forms.

Pour plus d’informations sur les paramètres de police supplémentaires, voir [Configuration des paramètres généraux d’AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**Définition de l’emplacement du répertoire des polices du client**

1. Dans Administration Console, cliquez sur Paramètres > Paramètres de Core Systems > Configurations.
1. Dans la zone Emplacement du répertoire des polices système, saisissez le chemin d’accès au répertoire des polices du client. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**
1. Cliquez sur OK.
1. Redémarrez le système sur lequel AEM forms est installé.

>[!NOTE]
>
>Les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est nécessaire pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client, assurez-vous de redémarrer le système sur lequel AEM Forms est installé.
