#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<conio.h>
typedef struct {
    int roomnumber;
    char name[10];
    char address[10];
    char phone[10];
    char mail[20];
    int period;
    char arrival[10];
}HOTEL;
struct node{
    int roomnumber;
    char name[10];
    char address[10];
    char phone[10];
    char mail[20];
    int period;
    char arrival[10];
    struct node *link;
};
typedef struct node* NODE;
NODE getnode()
{
    NODE x;
    x=(NODE) malloc (sizeof(struct node));
    if(x==NULL)
    {
        printf("Out of memory\n");
        exit(0);
    }
    return x;
}
NODE insert_rear(HOTEL item,NODE first)
{
    NODE temp,cur;
    temp=getnode();
    temp->roomnumber=item.roomnumber;
    strcpy(temp->name,item.name);
    strcpy(temp->address,item.address);
    strcpy(temp->phone,item.phone);
    strcpy(temp->mail,item.mail);
    temp->period=item.period;
    strcpy(temp->arrival,item.arrival);
    temp->link=NULL;
    if(first==NULL)
    return temp;cur=first;
    while(cur->link!=NULL)
       cur=cur->link;
    cur->link=temp;
    return first;
}
void display(NODE first)
{   //getch();
    NODE cur;
    int count=0;
    if(first==NULL)
    {
        printf("Hotel list is empty\n");
        return;
    }
    cur=first;
    while(cur!=NULL)
    {   
        printf("%10d %10s %10s %10s %10s %10d %10s\n",cur->roomnumber,cur->name,cur->address,cur->phone,cur->mail,cur->period,cur->arrival);
        
        cur=cur->link;
        count++;
    }
    printf("\nNumber of room booked:%d\n",count);
    printf("\n");
}
NODE delete_info(int key,NODE first)
{
    NODE prev,cur;
    if(first==NULL)
    {
        printf("List is empty\n");
        return NULL;
    }
    if(key==first->roomnumber)
    {
        cur=first;
        first=first->link;
        printf("\n\nThe Customer is successfully removed....\n");
        free(cur);
        return first;
    }
   prev=NULL;
   cur=first;
   while(cur!=NULL)
   {
       if(key==cur->roomnumber)
       break;
       prev=cur;
       cur=cur->link;
   }
   if(cur==NULL)
   {
       printf("Search is unsuccessful\n");
       return first;
   }
   prev->link=cur->link;
   printf("\n\nThe Customer is successfully removed....\n");
   free(cur);
   return first;
}
void login()
{   
    int i,n;
    char c=' ';
    char *user_name="USER";
    char *password="PASS";
    char user[10];
    char pass[10];
    for(;;){
    printf("        ENTER USER NAME:");
    scanf("%s",&user);
    printf("        ENTER PASSWORD:");

    for(i=0;i<=10;i++)
    {   
        pass[i]=getch();
        c=pass[i];
        if(c==13)
        break;
        else
        printf("*");
    }
    pass[i]='\0';
    printf("\n");
    if(strcmp(user_name,user)==0 && strcmp(password,pass)==0){
        printf("----------------------------------------------------------\n");
         printf("       WELCOME !!!! LOGIN IS SUCCESSFUL\n");
         printf("----------------------------------------------------------\n");
         break;
         }
    else{
        printf("----------------------------------------------------------\n");
         printf("         SORRY !!!!  LOGIN IS UNSUCESSFUL\n    ");
         printf("----------------------------------------------------------\n");
         }
    }

}
void main()
{
    NODE first;
    int choice;
    HOTEL item;
    first=NULL;
    int key;
    printf("\n  **************************  LOGIN FORM  **************************  \n");
    login();
    printf(" -------------------------------------------------------------------------\n");
	printf("|                                                                         |\n");
	printf("|                                                                         |\n");
	printf("|  OOOOOO   OOOOOO OOOOOO OOOOOO OOOOOO OOOOOO O      O OOOOOOO  OOOOOO   |\n");
	printf("|  O        O    O O      O        O      O    O O    O O        O        |\n");
	printf("|  O  OOOOO OOOOOO OOOOO  OOOOO    O      O    O  O   O O  OOOOO OOOOOO   |\n");
	printf("|  O    O   O  O   O      O        O      O    O   O  O O    O        O   |\n");
	printf("|  OOOOOO   O   O  OOOOOO OOOOOO   O    OOOOOO O    O O OOOOOO   OOOOOO   |\n");
	printf("|                                                                         |\n");
	printf(" -------------------------------------------------------------------------\n");
 	printf("\t\t*************************************************\n");
	printf("\t\t*                                               *\n");
	printf("\t\t*       -----------------------------           *\n");
	printf("\t\t*        WELCOME TO HOTEL DESERT CAVE           *\n");
	printf("\t\t*       -----------------------------           *\n");
	printf("\t\t*                                               *\n");
	printf("\t\t*                                               *\n");
	printf("\t\t*                                               *\n");
	printf("\t\t*    Brought To You By Prerana, Sahana          *\n");
	printf("\t\t*                 Sneha                         *\n");
	printf("\t\t*     CONTACT US: 8431970590       *\n");
	printf("\t\t*************************************************\n\n\n");
    for(;;)
    {    
        printf("******************************  |MAIN MENU|  ***************************** \n");
        printf(" \n Enter 1 -> Book a room");
		printf("\n------------------------");
		printf(" \n Enter 2 -> View Customer Record");
		printf("\n----------------------------------");
		printf(" \n Enter 3 -> Delete Customer Record");
		printf("\n-----------------------------------");
        printf(" \n Enter 4 -> Exit");
		printf("\n-----------------\n");
        printf("\nEnter the choice:");
        scanf("%d",&choice);
        switch(choice)
        {
            case 1: 
                    printf("\n Enter Customer Details:");
		            printf("\n**************************\n");  
                    printf("Room Number:\n");
                    scanf("%d",&item.roomnumber);
                    printf("Name:\n");
                    scanf("%s",item.name);
                    printf("Address:\n");
                    scanf("%s",item.address);
                    printf("Phone NUmber:\n");
                    scanf("%s",item.phone);
                    printf("Mail ID:\n");
                    scanf("%s",item.mail);
                    printf("Period:\n");
                    scanf("%d",&item.period);
                    printf("Arrival Date:\n");
                    scanf("%s",item.arrival);
                    printf("\nRoom is successfully booked!!\n\n");
                    first=insert_rear(item,first);
                    break;
            case 2:
            printf("|Room Nmber| |Name| |Address| |Phone Number| |Mail ID| |Period| |Arrival|\n");
                   display(first);
                   break;
            case 3:
                  printf("Enter the item to be deleted:\n");
                  scanf("%d",&key);
                  first=delete_info(key,first);
                  break;
            case 4:
            exit(0);
            break;
            default: printf("enter valid chocie\n");
        }
    }
}
