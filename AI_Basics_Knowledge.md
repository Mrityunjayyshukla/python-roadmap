## 2. Knowledge
Knowledge is required by AI agents to do a particular job.<br>
<b>Knowledge based agents: </b> agents that reason by operating on internal representations of knowledge.<br>
<p></p>
Logic is used to represent knowledge.<br>
There are certain terminologies used in logic like:

- <b>Sentence: </b> An assertion about the world in a knowledge representation language.
- <b>Propositional Logic: </b> A logic which uses sentences in the form of propositions (symbols).
- <b>Logical Connectives: </b> These are some connection symbols that are used to connect to or more sentences together.

  ```
    1. negation ( ¬ )
    2. conjunction/and ( ∧ )
    3. disjunction/or ( ∨ )
    4. implication ( → )
    5. biconditional ( ↔ )
  ```

<p></p>

### Negation / Not (¬)
Negation is used to represent the negative of a sentence. So if a sentence is positive statement, it's negation will be negative. <br>

| P     | ¬P    |
|-------|-------|
| True  | False |
| False | True  |

### Conjunction / And (∧)
Conjunction is used to connect two sentences in a such a way that the conjunction of the two sentences is only true if and only if both the sentences are seperately true.<br>

| P     | Q     | P ∧ Q |
| ----- | ----- | ----- |
| False | False | False |
| False | True  | False |
| True  | False | False |
| True  | True  | True  |

### Disjunction / Or (∨)
Disjunction is used to connect two sentences in such a way that the disjunction of the two sentences is true if either one or both the sentences are true.<br>

| P     | Q     | P∨Q   |
| ----- | ----- | ----- |
| False | False | False |
| False | True  | True  |
| True  | False | True  |
| True  | True  | True  |
