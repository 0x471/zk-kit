<p align="center">
    <h1 align="center">
        EdDSA Poseidon
    </h1>
    <p align="center">A JavaScript EdDSA library for secure signing and verification using  <a href="https://www.poseidon-hash.info">Poseidon</a> and the <a href="https://eips.ethereum.org/EIPS/eip-2494">Baby Jubjub</a> elliptic curve.</p>
</p>

<p align="center">
    <a href="https://github.com/privacy-scaling-explorations/zk-kit">
        <img src="https://img.shields.io/badge/project-zk--kit-blue.svg?style=flat-square">
    </a>
    <a href="https://github.com/privacy-scaling-explorations/zk-kit/tree/main/packages/eddsa-poseidon/LICENSE">
        <img alt="NPM license" src="https://img.shields.io/npm/l/%40zk-kit%2Feddsa-poseidon?style=flat-square">
    </a>
    <a href="https://www.npmjs.com/package/@zk-kit/eddsa-poseidon">
        <img alt="NPM version" src="https://img.shields.io/npm/v/@zk-kit/eddsa-poseidon?style=flat-square" />
    </a>
    <a href="https://npmjs.org/package/@zk-kit/eddsa-poseidon">
        <img alt="Downloads" src="https://img.shields.io/npm/dm/@zk-kit/eddsa-poseidon.svg?style=flat-square" />
    </a>
    <a href="https://bundlephobia.com/package/@zk-kit/eddsa-poseidon">
        <img alt="npm bundle size (scoped)" src="https://img.shields.io/bundlephobia/minzip/@zk-kit/eddsa-poseidon" />
    </a>
    <a href="https://eslint.org/">
        <img alt="Linter eslint" src="https://img.shields.io/badge/linter-eslint-8080f2?style=flat-square&logo=eslint" />
    </a>
    <a href="https://prettier.io/">
        <img alt="Code style prettier" src="https://img.shields.io/badge/code%20style-prettier-f8bc45?style=flat-square&logo=prettier" />
    </a>
</p>

<div align="center">
    <h4>
        <a href="https://appliedzkp.org/discord">
            🗣️ Chat &amp; Support
        </a>
        <span>&nbsp;&nbsp;|&nbsp;&nbsp;</span>
        <a href="https://zkkit.pse.dev/modules/_zk_kit_eddsa_poseidon.html">
            📘 Docs
        </a>
    </h4>
</div>

| This package offers a simplified JavaScript codebase essential for creating and validating digital signatures using EdDSA and Poseidon. It's built upon the Baby Jubjub elliptic curve, ensuring seamless integration with [Circom](https://github.com/iden3/circom) and enhancing the developer experience. |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

-   Super lightweight: [**~33kB**](https://bundlephobia.com/package/@zk-kit/eddsa-poseidon) (minified)
-   Compatible with browsers and NodeJS
-   TS type support
-   Comprehensive code [documentation](https://zkkit.pse.dev/modules/_zk_kit_eddsa_poseidon.html)
-   Full test coverage

👾 Would you like to try it now? Explore it now on [Ceditor](https://ceditor.cedoor.dev/52787e4ad57d2f2076648d509efc3448)!

> [!WARNING]  
> This library has **not** been audited.

## 🛠 Install

### npm or yarn

Install the `@zk-kit/eddsa-poseidon` package and its peer dependencies with npm:

```bash
npm i @zk-kit/eddsa-poseidon
```

or yarn:

```bash
yarn add @zk-kit/eddsa-poseidon
```

### CDN

You can also load it using a `script` tag using [unpkg](https://unpkg.com/):

```html
<script src="https://unpkg.com/@zk-kit/eddsa-poseidon"></script>
```

or [JSDelivr](https://www.jsdelivr.com/):

```html
<script src="https://cdn.jsdelivr.net/npm/@zk-kit/eddsa-poseidon"></script>
```

## 📜 Usage

\# **derivePublicKey**(privateKey: _BigNumberish_): _Point\<string>_

```typescript
import { derivePublicKey } from "@zk-kit/eddsa-poseidon"

const privateKey = "secret"
const publicKey = derivePublicKey(privateKey)

console.log(publicKey)
/*
[
    '17191193026255111087474416516591393721975640005415762645730433950079177536248',
    '13751717961795090314625781035919035073474308127816403910435238282697898234143'
]
*/
```

\# **signMessage**(privateKey: _BigNumberish_, message: _BigNumberish_): _Signature\<string>_

```typescript
import { derivePublicKey, signMessage } from "@zk-kit/eddsa-poseidon"

const privateKey = "secret"
const publicKey = derivePublicKey(privateKey)

const message = "message"
const signature = signMessage(privateKey, message)

console.log(signature)
/*
{    
    R8: [
        '12949573675545142400102669657964360005184873166024880859462384824349649539693',
        '18253636630408169174294927826710424418689461166073329946402765380454102840608'
    ],
    S: '701803947557694254685424075312408605924670918868054593580245088593184746870'
}
*/
```

\# **verifySignature**(message: _BigNumberish_, signature: _Signature_, publicKey: _Point_): _boolean_

```typescript
import { derivePublicKey, signMessage, verifySignature } from "@zk-kit/eddsa-poseidon"

const privateKey = "secret"
const publicKey = derivePublicKey(privateKey)

const message = "message"
const signature = signMessage(privateKey, message)

const response = verifySignature(message, signature, publicKey)

console.log(response) // true
```
