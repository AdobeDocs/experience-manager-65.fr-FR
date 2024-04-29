---
title: Comment générer et utiliser des hachages dans les PDF forms dynamiques ?
description: Génération et utilisation de hachages dans les PDF forms dynamiques
exl-id: 026f5686-39ea-4798-9d1f-031f15941060
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1189'
ht-degree: 100%

---

# Génération et utilisation de hachages dans les PDF forms dynamiques {#generate-work-with-hashes-dynamic-pdf-forms}

## Connaissances préalables {#prerequisite-knowledge}

Une certaine expérience avec AEM Forms sur JEE Designer est requise, de même que la possibilité d’accéder et d’appeler des fonctions dans des objets de script.

## Niveau d’utilisateur {#user-level}

Débutant

Lorsque vous souhaitez masquer un mot de passe dans votre formulaire PDF et que vous ne voulez pas qu’il apparaisse en clair dans le code source ou ailleurs dans le document PDF, il est essentiel de savoir comment générer et utiliser les hachages MD4, MD5, SHA-1 et SHA-256.

L’idée est d’obscurcir le mot de passe en générant un hachage unique et de stocker ce hachage dans le document PDF. Ce hachage unique peut être généré par différentes fonctions de hachage. Dans cet article, vous allez voir comment les générer dans le formulaire PDF et comment les utiliser.

Une fonction de hachage prend en entrée une longue chaîne (ou message) de n’importe quelle longueur et produit en sortie une chaîne de longueur fixe, parfois appelée Condensé de message ou empreinte numérique.

AEM Forms on JEE Designer vous permet d’implémenter les différentes fonctions de hachage dans des objets de script en JavaScript et de les exécuter dans un document PDF dynamique. Les PDF d’exemple qui sont inclus dans les fichiers d’exemple de cet article utilisent des implémentations open source des fonctions de hachage suivantes :

* MD4 et MD5, conçus par Ronald Rivest.

* SHA-1 et SHA-256, telles qu’elles sont définies par le NIST.

L’utilisation des hachages a pour principal avantage de ne pas avoir à comparer directement les mots de passe en comparant des chaînes de texte en clair ; au lieu de cela, vous pouvez comparer les deux hachages des deux mots de passe. Comme il est peu probable que deux chaînes différentes aient le même hachage, si les deux hachages sont identiques, alors vous pouvez supposer que les chaînes comparées (dans ce cas, les mots de passe) sont également identiques.

>[!NOTE]
>
>Il existe des problèmes de sécurité bien connus (appelés collisions de hachage) avec MD4 ou MD5. En raison de ces collisions de hachage et d’autres piratages de SHA-1 (y compris les tables arc-en-ciel), j’ai décidé de me concentrer sur la fonction de hachage SHA-256 dans le deuxième exemple. Pour plus d’informations, consultez les pages [Collision](https://fr.wikipedia.org/wiki/Collision_(informatique)) et [Tableau arc-en-ciel](https://fr.wikipedia.org/wiki/Rainbow_table) de Wikipédia.

## Examiner les objets de script {#examining-script-objects}

Lorsque vous ouvrez l’un des deux exemples fournis dans AEM Forms on JEE Designer, vous trouvez les quatre objets de script dans la palette Hiérarchie (voir la figure ci-dessous).

![Variables](assets/variables.jpg)

Pour voir l’implémentation JavaScript des fonctions de hachage dans ces objets de script, sélectionnez l’objet de script et explorez le code dans l’éditeur de script. Vous pouvez voir comment chacune des fonctions de hachage suivantes a été implémentée :

* soHASHING_MD4.hex_md4()
* soHASHING_MD4.b64_md4()
* soHASHING_MD4.str_md4()
* soHASHING_MD5.hex_md5()
* soHASHING_MD5.b64_md5()
* soHASHING_MD5.str_md5()
* soHASHING_SHA1.hex_sha1()
* soHASHING_SHA1.b64_sha1( )
* soHASHING_SHA1.str_sha1( )
* soHASHING_SHA256.hex_sha256()
* soHASHING_SHA256.b64_sha256()
* soHASHING_SHA256.str_sha256()

Comme vous pouvez le constater dans cette liste, différentes fonctions sont disponibles pour les différents types de sortie du hachage. Vous pouvez choisir entre `hex_` pour les chiffres hexadécimaux, `b64_` pour la sortie codée en Base64, ou `str_` pour un simple codage de chaîne.

Selon la fonction de hachage choisie, la longueur du hachage varie :

* MD4 : 128 bits
* MD5 : 128 bits
* SHA-1 : 160 bits
* SHA-256 : 256 bits

## Tester les exemples de formulaires PDF {#try-sample-pdf-forms}

Les exemples de fichiers pour cet article incluent deux formulaires PDF. Le premier exemple vous permet de saisir une chaîne, puis de générer des valeurs de hachage MD4, MD5, SHA-1 et SHA-256 pour la chaîne. Le deuxième exemple est un formulaire simple qui déverrouille les champs de texte si un mot de passe correct est saisi.

### Exemple 1 : générer des hachages {#generating-dashes}

Pour tester le premier exemple, procédez comme suit :

1. Après avoir téléchargé et décompressé les fichiers d’exemple, ouvrez hashing_forms_sample1.pdf avec AEM Forms on JEE Designer. Vous pouvez également utiliser Adobe Reader ou Adobe Acrobat Professional pour ouvrir et afficher l’exemple, mais vous ne pouvez pas voir le code source.
1. Dans le champ de texte intitulé [!UICONTROL texte clair], saisissez un mot de passe ou tout autre message que vous souhaitez hacher.
1. Cliquez sur l’un des quatre boutons pour générer le hachage MD4, MD5, SHA-1 ou SHA-256. Selon le bouton sur lequel vous avez appuyé, l’une des quatre fonctions de hachage qui produit la sortie hexadécimale est appelée et votre chaîne ou votre message est haché.

Le résultat de l’opération de hachage s’affiche dans le champ intitulé [!UICONTROL hachage]. La longueur du hachage varie selon la fonction de hachage choisie.

Tous les exemples utilisent des chiffres hexadécimaux comme type de sortie. Vous pouvez utiliser l’éditeur de script pour modifier les exemples et modifier le type de sortie en base64 ou en chaîne simple.

### Exemple 2 : mots de passe correspondants {#matching-passwords}

Le deuxième exemple illustre la comparaison des hachages en arrière-plan, sans avoir à dévoiler le vrai mot de passe. Le mot de passe saisi est haché. Le mot de passe réel, stocké dans un champ invisible, est également haché. Le mot de passe est sécurisé non pas parce qu’il est invisible, mais parce qu’il a été haché. Comme il est impossible de reconstruire le mot de passe à partir de la valeur hachée, il n’est pas risqué d’exposer le mot de passe sous forme de hachage. La comparaison n’est faite qu’entre les hachages, et non entre les mots de passe en texte clair. Si les deux hachages sont identiques, vous pouvez supposer que les mots de passe sont identiques.

Suivez les étapes ci-dessous pour essayer le deuxième exemple :

1. Ouvrez `hashing_forms_sample2.pdf` avec AEM Forms on JEE Designer. Vous pouvez également utiliser Adobe Reader ou Adobe Acrobat Professional pour ouvrir et afficher l’exemple, mais vous ne pouvez pas voir le code source.
1. Sélectionnez l’un des deux champs de mot de passe intitulés [!UICONTROL Password MAN] ou [!UICONTROL Password WOMAN] et saisissez les mots de passe :
   1. Le mot de passe pour Man est `bob`.
   1. Le mot de passe pour Woman est `alice`.
1. Lorsque vous déplacez la sélection hors des champs de mot de passe ou appuyez sur la touche Entrée, le hachage du mot de passe que vous avez saisi est généré automatiquement et comparé au hachage stocké du mot de passe correct en arrière-plan. Les mots de passe corrects et hachés sont stockés dans les champs de texte invisibles intitulés `passwd_man_hashed` et `passwd_woman_hashed`. Si vous saisissez le mot de passe correct pour l’homme, les champs de texte intitulés `Man 1` et `Man 2` sont rendus accessibles afin que vous puissiez y saisir du texte. Le même comportement s’applique aux champs pour la femme.
1. Vous pouvez éventuellement cliquer sur le bouton « supprimer les mots de passe », ce qui désactive les champs de texte et modifie leur bordure.

Le code permettant de comparer les deux valeurs hachées et d’activer les champs de texte est simple :

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## Que faire ensuite {#next-steps}

Où auriez-vous besoin de quelque chose comme ça ? Prenons l’exemple d’un formulaire PDF contenant des champs qui ne doivent être remplis que par des personnes autorisées. En sécurisant ces champs avec un mot de passe qui ne peut être affiché en clair nulle part dans le document comme dans Sample_2.pdf, vous pouvez vous assurer que ces champs sont accessibles uniquement aux utilisateurs et utilisatrices qui connaissent le mot de passe.

Je vous encourage à continuer à explorer les deux exemples de fichiers PDF.  Vous pouvez générer de nouvelles valeurs de hachage avec Sample_1.pdf et utiliser les valeurs générées pour modifier le mot de passe ou la fonction de hachage utilisée dans Sample_2.pdf.  Les ressources répertoriées dans la section Attributions fournissent également des informations supplémentaires sur le hachage et les implémentations JavaScript spécifiques utilisées dans cet article.

## Affectations {#attributions}

* [Ronald Rivest](https://fr.wikipedia.org/wiki/Ronald_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [Collision de hachage](https://fr.wikipedia.org/wiki/Collision_(informatique))
* [Tableau arc-en-ciel](https://fr.wikipedia.org/wiki/Rainbow_table)
* [Page d’accueil du projet JavaScript MD5](https://pajhome.org.uk/crypt/md5/)
* [Page d’accueil du projet jsSHA2](https://anmar.eu.org/projects/jssha2/)
