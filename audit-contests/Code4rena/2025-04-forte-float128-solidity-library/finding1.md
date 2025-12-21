# `Float128::toPackedFloat` Fails to Promote to L Size When Exponent Is Critically Low

**Platform**: Code4rena<br>
**Project**: Forte: Float128 Solidity Library (April 2025)<br>
**Severity**: High<br>
**Status**: Valid<br>
**Reported On**: April 11th 2025<br>
**Link to Submission**: [Click Here](https://code4rena.com/audits/2025-04-forte-float128-solidity-library/submissions?uid=dcPFPaF7mn3)

---

## Summary

`Float128.toPackedFloat()` incorrectly skips promotion to L-size (72-digit mantissa) when the exponent is already at or below the minimum safe range (`MAXIMUM_EXPONENT = -18`).
This occurs because the promotion check only triggers when `mantissaMultiplier > 0`. If the mantissa is already normalized, promotion is bypassed even for critically low exponents.

## Vulnerability Details

**Root cause**: Promotion logic depends on

```js
let isResultL := slt(MAXIMUM_EXPONENT, add(exponent, mantissaMultiplier));
```

When `mantissaMultiplier == 0`, this simplifies to `slt(MAXIMUM_EXPONENT, exponent)`, which evaluates false for all exponents `≤ MAXIMUM_EXPONENT`.
As a result, numbers near the exponent floor remain in M-format (38-digit mantissa) even though further arithmetic will underflow or lose precision.

**Affected line**: [Github Link](https://github.com/code-423n4/2025-04-forte/blob/4d6694f68e80543885da78666e38c0dc7052d992/src/Float128.sol#L1102)

## Impact

- Silent precision loss and rounding drift in low-exponent values
- Possible underflow during multiplication/division
- Breaks internal invariant that L-size promotion protects values near exponent limits
- Inconsistent numeric behavior across equivalent inputs (depends on prior normalization)
- Downstream DeFi logic relying on accurate fixed-point math can produce mispriced or unsafe results

## Proof of Concept

```js
function test_ToPackedFloat_MSizeWithBigExp_PromotesToL() public {
    packedFloat val = Float128.toPackedFloat(1e37, -34); // near max for M
    (int mantissa, int exponent) = Float128.decode(val);
    assertGt(exponent, -18, "Should promote to L size to avoid overflow");
}
```

This test shows that a value at the edge of the safe exponent range is not promoted, leading to an incorrect (underflow-prone) representation.

## Recommended Mitigation

Add a fallback check after normalization to ensure all critically low exponents trigger promotion regardless of mantissa adjustment:

```js
if (
    packedFloat.unwrap(float) & MANTISSA_L_FLAG_MASK == 0 &&
    exponent <= MAXIMUM_EXPONENT
) {
    mantissa = int(BASE_TO_THE_DIGIT_DIFF) * mantissa;
    exponent += int(DIGIT_DIFF_L_M);
    float = packedFloat.wrap(packedFloat.unwrap(float) | MANTISSA_L_FLAG_MASK);
}
```

## Lessons Learned

- Guard conditions must consider boundary cases where dependent variables are zero.
- Promotion logic should depend solely on numeric safety thresholds, not on prior scaling steps.
- Unit tests must include “already-normalized but near-limit” scenarios.
