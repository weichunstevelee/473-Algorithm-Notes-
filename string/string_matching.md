# String Matching
## References:
Books:

1. Algorithms on Strings, Trees, and Sequences.

Papers:

1. Looking for all palindromes: http://algo2006.csie.dyu.edu.tw/paper/2/A24.pdf
## Comparison
Common technique is to find "the suffix of a substring you are looking at that is also a prefix of the whole string!"
Comparison 

Z-algorithm | KMP | Boyer-Moore|Apostolico-Giancarlo | Suffix Tree
------------|:----| -----------| --------|-----|
Easy to implement | Nicely extended to multiple pattern searching | Usually sub-linear and linear time in worst case. This one is preffered in most cases.| Similar to Boyer-Moore, but easier to prove linear time worst case. | Pre-processing, more general, search time proportional to length of the pattern. |
## Z-Algorithm

### Z Value 
Given a string S, $z_i[s]$ is the length of the longest substring in S, starting at position i that matches a prefix of S. 
Example:
Given a string __aabcaabxaaz__

position i | z[i] |
-----------|:-----|
2 | 1|
3 | 0|
4 | 0|
5 | 3| 
6 | 0|
7 | 0|
8 | 0|
9 | 2|
10 | 1| 
11 | 0| 

Notice that we don't really care what is the value of $z_1$ here. 

Let's first assume that we have an efficient algorithm to compute z values, how do we utilize this to efficiently do a string matching? 
It turns out that we only have to do a string concatenation! 
Let S = P#T, where P is the pattern we are looking for in target string T. The punch sign is used to represent an unique character that is not in P and T. We can use null in C.  After we do the concatenation, we can compute the z array, and if at some point $i\geq len(P)+1$, z[i] = len(P), it means that the substring start at position i match the first $len(p)$ characters in S, so we find a match! 

### Z-value computation
In order to compute z values 

```c++
struct zbox{
  size_t l = 0;
  size_t r = 0;
  size_t getLen() const { return r-l;}
  zbox(){}
};
size_t computeZValue(const string& s, size_t pos, zbox& box) {
  size_t i = 0, n = s.size();
  while( i < n && s[i] == s[pos+i]) {
    i++;
  }
  box.l = pos;
  box.r = i;
  return i;
}
vector<size_t> createZArr(const string& s) {
  auto n = s.size();
  vector<size_t> zArr(n,0);
  zbox currZbox;
  
  zArr[1] = computeZValue(s, 1, currZbox);
  for(size_t i = 2; i < n ; ++i ) {
    if( i > currZbox.r) 
      zArr[i] = computeZValue(s, i, currZbox);
    else {
      auto beta = currZbox.r - i;
      auto correspond = z[i-currZbox.l];
      if ( correspond < beta) {
        z[i] = correspond;
      }
      else {
        z[i] = correspond + currZbox.getLen() - beta;
      }
    }
  }
  return zArr;
}

vector<size_t> findMatch(string target, string pattern) {
  char nc = 0;
  auto concat = target;
  concat += nc; concat += pattern;
  auto zArr = createZArr( concat);
  auto rev = vector<size_t>();
  for(size_t i = 0 ; i < zArr.size() ; ++i ) {
    if(zArr[i] == pattern.size())
      rev.push_back(i);
  }
  return rev;
}
```
### Pros and Cons
Pros:
1. Implementation is easy.
2. Concept is easy.
Cons:
1. Not easy to adapt to multiple pattern-matching problems: Given a set of words that we want to search for. 
2. Real-time string matching: when the input is a stream. 


### References 
A great video from UC-Davis on youtube: https://www.youtube.com/watch?v=NVJ_ELSbbew

## KMP-Algorithm
## Aho-Corasick Algorithm
