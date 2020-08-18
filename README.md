# Goal of this design study

The Goal of this design study is to try to understand the Hashfusion algorithm, and determine its potential applicability to Unbase/Mindbase as pertains to comutative/associative hashing. Determine if there exists any potential for hash parity between a subgraph of operations versus an intermediate state projection of same.

One of the key requirements of unbase, which has proven stymieing up to this point, is that each host node must be able to share the work of projecting state for a given entity without seeing all the events that contributed it.

## Scenario:

Given Operations A + B + C = State S
Node 1 observes only A and B. Performs X := (A + B)
Node 2 Observes only B and C. Performs Y := (B + C)
Node 3 Observes only A and C. Performs Z := (A + C)
Node 1 Observes Y and arrives at X + Y = S
Node 2 Observes Z and arrives at Y + Z = S
Node 3 Observes X and arrives at Z + X = S

## Three distinct requirements:

1. The operations themselves are able to commute
2. The hashes are identical once all operations are applied
3. Partial states which are fully overlapping those already applied must be ignored or otherwise applied idempotently. Eg: (A+B) + C + (C+A) still equals S. Not S + (C+A)

Some limited exploration of this idea has occurred within design-study-text-editor.

Potential Alternative (Albeit costly)
The alternative to HashFusion is a form of tree hashing whereby all hashes are computed on the "maximum fragmentation tree" of all operations and state, such that all orderings of operations

Bibliography:

- https://www.labs.hpe.com/techreports/2017/HPE-2017-08.pdf
- https://github.com/BrianMonahan/HashFusion/blob/master/src/app/hmt.c (suggest we port this to rust)
- https://www.figma.com/blog/realtime-editing-of-ordered-sequences/
- Real Differences between OT andn CRDT in Building Co-Editiing Systems and Real world applications Sun et al. https://arxiv.org/abs/1905.01517
- https://arxiv.org/abs/1810.00644
- https://www.semanticscholar.org/paper/HashFusion-–-a-method-for-combining-cryptographic-Monahan-Chen/9d70806482b90f2af240c803ed28cdbd7c3ab582
- https://keccak.team/files/TreeHashing.pdf
- https://crypto.stackexchange.com/questions/17935/associative-standard-cryptographic-hash-function
