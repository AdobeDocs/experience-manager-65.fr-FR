---
title: Techniques de test de l’accessibilité des formulaires
description: Découvrez les techniques de test de l’accessibilité des formulaires dans Forms Designer.
feature: Adaptive Forms, Forms Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
hide: true
exl-id: 77fd3bc5-9a05-4442-af2b-238169d8061a
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 1af3c3d4-88d7-5e0f-813c-eb70824bfcdd
    internal-label: Forms Designer
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 100%
---
# Techniques de test de l’accessibilité des formulaires

Pour vous assurer que vos formulaires sont accessibles à un large éventail d’utilisateurs et d’utilisatrices, vous devez les tester à l’aide de diverses technologies d’assistance. Vous pouvez tester vos formulaires de manière simple et peu coûteuse en utilisant les techniques décrites dans cette section.
Vérifiez que le formulaire peut être rempli à l’aide du clavier uniquement. Veillez à remplir le formulaire entier et à tester tous les champs et boutons. Lorsque vous remplissez le formulaire, déterminez si des améliorations sont nécessaires en fonction de vos réponses aux questions suivantes :

* Existe-t-il des opérations qui ne peuvent pas être exécutées ?
* Existe-t-il des opérations qui semblent bizarres ou difficiles à effectuer ?
* Est-ce que les séquences de touches sont bien documentées ?
* Est-ce qu’un raccourci clavier a été défini pour chacune des commandes et des touches ?

Les versions de démonstration des logiciels de lecteur d’écran peuvent être téléchargées gratuitement sur Internet. Pour tester les résultats des lecteurs d’écran, éteignez votre moniteur et utilisez uniquement le lecteur d’écran pour naviguer dans le formulaire et le remplir. En tant que personne ayant créé le formulaire, votre grande connaissance de ce dernier peut faire en sorte qu’il vous soit difficile de déterminer si l’information lue par le lecteur d’écran est suffisante et compréhensible. Si possible, demandez à une autre personne de tester votre formulaire de cette façon.

Des versions de démonstration d’agrandisseurs d’écran sont également disponibles sur Internet.

Un logiciel de reconnaissance vocale, disponible à un coût nominal, peut être utilisé pour tester le formulaire en utilisant uniquement la saisie vocale.
De nombreux utilisateurs et utilisatrices ayant une déficience visuelle s’appuient sur un contraste élevé entre le texte et l’arrière-plan pour lire le formulaire. Microsoft Windows propose un modèle de couleurs pour contraste élevé qui permet d’afficher des écrans semblables à ceux dont se servent les utilisateurs et utilisatrices ayant une déficience visuelle pour remplir leurs formulaires. Pour régler votre écran en mode contraste élevé, activez cette fonction dans les Options d’accessibilité du Panneau de configuration de Windows. À mesure que vous remplissez le formulaire en utilisant ce mode, déterminez les améliorations à apporter. Répondez pour cela aux questions suivantes :

* Certaines parties du formulaire deviennent-elles invisibles, indéchiffrables ou difficiles à utiliser ?
* Certaines zones restent-elles affichées en noir sur fond blanc ?
* Certains éléments ont-ils une taille incorrecte ou sont-ils tronqués ?
