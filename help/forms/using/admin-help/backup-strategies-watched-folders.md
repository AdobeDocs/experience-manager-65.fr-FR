---
title: Stratégies de sauvegarde pour les dossiers de contrôle
seo-title: Stratégies de sauvegarde pour les dossiers de contrôle
description: Ce document décrit la façon dont les dossiers de contrôle sont affectés par les différents scénarios de sauvegarde et de récupération. Il présente également les limites et les résultats de ces scénarios, ainsi que les possibilités de réduire les pertes de données.
seo-description: Ce document décrit la façon dont les dossiers de contrôle sont affectés par les différents scénarios de sauvegarde et de récupération. Il présente également les limites et les résultats de ces scénarios, ainsi que les possibilités de réduire les pertes de données.
uuid: c61997b8-6c36-4bd9-90e5-411841a6c176
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f775933-e989-4456-ad01-9bdf5dee3dad
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 95%

---


# Stratégies de sauvegarde pour les dossiers de contrôle {#backup-strategies-for-watched-folders}

Ce contenu décrit la façon dont les dossiers de contrôle sont affectés par les différents scénarios de sauvegarde et de récupération. Il présente également les limites et les résultats de ces scénarios, ainsi que les possibilités de réduire les pertes de données.

*Watched Folder* est une application basée sur système de fichiers. Elle appelle des opérations de service configurées qui manipulent le fichier au sein de l’un des dossiers suivants de la hiérarchie du dossier de contrôle :

* Entrée
* Évaluation
* Sortie
* Failure (Echecs)
* Preserve (Conservés)

Un utilisateur ou une application client dépose tout d’abord le fichier ou le dossier dans le dossier input (Entrée) du dossier de contrôle. L’opération de service déplace ensuite ce fichier dans le dossier stage en vue de son traitement. Après l’exécution par le service de l’opération indiquée, l’enregistrement du fichier modifié intervient dans le dossier output du dossier de contrôle. Les fichiers source correctement traités sont déplacés vers le dossier preserve (Conservés). Les fichiers dont le traitement a échoué sont quant à eux déplacés dans le dossier failure (Echecs) du dossier de contrôle. Lorsque l’attribut `Preserve On Failure` du dossier de contrôle est activé, les fichiers source traités en échec sont déplacés dans le dossier preserve. (voir [Configuration des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints)).

Vous pouvez sauvegarder les dossiers de contrôle en sauvegardant le système de fichiers.

>[!NOTE]
>
>cette sauvegarde est indépendante de la sauvegarde de stockage de la base de données ou des documents, de même que du processus de récupération.

## Fonctionnement des dossiers de contrôle {#how-watched-folders-work}

Cette section décrit le processus de manipulation des fichiers du dossier de contrôle. Il est important de bien comprendre ce processus avant de mettre en place un plan de récupération. Dans cet exemple, l&#39;attribut `Preserve On Failure` du dossier de contrôle est activé. Les fichiers sont traités selon leur ordre d’arrivée.

Le tableau suivant décrit la manipulation de cinq exemples de fichier (fichier1, fichier2, fichier3, fichier4 et fichier5) tout au long du processus. Dans ce tableau, l’axe x représente le temps, par exemple Temps 1 ou T1, et l’axe y représente les dossiers au sein de la hiérarchie du dossier de contrôle, par exemple output.

<table>
 <thead>
  <tr>
   <th><p>Dossier</p></th>
   <th><p>T1</p></th>
   <th><p>T2</p></th>
   <th><p>T3</p></th>
   <th><p>T4</p></th>
   <th><p>T5</p></th>
   <th><p>T6</p></th>
   <th><p>T7</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Entrée</p></td>
   <td><p>fichier1, fichier2, fichier3, fichier4</p></td>
   <td><p>fichier2, fichier3, fichier4</p></td>
   <td><p>fichier3, fichier4</p></td>
   <td><p>fichier4</p></td>
   <td><p>empty</p></td>
   <td><p>fichier5</p></td>
   <td><p>vide</p></td>
  </tr>
  <tr>
   <td><p>Évaluation</p></td>
   <td><p>vide</p></td>
   <td><p>fichier1</p></td>
   <td><p>fichier2</p></td>
   <td><p>fichier3</p></td>
   <td><p>fichier4</p></td>
   <td><p>vide</p></td>
   <td><p>fichier5</p></td>
  </tr>
  <tr>
   <td><p>Sortie</p></td>
   <td><p>vide</p></td>
   <td><p>vide</p></td>
   <td><p>fichier1_out</p></td>
   <td><p>fichier1_out, fichier2_out</p></td>
   <td><p>fichier1_out, fichier2_out</p></td>
   <td><p>fichier1_out, fichier2_out, fichier4_out</p></td>
   <td><p>fichier1_out, fichier2_out, fichier4_out</p></td>
  </tr>
  <tr>
   <td><p>Failure (Echecs)</p></td>
   <td><p>vide</p></td>
   <td><p>vide</p></td>
   <td><p>vide</p></td>
   <td><p>vide</p></td>
   <td><p>fichier3_fail, fichier3 </p></td>
   <td><p>fichier3_fail, fichier3 </p></td>
   <td><p>fichier3_fail, fichier3 </p></td>
  </tr>
  <tr>
   <td><p>Preserve (Conservés)</p></td>
   <td><p>vide</p></td>
   <td><p>vide</p></td>
   <td><p>fichier1 </p></td>
   <td><p>fichier1, fichier2 </p></td>
   <td><p>fichier1, fichier2 </p></td>
   <td><p>fichier1, fichier2, fichier4 </p></td>
   <td><p>fichier1, fichier2, fichier4 </p></td>
  </tr>
 </tbody>
</table>

Le texte suivant décrit la manipulation des fichiers à chacun des temps définis :

**T1 :** les quatre fichiers sont placés dans le dossier input.

**T2 :** l’opération de service déplace le fichier1 dans la scène dossier stage pour la manipulation.

**T3 :** l’opération de service déplace le fichier2 dans le dossier stage pour la manipulation. Elle place les résultats du fichier1 dans le dossier output et déplace le fichier1 dans le dossier preserve.

**T4 :** l’opération de service déplace le fichier3 dans le dossier stage pour la manipulation. Elle place les résultats du fichier2 dans le dossier output, et déplace le fichier2 dans le dossier preserve.

**T5 :** l’opération de service déplace le fichier4 dans le dossier stage pour la manipulation. La manipulation du fichier3 échoue et l’opération de service le place dans le dossier failure.

**T6 :** l’opération de service place fichier5 dans le dossier input. Elle place les résultats du fichier4 dans le dossier output et le fichier4 dans le dossier preserve.

**T7 :** l’opération de service déplace le fichier5 dans le dossier stage pour la manipulation.

## Sauvegarde des dossiers de contrôle {#backing-up-watched-folders}

Il est recommandé de sauvegarder l’intégralité du système de fichiers du dossier de contrôle dans un autre système de fichiers.

## Restauration des dossiers de contrôle  {#restoring-watched-folders}

Cette section décrit la façon de restaurer les dossiers de contrôle. Les dossiers de contrôle appellent souvent des processus de courte durée (une minute ou moins). Dans de tels cas, la restauration du dossier de contrôle au moyen d’une sauvegarde effectuée toutes les heures n’empêche pas les pertes de données.

Par exemple, si une sauvegarde est entreprise à T1 et que le serveur échoue à T7, alors fichier1, fichier2, fichier3 et fichier4 font déjà l’objet d’une manipulation. La restauration d’un dossier de contrôle au moyen d’une sauvegarde entreprise à T1 n’empêche pas les pertes de données.

Si une sauvegarde plus récente a eu lieu, vous pouvez restaurer les fichiers. Lors de cette restauration, vous devez prendre en compte le dossier de la hiérarchie du dossier de contrôle dans lequel se trouve le fichier actuel :

**Stage :** les fichiers de ce dossier sont traités à nouveau une fois le dossier de contrôle restauré.

**Input :** les fichiers de ce dossier sont traités à nouveau une fois le dossier de contrôle restauré.

**Result :** les fichiers de ce dossier ne sont pas traités.

**Output :** les fichiers de ce dossier ne sont pas traités.

**Preserve :** les fichiers de ce dossier ne sont pas traités.

## Stratégies visant à limiter les pertes de données  {#strategies-to-minimize-data-loss}

Les stratégies suivantes permettent de limiter les pertes de données des dossiers output et input au moment de restaurer un dossier de contrôle :

* Sauvegardez fréquemment les dossiers output et failure (toutes les heures par exemple) pour éviter les pertes de données au niveau des fichiers des dossiers result et failure.
* Sauvegardez les fichiers du dossier input dans un dossier autre que le dossier de contrôle. Vous assurez ainsi la disponibilité du fichier après la récupération au cas où les fichiers seraient introuvables dans le dossier output ou le dossier failure. Veillez à la cohérence de votre dispositif d’appellation.

   Par exemple, si vous enregistrez la sortie avec `%F.`*extension*, le fichier de sortie porte le même nom que le fichier d’entrée. Cela vous aidera à déterminer les fichiers d’entrée manipulés et ceux qui doivent être soumis à nouveau. Si vous ne voyez qu’un seul fichier fichier1_out dans le dossier result, et non fichier2_out, fichier3_out et fichier4_out, cela signifie que vous devez soumettre fichier2, fichier3 et fichier4 de nouveau.

* Si la sauvegarde du dossier de contrôle disponible est plus ancienne que le temps nécessaire au traitement de la tâche, vous devez autoriser le système à créer un nouveau dossier de contrôle et à placer automatiquement les fichiers dans le dossier input.
* Si la dernière sauvegarde disponible n’est pas suffisamment récente, que l’heure de la sauvegarde est plus récente que l’heure à laquelle vous parvenez en lançant un nouveau traitement des fichiers et que le dossier de contrôle est restauré, cela signifie que le fichier a été manipulé au cours de l’une des phases suivantes :

   * **Phase 1 :** dans le dossier input
   * **Phase 2 :** copie effectuée dans le dossier stage mais traitement non encore appelé
   * **Phase 3 :** copie effectuée dans le dossier stage et traitement appelé
   * **Phase 4 :** manipulation en cours
   * **Phase 5 :** résultats renvoyés

   Si les fichiers se trouvent en Phase 1, ils seront manipulés. Si les fichiers se trouvent en Phase 2 ou 3, placez-les dans le dossier input afin qu’ils soient manipulés à nouveau.

   >[!NOTE]
   >
   >en manipulant un fichier plusieurs fois, vous évitez les pertes de données mais vos résultats peuvent être dupliqués.

## Conclusion {#conclusion}

Du fait de la nature dynamique et en perpétuel changement des dossiers de contrôle, vous devez effectuer la restauration de tels dossiers avec des fichiers dont la sauvegarde date de moins de 24 heures. La meilleure pratique reste la sauvegarde des résultats, le stockage du dossier input sur un serveur plus sécurisé et le suivi des fichiers d’entrée, afin de pouvoir soumettre la tâche en cas d’échec.
