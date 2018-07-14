# 解题报告
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
