# verify-proof

[![Build Status](https://travis-ci.org/binded/verify-proof.svg?branch=master)](https://travis-ci.org/binded/verify-proof)

This is a client side library and web UI for verifying Binded issued proofs.

Proofs are composed of a merkle branch, original data and a root hash which is written on the Bitcoin blockchain, effectively timestamping the data.

The proof format is based on [chainpoint proof format](https://github.com/chainpoint/whitepaper/raw/master/chainpoint_white_paper.pdf).

<a href="https://verify.binded.com/">Verify a Binded proof</a>

## Install

```bash
npm install --save @binded/verify-proof
```

## Usage

```javascript
import bindedVerify from '@binded/verify-proof'
import fs from 'fs'

const proofData = JSON.parse(fs.readFileSync('./some-binded-proof.json', {
  encoding: 'utf-8',
}))

const proof = bindedVerify(proofData)

proof.analyze().then((results) => {
  console.log(results)
  /*
    {
      // optional info for nicer error messages in case
      // isValid is false
      validations: {
        isTargetHashValid: true,
        isMerkleRootValid: true,
        isDataHashValid: true,
        isTxValid: true,
      },
      confirmations: 4097,
      isValid: true, // true if valid and false if invalid
    }
  */
})
```

TODO: cli installed with `npm install -g @binded/verify-proof`

NB: Binded was formerly known as Blockai.

