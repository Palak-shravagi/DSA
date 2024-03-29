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

Level Order Traversal of Tree
```
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {    
     vector<vector<int>>v;
        if(root == NULL)return v;
        queue<TreeNode*>q;
        q.push(root);
        while(!q.empty()){
            int s = q.size();
            vector<int>vt;
            for(int i=0;i<s;i++){
                TreeNode *node =  q.front();
                q.pop();
                if(node->left != NULL)q.push(node->left);
                if(node->right != NULL)q.push(node->right);
                vt.push_back(node->val);
            }
            v.push_back(vt);
        }
        return v;
    }
    
};

```

Spiral level order traversal of Tree
```

class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>>v;
        if(root == NULL)return v;
        queue<TreeNode*>q;
        q.push(root);
         int flag = 0;
        while(! q.empty()){
            int size = q.size();
            vector<int>temp_v;
            for(int i=0;i<size;i++){   
                root = q.front();
                q.pop();
                if(root->left != NULL)q.push(root->left);
                if(root->right != NULL)q.push(root->right);
                temp_v.push_back(root->val);
            }
            if(flag == 1){
                reverse(temp_v.begin(),temp_v.end());
                v.push_back(temp_v);
            }else{
                v.push_back(temp_v);
            }
            if(flag == 0)
                flag = 1;
            else
                flag = 0;
        }
        return v;
    }
};
```

Height of Tree
```
class Solution{
    public:
    //Function to find the height of a binary tree.
    int height(struct Node* node){
     if(!node)return NULL;
     int left =  height(node->left);
     int right = height(node->right);
     return 1 + max(left,right);
        
    }
};
```

Diameter of Tree
```
class Solution {
public:
    int call_diameter(TreeNode *node ,int& diameter){
        if(!node)return 0;
        
        int lh = call_diameter(node->left,diameter);
        int rh = call_diameter(node->right,diameter);
        diameter = max(diameter,lh+rh);
        return 1 + max(lh,rh);
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        call_diameter(root,diameter);
        return diameter;
    }
};
```

Balanced Binary Tree
```
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        return diffOfTree(root) != -1;
    }
   int diffOfTree(TreeNode* root){
       if(!root)return 0;
       int left =  diffOfTree(root->left);
       int right =  diffOfTree(root->right);
       if(left == -1 || right == -1)return -1;
       if(abs(left-right)>1)return -1;
       return 1+max(left,right);
   }
};
```

Maximun Path Sum of Tree
```
class Solution {
public:
    
    int maxpath (TreeNode *root,int &maxi){
        if(!root)return 0;
        int left =max(0,maxpath(root->left,maxi));
        int right = max(0,maxpath(root->right,maxi));
        maxi = max(maxi,root->val+left+right);
        return root->val + max(left,right);
    }
    
    int maxPathSum(TreeNode* root) {
         int maxi = INT_MIN;
          maxpath(root,maxi);
        return maxi;
    }
};
```

LCA of tree
```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL || root == p || root == q)return root;
        
        TreeNode* left =  lowestCommonAncestor(root->left,p,q);
        TreeNode *right = lowestCommonAncestor(root->right,p,q);
        if(left == NULL)return right;
        else if(right == NULL)return left;
        else return root;
    }
};
```

Same Tree
```
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(!p) return !q;
        if(!q) return !p;
        return (p->val == q->val) && isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
    }
};
```

Symmetric Tree
```
class Solution {
public:
    bool f(TreeNode *root1, TreeNode* root2) {
        if(!root1) return !root2;
        if(!root2) return !root1;
        return (root1->val == root2->val) && f(root1->left, root2->right) && f(root1->right, root2->left);
    }
    bool isSymmetric(TreeNode* root) {
        if(!root) return true;
        return f(root->left, root->right);
    }
};
```

Flatten Tree into Binary Tree
```
class Solution {
public:
    TreeNode *prev = NULL;
    void flatten(TreeNode* root) {
        if(root == NULL)return;
        flatten(root->right);
        flatten(root->left);
        root->right = prev;
        root->left =  NULL;  
        prev =  root;
    }
};
```

Populating next right pointer
```
class Solution {
public:
    Node* connect(Node* root) {
         if(root == NULL)return NULL;
       Node *rt =  root;
        while(rt != NULL && rt->left != NULL ){
            Node *temp =  rt;
            while(1){
                temp->left->next =  temp->right;
                if(temp->next == NULL)break;
                temp->right->next =  temp->next->left;
                temp = temp->next;
            }
             rt = rt->left;
        }
        return root;
    }
};
```
