---
layout: post
title:  BFS_Algorithm
category: Algorithm
description: BFS_Algorithm 공부
---

- BFS Algorithm 정의
- BFS Algorithm 설명
- BFS Algorithm Code

## BFS Algorithm 정의
 
 BFS 너비우선 탐색이란 루트노드( 혹은 다른 임의의 노드)에서 출발하여 인접한 노드들은 먼저 탐색하고 나아가는 방식이다. 즉, DFS와는 다르게 깊지 않고 넓게 탐색하는 것을 말한다. 주로 사용하는 곳은 두 노드사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다.
 BFS는 DFS와 다르게 queue라는 자료구조를 이용하여 구현하는데 이때문에 재귀적으로는 작동하지 않으며 반드시 queue의 자료구조 형태를 이용하여 구현 해야한다. 여기서 queue는 선입선출의 원칙으로 탐색하는 자료구조를 뜻한다.
## BFS Algorithm 설명

 ![]({{http://22ema.github.io}}/assets/img/graph_dfs.JPG)
 
  - 저번에 dfs를 설명하기위해 사용했던 그래프를 그대로 사용해서 구현 해보겠습니다.


 1. 1의 노드에서 시작을 하면 queue에 1을 넣고 방문하였다는 표시를 해줍니다.1을 pop해줍니다.
 2. 1의 노드중 갈수 있는 곳은 3과 2 노드 두개 이빈다. 이때 2를 먼저 queue에 넣어주고 3도 같이 뒤따라서 넣어줍니다.
 3. queue에서 맨앞의 수인 2를 pop해주고 2가 갈 수 있는 경로인 4와 5를 push해줍니다.
 4. 그리고 다음 맨앞의 수인 3을 pop 해주고 3이 갈 수 있는 수인 1과 4를 넣습니다. 1은 이미 방문했기때문에 넣지 않습니다.
 5. 그리고 맨앞의 수인 4를 뺍니다. 4가 갈 수 있는 수는 이미 방문한 1,2,3, 밖에 없기 때문에 넘어가고
 6. 5가 다음에 선정됩니다. 하지만 5도 역시 이미 2를 방문 했기 때문에 끝이납니다. 그뒤의 숫자인 4도 이미 방문했기때문에 넘어가고 
 7. queue가 비어지게 되며 끝나게 됩니다. 

## BFS Algorithm 코드
 
 BFS는 DFS와는 다르게 방법이 queue를 쓰는 것 밖에 없습니다. 그래서 그냥 queue를 이용해서 bfs를 구현하는 것과 그것을 활용해 최단거리를 구하는 코드 두개를 소개 하겠습니다.
 - 1 bfs 구현
 

         	/*한윤성 http://22ema.github.io
        	queue 에대한 공부*/

        #include <iostream>
        #include <queue>
        #include <vector>
        using namespace std;

        int number = 9;									// 노드의 개수
        int visit[9];									// 방문 했는지 확인하는 배열
        vector<int> a[10];								// 백터를 만들어 경로를 갔는지 확인함

        void bfs(int start) {
            queue<int> q;
            q.push(start);
            visit[start] = true;

            while (!q.empty()) {
                                                        // 큐에 값이 있을 경우 계속 반복 실행
                                                        // 큐에 값이 있다. => 아직 방문하지 않은 노드가 존재 한다.
                int x = q.front();						// queue의 front를 x에 저장한다.
                q.pop();								// 젤 앞에 있는것을 pop 시킨다.
                printf("%d", x);						// x의 값을 출력한다.
                for (int i = 0; i < a[x].size(); i++) {	// a[x](vector)의 크기 만큼 반복한다.
                    int y = a[x][i];					//해당 벡터의 i위치를 변수 y에 넣는다.
                    if (!visit[y]) {					//방문한적없으면
                        q.push(y);						//q에 y를 push한다.
                        visit[y] = true;				// 방문했다고 표시한다.
                    }
                }
            }
        }
        int main() {
            for (int i = 0; i < number; i++) {			// 방문했다는 증거
                int N, M;
                cin >> N >> M;
                a[N].push_back(M);
                a[M].push_back(N);

            }
            bfs(1);
            return 0;
        }

 queue를 이용하여 bfs알고리즘을 구현하였다
 - 2 bfs를 이용해서 최단거리 찾기.


     		/*bfs 최단거리를 구하는 문제
        	미로찾기 문제임 백준 2178번문제
        22ema.github.io*/

        #include<iostream>
        #include<queue>

        #define MAX 101
        using namespace std;
        int N;
        int M;
        int maze[MAX][MAX];
        int plus_minus[4][2] = { {1,0},{0,1},{-1,0},{0,-1} };
        queue<pair<int, int>> q;
        void bfs() {
            q.push(pair<int, int>(0, 0));
            while (!q.empty()) {
                pair<int, int>current = q.front();
                q.pop();
                for (int i = 0; i < 4; i++) {
                    int nx = current.first + plus_minus[i][0];
                    int ny = current.second + plus_minus[i][1];
                    if (nx >= 0 && nx < N && ny >=0 && ny < M && maze[nx][ny] == 1) {//이부분이 가장중요
                        q.push(pair<int,int>(nx, ny));
                        maze[nx][ny] = maze[current.first][current.second] + 1;

                    }
                }
            }
            cout << maze[N-1][M-1] << endl;
        }

        int main() {
            cin >> N >> M;
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < M; j++) {
                    scanf_s("%1d", &maze[i][j]);
                }
            }
            bfs();

		}
        
 bfs 에서 자신이 갈 수 있고 가보지 않은 경로들을 파악하여 자기노드의 값에 1을 더해 그 경로에 넣어주어 그 경로의 최단거리를 구하는 형식입니다. 이때 방문정보는 필요가 없다는 것을 알고 있는것이 좋겠습니다.

 설명이 조금 미흡하긴 했지만 도움이 되길 바랍니다.