# [0.5.0](https://github.com/nickdemianchuk/actions/compare/0.4.1...0.5.0) (2026-09-14)


### Features

* require octo-buddy private key in terraform ([#26](https://github.com/nickdemianchuk/actions/issues/26)) ([8e1cdd7](https://github.com/nickdemianchuk/actions/commit/8e1cdd7fbe03c936315213ef109133ecb1709da6))

## [0.4.1](https://github.com/nickdemianchuk/actions/compare/0.4.0...0.4.1) (2026-09-14)


### Bug Fixes

* add condition to skip release on chore commits ([#25](https://github.com/nickdemianchuk/actions/issues/25)) ([8e44f5f](https://github.com/nickdemianchuk/actions/commit/8e44f5f8579f3673ceef78d47325b95df961f5fb))

# [0.4.0](https://github.com/nickdemianchuk/actions/compare/0.3.3...0.4.0) (2026-09-14)


### Features

* fail lint-pr when pr body is missing ([#24](https://github.com/nickdemianchuk/actions/issues/24)) ([700f81f](https://github.com/nickdemianchuk/actions/commit/700f81f40e8bc4a676982376d86d69808047fbcd))

## [0.3.3](https://github.com/nickdemianchuk/actions/compare/0.3.2...0.3.3) (2026-09-13)


### Bug Fixes

* set auto_approve to skip PR comment requirement ([#20](https://github.com/nickdemianchuk/actions/issues/20)) ([ac3a21c](https://github.com/nickdemianchuk/actions/commit/ac3a21c8bd789268a760bb0817c2bd772a8e5868))

## [0.3.2](https://github.com/nickdemianchuk/actions/compare/0.3.1...0.3.2) (2026-09-13)


### Bug Fixes

* pass GITHUB_TOKEN to dflook/terraform-apply for plan approval ([#18](https://github.com/nickdemianchuk/actions/issues/18)) ([c20bbef](https://github.com/nickdemianchuk/actions/commit/c20bbefd01a67b4701c52ea35c79b9a5ab9563ef))

## [0.3.1](https://github.com/nickdemianchuk/actions/compare/0.3.0...0.3.1) (2026-09-13)


### Bug Fixes

* pass workspace input to dflook/terraform-plan ([#13](https://github.com/nickdemianchuk/actions/issues/13)) ([0ef27cc](https://github.com/nickdemianchuk/actions/commit/0ef27ccaa20794ee637497ffae25101003777587))

# [0.3.0](https://github.com/nickdemianchuk/actions/compare/0.2.2...0.3.0) (2026-09-13)


### Features

* add reusable tf-plan and tf-apply workflows ([#12](https://github.com/nickdemianchuk/actions/issues/12)) ([5a0c842](https://github.com/nickdemianchuk/actions/commit/5a0c842c9aaa9b770e50aaef0c6695de4ad0aee9))

## [0.2.2](https://github.com/nickdemianchuk/actions/compare/0.2.1...0.2.2) (2026-09-13)


### Reverts

* Revert "fix: simplify release workflow by removing bot check ([#10](https://github.com/nickdemianchuk/actions/issues/10))" ([#11](https://github.com/nickdemianchuk/actions/issues/11)) ([4da27f3](https://github.com/nickdemianchuk/actions/commit/4da27f3bb1755a64984578525c67926439d3c254))

## [0.2.1](https://github.com/nickdemianchuk/actions/compare/0.2.0...0.2.1) (2026-09-13)


### Bug Fixes

* simplify release workflow by removing bot check ([#10](https://github.com/nickdemianchuk/actions/issues/10)) ([8b770db](https://github.com/nickdemianchuk/actions/commit/8b770dbad81c9797f9f860d44b9d811ea81ee0ef))

# [0.2.0](https://github.com/nickdemianchuk/actions/compare/0.1.0...0.2.0) (2026-09-13)


### Features

* use github-actions bot as release committer ([#9](https://github.com/nickdemianchuk/actions/issues/9)) ([e807c94](https://github.com/nickdemianchuk/actions/commit/e807c94cc4067a7fde9a0a38359c88525b1929a5))

# [0.1.0](https://github.com/[secure]/actions/compare/0.0.1...0.1.0) (2026-09-13)


### Bug Fixes

* use gh token for checkout ([#8](https://github.com/[secure]/actions/issues/8)) ([69d8e62](https://github.com/[secure]/actions/commit/69d8e6251c8f55056aba1b5dcc8569fdd4b1f567))


### Features

* set git author from github actions context for release commits ([#7](https://github.com/[secure]/actions/issues/7)) ([16b7fae](https://github.com/[secure]/actions/commit/16b7faea83af744e36940a95437140216a8b6ba5))
* use personal token for semantic release commits ([#6](https://github.com/[secure]/actions/issues/6)) ([a335c13](https://github.com/[secure]/actions/commit/a335c1302bca43d0d6005fb2bee43afdd5fb7dd1))

## [0.0.1](https://github.com/nickdemianchuk/actions/compare/0.0.0...0.0.1) (2026-09-12)


### Bug Fixes

* install semantic-release plugins explicitly ([#5](https://github.com/nickdemianchuk/actions/issues/5)) ([bc2f400](https://github.com/nickdemianchuk/actions/commit/bc2f4004f9b53100a8d4758335b9980c18935b7f))
