<h1>ExpNo 5 : Implement Simple Hill Climbing Algorithm</h1> 
<h3>Name: upendra r            </h3>
<h3>Register Number:  212224060290           </h3>
<H3>Aim:</H3>
<p>Implement Simple Hill Climbing Algorithm and Generate a String by Mutating a Single Character at each iteration </p>
<h2> Theory: </h2>
<p>Hill climbing is a variant of Generate and test in which feedback from test procedure is used to help the generator decide which direction to move in search space.
Feedback is provided in terms of heuristic function
</p>


<h2>Algorithm:</h2>
<p>
<ol>
 <li> Evaluate the initial state.If it is a goal state then return it and quit. Otherwise, continue with initial state as current state.</li> 
<li>Loop until a solution is found or there are no new operators left to be applied in current state:
<ul><li>Select an operator that has not yet been applied to the current state and apply it to produce a new state</li>
<li>Evaluate the new state:
  <ul>
<li>if it is a goal state, then return it and quit</li>
<li>if it is not a goal state but better than current state then make new state as current state</li>
<li>if it is not better than current state then continue in the loop</li>
    </ul>
</li>
</ul>
</li>
</ol>

</p>
<hr>
<h3> Steps Applied:</h3>
<h3>Step-1</h3>
<p> Generate Random String of the length equal to the given String</p>
<h3>Step-2</h3>
<p>Mutate the randomized string each character at a time</p>
<h3>Step-3</h3>
<p> Evaluate the fitness function or Heuristic Function</p>
<h3>Step-4:</h3>
<p> Lopp Step -2 and Step-3  until we achieve the score to be Zero to achieve Global Minima.</p>

```
import random
import string


def hamming_distance(a: str, b: str) -> int:
    if len(a) != len(b):
        raise ValueError("Strings must have equal length")
    return sum(x != y for x, y in zip(a, b))


def random_string(n: int, alphabet: str) -> str:
    return "".join(random.choice(alphabet) for _ in range(n))

def mutate_one_char(s: str, alphabet: str) -> str:
    i = random.randrange(len(s))
    new_c = random.choice(alphabet)
    while new_c == s[i]:
        new_c = random.choice(alphabet)
    return s[:i] + new_c + s[i+1:]


def hill_climb_target(
    target: str,
    alphabet: str = string.ascii_letters + string.digits + " .,;:!?'\"()-",
    max_iters: int = 200000,
    patience: int = 5000,
):
    current = random_string(len(target), alphabet)
    current_score = hamming_distance(current, target)

    best = current
    best_score = current_score
    no_improve = 0

    print(f"Score: {current_score} Solution : {current}")

    for it in range(1, max_iters + 1):
        neighbor = mutate_one_char(current, alphabet)
        score = hamming_distance(neighbor, target)

        # Accept only strict improvements
        if score < current_score:
            current, current_score = neighbor, score
            no_improve = 0
            if current_score < best_score:
                best, best_score = current, current_score
            print(f"Score: {current_score} Solution : {current}")
        else:
            no_improve += 1

        # Goal check
        if current_score == 0:
            return {
                "solution": current,
                "distance": 0,
                "iterations": it,
                "converged": True,
                "reason": "Reached global minimum (zero distance).",
            }

        # Stop if stuck without improvement
        if no_improve >= patience:
            return {
                "solution": best,
                "distance": best_score,
                "iterations": it,
                "converged": best_score == 0,
                "reason": f"No improvement for {patience} consecutive mutations.",
            }

    return {
        "solution": best,
        "distance": best_score,
        "iterations": max_iters,
        "converged": best_score == 0,
        "reason": "Max iterations reached.",
    }

if __name__ == "__main__":
    target = "Artificial Intelligence"
    result = hill_climb_target(
        target,
        alphabet=string.ascii_letters + string.digits + " .,;:!?'\"()-",
        max_iters=300000,
        patience=10000,
    )
    print(result)

 ```

<hr>
<h2>Sample Input and Output</h2>
<h2>Sample String:</h2> Artificial Intelligence
<h2>Output:</h2>
Score: 643  Solution :  8RzF:oG ]%;CPORRMe!zGvk<br>
Score: 609  Solution :  8RzF:oG ]%;CPqRRMe!zGvk<br>
Score: 604  Solution :  8RzF:oG ]%;CPqRRMe!zGqk<br>
Score: 594  Solution :  8RzF:oG ]%;CPqRRWe!zGqk<br>
Score: 551  Solution :  8RzF:oGK]%;CPqRRWe!zGqk<br>
Score: 551  Solution :  8RzF:oGK]%;CPqRRWe!zGqk<br>
Score: 551  Solution :  8RzF:oGK]%;CPqRRWe!zGqk<br>
Score: 551  Solution :  8RzF:oGK]%;CPqRRWe!zGqk<br>
Score: 551  Solution :  8RzF:oGK]%;CPqRRWe!zGqk<br>
....................................................<br>
..................................................<br>
................................................<br>
Score: 1  Solution :  Artificial Intelligencf<br>
Score: 1  Solution :  Artificial Intelligencf<br>
Score: 1  Solution :  Artificial Intelligencf<br>
Score: 1  Solution :  Artificial Intelligencf<br>
Score: 0  Solution :  Artificial Intelligence<br>

<H3>Result:</H3>
<p>Therefore, Simple Hill Climbing Algorithm is implemented and a String by Mutating a Single Character at each iteration is generated.</p>
