# student-
//5.15总框架 
//5.16.调试完search(),   :调用完search后，文本会被删除 !!!已解（文件的读写方式不符“if((fp=fopen("F:\1413.txt","a+"))==NULL)”）
//5.16。insert()函数问题 ,such   2-4之间插入，却在4之后，不在2-4之间
//功能缺失：成绩排名，平均成绩 
//不能多条添加 已解 
//5.28   未用二进制文件打开，文件指针fseek问题! 
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<conio.h>
struct iii
{
	int num;
	char name[20];
	int English;
	int Math;
	int Computer;
}stu[100];
void menu()
{
	printf("\n\n\n\n\n");
	printf("\t\t|--------------------------------------------|\n");
	printf("\t\t|-----------------0.exit---------------------|\n");
	printf("\t\t|-----------------1.in-----------------------|\n");
	printf("\t\t|-----------------2.search-------------------|\n");
	printf("\t\t|-----------------3.delete-------------------|\n");
	printf("\t\t|-----------------4.xiugai-------------------|\n");
	printf("\t\t|-----------------5.insert-------------------|\n");
	printf("\t\t|-----------------6.total--------------------|\n");
	printf("\t\t|--------------------------------------------|\n");
	printf("\n\nplease choose0~7:\n");
	
}
void show()
{
	int i,m=0,snum;
	char ch[2];
	FILE *fp;
	if((fp=fopen("F:/1413.txt","r"))==NULL)
	  {
	  	printf("not open!\n");
	  	return;
	  }
	   while(!feof(fp))
	  {
	  	if((fread(&stu[m],sizeof(struct iii),1,fp))==1)
	  		m++;
	  }
	  fclose(fp);
	  if((fp=fopen("F:/1413.txt","r"))==NULL)
	  {
	  	printf("not open!\n");
	  	return;
	  }
	  for(i=0;i<m;i++)
	  {
	  	printf("number:");	
	   	printf("%d\t",stu[i].num);
	   	printf("name:");
	   	printf("%s\t",stu[i].name);
	   	printf("English");
	   	printf("%d\t",stu[i].English);
	   	printf("Math");
	   	printf("%d\t",stu[i].Math);
	   	printf("Computer");
	   	printf("%d\t",stu[i].Computer);
	   	printf("\n");
		}
		fclose(fp);
}
void in()
{
	  int  i,m=0;
	  char ch[2];
	  
	  printf("please input yes or no");
	  scanf("%s",&ch);
	  while(strcmp(ch,"y")==0||strcmp(ch,"Y")==0)
	{
			FILE *fp;
	  if((fp=fopen("F:/1413.txt","r+"))==NULL)
	  {
	  	printf("not open!\n");
	  	return;
	  }
	  while(!feof(fp))
	  {
	  	if((fread(&stu[m],sizeof(struct iii),1,fp))==1)
	  		m++;
	  }
	  fclose(fp);
			printf("number：");
			scanf("%d",&stu[m].num);
	  for(i=0;i<m;i++)
			  if(stu[i].num==stu[m].num)
	  			{
				printf("the number is exising,press any key to continue\n");
	  			getch();
	  			fclose(fp);
	  			return;
	  			}
			printf("name：");
			scanf("%s",&stu[m].name);
			printf("English:");
			scanf("%d",&stu[m].English);
			printf("Math:");
			scanf("%d",&stu[m].Math);
			printf("Computer:");
			scanf("%d",&stu[m].Computer);
			if((fp=fopen("F:/1413.txt","a"))==NULL)
			{
				printf("cannot find");
				return;
			}
			if((fwrite(&stu[m],sizeof(struct iii),1,fp))!=1)
				printf("cannot save");
			else{
				printf("%s is save",stu[m].name);
				m++;
			}
			fclose(fp);
			printf("continue?(y/n)");
			scanf("%s",&ch);
		}
		
}

void search()
{
	int i,m=0,snum;
	char ch[2];
	FILE *fp;
	if((fp=fopen("F:/1413.txt","r"))==NULL)
	  {
	  	printf("not open!\n");
	  	return;
	  }
	  while(!feof(fp))
	  {
	  	if((fread(&stu[m],sizeof(struct iii),1,fp))==1)
	  		m++;
	  }
	  fclose(fp);
	  printf("please input what you want to search number");
	  scanf("%d",&snum);
	  if((fp=fopen("F:/1413.txt","r"))==NULL)
			{
				printf("cannot find");
				return;
			}
	  for(i=0;i<m;i++)
		if(stu[i].num==snum)
{
	  	printf("search it!show it?(y/n)");
	  scanf("%s",&ch);	   
	   if(strcmp(ch,"y")==0||strcmp(ch,"Y")==0)
	   {
	  	printf("number:");	
	   	printf("%d\t",stu[i].num);
	   	printf("name:");
	   	printf("%s\t",stu[i].name);
	   	printf("English");
	   	printf("%d\t",stu[i].English);
	   	printf("Math");
	   	printf("%d\t",stu[i].Math);
	   	printf("Computer");
	   	printf("%d\t",stu[i].Computer);  	
	   }
}
else 
	   printf("cannot search it");//
	fclose(fp);
}
void Delete()
{
	int i=0,j,m=0,dnum;
	char ch[2];
	struct iii stu[100];
	FILE *fp;
	if((fp=fopen("F:/1413.txt","r+"))==NULL)
	  {
	  	printf("not open!\n");
	  	return;
	  }
	  while(!feof(fp))
	  {
	  	fread(&stu[i],sizeof(struct iii),1,fp);
	  		i++;
	  		m++;
	  }
	  fclose(fp);
	  if((fp=fopen("F:/1413.txt","w"))==NULL)
	  {
	  	printf("not open!\n");
	  	return;
	  }
	  printf("please input what you want to delete number");
	  scanf("%d",&dnum);
	  for(i=0;i<m-1;i++)
	  {
	  	if(stu[i].num!=dnum)
	  		fwrite(&stu[i],sizeof(struct iii),1,fp);
	  }
	  
	  
//	  for(i=0;i<m;i++)
//		if(stu[i].num==dnum)
//			break;
//	  	printf("delete it?(y/n)");
//	  scanf("%s",&ch);	   
//	   if(strcmp(ch,"y")==0||strcmp(ch,"Y")==0)
//			for(j=i;j<m;j++)
//			stu[j]=stu[j+1];
//			m--;  
//			if((fp=fopen("F:/1413.txt","r+"))==NULL)
//			{
//				printf("cannot open");
//				return;
//				 } 	
//	for(i=0;i<m;i++)
//		if(fwrite(&stu[i],sizeof(struct iii),1,fp)!=1)
//		{
//			printf("cannot in");
//			getch();
//			return;
//		}
		fclose(fp);
		printf("delete seccessful");
}
void xiugai()
{
	int i,j,xnum,m=0;
	char ch[2];
	FILE *fp;
	if((fp=fopen("F:/1413.txt","r+"))==NULL)
	{
		printf("cannot open");
		return;
	}
	while(!feof(fp))
	{
		if(fread(&stu[m],sizeof(struct iii),1,fp)==1)
			m++;
	}
	fclose(fp);
	printf("please input the number what you want to ");
	scanf("%d",&xnum);
	for(i=0;i<m;i++)
		if(xnum==stu[i].num)
			break;
	printf("确认修改?(y/n)");
	scanf("%s",&ch);	   
	   if(strcmp(ch,"y")==0||strcmp(ch,"Y")==0)
			if(i<m)
			{
				printf("find this student\n");
			printf("请输入修改的内容:\n");
			printf("name:");
			scanf("%s",&stu[i].name);
			printf("English:");
			scanf("%d",&stu[i].English);
			printf("Math:");
			scanf("%d",&stu[i].Math);
			printf("Computer:");
			scanf("%d",&stu[i].Computer);
		}else{
			printf("cannot find");
			return;
		}
		if((fp=fopen("F:/1413.txt","r+"))==NULL)
			{
				printf("cannot open");
				return;
				 } 	
	for(j=0;j<m;j++)
		if(fwrite(&stu[j],sizeof(struct iii),1,fp)!=1)
		{
			printf("cannot in");
			getch();
			return;
		}
		fclose(fp);
	printf("successful!");
}
void insert()////////////////// 
{
	int i,j,m=0,k,inum;
	char ch[2];
	FILE *fp;
	if((fp=fopen("F:/1413.txt","r+"))==NULL)
	{
		printf("cannot open");
		return;
	}
	while(!feof(fp))
	{
		if(fread(&stu[m],sizeof(struct iii),1,fp)==1)
			m++;
	}
	fclose(fp);
	printf("please input what you want to insert number");
	scanf("%d",&inum);
	if((fp=fopen("F:/1413.txt","r+"))==NULL)
				{
					printf("cannot find");
					return;
				}
	for(i=0;i<m;i++)
		if(stu[i].num==inum)
		break;
		for(j=m-1;j>i;j--)
			stu[j+1]=stu[j];
			printf("please input information\n");
			printf("number:");
			scanf("%d",&stu[i].num);
			for(k=0;k<m;k++)
				if(stu[k].num==stu[i+1].num&&k!=i+1)
				{
					printf("cannot fine ");
					fclose(fp);
					return;
				}
				printf("name:");
				scanf("%s",&stu[i].name);
				printf("English:");
				scanf("%d",&stu[i].English);
				printf("Math:");
				scanf("%d",&stu[i].Math);
				printf("Computer:");
				scanf("%d",&stu[i].Computer);
				
				for(k=0;k<=m;k++)
				{
					if(fwrite(&stu[k],sizeof(struct iii),1,fp)!=1)
					{
						printf("cannot save");
						getch();
					}
				}
				fclose(fp);
 } 

void total()
{
	int i,j,m=0;
	char ch[2];
	FILE *fp;
	if((fp=fopen("F:/1413.txt","r+"))==NULL)
	{
		printf("cannot open");
		return;
	}
	while(!feof(fp))
	{
		if(fread(&stu[m],sizeof(struct iii),1,fp)==1)
			m++;
	}
	printf("人数:%d",m);
	fclose(fp);
}
int main()
{
	int n;
	menu();
	scanf("%d",&n);
	system("cls"); 
	while(n)
	{
		printf("PS:input exit 0 to exit\n\n");
		show();
		switch(n)
		{
			case 1:in();break;
			case 2:search();break;
			case 3:Delete();break;
			case 4:xiugai();break;
			case 5:insert();break;
			case 6:total();break; 
			default:break; 
		}
		getch();
		system("cls"); 
		menu();
		scanf("%d",&n);	
			}
			return 0;
 } 
