## Programming Principles Analysis


### SRP (Single Responsibility Principle)
Each method has a clear, focused purpose: [`PrintEntrant`](./Program.cs#L148) prints, [`SortEntrantsByPoints`](./Program.cs#185) sorts, [`GetEntrantsInfo`](./Program.cs#175) extracts stats. The `Entrant` struct handles its own domain logic (`GetCompMark`, `GetBestSubject`, `GetWorstSubject`) while I/O remains in `Program`. The [`Main`](./Program.cs#201) method, however, mixes menu rendering, input dispatching, and application state management.

---

### Encapsulation
Domain logic (`GetCompMark`, `GetBestSubject`, `GetWorstSubject`) is correctly placed inside the `Entrant` struct rather than in `Program`. However, all struct fields (`Name`, `IdNum`, etc.) are `public` with no access control, which breaks encapsulation — they should use properties with getters/setters.

---

### Separation of Concerns
Data structures (`Entrant`, `ZNO`), I/O (`ReadEntrantsArray`, `PrintEntrant`), and business logic (`GetCompMark`, sorting methods) are distinct layers. The console rendering and data logic do not bleed into each other significantly.

---

### DRY (Don't Repeat Yourself)
The `Input()` method is overloaded for both `int` and `double`, centralizing validation logic (error messages, negative number checks) rather than copy-pasting it everywhere user input is needed.
---

### KISS (Keep It Simple, Stupid)
Most logic is straightforward. The ternary chain in the sort comparators (markA > markB ? -1 : markA < markB ? 1 : 0) is slightly harder to read than markB.CompareTo(markA) would be.
