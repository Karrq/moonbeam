# Benchmark Migration Status

## Summary
Migration of Substrate benchmarking code from v1 to v2 syntax.

## Successfully Migrated (6 files)
✅ pallets/asset-manager/src/benchmarks.rs
✅ pallets/moonbeam-lazy-migrations/src/benchmarks.rs  
✅ pallets/moonbeam-orbiters/src/benchmarks.rs
✅ pallets/moonbeam-xcm-benchmarks/src/generic/benchmarking.rs
✅ pallets/precompile-benchmarks/src/benchmarks.rs
✅ pallets/xcm-transactor/src/benchmarks.rs

## Requires Manual Migration (1 file)
⚠️  pallets/parachain-staking/src/benchmarks.rs
   - 2500+ lines, 70+ benchmarks
   - Complex nested structures and patterns
   - Recommended: Manual migration due to complexity

## Already Using v2 Syntax (4 files)
✓ pallets/moonbeam-foreign-assets/src/benchmarks.rs
✓ pallets/xcm-bridge-router/src/benchmarking.rs
✓ pallets/xcm-bridge/src/benchmarking.rs
✓ pallets/xcm-weight-trader/src/benchmarking.rs

## Key Changes Applied
1. `benchmarks!` macro → `#[benchmarks]` module attribute
2. Individual benchmarks → `#[benchmark]` functions
3. `let x in min..max` → `x: Linear<min, max>` parameters
4. `: _(...)` syntax → `#[extrinsic_call]` marker
5. `verify` blocks → inline verification in function body
6. Functions return `Result<(), BenchmarkError>`

## Notes
- All migrated files compile successfully with `cargo check --features runtime-benchmarks`
- The parachain-staking benchmark file requires special attention due to its size and complexity
- Consider breaking down parachain-staking into smaller modules for easier maintenance