# MST(Minimum Spanning Tree)

## **Spanning Tree란?**
`그래프에서 일부 간선을 선택해서 만든 트리`
- 그래프 내의 모든 정점을 포함하는 트리
- 그래프의 일부 간선을 이용해 만든 트리로서 항상 그래프의 부분집합이 된다.
- 하나의 그래프에는 여러 신장트리를 가질 수 있다.
- 사이클 존재 X

## **MST란?**
Spanning Tree의 한 종류로 사용되는 **간선들의 가중치 합이 최소인 트리**

## **MST 특징**
- 간선의 가중치의 합이 최소여야 함
- n개의 정점을 가지는 그래프에 대해 반드시 n-1개의 간선만을 사용
- 사이클 포함 X


## **Kruskal 알고리즘**
- 최소 비용 신장 트리를 찾는 알고리즘
- 가장 적은 비용으로 모든 노드를 연결하기 위해 사용하는 알고리즘
- 간선의 가중치의 합이 최솟값이 되도록 하는 알고리즘

### **크루스칼 알고리즘 동작 원리**

![image](https://user-images.githubusercontent.com/63101648/131241542-017b7332-2538-4752-9123-90af6dc9c358.png)

- 모든 간선들의 가중치를 오름차순으로 정리
- 가중치가 가장 작은 간선 선택
- 위에서 선택한 간선이 연결하려는 2개의 노드가 서로 연결되지 않은 상태라면 2개의 노드를 서로 연결



## **Prim 알고리즘**
- 시작 정점을 기준으로 가장 작은 간선과 연결된 정점을 선택하며 신장 트리를 확장시키는 알고리즘
- 정점 선택을 기반으로 하는 알고리즘  

## **Prim 알고리즘 동작 원리**

![image (1)](https://user-images.githubusercontent.com/63101648/131241553-c0e7f1ad-d8f1-4372-b5fd-76a1af105ff0.png)

- 임의의 간선 선택
- 선택한 간선의 정점으로부터 가장 낮은 가중치를 갖는 정점 선택
- 모든 정점이 선택될 때까지 반복

### 출처
- https://velog.io/@fldfls/%EC%B5%9C%EC%86%8C-%EC%8B%A0%EC%9E%A5-%ED%8A%B8%EB%A6%AC-MST-%ED%81%AC%EB%A3%A8%EC%8A%A4%EC%B9%BC-%ED%94%84%EB%A6%BC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98
- https://ssungkang.tistory.com/entry/Algorithm-Spanning-Tree-%EC%99%80-MST-%EC%8A%A4%ED%8C%A8%EB%8B%9D-%ED%8A%B8%EB%A6%AC%EC%99%80-%EC%B5%9C%EC%86%8C-%EC%8A%A4%ED%8C%A8%EB%8B%9D-%ED%8A%B8%EB%A6%AC
- https://gmlwjd9405.github.io/2018/08/28/algorithm-mst.html