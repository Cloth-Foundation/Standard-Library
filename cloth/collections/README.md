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
| `set(usize index, T value)`    | void          | Replace the whole value at an existing index.                          |
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

`list[index]` and `list.get(index)` both take a `usize` index and return an
independent value of `T`. Replace an element with `list[index] = value` or
`list.set(index, value)`. Bracket writes check the captured list and index
before the right-hand side and again before writing. `set()` checks the
index inside the method after ordinary argument evaluation.

Use compound assignments and standalone `++` or `--` when the element type
supports the operation. A compound assignment reads the old value before
evaluating the right-hand side. To edit an array element stored in a list,
read the whole array into a binding, edit it there, and assign it back.

`List<int[]>` accepts rows with different lengths. Replacement gives the new
row its own shape and preserves the list's count. `copy()` preserves those
independent lengths. `toArray()` checks the ordinary rectangular array rules and
fails when present rows have incompatible dimensions. Empty and nullable rows
follow the same receiving rules as other arrays. Each stored slot keeps its own
shape; clearing a list imposes no width on later elements.

Use `for (def item <- list)` to traverse the list in order. Each loop entry
captures the elements before the first iteration. The loop visits that
snapshot even if the body edits or deletes the source list. Array elements
keep their independent shapes, and class elements keep their checked
identities. A nullable element uses an explicitly typed loop binding.

## OwningList

`OwningList<T>` accepts non-null classes and class-backed interface types.
`append(value)` gives the list deletion authority over the object. The same
object can occupy only one slot in one owning list. Inserting an already owned
object or creating an ownership cycle raises an ownership error.

```cloth
using cloth.collections.OwningList : OwningList

typedef<class> Item (pub def<int> value) {
    ~Item { println(value) }
}

fn main() {
    def items = OwningList<Item>::new
    items.append(Item::new(1))
    items.append(Item::new(2))
    items[0].value = 10
    for (def item <- items) println(item.value)

    def taken = items.removeAt(0)
    items::delete
    taken::delete
}
```

| Operation | Result | Behavior |
|---|---|---|
| `OwningList<T>::new` | `OwningList<T>` | Create an empty owning list. |
| `append(T value)` | void | Add the object at the end and acquire deletion authority. |
| `get(usize index)` or `items[index]` | `T` | Return a checked alias to the object. |
| `removeAt(usize index)` | `T` | Remove the entry and return its live object. The caller takes responsibility for deletion. |
| `size()` | `usize` | Return the current count. |
| `clear()` | void | Delete all owned objects in list order and leave the list empty and usable. |
| `items::delete` | void | Delete all owned objects in list order and destroy the list. |

Aliases can read and mutate the live object while the list owns it. After
`removeAt`, any live alias can delete the object or give it to an owning list.
Direct foreach captures the entries in order before the first iteration. The
snapshot holds aliases, so deleting an object also invalidates its snapshot entry.

During `clear()`, element destructors see an empty list. Attempts to append,
remove, clear, or delete that list during cleanup raise a runtime error. During
list destruction, ordinary access through aliases to the list fails its liveness
check. Aliases to each deleted element become stale as its destructor begins.

## Snapshot

Import `Snapshot` and `emptySnapshot` from `cloth.collections.Snapshot` to
give your own collection a `foreach` operator. Append elements in traversal
order and return the snapshot.

```cloth
using cloth.collections.Snapshot : Snapshot, emptySnapshot

typedef<class> Pair (def<int> first, def<int> second) {
    pub operator foreach() -> Snapshot<int> {
        def snapshot = emptySnapshot<int>()
        snapshot.append(first)
        snapshot.append(second)
        return snapshot
    }
}
```

The loop manages the snapshot's storage. Each iteration receives an
independent value under the same rules as array foreach.

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
