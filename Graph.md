# Graph

## DFS
```
class Solution {
  public:
    void dfs(int node,vector<int>adj[],vector<int>&vis,vector<int>&v){
        v.push_back(node);
        vis[node] =1;
        for(auto it:adj[node]){
            if(!vis[it]){
                dfs(it,adj,vis,v);
            }
        }
    }
    vector<int> dfsOfGraph(int V, vector<int> adj[]) {
        // Code here
       vector<int>v;
       vector<int>vis(V,0);
       dfs(0,adj,vis,v);
       return v;
    }
};
```

## BFS
```
class Solution {
  public:
    vector<int> bfsOfGraph(int V, vector<int> adj[]) {
	vector<int>v;
	vector<int>vis(V,0);
	queue<int>q;
	q.push(0);
	vis[0] =1;
	while(!q.empty()){
	    int node = q.front();
	    q.pop();
	    v.push_back(node);
	    for(auto it:adj[node]){
	        if(!vis[it]){
	            vis[it] = 1;
	            q.push(it);
	        }
	    }
	}
	return v;
	   
    }
};
```
