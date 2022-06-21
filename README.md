# Tree

## View of Tree


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

BottomView of Tree

```
class Solution {
  public:
    vector <int> bottomView(Node *root) {
        vector<int> ans; 
        if(root == NULL) return ans; 
        map<int,int> mpp; 
        queue<pair<Node*, int>> q; 
        q.push({root, 0}); 
        while(!q.empty()) {
            auto it = q.front(); 
            q.pop(); 
            Node* node = it.first; 
            int line = it.second; 
            mpp[line] = node->data; 
            
            if(node->left != NULL) {
                q.push({node->left, line-1}); 
            }
            if(node->right != NULL) {
                q.push({node->right, line + 1}); 
            }
            
        }
        
        for(auto it : mpp) {
            ans.push_back(it.second); 
        }
        return ans;  
    }
};

```

TopView of Tree
```
class Solution
{
    public:
    //Function to return a list of nodes visible from the top view 
    //from left to right in Binary Tree.
    vector<int> topView(Node *root)
    {
        vector<int> ans; 
        if(root == NULL) return ans; 
        map<int,int> mpp; 
        queue<pair<Node*, int>> q; 
        q.push({root, 0}); 
        while(!q.empty()) {
            auto it = q.front(); 
            q.pop(); 
            Node* node = it.first; 
            int line = it.second; 
            //only diff line from bottom view
            if(mpp.find(line) == mpp.end()) mpp[line] = node->data; 
            
            if(node->left != NULL) {
                q.push({node->left, line-1}); 
            }
            if(node->right != NULL) {
                q.push({node->right, line + 1}); 
            }
            
        }
        
        for(auto it : mpp) {
            ans.push_back(it.second); 
        }
        return ans; 
    }

};
```
