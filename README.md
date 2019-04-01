# -
解决两点之间最短路径最优搜索算法
Dijkstra(达杰斯特拉算法)
算法复杂度：O(n 2 )
优点：运行时间较短
缺点：对于截取小路径，从中间点入手不方便
 def ShortestPath_Dijkstra(self,lists):

        MaxVex = 9   #此处是举例 V0-V8搜索最优路径
        self.Inf = 65535
        #进行初始化
        final = [0 for _ in range(MaxVex)]  #用于定义已经访问过的点
        D = [(lists[0][i]) for i in range(MaxVex)]  #储存到该点最短距离
        P = [-1 for _ in range(MaxVex)]   #用于储存路径上一个点位置
        #初始从V0出发，让0点作为最优点，
        D[0] = 0
        final[0] = 1
        for v in range(1,MaxVex):   #接下来从V1开始遍历各点
            min = self.Inf
            for w in range(0,MaxVex):
                if not final[w] and D[w] < min:
                    k = w
                    min = D[w]
            final[k] = 1
            for w in range(0, MaxVex):
                #计算从V0->Vk->Vw点的距离是否小于V0->Vw
                if not final[w] and min + lists[k][w] < D[w]:
                    D[w] = min +lists[k][w]   #保留当前V0 -> Vw的最短距离
                    P[w] = k   #保留Vw之前的前驱点Vk
        print("F:", final)
        print("D:", D)
        print("P:", P)
        string = []
        i = len(P) - 1
        while P[i] != (-1):
            string.append(P[i])
            i = P[i]
        string.append(0)
        string = map(str,string)
        string = '->'.join(string)
        print(string)
弗洛伊德（Floyd）算法
优点：它求所有顶点到所有顶点，相对灵活，代码简洁
缺点：时间复杂度是O(n 3 )，运行时间比较长

    def ShortestPath_Floyd(self,lists):
        MaxVex = 9
        P=[[i for i in range(MaxVex)]for _ in range(MaxVex)]
        D = [[lists[v][w]for w in range(MaxVex)]for v in range(MaxVex)]
        for k in range(MaxVex):
            for v in range(MaxVex):
                for w in range(MaxVex):
                    if D[v][w] > D[v][k] + D[k][w]:
                        D[v][w] = D[v][k] + D[k][w]
                        P[v][w] = P[v][k]
        k = MaxVex - 1
        v = 0
        w = 8
        string = [0]
        while P[v][w] != k:
            v = P[v][w]
            string.append(v)
        string.append(k)
        string = map(str,string)
        print('->'.join(string))
