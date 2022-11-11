# lintcode 444 graph valid tree II
Use union find to check whether there is a circle, also the condition to construct a tree is non-circle, one connected graph
```cpp
class Solution {
private:
    bool flag=true;
    int cnt=0;
    int group=0;
    unordered_map<int,int> fa;
    int find(int x){
        while(x!=fa[x]) x=fa[x]=fa[fa[x]];
        return x;
    }
    bool merge(int x,int y){
        int xx=find(x),yy=find(y);
        if (xx!=yy) {fa[yy]=xx;group--;return true;}
        return false;
    }
public:
    /**
     * @param a: the node a
     * @param b: the node b
     * @return: nothing
     */
    void addEdge(int a, int b) {
        auto find_it=fa.find(a);
        if (find_it==fa.end()) fa[a]=a,++group;
        find_it=fa.find(b);
        if (find_it==fa.end()) fa[b]=b,++group;
        if (!merge(a,b)) flag=false;
        //if (!flag) cout<<" "<< a <<" "<< b<< " "<<flag<<endl;
    }

    /**
     * @return: check whether these edges make up a valid tree
     */
    bool isValidTree() {
        
        return flag&&(group==1);
    }
};
```
