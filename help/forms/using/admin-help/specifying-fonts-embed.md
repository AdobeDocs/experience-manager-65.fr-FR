---
title: Définition des polices à incorporer
seo-title: Définition des polices à incorporer
description: Découvrez comment spécifier les polices à incorporer.
seo-description: Découvrez comment spécifier les polices à incorporer.
uuid: 97de6f98-ed3b-4a93-854a-193a967b4672
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4c83694c-b00f-40be-9ac4-f5785cd60741
exl-id: b2cbf5f3-ee13-47bf-bf7f-f6a1884cee66
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 80%

---

# Définition des polices à incorporer {#specifying-fonts-to-embed}

Vous pouvez spécifier les polices qui sont toujours ou jamais incorporées dans les formulaires générés par le service Forms. L’incorporation de polices augmente la taille de fichier des formulaires. Incorporer des polices inhabituelles que les utilisateurs ont rarement de leurs systèmes. N’incorporez pas les polices courantes qui sont généralement installées.

>[!NOTE]
>
>si vous avez défini un fichier XCI personnalisé pour Forms, l’option d’incorporation de polices dans le fichier XCI remplace ces paramètres (voir [Configuration des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)).

1. Dans Administration Console, cliquez sur **[!UICONTROL Services > Forms]**.
1. Sous **[!UICONTROL Paramètres d’incorporation des polices]**, dans la zone **[!UICONTROL Toujours incorporer les polices]**, saisissez les noms des polices à incorporer aux formulaires, séparés par des virgules. Les polices spécifiées ne sont incorporées au formulaire généré que si elles sont effectivement utilisées dans le formulaire. Ce paramètre est ignoré si l’option d’incorporation des polices a été activée dans le fichier XCI transmis au service car, dans ce cas, toutes les polices utilisées dans le PDF sont systématiquement incorporées.
1. Dans la zone **[!UICONTROL Ne jamais incorporer les polices]**, saisissez les noms des polices à ne pas incorporer aux formulaires, séparés par des virgules. Les polices spécifiées ne sont pas incorporées au PDF, même si elles sont utilisées dans le PDF généré. Ce paramètre est ignoré si l’option d’incorporation des polices a été désactivée dans le fichier XCI transmis au service car, dans ce cas, aucune des polices utilisées dans le PDF n’est incorporée.
1. Cliquez sur **[!UICONTROL Enregistrer]**.
