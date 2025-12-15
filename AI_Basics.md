# AI Basics
AI can use certain information and on the basis of that, it can draw out conclusions. There are various ways in which AI can work.

## 1. Search
Searching can be done by searching out the most optimal way to go from Initial to Final Point<br>
Some terminologies that can be used is:<br>
<p></p>
<b>1. Agent: </b> Entity that perceives its environment and acts upon that environment.<br>
<b>2. State: </b> Configuration of the agent and its environment.<br>
&emsp;&emsp;<b>2.1 Initial State: </b> The state in which the agent begins.<br>
&emsp;&emsp;<b>2.2 Final State: </b> The state in which the agent has to go.<br>
<b>3. Action: </b> Choices that can be made in a state.<br>
<i>Actions(s)</i> returns the set of actions that can be executed in a state <i>s</i>.<br>
<b>4. Transition Model: </b> a description of what state results from performing any applicable action in any state.<br>
<i>Result(s,a)</i> returns the state resulting from performing action <i>a</i> in state <i>s</i>.<br>
<b>5. State Space: </b> the set of all states reachable from the initial state by any sequence of actions.<br>
<b>6. Goal State: </b> a way to determine whether the current state is goal state or not.<br>
<b>7. Path Cost: </b> Numerical Cost associated with a given path (Most optimal path is the one with the minimum cost).<br>
<p></p>
A Search problem consists of <b>Initial State</b>, <b>Actions</b>, <b>Transition Model</b>, <b>Goal Test</b>, <b>Path cost function</b>
