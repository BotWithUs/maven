# BotWithUs Maven repository

A **static Maven repository** — a plain artifact tree served over GitHub Pages at
<https://botwithus.github.io/maven>. It resolves anonymously: no token, no login,
no `gradle.properties` credentials. (GitHub Packages, by contrast, requires a
personal access token even to *read* a public artifact.)

Do not edit this repository by hand. `bot-api` is written by the
[`Publish bot-api`](https://github.com/BotWithUs/BWUJavaScriptingFramework/blob/master/.github/workflows/publish-api.yml)
workflow in `BotWithUs/BWUJavaScriptingFramework`, which runs when a `v*` tag is
pushed there. The v1 `botwithus-api` is written by a local publish script in
`BotWithUsAPI`, and each release arrives here as a pull request.
The v1 extended API `net.botwithus.xapi.public:api` is published the same way from
[`BwuExtendedPublicAPI`](https://github.com/BotWithUs/BwuExtendedPublicAPI) (Gradle `maven-publish` to a
local checkout of this repository), also as a pull request.

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

Sources and Javadoc jars accompany every `bot-api` release, so IDEs pick up
documentation and step-through sources automatically.

### v1 API

The v1 scripting API is served from the same repository:

```kotlin
repositories {
    mavenCentral()
    maven { url = uri("https://botwithus.github.io/maven") }
}

dependencies {
    implementation("net.botwithus.rs3:botwithus-api:1.0.9")
}
```

Each `botwithus-api` release is the ProGuard-processed jar plus a Javadoc jar.
Its POM lists no dependencies.

## Published artifacts

| Coordinates | Description |
|---|---|
| `com.botwithus:bot-api` | Public scripting API for the BotWithUs Java host |
| `net.botwithus.rs3:botwithus-api` | v1 scripting API |

Available versions are listed in
[`com/botwithus/bot-api/maven-metadata.xml`](com/botwithus/bot-api/maven-metadata.xml)
and
[`net/botwithus/rs3/botwithus-api/maven-metadata.xml`](net/botwithus/rs3/botwithus-api/maven-metadata.xml).

## Guarantees

**Published versions are immutable.** Both publish paths refuse to overwrite a
version that already exists — a bad release is corrected by cutting the next one,
never by replacing an artifact someone may already have resolved and cached.

Nothing is ever deleted, so older releases stay resolvable indefinitely.

Every file is stored byte-for-byte (see `.gitattributes`), so the checksum files
beside each artifact match what is served even when a release is committed from
Windows.

## Licence

Artifacts here are published under the licence of their source project. `bot-api`
is [GPL-3.0](https://github.com/BotWithUs/BWUJavaScriptingFramework/blob/master/LICENSE).
