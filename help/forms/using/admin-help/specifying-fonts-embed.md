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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Définition des polices à incorporer {#specifying-fonts-to-embed}

Vous pouvez spécifier les polices qui sont toujours ou jamais incorporées dans les formulaires générés par le service Forms. L’incorporation de polices augmente la taille de fichier des formulaires. Incorporer des polices inhabituelles que les utilisateurs ont rarement de leurs systèmes. N’incorporez pas les polices courantes qui sont généralement installées.

>[!NOTE]
>
>si vous avez défini un fichier XCI personnalisé pour Forms, l’option d’incorporation de polices dans le fichier XCI remplace ces paramètres (voir [Configuration des emplacements pour Forms](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)).

1. In administration console, click **[!UICONTROL Services > Forms]**.
1. Under **[!UICONTROL Font Embedding Settings]**, in the **[!UICONTROL Always Embed Fonts]** box, type the names of the fonts to embed with the forms, separated by commas. Les polices spécifiées ne sont incorporées au formulaire généré que si elles sont effectivement utilisées dans le formulaire. Ce paramètre est ignoré si l’option d’incorporation des polices a été activée dans le fichier XCI transmis au service car, dans ce cas, toutes les polices utilisées dans le PDF sont systématiquement incorporées.
1. In the **[!UICONTROL Never Embed Fonts]** box, type the names of the fonts not to embed with the forms, separated by commas. Les polices spécifiées ne sont pas incorporées au PDF, même si elles sont utilisées dans le PDF généré. Ce paramètre est ignoré si l’option d’incorporation des polices a été désactivée dans le fichier XCI transmis au service car, dans ce cas, aucune des polices utilisées dans le PDF n’est incorporée.
1. Cliquez sur **[!UICONTROL Enregistrer]**.

