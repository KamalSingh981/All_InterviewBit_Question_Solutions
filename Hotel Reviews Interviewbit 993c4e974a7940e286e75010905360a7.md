# Hotel Reviews | Interviewbit

Created: July 23, 2022 10:43 PM
Tags: Hashing, Trie
URL: https://www.interviewbit.com/problems/hotel-reviews/

**Problem Description**

Given a set of reviews provided by the customers for different hotels and a string containing **Good Words**, you need to sort the reviews in descending order according to their **Goodness Value** (Higher goodness value first). We define the **Goodness Value** of a string as the number of **Good Words** in that string.

**NOTE:** Sorting should be stable. If review **i** and review **j** have the same **Goodness Value** then their original order would be preserved.

`You are expected to use Trie in an Interview for such problems`

**Problem Constraints**

1. 1 <= No.of reviews <= 200
2. 1 <= No. of words in a review <= 1000
3. 1 <= Length of an individual review <= 10,000
4. 1 <= Number of Good Words <= 10,000
5. 1 <= Length of an individual Good Word <= 4
6. All the alphabets are lower case (a - z)

**Input Format**

First argument is a string A containing "Good Words" separated by "*" character*

*Second argument is a vector B of strings containing Hotel Reviews. Review strings are also separated by "*" character.

**Output Format**

Return a vector of integers which contain the original indexes of the reviews in the sorted order of reviews.

**Example Input**

Input 1:

```
 A = "coolicewifi"
 B = ["wateriscool", "coldicedrink", "coolwifispeed"]
```

**Example Output**

Output 1:

```
 [2, 0, 1]
```

**Example Explanation**

Explanation 1:

```
 sorted reviews are ["coolwifispeed", "wateriscool", "coldicedrink"]
```

HashMap Solution 

```cpp
bool sortbysec(const pair<int,int> &a,
              const pair<int,int> &b)
{
    if(a.first == b.first){
        return a.second < b.second;
    }
    return (a.first > b.first);
}
map<string, bool> words(string str){
    map<string , bool > m;
    string word = "";
    for (auto x : str) 
    {
        if (x == '_')
        {
            m[word] = true;
            word = "";
        }
        else {
            word = word + x;
        }
    }
    m[word] = true;
    return m;
}

vector<int> Solution::solve(string A, vector<string> &B) {
    vector<pair<int, int>> a;
    map<string, bool> m = words(A);
    for(int i = 0; i<B.size(); i++){
        int q = 0;
        string word = "";
        for (auto x : B[i]) 
        {
            if (x == '_')
            {
                if(m[word]){
                    q++;
                }
                word = "";
            }
            else {
                word = word + x;
            }
        }
        if(m[word]){
            q++;
        }
        a.push_back({q, i});
    }
    sort(a.begin(), a.end(), sortbysec);
    vector<int> ans;
    for(auto i: a){
        ans.push_back(i.second);
    }    
    
    return ans;
}
```

Using Trie

```cpp
#define F first
#define S second

bool cmp(const pair<int, int>& a, const pair<int, int>& b){
    if(a.F == b.F) return a.S < b.S;
	return a.F > b.F;	
}

//Trie node
struct node{
	bool exist;
	node* arr[26];
	node(bool bul=false){
		exist = bul;
		for(int i=0; i<26; i++)	arr[i] = NULL;
	}
};

void add(string s,node* trie){
    //add a node to the trie
	int n = s.size();
	for(int i=0; i<n; i++){
		if(trie->arr[s[i]-'a']==NULL)	trie->arr[s[i]-'a'] = new node();
		trie = trie->arr[s[i]-'a'];
	}
	trie->exist=true;
	return;
}

bool search(string s,node* trie){
    //search for a node in the trie
	for(int i=0; i<s.size(); i++){
		if(trie->arr[s[i]-'a']==NULL)	return false;
		trie = trie->arr[s[i]-'a'];
	}
	return trie->exist;
}

void convert(string &str){
    //Convert _ to spaces
	for(int i=0; i<str.size(); i++)	if(str[i]=='_')	str[i]=' ';
	return;
}

vector<int> Solution::solve(string good, vector<string>& review){
	convert(good);
	node* trie = new node();
	string word;
	stringstream ss;
	ss<<good;
	while(ss>>word)	add(word,trie);
	int n = review.size();
	int k;
	vector<pair<int,int> > rating(n);
	for(int i=0; i<n; i++){
		convert(review[i]);
		ss.clear();
		ss<<review[i];
		k=0;
		while(ss>>word)	if(search(word,trie))	k++;
		rating[i].first = k;	rating[i].second = i;
	}
	sort(rating.begin(),rating.end(),cmp);
	vector<int> ans(n);
	for(int i=0; i<n; i++)	ans[i] = rating[i].second;
	return ans;
}
```