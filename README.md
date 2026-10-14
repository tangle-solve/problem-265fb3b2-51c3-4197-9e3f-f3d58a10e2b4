<!-- solve-problem:265fb3b2-51c3-4197-9e3f-f3d58a10e2b4 -->
# Fully decentralized stablecoin participation conjecture

A [Tangle Solve problem](https://solve.tangle.tools/problems/265fb3b2-51c3-4197-9e3f-f3d58a10e2b4).

## What is the problem?

The conjecture concerns whether a *fully decentralized* stablecoin — a protocol running on smart contracts with no legal entity, no issuer with enforceable claims, and governance decided entirely by on-chain token voting — can sustain long-run participation by all stakeholder classes it needs (holders seeking price stability, capital providers/collateral stewards, governance token holders, arbitrageurs/keepers of price feeds and liquidations).

Formalize it as a dynamic game: a repeated/infinite-horizon stochastic game among stakeholder classes i ∈ {H (holders), K (capital/stakers), G (governance), A (agents maintaining the system)}. In each period, players choose participation levels (deposit, stake, exit, vote, provide services) and the protocol executes a fixed smart-contract mechanism m (minting, redemption, liquidation, fee distribution). The question: does there exist a mechanism m and a self-enforcing equilibrium (subgame-perfect, or sequentially rational) such that (a) the peg is maintained in expectation (price ≈ $1 up to bounded deviation), and (b) all classes' participation stays strictly positive in the long run, under *sufficiently flexible governance* — i.e., governance parameters can be changed by the G class itself.

The conjecture (of the "impossibility" type) is that no such mechanism exists: flexible governance lets a coalition capture seigniorage or drain collateral, so exit dominates for some class, and participation collapses. The precise statement must be constructed — that formalization of "realistic parameter and governance restrictions" is itself part of the problem.

## Why does it matter?

A proof of impossibility would delineate exactly which stablecoins (DeFi-native like algorithmic or overcollateralized-decentralized designs) are structurally unsound without external enforcement or deliberately crippled governance — a direct guide for regulators and protocol designers. A refutation — an explicit construction with a proven sustainable equilibrium — would give the first rigorous foundation for fully decentralized money, unblocking formal security analysis of a multi-hundred-billion-dollar asset class. It also connects to classic corporate-control theory: it is the on-chain analogue of whether control rights can be separated from residual claims without agency collapse.

## What's already known?

- Klages-Mundt et al. (2020) map the design space of "Stablecoins 2.0," formalizing stakeholder classes and risk models, and observe informally that fully decentralized designs face unresolved participation/incentive problems — this is the source of the conjecture. They do not prove a theorem.
- Empirical/practitioner literature (Terra collapse, Iron Finance, MakerDAO governance analyses) documents participation failures consistent with the conjecture, but without game-theoretic rigor.
- Related theory: bank-run models (Diamond–Dybvig, Morris–Shin global games) cover runs on stablecoins but assume fixed mechanisms, not endogenous governance capture.
- Incomplete-contracts and corporate-control theory (Grossman–Hart–Moore lineage; Aghion–Bolton) provides the off-chain analogue: control rights create hold-up and agency rents. No one has ported this to self-amending smart-contract mechanisms.

Main gap: no formal model in which "sufficiently flexible governance" is a well-defined action space, hence no theorem in either direction.

## What would count as solving it?

1. **Impossibility (conjecture true):** Define a class of protocols M (decentralized, self-amending via token governance, with stakeholder utility functions from Klages-Mundt et al.). Prove: for every m ∈ M, every equilibrium has some stakeholder class's participation converging to zero, or peg failure with positive probability. A referee wants: precise mechanism class, equilibrium concept, and a nontriviality check (the result must not follow merely from assuming away commitment).
2. **Refutation:** An explicit mechanism m with a proven equilibrium sustaining peg and positive participation of all classes indefinitely, robust to a specified deviation/adversary model.
3. **Boundary result (most valuable):** Characterize the exact governance restrictions (e.g., timelocks, quorum rules, collateral-locked voting) that separate possible from impossible — an if-and-only-if theorem.

## How to start

1. Read Klages-Mundt et al. (2020), Sections on stakeholder incentives and risk-based models — extract their taxonomy as your primitives.
2. Build the minimal formal model: two classes (holders, stakers) plus a governance parameter that can be re-set each period. Model it as a dynamic mechanism-design problem with self-enforcement (no external court). The natural tool is repeated-game folk-theorem analysis — and the obstacle is that self-amendment means the "mechanism" is endogenous, so folk-theorem sustaining punishments may itself be undone by governance.
3. Import the incomplete-contracts insight: control rights over the mechanism are non-contractible on-chain; try an adaptation of a Grossman–Hart style hold-up argument to show a governance coalition extracts rents that drive out one class.
4. Sanity-check candidate impossibility proofs against a concrete protocol (MakerDAO-style vault system) to ensure the mechanism class isn't strawmanned.

## Key references

- Klages-Mundt, J., Harz, D., Gudgeon, L., Liu, H., Minca, A. (2020), *Stablecoins 2.0: Economic Foundations and Risk-based Models*, arXiv:2006.12388 — develops the stakeholder/risk framework for stablecoin design and articulates the informal decentralization-participation problem. https://arxiv.org/abs/2006.12388
- Diamond, D., Dybvig, P. (1983), "Bank Runs, Deposit Insurance, and Liquidity," *JPE* — canonical run model underlying stablecoin run analysis. (verify edition/details)
- Morris, S., Shin, H.S. (1998), "Unique Equilibrium in a Model of Self-Refilling Currency Attacks," *AER* — global-games refinement for coordination failures relevant to peg defense.
- Aghion, P., Bolton, P. (1992), "An Incomplete Contracts Approach to Financial Contracting," *REStud* — the corporate-control/agency framework to port on-chain. (verify)

## Warnings

- The conjecture is informal; the biggest risk is proving a vacuous impossibility by over-restricting the mechanism class, or a trivial refutation by smuggling in external enforcement (e.g., assuming courts punish governance attackers). State adversary and commitment assumptions explicitly.
- "Sufficiently flexible governance" is undefined in the source — you must define it, and your result's value hinges on that definition being neither too strong nor too weak.
- Folk-theorem instincts mislead: in self-amending protocols, punishment strategies are themselves amendable, so standard repeated-game sustainability arguments may fail — this is likely where either the impossibility proof or its loophole lives.
- Do not conflate peg stability with participation sustainability; the conjecture concerns the latter under the former.

---
*`BCGT-000327` · unverified*

## Acceptance guidance

1. **Impossibility (conjecture true):** Define a class of protocols M (decentralized, self-amending via token governance, with stakeholder utility functions from Klages-Mundt et al.). Prove: for every m ∈ M, every equilibrium has some stakeholder class's participation converging to zero, or peg failure with positive probability. A referee wants: precise mechanism class, equilibrium concept, and a nontriviality check (the result must not follow merely from assuming away commitment).
2. **Refutation:** An explicit mechanism m with a proven equilibrium sustaining peg and positive participation of all classes indefinitely, robust to a specified deviation/adversary model.
3. **Boundary result (most valuable):** Characterize the exact governance restrictions (e.g., timelocks, quorum rules, collateral-locked voting) that separate possible from impossible — an if-and-only-if theorem.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/265fb3b2-51c3-4197-9e3f-f3d58a10e2b4?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: BCGT-000327.

- [Public source catalog](https://drewstone.github.io/problems/#/p/BCGT-000327)
