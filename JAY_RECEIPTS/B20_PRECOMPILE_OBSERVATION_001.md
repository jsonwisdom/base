# B20 Precompile Observation 001

**Repository:** `jsonwisdom/base`  
**Source upstream:** `base/base`  
**Branch:** `jay/b20-precompile-audit-001`  
**Observed HEAD:** `a052beb374f256078eccf0e0241b192f84208d06`  
**Status:** `OBSERVATION_ONLY_NO_CODE_MUTATION`  
**Purpose:** Preserve a public, auditable research trail for B20 precompile-related code paths observed in the copied Base repository.

---

## 1. Scope

This receipt documents observed files and symbols related to Base B20 precompile infrastructure.

This receipt does **not** claim production activation, mainnet deployment, official roadmap status, or legal/security classification. It records only repository-visible evidence from the copied codebase.

---

## 2. Primary Observation

The repository contains B20-related precompile components, including activation flags, factory dispatch, ABI definitions, storage handling, token variants, and benchmark hooks.

Key observed feature identifiers include:

```txt
base.b20_token
base.b20_factory
base.b20_stablecoin
base.b20_security
```

Key observed callable/function labels include:

```txt
createB20
getB20Address
transfer_with_memo
```

Key observed variants include:

```txt
B20
Stablecoin
Security
```

---

## 3. Logical Trace Map

```txt
activation/storage.rs
  -> ActivationFeature::{B20Token, B20Factory, B20Stablecoin, B20Security}

provider.rs
  -> installs B20Factory precompile when expected by spec/activation path

b20_factory/mod.rs
  -> declares B20Factory native precompile module

b20_factory/abi.rs
  -> exposes createB20 and getB20Address ABI surface

b20_factory/dispatch.rs
  -> dispatches calldata to createB20 / getB20Address

b20_factory/variant.rs
  -> maps ABI enum variants DEFAULT/STABLECOIN/SECURITY

b20_factory/storage.rs
  -> initializes token storage for B20, Stablecoin, and Security variants

benches/base_precompiles.rs
  -> benchmarks B20 precompile behaviors and cycle/proving paths
```

---

## 4. Grep Evidence Receipt

Command executed locally:

```bash
grep -R "B20" -n crates/common/precompiles crates | head -50
grep -R "createB20\|Stablecoin\|Security\|transfer_with_memo" -n crates | head -80
```

Observed excerpts:

```txt
crates/common/precompiles/src/activation/storage.rs:27:    B20Token,
crates/common/precompiles/src/activation/storage.rs:29:    B20Factory,
crates/common/precompiles/src/activation/storage.rs:33:    B20Stablecoin,
crates/common/precompiles/src/activation/storage.rs:35:    B20Security,
crates/common/precompiles/src/activation/storage.rs:279:        assert_eq!(ActivationFeature::B20Token.id(), keccak256("base.b20_token"));
crates/common/precompiles/src/activation/storage.rs:280:        assert_eq!(ActivationFeature::B20Factory.id(), keccak256("base.b20_factory"));
crates/common/precompiles/src/activation/storage.rs:282:        assert_eq!(ActivationFeature::B20Stablecoin.id(), keccak256("base.b20_stablecoin"));
crates/common/precompiles/src/activation/storage.rs:283:        assert_eq!(ActivationFeature::B20Security.id(), keccak256("base.b20_security"));
crates/common/precompiles/src/b20_factory/mod.rs:1://! `B20Factory` native precompile — creates B-20 tokens at deterministic prefix-encoded addresses.
crates/common/precompiles/src/b20_factory/dispatch.rs:30:            IB20Factory::IB20FactoryCalls::createB20(call) => {
crates/common/precompiles/src/b20_factory/abi.rs:83:        function createB20(
crates/common/precompiles/src/b20_factory/abi.rs:90:        /// Returns the address a `createB20` call would produce.
crates/common/precompiles/src/b20_factory/variant.rs:18:    /// Stablecoin B-20 token.
crates/common/precompiles/src/b20_factory/variant.rs:20:    /// Security B-20 token.
```

---

## 5. Boundary Statement

This receipt preserves evidence only.

Forbidden elevations without additional public evidence:

```txt
DEVNET_CODE -> MAINNET_FEATURE
BENCHMARK -> PRODUCTION_ROADMAP
SYMBOL_NAME -> OFFICIAL_POLICY
SECURITY_VARIANT -> REGULATED_SECURITY_OFFERING
STABLECOIN_VARIANT -> LIVE_STABLECOIN_DEPLOYMENT
```

Allowed claim:

```txt
The copied Base repository at observed HEAD contains B20-related native precompile code paths and benchmarks.
```

---

## 6. Integrity Classification

```json
{
  "receipt_id": "B20_PRECOMPILE_OBSERVATION_001",
  "repository": "jsonwisdom/base",
  "branch": "jay/b20-precompile-audit-001",
  "observed_head": "a052beb374f256078eccf0e0241b192f84208d06",
  "mode": "OBSERVATION_ONLY",
  "code_mutation": false,
  "claim_boundary": "REPOSITORY_VISIBLE_EVIDENCE_ONLY",
  "status": "SEALED_AS_DOCUMENTATION_RECEIPT"
}
```

Proof over narrative. Receipts over authority. ⚙️🧾
