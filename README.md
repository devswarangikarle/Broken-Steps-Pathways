# Broken-Steps-Pathways

Leo is about to climb a staircase with N steps, starting from the ground (step 0) and aiming to reach the top (step N). He has two options for each move: either take a single step or a double step (skipping one). However, some steps are damaged - specifically steps S1, S2, …, SM - and Leo must avoid these broken steps as he climbs. How many distinct ways can Leo reach the top of the staircase? Since the total count could be large, return the answer modulo 1,000,000,007.

def count_ways(N, M, broken_steps):
    MOD = 1_000_000_007
    dp = [0] * (N + 1)
    dp[0] = 1  # There's one way to be at step 0
    
    # Mark broken steps
    broken = set(broken_steps)
    
    for i in range(1, N + 1):
        if i not in broken:
            dp[i] = dp[i - 1]
            if i > 1:
                dp[i] += dp[i - 2]
            dp[i] %= MOD  # Take modulo to avoid overflow
    
    return dp[N]

# Input reading
N, M = map(int, input().split())
broken_steps = [int(input()) for _ in range(M)]

# Compute and print result
print(count_ways(N, M, broken_steps))

