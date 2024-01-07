# Jvm Builds

## Evolution of Build Tools

As with everything, build tools evolve over time. if we consider a car at the beginning, it only has Accelerate, Turn and Brake which are basic things a car needs. But overtime more things are are added to the cars like Seat Belts, Self Parking, etc.

![Evolution of Cars](./assets/car-revolution.png)

As you can see in the following image, at the beginning build tools only consisted of basic features which are a way to compile the app, run application tests and package the app.


<figure markdown>

  ![Build Tool Evolution Basic](./assets/build-tool-evolution-basic.png){ width="300" }

</figure>

and as time passed more features were added to build systems Dependency Management, Static code analysis and Test Grouping.

![Build Tool Evolution Over time](./assets/build-tool-evolution-over_time.png)

They are evolving continuously to Help us create code better and they do a lot of heavy lifting behind the scenes like dependency management.

## Gradle JVM Plugins

As you (should) know gradle by itself provide minimal configuration and most thing are added to it by applying plugins. The same goes for java and other jvm languages kotlin, groovy and scala.

In this section we check common used plugins in jvm builds for java, kotlin, groovy and scala languages.

### Java Plugins

For **java** there are 3 main plugins when it comes to java: `java` plugin, `java-library` plugin and `application` plugin

- **`java`** plugin

    This plugin is the base java plugin which provides **source code locations** for java which are called SourceSets.
    
    -   `src/main/java`
    -   `src/test/java`

    adds tasks like **compileJava** and **test** for compiling the source codes and running tests respectively  

- **`java-library`** plugin

    This plugins applies the java plugin automatically which means by applying it we will have everything the java plugin has.
    
    Add **api** dependency configuration which will talk more about it later.

- **`application`** plugin

    This plugins applies the java plugin automatically which means by applying it we will have everything the java plugin has.

    Adds build configuration to determine _main_ class

    Adds **run** and **package** tasks to run the application (via the main class provided) and package the app respectively

- **kotlin** plugin

    It is `org.jetbrains.kotlin.jvm` plugin which is maintained by jetbrains.

    This plugins applies the java plugin automatically which means by applying it we will have everything the java plugin has.

    Adds sourceSets for **kotlin** code which can be used along side normal java sourceSets:

    - `src/main/kotlin`
    - `src/test/kotlin`

    !!! warning ""

        Never put `java` files inside kotlin sourceSets. they will not be compiled. put them in the appropriate java sourceSet (`src/main/java` or `src/test/java`)

    Adds **CompileKotlin** task to compile kotlin code.

    `java-library` and `application` plugins can be applied along side this plugin to add more functionality.
    
- **`groovy`** plugin

    This plugin extends the `java` plugin.

    Adds sourceSets for **kotlin** code which can be used along side normal java sourceSets:
    
    - `src/main/groovy`
    - `src/test/groovy`

    Adds **CompileGroovy** task to compile groovy code.

    Can be used along side java.

    `java-library` and `application` plugins can be applied along side this plugin to add more functionality.

- **`scala`** plugin

    This plugin extends the `java` plugin.

    Adds sourceSets for **kotlin** code which can be used along side normal java sourceSets:
    
    - `src/main/scala`
    - `src/test/scala`

    Adds **CompileScala** task to compile scala code.

    Can be used along side java.

    `java-library` and `application` plugins can be applied along side this plugin to add more functionality.
