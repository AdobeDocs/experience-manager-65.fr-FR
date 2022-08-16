---
title: Définition des polices à incorporer
seo-title: Specify fonts to embed
description: Découvrez comment spécifier les polices à incorporer.
seo-description: Learn how to specify fonts to embed.
uuid: 02da5c00-0467-4633-a076-c36725cbfbad
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 180f0448-d507-4b6d-bb8a-d12a434e1250
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 100%

---

# Définition des polices à incorporer{#specify-fonts-to-embed}

Vous pouvez spécifier les polices qui sont toujours ou jamais incorporées avec les formulaires utilisés par le service Output. L’incorporation de polices augmente la taille de fichier des formulaires. Incorporez les polices inhabituelles dont les utilisateurs disposent rarement sur leurs systèmes mais n’incorporez pas les polices courantes qui sont généralement installées.

>[!NOTE]
>
>si vous avez défini un fichier XCI personnalisé pour Output, l’option d’incorporation de polices dans le fichier XCI remplace ces paramètres (voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)).

1. Dans la console d’administration, cliquez sur Services > Output.
1. Sous Paramètres d’incorporation des polices, dans le champ Toujours incorporer les polices, saisissez les noms des polices à incorporer aux formulaires (en les séparant par des virgules). Les polices spécifiées ne sont incorporées au formulaire généré que si elles sont effectivement utilisées dans le formulaire. Ce paramètre est ignoré si l’option d’incorporation des polices a été activée dans le fichier XCI transmis au service car, dans ce cas, toutes les polices utilisées dans le PDF sont systématiquement incorporées.
1. Dans le champ Ne jamais incorporer les polices, saisissez les noms des polices à ne pas incorporer avec les formulaires (en les séparant par des virgules). Les polices spécifiées ne sont pas incorporées au PDF, même si elles sont utilisées dans le PDF généré. Ce paramètre est ignoré si l’option d’incorporation des polices a été désactivée dans le fichier XCI transmis au service car, dans ce cas, aucune des polices utilisées dans le PDF n’est incorporée.
1. Cliquez sur Enregistrer.
