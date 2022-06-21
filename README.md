# Tree
LeftView of Tree 
```
void solve(Node *root,int level, vector<int> &v) {
    if(root==NULL) {
        return;
    }
    if(level == v.size()) {
        v.push_back(root->data);
    }
    solve(root->left, level+1, v);
    solve(root->right, level+1, v);
}

vector<int> leftView(Node *root)
{
    vector<int> v;
    solve(root, 0, v);
    return v;
}
```
