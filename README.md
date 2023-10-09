# 条形码编程设计——物联网导论作业 


## code39
ISO/IEC 16388:2007

>https://cdn.standards.iteh.ai/samples/43897/358ed85e97e14c3e81d30f621f57ec34/ISO-IEC-16388-2007.pdf


> 可以表示43个字元，包含大写拉丁字母（A到Z）、数字（0到9）和几个特殊字元（-、.、$，/、+、％与空格）。另有一个外加符号作为终止符号（标示为“*”）。每个字元由九个部分组成：五条线与和四个空格，当中三个部分较宽（二进制1），六个较窄。窄与宽之间的比例并不重要，在1:2和1:3之间都可。本身不包含校验位。数据密度低
> [维基百科]( https://zh.wikipedia.org/wiki/Code39)



编码方式：查表（IEC文档中只提供了这一种方式）

~~~C++
//使用小熊猫ide
#include <rturtle.h>
#include <iostream>
#include<string.h>

using namespace std;

string encode(string& str){
	string out="0100101000";
	
	for(long long unsigned int i=0;i<str.length();i++){
		if(str[i]==48) out+="0001101000";
		if(str[i]==49) out+="1001000010";
		if(str[i]==50) out+="1001000010";
		if(str[i]==51) out+="1011000000";
		if(str[i]==52) out+="0001100010";
		if(str[i]==53) out+="1001100000";
		if(str[i]==54) out+="0011100000";
		if(str[i]==55) out+="0001001010";
		if(str[i]==56) out+="1001001000";
		if(str[i]==57) out+="0011001000";
		if(str[i]==65) out+="1000010010";
		if(str[i]==66) out+="0010010010";
		if(str[i]==67) out+="1010010000";
		if(str[i]==68) out+="0000110010";
		if(str[i]==69) out+="1000110000";
		if(str[i]==70) out+="0010110000";
		if(str[i]==71) out+="0000011010";
		if(str[i]==72) out+="1000011000";
		if(str[i]==73) out+="0010011000";
		if(str[i]==74) out+="0000111000";
		if(str[i]==75) out+="1000000110";
		if(str[i]==76) out+="0010000110";
		if(str[i]==77) out+="1010000100";
		if(str[i]==78) out+="0000100110";
		if(str[i]==79) out+="1000100100";
		if(str[i]==80) out+="0010100100";
		if(str[i]==81) out+="0000001110";
		if(str[i]==82) out+="1000001100";
		if(str[i]==83) out+="0010001100";
		if(str[i]==84) out+="0000101100";
		if(str[i]==85) out+="1100000010";
		if(str[i]==86) out+="0110000010";
		if(str[i]==87) out+="1110000000";
		if(str[i]==88) out+="0100100010";
		if(str[i]==89) out+="1100100000";
		if(str[i]==90) out+="0110100000";

	}
	
	
	
	
	out = out + "010010100";
	return out;
}

bool isLegal(string& str){
	for(long long unsigned int i=0;i<str.length();i++){
		if(str[i]<=90&&str[i]>=65){		//is letter
			return 1;		
		}
		if(str[i]<=57&&str[i]>=48){		//is digit
			return 1;			
		}
		if(str[i]==45||str[i]==46||str[i]==36||str[i]==47||str[i]==37||str[i]==32||str[i]==43){		//is rest
			return 1;
		}
		return 0;
	}
}

void draw(string &str){
	int isBlack = 0;
	for(long long unsigned int i=0;i<str.length();i++){
		
			
			
			if(str[i]=='0') {//narrow

				
					penDown();
					
				
				fd(50);
				rt(90);
				fd(5);
				rt(90);
				fd(50);
				rt(90);
				fd(5);
	
				rt(180);
				fd(5);
				lt(90);
				
				
			}
			if(str[i]=='1') {//wide
		
				
					penDown();
				fd(50);
				rt(90);
				fd(10);
				rt(90);
				fd(50);
				rt(90);
				fd(10);
		
				rt(180);
				fd(10);
				lt(90);
				penUp();
				
			}
			
		isBlack++;
		if(isBlack==8){
			isBlack=0;
		}
	}

}

int main() {
	string str;
	cin>>str;
	
	initWorld(2400,600);
	
	
	
	setSpeed(5000);
	setPenSize(1);
	string out;
	if(isLegal(str)) out=encode(str);
	draw(out);
	

	
	setVisible(0);
	waitClick();
	
	closeWorld();
	return 0;
}
~~~
### 运行后生成学号  条码


## 噪声测试

###结论：存在相对多的全部行像素。

### 斑点
![bandian]
结果
![result]
### 划痕
![划痕]
结果：不能扫出
### 遮挡
![Alt text]
结果：不能扫出

