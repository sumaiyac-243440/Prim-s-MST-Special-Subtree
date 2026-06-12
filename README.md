#include <iostream>
#include <vector>
#include <queue>
using namespace std;

int main() {

    int n, m;
    cin >> n >> m;

    vector<pair<int,int>> adj[n + 1];

    for(int i=0;i<m;i++){
        int u,v,w;
        cin>>u>>v>>w;

        adj[u].push_back({v,w});
        adj[v].push_back({u,w});
    }

    int start;
    cin>>start;

    vector<bool> visited(n+1,false);

    priority_queue<
        pair<int,int>,
        vector<pair<int,int>>,
        greater<pair<int,int>>
    > pq;

    pq.push({0,start});

    long long mstCost=0;

    while(!pq.empty()){

        auto cur=pq.top();
        pq.pop();

        int cost=cur.first;
        int node=cur.second;

        if(visited[node])
            continue;

        visited[node]=true;
        mstCost+=cost;

        for(auto edge:adj[node]){

            int next=edge.first;
            int wt=edge.second;

            if(!visited[next])
                pq.push({wt,next});
        }
    }

    cout<<mstCost<<endl;

    return 0;
}
