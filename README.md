# Babel

> String-based internationalization (i18n) for Scala applications

## Features

- First class support for plurals
- Great fit for Scala.js clients, since `java.util.Locale` is not used
- Translation definitions in either code or a supported serialization format (e.g. JSON)
- Allows lifting translations into data classes: no more `String` key look-ups
- Creating translation subsets that are only suitable for a specific language, which can be useful for clients that request all translations for a single language 
- Open to arbitrary `String` formatting solutions (e.g. `String.format` or `java.util.MessageFormat`)
- Dependency-free `core` module

## Installation

Dependency-free core module, that contains all data class definitions, type classes and pre-defined locales

```scala
"io.taig" %%% "babel-core" % "x.y.z" 
```
JSON serialization and deserialization

```scala
"io.taig" %%% "babel-circe" % "x.y.z"
```

Reading serialized language definitions from resources (JVM only)

```scala
"io.taig" %% "babel-loader" % "x.y.z"
```

Codecs to populate custom translation data classes

```scala
"io.taig" %%% "babel-generic" % "x.y.z"
```

String formatting choices, pick one or role your own

> Please note that `java.util.MessageFormat` is not available for Scala.js, so the `printf` module is recommended

```scala
"io.taig" %%% "babel-formatter-printf" % "x.y.z"
"io.taig" %% "babel-formatter-message-format" % "x.y.z"
```

Default setup which is assumed in the documentation below

```scala
"io.taig" %% "babel-loader" % "x.y.z"
"io.taig" %%% "babel-circe" % "x.y.z"
"io.taig" %%% "babel-generic" % "x.y.z"
"io.taig" %%% "babel-formatter-printf" % "x.y.z"
```

## Overview

### Data classes

- `Locale`, `Language`, `Country`  
Basic data classes in the fashion of `java.util.Locale`. It is possible to convert between `java.util.Locale` and `io.taig.babel.Locale`.
- `Text`, `Quantity`  
`Text` holds the actual `String` value of a translation as well as a `Map` of `Quantity` to describe plural forms
- `Segments`, `Path`  
`Segments` is a tree structure that mimics nested case classes. A `Path` can be used to identify a `Node` or a `Leaf` in such a tree.
- `Dictionary`  
A collection of `Text`s that are namespaced in `Segments`, so basically only translations of a single language,
- `Translation`  
A collection of `Text`s with their respective `Locale`s. This is the translation of one particular phrase into several languages.
- `Babel`  
The collection of all translations: namespaced in `Segment`s with `Translation`s in the leaves.

### Type classes

- `Formatter`: `(String, Seq[Any]) => String`  
String formatting instances but no default is provided. Depend on either `babel-formatter-printf` or `babel-formatter-message-format` and import the instance explicitly.
- `Printer`: `A => String`
- `Parser`: `String => Either[Error, A]`  
- `Encoder`: `F[A] => Segments[A]`  
- `Decoder`: `Segments[A] => Either[Error, F[A]]`  

## Guide

### Defining translations in JSON files

For each language a separate file must be created in the `resources/babel` folder and the name of the `Locale` as filename.

`resources/babel/en.json`

```json
{
  "greeting": "Good afternoon"
}
```

`resources/babel/de.json`

```json
{
  "greeting": "Guten Tag"
}
```

`resources/babel/de-AT.json`

```json
{
  "greeting": "Grüß Gott"
}
```

In addition to that, it is possible to provide language agnostic fallbacks in the  `*.json` file.

`resources/babel/*.json`

```json
{
  "greeting": "Hi"
}
```

### Loading translations into a `Babel`

```scala
import io.taig.babel.{Babel, Loader}
import io.taig.babel.circe._

val babel = Loader.auto[IO](blocker).unsafeRunSync()
```

```
> Babel(greeting ➞ {de-AT: "Grüß Gott", de: "Guten Tag", en: "Good afternoon", *: "Hi"})
```

```scala
babel(Path.Root / "greeting", Locales.de)
```

```
> Guten Tag
```

```scala
babel(Path.Root / "greeting", Locales.de_AT)
```

```
> Grüß Gott
```

```scala
babel(Path.Root / "greeting", Locales.de_CH)
```

```
> Guten Tag
```

```scala
babel(Path.Root / "greeting", Locales.fr)
```

```
> Hi
```

## Cookbook

### Resolve the user's preferred language from the `Accept-Language` header in an http4s middleware

Uses Java's `Locale.LanguageRange.parse` to lift the `Accept-Language` header value into an ordered list of `Locale`s and aligns it with the `Locale`s that are supported by the application.

```scala
import java.util.{Locale => JavaLocale}

import scala.jdk.CollectionConverters._

import cats.Defer
import io.taig.babel.Locale
import org.http4s.HttpRoutes
import org.http4s.headers.`Accept-Language`

final class LocalesMiddleware[F[_]: Defer](locales: Set[Locale], fallback: Locale) {
  def apply(routes: Locale => HttpRoutes[F]): HttpRoutes[F] =
    HttpRoutes[F] { request =>
      val locale = request.headers
        .get(`Accept-Language`)
        .map(_.value)
        .flatMap { value =>
          JavaLocale.LanguageRange
            .parse(value)
            .asScala
            .sortWith(_.getWeight > _.getWeight)
            .map(language => JavaLocale.forLanguageTag(language.getRange))
            .flatMap(Locale.fromJavaLocale)
            .find(locales.contains)
        }
        .getOrElse(fallback)

      routes(locale).run(request)
    }
}
```