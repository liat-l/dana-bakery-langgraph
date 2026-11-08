# Final technical prompt — Dana's Bakery

Build a clear student-level Python LangGraph project and a standalone Google Colab notebook named `dana_bakery_langgraph.ipynb`. Use Hebrew comments and explanations. No LLM, AI API, API key, randomness, shared mutable inventory, or persistence. Support `graph.invoke({"item": "babka", "quantity": 2, "day": "Thursday", "city": "Jerusalem"})`.

Before implementation show a Mermaid flowchart. Use StateGraph with a typed state, seven separate nodes (validation, stock check, substitution, pricing, delivery, customer message, final processing), and actual conditional edges for validity, availability and substitution success/failure.

Fixed initial stock/prices in NIS: challah 10/18, babka 0/45, rugelach 3/30, sourdough 4/25. Croissants and unknown products are invalid. Require a positive integer quantity (exclude bool), one of the seven English weekday names, and a string city. Missing/None/empty/whitespace city means pickup. A non-string city is invalid. Any valid city outside Jerusalem must cause free pickup, never rejection. Normalize surrounding whitespace in cities and match Jerusalem case-insensitively.

Require enough stock for the entire quantity. Substitution chain: babka → rugelach → sourdough → challah, at most TWO attempts from the requested item. Retain quantity, check stock at every attempt, and price the actual sold product. Reject politely when the attempt limit is exhausted or unavailable challah has no alternative. Start every invocation with an independent copy of the initial inventory. Deduct only from this copy on acceptance.

Apply precisely 15% to the baked-goods subtotal only when subtotal > 150 and day is not Friday. Never use the outdated 10% rule. Add a 20 NIS Jerusalem delivery fee AFTER discount. Other deliveries become free pickup and the customer must be informed. Use Decimal for monetary calculation and return numeric totals.

Use deterministic friendly Hebrew message templates explaining the ordered quantity/day, substitutions, pickup conversion, discounts, Friday exclusion and rejection as applicable. Every invocation returns at least status (accepted/rejected), item (actual sold product or None), delivery (pickup/delivery), total (0 on rejection), message, steps (chronological list). Rejected orders have pickup and no delivery fee. Record validation, each stock check and replacement, pricing, delivery, message creation, final status.

Include assertions with explicit expected outcomes for available stock, one/two successful replacements, exhausted replacements, unavailable challah, discontinued products and malformed/missing input, discount and Friday exclusion, Jerusalem/other/missing/empty city. Check all six fields for every case, deterministic repeat invocations, independent stock, original quantity and substituted prices. Enumerate products × quantities 1–11 × weekdays × delivery categories against an independent calculation to cover all feasible branches and bounded inventory paths.

Notebook: introduction, installation of verified pinned libraries, configuration, typed state, nodes/routing, compilation, `draw_mermaid_png()` displayed as an image, example invocation, explicit expected outcomes and assertions. Keep the notebook self-contained. Network is needed for installation and Mermaid rendering only; do not silently swallow rendering errors. Create README and this prompt. Execute tests and rendering; report actual verification. Commit and push to `dana-bakery-langgraph` if authenticated GitHub access is available. Do not overwrite unrelated files or claim publishing/sharing that was not verified.

## Corrections and improvements

- Clarified that initial product is not a substitution attempt; the third stock check is the last permitted candidate.
- Explicitly reject bool/fractional/string quantities and invalid weekday/type inputs; missing city remains valid.
- Separate the goods discount from delivery; use the actual substitute price and keep rejected totals at zero.
- Added repeatability, stock isolation and exhaustive bounded path checks, beyond six examples.
- A subtotal of exactly 150 is unreachable with the supplied inventory and prices. Verify feasible neighboring totals (144 and 162) and implement the strict `> 150` rule directly.
- Explain the rendering network dependency separately from the deterministic, offline order workflow.
