Source Code


# include<stdio.h># include<stdlib.h>

typedef struct student
{
	char fname[15],lname[15],emailid[30];
	int roll;
	int marks[3];
}student;


FILE *open_file(int class,char section,char mode[4])
{
	int sec;
	student s;
	sec = section;
	FILE* fp;
	if(sec>96 && sec<123)
		sec -= 32;
	if(sec>64 && sec<91)
	{			
		if(class>9)
		{	char file_name[7];file_name[0] = class/10 + 48;file_name[1] = class%10 + 48;
			file_name[2] = sec;file_name[3] = '.';file_name[4] = 't';file_name[5] = 'x';file_name[6] = 't';
			fp = fopen(file_name,mode);
			
		}
		else
		{
			char file_name[6];file_name[0] = class + 48;
			file_name[1] = sec;file_name[2] = '.';file_name[3] = 't';file_name[4] = 'x';file_name[5] = 't';	
			fp = fopen(file_name,mode);
		}
		if(fp == NULL)
		{	printf("can't open file");
			return NULL;
		}
		else
		{	
			return fp;
		}
	}
	else
		return NULL;

}


int see_info(int class,char section)
{
	FILE* fp;
	int roll;
student s;
	fp = open_file(class,section,"rb");
	if(fp == NULL) return 1;
	printf("Enter roll no.,enter 0 to see all : ");scanf("%d",&roll);
	if(roll == 0)
		while(fread(&s,sizeof(student),1,fp) == 1)
		{	printf("\n\n%s %s\n%d - %c - %d\nemail-id : %s\n",s.fname,s.lname,class,section,s.roll,s.emailid);
			printf("\nmarks: science = %d maths = %d language = %d",s.marks[0],s.marks[1],s.marks[2]);
		}
	else
		if(fseek(fp,sizeof(student)*(roll-1),0) == 0)
		{	
			fread(&s,sizeof(student),1,fp);
			printf("%s %s\n%d - %c - %d\nemail-id : %s\n",s.fname,s.lname,class,section,s.roll,s.emailid);
			printf("\nmarks: science = %d maths = %d language = %d",s.marks[0],s.marks[1],s.marks[2]);
		}
		else
			printf("\nthis roll does not exist"); 
	fclose(fp);
}


int update_info(int class,char section)
{
	FILE* fp;
	int roll,n;
	student s;	
	fp = open_file(class,section,"rb+");
	if(fp == NULL) return 1;
	printf("enter student's rollno. :");scanf("%d",&roll);
	if(fseek(fp,sizeof(student)*(roll-1),0) == 0)
	{	fread(&s,sizeof(student),1,fp);
		fseek(fp,sizeof(student)*(roll-1),0);
		printf("%s %s\n%d - %c - %d\nemail id : %s\n",s.fname,s.lname,class,section,s.roll,s.emailid);
		printf("\nmarks: science = %d maths = %d language = %d",s.marks[0],s.marks[1],s.marks[2]);
		printf("\nto update name, press 1 ; other wise press 0 : ");scanf("%d",&n);
		if(n==1)
		{	
			printf("\nenter student's first name : ");scanf("%s",s.fname);
			printf("\nenter student's last name : ");scanf("%s",s.lname);
		}
		n = 0;
		printf("\nto update emailid, press 1 ; other wise press 0 : ");scanf("%d",&n);
		if(n==1)	
			{printf("\nenter student's emailid : ");scanf("%s",s.emailid);}
		n = 0;
		printf("\nto update marks, press 1 ; other wise press 0 : ");scanf("%d",&n);
		if(n==1)
		{	
			printf("\nenter marks; if not known enter -1 :");
			printf("\nenter student's marks in science : ");scanf("%d",s.marks);
			printf("\nenter student's marks in maths : ");scanf("%d",s.marks+1);
			printf("\nenter student's marks in language : ");scanf("%d",s.marks+2);
		}
		if(fwrite(&s,sizeof(student),1,fp)==1)
			printf("\nupdatation completed");
		else printf("\nsomething went wrong...please try later");
	}
	else
		printf("some thing went wrong..this roll does not exist");
	fclose(fp);
		
		
}


int add_info(int class,char section)
{	
	int n;
	while(1)
	{	FILE* fp;
		int roll;
		student so,s;
		fp = open_file(class,section,"rb+");
		if(fp == NULL)return(1);
			
		else
		{
			fseek(fp,-1*sizeof(student),2);
			fread(&so,sizeof(student),1,fp);
			roll = so.roll;
			roll += 1;
			printf("\n roll no. of the new student will be %d",roll);
			printf("\nenter student's first name : ");scanf("%s",s.fname);
			printf("\nenter student's last name : ");scanf("%s",s.lname);
			printf("\nenter student's emailid : ");scanf("%s",s.emailid);
			printf("\nenter marks; if not known enter -1 : ");
			printf("\nenter student's marks in science ");scanf("%d",s.marks);
			printf("\nenter student's marks in maths ");scanf("%d",s.marks+1);
			printf("\nenter student's marks in language ");scanf("%d",s.marks+2);
			s.roll = roll;
			if(roll != 1)
				fwrite(&s,sizeof(student),1,fp);
			else
			{
				fclose(fp);
				fp = open_file(class,section,"wb");
				fwrite(&s,sizeof(student),1,fp);
			}
			
		}
	printf("enter 1 to continue adding new students,otherwise press any key : ");scanf("%d",&n);
	if(n != 1)
		{fclose(fp);
		return(1);}
	fclose(fp);
	}

}
void creat_new_file(int classf,char sectionf)
{
	int sec,c = 0;
	sec = sectionf;
	student s;
	s.roll = 0;
	if(sec>96 && sec<123)
	{	sec -= 32;
		sectionf = sec;
	}

	
	FILE* fp;		
	if(classf>9)
	{	char file_name[8];
		file_name[0] = classf/10 +48;file_name[1] = classf%10 + 48;
		file_name[2] = sectionf;file_name[3] = '.';file_name[4] = 't';file_name[5] = 'x';file_name[6] = 't';file_name[7] = '\0';
		fp = fopen(file_name,"wb");
	}
	else
	{
		char file_name[7];
		file_name[0] = classf + 48;
		file_name[1] = sectionf;file_name[2] = '.';file_name[3] = 't';file_name[4] = 'x';file_name[5] = 't';file_name[6] ='\0';	
		fp = fopen(file_name,"wb");
	}
	
	fwrite(&s,sizeof(student),1,fp);
	fclose(fp);
	fp = open_file(classf,sectionf,"rb");
	student s1;
	fread(&s1,sizeof(student),1,fp);
	printf("\nroll initialized to = %d",s1.roll);
	fclose(fp);
	printf("to add new records in this new file, press 1 : ");scanf("%d",&c);
	if(c == 1)add_info(classf,sectionf);
		
}
	

void main()
{	fflush(stdin);
	int class,choice,a = 1, f = 0,f1 = 0;
	char section;
	printf("\nWelcome to student's database\n\npress 0 to exit : ");
	while(a == 1)
	{	if(f == 1){printf("to remain in current file press 1 other wise press 0 : ");scanf("%d",&f1);}
		if(f == 0 || f1 == 0)
		{	printf("\nenter class and section,for all enter 0 : ");
			printf("\nclass = ");
			scanf("%d",&class);
			printf("\nsection = ");
			section = getc(stdin);
			section = getc(stdin);
		}
		printf("%d%c\n",class,section);
		printf("\n to see database press 1, to update press 2,to add new student press 3, to add new section press 4 : ");
		scanf("%d",&choice);
		if(choice == 1) see_info(class,section);
		else if(choice == 2){if(class>0 && section != '0')update_info(class,section);else printf("to update go one by one");}
		else if(choice == 3) add_info(class,section);
		else if(choice == 4){creat_new_file(class,section);}
		else printf("\nwrong input");
		printf("\nto exit press 0;to continue press 1 : ");scanf("%d",&a);
		f = 1;
		
		
	}
}		




