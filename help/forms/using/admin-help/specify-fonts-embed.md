---
title: Spécifier les polices à incorporer
description: Découvrez comment spécifier les polices à incorporer dans un formulaire adaptatif. Vous pouvez spécifier les polices qui sont incorporées ou jamais incorporées dans des formulaires générés par le service Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 02c28b2c-0cab-4431-9fab-fa332c96e092
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 22%

---

# Spécifier les polices à incorporer{#specify-fonts-to-embed}

Vous pouvez spécifier les polices qui sont toujours incorporées ou jamais incorporées avec les formulaires utilisés par Output. L’incorporation de polices augmente la taille de fichier des formulaires. Incorporez les polices inhabituelles que les utilisateurs ne sont pas susceptibles de posséder sur leurs systèmes et n’incorporez pas les polices courantes qu’ils auront installées.

>[!NOTE]
>
>Si vous avez spécifié un fichier XCI personnalisé pour Output, l’option d’incorporation de polices dans le fichier XCI remplace ces paramètres. (Voir [Définition des emplacements de fichiers pour Output](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)

1. Dans Administration Console, cliquez sur Services > Output.
1. Sous Paramètres d’incorporation des polices, dans le champ Toujours incorporer les polices, saisissez les noms des polices à incorporer aux formulaires (en les séparant par des virgules). Les polices que vous spécifiez ne sont incorporées dans le formulaire généré que si elles sont utilisées dans le formulaire. Ce paramètre est ignoré si l’option d’incorporation des polices a été activée dans le fichier XCI transmis au service. Dans ce cas, toutes les polices utilisées dans le PDF sont toujours incorporées.
1. Dans le champ Ne jamais incorporer les polices, saisissez les noms des polices à ne pas incorporer avec les formulaires (en les séparant par des virgules). Les polices que vous spécifiez ne sont pas incorporées dans le PDF, même si elles sont utilisées dans le PDF généré. Ce paramètre est ignoré si l’option d’incorporation des polices a été désactivée dans le fichier XCI transmis au service. Dans ce cas, aucune des polices utilisées dans le PDF n’est incorporée.
1. Cliquez sur Enregistrer.
