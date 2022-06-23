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
