---
layout: post
title:  DFS_Algorithm
category: Algorithm
description: DFS_Algorithm 공부
---
- DFS Algorithm 정의

- DFS Algorithm 설명

- DFS Algorithm Code

## DFS Algorithm 정의

 트리나 그래프에서 한루트로 탐색하며 최대한 깊숙히 들어가서 확인한 뒤 다시 돌아가 다른 루트를 탐색하는 방식이다. 이때 stack 자료구조를 사용한다.
 
 재귀함수는 함수가 호출될 때 스택 메모리를 사용하기 때문에 stack의 자료구조를 사용하게 된다. 그래서 많은 사람들이 dfs를 만들때 재귀함수를 사용하여 코딩을 하게된다.
 
## DFS Algorithm 설명
 
먼저 그림을 보면서 설명을 드리겠습니다.
![]({{http://22ema.github.io}}/assets/img/graph_dfs.JPG)
 1. 1의 노드에서 시작을 하면 스택에 1을 넣고 방문했다는 표시를 해줍니다.
 2. 1의 노드 중에 갈수있는 곳은 3과 2 노드 두개입니다. 이때 2를 먼저 방문하기 때문에 2를 스택에 넣고 2를 방문했다고 표시를 합니다.
 3. 2의 노드에서 갈 수 있는 곳은 4와 5노드 입니다. 4를 먼저 방문하니 4를 스택에 넣고 방문 표시를 합니다.
 4. 4는 2와 3을 갈 수 있는데 2는 이미 방문 했다는 표시가 있기 때문에 3을 스택에 넣고 방문 합니다.
 5. 이제 3인데 3은 1과4 둘다 방문 하였기 때문에 방문 할곳 이 없습니다.
 6. 그렇기 때문에 스택에서 차례로 값들을 빼내어 갈 수 있는 노드가 남은 곳을 찾습니다. 4까지 스택에서 빠지고 2에서 5로 갈 수 있습니다. 그래서 5를 방문하고 나머지를 스택에서 다빼내고 끝이나게 됩니다.

## DFS Algorithm 코드

코드는 두가지의 방법이 있습니다. 스택을 이용하여 구현하거나 시스템스택을 이용한 재귀함수의 방법 입니다. 사람들이 간단해서 더많이 사용하는 재귀 함수를 이용하여 한번 구현해 보겠습니다.

	/*백준 11724 연결요소 문제
	22ema.github.io*/
	
	#include<iostream>  
	#include <vector>
	using namespace std;
	const int N_MAX = 1001;
	int N; //노드의 갯수
	int M; //간선의 갯수
	vector<int> path[N_MAX];
	bool is_visited[N_MAX];
	void dfs(int number) { //dfs 함수 구현
		is_visited[number] = true;
		for (int i = 0; i < path[number].size(); i++) {
			int next = path[number][i];

			if (is_visited[next] == false) {
				dfs(next);
			}
		}

	
	}


	int main() {
	
		cin >> N >> M; //입력
		for (int i = 0; i < M; i++) { //입력
			int K, J;
			cin >> K >> J;
			path[K].push_back(J);
			path[J].push_back(K);
		}
		int Count = 0;
		for (int i = 1; i <= N; i++) { 
			if (is_visited[i] == false) { //방문하지 않았으면
				dfs(i);//함수호출
				Count++;
			}
		}
		cout << Count << endl;
		return 0;
	
	}
- 입력값을 노드와 간선수를 주고 연결된 노드를 입력시켜주면 작동하는 프로그램이다.
- 이것을 참고해서 백준 문제를 몇개 풀어보며 공부할 것을 권합니다.

이것으로 bfs대하여 알아 보았는데 다음에는 bfs algorithm에 대해서 알아 보겠습니다.

