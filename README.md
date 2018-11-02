# Banking-
//BANK
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<conio.h>
void create();
void manage();
void interest();
void about();
int pos;
struct info
{
		char name[15];
	char dob[10];
	char add[20];
	char num[11];
	char code[20];
}banker1;
	
void main()
{
	int option;

	printf("                                                        WELCOME TO MY_BANK \n");
	printf("Select option:-\n\n1)Create an accoount\n2)Manage Account\n3)About Bank\n\n");
	scanf("%d",&option);
	fflush(stdin);
	switch(option)
	{
		case 1: create();
					break;
					
		case 2: manage();
					break;
					
		case 3: about();
					break;
					
		default: exit(0);
	
	}
 
}
void create()
{
	int acno;
		FILE *acc;
	acc=fopen("C:/Users/SONY/Desktop/acc.txt","w");
	
		printf("Enter your Name: ");
	scanf("%[^\n]",banker1.name);
	fprintf(acc,"%s ",banker1.name);
		fflush(stdin);

	printf("Date Of Birth: ");
	scanf("%[^\n]",banker1.dob);
	fprintf(acc,"%s ",banker1.dob);
		fflush(stdin);

	printf("Address: ");
	scanf("%[^\n]",banker1.add);
	fprintf(acc,"%s ",banker1.add);
		fflush(stdin);
		
	printf("Mobile Number: ");
	scanf("%[^\n]",banker1.num);
	fprintf(acc,"%s ",banker1.num);
	fflush(stdin);

	srand(time(0));
	acno=rand();
     printf("\n\nYour Account is Generated!\n\n");
     printf("Your A/C No.:%d\n",acno);
 
     	fprintf(acc,"\n%d\n",acno);
     
     printf("SETUP PASSWORD : ");
      repeat:
     scanf("%s",banker1.code);
     if(banker1.code[5]!='\0' && banker1.code[4]!='\0' && banker1.code[3]!='\0' && banker1.code[2]!='\0' && banker1.code[1]!='\0'){
     printf("-Password Saved-\n");
     fprintf(acc,"%s\n",banker1.code);}
     else{
     printf("Password too small....Enter a password having atleast 6 characters\n");
     fflush(stdin);
     goto repeat;}
     	printf("\nTHANK YOU FOR BANKING\n\n\n");
     fprintf(acc,"%d\n",0);
     fclose(acc);
     
 }
void manage()
{
	FILE *open;
 	float dep,draw,amt=0;
	int choose;
	int acno,acno1,k;
	char code[20],code1[20];
	char a[10],b[10],c[10],d[10];
	repeat:
	printf("Enter A/C No.: ");
	scanf("%d",&acno);
	
	open=fopen("C:/Users/SONY/Desktop/acc.txt","r+");
	fflush(stdin);
	printf("Enter Password: ");
	scanf("%s",code);

	fscanf(open,"%s %s %s %s %d %s\n",a,b,c,d,&acno1,code1);

	if(acno==acno1 && strcmp(code,code1)==0)
	{
		goto 	logged_in;
	}
	else
	{
		printf("worng details entered\n\n");
		goto repeat;
	}
	logged_in:
	printf("SELECT \n1)Deposit Amount\n2)Withdraw Amount\n3)Balance Enquiry\n\n");
	scanf("%d",&choose);
	k=ftell(open);
		fseek(open,k,0);
			fscanf(open,"%f ",&amt);
	switch(choose)
	{
		case 1:  printf("INR: ");
			   	scanf("%f",&dep);
			   		amt=amt+dep;
					printf("Amount Deposited...\n");
					fseek(open,k,0);
					fprintf(open,"%f ",amt);
					fclose(open);
						printf("\nTHANK YOU FOR BANKING\n\n\n");
					break;
					
		case 2:	printf("INR: ");
					scanf("%f",&draw);
					amt=amt-draw;
					if(amt<0)
					printf("No Sufficient Balance\n");
					else
					printf("Amount Withdraw...\n");
					fseek(open,k,0);
					fprintf(open,"%f ",amt);
					fclose(open);
						printf("\nTHANK YOU FOR BANKING\n\n\n");
					break;
					
		case 3:	printf("Available Balance :-  ");
					fscanf(open,"%f ",&amt);
					fseek(open,k,0);
					printf("%.3f\n",amt);
						printf("\nTHANK YOU FOR BANKING\n\n\n");
					break;   			
	}
}
void about()
{
	printf("This system is created by G.Nitish.\nCoded on C-Free IDE\n");
	printf("\nTHANK YOU FOR BANKING\n\n\n");
}
