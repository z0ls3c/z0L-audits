# `Ln::ln()` Fails to Validate Negative Inputs, Causing Division-by-Zero Panics

**Platform**: Code4rena<br>
**Project**: Forte: Float128 Solidity Library (April 2025)<br>
**Severity**: High<br>
**Status**: Valid<br>
**Reported On**: April 11th 2025<br>
**Link to Submission**: [Click Here](https://code4rena.com/audits/2025-04-forte-float128-solidity-library/submissions/S-208)<br>
**Tags:** `solidity` · `math` · `validation` · `domain-error` · `code4rena` · `forte` · `float128` · `panic` · `input-sanitization`

## Summary

The `Ln.ln()` function does not validate whether a `packedFloat` input is **negative** before proceeding with logarithmic computation.
When a negative value is passed, the function enters invalid logic paths inside `ln_helper`, eventually triggering an **EVM panic (0x12: division/modulo by zero)** instead of a clean revert.

This bypasses intended error handling, introduces reliability issues for any consumer of the library, and can cause full transaction reverts in DeFi contracts performing on-chain math operations.

## Vulnerability Details

**Root cause**:

`Ln.ln()` performs no explicit sign validation before invoking the logarithmic calculation. As a result, negative inputs propagate into internal math routines that expect positive domain values.

The resulting computation reaches a `div` or `mod` by zero condition, causing the EVM to panic rather than revert with a custom or predictable error.

**Affected line**: [GitHub Link](https://github.com/code-423n4/2025-04-forte/blob/4d6694f68e80543885da78666e38c0dc7052d992/src/Ln.sol#L63)

## Impact

- **Unexpected contract behavior**: `ln()` panics deep within its helper logic, bypassing the expected revert flow.
- **Denial of Service**: Any protocol or contract depending on `ln()` may break if it encounters negative inputs.
- **Poor developer experience**: Developers integrating the math library get no meaningful feedback, only opaque panic errors.
- **Reliability risk**: Panics may mask input validation gaps in dependent systems.

## Proof of Concept

```js
function test_ln_negative_returnsZero() public {
    // Construct a negative packed float
    packedFloat negative = Float128.toPackedFloat(-1e37, -37);

    // Expect a clean revert, not a silent panic or zero return
    vm.expectRevert("float128: log of negative number");
    Ln.ln(negative);
}
```

**Observed result (current)**:

```js
[FAIL: Error != expected error: panic: division or modulo by zero (0x12) != float128: log of negative number]
```

**Expected result (after fix)**:
Clean revert with float128: log of negative number.

## Recommended Mitigation

Add a validation guard at the start of the `ln()` function to reject invalid domain inputs:

```js
function ln(packedFloat input) public pure returns (packedFloat result) {
    if (int256(uint256(packedFloat.unwrap(input))) < 0) {
        revert("float128: log of negative number");
    }
    ...
}
```

This ensures that negative values are rejected gracefully, preventing internal division-by-zero panics and maintaining consistent error semantics.

## Lessons Learned

- Always validate **mathematical domain assumptions** before entering core math logic.
- Library functions should fail **predictably** (via revert) instead of panicking.
- Public math APIs must include boundary tests for invalid inputs (negative, zero, NaN-equivalents).
- Domain errors should use meaningful custom errors to improve integration safety and debuggability.
