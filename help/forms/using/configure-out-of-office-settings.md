---
title: Configuration des paramètres d’absence du bureau
description: Découvrez comment configurer les paramètres d’absence du bureau sur votre instance Adobe Experience Manager Forms.
exl-id: e4c9d74c-e08d-4675-91f2-4f9fc2f1bcea
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 100%

---

# Configuration du paramètre d’absence du bureau {#configure-out-of-office-settings}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/configure-out-of-office-settings.html?lang=fr) |
| AEM 6.5 | Cet article |

Si vous envisagez de vous absenter du bureau, vous pouvez spécifier les actions à entreprendre pour les tâches qui vous sont affectées pendant cette période.

Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Si vous êtes dans un fuseau horaire différent de celui du serveur, le fuseau horaire utilisé est celui du client.

Vous pouvez définir une personne par défaut à laquelle toutes vos tâches sont envoyées. Vous pouvez également spécifier des exceptions pour que des tâches issues de processus spécifiques soient envoyées à un utilisateur différent ou pour qu’elles restent dans votre boîte de réception jusqu’à votre retour. Si la personne désignée est également absente du bureau, la tâche passe à l’utilisateur qu’elle aura désigné. Si la tâche ne peut pas être affectée à un utilisateur qui n’est pas absent du bureau, elle demeure dans votre boîte de réception.

Vous pouvez séparer la délégation de tâches en fonction des modèles de processus. Par exemple, vous pouvez affecter une tâche liée au processus A à l’utilisateur A et affecter une tâche liée au processus B à l’utilisateur B.


>[!NOTE]
>
>* Lorsque vous activez le paramètre Absence du bureau, tous les éléments disponibles dans votre boîte de réception avant d’activer ce paramètre restent dans votre boîte de réception. Seules les tâches reçues après l’activation du paramètre sont déléguées.
>* Lorsque vous désactivez le paramètre Absence du bureau, les tâches déléguées ne vous sont pas automatiquement réaffectées. Vous pouvez utiliser la fonctionnalité de revendication pour que ces tâches vous soient attribuées.
>* Lorsque l’utilisateur A délègue des tâches à l’utilisateur B et que l’utilisateur B délègue des tâches à l’utilisateur C, les tâches sont affectées uniquement à l’utilisateur C et non à l’utilisateur B.
>* Lorsqu’une boucle est présente dans l’affectation, les tâches restent chez l’utilisateur initial. Par exemple, lorsque l’utilisateur A délègue des tâches à l’utilisateur B, l’utilisateur C délègue des tâches à l’utilisateur C, l’utilisateur C délègue des tâches à l’utilisateur D et l’utilisateur D délègue des tâches à l’utilisateur B, une boucle est créée. Dans ce cas, la tâche reste à l’utilisateur initial. L’utilisateur A est l’utilisateur initial dans l’exemple ci-dessus.

## Activez le paramètre Absence du bureau pour votre compte {#enable-out-of-office}

Effectuez les étapes suivantes pour activer le paramètre Absence du bureau pour votre compte et déléguez les tâches de votre boîte de réception à un autre utilisateur :

1. Connectez-vous à l’instance AEM. Sélectionnez l’icône ![Boîte de réception](assets/bell.svg), puis **[!UICONTROL Afficher tout]**. La liste des éléments de votre boîte de réception s’affiche.
1. Sélectionnez l’icône ![Sélecteur de vue](assets/viewlist.svg) ou ![Sélecteur de vue](assets/calendar.svg) en regard du bouton **[!UICONTROL Créer]**, puis sélectionnez **[!UICONTROL Paramètres]**. La boîte de dialogue des paramètres apparaît.
1. Ouvrez l’onglet **[!UICONTROL Absence du bureau]** dans la boîte de dialogue des paramètres.
1. Appuyez sur le bouton **[!UICONTROL Activer/Désactiver]** pour activer le paramètre Absence du bureau.
1. Spécifiez les paramètres **[!UICONTROL Heure de Début]** et **[!UICONTROL Heure de fin]**. Les tâches sont déléguées uniquement pendant la période spécifiée. Laissez le champ **[!UICONTROL Heure de fin]** vide pour déléguer des tâches pour une période indéfinie.
1. Cochez la case **[!UICONTROL Transférer mes tâches pendant cette période]**. Si vous ne sélectionnez pas l’option et ne spécifiez pas de personne désignée, vos éléments ne sont transférés à aucun utilisateur ni utilisatrice. Bien que vous soyez en déplacement et que le paramètre soit activé, les éléments restent dans votre boîte de réception.
1. Sélectionnez **[!UICONTROL Ajouter une personne désignée]**. Spécifiez un utilisateur ou une utilisatrice dans le champ **[!UICONTROL Personne désignée]** pour déléguer des éléments. Spécifiez le **[!UICONTROL modèle de workflow]** à déléguer à la personne spécifiée. Vous pouvez sélectionner plusieurs modèles de processus.

   En outre, pour affecter toutes les tâches, quel que soit le modèle de processus, à un utilisateur particulier, sélectionnez **[!UICONTROL Tous les processus]** dans la liste déroulante Modèle de processus. <br>

   Pour attribuer des éléments à un utilisateur ou une utilisatrice spécifique pour quasiment tous les modèles de workflow, sélectionnez **[!UICONTROL Tous les workflows]** dans la liste déroulante Modèle de workflow, appuyez sur **[!UICONTROL + Ajouter des exceptions]** et spécifiez les modèles de workflow à exclure.
   <br>

   Répétez l’étape pour ajouter d’autres personnes désignées. <br>

   >[!NOTE]
   >
   >L’ordre des personnes désignées est important. Lorsqu’un élément est affecté à un utilisateur ou une utilisatrice qui a activé le paramètre Absence du bureau, l’élément est évalué par rapport à la liste des personnes désignées dans leur ordre d’ajout. Lorsqu’un élément correspond aux critères, il est affecté à la personne désignée et la personne désignée suivante n’est pas cochée.

1. Sélectionnez **[!UICONTROL Enregistrer]**. Ce paramètre prend effet à la date et à l’heure de début spécifiées. Si vous vous connectez pendant que vous êtes absent du bureau, vous êtes toujours considéré comme absent du bureau jusqu’à ce que vous ayez modifié vos paramètres.

Désormais, les tâches qui vous sont affectées au cours de la période d’absence du bureau sont automatiquement affectées au délégataire spécifié.
![Absence du bureau](assets/out-of-office.png)

>[!NOTE]
>
>(Pour les éléments de processus orientés formulaire uniquement) Activez l’option **Autoriser les délégataires à déléguer à l’aide des paramètres « Absence du bureau »** de l’étape **Attribuer la tâche** du processus. Seules les tâches pour lesquelles l’option ci-dessus est activée sont déléguées à d’autres utilisateurs ou utilisatrices.

## Limites {#limitations}

* L’affectation de tâches à un groupe n’est pas prise en charge.
* L’activation du paramètre Absence du bureau pour les tâches de projet n’est actuellement pas prise en charge.
