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
##Check cycle in Undirected graph DFS
```

class Solution {

public:
    bool checkForCycle(int node, int parent, vector<int> &vis, vector<int> adj[]) {
        vis[node] = 1; 
        for(auto it: adj[node]) {
            if(!vis[it]) {
                if(checkForCycle(it, node, vis, adj)) 
                    return true; 
            }
            else if(it!=parent) 
                return true; 
        }
        
        return false; 
    }
public:
	bool isCycle(int V, vector<int>adj[]){
	    vector<int> vis(V+1, 0); 
	    for(int i = 0;i<V;i++) {
	        if(!vis[i]) {
	            if(checkForCycle(i, -1, vis, adj)) return true; 
	        }
	    }
	    
	    return false; 
	}
};



```
##Check cyle in undirected graph BFS
```
class Solution {

public:
    bool checkForCycle(int s, int V, vector<int> adj[], vector<int>& visited)
    {
        vector<int> parent(V, -1);
     
        // Create a queue for BFS
        queue<pair<int,int>> q;
     
        visited[s] = true;
        q.push({s, -1});
     
        while (!q.empty()) {
     
            int node = q.front().first;
            int par = q.front().second;
            q.pop();
     
            for (auto it : adj[node]) {
                if (!visited[it]) {
                    visited[it] = true;
                    q.push({it, node});
                }
                else if (par != it)
                    return true;
            }
        }
        return false;
    }
public:
	bool isCycle(int V, vector<int>adj[]){
	    vector<int> vis(V, 0); 
	    for(int i = 0;i<V;i++) {
	        if(!vis[i]) {
	            if(checkForCycle(i, V, adj, vis)) return true; 
	        }
	    }
	    
	    return false; 
	}
};
```
