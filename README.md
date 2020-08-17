## npx lerna init
lernaに必要なファイルやディレクトリが作成される

## lerna run [script]
どの階層でいても全てのpackage.jsonの指定したscripteを実行してくれる

例、このプロジェクトの場合

```
% yarn test

yarn run v1.22.4
$ lerna run test
lerna notice cli v3.22.1
lerna info Executing command in 2 packages: "yarn run test"
lerna info run Ran npm script 'test' in '@walnut/common' in 0.4s:
$ echo testing common with version: $npm_package_version
testing common with version: 1.0.0
lerna info run Ran npm script 'test' in '@walnut/server' in 0.3s:
$ echo testing server with version: $npm_package_version
testing server with version: 1.0.0
lerna success run Ran npm script 'test' in 2 packages in 0.7s:
lerna success - @walnut/common
lerna success - @walnut/server
✨  Done in 2.15s.
---------------------------
```

### --scopeでpackage.jsonを指定すると全体てはなく、個別にscriptを実行出来る

```
% yarn test:common  
yarn run v1.22.4
$ lerna run test --scope=@walnut/common
lerna notice cli v3.22.1
lerna notice filter including "@walnut/common"
lerna info filter [ '@walnut/common' ]
lerna info Executing command in 1 package: "yarn run test"
lerna info run Ran npm script 'test' in '@walnut/common' in 0.4s:
$ echo testing common with version: $npm_package_version
testing common with version: 1.0.0
lerna success run Ran npm script 'test' in 1 package in 0.4s:
lerna success - @walnut/common
✨  Done in 1.61s.
```

### --scope={}で複数指定することも可能

```
% yarn tests

yarn run v1.22.4
$ lerna run test --scope={@walnut/common,@walnut/server}
lerna notice cli v3.22.1
lerna notice filter including ["@walnut/common","@walnut/server"]
lerna info filter [ '@walnut/common', '@walnut/server' ]
lerna info Executing command in 2 packages: "yarn run test"
lerna info run Ran npm script 'test' in '@walnut/common' in 0.6s:
$ echo testing common with version: $npm_package_version
testing common with version: 1.0.0
lerna info run Ran npm script 'test' in '@walnut/server' in 0.3s:
$ echo testing server with version: $npm_package_version
testing server with version: 1.0.0
lerna success run Ran npm script 'test' in 2 packages in 0.9s:
lerna success - @walnut/common
lerna success - @walnut/server
✨  Done in 2.47s.
```

### git commit をした後に`lerna version --conventional-commits --yes`を実行するとVersionをアップしてリリースログを残すことが可能、自動でpushまでしてくれる

```
$ lerna version --conventional-commits --yes
lerna notice cli v3.22.1
lerna info current version 0.0.0
lerna info Assuming all packages changed
lerna info getChangelogConfig Successfully resolved preset "conventional-changelog-angular"

Changes:
 - @walnut/common: 1.0.0 => 1.0.1
 - @walnut/server: 1.0.0 => 1.0.1

lerna info auto-confirmed 
lerna info execute Skipping releases
lerna info git Pushing tags...
lerna success version finished
✨  Done in 12.36s.
```