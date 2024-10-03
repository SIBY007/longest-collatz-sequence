# longest-collatz-sequence
The following iterative sequence is defined for the set of positive integers:

Using the rule above and starting with 13, we generate the following sequence:

It can be seen that this sequence (starting at 13 and finishing at 1) contains 10 terms. Although it has not been proved yet (Collatz Problem), it is thought that all starting numbers finish at 1.

Which starting number,  produces the longest chain? If many possible such numbers are there print the maximum one.

Note: Once the chain starts the terms are allowed to go above .

Input Format

The first line contains an integer  , i.e., number of test cases.
Next  lines will contain an integers .

Constraints

Output Format

Print the values corresponding to each test case.

Sample Input

3
10 
15
20
Sample Output

9
9
19
Explanation

Collatz sequence for  is,

containing  steps and is the longest for 
--------------------------------------------------------------------------------------------------------------------------------------------------
#include <bits/stdc++.h>
using namespace std;

long long memo[10000000] = {0};
long long length[10000000] = {0};
long long ans[5000001] = {0};


long long Collatz(long long n)
{
    long long res = 0;

    while(n != 1)
    {
        if(n < 10000000 && memo[n] != 0)
        {
            return res + memo[n];
        }
        n = (n % 2 == 0) ? n / 2 : n * 3 + 1;
        res++;
    }
    return res + 1;
}

int main()
{
    long long largest = 0;

    for(long long i = 1; i <= 5000000; i++)
    {
        memo[i] = Collatz(i);
        length[memo[i]] = max(length[memo[i]], i);
        largest = max(largest, memo[i]);

        ans[i] = length[largest];
    }
    int t;
    cin >> t;

    while(t--)
    {
        int n;
        cin >> n;

        cout << ans[n] << "\n";
    }

    return 0;
}
