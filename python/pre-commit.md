# pre-commit

## Local / offline use of pre-commit

### Links

- <https://stackoverflow.com/a/67796237>
- <https://pre-commit.com/#repository-local-hooks>

### StackOverflow response from pre-commit developer

From [StackOverflow answer](https://stackoverflow.com/a/67796237) from
pre-commit developer:

> repository local hooks are documented here
>
> generally they are the escape hatch for the framework and are generally not
> the route you should be aiming to take (the suggested route being using the
> reusable repositories)
>
> language: system is an additional escape hatch, in this mode pre-commit does
> not manage your tools and you must install them all manually (this defeats
> the purpose of the framework entirely, but it enable some amount of legacy
> compatibility in some use cases). for language: system it will run the tools
> as if you're running them in your shell (for example entry: flake8 will use
> whatever which flake8 returns)
>
> language: python on the other hand is a managed environment, pre-commit will
> set it up and install it for you. ~generally if you're using language: python
> with repo: local you'll leverage additional_dependencies to install those
> things
>
> each of the languages are documented on the website as well
>
> disclaimer: I created pre-commit

### pre-commit documentation

From pre-commit documentation:

> Repository-local hooks are useful when:
>
> The scripts are tightly coupled to the repository and it makes sense to
> distribute the hook scripts with the repository.
> Hooks require state that is only present in a built artifact of your
> repository (such as your app's virtualenv for pylint).
> The official repository for a linter doesn't have the pre-commit metadata.
> You can configure repository-local hooks by specifying the repo as the
> sentinel local.
>
> local hooks can use any language which supports additional_dependencies or
> docker_image / fail / pygrep / script / system. This enables you to install
> things which previously would require a trivial mirror repository.
>
> A local hook must define id, name, language, entry, and files / types as
> specified under Creating new hooks.
>
> Here's an example configuration with a few local hooks:
>
> ```yaml
> -   repo: local
>     hooks:
>     -   id: pylint
>         name: pylint
>         entry: pylint
>         language: system
>         types: [python]
>         require_serial: true
>     -   id: check-x
>         name: Check X
>         entry: ./bin/check-x.sh
>         language: script
>         files: \.x$
>     -   id: scss-lint
>         name: scss-lint
>         entry: scss-lint
>         language: ruby
>         language_version: 2.1.5
>         types: [scss]
>         additional_dependencies: ['scss_lint:0.52.0']
> ```
