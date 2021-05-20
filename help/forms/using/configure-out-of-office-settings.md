---
title: Configuration des paramètres d’absence du bureau
seo-title: Configuration des paramètres d’absence du bureau
description: Configuration des paramètres d’absence du bureau
seo-description: Configuration des paramètres d’absence du bureau
exl-id: e4c9d74c-e08d-4675-91f2-4f9fc2f1bcea
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 100%

---

# Configuration du paramètre d&#39;absence du bureau {#configure-out-of-office-settings}

Si vous envisagez de vous absenter du bureau, vous pouvez spécifier les actions à entreprendre pour les tâches qui vous sont affectées pendant cette période.

Vous pouvez spécifier une date et une heure de début, ainsi qu’une date et une heure de fin, pour l’application de vos paramètres d’absence du bureau. Si vous êtes situé dans un fuseau horaire différent de celui du serveur, le fuseau horaire utilisé est celui du client.

Vous pouvez définir une personne par défaut à laquelle toutes vos tâches sont envoyées. Vous pouvez également spécifier des exceptions pour que des tâches issues de processus spécifiques soient envoyées à un utilisateur différent ou pour qu’elles restent dans votre boîte de réception jusqu’à votre retour. Si la personne désignée est également absente du bureau, la tâche passe à l’utilisateur qu’elle aura désigné. Si la tâche ne peut pas être affectée à un utilisateur qui n’est pas absent du bureau, elle demeure dans votre boîte de réception.

Vous pouvez séparer la délégation de tâches en fonction des modèles de processus. Par exemple, vous pouvez affecter une tâche liée au processus A à l’utilisateur A et affecter une tâche liée au processus B à l’utilisateur B.


>[!NOTE]
>
>* Lorsque vous activez le paramètre Absence du bureau, toutes les tâches disponibles dans votre boîte de réception avant d’activer ce paramètre restent dans votre boîte de réception. Seules les tâches reçues après l’activation du paramètre sont déléguées.
>* Lorsque vous désactivez le paramètre Absence du bureau, les tâches déléguées ne vous sont pas automatiquement réaffectées. Vous pouvez utiliser la fonctionnalité de revendication pour que ces tâches vous soient attribuées.
>* Lorsque l’utilisateur A délègue des tâches à l’utilisateur B et que l’utilisateur B délègue des tâches à l’utilisateur C, les tâches sont affectées uniquement à l’utilisateur C et non à l’utilisateur B.
>* Lorsqu’une boucle est présente dans l’affectation, les tâches restent chez l’utilisateur initial. Par exemple, lorsque l’utilisateur A délègue des tâches à l’utilisateur B, l’utilisateur C délègue des tâches à l’utilisateur C, l’utilisateur C délègue des tâches à l’utilisateur D et l’utilisateur D délègue des tâches à l’utilisateur B, une boucle est créée. Dans ce cas, la tâche reste à l’utilisateur initial. L’utilisateur A est l’utilisateur initial dans l’exemple ci-dessus.


## Activez le paramètre Absence du bureau pour votre compte {#enable-out-of-office}

Effectuez les étapes suivantes pour activer le paramètre Absence du bureau pour votre compte et déléguez les tâches de votre boîte de réception à un autre utilisateur :

1. Connectez-vous à l’instance AEM. Appuyez sur l&#39;icône ![Boîte de réception](assets/bell.svg) et appuyez sur **[!UICONTROL Afficher tout]**. Une liste des tâches figurant dans votre boîte de réception s&#39;affiche.
1. Appuyez sur l&#39;icône ![Sélecteur de Vue](assets/viewlist.svg) ou ![Sélecteur de Vue](assets/calendar.svg) à côté du bouton **[!UICONTROL Créer]** et appuyez sur **[!UICONTROL Paramètres]**. La boîte de dialogue des paramètres s&#39;affiche.
1. Ouvrez l&#39;onglet **[!UICONTROL Absence du bureau]** dans la boîte de dialogue des paramètres.
1. Appuyez sur le bouton **[!UICONTROL Activer/Désactiver]** pour activer le paramètre Absence du bureau.
1. Spécifiez les paramètres **[!UICONTROL Heure de Début]** et **[!UICONTROL Heure de fin]**. Les tâches sont déléguées uniquement pendant la période spécifiée. Laissez le champ **[!UICONTROL Heure de fin]** vide pour déléguer des tâches pour une période indéfinie.
1. Cochez la case **[!UICONTROL Transférer mes tâches au cours de cette période]**. Si vous ne sélectionnez pas l’option et ne spécifiez pas de personne désignée, vos tâches ne sont transférées à aucun utilisateur. Bien que vous soyez absent et que le paramètre soit activé, les tâches restent dans votre boîte de réception.
1. Appuyez sur **[!UICONTROL Ajouter un délégataire]**. Spécifiez un utilisateur dans le champ **[!UICONTROL Délégataire]** pour lui déléguer les tâches. Spécifiez le **[!UICONTROL modèle de processus]** à déléguer à l&#39;utilisateur spécifié. Vous pouvez sélectionner plusieurs modèles de processus.

   En outre, pour affecter toutes les tâches, quel que soit le modèle de processus, à un utilisateur particulier, sélectionnez **[!UICONTROL Tous les processus]** dans la liste déroulante Modèle de processus. <br>

   Pour affecter des tâches à un utilisateur particulier pour tous les modèles de processus sauf quelques-uns, sélectionnez **[!UICONTROL Tous les processus]** dans la liste déroulante Modèle de processus, appuyez sur **[!UICONTROL + Ajouter exceptions]** et spécifiez les modèles de processus à exclure.
   <br>

   Répétez cette étape pour ajouter d’autres délégataires. <br>

   >[!NOTE]
   >
   >L&#39;ordre des délégataires est important. Lorsqu’une tâche est affectée à un utilisateur qui a activé le paramètre Absence du bureau, la tâche est évaluée par rapport à la liste des délégataires dans leur ordre d&#39;ajout. Lorsqu’une tâche correspond aux critères, elle est affectée au délégataire et le délégataire suivant n’est pas coché.

1. Appuyez sur **[!UICONTROL Enregistrer]**. Ce paramètre prend effet à la date et à l’heure de début spécifiées. Si vous vous connectez pendant que vous êtes absent du bureau, vous êtes toujours considéré comme absent du bureau jusqu’à ce que vous ayez modifié vos paramètres.

Désormais, les tâches qui vous sont affectées au cours de la période d’absence du bureau sont automatiquement affectées au délégataire spécifié.
![Absence du bureau](assets/out-of-office.png)

>[!NOTE]
>
>(Pour les éléments de processus orientés formulaire uniquement) Activez l&#39;option **Autoriser les délégataires à déléguer à l&#39;aide des paramètres « Absence du bureau »** de l&#39;étape **Attribuer la tâche** du processus. Seules les tâches pour lesquelles l’option ci-dessus est activée sont déléguées à d’autres utilisateurs.

## Restrictions {#limitations}

* L’affectation de tâches à un groupe n’est pas prise en charge.
* L’activation du paramètre Absence du bureau pour les tâches de projet n’est actuellement pas prise en charge.
