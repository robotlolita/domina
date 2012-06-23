_     = require \slake-build-utils
fs    = _.fs
glob  = require \glob .sync

global <<< require \prelude-ls

defer = process.next-tick

defaults    = void
environment =
  package: require \./package.json


task \clean 'Removes all build artifacts.' ->
  each fs.remove, <[ lib build dist ]>
  defer _.display-errors


task \build 'Builds JavaScript files out of the LiveScript ones.' ->
  defer _.display-errors
  _.tasks.compile-ls \src \lib compile: defaults, environment: environment



task \build:bundle 'Generates browserify bundles for Moros.' ->
  defer _.display-errors
  "moros" |> _.tasks.bundle \build, {+bare, -prelude, require: [\moros]}, []


task \build:all 'Runs all build tasks.' ->
  defer _.display-errors
  invoke \build
  invoke \build:bundle


task \package 'Packages Moros in a nice .tar.gz package.' ->
  version = environment.package.version
  fs.initialise \dist
  fs.copy \build "dist/moros-#version"
  _.tasks.pack \dist "moros-#version" ["moros-#version"] _.display-errors