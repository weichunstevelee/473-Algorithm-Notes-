# String Matching
Common technique is to find "the suffix of a substring you are looking at that is also a prefix of the whole string!"

## Z-Algorithm

### Z Value 
Given a string S, $z_i[s]$ is the length of the longest substring in S, starting at position i that matches a prefix of S. 
Example:
Given a string __aabcaabxaaz__

position i | Z[i] |
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
## KMP-Algorithm
## Aho-Corasick Algorithm
