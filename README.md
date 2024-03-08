# POLICY ITERATION ALGORITHM

## AIM
To develop a Python porgram to find the optiml policy for the given MDP using the policy iteration algorithm 

## PROBLEM STATEMENT
The situation is to create a python program where a policy is generated with random actions and for that policy we have to perform policy evaluation and policy improvement to find the optimal new policy and state value function and check for the difference between the new policy and the old policy. The combine operation of the 
policy evaluation and policy improvement is reffered to as policy iteration.

## POLICY ITERATION ALGORITHM
### Step 1: Initialize :
Start with an arbitary policy pi(s) for each state s in the environment.
### Step 2: Policy Evaluation:
Evaluate the current policy pi(s) by estimating the state-value function vpi(s) or action value Qpi(s,a) which can be achieved by using iterative policy evaluation method.
Stop the iteration when the difference is less than the threshold value.
### Step 3: Policy Improvement:
Update the policy pi by acting greedily with respect to the value function.Stop the iteration when the previous policy is equal to the current policy  

### Step 4: Policy Iteration:
Here the algorithm alternates between policy evaluation and policy improvement steps until convergence to an optimal policy is achieved.

### Step 5: Display the results:
Final print the new optimal policy and state value function.

## POLICY IMPROVEMENT FUNCTION
~~~
def policy_improvement(V, P, gamma=1.0):
    Q = np.zeros((len(P), len(P[0])), dtype=np.float64)
    for S in range(len(P)):
      for a in range(len(P[S])):
        for prob, next_state, reward, done in P[S][a]:
          Q[S][a] += prob*(reward+gamma*V[next_state]*(not done))
      new_pi = lambda S:{s:a for s,a in enumerate(np.argmax(Q,axis=1))}[S]

    return new_pi
~~~

## POLICY ITERATION FUNCTION
~~~
def policy_iteration(P, gamma=1.0, theta=1e-10):
    random_actions = np.random.choice(tuple(P[0].keys()), len(P))
    pi = lambda s: {s:a for s,a in enumerate(random_actions)}[s]
    while True:
      old_pi = {s:pi(s) for s in range(len(P))}
      V = policy_evaluation(pi, P, gamma, theta)
      pi = policy_improvement(V,P,gamma)
      if old_pi == {s:pi(s) for s in range(len(P))}:
        break
    return V, pi
~~~

## OUTPUT:
## Policy 1:
<img width="697" alt="image" src="https://github.com/KoduruSanathKumarReddy/policy-iteration-algorithm/assets/69503902/bc983ffb-33c1-4a89-bb87-379732a2417c">

## Policy Evaluation:
<img width="697" alt="image" src="https://github.com/KoduruSanathKumarReddy/policy-iteration-algorithm/assets/69503902/03647c0f-8833-4a6e-af28-4ccd96fd2354">

## Improved Policy:
<img width="697" alt="image" src="https://github.com/KoduruSanathKumarReddy/policy-iteration-algorithm/assets/69503902/c82c4ed0-0970-4618-ac0b-6f974c94dc8f">


## Value function for improved policy:
<img width="717" alt="image" src="https://github.com/KoduruSanathKumarReddy/policy-iteration-algorithm/assets/69503902/d522244a-9b87-40a6-87b9-39deabef271f">

## Optimal Policy and State value function:
<img width="717" alt="image" src="https://github.com/KoduruSanathKumarReddy/policy-iteration-algorithm/assets/69503902/f35c1a41-95d3-4745-ac56-08a5d70a196e">

## State Value Function:
<img width="717" alt="image" src="https://github.com/KoduruSanathKumarReddy/policy-iteration-algorithm/assets/69503902/c264cbd4-8892-4923-9f70-26d2ac035411">




## RESULT:
Therefore a Python program is successfully developed to find the optimal policy for the given MDP using the policy iteration algorithm.
