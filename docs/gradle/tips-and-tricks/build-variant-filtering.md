# Filter Build Variants

Gradle allows configuring build variants by changing **Build Types**, **Product Flavors** and **Dimensions** which could create a boatload of variants which we don't want. we can use the following code to filter them out and remove the useless ones:

=== "Groovy"

    ```groovy   
    android {
        // ...
        variantFilter { variant ->
            // this is a list because if we apply dimensions, each variant we consists
            // of multiple flavors
            def names = variant.flavors*.name
            // not we check the conditions that we want...
            if ((names.contains("direct") && variant.buildType.name == "debug")) {
                variant.ignore = true // setting this to true we make the variant go away :)
            }
        }
    }
    ```

=== "Kotlin"

    ```kotlin
    android {
        // ...
    }
    // note that this is a sibling of android block
    androidComponents {
        beforeVariants { variantBuilder ->
            // change the condition to whatever you want
            // name is the fullName of variant, consisting of flavors and build type
            if(variantBuilder.name == "something") {
                variantBuilder.enable = false // setting this to false we make the variant go away :)
            }
        }
    }
    ```

## Reference

[developer.android: Configure Build Variants](https://developer.android.com/build/build-variants)