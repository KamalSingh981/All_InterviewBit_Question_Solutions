# Justified Text | Interviewbit

Created: August 10, 2022 3:36 AM
Tags: String
URL: https://www.interviewbit.com/problems/justified-text/

**Problem Description**

Given an array of words and a length **L**, format the text such that each line has exactly **L** characters and is fully (left and right) justified. You should pack your words in a greedy approach; that is, pack as many words as you can in each line.

Pad extra spaces ' ' when necessary so that each line has exactly **L** characters. Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right. For the last line of text, it should be left justified and no extra space is inserted between words.

Your program should return a list of strings, where each string represents a single line.

**Example:**

```
words: ["This", "is", "an", "example", "of", "text", "justification."]

L: 16.Return the formatted lines as:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]

```

Note: Each word is guaranteed not to exceed L in length.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
string leftJustifiedString(int i, int j, vector<string> &A, int B){
    string ans = "";
    for(int ind = i; ind<j; ind++){
        ans += A[ind];
        if(ind != j-1){
            ans += " ";
        }
    }
    
    while(ans.size() < B){
        ans+=" ";
    }

    return ans;
}

string middleJustifiedString(int i, int j, vector<string> &A, int B, int lineLength){
    int remainingSpace = B - lineLength;
    int NumberOfWords = j - i;
    int distributedSpace = remainingSpace/(NumberOfWords-1); // spaces needed will be always 
    int extraSpace = remainingSpace%(NumberOfWords-1); // less the 1 by words
    
    string ans = "";
    for(int ind = i; ind<j - 1; ind++){
        ans += A[ind];
        int addSpace = distributedSpace +  ((extraSpace-- > 0)?1:0);;
        for(int k = 0; k<addSpace; k++){
            ans += " ";
        }
    }
    
    ans += A[j - 1];
    
    return ans;

}

vector<string> Solution::fullJustify(vector<string> &A, int B) {
    
    vector<string> ans; // stores the answer
    
    int n = A.size();
    
    int i = 0; 

    while(i < n){
        int j = i + 1;
        int lineLength = A[i].size();
        while(j<n and (lineLength + A[j].length() + j - i <= B)){
            lineLength  += A[j].size();
            j++;
        }
        
        // if the line has only one word or the last line
        // then we need to justified it to the right left side
        if(j -i == 1 or j == n){
            ans.push_back(leftJustifiedString(i, j, A, B));
        }
        else{
            ans.push_back(middleJustifiedString(i, j, A, B, lineLength));
        }
        
        i = j;   
    }  
    return ans;
}
```