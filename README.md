#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main()
{
	FILE *fp1, *fp2;
	char *str;
	int len;
	char lat[100];
	char lon[100];
	char time[100]; 
	int i=0;
	fp1=fopen("C:\\Users\\q\\Desktop\\export.gpx","r");
	fp2=fopen("C:\\Users\\q\\Desktop\\export.csv","w");
	if((fp1 =fopen("C:\\Users\\q\\Desktop\\export.gpx","r"))==0) 
	{
		printf("文件读取错误");
		return (-1);
	}
	fseek(fp1,0,SEEK_END);
	len=ftell(fp1);
	str=(char*)malloc(len);//	printf("length=%d\n",len);
   
	fseek(fp1,0,SEEK_SET);//fread(text,1,len,fp1);
	
	fread(str,sizeof(char),len,fp1);
	
	fprintf(fp2,"经度           纬度          时间\n");

	while(!((*(str+i)=='<')&&(*(str+i+1)=='/')&&(*(str+i+2)=='g')&&(*(str+i+3)=='p')&&(*(str+i+4)=='x')&&(*(str+i+5)=='>')))
	{
		if(((*(str+i)==' ')&&(*(str+i+1)=='l')&&(*(str+i+2)=='a')&&(*(str+i+3)=='t')))
		{
	        strncpy(lat,&str[i+6],9);
	        lat[9]='\0';
	        printf("%s\t",lat);
	        strncpy(lon,&str[i+22],10);
	        lon[10]='\0';
	        printf("%s\t",lon);
	        strncpy(time,&str[i+44],20);
	        time[19]='\0';
	        printf("%s\n",time);
	        fprintf(fp2,"%s     %s    %s\n",lat,lon,time); 
     	}
     	i++;
    }
    fclose(fp1);
    fclose(fp2);
	return 0;
} 
