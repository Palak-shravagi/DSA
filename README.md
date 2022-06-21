# Tree
LeftView of Tree 
```
class Solution {
public:

    void view(TreeNode* root,vector<int>&v,int level){
        if(!root)return;
        if(level ==  v.size())v.push_back(root->val);
        view(root->left,v,level+1);
        view(root->right,v,level+1);
    }
    
    vector<int> rightSideView(TreeNode* root) {
       vector<int>v;
        view(root,v,0);
        return v;
    }
};

```

RightView of Tree
```
class Solution {
public:

    void view(TreeNode* root,vector<int>&v,int level){
        if(!root)return;
        if(level ==  v.size())v.push_back(root->val);
        view(root->right,v,level+1);
        view(root->left,v,level+1);
    }
    
    vector<int> rightSideView(TreeNode* root) {
       vector<int>v;
        view(root,v,0);
        return v;
    }
};

```

