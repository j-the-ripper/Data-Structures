
# Table of Contents

1.  [Stack DS](#orgd9408ac)
    1.  [Nearest greater to left (unique elements)](#org5c00d2f)
    2.  [Nearest greater to right (unique elements)](#org102aef2)
    3.  [Nearest smaller to right (unique elements)](#orgdb88c70)
    4.  [Nearest smaller to right (unique elements)](#org6381bb5)
    5.  [Reverse string using stack](#org06de31e)



<a id="orgd9408ac"></a>

# Stack DS


<a id="org5c00d2f"></a>

## Nearest greater to left (unique elements)

    
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


<a id="org102aef2"></a>

## Nearest greater to right (unique elements)

    
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


<a id="orgdb88c70"></a>

## Nearest smaller to right (unique elements)

    
    vector<int> arr = {1,5,3,2,4};
    stack<int> s;
    unordered_map<int,int> hash;
    vector<int> res;
    
    for(auto &x : arr){
        while(s.size() && s.top() > x){
            hash[s.top()] = x;
            s.pop();
        }
        s.push(x);
    }
    for(auto &x : arr) res.push_back( hash.find(x) != hash.end() ? hash[x] : -1);
    for(auto &x : res) cout << x << " ";


<a id="org6381bb5"></a>

## Nearest smaller to right (unique elements)

    
    vector<int> arr = {1,5,3,2,4};
    stack<int> s;
    unordered_map<int,int> hash;
    vector<int> res;
    
    for(auto &x : arr){
        while(s.size() && s.top() > x){
            s.pop();
        }
        if(s.size() && s.top() < x) hash[x] = s.top();
        s.push(x);
    }
    for(auto &x : arr) res.push_back( hash.find(x) != hash.end() ? hash[x] : -1);
    for(auto &x : res) cout << x << " ";


<a id="org06de31e"></a>

## Reverse string using stack

    
    string st =  "abcdefgh";
    stack<char>s;
    string res = "";
    for(int i = 0; i < st.length(); i++) s.push(st[i]);
    while(!s.empty()){
        res += s.top();
        s.pop();
    }
    cout << res;

