# Zigzag String | Interviewbit

Created: June 15, 2022 5:46 PM
Tags: String
URL: https://www.interviewbit.com/problems/zigzag-string/

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P.......A........H.......N
..A..P....L....S....I...I....G
....Y.........I........R

```

And then read line by line: `PAHNAPLSIIGYIR`
 Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR"

```

- *Example 2 : ** ABCD, 2 can be written as

```
A....C
...B....D

```

and hence the answer would be `ACBD`.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
string Solution::convert(string s, int b)
{
    if(b==1)
    return s;
    vector<vector<char> > v(b);
    int i,l=s.length(),f=0,k=0;
    for(i=0;i<l;i++)
    {
        if(f==0)
        {
            v[k].push_back(s[i]);
            k++;
            if(k==b)
            {
                k-=2;
                f=1;
            }
        }
        else
        {
            v[k].push_back(s[i]);
            k--;
            if(k==-1)
            {
                k+=2;
                f=0;
            }
        }
    }
    string w="";
    for(i=0;i<v.size();i++)
    {
        for(int j=0;j<v[i].size();j++)
        {
            w+=v[i][j];
        }
    }
    return w;
}
```