# Component Manifest
<sup>**`compfest`**</sup>

> Inspired from [TextMate grammar](https://macromates.com/manual/en/language_grammars) for syntax highlighting
> And based on [UML component diagram](https://www.uml-diagrams.org/component-diagrams.html)

## About
Extract the manifest file from the sources by providing a specific grammar.
```yml
grammar: [svelte.rpl]
components:
  - svelte.htmltag.component.name
provides:
  - svelte.EventDispatcher
connectors:
  - require: svelte.directive.bind.property
    provide: svelte.directive.bind.variable
requires:
  - svelte.export.let.Unassigned
  - svelte.export.let.Assigned
```

## Motivation
>- How many component framework we have in the ecosystem? 3~4?
>- What if we include another programming language? ~7?
>- What if we _not_ limit it only to front-end or mobile? 9~15?
>- What if we include not so popular framework too? >40?

Having many choices is good and utilizing all of them in the organization make several projects faster to deliver.
However, what if we want to analyze that? Maybe we want to reuse or rewrite some component from other projects.
Well, good luck with that 😅

## Usage (still draft)
```console
$ compfest gen 'src/**/*.svelte' --grammar svelte.rosie.yml --as yaml
version: '1'
connections:
  - provide: # no connection
      component: MyComponent
      property: error
      type: IError
  - provide: # because <MyComponent on:hear={hear}/> <YourComponent bind:talk={hear}/>
      component: MyComponent
      property: hear
      type: string
    require:
      component: YourComponent
      property: talk
      type: string
  - require: # no connection
      component: MyComponent
      property: accept
      type: IResponse
```
