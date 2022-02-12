# Changelog

# 0.5.0

_2022-02-12_

* Add support for Scala 3 (#196) [@bardurdam]
* Update cats-effect to 3.3.5 (#192)
* Update http4s to 1.0.0-M31 (#194)
* Update mdoc to 2.3.0 (#191)
* Update sbt to 1.6.2 (#193)
* Update sbt-ci-release to 1.5.10 (#188)
* Update sbt-houserules to 0.3.19 (#183)
* Update sbt-scalajs to 1.9.0
* Update scala-library to 2.13.8 (#185)
* Update sconfig to 1.4.9 (#190)
* Update slf4j-simple to 1.7.36 (#195)

# 0.4.0

_2022-01-08_

* Change organization to `io.taig`
* Migrate CI to github actions
* Rename `master` branch to `main`
* Upgrade to cats 2.7.0
* Upgrade to cats-effect 3.3.3
* Upgrade to http4s 1.0.0-M30
* Upgrade to munit 0.7.29
* Upgrade to munit-cats-effect 1.0.7
* Upgrade to sbt 1.6.1
* Upgrade to sbt-houserules 0.3.18
* Upgrade to sbt-mdoc 2.2.24
* Upgrade to sbt-scalajs 1.8.0
* Upgrade to sbt-scalajs-crossproject 1.1.0
* Upgrade to sbt-web-scalajs 1.2.0
* Upgrade to scala 2.13.7
* Upgrade to scalajs-dom 2.1.0
* Upgrade to sconfig 1.4.7
* Upgrade to slf4j-simple 1.7.32

# 0.3.3

_2021-05-28_

* Update cats-core, cats-laws to 2.6.1 (#165)
* Update cats-effect, cats-effect-kernel to 3.1.1 (#166)
* Update circe-parser to 0.14.1 (#178)
* Update discipline-munit to 1.0.9 (#167)
* Update http4s-blaze-server, http4s-dsl to 1.0.0-M23 (#179)
* Update mdoc, sbt-mdoc to 2.2.21 (#171)
* Update munit, munit-scalacheck to 0.7.26 (#164)
* Update munit-cats-effect-3 to 1.0.3 (#168)
* Update sbt to 1.5.2 (#162)
* Update sbt-houserules to 0.3.10 (#175)
* Update scala-library to 2.13.6 (#174)
* Update sconfig to 1.4.4 (#169)
* Update shapeless to 2.3.7 (#173)

# 0.3.1

_2021-04-01_

* Fix broken `Quantities` JSON encoder
* Upgrade to cats-effect 3
* Upgrade to discipline-munit 1.0.7
* Upgrade to munit 0.7.23
* Upgrade to cats 2.5.0
* Upgrade to sbt-mdoc 2.2.19
* Update sbt-scalajs to 1.5.1 (#146)
* Update sbt-ci-release to 1.5.7 (#136)
* Update sbt to 1.5.0-RC2 (#135)

# 0.3.0

_2021-04-01_

Release failed, please use 0.3.0 instead

# 0.2.1

_2021-03-22_

* Plural ranges (#107)
* Fix StringFormatN source generator to start at index 0
* Don't publish documentation artifacts
* Update cats-core, cats-laws to 2.4.2 (#120)
* Update cats-effect to 2.4.0 (#134)
* Update discipline-munit to 1.0.6 (#119)
* Update http4s-blaze-server, http4s-dsl to 0.21.20 (#129)
* Update mdoc_2.13, sbt-mdoc to 2.2.18 (#122)
* Update munit, munit-scalacheck to 0.7.22 (#118)
* Update munit-cats-effect-2 to 0.13.1 (#124)
* Update paradox-theme-generic, sbt-paradox to 0.9.2 (#126)
* Update sbt to 1.5.0-RC1 (#133)
* Update sbt-ci-release to 1.5.6 (#132)
* Update sbt-houserules to 0.3.6 (#130)
* Update sbt-scalajs, scalajs-compiler, ... to 1.5.0 (#114)
* Update scala-library to 2.13.5 (#128)
* Update sconfig to 1.4.1 (#127)
* Upgrade to sbt 1.5.0-M2

# 0.2.0

_2021-01-29_

* Add `MonoidK` instance for `Translations`
* Add ``SemigroupK`` instance for `NonEmptyTranslations`
* Rename `Dictionaty` to `NonEmptyTranslations`
* Rename `Translations.toDictionary` to `.withFallback`
* Streamline collection APIs
* Improve docs

# 0.1.6

_2021-01-29_

* Generate `StringFormatN` boilerplate up to n=22
* Update munit-cats-effect-2 to 0.13.0 (#106)
* Minor doc enhancements

# 0.1.5

_2021-01-28_

* Fix `StringFormat.toString` to use 0-based-indices
* Fix plurals example in docs

# 0.1.4

_2021-01-28_

* Change `StringFormat` encoding to `MessageFormat` style
* Add plurals section to docs
* Add argument section to docs

# 0.1.3

_2021-01-28_

* Create paradox documentation microsite
* Update sconfig to 1.4.0 (#104)

# 0.1.2

_2021-01-26_

* Add cats module
* Improve sample app

# 0.1.1

_2021-01-26_

* Allow `Option` decoding for missing fields
* Fix `DerivedDecoder` giving wrong path in error message
* Fix hocon loader `null` handling
* Add numeric `Encoder` instances
* Add support for `Option` in codecs
* Add `Dictionary` and `Translations.toMap`
* Add `Dictionary` collection operations
* Improve `Translations.toDictionary`
* Add `Dictionary.of`
* Add StringFormat tests

# 0.1.0

_2021-01-26_

* Ditch collection types and go all in on data classes
* Introduce `StringFormat` for `String` argument injection

# 0.0.1

_2021-01-01_

* Initial release