# Logistics Package Sorting — Merge Sort vs Quick Sort

## Problem Statement
A logistics company receives package weights (each package also has a unique ID):

```
ID:     P1  P2  P3  P4  P5  P6  P7  P8
Weight: 20  15  20  10  15  20  25  10
```

**Tasks:**
- (a) Implement Merge Sort and Quick Sort in C to sort packages by weight; record intermediate steps.
- (b) Modify the program so packages of equal weight keep their original relative order; verify using package IDs.
- (c) Analyse both algorithms on: duplicate values, stability, number of comparisons, time complexity, space complexity — and determine which is more suitable when order-preservation matters.

## Repository Structure
```
├── src/
│   ├── merge_sort.c           # Part (a) — Merge Sort (naturally stable)
│   ├── quick_sort.c           # Part (a) — Quick Sort (plain, unstable)
│   └── quick_sort_stable.c    # Part (b) — Quick Sort modified with (weight, orig_index) tie-break
├── input/
│   └── weights.txt            # Input data: package ID + weight
├── output/
│   ├── output_mergesort.txt
│   ├── output_quicksort.txt
│   └── output_quicksort_stable.txt
├── docs/
│   ├── trace_table.md          # Step-by-step execution trace for all 3 programs
│   ├── complexity_analysis.md  # Time & space complexity (best/avg/worst case)
│   ├── comparison_table.md     # Side-by-side comparison of both algorithms
│   └── conclusion.md           # Final justified recommendation
└── README.md
```

## How to Compile & Run
```bash
cd src
gcc -o merge_sort merge_sort.c && ./merge_sort
gcc -o quick_sort quick_sort.c && ./quick_sort
gcc -o quick_sort_stable quick_sort_stable.c && ./quick_sort_stable
```
Each program reads `../input/weights.txt`, prints a full trace of its intermediate steps, the final sorted list (with package ID + original index so stability can be checked visually), the total number of comparisons, and an automatic stability check.

## Key Results (n = 8)

| Algorithm | Comparisons | Stable? | Final ID order |
|---|---|---|---|
| Merge Sort | 16 | Yes | P4, P8, P2, P5, P1, P3, P6, P7 |
| Quick Sort (plain) | 18 | **No** | P8, P4, P5, P2, P1, P3, P6, P7 |
| Quick Sort (stable, tie-broken by original index) | 18 | Yes | P4, P8, P2, P5, P1, P3, P6, P7 |

The modified Quick Sort's output is **identical** to Merge Sort's output (verified with `diff`), confirming the fix works.

## Complexity Summary

| | Merge Sort | Quick Sort |
|---|---|---|
| Best | O(n log n) | O(n log n) |
| Average | O(n log n) | O(n log n) |
| Worst | O(n log n) | O(n²) |
| Space | O(n) | O(1) data / O(log n)–O(n) stack |
| Stable (standard form) | Yes | No |

See `docs/complexity_analysis.md` for full derivations and `docs/comparison_table.md` / `docs/conclusion.md` for the full analysis and final justified recommendation.

## Conclusion (short version)
**Merge Sort is the more suitable choice** when preserving the original relative order of equal-weight packages matters — it is stable by construction and guarantees O(n log n) time in every case, at the cost of O(n) extra memory. Quick Sort can be made to behave the same way only by adding an explicit original-index tie-break, and even then keeps its O(n²) worst-case risk. Full reasoning in `docs/conclusion.md`.
