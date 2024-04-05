---
title: Stratégies de sauvegarde pour les dossiers de contrôle
description: Ce document décrit l’impact des dossiers de contrôle sur différents scénarios de sauvegarde et de récupération, les limites et les résultats de ces scénarios, ainsi que la manière de minimiser les pertes de données.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0d36160a-29fa-4cc4-a0ff-fc681d3e040e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 100%

---

# Stratégies de sauvegarde pour les dossiers de contrôle {#backup-strategies-for-watched-folders}

Ce contenu décrit l’impact des dossiers de contrôle sur différents scénarios de sauvegarde et de récupération, les limites et les résultats de ces scénarios, ainsi que la manière de minimiser les pertes de données.

*Watched Folder* est une application basée sur un système de fichiers. Elle appelle des opérations de service configurées qui manipulent le fichier dans l’un des dossiers suivants de la hiérarchie du dossier de contrôle :

* Entrée
* Évaluation
* Sortie
* Échec
* Preserve (Conservés)

Une personne ou une application cliente dépose tout d’abord le fichier ou le dossier dans le dossier d’entrée. L’opération de service déplace ensuite le fichier dans le dossier stage en vue de son traitement. Après l’exécution par le service de l’opération indiquée, l’enregistrement du fichier modifié intervient dans le dossier output. Les fichiers source correctement traités sont déplacés vers le dossier preserve (Conservés). Les fichiers dont le traitement a échoué sont quant à eux déplacés dans le dossier failure (Échecs) du dossier de contrôle. Si l’attribut `Preserve On Failure` est activé pour le dossier de contrôle, les fichiers source dont le traitement a échoué sont déplacés dans le dossier preserve (Conservés). (Voir [Configurer des points d’entrée de Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#configuring-watched-folder-endpoints).)

Vous pouvez sauvegarder les dossiers de contrôle en sauvegardant le système de fichiers.

>[!NOTE]
>
>Cette sauvegarde est indépendante du processus de sauvegarde et de récupération de la base de données ou du stockage de documents.

## Fonctionnement des dossiers de contrôle {#how-watched-folders-work}

Ce contenu décrit le processus de manipulation des fichiers du dossier de contrôle. Il est important de comprendre ce processus avant d’élaborer un plan de restauration. Dans l’exemple fourni, l’attribut `Preserve On Failure` est activé pour le dossier de contrôle. Les fichiers sont traités selon leur ordre d’arrivée.

Le tableau suivant décrit la manipulation de cinq fichiers d’exemple (file1, file2, file3, file4, file5) tout au long du processus. Dans le tableau, l’axe X représente le temps, par exemple Temps 1 ou T1, et l’axe Y représente les dossiers dans la hiérarchie des dossiers de contrôle, par exemple output.

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
   <td><p>file1, file2, file3, file4</p></td>
   <td><p>file2, file3, file4</p></td>
   <td><p>file3, file4</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
   <td><p>empty</p></td>
  </tr>
  <tr>
   <td><p>Évaluation</p></td>
   <td><p>empty</p></td>
   <td><p>file1</p></td>
   <td><p>file2</p></td>
   <td><p>file3</p></td>
   <td><p>file4</p></td>
   <td><p>empty</p></td>
   <td><p>file5</p></td>
  </tr>
  <tr>
   <td><p>Sortie</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
   <td><p>file1_out, file2_out, file4_out</p></td>
  </tr>
  <tr>
   <td><p>Échec</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
   <td><p>file3_fail, file3 </p></td>
  </tr>
  <tr>
   <td><p>Preserve (Conservés)</p></td>
   <td><p>empty</p></td>
   <td><p>empty</p></td>
   <td><p>file1 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2 </p></td>
   <td><p>file1, file2, file4 </p></td>
   <td><p>file1, file2, file4 </p></td>
  </tr>
 </tbody>
</table>

Le texte suivant décrit la manipulation des fichiers à chacun des temps définis :

**T1 :** les quatre fichiers d’exemple sont placés dans le dossier input.

**T2 :** l’opération de service déplace le fichier1 dans la scène dossier stage pour la manipulation.

**T3 :** l’opération de service déplace le fichier2 dans le dossier de traitement pour la manipulation. Elle place les résultats de file1 dans le dossier output, et déplace file1 dans le dossier de preserve.

**T4 :** l’opération de service déplace le fichier3 dans le dossier stage pour la manipulation. Elle place les résultats du fichier2 dans le dossier output, et déplace le fichier2 dans le dossier preserve.

**T5 :** l’opération de service déplace le fichier4 dans le dossier stage pour la manipulation. La manipulation du fichier3 échoue et l’opération de service le place dans le dossier failure.

**T6 :** l’opération de service place fichier5 dans le dossier input. Elle place les résultats du fichier4 dans le dossier output et le fichier4 dans le dossier preserve.

**T7 :** l’opération de service déplace le fichier5 dans le dossier stage pour la manipulation.

## Sauvegarde des dossiers de contrôle {#backing-up-watched-folders}

Il est recommandé de sauvegarder l’intégralité du système de fichiers du dossier de contrôle dans un autre système de fichiers.

## Restauration des dossiers de contrôle {#restoring-watched-folders}

Cette section décrit comment restaurer les dossiers de contrôle. Les dossiers de contrôle appellent souvent des processus de courte durée (une minute ou moins). Dans de tels cas, la restauration du dossier de contrôle au moyen d’une sauvegarde effectuée toutes les heures n’empêche pas les pertes de données.

Par exemple, si une sauvegarde est entreprise à T1 et que le serveur échoue à T7, alors file1, file2, file3 et file4 font déjà l’objet d’une manipulation. La restauration d’un dossier de contrôle au moyen d’une sauvegarde entreprise à T1 n’empêche pas les pertes de données.

Si une sauvegarde plus récente a été effectuée, vous pouvez restaurer les fichiers. Lors de cette restauration, vous devez prendre en compte le dossier de la hiérarchie du dossier de contrôle dans lequel se trouve le fichier actuel :

**Stage :** les fichiers de ce dossier sont traités à nouveau une fois le dossier de contrôle restauré.

**Input :** les fichiers de ce dossier sont traités à nouveau une fois le dossier de contrôle restauré.

**Résult :** les fichiers de ce dossier ne sont pas traités.

**Output :** les fichiers de ce dossier ne sont pas traités.

**Preserve :** les fichiers de ce dossier ne sont pas traités.

## Stratégies de réduction des pertes de données {#strategies-to-minimize-data-loss}

Les stratégies suivantes peuvent réduire la perte de données des dossiers de sortie et d’entrée lors de la restauration d’un dossier de contrôle :

* Sauvegardez fréquemment les dossiers de sortie et d’échec, par exemple toutes les heures, afin d’éviter toute perte de fichiers de résultat et d’échec.
* Sauvegardez les fichiers d’entrée dans un dossier autre que le dossier de contrôle. Cela garantit la disponibilité des fichiers après récupération, au cas où vous ne trouveriez pas les fichiers dans le dossier de sortie ou celui d’échec. Assurez-vous que votre schéma d’affectation de noms de fichier est cohérent.

  Par exemple, si vous enregistrez la sortie avec l’`%F.`*extension*, le fichier de sortie porte le même nom que le fichier d’entrée. Vous pouvez ainsi déterminer les fichiers d’entrée manipulés et ceux qui doivent être envoyés à nouveau. Si vous voyez uniquement le fichier file1_out dans le dossier de résultat et non file2_out, file3_out et file4_out, vous devez envoyer à nouveau file2, file3 et file4.

* Si la sauvegarde du dossier de contrôle disponible est antérieure au temps nécessaire à l’exécution du traitement, vous devez autoriser le système à créer un dossier de contrôle et à placer automatiquement les fichiers dans le dossier d’entrée.
* Si la dernière sauvegarde disponible n’est pas suffisamment récente, que le temps de sauvegarde est inférieur au temps nécessaire au traitement des fichiers et que le dossier de contrôle est restauré, le fichier a été manipulé au cours de l’une des étapes suivantes :

   * **Étape 1 :** dans le dossier d’entrée.
   * **Étape 2 :** copié dans le dossier d’évaluation, mais le processus n’est pas encore appelé.
   * **Étape 3 :** copié dans le dossier d’évaluation et le processus est appelé.
   * **Étape 4 :** manipulation en cours.
   * **Étape 5 :** résultats renvoyés.

  Si les fichiers se trouvent dans l’étape 1, ils seront manipulés. Si les fichiers se trouvent dans l’étape 2 ou 3, placez-les dans le dossier d’entrée pour que la manipulation se reproduise.

  >[!NOTE]
  >
  >Si un fichier est manipulé plusieurs fois, la perte de données est évitée, mais les résultats peuvent être dupliqués.

## Conclusion {#conclusion}

En raison de la nature dynamique et constamment changeante d’un dossier de contrôle, la restauration des dossiers de contrôle doit être effectuée avec des fichiers sauvegardés dans la journée. Il est recommandé de sauvegarder les résultats, de stocker le dossier d’entrée sur un serveur et de suivre les fichiers d’entrée afin de pouvoir soumettre à nouveau le traitement en cas d’échec.
