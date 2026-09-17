#include<bits/stdc++.h>
using namespace std;
#define int long long
signed main()
{
	ios::sync_with_stdio(0);
	cin.tie(0);
	//一共有13条通道分别为AB(1),AC(2),AD(3),BA(4),BC(5),BD(6),DA(7),DB(8),DC(9),EA(10),EB(11),EC(12),ED(13),用1 2 3 ... 12 13表示
	vector<string>st(15);
	st[1]="AB";st[2]="AC";st[3]="AD";st[4]="BA";st[5]="BC";
	st[6]="BD";st[7]="DA";st[8]="DB";st[9]="DC";st[10]="EA";
	st[11]="EB";st[12]="EC";st[13]="ED";
	//已知AC和BD,DB,EB,冲突，AD和EB,EC冲突,BD和AC,EC冲突,DB和AC,EC冲突，DA和EB，EC冲突,EB和AC,AD,DA冲突，EC和AD,DA,BD,DB冲突,以此构建map;
	map<int,set<int>>mp;
	mp[2].insert(6);mp[2].insert(8);mp[2].insert(11);mp[3].insert(11);mp[3].insert(12);
	mp[6].insert(2);mp[6].insert(12);mp[8].insert(2);mp[8].insert(12);mp[7].insert(11);
	mp[7].insert(12);mp[11].insert(2);mp[11].insert(3);mp[11].insert(7);mp[12].insert(3);
	mp[12].insert(7);mp[12].insert(6);mp[12].insert(8);
	
	vector<int>a(15,0);//用来判断路是否已分配;
	int use=0;//标记已分配的数量; 
	//用一个set来维护，通过贪心来判断哪些道路可以同时走； 
	set<int>se;
	while(use!=13)
	{
		se.clear();
		for(int i=1;i<=13;i++)
		{
			if(a[i]==1)continue;
			//判断能否同时通行;
			int biao=1;
			for(int p:mp[i])
			{
				if(se.count(p))
				{
					biao=0;
					break;
				}
			}
			if(biao==1)
			{
				se.insert(i);
				a[i]=1;
				use++; 
			}
		}
		//可以同时通行的输出 
		for(int s:se)
		{
			cout << st[s] << " ";
		}
		cout << "可以同时通行\n";
	}
	return 0;
} 
