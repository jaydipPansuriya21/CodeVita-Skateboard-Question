// Jaydip Pansuriya
#include<bits/stdc++.h>
#define ll long long 
#define ul unsigned long 
#define ull unsigned long long 
#define MOD 1000000007
const int N = 1e5 + 5;

#define p(a,b) pair<a,b>
#define ff first
#define ss second
#define pb push_back

#define for1(i,a,b) for(int i = a;i<b;++i)
#define for2(i,b) for(int i = b;i>=0;--i) 

// it has only veriabe tp always veriable.
#define vec1(tp,sz,ini) vector<tp> v1(sz,ini); 
#define vec2(tp,sz,ini) vector<tp> v2(sz,ini);
#define vec2D(tp,sz,ini)vector<vector<tp>> vD(sz,vector<int>(sz,ini));

#define ci  cin>> 
#define co  cout<< 
#define e   '\n'

#define deb1(x) cout<<#x<<" : "<<x<<endl;
#define deb2(x,y) cout<<#x<<" : "<<x<<" "<<#y<<" : "<<y<<endl;
#define deb3(x,y,z) cout<<#x<<" : "<<x<<"   "<<#y<<" : "<<y<<"  "<<#z<<" : "<<z<<endl;

#define FAST ios_base::sync_with_stdio(false),cin.tie(0),cout.tie(0);
#define READ freopen("input.txt","r",stdin);
#define WRITE freopen("output.txt","w",stdout);
#define RANDOM srand(time(NULL));

using namespace std;
const bool testCase = 0;
map<char, int> mpx, mpy;


struct Que {
	Que(int x, int y, int dist) {
		this->x = x;
		this->y = y;
		this->dist = dist;
	}
	int x, y, dist, la;
};
class cmp {
public:
	bool operator()(Que a, Que b) {
		if (a.la == b.la) {
			return a.dist > b.dist;
		}
		else {
			return a.la < b.la;
		}
	}
};
priority_queue<Que, vector<Que>, cmp> pq;
bool dfsHelper(vector<vector<string>> grid, Que q, int n) {
	if (q.x >= n || q.y >= n) {
		return false;
	}
	if (grid[q.x][q.y] == "F") {
		
		return true;
	}
	if (grid[q.x][q.y] == "D") return false;
	string g = (grid[q.x][q.y]);
	for1(i, 0, g.length()) {
		int x = q.x + mpx[g[i]];
		int y = q.y + mpy[g[i]];
		if (dfsHelper(grid, Que(x, y, 0), n)) {
			return true;
		}
	}
	return false;
}
int minDistance(vector<vector<string>> grid, int r) {

	int ans = 0;
	for1(i, 0, r) {
		if (dfsHelper(grid, Que(0, i, 0), r))ans++, cout <<  1 << " " << i + 1 << e;;
	}
	for1(i, 1, r) {
		if (dfsHelper(grid, Que(i, 0, 0), r))ans++, cout << i+ 1 << " " <<  1 << e;;
	}
	return ans;



}

int main() {

	FAST
	mpx['S'] = 1;
	mpy['S'] = 0;
	mpx['E'] = 0;
	mpy['E'] = 1;
	mpx['N'] = -1;
	mpy['N'] = 0;
	mpx['W'] = 0;
	mpy['W'] = -1;

	ll t = 1;
	if (testCase) {
		cin >> t;
	}
	while (t-- > 0)
	{

		ll r, c;
		cin >> r;
		int temp;
		vector<vector<string>> grid(r, vector<string>(r, ""));
		for1(i, 0, r) {
			int j = 0;
			/*char str[100];
			string st;
			cin >> st;
			for1(k, 0, st.length()) {
				str[k] = st[k];
			}
			str[st.length()] = '\0';


			char *token = strtok(str, ",");*/
			while (j!=r)
			{
				string to;
				cin >> to;
				//printf("%s\n", token);
				grid[i][j] = to;
				j++;
				//token = strtok(NULL, ",");
			}
		}

		cout << minDistance(grid, r) << e;













	}


	return 0;
}




