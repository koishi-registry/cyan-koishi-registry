# Koishi registry fetch app

> [!CAUTION]
> **Close source since `0.3.0`**.
> 
> Due to violation of the project's license  
> (the mirror with domain `cyans.icu` from GitHub@lovemilk2333, forum.koishi.xyz@zhuhansan666),  
> The project will be continue developing in private. This repository may still receives some updates.
> 
> Contact me on [contact@cyans.me](mailto:contact@cyans.me) if you need help, or want to join our private program.

> [!NOTE]
> End users will still be able to use our
> **Partner registry**.  
> https://kp.itzdrli.cc/  
> Our **Partner registry** stayed updated with latest features and fixes.

---
### 0.2.99
Fix a bug that makes the KG feature of app doesn't work.

---


# Original README

> [!IMPORTANT]  
> All rights reserved 2024 Copyright Cyan Changes/koishi-registry authors  
> More details in [#License](https://github.com/CyanChanges/koishi-registry/blob/main/LICENSE)

For end-user, use our
**Partner registry**
https://kp.itzdrli.cc/

> [!IMPORTANT]  
> If you find an unexpected behaviour different with Koishi's [Official registry](https://registry.koishi.chat/),
> please open an issue.

## Install
Deno is required.
```shell
deno install
```

## Usage
```shell
$ cp .env.example .env
```
```shell
$ deno task start
Listening on http://0.0.0.0:8080/
```

It takes time to synchronize for the first time.

You can configure configurations in main.ts.

Check http://127.0.0.1:8080/api/plugins,
should return currently found plugins.
(It's empty list for a while because no plugins found now, please sit and relax)

Check http://127.0.0.1:8080/index.json
should return a Koishi Registry like JSON of all found plugins.
(The `objects` may be an empty list, because no plugins found now, please sit and relax)

### API Endpoint
#### /api/status
```typescript
let returns: {
  "synchronized": boolean, // If synchronized with npm
  "updateAt": string, // UTC Date String
  features: Record<Feature, boolean> // Field Features
}
```
#### /api/plugins
```typescript
let returns: string[] // a list of package name of koishi plugins
```

## Todo
- [x] Refactor `NpmWatcher` to provide a more reliable change information.
- [x] Refactor `KoishiRegistry` cache structure to provide Quick Patch functionality.
- [ ] Support `show_deprecated`, `show_incompatible`, `recover_unpublished` params.
- [ ] Support all fields of official registry
  - [x] verified - defaults to same behaviour with `@koishijs/registry`. controlled by `analyzer/is-verified`
  - [x] insecure - a default cloud analyzer is configured, official insecure list and algorithm is private (for @koishijs orgs member, contact me on social for official implementation)
                   could control by bail event `analyze/is-insecure`
  - [ ] score    - npm search api is unreliable
  - [x] rating   - a custom rating algorithm is implemented, official rating algorithm is private (for @koishijs orgs member, contact me on social for official implementation)
  - [x] portable - detect `koishi.browser` from package meta
  - [ ] downloads - support custom implementation(implements `Analyzer`), original one removed due to the hard rate limiting of npm downloads api

## License

The project is All rights reserved.
Public deployment requires authorization in the [Project Issue](https://github.com/CyanChanges/koishi-registry),
No authorization required for personal local deployments.
use `Context.prototype.plugin` to plug your own plugin to make modification,
without modify the original codebase.
Any monkeypatch to manipulate original plugin behaviour is not allowed
(including modify prototype of classes of this project, or any ES6 builtin object aka "prototype pollution").
The license includes additional restrictions:

ilharp(Individual with GitHub https://github.com/ilharp, refers as "ilharp")
is **FORBIDDEN** to deal with the software in any form (including use, copy, modify, or distribute the software).

Individual or organization related to ilharp **can not** deal with the software without explicit authorization of the project author.

You are **FORBIDDEN** to do anything that would make Deno users unable to use this app (e.g. use Node.js specified feature, or a feature not available in Deno) or use code from this project in a project that does not intended for Deno.

You are **FORBIDDEN** to port this app to Node.js or use code from this project in a project that uses Node.js.

You are **FORBIDDEN** to use JavaScript in this project (e.g. compile TypeScript source code to JavaScript), you should always use TypeScript in this project.

The above **MUST BE** included in the license of any forks of this project.

The final explanation belongs to the author of the project.
