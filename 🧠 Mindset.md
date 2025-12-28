1. **Understand the problem deeply** (UX + data).
2. **Plan components & data flow.**
3. **Define types before code.**
4. **Think about state placement.**
5. **Prioritize UX and accessibility.**
6. **Focus on performance.**
7. **Respect the design system.**
8. **Write maintainable, minimal code.**
9. **Don’t over-engineer.**
10. **Consider testing and edge cases.**

## **1. Clarify the Problem First**
Before thinking about components or code, ask yourself:
- What _exactly_ is the user trying to do?
- What is the data flow?
- What changes over time? (state)
- What stays constant? (props or config)
- How will the UI respond to each state (loading/error/empty/success)?
> Senior devs spend more time clarifying than coding.
---
## **2. Design the Component Architecture**
Think in terms of **“smart vs. dumb”**, or **container vs. presentational** components.
- What should be reusable?
- What should be isolated?
- What should NOT know about global logic?
Ask:
- Is this a new component or an extension of an existing one?
- Can it be broken down into smaller subcomponents?
- Where should the state live?
---
## **3. Plan the Data Flow**
React is _data in → UI out_.
You should think:
- Does this component need internal state?
- Is this state local, shared, or global?
- Should I lift the state?
- Would a server component simplify this? (RSC-aware mindset)
- Should I memoize something? (useMemo/useCallback)
- Should I treat this as side-effectful logic? (useEffect, but sparingly)
---
## **4. Think About Types Early (TS Mindset)**
Before writing JSX, determine the types:
- What props will the component accept?
- What shape will the data returned from APIs have?
- Should any part be generic?
- Where should types live? (local, shared folder, API response types
Ask:
- What is nullable?
- What errors might emerge?
- Can the TS compiler help me avoid runtime bugs?
---
## **5. User Experience First**
A frontend expert always considers:
- Loading states
- Error states
- Partial states (empty lists, slow networks)
- Accessibility (ARIA, keyboard navigation)
- Responsiveness
- Interaction feedback (animations, micro-interactions)
For every feature:
> “How should the user experience this?”
---
## **6. Performance Considerations**
Think early:
- Can this re-render too often?
- Should I wrap it with `memo`?
- Should this fetch be cached (React Query / RSC caching)?
- Are large components or libraries lazy-loadable?
- Can the list use virtualization?
Ask:
- “What is the worst-case performance scenario for this component?”
---
## **7. Consistency & Design System Awareness**
A senior dev asks:
- Does this fit the UI system?
- Are there existing components to reuse?
- Is this styled using the agreed system (Tailwind, CSS modules, shadcn, etc.)?
---
## **8. Build for Maintainability**
Think:
- Could someone understand this code in 6 months?
- Is state as minimal as possible?
- Are functions small and pure?
- Is the file structured clearly?
- Should I extract logic into hooks? (custom hooks)
- Should this component be colocated or shared?
---
## **9. Avoid Over-Engineering**
Ask:
- Do I actually need context here?
- Is the simplest thing good enough?
- Is this complexity necessary right now?
- How easy is this to refactor -> loosely coupling & high cohesion
Great engineers simplify first — optimize later if needed.
---
## **10. Testing & Edge Cases**
Think:
- What should I unit test? (logic, critical components)
- What user flows could break?
- What assumptions may be wrong?
- How does this behave with:
    - empty data
    - slow API
    - invalid responses
    - user spamming actions
---
## **11. Clean Code Mindset**
Keep in mind:
- Avoid giant components
- Keep render return blocks clean
- Extract logic from JSX whenever possible
- Prefer declarative patterns over imperative ones
- 
───────────────────────────────────────
        FRONTEND MENTAL MODEL           
───────────────────────────────────────

                 ┌───────────────────┐
                 │   1. PROBLEM     │
                 │   UNDERSTANDING  │
                 └───────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ What is the user trying to do?                       │
 │ What are the states (loading/error/empty/ready)?     │
 │ What data flows through this feature?                │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
                 ┌───────────────────┐
                 │   2. COMPONENT   │
                 │   ARCHITECTURE   │
                 └───────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Break UI into components:                            │
 │   - Container vs Presentational                      │
 │   - Reusable vs local                                │
 │ Decide what has state and what receives props        │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
                ┌────────────────────┐
                │   3. DATA FLOW     │
                └────────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Where does state live?                               │
 │   - local (useState)                                 │
 │   - parent (lifted state)                             │
 │   - global store?                                     │
 │ Side-effects? (useEffect, fetches, subscriptions)     │
 │ Memoization needed? (useMemo/useCallback)             │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
               ┌──────────────────────┐
               │   4. TYPES (TS)      │
               └──────────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Define:                                              │
 │   - Props interfaces                                 │
 │   - API response types                               │
 │   - Nullable/optional values                         │
 │   - Enums/unions for clean modeling                  │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
           ┌────────────────────────────────┐
           │        5. UX & ACCESSIBILITY   │
           └────────────────────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Loading, Empty, Error states                         │
 │ Keyboard navigation                                   │
 │ ARIA roles                                            │
 │ Responsiveness + layout                               │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
             ┌──────────────────────────┐
             │   6. PERFORMANCE THINK   │
             └──────────────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Avoid unnecessary state or re-renders                │
 │ Memoization patterns                                 │
 │ Virtualization for large lists                       │
 │ Lazy loading heavy components                        │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
                 ┌────────────────┐
                 │  7. CLEAN CODE │
                 └────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Small pure functions                                 │
 │ Extract hooks for logic                              │
 │ Clear file structure                                 │
 │ No massive render blocks                             │
 └──────────────────────────────────────────────────────┘
                           │
                           ▼
           ┌──────────────────────────────────┐
           │   8. EDGE CASES & TESTABILITY   │
           └──────────────────────────────────┘
                           │
                           ▼
 ┌──────────────────────────────────────────────────────┐
 │ Think through:                                       │
 │   - empty data                                        │
 │   - network failure                                   │
 │   - invalid server data                               │
 │   - rapid user actions                                │
 │ Automated tests for critical logic                   │
 └──────────────────────────────────────────────────────┘
