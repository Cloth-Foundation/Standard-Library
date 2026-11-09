# Collections

## List

Import the public class explicitly:

```cloth
using cloth.collections.List : List

fn main() {
    def values := List<int>::new
    values.append(1)
    values.insert(0, 2)
    def saved = values.toArray()
    values::delete
    println(saved)
}
```

This prints `[2, 1]` and normal completion. `List<T>::new` creates an empty list.
Type arguments are explicit and invariant. The private `ListSlot<T>` helper and
backing field are implementation details; they are not exported.

| Method                         | Result        | Behavior                                                               |
|--------------------------------|---------------|------------------------------------------------------------------------|
| `append(T value)`              | void          | Add an independent value at the end.                                   |
| `get(usize index)`             | T             | Return an independent value at an existing index.                      |
| `insert(usize index, T value)` | void          | Insert before index; size is a valid insertion index.                  |
| `removeAt(usize index)`        | T             | Remove and return an independent value; preserve order.                |
| `size()`                       | usize         | Return the current element count.                                      |
| `clear()`                      | void          | Release stored values and keep reserved capacity for reuse.            |
| `reserve(usize minimum)`       | void          | Ensure capacity for at least this many elements without changing size. |
| `toArray()`                    | T[]           | Return an independent growable rectangular array.                      |
| `copy()`                       | List&lt;T&gt; | Create a separate list identity with independent value storage.        |

Invalid indices and allocation failures stop execution at the first runtime error.
An immutable binding (`:=` or `final`) still permits list mutation. Assigning a
list to another binding copies its class identity, so aliases mutate the same list.
Explicitly delete every created list, including each result of `copy()`.

Strings, arrays and structs copy recursively. Class-valued elements keep their
object identities. Clearing or deleting a list does not delete those objects;
their lifetime remains the caller's responsibility.

`get()` returns a value snapshot. Changing a returned value does not replace the
stored element; use `removeAt()` and `insert()` to replace a value. Class-valued
snapshots retain the same object identity, as described above.

`List<int[]>` accepts rows with different lengths. `copy()` preserves those
independent lengths. `toArray()` checks the ordinary rectangular array rules and
fails when present rows have incompatible dimensions. Empty and nullable rows
follow the same receiving rules as other arrays. Each stored slot keeps its own
shape; clearing a list imposes no width on later elements.

Use `get()` and `size()` to traverse a list. Class indexing, indexed assignment,
`::size` as a collection count, and direct foreach are separate language features.
Exported arrays support ordinary array operations and snapshot foreach traversal.

## Deque, Queue, and Stack

Import each class from its own source file.

```cloth
using cloth.collections.Deque : Deque
using cloth.collections.Queue : Queue
using cloth.collections.Stack : Stack

fn main() {
    def jobs := Queue<string>::new
    jobs.enqueue("first")
    jobs.enqueue("second")
    while (!jobs.isEmpty()) println(jobs.dequeue())
    jobs::delete
}
```

All three start empty and accept explicit invariant element types.

| Type       | Add                                       | Remove and return T       | Peek and return T           |
|------------|-------------------------------------------|---------------------------|-----------------------------|
| `Deque<T>` | `pushFront(T value)`, `pushBack(T value)` | `popFront()`, `popBack()` | `peekFront()`, `peekBack()` |
| `Queue<T>` | `enqueue(T value)` at the back            | `dequeue()` at the front  | `peek()` at the front       |
| `Stack<T>` | `push(T value)` at the top                | `pop()` at the top        | `peek()` at the top         |

Each type supplies `size()` returning `usize`, `isEmpty()` returning `bool`,
`clear()`, and `reserve(usize minimum)`. Clear releases the stored values and
retains backing capacity. Reserve ensures backing capacity without changing
size or order. Deque and Queue reserve space on both sides and may allocate
temporary storage when rebalancing.

Use `isEmpty()` to handle expected emptiness. Removal or peek on an empty
collection terminates at the ordinary array bounds diagnostic. A stored null
is a valid element when T is nullable.

Insertion, removal, and peek use ordinary value copies. Strings, arrays, and
structs have independent buffers, and array elements can have different lengths.
Class elements retain their identities. Collection bindings can alias the same
object, and an immutable binding still permits collection mutation. Explicitly
delete each collection. Callers remain responsible for deleting class elements.

Stack pushes and deque pushes take amortized constant time in the element
count. Stack pops and all peeks take constant time in that count. Deque and
Queue removal takes amortized constant time, with occasional linear rebalancing.
Copying a buffered element also depends on the size of its value.
