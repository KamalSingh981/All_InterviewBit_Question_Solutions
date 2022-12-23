# LRU Cache | Interviewbit

Created: July 18, 2022 11:38 PM
Tags: Heap and Maps
URL: https://www.interviewbit.com/problems/lru-cache/

Design and implement a data structure for LRU (Least Recently Used) cache. It should support the following operations: get and set.

1. `get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return `1`.
2. `set(key, value)` - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least recently used item before inserting the new item.

The LRU Cache will be initialized with an integer corresponding to its capacity. Capacity indicates the maximum number of unique keys it can hold at a time.

**Definition of “least recently used”** : An access to an item is defined as a get or a set operation of the item. “Least recently used” item is the one with the oldest access time.

> 
> 
> 
> **NOTE:** If you are using any global variables, make sure to clear them in the constructor.
> 

**Example :**

```
Input :
         capacity = 2
         set(1, 10)
         set(5, 12)
         get(5)        returns 12
         get(1)        returns 10
         get(10)       returns -1
         set(6, 14)    this pushes out key = 5 as LRU is full.
         get(5)        returns -1

```

```cpp
unordered_map<int, int> mp;
deque<int> d;
int  n;
    
LRUCache::LRUCache(int capacity) {
    mp.clear();
    d.clear();
    n = capacity;
}

void update(deque<int> &d, int key){
    int s = d.size();
        while(s--){
            if(d.front()!=key) d.push_back(d.front());
            d.pop_front(); 
        }
}

int LRUCache::get(int key) {
    
    if(mp.count(key) == 0){
        return -1;
    }
    update(d, key);
    d.push_back(key);
    return mp[key];
}

void LRUCache::set(int key, int value) {
    if(mp.count(key)){
        update(d, key);
    }
    else if(mp.size() == n){
        mp.erase(d.front());
        d.pop_front();
        mp.erase(key);
    }
    mp[key] = value;
    d.push_back(key);
}
```

Efficient Solution

```cpp
#include <list>
unordered_map<int, list<pair<int, int>>::iterator> mp;
list<pair<int, int>> d;
int  n;
    
LRUCache::LRUCache(int capacity) {
    mp.clear();
    d.clear();
    n = capacity;
}

int LRUCache::get(int key) {
    
    if(mp.count(key) == 0){
        return -1;
    }
    
    auto it = mp[key];
    int val =it->second;
    d.erase(it);
    d.push_back({key, val});
    it = d.end(); it--;
    mp[key] = it;
    
    return val;
    
}

void LRUCache::set(int key, int value) {
    if(mp.count(key)){
        auto it = mp[key];
        d.erase(it);
    }
    else if(mp.size() == n){
        int k = d.front().first;
        mp.erase(k);
        d.pop_front();
    }
    
    d.push_back({key, value});
    auto it = d.end(); it--;
    mp[key] = it;
}
```