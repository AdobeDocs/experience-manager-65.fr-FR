---
title: Création de projets AEM à l’aide d’Apache Maven
seo-title: Création de projets AEM à l’aide d’Apache Maven
description: Ce document explique comment configurer un projet AEM basé sur Apache Maven.
seo-description: Ce document explique comment configurer un projet AEM basé sur Apache Maven.
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: add17f46dfb292aeaf8425e5f75cfe955ed93cbc
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 58%

---


# Création de projets AEM à l’aide d’Apache Maven{#how-to-build-aem-projects-using-apache-maven}

## Présentation {#overview}

Ce document explique comment configurer un projet AEM basé sur [Apache Maven](https://maven.apache.org/).

Apache Maven est un outil Open Source destiné à gérer des projets logiciels en automatisant les générations et en fournissant des informations de qualité à leur sujet. Il s’agit de l’outil de gestion des versions recommandé pour les projets AEM.

L’utilisation de Maven pour créer votre projet AEM présente plusieurs avantages :

* Environnement de développement indépendant de l’IDE
* Utilisation des archetypes et des artifacts Maven fournis par Adobe
* Utilisation des jeux d’outils Apache Sling et Apache Felix basés sur les configurations de développement
* Importation aisée dans un IDE ; Eclipse et/ou IntelliJ, par exemple
* Intégration aisée dans les systèmes d’intégration continue

### Maven Project Archetypes {#maven-project-archetypes}

adobe fournit deux archétypes Maven qui peuvent servir de base à vos projets AEM. Pour plus d&#39;informations, consultez les liens ci-dessous :

* [archétype du projet AEM](https://github.com/adobe/aem-project-archetype)
* [Maven archetype for Single Page Applications Starter Kit](https://github.com/adobe/aem-spa-project-archetype)

## Dépendances de l’API Experience Manager {#experience-manager-api-dependencies}

### What is the UberJar? {#what-is-the-uberjar}

&quot;UberJar&quot; est le nom informel donné au fichier spécial d&#39;archives Java (JAR) fourni par l&#39;Adobe. Ces fichiers JAR contiennent toutes les API Java publiques exposées par Adobe Experience Manager. Ils comprennent également des bibliothèques externes limitées, en particulier toutes les API publiques disponibles dans AEM qui proviennent d&#39;Apache Sling, Apache Jackrabbit, Apache Lucene, Google Guava, et deux bibliothèques utilisées pour le traitement d&#39;images (la bibliothèque CYMK JPEG ImageIO de Werner Randelshofer et la bibliothèque d&#39;images TwelveMonkeys). Les variables UberJars contiennent uniquement des interfaces et des classes d&#39;API, ce qui signifie qu&#39;elles contiennent uniquement des interfaces et des classes qui sont exportées par un lot OSGi dans AEM. They also contain a *MANIFEST.MF* file containing the correct package export versions for all of these exported packages, thus ensuring that projects built against the UberJar have the correct package import ranges.

### Why did Adobe create the UberJars? {#why-did-adobe-create-the-uberjars}

Auparavant, les développeurs devaient gérer un nombre relativement élevé de dépendances individuelles par rapport aux différentes bibliothèques AEM. Chaque fois qu’une nouvelle API était utilisée, une ou plusieurs dépendances individuelles devaient être ajoutées au projet. Sur un seul projet, l’introduction du fichier UberJar a entraîné la suppression de 30 dépendances distinctes.

À partir de AEM 6.5, Adobe fournit deux UberJars : l&#39;une qui inclut des interfaces obsolètes et l&#39;autre qui supprime ces interfaces obsolètes. En en référençant explicitement un au moment de la création, les clients sont sûrs de comprendre s’ils dépendent d’un code obsolète.

La seconde variable Uber Jar supprime toutes les classes, méthodes et propriétés obsolètes afin que les clients puissent les compiler et déterminer si le code personnalisé est un BAT futur.

### Quel UberJar utiliser ? {#which-uberjar-to-use}

aem 6.5 est disponible en deux versions d&#39;Uber Jar :

1. Uber Jar - Inclut uniquement les interfaces publiques qui ne sont pas marquées pour la dépréciation. Il s’agit de l’UberJar **recommandé** à utiliser, car il aide les futurs BAT à utiliser le code de base à partir d’API obsolètes.
1. Uber Jar avec des API obsolètes - Inclut toutes les interfaces publiques, y compris celles marquées pour la dépréciation dans une future version d&#39;AEM.

>[!NOTE]
>
>A partir de AEM 6.5.6, UberJar et d’autres artefacts associés sont disponibles dans le référentiel [](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/) Maven Central au lieu du référentiel Adobe Public Maven (repo.adobe.com). Le fichier UberJar principal est renommé `uber-jar-<version>.jar`. Par conséquent, il n’existe aucune `classifier`valeur, avec `apis` comme valeur, pour la `dependency` balise.

### Comment utiliser UberJars ? {#how-do-i-use-the-uberjars}

If you are using Apache Maven as a build system (which is the case for most AEM Java projects), you will need to add one or two elements to your *pom.xml* file. The first is a *dependency* element adding the actual dependency to your project:

**Dépendance Uber Jar *(sans API obsolètes)***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**Dépendance de Jar Uber avec des API obsolètes**

>[!CAUTION]
>
>L’Adobe recommande le déploiement sur le Jar Uber pour que ***ne contienne pas* **les API obsolètes afin de s’assurer que vos applications s’exécuteront correctement sur les versions futures de l’AEM.
>
>N&#39;utilisez Uber Jar avec prise en charge d&#39;API obsolète que si le code qui repose sur les API obsolètes ne peut pas être modifié pour prendre en charge les modifications.

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

If your company is already using a Maven Repository Manager such as Sonatype Nexus, Apache Archiva, or JFrog Artifactory, add the appropriate configuration to your project to reference this repository manager and add Adobe&#39;s Maven repository ([https://repo.maven.apache.org/maven2/](https://repo.maven.apache.org/maven2/)) to your repository manager.

If you are not using a repository manager, then you will need to add a *repository* element to your *pom.xml* file:

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.maven.apache.org/maven2/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.maven.apache.org/maven2/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### What can I do with the UberJar? {#what-can-i-do-with-the-uberjar}

UberJar vous permet de compiler le code de projet qui dépend d’API AEM (et des API utilisées par les projets mentionnés ci-dessus). Vous pouvez également générer des informations SCR (Service Component Runtime) et Metatype OSGi. Vous pouvez également rédiger et exécuter des tests unitaires, moyennant certaines restrictions.

### Quelles sont les limitations du fichier UberJar ? {#what-can-t-i-do-with-the-uberjar}

Because the UberJar contains **only** APIs, it is not executable and cannot be used to **run** Adobe Experience Manager. Pour exécuter AEM, vous avez besoin d’AEM Quickstart, que ce soit sous la forme Autonome ou WAR (Web Application Archive).

### Vous avez mentionné des restrictions sur les tests unitaires. Veuillez donner davantage de précisions. {#you-mentioned-limitations-on-unit-tests-please-explain-further}

En règle générale, les tests unitaires interagissent avec les API du produit de trois manières différentes ; le fichier UberJar ayant, dans chaque cas, une incidence légèrement différente.

#### Scénario d’utilisation n° 1 : Code personnalisé appelant une interface API {#use-case-custom-code-which-calls-a-api-interface}

Ce scénario, qui est le plus courant, implique du code personnalisé qui exécute des méthodes sur une interface Java définie par l’API AEM. Une implémentation de cette interface peut soit être fournie directement, soit être injectée à l’aide du modèle d’injection de dépendances. **Ce scénario d’utilisation peut être traité avec le fichier UberJar.**

Exemple de fourniture directe :

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

Exemple d’utilisation du modèle d’injection :

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

To unit test either of these methods, a developer would use a mocking framework such as [JMockit](http://jmockit.github.io), [Mockito](https://mockito.org/), [JMock](https://www.jmock.org/), or [Easymock](https://easymock.org/) to create a mock object for the AEM API referenced. Ces exemples utilisent JMockit. Cependant, pour ce scénario d’utilisation particulier, la différence entre ces structures est, en grande partie, d’ordre syntaxique.

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### Scénario d’utilisation n° 1 : Code personnalisé appelant une classe d’implémentation API {#use-case-custom-code-which-calls-an-api-implementation-class}

Dans ce scénario d’utilisation, il est fait appel à une méthode d’instance ou statique d’une classe dans l’API AEM où vous faites référence à une classe concrète, contrairement à une interface dans le scénario d’utilisation n° 1.

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**Ce scénario d’utilisation peut être traité avec le fichier UberJar**. Cependant, il est conseillé de simuler l’API lorsque cela s’avère possible pour réaliser des tests performants.

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### Scénario d’utilisation n° 3 : Code personnalisé étendant une classe de base à partir de l’API {#use-case-custom-code-which-extends-a-base-class-from-the-api}

As with SCR Generation, if your code extends a base class (abstract or concrete) from the AEM API, you **must** use the UberJar in order to test it.

## Tâches de développement courantes à l’aide de Maven {#common-development-tasks-with-maven}

### Procédure d’ajout de chemins d’accès au module de contenu {#how-to-add-paths-to-the-content-module}

Le module de contenu inclut un fichier src/main/content/META-INF/vault/filter.xml qui définit les filtres pour le module AEM généré par Maven. Le fichier créé par l’archetype Maven se présente comme suit :

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Ce fichier est utilisé de différentes façons :

* Par `content-package-maven-plugin` pour déterminer le contenu à inclure dans le module
* Par l’outil VLT pour déterminer les chemins d’accès à prendre en compte
* Si le package est recréé dans le gestionnaire de modules AEM, cela définit également les chemins d’accès à inclure

En fonction des besoins de votre application, vous pouvez ajouter ces chemins d’accès afin d’inclure davantage de contenu. Par exemple :

* Configurations du déploiement
* Plans directeurs
* Modèles de workflow
* Pages de conception
* Échantillon de contenu

To add to the paths, add more `<filter>` elements:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### Ajout de chemins d’accès au module sans les synchroniser {#adding-paths-to-the-package-without-syncing-them}

If you have files that should be added to the package that is built by the content-package-maven-plugin but that should not be synchronized between the file system and the repository, you can use `.vltignore` files. Ces fichiers ont la même syntaxe que les fichiers [.gitignore](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).

For example, the archetype uses a `.vltignore` file to prevent the JAR file that is installed as part of the bundle from being synced back to the file system:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### Synchronisation de chemins d’accès sans les ajouter au module {#syncing-paths-without-adding-them-to-the-package}

Dans certains cas, vous pouvez faire en sorte que des chemins d’accès spécifiques restent synchronisés entre le système de fichiers et le référentiel, mais ne pas les inclure dans le module créé pour être installé dans AEM.

A typical case is the `/libs/foundation` path. Dans le cadre du développement, vous pouvez faire en sorte que le contenu de ce chemin d’accès soit disponible dans votre système de fichiers afin que votre IDE, par exemple, puisse résoudre les inclusions JSP qui insèrent des JSP dans `/libs`. However, you don&#39;t want to include that part in the package you build, as the `/libs` part contains product code that must not be modified by custom implementations.

To achieve this, you can provide a file `src/main/content/META-INF/vault/filter-vlt.xml`. If this file exists, it will be used by the VLT tool, e.g. when you perform `vlt up` and `vlt ci`, or when you have set `vlt sync` set up. The content-package-maven-plugin will continue to use the file `src/main/content/META-INF/vault/filter.xml` when creating the package.

For example, to make `/libs/foundation` available locally for development, but only include `/apps/myproject` in the package, use the following two files.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

Vous devez également reconfigurer maven-resources-plugin de sorte qu’il n’inclue pas ces fichiers dans le module : le fichier filter.xml n’est pas appliqué lorsque le module est installé, mais uniquement lorsqu’il est généré à nouveau à l’aide du gestionnaire de modules.

Change the `<resources>` section in the content pom accoringly:

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### Utilisation de JSP {#how-to-work-with-jsps}

La configuration Maven décrite jusqu’à présent crée un module de contenu qui peut également inclure des composants et les JSP correspondants. Cependant, Maven les traite comme n’importe quel autre fichier faisant partie du module de contenu et ne les identifie même pas comme des JSP.

Les composants obtenus fonctionnent tout de même dans AEM, mais le fait que Maven reconnaisse les JSP présente deux avantages majeurs.

* Cela permet à Maven d’échouer si les JSP contiennent des erreurs, de sorte que celles-ci apparaissent au moment de la génération et non lors de leur compilation initiale dans AEM.
* Dans le cas des IDE qui peuvent importer des projets Maven, cela permet également une prise en charge de la bibliothèque de balises et une complétion de code dans les JSP.

Deux opérations sont nécessaires pour activer cette configuration :

1. Ajout de dépendances de bibliothèques de balises
1. Compilation des JSP dans le cadre du processus de compilation Maven

#### Ajout de dépendances de bibliothèques de balises {#adding-tag-library-dependencies}

Les dépendances ci-dessous doivent être ajoutées au POM des modules `content`.

>[!NOTE]
>
>Unless you are importing the product dependencies as described in [Importing AEM Product Dependencies](#importingaemproductdependencies) above, they also need to be added to the parent POM along with the version matching your AEM setup as described in [Adding Dependencies](#addingdependencies) above. Les commentaires de chaque entrée ci-dessous indiquent le module à rechercher dans Dependency Finder.

>[!NOTE]
>
>L’artifact `com.adobe.granite.xssprotection` n’est pas inclus dans le POM cq-quickstart-product-dependencies et nécessite des coordonnées Maven complètes, telles qu’elles sont générées par Dependency Finder.

#### Compilation des JSP dans le cadre de la phase de compilation Maven {#compiling-jsps-as-part-of-the-maven-compile-phase}

To compile JSPs in Maven&#39;s `compile` phase, we use Apache Sling&#39;s [Maven JspC Plugin](https://sling.apache.org/documentation/development/jspc.html) as shown below:

* Nous configurons une exécution pour l’objectif `jspc` (qui, par défaut, est associé à la phase `compile`, de sorte que la phase ne doive pas être spécifiée explicitement).

* we tell it to compile any JSPs in `${project.build.directory}/jsps-to-compile`
* and output the result to `${project.build.directory}/ignoredjspc` (which translates to `myproject/content/target/ignoredjspc`)

* we set up maven-resources-plugin to copy the JSPs to `${project.build.directory}/jsps-to-compile` in the generate-sources phase and configure it to not copy the `libs/` folder (because that is AEM product code and we neither want to incur the dependencies for compilation for our project, nor do we need to validate that it compiles.

Comme indiqué précédemment, notre objectif principal consiste à valider les pages JSP et à nous assurer que le processus de génération échoue si elles contiennent des erreurs. C’est la raison pour laquelle nous les compilons dans un répertoire distinct qui est ignoré (et, en fait, supprimé immédiatement après, comme vous le verrez dans quelques instants).

Le résultat du module externe JspC Maven JspC peut également être mis en package et déployé dans le cadre d’un lot OSGi. Cependant, cette opération, qui présente d’autres implications et effets secondaires, va au-delà de l’objectif recherché qui consiste à valider les pages JSP.

Pour parvenir à la suppression des classes compilées à partir des pages JSP, nous allons configurer le module externe Maven Clean comme illustré ci-dessous. If you want to inspect the result of the Maven JspC Plugin, run `mvn compile` in `myproject/content` -- after that, you will find the result in `myproject/content/target/ignoredjspc`).

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>Depending on whether you actually make use of JSP code in `/libs` (i.e. include JSPs from there), you will need to refine which JSPs are copied for compilation.
>
>E.g. if you include `/libs/foundation/global.jsp`, you can use the following configuration for the `maven-resources-plugin` instead of the configuration above which completely skips over `/libs`.
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### Utilisation des systèmes SCM {#how-to-work-with-scm-systems}

Lorsque vous utilisez des systèmes SCM (Source Configuration Management), vous devez veiller à ce que :

* le VCS ignore les artifacts non sources dans le système de fichiers,
* VLT ignore les artifacts du VCS et ne les vérifie pas dans le référentiel.

>[!NOTE]
>
>L’objet de cette section n’est pas de décrire la configuration de Maven en vue de le faire fonctionner avec votre système SCM. Cette procédure est décrite en détail à la section [Référence POM Maven](https://maven.apache.org/pom.html#SCM) et dans la [documentation du module externe Maven SCM](https://maven.apache.org/scm/).

#### Motifs à exclure de SCM {#patterns-to-exclude-from-scm}

Vous trouverez, ci-dessous, une liste type des motifs à exclure de SCM. E.g., if you are using git, you can add these to your project&#39;s `.gitignore` file.

#### Exemple de fichier .gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### Ignorer les fichiers de contrôle SCM dans VLT {#ignoring-scm-control-files-in-vlt}

Dans certains cas, l’arborescence de source de contenu peut inclure des fichiers de contrôle SCM qui ne doivent pas être archivés dans le référentiel.

Veuillez tenir compte du scénario ci-dessous :

L’archetype a déjà créé un fichier .vltignore pour empêcher le fichier JAR installé dans le cadre du lot d’être resynchronisé avec le système de fichiers :

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

Bien évidemment, vous ne souhaitez pas non plus que ce fichier se trouve dans votre système SCM. Par conséquent, si vous utilisez git, par exemple, vous allez ajouter un `gitignore` approuvé:

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

Étant donné que le fichier `gitignore` ne doit pas résider non plus dans le référentiel, le fichier `vltignore`.  doit être étendu afin d’inclure le `gitignore` approuvé:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### Utilisation de profils de déploiement {#how-to-work-with-deployment-profiles}

Si votre processus de génération fait partie d’une configuration de gestion du cycle de vie de développement plus vaste, comme un processus d’intégration continue, vous êtes souvent amené à effectuer un déploiement sur d’autres ordinateurs, et pas seulement sur l’instance locale du développeur.

Dans ce cas, vous pouvez facilement ajouter de nouveaux [profils de génération Maven](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) au POM du projet.

L’exemple ci-dessous ajoute un profil `integrationServer` qui redéfinit les noms d’hôte et les ports pour les instances de création et de publication. Vous pouvez effectuer un déploiement sur ces serveurs en exécutant Maven à partir de la racine du projet, comme illustré ci-dessous.

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### Utilisation d’AEM Communities {#how-to-work-with-aem-communities}

En cas d’utilisation sous-licence pour la fonctionnalité AEM Communities, un fichier jar d’API supplémentaire est nécessaire.

Pour plus d’informations, voir [Utilisation de Maven pour Communities](/help/communities/maven.md).
