# 2018暑期第一次积分赛解题报告
## A-计算两点间的距离
### describe
     输入两点坐标（X1,Y1）,（X2,Y2）,计算并输出两点间的距离。 
     Input
        输入数据有多组，每组占一行，由4个实数组成，分别表示x1,y1,x2,y2,数据之间用空格隔开。
     Output
        对于每组输入数据，输出一行，结果保留两位小数。
     Sample Input

        0 0 0 1
        0 1 1 0
     Sample Output

        1.00
        1.41
### code
    //两点间距离公式，输出保留两位小数
 ```cpp   
    #include <iostream>
    #include <cmath>
    #include <iomanip>
    #include <algorithm>
    using namespace std;
    int main()
    {
	    double x1,y1,x2,y2;
	    while(cin>>x1>>y1>>x2>>y2)
	    {
    	    double sum;
		    sum=sqrt(fabs(x1-x2)*fabs(x1-x2)+fabs(y1-y2)*fabs(y1-y2));
            cout<<setiosflags(ios::fixed)<<setprecision(2)<<sum<<endl;
        }
    	return 0;
    } 
```

## B-小学生的游戏
### describe
    
    某天，无聊的小斌叫上几个同学玩游戏，其中有比较笨的小兴，比较傻的小雪，可爱的小霞和自以为是的小楠。他们去找聪明的小明去给他们当裁判。判定谁取得游
    戏胜利。
    而这个游戏是由小斌想个1到10000000的数字让大家猜，看谁先猜中。为了防止小斌作弊，小明记录下了游戏的整个过程。你的任务是判断小斌是否有作弊。
    Input
        输入数据包括多盘游戏。一次猜数包含两行，第一行是一个数字n(1<=n<=10000000)，表示所猜数字。第二行是小斌的回答为"too high","too low","right 
        on"三种答案之一。每盘游戏结束于"right on"。当n=0的时候，整个游戏结束。
    Output
        对于每盘游戏，若小斌确有撒谎，请输出一行"The guy is dishonest",否则请输出"The guy may be honest"。
    Sample Input

        10
        too high
        3
        too low
        4
        too high
        2
        right on
        5
        too low
        7
        too high
        6
        right on
        0

    Sample Output

        The guy is dishonest
        The guy may be honest
### code
    //构建ans结构体，用结构体数组保存猜数的情况，然后遍历结构体数组与最后一组回答情况比较。
    //注：cin.getline前需要加上getchar接收前面输入的回车。
```cpp    
    #include <iostream>
    #include <cmath>
    #include <iomanip>
    #include <algorithm>
    #include <string>
    using namespace std;
    struct ans
    {
    	int num;    //猜的数
    	char a[15]; //小斌的回答
    };
    int main()
    {
    	ans s[105];
    	int len;
    	int i;
    	const char x[15]={"right on"};
    	const char b[15]={"too high"};
    	const char c[15]={"too low"};
    	bool flag;
    	while(cin>>s[0].num&&s[0].num)
    	{
    		len=0;
    		getchar();
    		flag=1;
    		cin.getline(s[0].a,15);
    		len++;
    		while(strcmp(s[len-1].a,x)!=0)
    	   	{
    	   		cin>>s[len].num;
    	   		getchar();
    	   		cin.getline(s[len].a,15);
    	   		len++;
    		}
    		for(i=0;i<len-1;i++)
    		{
    			if(s[i].num<=s[len-1].num&&strcmp(s[i].a,b)==0)
    			{
    				flag=0;
    				break;
    			}
    			if(s[i].num>=s[len-1].num&&strcmp(s[i].a,c)==0)
    			{
    				flag=0;
    				break;
    			}
    		}
    		if(flag) cout<<"The guy may be honest"<<endl;
    		else cout<<"The guy is dishonest"<<endl;
    	}
    	return 0;
    } 
```
 ## D-又见LKity
 ### describe
 
    嗨！大家好，在TempleRun中大家都认识我了吧。我是又笨又穷的猫猫LKity。很高兴这次又与各位FZU的ACMer见面了。最近见到FZU的各位ACMer都在刻苦地集训，
    整天在日光浴中闲得发慌的我压力山大呀！于是，我准备为诸位编写一款小工具——LKity牌文本替换（众怒，：敢不敢更土点！）。这个小工具可以帮助诸位替换代
    码中的变量等功能，真心是一款编程，刷题必备的神器。其功能如下：
    将给定的字符序列中所有包含给定的子串替换成另外一个给定的字符串。为了让其功能更加强大，替换过程中，将忽略大小写。并且不进行递归替换操作。
    不过，作为笨笨的猫猫，我是心有余而力不足呀！希望诸位ACMer能帮我实现哈。（众FZU的ACMer：”……”）；
    Input
        输入包含多组数据。 输入为标准输入，输入包含3行。 第一行为需要查找的字符串S1。S1仅由大写或者小写字母组成，且其长度在区间[1，,100]内。 第二行
        为要替换的字符串S2。S2由[32,125]的字符组成，且其长度在区间[1,100]内。 第三行为原始字符串S，S由[32,125]的字符组成。且其长度在区间
        [1,50,000]内。 
    Output
        对于每组数据，请输出替换后的字符串。 
    Sample Input
        abc
        bc ab
        aaa aaabca 333Abcc##
    Sample Output
        aaa aabc aba 333bc abc##
 ### code
    /*
    定义一个sum字符串用来储存结果，遍历S串，比较与S1串长度相同的字串是否与S1串相等（比较时都换成大写或者小写比较），如果相等，将S2串存入sum串相应的 
    位置，如果不等存入相应的S串
    存入时要注意位置，S2和S都可能含有空格，输入时不能用cin。
    */
 ```cpp   
    #include <iostream>
    #include <iostream.h> 
    #include <cmath>
    #include <iomanip>
    #include <algorithm>
    #include <string>
    using namespace std;
    bool contain(char *s,char *t,int n)//判断S串和T串是否相同 
    {
        for(int i=0;i<n;i++)
        {
            if(tolower(s[i])!=tolower(t[i])) return 0;
        }
        return 1;
    }
    int main()
    {
        char s1[105];
        char s2[105];
        char s[500500];
        char sum[500500];
        int i,j,k;
        while(cin>>s1)
        {
            getchar();
            int lens=0;
            cin.getline(s2,105);
            cin.getline(s,500500);
            int len1,len2,len;
            len1=strlen(s1);
            len2=strlen(s2);
            len=strlen(s);
            for(i=0;i<len;)
            {
                if(contain(s+i,s1,len1))
                {
                    for(j=0;j<len2;j++)
                    {
                        sum[lens]=s2[j];
                        lens++;
                    }
                    i+=len1;
                }
                else {
                    sum[lens]=s[i];
                    lens++;
                    i++;
                }
            }
            sum[lens]='\0';
            cout<<sum<<endl;
        }
        return 0;
    }
```    
## E-数字的孔数
### describe
         S得到一个数，他想知道这个数每一位上的数字的孔数之和。1,2,3,5,7这几个数字是没有孔的，0,4,6,9都有一个孔，8有两个孔。 
    Input
        输入数据的第一行为一个数T表示数据组数。接下来T行，每行输入一个正整数n(1<=n<=1000)，表示要求数字孔数之和的数。n不会有前导0。 
    Output
        对于每组数据输出一行一个整数，表示该数的每一位上的数字的孔数之和。 
    Sample Input
        2
        42
        669
    Sample Output
        1
        3
### code
    //按位数拆开求孔数和即可。
```cpp    
    #include <iomanip>
    #include <algorithm>
    #include <string>
    using namespace std;
    int main()
    {
        int t;
        int n;
        cin>>t;
        while(t--)
        {
            cin>>n;
            int sum=0;
            int num;
            while(n)
            {
                num=n%10;
                n/=10;
                if(num==0||num==4||num==6||num==9) sum+=1;
                else if(num==8) sum+=2;
            }
            cout<<sum<<endl;
        }
        return 0;
    }
```    
## F-简单的等式
### describe
         现在有一个等式如下：x^2+s(x,m)x-n=0。其中s(x,m)表示把x写成m进制时，每个位数相加的和。现在，在给定n，m的情况下，求出满足等式的最小的正整数
         x。如果不存在，请输出-1。 
    Input
        有T组测试数据。以下有T(T<=100)行，每行代表一组测试数据。每个测试数据有n（1<=n<=10^18），m(2<=m<=16)。 
    Output
        输出T行，有1个数字，满足等式的最小的正整数x。如果不存在，请输出-1。 
    Sample Input
        4
        4 10
        110 10
        15 2
        432 13
    Sample Output
        -1
        10
        3
        18
### code
    /*
    看到题目首先想到的是枚举法，枚举x的值，然后带入等式中验算
    第一次，x枚举范围[1~1000000],结果TLE，想了一下，可能x没有这么大，x范围缩小为[1~100000]，结果WA。想了一会没有找到更好的方法就先放着了
    回过头来看发现S(x,m)范围很小，一百位的二进制数值为2^100，S(x,m)最大为100，当m为16进制时，16^(100/15)也很大，题目明显不是大数题，所以
    S(x,m)的范围很小，这里我取得的是100，可能更大或者更小。
    这样枚举S(x,m)的值题目就变为已知一元二次方程求是否有整数解了，把求出的解带回式子验算即可。
    */
```cpp    
    #include <iostream>
    #include <cmath>
    #include <iomanip>
    #include <algorithm>
    #include <string>
    using namespace std;
    int s(int x,int m)
    {
        int sum=0;
        while(x)
        {
            sum+=(x%m);
            x/=m;
        }
        return sum;
    }
    int main()
    {
        int t;
        long long n,m;
        long long x;
        cin>>t;
        while(t--)
        {
            int num;
            cin>>n>>m;
            int i;
            bool flag=1;
            for(i=1;i<=100;i++)
            {
                long long sum=sqrt(n*4+i*i)/2-i/2;
                if(sum*sum+s(sum,m)*sum==n)
                {
                    cout<<sum<<endl;
                    flag=0;
                    break;
                }
            }
            if(flag) cout<<-1<<endl;
        }
        return 0;
    } 
```
## G-众数问题
### describe
	    给定含有n个元素的多重集合S，每个元素在S中出现的次数称为该元素的重数。多重集S中重数最大的元素称为众数。
	    例如，S={1，2，2，2，3，5}。
	    多重集S的众数是2，其重数为3。
	    现在给你一个已经排好序的集合S，让你求出其众数和重数。
	Input
	    输入只有一行，有一个整数n(1<=n<=100)开始，表示集合S中元素个数，接下来有n个由一个空格隔开的整数(-100~100), 为集合S的元素，<br>元素从小到大或者从大到小给出。 
	Output
	    输出一行二个整数X和Y，X表示众数和Y为重数，用一个空格隔开。如果存在多个解，只需输出值最小的众数即可。 
	Sample Input
	    6 1 2 2 2 3 5
	    3 -1 -1 -1
	Sample Output
	    2 3
	    -1 3
### code
	//用一个数组记录S集中各数出现的次数，数组的下标为数的值，遍历数组找到从数和重数即可。
```cpp	
	#include <iostream>
	#include <cmath>
	#include <iomanip>
	#include <algorithm>
	#include <string>
	using namespace std;
	int main()
	{
		int n;
		int i;
		int num[105];
		int sum;
		while(cin>>n)
		{
			int a[205]={0};
			int max=0;
			for(i=0;i<n;i++)
			{
				cin>>num[i];
				num[i]+=100;
				a[num[i]]++;
			}
			for(i=0;i<205;i++)
			{
				if(a[i]>max){
					sum=i;
					max=a[i];
				}
			}
			cout<<sum-100<<" "<<max<<endl;
		}
		return 0;
	}
```	
## H-分解质因数
### describe
	     假设x是一个正整数，它的值不超过65535(即1<x<=65535)，请编写一个程序，将x分解为若干个素数的乘积。 
	Input
	    输入的第一行含一个正整数k (1<=k<=10)，表示测试例的个数，后面紧接着k行，每行对应一个测试例，包含一个正整数x。 
	Output
	    每个测试例对应一行输出，输出x的素数乘积表示式，式中的素数从小到大排列，两个素数之间用“*”表示乘法。 
	Sample Input

	    2
	    11
	    9828

	Sample Output

	    11
	    2*2*3*3*3*7*13
### code
	//循环出输出这个数的质因子，直到这个数本身为质数为止
```cpp
	#include <iostream>
	#include <cmath>
	#include <iomanip>
	#include <algorithm>
	#include <string>
	using namespace std;
	bool isprime(int x)
	{
		int n=sqrt(x);
		int i;
		for(i=2;i<=n;i++)
		{
			if(x%i==0) return 0;
		}
		return 1;
	}
	int main()
	{
		int t;
		int x;
		int i;
		cin>>t;
		while(t--)
		{
			cin>>x;
			while(!isprime(x))
			{
				int n=sqrt(x);
				for(i=2;i<=n;i++)
				{
					if(x%i==0) {
						cout<<i<<"*";
						x/=i;
						break;
					}
				}
			}
			cout<<x<<endl;
		}
		return 0;
	}
```
## I-穿越沙漠
### describe
	     一辆吉普车来到x公里宽的沙漠边沿A点，吉普车的耗油量为1升/公里，总装油量为500升。通常，吉普车必须用自身油箱中的油在沙漠中设置若干个临时储
	     油点，才能穿越沙漠的。假设在沙漠边沿A点有充足的汽油可供使用，那么吉普车从A点穿过这片沙漠到达终点B，至少要耗多少升油。请编写一个程序，计
	     算最少的耗油量（精确到小数点后3位）。
	    （1）假设吉普车在沙漠中行进时不发生故障；
	    （2）吉普车在沙漠边沿A点到终点B的直线距离为x≧500公里(即沙漠宽度)； 
	Input
	    输入的第一行含一个正整数k (1<=k<=6)，表示测试例的个数。后面紧接着k行，每行对应一个测试例，包含一个正整数x，表示从A点到B点的距离
	    （1<=x<=2000）。 
	Output
	    每个测试例对应一行输出，包含一个数，表示最少的油耗量。 
	Sample Input
	    2
	    500
	    1000
	Sample Output
	    500.000
	    3836.497
### code
	
	除C题外我认为最难的一题，这里尽量把思路写的详细一些。
	车子要穿越沙漠，
	当距离小于500时，毫无疑问，距离是多少就需要多少油。
	当距离大于500时就需要建立储油点，如何建立储油点就是最关键的问题。
	这时需要反着分析，要使耗油量最少，毫无疑问，最后的一个储油点的位置是离终点500里处，且当车子经过这里车子所剩的油加上储油点的刚好为500，
	可以看成，最后一个储油点需要有500升油。(oid[1]=500,2k-1=1,x[1]=500)
	然后是倒数第二个储油点，这个储油点需要往倒数第一个储油点送500升油，不难发现两储油点车子的往返数是奇数，设为2k-1，当k=1，无法运送500
	升油，k=2时往返3次，距离x=500/3时刚好可以运送500升，此时第二个储油点为1000升，当k=3时往返5次，x=200，需储油1500升，以此类推当x=500/3
	时耗油量最少，所以倒数第二储油点储油1000升。(oil[2]=1000,2k-1=3,x[2]=500/3)。
	类推可知倒数第三个储油点与倒数第二个储油点需往返5次，k=3，距离x=500/5，储油oil[3]=1500。(oil[3]=1500,2k-1=5,x[3]=500/5)
	.......
	可得出公式：oil[i]=oil[i-1]+(2i-1)*x[i],oil[1]=500
	oil[i]=500*i
	可以最少需要油量oil=oil[k]+(x[1]+....+x[k]-x)*(2*k-1)
```cpp	
	#include <iostream>
	#include <cmath>
	#include <iomanip>
	#include <algorithm>
	#include <string>
	using namespace std;
	int main()
	{
		int t;
		int k;
		double oil,sum,x;
		cin>>t;
		while(t--)
		{
			cin>>x;
			k=1;
			sum=500;
			if(x<500)
			{
				oil=x;
			}
			while(sum<x)
			{
				k++;
				sum+=(double)500/(2*k-1);
			}
			oil=500*k+(x-sum)*(2*k-1);	//倒数第k个储油点的油量减去多出距离的耗油量(第K个储油点在起点或者起点的后面)
			cout<<setiosflags(ios::fixed)<<setprecision(3)<<oil<<endl;
		}
		return 0;
	} 
```	
## J-神庙逃亡
### describe


	    话说最近穷猫猫LKity意外得到了一部ANDROID手机，于是，LKity兴奋地为自己的新机子安装了神往已久的游戏——神庙逃亡（Temple Run）。可惜，
	    LKity不仅仅是一只穷猫猫，更是一只笨猫猫。每次她玩这款游戏的时候，都被群鄙视了。例如下图所示情形：
	    逃亡路途中，在Merida公主正前方S米出现了一堵火墙。火墙高度为H米。LKity控制着Merida公主以垂直方向上为Vy米/秒的速度试图跨越前方的火墙。已
	    知现在Merida公主奔跑的速度（即水平速度）为Vx米/秒。你猜猜，笨笨的LKity能顺利控制Merida公主通过此障碍吗？【注：为了简便，在TempleRun的
	    世界中，重力加速度恒为10m*s^-2】
	Input
	    输入为标准输入，输入数据第一行为一个正整数T(1<=T<=100)表示接下来有T组测试数据 接下来为T行，每行一组数据，包括4个正整数S，H。Vx，Vy用空
	    格隔开。其中，所有整数都在区间【1，1,000,000】内。数据保证S为Vx的倍数。 
	Output
	    对于每组数据，请输出一行，如果Merida公主能顺利通过前方火墙则输出“good done!”，否则输出“poor Merida!”。 
	Sample Input
	    2
	    100 1 1 1
	    10 1 10 100
	Sample Output
	    poor Merida!
	    good done!
### code
	//物理题，X=V0*t-1/2*g*t^2
```cpp	
	#include <iostream>
	#include <cmath>
	#include <iomanip>
	#include <algorithm>
	#include <string>
	using namespace std;
	int main()
	{
		int T;
		cin>>T;
		int s,h,x,y;
		bool flag;
		while(T--)
		{
			cin>>s>>h>>x>>y;
			int t=s/x;
			int m=y*t-(10*t*t)/2;
			if(m>h) cout<<"good done!"<<endl;
			else cout<<"poor Merida!"<<endl;
		}
		return 0;
	} 
```	
