### Numbrix Puzzle Solver (IA / Artificial Intelligence, IST)
- **Repo:** ia-project-ist
- **One-liner:** A Python constraint-satisfaction solver for the Numbrix logic puzzle, built on a classic tree-search framework, for a university Artificial Intelligence course.
- **Problem it solves:** Numbrix is an N×N grid puzzle where a partially-filled board must be completed so the numbers 1..N² form a single chain of orthogonally-adjacent consecutive integers. The project formulates this as a state-space search problem and finds a valid completion for a given instance read from a file.
- **What was built** (all original work is in `numbrix.py`; `search.py` and `utils.py` are the course-provided AIMA `aima-python` template library, not authored here):
  - A `Board` representation with file parsing (`parse_instance`), O(1) adjacency queries (horizontal/vertical neighbours), and incremental tracking of filled/missing values.
  - A `Numbrix(Problem)` subclass implementing the search interface: `actions`, `result`, and `goal_test`, wired into the provided search functions.
  - A constraint-pruned `actions` generator that, rather than enumerating all placements, picks the next missing value in a heuristically sorted order and only proposes cells that could legally continue the chain (forced-sequence detection, dead-end / isolated-cell pruning, endpoint handling for 1 and N²).
  - A domain heuristic `h` combining a "sparseness / number-of-sequences" ratio with feasibility pruning: an `acceptable_distance_to_all_filled_values` check using Manhattan distance plus a parity (odd/even) constraint between values and grid positions to reject unreachable states early (returns `inf`).
  - An immutable-style `result` that builds a fresh `Board`/state per move (explicitly replacing an earlier `copy.deepcopy` approach, per commit history) and marks boards impossible when a placed value has no room to extend.
  - A CLI entry point (`python numbrix.py <input_file>`) that parses an instance, solves it with greedy best-first search, and prints the completed board; scaffolding for BFS/DFS/A*/RBFS and a `compare_searchers` benchmarking path is present but commented out.
- **Skills demonstrated:**
  - Languages: Python 3.
  - Frameworks/libraries: standard library only (`sys`, `copy`, `time`); reused the course-supplied AIMA search framework (`Problem`/`Node`/`best_first_graph_search`, etc.). No third-party dependencies, no package manifest.
  - Tools/infra: git (feature-branch + merge PR workflow visible in history). No tests, CI, containerization, or build tooling.
  - Concepts/techniques: state-space search and problem formulation; greedy best-first / A* (algorithm selected: greedy); admissible-style domain heuristic design; constraint propagation and forward-checking-style pruning; parity-based reachability pruning; Big-O annotations throughout (self-reported O(1)–O(N⁴) per method).
- **Scope & complexity:** Team project — group 39, two students (code header: "Joao Silva", "Maria Varanda"; README repeats these names; all commits are authored under the repo owner's account `Uhphonsoo` / joao.afonso.hs@gmail.com). Single-file original contribution (~720 lines) on top of a ~2,300-line provided library. A substantial single-assignment exercise: non-trivial heuristic and pruning engineering, but narrow in scope (one puzzle, one entry point) and not a multi-module system.
- **CV-relevance signals:**
  - Strengths: a genuinely non-trivial search/CSP implementation with a hand-designed heuristic and multiple pruning strategies (parity constraint, dead-end detection, forced-move detection) — more than boilerplate; iterative optimization is evidenced in commit history ("Improve heuristic", "Implement faster goal testing", "Get rid of deepcopy", "new actions() method"); clean separation of the student code from the framework; consistent complexity reasoning.
  - Weaknesses: academic single-exercise scope; no automated tests, CI, packaging, or documentation beyond a 3-line README; only one search strategy actually enabled (others commented out); no real-world dataset or deployment; correctness rests on the course's own grader, not reproducible here.
- **Evidence gaps:**
  - No test inputs or expected outputs are committed, so I could not run or verify that the solver produces correct solutions or its performance on larger N.
  - Author attribution is ambiguous: the README/code name two students but 100% of git commits are under a single account; the individual split of work within the pair is unverifiable.
  - The assignment specification (`Enunciado-P3-09Mar.pdf`) is present but is a binary I did not parse; heuristic-quality and grading claims could not be cross-checked against it.
  - Dates/recency: development commits span **Mar 2022 – Jan 2023** (course academic year 2021/2022); the Jan 2023 commit is a minor "final version" touch-up. Effectively a 2022 project.
</content>
</invoke>
