
# Table of Contents

1.  [Stack DS](#org001241d)
    1.  [Nearest greater to left](#orgb19f824)
    2.  [Nearest greater to right](#org41c84dc)



<a id="org001241d"></a>

# Stack DS


<a id="orgb19f824"></a>

## Nearest greater to left

    
    vector<int> arr = {1,5,3,2,4};
    stack<int> s;
    unordered_map<int,int> hash;
    vector<int> res;
    
    for(auto &x : arr){
        while(s.size() && s.top() < x){
            s.pop();
        }
        if(s.size() && x < s.top()) hash[x] = s.top();
        s.push(x);
    }
    for(auto &x : arr) res.push_back( hash.find(x) != hash.end() ? hash[x] : -1);
    for(auto &x : res) cout << x << " ";


<a id="org41c84dc"></a>

## Nearest greater to right

    
    vector<int> arr = {1,5,3,2,4};
    stack<int> s;
    unordered_map<int,int> hash;
    vector<int> res;
    
    for(auto &x : arr){
        while(s.size() && s.top() < x){
            hash[s.top()] = x;
            s.pop();
        }
        s.push(x);
    }
    for(auto &x : arr) res.push_back( hash.find(x) != hash.end() ? hash[x] : -1);
    for(auto &x : res) cout << x << " ";

