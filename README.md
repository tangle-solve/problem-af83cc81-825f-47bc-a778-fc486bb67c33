<!-- solve-problem:af83cc81-825f-47bc-a778-fc486bb67c33 -->
# Optimal output-sensitive high-dimensional convex hulls

A [Tangle Solve problem](https://solve.tangle.tools/problems/af83cc81-825f-47bc-a778-fc486bb67c33).

## What is the problem?

Given a set P of n points in fixed dimension d (d treated as a constant), compute the convex hull of P in time O(n log f + f), where f is the total output size (number of faces of all dimensions, or equivalently facets, of the hull). The bound must be *output-sensitive*: worst case f = Θ(n^⌊d/2⌋) should cost about that much, but if f is small (e.g., f = O(n)), the algorithm should run in near-linear time O(n log n), independent of the worst-case combinatorial explosion. Precise formalization: for every fixed d ≥ 3 (d = 2 is solved), find an algorithm with running time O(n log f + f) in the worst case over inputs whose hull has f facets; matching lower bounds Ω(n log f) are essentially settled via reduction to sorting when f ≤ n. The current best algorithms fall short of O(n log f + f) for general fixed d; the open question is closing the remaining polylogarithmic or dimensional-constant-factor gaps and proving optimality. Ambiguity note: "output size" may be measured as facets only or all faces; for fixed d these differ by constant factors (Upper Bound Theorem), so the formulations are equivalent up to constants.

## Why does it matters?

Output-sensitive hull algorithms are the workhorse primitive behind Voronoi/Delaunay computation, halfspace intersection, linear programming with many constraints, and polytope enumeration used in robotics, rendering, and optimization. Closing the gap would settle TOPP Problem 15, one of the most cited open problems in computational geometry, and settle the optimal complexity of a fundamental operation: paying only for the structure actually present rather than the worst case. Many lower-level geometric results quote hull complexity as a black box, so an optimal bound propagates widely.

## What's already known?

- d = 2: solved optimally — Kirkpatrick–Seidel (1986) gave O(n log f); Chan (1996) improved to O(n log f) with a simpler method (also O(n log h) for extreme points/h ∈ # vertices).
- d = 3: optimal or near-optimal output-sensitive algorithms exist; hulls of size f can be computed in O(n log f) expected time (verify exact current status — Chazelle–Preparata-style incremental and randomized methods give close bounds).
- Fixed d ≥ 4: the best known bounds come from Chan's work and later refinements (Chan–Chen–others): roughly O(n log f + (nf)^{1−1/(⌊d/2⌋+1)} polylog) — i.e., output sensitivity is achieved only partially; an extra term depending jointly on n and f remains. Chazelle's deterministic worst-case O(n log n + n^⌊d/2⌋) shows optimal *worst-case* behavior, but is not output-sensitive. Randomized incremental construction (Clarkson–Shor) gives O(n log n + f) expected — output-insensitive in the log term. The gap: no known algorithm achieves O(n log f + f) for all fixed d.

## What would count as solving it?

1. **Upper bound (main):** a deterministic or randomized algorithm for every fixed d computing the hull in O(n log f + f) time (expected time acceptable if stated).
2. **Lower bound:** a proof that Ω(n log f) is unavoidable for all d ≥ 2 (essentially known via sorting reductions; formalizing suffices).
3. Together, a matching bound settling TOPP Problem 15.
4. Partial credit: an algorithm achieving O(n log f + f · polylog f) or removing the mixed (nf)^{1−…} term would be significant progress.

## How to start

1. Read Chan (1996) fully — the "marriage-before-concession"/shrink-and-conquer technique that solved the 2D case is the natural template; understand exactly where it fails for d ≥ 4.
2. Read TOPP Problem 15 (The Open Problems Project, Demaine et al.) for the community's precise statement and partial results.
3. Study Chazelle's deterministic hull algorithm (via derandomized incremental construction) and Clarkson–Shor randomized incremental analysis; the open problem is essentially "make the log n term depend on f instead."
4. Main obstacle: in high dimensions, intermediate structures (conflict graphs, ε-nets, ray-shooting data structures) cost more than f; a natural attack is Chan's grouping technique combined with high-dimensional shallow cutting / simplicial partitions (Matoušek), trading recursion depth against output size.

## Key references

- T. M. Chan, "Optimal output-sensitive convex hull algorithms in two and three dimensions", Discrete & Computational Geometry 16:361–368, 1996. Achieves O(n log f) in 2D (and 3D results); the key reference technique-wise. (verify exact title/pages)
- T. M. Chan, "Output-sensitive results on convex hulls, extreme points, and related problems", Discrete & Computational Geometry 16:369–387, 1996. Establishes the best known output-sensitive tradeoffs including higher-dimensional bounds.
- The Open Problems Project, Problem 15 ("O(n log k) time algorithms for convex hulls"), Demaine, O'Rourke, et al.; http://cs.smith.edu/~jorourke/TOPP/ — authoritative problem statement and progress log.
- B. Chazelle, "An optimal convex hull algorithm in any fixed dimension", Discrete & Computational Geometry 10:377–429, 1993. Optimal worst-case O(n log n + n^⌊d/2⌋) deterministic algorithm via derandomization.
- K. L. Clarkson, P. W. Shor, "Applications of random sampling in computational geometry, II", Discrete & Computational Geometry 4:387–421, 1989. Randomized incremental hull construction, O(n log n + f) expected.

## Warnings

- "Fixed dimension" means constants may depend exponentially on d; do not chase bounds uniform in d.
- Clarify whether f counts facets or all faces — cite the Upper Bound Theorem when converting.
- The 2D O(n log h) extreme-points algorithm is *not* directly the hull problem; hull output sensitivity is strictly subtler in d ≥ 3.
- Kirkpatrick–Seidel-style pruning relies on order properties (sorting by coordinate) absent in higher dimensions — a common reason transplanted proofs fail.
- Verify all citations and the current d = 3, 4 status before claiming novelty; this problem has a long literature of incremental improvements.

---
*`ALGO-000149` · unverified*

## Acceptance guidance

1. **Upper bound (main):** a deterministic or randomized algorithm for every fixed d computing the hull in O(n log f + f) time (expected time acceptable if stated).
2. **Lower bound:** a proof that Ω(n log f) is unavoidable for all d ≥ 2 (essentially known via sorting reductions; formalizing suffices).
3. Together, a matching bound settling TOPP Problem 15.
4. Partial credit: an algorithm achieving O(n log f + f · polylog f) or removing the mixed (nf)^{1−…} term would be significant progress.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/af83cc81-825f-47bc-a778-fc486bb67c33?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000149.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000149)
