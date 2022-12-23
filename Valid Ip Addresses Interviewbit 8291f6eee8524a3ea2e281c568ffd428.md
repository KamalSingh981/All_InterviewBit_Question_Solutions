# Valid Ip Addresses | Interviewbit

Created: June 17, 2022 3:07 AM
Tags: String
URL: https://www.interviewbit.com/problems/valid-ip-addresses/

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

A valid IP address must be in the form of A.B.C.D, where A,B,C and D are numbers from 0-255. The numbers cannot be 0 prefixed unless they are 0.

**Example:**

Given “25525511135”,

return [“255.255.11.135”, “255.255.111.35”]. (Make sure the returned strings are sorted in order)

```cpp
bool correct(int i, int j, int k, string &s, string A){
    string p = A.substr(0, i);
    string q = A.substr(i, j -i);
    string r = A.substr(j, k-j);
    string d = A.substr(k, A.size()- k);
    if(p=="" || q=="" || r=="" || d=="") return false;
    if((p[0]=='0' && p.length()>1) || (q[0]=='0' && q.length()>1) ||(r[0]=='0' && r.length()>1) ||(d[0]=='0' && d.length()>1)) return false;
    if(stoi(p)>255 or stoi(q)>255 or stoi(r)>255 or stoi(d)>255) return false;
    s = p + '.' + q + '.' + r + '.' + d;
    return true;
}

vector<string> Solution::restoreIpAddresses(string A) {
    vector<string> ans;
    if(A.size()>12 or A.size()<4)return ans;
    for(int i = 0; i<A.size()-2; i++){
        for(int j =i+1; j<A.size()-1; j++){
            for(int k = j+1; k<A.size(); k++){
                string x;
                if(correct(i,j,k,x,A)) ans.push_back(x);
            }
        }
    }
    return ans;
}
```