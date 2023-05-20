# Strongly-Connected-Components-Kosaraju-s-Algo-




stack<int>st;
	int ans=0;
	void dfs(int ver, vector<vector<int>>&adj, vector<bool>&vis)
	{
	    
	    for(auto it:adj[ver])
	    {
	        if(!vis[it])
	        {
	            vis[it]=true;
	            dfs(it,adj,vis);
	        }
	    }
	    st.push(ver);
	}
	
	void dfs2(int ver, vector<int>adj2[], vector<bool>&vis)
	{
	    for(auto it:adj2[ver])
	    {
	        if(!vis[it])
	        {
	            vis[it]=true;
	            dfs2(it,adj2,vis);
	        }
	    }
	    
	}
	
	
	
	
	
    int kosaraju(int V, vector<vector<int>>& adj)
    {
        
        //step-1.get node in stack (toposort)
        vector<bool>vis(V,false);
        for(int i=0;i<V;i++)
        {
            if(!vis[i])
            {
                vis[i]=true;
                dfs(i,adj,vis);
            }
        }
        
        
      //step -2 transpose graph
        vector<int>adj2[V];
        
        for(int i=0;i<adj.size();i++)
        {
            for(auto it:adj[i])
            {
                adj2[it].push_back(i);
            }
        }
        
        vector<bool>vis2(V,false);
        
        
        //step -3. doing dfs of transpose graph according to stack node 
        while(!st.empty())
        {
            int node = st.top();
            st.pop();
            if(!vis2[node])
            {
                ans++;
                dfs2(node,adj2,vis2);
            }
        }
        
        return ans;
   }
