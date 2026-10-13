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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
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

1. Dans la console d’administration, cliquez sur Paramètres > Paramètres des systèmes principaux > Configurations.
1. Dans la zone Emplacement du répertoire des polices système, tapez le chemin d’accès au répertoire des polices client. Vous pouvez ajouter plusieurs répertoires en les séparant par des points-virgules **;**
1. Cliquez sur OK.
1. Redémarrez le système sur lequel AEM Forms est installé.

>[!NOTE]
>
>Les polices sont sélectionnées à partir du cache des polices du système Windows et un redémarrage du système est requis pour mettre à jour le cache. Après avoir spécifié le répertoire des polices du client ou de la cliente, assurez-vous de redémarrer le système sur lequel AEM forms est installé.
