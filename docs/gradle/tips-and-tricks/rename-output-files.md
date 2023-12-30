# Rename Output Files

This fllowing code snippets allow you to change the generated apk and bundle files so you do not have to build it automatically.

## Apk

if we want to change the name of the generated apk files for all build variants we can use android.applicationVariants block:

=== "Groovy"

    ``` groovy
    android {
        // ...
        applicationVariants.all { variant ->
            variant.outputs.all {
                outputFileName = "MyName.apk" // put apk name here
            }
        }
    }
    ```

=== "Kotlin"

    ``` kotlin
    android {
        // ...
        applicationVariants.all {
            // the case is necessary to be able to access outputFileName
            outputs.map { it as com.android.build.gradle.internal.api.BaseVariantOutputImpl }
                .forEach { variant ->
                    variant.outputFileName = "MyName.apk"
                }
        }
    }
    ```

Another solution for kotlin dsl can be found [here](https://gist.github.com/ychescale9/fffef60e49de36375698997b277fab9d)!

---

## Bundles

=== "Groovy"

    ```groovy
    // DO NOT FORGET THIS. put if at the top of gradle file!
    import com.android.build.gradle.internal.tasks.FinalizeBundleTask
    // ...
    android {
        // ...
        applicationVariants.all {
            tasks.named("sign${variant.name.capitalize()}Bundle", FinalizeBundleTask) {
                val artifactName = "MyBundle" // change to whatever you want
                File file = finalBundleFile.asFile.get()
                File finalFile = new File(file.parentFile, "${artifactName}.aab")
                finalBundleFile.set(finalFile)
            }
        }
    }
    ```

=== "Kotlin"

    ```kotlin
    // DO NOT FORGET THIS. put if at the top of gradle file!
    import com.android.build.gradle.internal.tasks.FinalizeBundleTask
    // ...
    android {
        // ...
        applicationVariants.all {
            val variant = this
            tasks.named("sign${variant.name.capitalize()}Bundle", FinalizeBundleTask::class) {
                val artifactName = "MyBundle" // change to whatever you want
                val file = finalBundleFile.asFile.get()
                val finalFile = File(file.parentFile, "${artifactName}.aab")
                finalBundleFile.set(finalFile)
            }
        }
    }
    ```

