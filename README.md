# BotWithUs Maven repository

A **static Maven repository** — a plain artifact tree served over GitHub Pages at
<https://botwithus.github.io/maven>. It resolves anonymously: no token, no login,
no `gradle.properties` credentials. (GitHub Packages, by contrast, requires a
personal access token even to *read* a public artifact.)

Do not edit this repository by hand. Its contents are written by the
[`Publish bot-api`](https://github.com/BotWithUs/BWUJavaScriptingFramework/blob/master/.github/workflows/publish-api.yml)
workflow in `BotWithUs/BWUJavaScriptingFramework`, which runs when a `v*` tag is
pushed there.

## Using it

```kotlin
repositories {
    mavenCentral()
    maven { url = uri("https://botwithus.github.io/maven") }
}

dependencies {
    implementation("com.botwithus:bot-api:1.0.0")
}
```

Maven:

```xml
<repositories>
  <repository>
    <id>botwithus</id>
    <url>https://botwithus.github.io/maven</url>
  </repository>
</repositories>
```

Sources and Javadoc jars accompany every release, so IDEs pick up documentation
and step-through sources automatically.

## Published artifacts

| Coordinates | Description |
|---|---|
| `com.botwithus:bot-api` | Public scripting API for the BotWithUs Java host |

Available versions are listed in
[`com/botwithus/bot-api/maven-metadata.xml`](com/botwithus/bot-api/maven-metadata.xml).

## Guarantees

**Published versions are immutable.** The publish workflow refuses to overwrite a
version that already exists — a bad release is corrected by cutting the next one,
never by replacing an artifact someone may already have resolved and cached.

Nothing is ever deleted, so older releases stay resolvable indefinitely.

## Licence

Artifacts here are published under the licence of their source project. `bot-api`
is [GPL-3.0](https://github.com/BotWithUs/BWUJavaScriptingFramework/blob/master/LICENSE).
