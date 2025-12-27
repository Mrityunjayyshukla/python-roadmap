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

### Implication (→)
Implication is used to connect two sentences in such a way that the implication will only be false if first sentence is true and second sentence is false.

| P     | Q     | P→Q   |
| ----- | ----- | ----- |
| False | False | True  |
| False | True  | True  |
| True  | False | False |
| True  | True  | True  |

### Biconditional (↔)
Biconditional connects the sentence in a way that the bicondition will be only true if both the sentences are either true or false.

| P     | Q     | P↔Q   |
| ----- | ----- | ----- |
| False | False | True  |
| False | True  | False |
| True  | False | False |
| True  | True  | True  |

<p></p>
<b>Model: </b> Assignment of a truth value to every propositional symbol (a "possible world").<br>
For Example:<br>
<b>P: It is raining</b><br>
<b>Q: It is a Tuesday</b><br>
So, if {P=True, Q=False}, we can say that this is one of the possible models.<br>
<p></p>
<b>Knowledge Base: </b> A set of sentences known by a knowledge based agent. The set of propositional logic that are known by the agent form the knowledge base.<br>
<p></p>
For knowledge base, we introduce:<br>
<b>Entailment (a⊨b): </b> In every model in which sentence 'a' is true, sentence 'b' will also be true.<br>
<p></p>
So, for deriving new sentences, we use something called <b>Inference</b>.<br>
<b>Inference: </b> The process of deriving new sentences from old sentences.
<p></p>

```
P: It is a Tuesday.
Q: It is raining.
R: Harry will go for a run.

Knowledge Base:
(P∧¬Q)→R : It is a Tuesday and it is NOT raining, that implies that Harry will go for a run.
P is true.
¬Q is true.

From this, we can conclude and inference that:
R is true as P and ¬Q is true so if (P∧¬Q) is true, then R is true.
```

We require an algorithm which can prove that Knowledge base⊨a.<br>
The first algorithm that we have is:<br>

- <b>Model Checking</b><br>
  To determine if KB⊨a:
  - Enumerate all possible models.
  - If in every model where KB is true, a is true, then KB entails a.
  - Otherwise, KB does not entail a.

  Here's how it works in Python:

  ```
  import itertools
  class Sentence():
      def evaluate(self, model):
          """Evaluates the logical sentence."""
          raise Exception("nothing to evaluate")
  
      def formula(self):
          """Returns string formula representing logical sentence."""
          return ""
  
      def symbols(self):
          """Returns a set of all symbols in the logical sentence."""
          return set()
  
      @classmethod
      def validate(cls, sentence):
          if not isinstance(sentence, Sentence):
              raise TypeError("must be a logical sentence")
  
      @classmethod
      def parenthesize(cls, s):
          """Parenthesizes an expression if not already parenthesized."""
          def balanced(s):
              """Checks if a string has balanced parentheses."""
              count = 0
              for c in s:
                  if c == "(":
                      count += 1
                  elif c == ")":
                      if count <= 0:
                          return False
                      count -= 1
              return count == 0
          if not len(s) or s.isalpha() or (
              s[0] == "(" and s[-1] == ")" and balanced(s[1:-1])
          ):
              return s
          else:
              return f"({s})"
  
  
  class Symbol(Sentence):
  
      def __init__(self, name):
          self.name = name
  
      def __eq__(self, other):
          return isinstance(other, Symbol) and self.name == other.name
  
      def __hash__(self):
          return hash(("symbol", self.name))
  
      def __repr__(self):
          return self.name
  
      def evaluate(self, model):
          try:
              return bool(model[self.name])
          except KeyError:
              raise EvaluationException(f"variable {self.name} not in model")
  
      def formula(self):
          return self.name
  
      def symbols(self):
          return {self.name}
  
  
  class Not(Sentence):
      def __init__(self, operand):
          Sentence.validate(operand)
          self.operand = operand
  
      def __eq__(self, other):
          return isinstance(other, Not) and self.operand == other.operand
  
      def __hash__(self):
          return hash(("not", hash(self.operand)))
  
      def __repr__(self):
          return f"Not({self.operand})"
  
      def evaluate(self, model):
          return not self.operand.evaluate(model)
  
      def formula(self):
          return "Â¬" + Sentence.parenthesize(self.operand.formula())
  
      def symbols(self):
          return self.operand.symbols()
  
  
  class And(Sentence):
      def __init__(self, *conjuncts):
          for conjunct in conjuncts:
              Sentence.validate(conjunct)
          self.conjuncts = list(conjuncts)
  
      def __eq__(self, other):
          return isinstance(other, And) and self.conjuncts == other.conjuncts
  
      def __hash__(self):
          return hash(
              ("and", tuple(hash(conjunct) for conjunct in self.conjuncts))
          )
  
      def __repr__(self):
          conjunctions = ", ".join(
              [str(conjunct) for conjunct in self.conjuncts]
          )
          return f"And({conjunctions})"
  
      def add(self, conjunct):
          Sentence.validate(conjunct)
          self.conjuncts.append(conjunct)
  
      def evaluate(self, model):
          return all(conjunct.evaluate(model) for conjunct in self.conjuncts)
  
      def formula(self):
          if len(self.conjuncts) == 1:
              return self.conjuncts[0].formula()
          return " âˆ§ ".join([Sentence.parenthesize(conjunct.formula())
                             for conjunct in self.conjuncts])
  
      def symbols(self):
          return set.union(*[conjunct.symbols() for conjunct in self.conjuncts])
  
  
  class Or(Sentence):
      def __init__(self, *disjuncts):
          for disjunct in disjuncts:
              Sentence.validate(disjunct)
          self.disjuncts = list(disjuncts)
  
      def __eq__(self, other):
          return isinstance(other, Or) and self.disjuncts == other.disjuncts
  
      def __hash__(self):
          return hash(
              ("or", tuple(hash(disjunct) for disjunct in self.disjuncts))
          )
  
      def __repr__(self):
          disjuncts = ", ".join([str(disjunct) for disjunct in self.disjuncts])
          return f"Or({disjuncts})"
  
      def evaluate(self, model):
          return any(disjunct.evaluate(model) for disjunct in self.disjuncts)
  
      def formula(self):
          if len(self.disjuncts) == 1:
              return self.disjuncts[0].formula()
          return " âˆ¨  ".join([Sentence.parenthesize(disjunct.formula())
                              for disjunct in self.disjuncts])
  
      def symbols(self):
          return set.union(*[disjunct.symbols() for disjunct in self.disjuncts])
  
  
  class Implication(Sentence):
      def __init__(self, antecedent, consequent):
          Sentence.validate(antecedent)
          Sentence.validate(consequent)
          self.antecedent = antecedent
          self.consequent = consequent
  
      def __eq__(self, other):
          return (isinstance(other, Implication)
                  and self.antecedent == other.antecedent
                  and self.consequent == other.consequent)
  
      def __hash__(self):
          return hash(("implies", hash(self.antecedent), hash(self.consequent)))
  
      def __repr__(self):
          return f"Implication({self.antecedent}, {self.consequent})"
  
      def evaluate(self, model):
          return ((not self.antecedent.evaluate(model))
                  or self.consequent.evaluate(model))
  
      def formula(self):
          antecedent = Sentence.parenthesize(self.antecedent.formula())
          consequent = Sentence.parenthesize(self.consequent.formula())
          return f"{antecedent} => {consequent}"
  
      def symbols(self):
          return set.union(self.antecedent.symbols(), self.consequent.symbols())
  
  
  class Biconditional(Sentence):
      def __init__(self, left, right):
          Sentence.validate(left)
          Sentence.validate(right)
          self.left = left
          self.right = right
  
      def __eq__(self, other):
          return (isinstance(other, Biconditional)
                  and self.left == other.left
                  and self.right == other.right)
  
      def __hash__(self):
          return hash(("biconditional", hash(self.left), hash(self.right)))
  
      def __repr__(self):
          return f"Biconditional({self.left}, {self.right})"
  
      def evaluate(self, model):
          return ((self.left.evaluate(model)
                   and self.right.evaluate(model))
                  or (not self.left.evaluate(model)
                      and not self.right.evaluate(model)))
  
      def formula(self):
          left = Sentence.parenthesize(str(self.left))
          right = Sentence.parenthesize(str(self.right))
          return f"{left} <=> {right}"
  
      def symbols(self):
          return set.union(self.left.symbols(), self.right.symbols())
  
  
  def model_check(knowledge, query):
      """Checks if knowledge base entails query."""
  
      def check_all(knowledge, query, symbols, model):
          """Checks if knowledge base entails query, given a particular model."""
  
          # If model has an assignment for each symbol
          if not symbols:
  
              # If knowledge base is true in model, then query must also be true
              if knowledge.evaluate(model):
                  return query.evaluate(model)
              return True
          else:
  
              # Choose one of the remaining unused symbols
              remaining = symbols.copy()
              p = remaining.pop()
  
              # Create a model where the symbol is true
              model_true = model.copy()
              model_true[p] = True
  
              # Create a model where the symbol is false
              model_false = model.copy()
              model_false[p] = False
  
              # Ensure entailment holds in both models
              return (check_all(knowledge, query, remaining, model_true) and
                      check_all(knowledge, query, remaining, model_false))
  
      # Get all symbols in both knowledge and query
      symbols = set.union(knowledge.symbols(), query.symbols())
  
      # Check that knowledge entails query
      return check_all(knowledge, query, symbols, dict())
  ```
  Applying it will be like this:

  ```
  from logic import *
  rain = Symbol("rain")
  hagrid = Symbol("hagrid")

  knowledge = And(
    Implication(Not(rain), hagrid),
    Or(hagrid, dumbledore),
    Not(And(haagrid, dumbledore)),
    dumbledore
  )
  
  print(knowledge.formula())
  print(model_check(knowledge, rain))  #True
  ```
2:53:58
  
