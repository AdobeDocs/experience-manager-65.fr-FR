---
title: Définition des polices à incorporer
description: Découvrez comment spécifier les polices à incorporer dans un formulaire adaptatif. Vous pouvez spécifier les polices qui sont incorporées ou ne le sont jamais dans des formulaires générés par le service Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
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
source-wordcount: '282'
ht-degree: 100%
---
# Définition des polices à incorporer {#specifying-fonts-to-embed}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Vous pouvez spécifier les polices qui sont toujours incorporées ou qui ne le sont jamais dans les formulaires générés par le service Forms. L’incorporation de polices augmente la taille du fichier des formulaires. Incorporez des polices inhabituelles que les utilisateurs et utilisatrices ont rarement sur leurs systèmes. N’incorporez pas les polices courantes généralement installées.

>[!NOTE]
>
>Si vous avez spécifié un fichier XCI personnalisé pour Forms, l’option d’incorporation de polices dans le fichier XCI remplace ces paramètres. (Voir [Configurer des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms).)

1. Dans la console d’administration, cliquez sur **[!UICONTROL Services > Forms]**.
1. Sous **[!UICONTROL Paramètres d’incorporation des polices]**, dans le champ **[!UICONTROL Toujours incorporer les polices]**, saisissez les noms des polices à incorporer aux formulaires (en les séparant par des virgules). Les polices que vous spécifiez ne sont incorporées dans le formulaire généré que si elles sont utilisées dans le formulaire. Ce paramètre est ignoré si l’option d’incorporation des polices a été activée dans le fichier XCI transmis au service, car dans ce cas, toutes les polices utilisées dans le PDF sont toujours incorporées.
1. Dans le champ **[!UICONTROL Ne jamais incorporer les polices]**, saisissez les noms des polices à ne pas incorporer avec les formulaires (en les séparant par des virgules). Les polices que vous spécifiez ne sont pas incorporées dans le PDF, même si elles sont utilisées dans le PDF généré. Ce paramètre est ignoré si l’option d’incorporation des polices a été désactivée dans le fichier XCI transmis au service, car dans ce cas, aucune des polices utilisées dans le PDF n’est incorporée.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
