# Examples

Real scenarios where the Input Integrity Protocol changes the outcome.

---

## Scenario 1 — File count mismatch

**Context:** User uploads 4 files and requests a cross-document review.

**The gap:** Only 2 files were extracted into context.

**Without this protocol:**
> Model acknowledges receiving only 2 files, notes the discrepancy, then proceeds with the 2 it has — leaving the user to discover the incomplete analysis after the fact.

**With this protocol:**
> "I can access 2 files. You uploaded 4. Should I proceed with what's here, or would you like to re-upload before I begin?" — output ends there. No analysis until confirmation received.

---

## Scenario 2 — Confirmation gate violation

**Context:** User references an image alongside text. Image didn't come through.

**The gap:** Model flags the missing image and asks for a decision — then immediately proceeds without waiting for a response.

**Without this protocol:**
> "I don't see the image. Proceed without it or re-send? — Proceeding with text only." Both in the same output.

**With this protocol:**
> "I don't see the image. Should I proceed with text only, or would you like to re-send?" — output ends there. Waits.

---

These scenarios are what built this protocol.
