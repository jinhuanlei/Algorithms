## Edit Distance
Given two strings of alphanumeric characters, determine the minimum number of Replace, Delete, and Insert operations needed to transform one string into the other.

#### Assumptions

Both strings are not null

#### Examples

string one: “sigh”, string two : “asith”

the edit distance between one and two is 2 (one insert “a” at front then replace
 “g” with “t”).
 
 #### Analysis
 
 Case 0 : s1[x] == s2[x]  ==> ignore
 
 Case 1 : s1[x] != s2[x]
 
1. replace M[i][j] = M[i - 1][j - 1] + 1
1. delete M[i][j] = M[i - 1][j] + 1
1. insert M[i][j] = M[i][j - 1] + 1

Case case : 
1. M[0][0] = 0
1. M[0][j] = j
1. M[i][0] = i

Induction rule :
1.  M[i][j] represents the minimum number of actions to transform the first i 
    letters of S1 to the first j letters of S2.
1. M[i][j] = M[i - 1][j - 1]         ==>    s1[i - 1] == s2[j - 1]

   M[i][j] = min(M[i - 1][j - 1], M[i - 1][j], M[i][j - 1])   ==>   otherwise