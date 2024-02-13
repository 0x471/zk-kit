<p align="center">
    <h1 align="center">
        SnarkJS Groth16
    </h1>
    <p align="center">A snippet of SnarkJS code for verifying and generating Groth16 proofs only.</p>
</p>

<p align="center">
    <a href="https://github.com/privacy-scaling-explorations/zk-kit">
        <img src="https://img.shields.io/badge/project-zk--kit-blue.svg?style=flat-square">
    </a>
    <a href="https://github.com/privacy-scaling-explorations/zk-kit/tree/main/packages/groth16/LICENSE">
        <img alt="NPM license" src="https://img.shields.io/npm/l/%40zk-kit%2Fgroth16?style=flat-square">
    </a>
    <a href="https://www.npmjs.com/package/@zk-kit/groth16">
        <img alt="NPM version" src="https://img.shields.io/npm/v/@zk-kit/groth16?style=flat-square" />
    </a>
    <a href="https://npmjs.org/package/@zk-kit/groth16">
        <img alt="Downloads" src="https://img.shields.io/npm/dm/@zk-kit/groth16.svg?style=flat-square" />
    </a>
    <a href="https://bundlephobia.com/package/@zk-kit/groth16">
        <img alt="npm bundle size (scoped)" src="https://img.shields.io/bundlephobia/minzip/@zk-kit/groth16" />
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
        <a href="https://zkkit.pse.dev/modules/_zk_kit_groth16.html">
            📘 Docs
        </a>
    </h4>
</div>

> [!WARNING]  
> This package is no longer maintained as [SnarkJS](https://github.com/iden3/snarkjs) has integrated most of the above optimizations. Please, consider installing it instead.

| This package contains [SnarkJS](https://github.com/iden3/snarkjs) functions for generating and verifying zero knowledge proofs with Groth16 specifically. In addition to the original code it also uses the cached `bn128` curve if it already exists, making verification and generation of consecutive proofs faster. |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Some advantages of using this package instead of `snarkjs` directly are:

-   It only includes code to verify and generate Groth16 proofs, making your final bundle lighter.
-   It doesn't call the [ffjavascript](https://github.com/iden3/ffjavascript) `buildBn128` function if a `bn128` cached curve already exists, making verification and generation of consecutive proofs much faster (e.g. verification seems to be ~9 times faster after the first one).
-   It includes TS types.
-   It provides an ESM bundle that is compatible with browsers. So there is no need to add any polyfill or additional configuration.

## References

1. Jens Groth. _On the Size of Pairing-Based Non-interactive Arguments_. 2016-04-28. https://link.springer.com/chapter/10.1007/978-3-662-49896-5_11.

---

## 🛠 Install

### npm or yarn

Install the `@zk-kit/groth16` package and its peer dependencies with npm:

```bash
npm i @zk-kit/groth16
```

or yarn:

```bash
yarn add @zk-kit/groth16
```

## 📜 Usage

> [!WARNING]  
> You will need to provide your own circuits here in your specified path. Remember to define your circuit input and rename the files accordingly.

```typescript
import { prove, verify, buildBn128 } from "@zk-kit/groth16"
;(async () => {
    // Build the BN128 curve for Groth16.
    // https://github.com/iden3/ffjavascript/blob/master/src/wasm_field1.js
    await buildBn128() // WasmField1

    // Define your circuit input.
    // const input = {
    //     input1: 1,
    //     input2: 2,
    //     inputN: "N"
    // }

    // Compute the proof.
    const proof = await prove(input, "<YOUR-PATH>/circuit.zkey", "<YOUR-PATH>/circuit.wasm")

    /*
    {
        proof: {
            pi_a: [
                '8259885706934172848141475422209230656096448508815982888010519325096632035723',
                '3142099172052192611205205328157407975469005554072266974009053708782134081166',
                '1'
            ],
            pi_b: [ [Array], [Array], [Array] ],
            pi_c: [
                '13863804425308906943736719856399634046638544298517159271373916818387594277305',
                '21340646707244019956779928177502771923632450548108204371058275686712196195969',
                '1'
            ],
            protocol: 'groth16',
            curve: 'bn128'
        },
        publicSignals: [
            '527758365153958423212195330785598453331596731388181860789801455413116800554',
            '19104626566001952573667666924569656871967113105870778077087237826253896482830',
            '122'
        ]
    }
    */
    console.log(proof)

    // Verify the proof.
    const response = await verify("<YOUR-PATH>/circuit_verification_key.json", proof)

    // true or false.
    console.log(response)

    process.exit(0)
})()
```
