---
title: Comment générer et utiliser des hachages dans les PDF forms dynamiques ?
description: Génération et utilisation de hachages dans les PDF forms dynamiques
source-git-commit: 730ae7cd6cd04eb6377b37eafe29db597e93cce3
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Génération et utilisation de hachages dans les PDF forms dynamiques {#generate-work-with-hashes-dynamic-pdf-forms}


## Connaissances préalables {#prerequisite-knowledge}

Une certaine expérience avec AEM Forms on JEE Designer est requise, de même que la possibilité d’accéder à des fonctions et d’en appeler dans des objets de script.

## Niveau d’utilisateur {#user-level}

Début

Lorsque vous souhaitez masquer un mot de passe dans votre formulaire PDF et que vous ne souhaitez pas le placer en texte clair dans le code source ou ailleurs dans le document PDF, il est essentiel de savoir comment générer et utiliser les hachages MD4, MD5, SHA-1 et SHA-256.

L’idée est d’obscurcir le mot de passe en générant un hachage unique et de stocker ce hachage dans le document PDF. Ce hachage unique peut être généré par différentes fonctions de hachage. Dans cet article, je vous montrerai comment les générer dans le formulaire PDF et comment les utiliser.

Une fonction de hachage utilise une longue chaîne (ou un message) de n’importe quelle longueur comme entrée et produit une chaîne de longueur fixe comme sortie, parfois appelée condensé du message ou empreinte numérique.

AEM Forms on JEE Designer vous permet de mettre en oeuvre les différentes fonctions de hachage dans les objets de script en tant que JavaScript et de les exécuter dans un document PDF dynamique. Les exemples de fichiers PDF inclus dans les fichiers d’exemple pour cet article utilisent des implémentations open source des fonctions de hachage suivantes :

* MD4 et MD5 - conçus par Ronald Rivest

* SHA-1 et SHA-256, tels qu’ils sont définis par le NIST

L’utilisation des hachages a pour principal avantage de ne pas avoir à comparer directement les mots de passe en comparant les chaînes de texte claires ; vous pouvez comparer les deux hachages des deux mots de passe. Comme il est très peu probable que deux chaînes différentes aient le même hachage, si les deux hachages sont identiques, alors vous pouvez supposer que les chaînes comparées (dans ce cas, les mots de passe) sont également identiques.

>[!NOTE]
>
>Il existe des problèmes de sécurité bien connus (appelés collisions de hachage) avec MD4 ou MD5. En raison de ces collisions de hachage et d’autres hacks SHA-1 (y compris les tables arc-en-ciel), j’ai décidé de me concentrer sur la fonction de hachage SHA-256 dans le deuxième échantillon.  Pour plus d’informations, voir les pages [Collision](https://en.wikipedia.org/wiki/Hash_collision) et [Tableau arc-en-ciel](https://en.wikipedia.org/wiki/Rainbow_table) de Wikipedia.

## Examen des objets de script {#examining-script-objects}

Lorsque vous ouvrez l’un des deux exemples fournis dans AEM Forms on JEE Designer, les quatre objets de script sont répertoriés dans la palette Hiérarchie (voir la figure ci-dessous).

![Variables](assets/variables.jpg)

Pour afficher l’implémentation JavaScript des fonctions de hachage dans ces objets de script, sélectionnez l’objet de script et explorez le code dans l’éditeur de script.  Vous pouvez voir comment chacune des fonctions de hachage suivantes a été implémentée :

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

Comme vous pouvez le constater dans cette liste, différentes fonctions sont disponibles pour les différents types de sortie du hachage. Vous pouvez choisir entre `hex_` pour les chiffres hexadécimaux, `b64_` pour la sortie codée Base64, ou `str_` pour le codage de chaîne simple.

Selon la fonction de hachage choisie, la longueur du hachage varie :

* MD4 : 128 bits
* MD5 : 128 bits
* SHA-1 : 160 bits
* SHA-256 : 256 bits

## Tester les exemples de PDF forms {#try-sample-pdf-forms}

Les exemples de fichiers pour cet article incluent deux PDF forms. Le premier exemple vous permet de saisir une chaîne, puis de générer des valeurs de hachage MD4, MD5, SHA-1 et SHA-256 pour la chaîne.  Le deuxième exemple est un formulaire simple qui déverrouille les champs de texte si un mot de passe correct est saisi.

### Exemple 1 :  génération de hachages {#generating-dashes}

Pour tester le premier exemple, procédez comme suit :

1. Après avoir téléchargé et décompressé les fichiers d’exemple, ouvrez hashing_forms_sample1.pdf avec AEM Forms on JEE Designer. Vous pouvez également utiliser Adobe Reader ou Adobe Acrobat Professional pour ouvrir et afficher l’exemple, mais vous ne pourrez pas voir le code source.
1. Dans le champ de texte intitulé [!UICONTROL clear text] , saisissez un mot de passe ou tout autre message que vous souhaitez hacher.
1. Cliquez sur l’un des quatre boutons pour générer le hachage MD4, MD5, SHA-1 ou SHA-256. Selon le bouton sur lequel vous avez appuyé, l’une des quatre fonctions de hachage qui produit la sortie hexadécimale est appelée et votre chaîne ou votre message est haché.

Le résultat de l’opération de hachage s’affiche dans le champ intitulé [!UICONTROL hash]. La longueur du hachage varie en fonction de la fonction de hachage choisie.

Tous les exemples utilisent des chiffres hexadécimaux comme type de sortie. Vous pouvez utiliser l’éditeur de script pour modifier les exemples et modifier le type de sortie en Base64 ou chaîne simple.

### Exemple 2 :  mots de passe correspondants {#matching-passwords}

Le deuxième exemple illustre la comparaison des hachages en arrière-plan, sans avoir à dévoiler le vrai mot de passe. Le mot de passe saisi est haché. Le mot de passe réel, stocké dans un champ invisible, est également haché. Le mot de passe est sécurisé non pas parce qu’il est invisible, mais parce qu’il a été haché. Comme il est impossible de reconstruire le mot de passe à partir de la valeur hachée, il est sans risque d’exposer le mot de passe sous forme de hachage. La comparaison n’est faite qu’entre les hachages, et non entre les mots de passe en texte clair. Si les deux hachages sont identiques, vous pouvez supposer que les mots de passe sont identiques.

Suivez les étapes ci-dessous pour essayer le deuxième exemple :

1. Ouvrez `hashing_forms_sample2.pdf` avec AEM Forms on JEE Designer. Vous pouvez également utiliser Adobe Reader ou Adobe Acrobat Professional pour ouvrir et afficher l’exemple, mais vous ne pourrez pas voir le code source.
1. Sélectionnez l’un des deux champs de mot de passe intitulés [!UICONTROL Password MAN] ou [!UICONTROL Password WOMAN] et saisissez les mots de passe :
   1. Le mot de passe de l’homme est `bob`
   1. Le mot de passe de la femme est `alice`
1. Lorsque vous déplacez la sélection hors des champs de mot de passe ou appuyez sur la touche Entrée, le hachage du mot de passe que vous avez saisi est généré automatiquement et comparé au hachage stocké du mot de passe correct en arrière-plan. Les mots de passe corrects et hachés sont stockés dans les champs de texte invisibles intitulés `passwd_man_hashed` et `passwd_woman_hashed`. Si vous saisissez le mot de passe correct pour l’homme, les champs de texte intitulés `Man 1` et `Man 2` sont rendus accessibles afin que vous puissiez y saisir du texte. Le même comportement s’applique aux champs de la femme.
1. Vous pouvez éventuellement cliquer sur le bouton &quot;supprimer les mots de passe&quot;, ce qui désactive les champs de texte et modifie leur bordure.

Le code permettant de comparer les deux valeurs hachées et d’activer les champs de texte est simple :

```xml
if (soHASHING_SHA256.hex_sha256(this.rawValue) == passwd_man_hashed.rawValue){
     VAL_man_1.access = "open";
     VAL_man_2.access = "open";
     VAL_man_1.borderColor = "0,255,0";
     VAL_man_2.borderColor = "0,255,0";
}
```

## Où aller d&#39;ici {#next-steps}

Où auriez-vous besoin de quelque chose comme ça ? Prenons l’exemple d’un formulaire PDF contenant des champs qui ne doivent être remplis que par des personnes autorisées. En sécurisant ces champs avec un mot de passe, qui ne peut être affiché en clair nulle part dans le document comme dans Sample_2.pdf, vous pouvez vous assurer que ces champs sont accessibles uniquement aux utilisateurs qui connaissent le mot de passe.

Je vous encourage à continuer à explorer les deux fichiers PDF d’exemple.  Vous pouvez générer de nouvelles valeurs de hachage avec Sample_1.pdf et utiliser les valeurs générées pour modifier le mot de passe ou la fonction de hachage utilisée dans Sample_2.pdf.  Les ressources répertoriées dans la section Attributions fournissent également des informations supplémentaires sur le hachage et les mises en oeuvre JavaScript spécifiques utilisées dans cet article.

## Attributions {#attributions}

* [Ronald Rivest](https://en.wikipedia.org/wiki/Ron_Rivest)
* [NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines)
* [collision de hachage](https://en.wikipedia.org/wiki/Hash_collision)
* [Table arc-en-ciel](https://en.wikipedia.org/wiki/Rainbow_table)
* [Page d’accueil du projet JavaScript MD5](http://pajhome.org.uk/crypt/md5/)
* [Page d’accueil du projet jsSHA2](https://anmar.eu.org/projects/jssha2/)


