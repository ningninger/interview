# string stream

## 写入

```c++
stringstream ss;
ss << "Hello";
// str设置
ss.str("Hello");
```

## 读取

遇到delim停止, 并且会进行消耗

```c++
cout << ss;
```

返回所有, 并且不会消耗

```c++
cout << ss.str();
```

## 转化

```c++
using namespace std;
stringstream ss;
int nValue = 12345;
double dValue = 67.89;
ss << nValue << " " << dValue;

string strValue1, strValue2;
ss >> strValue1 >> strValue2;
cout << strValue1 << " " << strValue2 << endl;
/* ----------------------------------------------------- */
stringstream ss;
ss << "12345  67.89";
int nValue;
double dValue;

ss >> nValue >> dValue;
cout << nValue << " " << dValue << endl;
```

## 清空

```C++
ss.str("");
ss.str(std::string());
ss.clear(); //这个成员函数还会将stream的state设为OK, 清空error flags.
```

# 读取一行输入

```c++
string line, token;
getline(cin, line);
stringstream ss(line);
while (ss >> token) { ... }
```

geline会把换行符消耗掉, 但是不会读入`line`

# 常用写法

## 



## int与str

```c++
int stoi(string);
long long stoll(long long);
float stof(string);
double stod(string);
string to_string(int / long long / float / double);

~ ato~(char *);
string.c_str();
```



## 二分

```c++
while (left <= right) {
    int mid = ((right - left) >> 1) + left;
    if (nums[mid] == target) {
        return mid;
    } else if (...) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}
```



## 其它

```c++
bool isdigit(char);
bool isalpha(char);
bool isalnum(char);
```





# STL

## sort

```c++
sort(envelopes.begin(), envelopes.end(), [](const auto& e1, const auto& e2) {
            return e1[0] < e2[0] || (e1[0] == e2[0] && e1[1] > e2[1]);
        });
```

## priority_queue



## deque



## bound

对于小到大的有序

lower_bound: 第一个大于等于的数

upper_bound: 第一个大于的数

用于LIS, lower_bound产生递增子序列, upper_bound产生不降子序列

## 单调栈

在一维数组中对每一个数找到第一个比自己小的元素。这类“在一维数组中找第一个满足某种条件的数”的场景就是典型的单调栈应用场景。

### t1

[84. 柱状图中最大的矩形](https://leetcode.cn/problems/largest-rectangle-in-histogram/)

给定 *n* 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

```c++
int dp1[100000], dp2[100000];
int largestRectangleArea(vector<int>& heights) {
    stack<int> stk;
    // vector<int> dp1(heights.size()), dp2(heights.size());
    int n = heights.size();
    for (int i = 0; i < n; ++i) {
        while (!stk.empty() && heights[stk.top()] >= heights[i])
            stk.pop();
        if (stk.empty())
            dp1[i] = (i + 1) * heights[i];
        else
            dp1[i] = (i - stk.top()) * heights[i];
        stk.push(i);
    }
    stk = stack<int>();
    for (int i = n - 1; i >= 0; --i) {
        while (!stk.empty() && heights[stk.top()] >= heights[i])
            stk.pop();
        if (stk.empty())
            dp2[i] = (n-i)*heights[i];
        else
            dp2[i] = (stk.top()-i)*heights[i];
        stk.push(i);
    }
    int ret = 0;
    for (int i = 0; i < n; ++i) {
        ret = max(ret, dp1[i]+dp2[i]-heights[i]);
    }
    return ret;
}
```



## 单调队列

+ 最基础的形式
+ 结合前缀和
+ dp优化

### 滑动窗口最大值

```c++
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> q;
    for (int i = 0; i < k-1; ++i) {
        while (!q.empty() && nums[q.back()] <= nums[i])
            q.pop_back();
        q.push_back(i);
    }
    vector<int> ret;
    for (int i = k-1; i < nums.size(); ++i) {
        while (!q.empty() && nums[q.back()] <= nums[i])
            q.pop_back();
        q.push_back(i);
        ret.push_back(nums[q.front()]);
        if (q.front() == i - k + 1)
            q.pop_front();
    }
    return ret;
}
```



### 前缀和 单调队列 贪心

返回数组 𝐴 的最短的非空连续子数组的长度，该子数组的和至少为 𝑘 。如果没有和至少为 𝑘 的非空子数组，返回 −1。

```c++
int shortestSubarray(vector<int>& nums, int k) {
    vector<long long> prefix(nums.size()+1, 0);
    for (int i = 0; i < nums.size(); ++i)
        prefix[i+1] = prefix[i] + nums[i];
    deque<int> q;
    q.push_back(0);
    int ret = INT_MAX;
    for (int i = 1; i <= nums.size(); ++i) {
        while (!q.empty() && prefix[i]-prefix[q.front()] >= k) {
            ret = min(ret, i-q.front());
            q.pop_front();
        }
        while (!q.empty() && prefix[q.back()] >= prefix[i])
            q.pop_back();
        q.push_back(i);
    }
    return ret==INT_MAX?-1:ret;
}
```

### 单调队列优化dp

给定一个下标从 0 开始，元素个数为 𝑛(𝑛≤105) 的整数数组 𝑎 和一个整数 𝑘 。开始在下标 0 处。每一步，最多可以往前跳 𝑘 步，但不能跳出数组的边界。也就是说，可以从下标 𝑖 跳到 ，[𝑖+1，𝑚𝑖𝑛(𝑛−1,𝑖+𝑘)] 包含 两个端点的任意位置。
目标是到达数组最后一个位置（下标为 𝑛−1 ），**得分** 为经过的所有数字之和，求得分的最大值。

```c++
int maxResult(vector<int>& nums, int k) {
    deque<int> q;
    vector<int> dp(nums);
    q.push_back(0);
    for (int i = 1; i < nums.size(); ++i) {
        dp[i] += dp[q.front()];
        while (!q.empty() && dp[q.back()] <= dp[i])
            q.pop_back();
        q.push_back(i);
        if (q.front() == i - k)
            q.pop_front();
    }
    return dp[nums.size() - 1];
}
```

在幻想乡，琪露诺是以笨蛋闻名的冰之妖精。

某一天，琪露诺又在玩速冻青蛙，就是用冰把青蛙瞬间冻起来。但是这只青蛙比以往的要聪明许多，在琪露诺来之前就已经跑到了河的对岸。于是琪露诺决定到河岸去追青蛙。

小河可以看作一列格子依次编号为 00 到 𝑁*N*，琪露诺只能从编号小的格子移动到编号大的格子。而且琪露诺按照一种特殊的方式进行移动，当她在格子 𝑖*i* 时，她只移动到区间 [𝑖+𝐿,𝑖+𝑅][*i*+*L*,*i*+*R*] 中的任意一格。你问为什么她这么移动，这还不简单，因为她是笨蛋啊。

每一个格子都有一个冰冻指数 𝐴𝑖*A**i*，编号为 00 的格子冰冻指数为 00。当琪露诺停留在那一格时就可以得到那一格的冰冻指数 𝐴𝑖*A**i*。琪露诺希望能够在到达对岸时，获取最大的冰冻指数，这样她才能狠狠地教训那只青蛙。

但是由于她实在是太笨了，所以她决定拜托你帮它决定怎样前进。

开始时，琪露诺在编号 00 的格子上，只要她下一步的位置编号大于 𝑁*N* 就算到达对岸。

```c++
int n, l, r;
int arr[400001], f[400001];

int main() {
	scanf("%d %d %d", &n, &l, &r);
	for (int i = 0; i <= n; ++i)
		scanf("%d", &arr[i]);
	deque<int> q;
	q.push_back(0);
	f[0] = 0;

	for (int i = l; i <= n+r; ++i) {
		if (q.empty())
			f[i] = INT_MIN;
		else
			f[i] = arr[i] + f[q.front()];
		if (i+1-l >= l) {
			while (!q.empty() && f[q.back()] <= f[i+1-l])
				q.pop_back();
			q.push_back(i+1-l);
		}
		if (!q.empty() && q.front() == i-r)
			q.pop_front();
	}
	int ret = INT_MIN;
	for (int i = n+1; i <= n+r; ++i)
		ret = max(ret, f[i]);
	printf("%d", ret);
}
```







# 其它

[ACM常用模板(+模板题)(基础)_acm竞赛模板-CSDN博客](https://blog.csdn.net/zxzxzx0119/article/details/79838261)

+ 泛型模板

# dp

滚动数组与初始化

```c++
memset(arr2, ~0x3f, sizeof arr2);
arr2[bias] = 0;
// 注意初始化arr2而不是arr1
// 初始化inf可以用0x3f, 初始化-inf用~0x3f
swap(arr1, arr2);
// 交换
```

# c++ 模板

```c++
template<typename  T> void swap(T& t1, T& t2) {
    T tmpT;
    tmpT = t1;
    t1 = t2;
    t2 = tmpT;
}

swap(num1, num2);
```

```c++
template <class T> class Stack {
    public:
        Stack();
        ~Stack();
        void push(T t);
        T pop();
        bool isEmpty();
    private:
        T *m_pT;        
        int m_maxSize;
        int m_size;
};

template <class  T>  Stack<T>::Stack(){
   m_maxSize = 100;      
   m_size = 0;
   m_pT = new T[m_maxSize];
}
template <class T>  Stack<T>::~Stack() {
   delete [] m_pT ;
}
        
template <class T> void Stack<T>::push(T t) {
    m_size++;
    m_pT[m_size - 1] = t;
    
}
template <class T> T Stack<T>::pop() {
    T t = m_pT[m_size - 1];
    m_size--;
    return t;
}
template <class T> bool Stack<T>::isEmpty() {
    return m_size == 0;
}

Stack<int> intStack;
```

加其它参数

```c++
template <class T, int maxsize = 100> class Stack {
    public:
        Stack();
        ~Stack();
        void push(T t);
        T pop();
        bool isEmpty();
    private:
        T *m_pT;        
        int m_maxSize;
        int m_size;
};
template <class T,int maxsize> Stack<T, maxsize>::Stack(){
   m_maxSize = maxsize;      
   m_size = 0;
   m_pT = new T[m_maxSize];
}
template <class T,int maxsize>  Stack<T, maxsize>::~Stack() {
   delete [] m_pT ;
}
        
template <class T,int maxsize> void Stack<T, maxsize>::push(T t) {
    m_size++;
    m_pT[m_size - 1] = t;
    
}
template <class T,int maxsize> T Stack<T, maxsize>::pop() {
    T t = m_pT[m_size - 1];
    m_size--;
    return t;
}
template <class T,int maxsize> bool Stack<T, maxsize>::isEmpty() {
    return m_size == 0;
}

Stack<int,1024> intStack;
```

模板专门化

```c++
template<class T> void swap(T& t1, T& t2) {
    T tmpT;
    tmpT = t1;
    t1 = t2;
    t2 = tmpT;
}

void swap(std::vector<int>& t1, std::vector<int>& t2) {
    t1.swap(t2);
}

template<class V> void swap(std::vector<V>& t1, std::vector<V>& t2) {
    t1.swap(t2);
}
```

