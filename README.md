# Infix-to-postfix
C++
#include<iostream>
#include<stack>

using namespace std;
int precedencecheck(char c){
    if(c=='^'){
        return 3;
    }
    else if(c=='*' && c=='/'){
        return 2;
    }
    else if(c=='+' && c=='-'){
        return 1;
    }
    else 
    return -1;
}
    string infixtopostfix(string s){
        stack<char>st;
        string ans;
        for(int i=0;i<s.length();i++){
           if(s[i]>='a' && s[i]<='z' || s[i]>='A' && s[i]<='Z' ) {
               ans+=s[i];
           }
           else if(s[i]=='('){
               st.push(s[i]);
           }
               else if(s[i]==')'){
                   while(st.top()!='(' && !st.empty()){
                       ans+=st.top();
                       st.pop();
                   }
                   if(!st.empty()){
                       st.pop();
                   }
               }
               else{
                   while(!st.empty() && precedencecheck(st.top())> precedencecheck(s[i])){
                           ans += st.top();
                           st.pop();
                       }
                   st.push(s[i]);
               }
           }
           while(!st.empty()){
               ans += st.top();
               st.pop();
           }
           return ans;
    }
    


 int main(){
     cout << infixtopostfix("asd-sd*(a-b-c)") << endl;
     return 0;
 }
