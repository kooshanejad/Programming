# Stacks and Queues Lab

## Task 1
```
Initial:
[ _, _, _, _, _, _ ]    S.top = 0

PUSH(S,4):
[ 4, _, _, _, _, _ ]    S.top = 1

PUSH(S,1):
[ 4, 1, _, _, _, _ ]    S.top = 2

PUSH(S,3):
[ 4, 1, 3, _, _, _ ]    S.top = 3

POP(S):
[ 4, 1, 3, _, _, _ ]    S.top = 2    (3 removed)

PUSH(S,8):
[ 4, 1, 8, _, _, _ ]    S.top = 3

POP(S):
[ 4, 1, 8, _, _, _ ]    S.top = 2    (8 removed)
```
## Task 2
```
Initial:
[ _, _, _, _, _, _ ]    Q.head = 1, Q.tail = 1

ENQUEUE(Q,4):
[ 4, _, _, _, _, _ ]    Q.head = 1, Q.tail = 2

ENQUEUE(Q,1):
[ 4, 1, _, _, _, _ ]    Q.head = 1, Q.tail = 3

ENQUEUE(Q,3):
[ 4, 1, 3, _, _, _ ]    Q.head = 1, Q.tail = 4

DEQUEUE(Q):
[ 4, 1, 3, _, _, _ ]    Q.head = 2, Q.tail = 4    (4 removed)

ENQUEUE(Q,8):
[ 4, 1, 3, 8, _, _ ]    Q.head = 2, Q.tail = 5

DEQUEUE(Q):
[ 4, 1, 3, 8, _, _ ]    Q.head = 3, Q.tail = 5    (1 removed)
```
## Task 3
```
ENQUEUE(Q, x)

if (Q.head = Q.tail + 1) or (Q.head = 1 and Q.tail = Q.length) then
    error "overflow"
else
    Q[Q.tail] = x
    if Q.tail = Q.length then
        Q.tail = 1
    else
        Q.tail = Q.tail + 1

DEQUEUE(Q)

if Q.head = Q.tail then
    error "underflow"
else
    x = Q[Q.head]
    if Q.head = Q.length then
        Q.head = 1
    else
        Q.head = Q.head + 1
    return x
```
## Task 4
```
INSERT-FRONT(D, x)

if (D.head = D.tail + 1) or (D.head = 1 and D.tail = D.length) then
    error "overflow"
else
    if D.head = 1 then
        D.head = D.length
    else
        D.head = D.head - 1
    D[D.head] = x

INSERT-REAR(D, x)

if (D.head = D.tail + 1) or (D.head = 1 and D.tail = D.length) then
    error "overflow"
else
    D[D.tail] = x
    if D.tail = D.length then
        D.tail = 1
    else
        D.tail = D.tail + 1

DELETE-FRONT(D)

if D.head = D.tail then
    error "underflow"
else
    x = D[D.head]
    if D.head = D.length then
        D.head = 1
    else
        D.head = D.head + 1
    return x

DELETE-REAR(D)

if D.head = D.tail then
    error "underflow"
else
    if D.tail = 1 then
        D.tail = D.length
    else
        D.tail = D.tail - 1
    return D[D.tail]
```

Video:
