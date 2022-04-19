# @stealify/ecmascript-loader
A Collection ECMAScript Module Loaders for use with rollup compatible with rollup plugins.

```js
const { steal } = require('@stealify/ecmascript-loader');
```

```js
const { steal } = await import('@stealify/ecmascript-loader');
```

```js
import { steal } from '@stealify/ecmascript-loader';
```

if a default property exists no matter how it got produced it must match the moduleNamespace the exports a default property and the usage of export = is a antiPattern
that causes confusion for the Engine and the Package Authors as also Maintainers and Users. a Module is always a NameSpace and in case of CJS the same rule applys never assign a none string property on exports or module.exports if there is no module.exports it defaults to exports already! if it is there it overwrites exports.

## Short Description
It eliminates inconsistencys when importing or requiring ECMAScript Modules it turns them into a so called StealifyModule

a StealifyModules TypeDefinition is always === rollupChunk as of time of writing as this definition contains everything
that is needed to neogate Module Loading and Registration. 

so all loaders in this repository do accept rollup.OutputChunk[]

## Why?
- supports all bundlers and bundler configs
- supports all source code variants
- supports all package variants
- Defines a Programatical Resolve Algo that is fully cache, write, load able.
- Replaces the need for a packageManager as you can also integrate any dependencie from any source.
- Full Typescript Support
  - produces correct typescript definitions for the resulting loaded Module
  - everything just works magicaly even if the project or package maintainer authored for a diffrent target environment
- Typescript produces inconsistent results by default without hugh config effort
- Package Authors do produce inconsistent Module Bundels aka to much chor updates
- I want to work with the Same Code that i write once no matter if it is for a CJS or ESM Consumer
- creates a ModuleSystem Agnostic Module System the Stealify Lang EcmaScript Module System
  - for Stealify Lang 
    - import.meta.url gets always injected
    - top level: ```top level: import, require(), await import()``` are Static Linked at Runtime
    - none top level: ```import(), require()``` and top level: ```import()``` are Dynamic Linked at Runtime
    - with Stealify Lang you can define Constants and Variables on Load to shim the correct environment for the Module.
 - create a ECMAScript Ecosystem that works in all Environments even if the Developer did not consider that

## Credits
This is the Final Result of Years of Iterations on rollup and rollup plugins as also stealjs webpack and all other module bundlers and module systems like Typescript Modules

## Examples 
- a package authored with Typescript ESM Syntax Transpiled Bundled with something
- a package authored with Typescript CJS Syntax Transpiled Bundled with something to CJS, ESM NPM Meta Package containing single d.ts definition exported for both packages 
  - it is often the case that types do contain a default property that simply does not exist on the cjs version or the cjs version has no other namedExport that matches the same type as the default all this leads to none resolve able types.
