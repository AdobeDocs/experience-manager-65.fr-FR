---
title: Enregistrer les formulaires sous forme de modèles
description: Découvrez comment créer des modèles à partir de formulaires avec des données requises à plusieurs reprises.
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: b97175fd-cc3d-457a-af11-1f8c83192eb7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 28%

---

# Enregistrer les formulaires sous forme de modèles {#save-forms-as-templates}

Parfois, lorsque les utilisateurs remplissent un formulaire, les entrées de quelques champs restent les mêmes. Pour de telles instances, vous pouvez remplir les champs nécessitant des valeurs identiques dans chaque instance et enregistrer le formulaire ou le brouillon comme modèle. Désormais, chaque fois que vous créez une instance du modèle, les champs spécifiés sont déjà remplis avec les valeurs spécifiées dans le modèle. Cela vous permet de gagner du temps et vous évite les efforts nécessaires pour remplir le formulaire.

Procédez comme suit pour créer un modèle :

1. Ouvrez un formulaire et sélectionnez ou remplissez les champs dont les valeurs sont identiques presqu’à chaque fois que vous l’utilisez. Vous pouvez inclure une pièce jointe au modèle que vous ajoutez généralement lorsque vous remplissez le formulaire.
1. Sélectionnez la variable **Enregistrer en tant que modèle** ![save_as_template](assets/save_as_template.png)Icône Une boîte de dialogue pour indiquer le nom du modèle s’affiche.
1. Indiquez le nom du modèle et sélectionnez **Enregistrer**. Le modèle apparaît dans le dossier de modèles.

   S’il existe un modèle portant le même nom, une boîte de dialogue s’affiche pour confirmer le remplacement du modèle existant. Pour remplacer le modèle existant par un nouveau modèle, sélectionnez **Continuer** ou pour enregistrer le modèle sous un autre nom, sélectionnez **Annuler**.

Vous pouvez maintenant ouvrir le modèle enregistré. Chaque fois qu’un modèle est ouvert, un nouveau formulaire ou une nouvelle tâche est créé et le formulaire affiche les données enregistrées et les options. Grâce aux modèles, vous pouvez modifier les données préremplies, ajouter une pièce jointe, enregistrer en tant que brouillon, envoyer la tâche, ou les utiliser pour créer un autre modèle. Les modèles sont spécifiques aux appareils mobiles et ne sont pas synchronisés avec le serveur Adobe Experience Manager Forms.

Vous pouvez également supprimer un modèle s’il n’est plus nécessaire. Pour supprimer un modèle, accédez au dossier de modèles, sélectionnez les points de suspension, puis sélectionnez **Supprimer le modèle**.

>[!NOTE]
>
>Un modèle est disponible localement et n’est pas synchronisé avec le serveur. L’effacement des données locales de l’application supprime le modèle.
