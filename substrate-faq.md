This page records Substrate related questions and answers that we know of.  
To contribute, refer to the [contribution rules](#contribution-rules).

### Validators could not finalize blocks even when online all the time. What is the solution?

- Substrate ver: <`v2.0.0-rc2`

1. Updating to Substrate v2.0.0-rc2 helps.
2. (Fallback) Sometimes even rc2 could get stuck. So create a script to monitor the finlized block and restart Substrate if happening.

*Last updated: 2020-06-10*

### How is transaction fee calculated?

- Substrate ver: `v2.0.0-rc3`

Currently the code is a bit different from the specification.

What's in the spec:

```
some_value = (1 + (v * diff) + (v * diff)^2 / 2)
new_weight = old_weight * some_value
```

What's actually in the code:

```
some_value = (1 + (v * diff) + (v * diff)^2 / 2)
new_weight = old_weight + some_value
```

Refer to: [paritytech/substrate#6297](https://github.com/paritytech/substrate/pull/6297)

Under review now. Probably the code need to be updated. 

*Last updated: 2020-06-10*

### How to migrate a Substrate network from PoA to PoS consensus?

- Substrate ver: `v2.0.0-rc3`

1. To start proof-of-authority, the validators are just hard-coded into the chain specification.
Validator elections only take place on era change.

2. The era-forcing mode is described by the [forcing enum from the staking pallet](https://github.com/paritytech/substrate/blob/v2.0.0-rc3/frame/staking/src/lib.rs#L917).

3. The era-forcing mode for proof-of-authority is ForceNone.

4. Migrating to proof-of-stake only requires calling the [force_new_era function](https://github.com/paritytech/substrate/blob/v2.0.0-rc3/frame/staking/src/lib.rs#L1812), which changes the era-forcing mode from ForceNone to ForceNew.

5. Remove all the invulnerable validators by calling [set_invulnerables](https://github.com/paritytech/substrate/blob/v2.0.0-rc3/frame/staking/src/lib.rs#L1841). This removes the genesis authorities from the invulnerables.

*Last updated: 2020-06-10*

### What is the recommended practice to perform runtime migration in a fail-safe / data-restorable way?

- Substrate ver: `v2.0.0-rc3`

1. [Substrate Seminar on runtime upgrade](https://youtu.be/0eNGZpNkJk4).

2. [Gav script on upgrading Kusama network](https://hackmd.io/mGgNZX0VT4S0UTaq89-_SQ) for reference. Tweak accordingly.

3. Use `export-blocks` and `import-blocks` sub-commands to export blocks and try out the migration in a single node dev environment.

*Last updated: 2020-06-10*

---

## Contribution Rules

```
### The question here

- Substrate ver: Substrate tag defined at: https://github.com/paritytech/substrate/tags.

The answer here

*Last updated: 2020-06-10 (optional: contributor)*
```
