# Default code
```py
class Fenwick:
  def __init__(self,n):
    self.sz=n 
    self.dp=[0]*(n+1)
  
  def update(self,ix,v):
    while ix<=self.sz:
      self.dp[ix]=max(self.dp[ix],v)
      ix+=ix&-ix
  
  def query(self,ix):
    mx=0
    while ix>0:
      mx=max(res,self.dp[ix])
      ix-=ix&-ix 
    return mx
```

```cpp
//---------------------------------------------------------------
//               Jai Gurudev Naam Prabhu Ka
//---------------------------------------------------------------

#include <bits/stdc++.h>
using namespace std;

//---------------------------------------------------------------
// Code reference: https://github.com/myJaiGurudev/CP/blob/main/README.md
//---------------------------------------------------------------

//---------------------------------------------------------------
//                     Macros begin
//---------------------------------------------------------------

//---------------------------------------------------------------
//                     Speed + Optimization
//---------------------------------------------------------------

#pragma GCC optimize("O3,unroll-loops")
#pragma GCC target("avx2,bmi,bmi2,lzcnt,popcnt")
#define fast() ios::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr)

//---------------------------------------------------------------

#define fori(i,b,n) for(int i=b;i<n;i++)
#define forv(i,ar) for(auto i:ar)
#define fo(i,n) for(int i=0;i<n;i++) 
#define nl cout<<"\n";
#define ll long long
#define um unordered_map
#define upto(n) fixed << setprecision(n)
#define lower(s) transform(s.begin(),s.end(),s.begin(),::tolower)
#define upper(s) transform(s.begin(),s.end(),s.begin(),::toupper)
#define inf INT_MAX
#define sum(v) accumulate((v).begin(),(v).end(),0)
#define pb push_back 
#define eb emplace_back
#define print(...) print_values(__VA_ARGS__)
#define input(...) input_values(__VA_ARGS__)
#define index(v,x) (find((v).begin(),(v).end(),(x))!=(v).end()?distance((v).begin(),find((v).begin(),(v).end(),(x))):-1)
#define rsort(a) sort(a.rbegin(),a.rend())
#define asort(a) sort(a.begin(),a.end())
#define maxv(vec) *max_element(vec.begin(),vec.end())
#define maxa(arr,n) *max_element(arr,arr+n)
#define minv(vec) *min_element(vec.begin(),vec.end())
#define mina(arr,n) *min_element(arr,arr+n)

ll gcd(ll a,ll b) {
    while(b!=0) { ll temp=b; b=a%b; a=temp; }
    return a;
}
void YES(int t) { if(t) cout<<"YES"; else cout<<"NO"; }
void Yes(int t) { if(t) cout<<"Yes"; else cout<<"No"; }
void yes(int t) { if(t) cout<<"yes"; else cout<<"no"; }

//---------------------------------------------------------------

template<typename T> void print_values(const T&t){cout<<t<<" ";}
template<typename T> void print_values(const T arr[],int n){for(int i=0;i<n;++i){cout<<arr[i]<<" ";}}
template<typename T> void print_values(const vector<T>&vec){for(const auto&val:vec){cout<<val<<" ";}}
template<typename T,typename...Args> void print_values(const T&t,const Args&...args){print_values(t);print_values(args...);}
template<typename T> void input_values(T&t){cin>>t;}
template<typename T> void input_values(vector<T>&vec,int n){T val;for(int i=0;i<n;++i){cin>>val;vec.push_back(val);}}
template<typename T,typename...Args> void input_values(T&t,Args&...args){input_values(t);input_values(args...);}

//---------------------------------------------------------------
//                     General Segment Tree
//---------------------------------------------------------------

template<typename T> struct SegmentTree {
    int n;
    vector<T> tree, lazy;
    bool lazy_flag;
    T def;
    function<T(T,T)> func;

    SegmentTree(vector<T> &arr, T d, function<T(T,T)> f, bool lf=false) {
        n = arr.size();
        def = d;
        func = f;
        lazy_flag = lf;
        tree.assign(4*n, def);
        if(lazy_flag) lazy.assign(4*n,0);
        build(0,0,n-1,arr);
    }

    void build(int v,int l,int r, vector<T> &a) {
        if(l==r){ tree[v]=a[l]; return; }
        int m=(l+r)/2;
        build(2*v+1,l,m,a);
        build(2*v+2,m+1,r,a);
        tree[v]=func(tree[2*v+1],tree[2*v+2]);
    }

    void push(int v,int l,int r) {
        if(!lazy_flag || lazy[v]==0) return;
        tree[v]+=lazy[v];
        if(l!=r){ lazy[2*v+1]+=lazy[v]; lazy[2*v+2]+=lazy[v]; }
        lazy[v]=0;
    }

    void update(int v,int l,int r,int ql,int qr,T val){
        push(v,l,r);
        if(qr<l || ql>r) return;
        if(ql<=l && r<=qr){
            if(lazy_flag){ lazy[v]+=val; push(v,l,r); }
            else tree[v]=val;
            return;
        }
        int m=(l+r)/2;
        update(2*v+1,l,m,ql,qr,val);
        update(2*v+2,m+1,r,ql,qr,val);
        tree[v]=func(tree[2*v+1],tree[2*v+2]);
    }

    T query(int v,int l,int r,int ql,int qr){
        push(v,l,r);
        if(qr<l || ql>r) return def;
        if(ql<=l && r<=qr) return tree[v];
        int m=(l+r)/2;
        return func(query(2*v+1,l,m,ql,qr), query(2*v+2,m+1,r,ql,qr));
    }

    void update(int l,int r,T val){ update(0,0,n-1,l,r,val); }
    T query(int l,int r){ return query(0,0,n-1,l,r); }
};

//---------------------------------------------------------------
//                     Macros end
//---------------------------------------------------------------


//---------------------------------------------------------------
//               Goal To Become Legendary Grandmaster
//---------------------------------------------------------------


int main(){
    fast();
    
}
