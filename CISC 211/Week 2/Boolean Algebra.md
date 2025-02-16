# Boolean Algebra

1. Flowchart:

![Boolean Algebra](https://github.com/user-attachments/assets/1eb65ba9-3e26-4820-aa49-f52eba99c794)

2. My main challenge in performing the lab was figuring out how the boolean algebra properties work.
3. Equation: F = A′B′C′+ A′B′C + A′BC + AB′C + ABC′
Group terms to find common factors:
(A′B′C′ + A′B′C) + (A′BC + AB′C + ABC′)
Factor common terms:
First Group:
Factor out A′B′: (A′B′C′ + A′B′C) = A′B′(C′ + C)
C′ + C = 1, which simplifies to A′B′(1) = A′B′
Second Group:
A′BC + AB′C = C(A′B + AB′)
Simplify A′B + AB′ using Distributive Law: A′B + AB′ = (A′ + B′)(A + B)
Simplifies to C(A + B)
Third Group:
ABC′, stays the same
Step 3: Put everything together:
F = A′B′ + C(A + B) + ABC′
Step 4: Simplify
Expand C(A + B): C(A + B) = CA + CB
F = A′B′ + CA + CB + ABC′
Absorb ABC′ into CA: F = A′B′ + CA + CB
Final Answer:
F = A′B′ + CA + CB
Motion sensing light equation: i=(m⋅t′)+(t⋅m′)+(t⋅m)
