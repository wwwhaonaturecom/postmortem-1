require 'shortcake'

option '-g', '--grep [filter]', 'test filter'
option '-v', '--version [<newversion> | major | minor | patch | build]', 'new version'

task 'clean', 'clean project', (options) ->
  exec 'rm -rf lib'

task 'build', 'build project', (options) ->
  exec 'node_modules/.bin/coffee -bcm -o lib/ src/'

task 'watch', 'watch for changes and recompile project', ->
  exec './node_modules/.bin/coffee -bc -m -w -o lib/ src/'

task 'test', 'run tests', (options) ->
  test = options.test ? 'test'
  if options.grep?
    grep = "--grep #{options.grep}"
  else
    grep = ''

  exec "NODE_ENV=test ./node_modules/.bin/mocha
  --colors
  --recursive
  --reporter spec
  --timeout 5000
  --compilers coffee:coffee-script/register
  --require ./register
  #{grep}
  #{test}"

task 'gh-pages', 'Publish docs to gh-pages', ->
  brief = require 'brief'
  brief.update()

task 'publish', 'publish project', (options) ->
  newVersion = options.version ? 'patch'

  exec """
  git push
  npm version #{newVersion}
  npm publish
  """.split '\n'
