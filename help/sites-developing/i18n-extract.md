---
title: Extraction de chaînes pour la traduction
seo-title: Extracting Strings for Translating
description: Utilisez xgettext-maven-plugin pour extraire de votre code source les chaînes qui doivent être traduites.
seo-description: Use xgettext-maven-plugin to extract strings from your source code that need translating
uuid: 2c586ecb-8494-4f8f-b31a-1ed73644d611
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: 034f70f1-fbd2-4f6b-b07a-5758f0461a5b
exl-id: 4acc5f7f-0bcb-4b5a-8531-52e146cffeae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 71%

---

# Extraction de chaînes pour la traduction{#extracting-strings-for-translating}

Utilisez xgettext-maven-plugin pour extraire de votre code source les chaînes qui doivent être traduites. Le module externe Maven extrait les chaînes dans un fichier XLIFF que vous envoyez en traduction. Les chaînes sont extraites aux emplacements suivants :

* Fichiers sources Java.
* Fichiers sources JavaScript
* Représentations XML de ressources SVN (nœuds JCR)

## Configuration de l’extraction de chaînes {#configuring-string-extraction}

Configurez la manière dont l’outil xgettext-maven-plugin extrait des chaînes pour votre projet.

```xml
/filter { }
/parsers {
   /vaultxml { }
   /javascript { }
   /regexp {
      /files {
         /java { }
         /jsp { }
         /extjstemplate { }
      }
   }
}
/potentials { }
```

| Section | Description |
|---|---|
| /filter | Identifie les fichiers qui sont analysés. |
| /parsers/vaultxml | Configure l’analyse des fichiers Vault. Identifie les nœuds JCR contenant des indices de localisation et des chaînes externalisées. Identifie également les nœuds JCR à ignorer. |
| /parsers/javascript | Identifie les fonctions JavaScript qui externalisent les chaînes. Il n’est pas nécessaire de modifier cette section. |
| /parsers/regexp | Configure l’analyse des fichiers de modèle Java, JSP et ExtJS. Il n’est pas nécessaire de modifier cette section. |
| /potentials | Formule de détection des chaînes à internationaliser. |

### Identification des fichiers à analyser {#identifying-the-files-to-parse}

La section /filter du fichier i18n.any identifie les fichiers analysés par l’outil xgettext-maven-plugin. Ajoutez plusieurs règles d’inclusion et d’exclusion qui identifient les fichiers qui sont analysés et ignorés, respectivement. Vous devez inclure tous les fichiers, puis exclure ceux que vous ne souhaitez pas analyser. En règle générale, vous excluez les types de fichiers qui n’appartiennent pas à l’interface utilisateur ou ceux qui définissent l’interface utilisateur, mais qui ne sont pas traduits. Les règles d’inclusion et d’exclusion présentent le format suivant :

```
{ /include "pattern" }
{ /exclude "pattern" }
```

La partie « pattern » d’une règle est utilisée pour faire correspondre les noms des fichiers à inclure ou à exclure. Le préfixe de motif indique si vous effectuez une correspondance avec un nœud JCR (sa représentation dans Vault) ou le système de fichiers.

| Préfixe | Effet |
|---|---|
| / | Indique un chemin JCR. Par conséquent, ce préfixe correspond aux fichiers situés dans le répertoire jcr_root. |
| &amp;ast; | Indique un fichier normal sur le système de fichiers. |
| aucune | Aucun préfixe, ou modèle commençant par un nom de fichier ou de dossier, n’indique un fichier normal sur le système de fichiers. |

Lorsqu’il est utilisé dans un modèle, le caractère / indique un sous-répertoire et &amp;ast; correspond à tous les caractères. Le tableau suivant répertorie plusieurs exemples de règles.

<table>
 <tbody>
  <tr>
   <th>Exemple de règle</th>
   <th>Effet</th>
  </tr>
  <tr>
   <td><code>{ /include "*" }</code></td>
   <td>Inclure tous les fichiers.</td>
  </tr>
  <tr>
   <td><code>{ /exclude "*.pdf" }</code></td>
   <td>Exclure tous les fichiers du PDF.</td>
  </tr>
  <tr>
   <td><code> { /exclude "*/pom.xml" }</code></td>
   <td>Exclure les fichiers POM.</td>
  </tr>
  <tr>
   <td><code class="code">{ /exclude "/content/*" }
      { /include "/content/catalogs/geometrixx/templatepages" }
      { /include "/content/catalogs/geometrixx/templatepages/*" }</code></td>
   <td><p>Excluez tous les fichiers sous le noeud /content .</p> <p>Incluez le noeud /content/catalogs/geometrixx/templatepages .</p> <p>Incluez tous les noeuds enfants de /content/catalogs/geometrixx/templatepages.</p> </td>
  </tr>
 </tbody>
</table>

### Extraction des chaînes  {#extracting-the-strings}

Aucun POM :

```shell
mvn -N com.adobe.granite.maven:xgettext-maven-plugin:1.2.2:extract  -Dxgettext.verbose=true -Dxgettext.target=out -Dxgettext.rules=i18n.any -Dxgettext.root=.
```

Avec un POM : ajoutez ceci au POM :

```xml
<build>
    <plugins>
        <plugin>
            <groupId>com.adobe.granite.maven</groupId>
            <artifactId>xgettext-maven-plugin</artifactId>
            <version>1.1</version>
            <configuration>
                <rules>i18n.any</rules>
                <root>jcr_root</root>
                <xliff>cq.xliff</xliff>
                <verbose>true</verbose>
            </configuration>
        </plugin>
    </plugins>
</build>
```

La commande :

```shell
mvn xgettext:extract
```

### Fichiers de sortie {#output-files}

* `raw.xliff`: chaînes extraites
* `warn.log`: les avertissements (le cas échéant), si `CQ.I18n.getMessage()` L’API n’est pas utilisée correctement. Une correction est toujours nécessaire, suivie d’une nouvelle exécution.

* `parserwarn.log` : avertissements de l’analyseur (le cas échéant) ; problèmes de l’analyseur js, par exemple
* `potentials.xliff` : candidats « potentiels » qui ne sont pas extraits, mais il peut s’agir de chaînes lisibles qui doivent être traduites (peuvent être ignorées ; produisent toujours un grand nombre de faux positifs)
* `strings.xliff` : fichier xliff aplati, à importer dans ALF
* `backrefs.txt` : permet de rechercher rapidement une chaîne donnée dans des emplacements de code source
