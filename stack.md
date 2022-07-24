
# Table of Contents

1.  [Stack DS](#orgb863f80)
    1.  [Nearest greater to left](#org6b70f5c)
    2.  [Nearest greater to right](#org23fd375)
    3.  [Nearest smaller to right](#org87e2009)
    4.  [Nearest smaller to left](#orgdbf248a)
    5.  [Reverse string using stack](#orge58e803)
    6.  [Postfix expression evaluation](#orgbd2bc39)
    7.  [Infix to postfix](#orgb25f3e2)



<a id="orgb863f80"></a>

# Stack DS


<a id="org6b70f5c"></a>

## Nearest greater to left

    
    vector<int> arr = {1,3,2,4};
    stack<int>s;
    vector<int> res(arr.size(),-1);
    for(int i = 0; i < arr.size(); i++){
        while(s.size() && arr[s.top()] <= arr[i]){
            s.pop();
        }
        if(s.size()) res[i] = arr[s.top()];
        s.push(i);
    }
    for(auto &x : res) cout << x << " ";


<a id="org23fd375"></a>

## Nearest greater to right

    
    vector<int> arr = {6,2,5,4,5,1,6};
    stack<int>s;
    vector<int> res(arr.size(),-1);
    for(int i = 0; i < arr.size(); i++){
        while(s.size() && arr[s.top()] < arr[i]){
            res[s.top()] = arr[i];
            s.pop();
        }
        s.push(i);
    }
    for(auto &x : res) cout << x << " ";


<a id="org87e2009"></a>

## Nearest smaller to right

    
    vector<int> arr = {1,3,2,4};
    stack<int>s;
    vector<int> res(arr.size(),-1);
    for(int i = 0; i < arr.size(); i++){
        while(s.size() && arr[s.top()] > arr[i]){
            res[s.top()] = arr[i];
            s.pop();
        }
        s.push(i);
    }
    for(auto &x : res) cout << x << " ";


<a id="orgdbf248a"></a>

## Nearest smaller to left

    
    vector<int> arr = {1,3,2,4};
    stack<int>s;
    vector<int> res(arr.size(),-1);
    for(int i = 0; i < arr.size(); i++){
        while(s.size() && arr[s.top()] >= arr[i]){
            s.pop();
        }
        if(s.size()) res[i] = arr[s.top()];
        s.push(i);
    }
    for(auto &x : res) cout << x << " ";


<a id="orge58e803"></a>

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


<a id="orgbd2bc39"></a>

## Postfix expression evaluation

    
    string st = "23*54*+9-";
    stack<int>s;
    int res = 0;
    for(int i = 0; i < st.length(); i++){
        if(st[i] == '*' || st[i] == '+' || st[i] == '/' || st[i] == '-'){
            int num1 = s.top();
            s.pop();
            int num2 = s.top();
            s.pop();
            if(st[i] == '+') res = num1 + num2;
            else if(st[i] == '*') res = num1 * num2;
            else if(st[i] == '-') res = num2 - num1;
            else if(st[i] == '/') res = num2 / num1;
            s.push(res);
        }else{
            s.push(st[i] - '0');
        }
    }
    cout << res;


<a id="orgb25f3e2"></a>

## Infix to postfix

    
    bool isOperand(char& A){
       if((A >= 97 && A <= 122) || (A >= 65 && A <= 90)) return true;
       return false;
    }
    
    bool isOpening(char& A){
       if(A == '[' || A == '(' || A == '{') return true;
       return false;
    }
    
    
    bool isClosing(char& A){
       if(A == ']' || A == ')' || A == '}') return true;
       return false;
    }
    
    void solve(){
        string st;
        cin >> st;
        stack<char>s;
        string operators = "-+*/^";
        unordered_map<char,int> Precedence;
        string res = "";
        for(unsigned int i = 0; i < operators.length(); i++) Precedence[operators[i]] = i + 1;
        for(unsigned int i = 0; i < st.length(); i++){
            if(isOperand(st[i])){
                res += st[i];
            }else if(st[i] == '-' || st[i] == '+' || st[i] == '*' || st[i] == '/' || st[i] == '^' ){
                while(s.size() && Precedence[s.top()] > Precedence[st[i]] && !isOpening(st[i])){
                    res += s.top();
                    s.pop();
                }
                s.push(st[i]);
            }else if(isOpening(st[i])){
                s.push(st[i]);
            }else{
                while(s.size() && !isOpening(s.top())){
                    res += s.top();
                    s.pop();
                }
                if(s.size()) s.pop();
            }
        }
        while(s.size() && !isOpening(s.top())){
            res += s.top();
            s.pop();
        }
        cout << res << endl;
    }

