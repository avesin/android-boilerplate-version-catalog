# Android Core Version Catalog

`core.versions.toml` is a **shared dependency catalog** for Android projects.
It provides a centralized place to manage commonly used libraries and plugin versions for modern Android development.

The goal is to **remove boilerplate setup** when creating new Android applications and ensure **consistent dependency versions** across projects.

---

## Features

This catalog includes dependencies for a typical modern Android stack:

* Kotlin
* Jetpack Compose
* Coroutines
* Hilt (Dependency Injection)
* Room (Database)
* Retrofit (Networking)
* OkHttp (HTTP client)
* Coil (Image loading)
* Navigation Compose
* Lifecycle
* DataStore
* Testing libraries

This setup supports a common architecture such as:

```
MVVM
Jetpack Compose
Hilt DI
Room Database
Retrofit Networking
Repository Pattern
```

---

## File Location

The catalog is typically stored inside the Gradle directory:

```
project
 ├─ gradle
 │   └─ core.versions.toml
 ├─ settings.gradle.kts
 └─ app
```

---

## Setup

Register the catalog inside `settings.gradle.kts`.

```kotlin
dependencyResolutionManagement {

    versionCatalogs {

        create("coreLibs") {
            from(files("gradle/core.versions.toml"))
        }

    }

}
```

After this, the catalog will be available as `coreLibs` inside Gradle build scripts.

---

## Usage

### Plugins

```kotlin
plugins {
    alias(coreLibs.plugins.android.application)
    alias(coreLibs.plugins.kotlin.android)
    alias(coreLibs.plugins.compose)
    alias(coreLibs.plugins.ksp)
    alias(coreLibs.plugins.hilt)
}
```

### Dependencies

```kotlin
dependencies {

    implementation(platform(coreLibs.compose.bom))

    implementation(coreLibs.compose.ui)
    implementation(coreLibs.compose.material3)

    implementation(coreLibs.coroutines.android)

    implementation(coreLibs.hilt.android)
    ksp(coreLibs.hilt.compiler)

    implementation(coreLibs.room.runtime)
    implementation(coreLibs.room.ktx)
    ksp(coreLibs.room.compiler)

    implementation(coreLibs.retrofit)
    implementation(coreLibs.retrofit.gson)

    implementation(coreLibs.coil.compose)
}
```

---

## Why Use a Version Catalog

Using a shared version catalog provides several advantages:

* Centralized dependency version management
* Easier upgrades across multiple projects
* Cleaner `build.gradle.kts` files
* Reduced dependency duplication
* Consistent tooling versions across apps

---

## Recommended Project Stack

This catalog is designed to support the following architecture:

```
data/
network/
database/
repository/
di/
ui/
viewmodel/
navigation/
```

Technologies included:

* Jetpack Compose
* MVVM
* Hilt Dependency Injection
* Room Database
* Retrofit Networking
* Coroutines
* Navigation Compose

---

## License

This catalog can be freely used as a base dependency configuration for Android projects.
