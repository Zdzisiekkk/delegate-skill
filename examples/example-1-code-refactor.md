# Example 1: Code Refactoring with Backward Compatibility

## Scenario

You have a large payment module that's grown unwieldy. Time to refactor it, but you need:
- Backward compatibility with v1.2+
- Multiple payment gateway support (Stripe, PayPal, Square)
- No downtime for existing integrations

This is a perfect `/delegate` task: multi-step, architectural, high-risk (payment systems!), and well-defined.

## Step 1: You Write the Task

```
/delegate

I need to refactor the payment module (src/payment/) to support multiple 
payment gateways cleanly. Currently all logic is in PaymentProcessor.ts, 
mixing Stripe-specific code with generic logic.

Requirements:
- Maintain backward compatibility with v1.2 and v1.3 of our payment API
- Support Stripe, PayPal, and Square as separate adapters
- Existing code should continue working without changes
- Add tests for new adapter pattern
- Update documentation

Current structure:
- src/payment/PaymentProcessor.ts (800 lines, mixed concerns)
- src/payment/types.ts (interfaces)
- src/payment/__tests__/PaymentProcessor.test.ts
- No other payment-related files

Timeline: Today (it's just refactoring, not new features)
```

## Step 2: Fable Plans

Fable 5 analyzes and returns something like:

```
## Understanding

Extract payment gateway logic into adapter pattern.
Current: monolithic PaymentProcessor mixing Stripe with generic logic.
Target: PaymentProcessor delegates to gateway-specific adapters.
Why: Easier to add new gateways, testable, maintains compatibility.

## Context

Read:
- src/payment/PaymentProcessor.ts (core logic, Stripe-specific code)
- src/payment/types.ts (interfaces we need to maintain)
- src/payment/__tests__/PaymentProcessor.test.ts (test requirements)
- Check package.json for current Stripe/PayPal/Square versions

## Plan

1. **Create adapter interfaces** in src/payment/adapters/types.ts
   - Define IPaymentAdapter interface
   - Ensure it covers all methods PaymentProcessor currently uses
   - Maintain backward compatibility

2. **Extract Stripe adapter** → src/payment/adapters/StripeAdapter.ts
   - Move all Stripe-specific code from PaymentProcessor
   - Implement IPaymentAdapter
   - Keep backward compatibility wrapper

3. **Create PayPal adapter** → src/payment/adapters/PayPalAdapter.ts
   - New implementation following IPaymentAdapter
   - Translate PayPal API calls to our interface
   - Handle PayPal-specific error codes

4. **Create Square adapter** → src/payment/adapters/SquareAdapter.ts
   - Same pattern as PayPal
   - Handle Square-specific quirks

5. **Refactor PaymentProcessor** to use adapters
   - Switch from direct Stripe calls to adapter pattern
   - Maintain backward-compatible public API
   - Add internal routing: if provider=stripe use StripeAdapter, etc.

6. **Update tests**
   - Create test suite for each adapter
   - Mock each gateway separately
   - Verify backward compatibility with existing tests

7. **Update documentation**
   - README: how to add new payment gateway
   - JSDoc for new adapter interfaces
   - Migration guide (if any breaking changes, though we avoid them)

## Success Criteria

- All existing PaymentProcessor tests pass (backward compatibility ✓)
- New tests for each adapter pass
- Type checking passes (no `any` except where unavoidable)
- Payment flow still works for Stripe (existing code path)
- Can add new gateways by creating new adapter (extensibility ✓)

## Risks & Mitigation

- **Risk:** Existing code breaks during refactoring
  → **Mitigation:** Extract adapters first, then refactor PaymentProcessor last (reduces breakage window)

- **Risk:** Performance regression from adapter layer
  → **Mitigation:** No new abstractions (adapters just delegate), benchmarks if needed

- **Risk:** Missing edge cases from Stripe-specific logic
  → **Mitigation:** Run existing tests against new code before release

## Model Recommendation

**Sonnet 5** — This task is well-defined:
- Clear structure and requirements
- Mechanical extraction and refactoring
- Existing tests validate correctness
- Doesn't need creative decisions, just good engineering
```

## Step 3: You Review & Accept

Claude shows you:

```
📋 REFACTORING PLAN

Objective: Extract payment processor into adapter pattern 
(Stripe, PayPal, Square) while maintaining backward compatibility.

Main Steps:
1. Create adapter interfaces and types
2. Extract Stripe adapter from existing code
3. Implement PayPal and Square adapters
4. Refactor PaymentProcessor to delegate to adapters
5. Update all tests for new structure
6. Update documentation

Recommended Model: Sonnet 5
Reason: Well-defined refactoring with clear requirements. 
Existing tests validate correctness. No ambiguity about edge cases.

⚠️ Risks:
- Existing tests must pass (critical for backward compatibility)
- Edge cases in Stripe logic must be preserved
```

**You choose:** "Okay, execute with Sonnet 5"

## Step 4: Sonnet Executes

Sonnet receives the full plan and gets to work:

```
### Creating adapter interfaces
$ Creating: src/payment/adapters/types.ts

interface IPaymentAdapter {
  charge(amount: number, currency: string, options: ChargeOptions): Promise<ChargeResult>;
  refund(transactionId: string, amount?: number): Promise<RefundResult>;
  ...
}

### Extracting Stripe adapter
$ Moving Stripe-specific code from PaymentProcessor to StripeAdapter.ts
$ Ensuring StripeAdapter implements IPaymentAdapter interface
$ All methods preserve original behavior

### Creating PayPal adapter
$ Implementing PayPalAdapter following IPaymentAdapter
$ Translating PayPal API responses to our interface
$ Added note about PayPal's 180-day refund limit

### Refactoring PaymentProcessor
$ Updated payment() method to use adapter pattern
$ Added provider routing logic
$ Verified existing tests still work...
$ ✅ All 24 tests pass
```

## Step 5: Done

Sonnet reports:

```
✅ Refactoring complete

Modified files:
- src/payment/PaymentProcessor.ts (refactored to use adapters)
- src/payment/adapters/types.ts (new — shared interfaces)
- src/payment/adapters/StripeAdapter.ts (new — extracted)
- src/payment/adapters/PayPalAdapter.ts (new — implemented)
- src/payment/adapters/SquareAdapter.ts (new — implemented)
- src/payment/__tests__/PaymentProcessor.test.ts (updated for new structure)
- src/payment/__tests__/adapters/ (new test files)
- README.md (added: how to add new gateway)

Test results:
- 24 existing tests: PASS (backward compatibility ✓)
- 18 new adapter tests: PASS
- Type checking: PASS

This refactoring works. Ready for PR.
```

---

## Why This Worked

✅ **Task was well-defined** — clear requirements, file structure, constraints
✅ **Fable planned well** — extracted all the architectural decisions upfront
✅ **Sonnet executed cleanly** — just followed the plan, no improvisation needed
✅ **Cost-efficient** — Fable for thinking (necessary), Sonnet for building (sufficient)

## What If Something Went Wrong?

**Scenario:** Sonnet gets confused about PayPal's API

```
❌ Issue: PayPalAdapter test failing
Error: PayPal response format doesn't match expected interface

→ You would: "Revise plan - clarify PayPal API response structure, 
   provide example response from PayPal docs"

→ Fable regenerates plan with PayPal details added

→ Sonnet re-runs with correct assumptions
```

This is why review is important — catches issues before execution.

---

## Next Task

After this refactoring works, adding a new gateway (Crypto payment processor) would be:

```
/delegate

Add Crypto payment gateway using the new adapter pattern.
Follow the same approach as PayPal adapter, but for Stripe's crypto API.
Tests required. No changes to PaymentProcessor itself.
```

Same pattern, even simpler second time (adapters already proven).
