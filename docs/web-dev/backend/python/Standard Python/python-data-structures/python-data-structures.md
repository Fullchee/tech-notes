# Data Structures

## [Dict](python-dict.md)

## [List](python-lists.md)

## [Custom classes](python-objects/python-custom-classes.md)

## Counter: TODO

```python
collections.counter
```

```python
class Solution:
    def fourSumCount(self, A: List[int], B: List[int], C: List[int], D: List[int]) -> int:
        m = collections.defaultdict(int)
        lists = [A, B, C, D]

        def nSumCount() -> int:
            addToHash(0, 0)
            return countComplements(len(lists) // 2, 0)

        def addToHash(i: int, total: int) -> None:
            if i == len(lists) // 2:
                m[total] += 1
            else:
                for a in lists[i]:
                    addToHash(i + 1, total + a)

        def countComplements(i: int, complement: int) -> int:
            if i == len(lists):
                return m[complement]
            cnt = 0
            for a in lists[i]:
                cnt += countComplements(i + 1, complement - a)
            return cnt

        return nSumCount()
```

## Stacks

-   list
    -   amortized O(1) for inserts and deletes

### `collections.deque`

-   double-ended queue
    -   linked list

Adding: stack is the same as queue

```python
>>> from collections import deque
>>> s = deque()
>>> s.append('eat')
```

```python
>>> s.pop()
'eat'
>>> s.pop()
IndexError: "pop from an empty deque"
```

### `queue.LifoQueue`

-   multi-producers & multi-consumers from different threads
    -   same process
- 

```python
>>> from queue import LifoQueue
>>> s = LifoQueue()
>>> s.put('eat')
>>> s.get()
'eat'
>>> s.get_nowait()
queue.Empty
>>> s.get()
# Blocks / waits forever...
```

## Queues

### `collections.deque`

Adding: stack is the same as queue

```python
>>> from collections import deque
>>> q = deque()
>>> q.append('eat')
```

```python
>>> q.popleft()
'eat'
>>> q.popleft()
IndexError: "pop from an empty deque"
```

### `queue.Queue`

-   multi-producers & multi-consumers from different threads
    -   same process
- 

```python
>>> from queue import Queue
>>> q = Queue()
>>> q.put('eat')
```

```python
>>> q.get()
'eat'
>>> q.get_nowait()
queue.Empty
>>> q.get()
# Blocks / waits forever...
```

### [`multiprocessing.Queue`](https://stackoverflow.com/a/30294648/8479344)

-   similar to `queue.Queue`
-   also handles different processes vs threads

## Priority Queue

### `heapq`

-   binary heap

```python
from heapq import heapq

pq = []

heappush(pq.(2, 'code'))
```

### `queue.PriorityQueue`

-   wrapper around `heapq`
-   supports concurrency (locks, threads, ...)
-   API is class based

```python
from queue import PriorityQueue

q = PriorityQueue()
q.put((2, 'code'))
q.put((1, 'eat'))
q.put((3, 'sleep'))
```
