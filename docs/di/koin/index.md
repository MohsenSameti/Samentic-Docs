# Koin

## References

- [Koin Framework for Dependency Injection (Part-1) — Most Underrated Framework](https://nameisjayant.medium.com/koin-framework-for-dependency-injection-part-1-most-underrated-framework-8cdc1fa5781d)
- [Koin Framework- Provide Interface Dependency (Part-2)- Most Underrated Framework](https://nameisjayant.medium.com/koin-framework-provide-interface-dependency-part-2-most-underrated-framework-40809a21fbcc)

## Koin 

### Basic Usage

This is a summery of *Koin Framework for Dependency Injection (Part-1)*

- Step 1: Provide classes using **modules**:

    ```kotlin
    class Car(private val engine: Engine, private val wheels: Wheels)

    class Wheels

    class Engine

    val carModule = module {
        factory { Engine() }

        factory { Wheels() }

        single { Car(get(), get()) }
    }
    ```

    **factory** methods create a new class on each request while **single** class create the class first time requested then cache it.

    **get()** eagerly creates the class needed

- Step 2: Create a component for access (implement KoinComponent interface)

    ```kotlin
    class CarComponent : KoinComponent {
        //lazily initialisation
        val car: Car by inject()    
        //eagerly initialisation
        val car1:Car = get()    
        // or
        fun car2(): Car = get()
    }

    class SomeCls {
        init {
            CarComponent().car2()
        }
    }
    ```

- Step3: Make sure you call `startKoin` (and pass modules) before using components:

    ```kotlin
    fun main() {
        startKoin {
            modules(carModule) // takes a vararg of mudules
        }
        // now we can use this!
        CarComponent().car2()
    }

    ```

### Provide Interfaces

    This is a summery of *Koin Framework for Dependency Injection (Part-2)*

    Providing interface is used through the **bind**/**binds** methods:

    ```kotlin
    interface UserOne{}
    interface UserTwo{}

    class MainUser: UserOne, UserTwo{}

    module {
        // factory { MainUser(/*...*/) } bind UserOne::class
        factory { MainUser(/*...*/) } binds arrayOf(UserOne::class, UserTwo::Class)
    }
    ```

    There are two other ways to provide interfaces. check article for those.