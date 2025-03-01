# Bank-Management-System

#include<stdio.h>
#include<string.h>
#include<stdlib.h>

#define maxaccount 100

typedef struct account{
        int accountnumber;
        char name[50];
        float balance;

}acc;

acc accounts[maxaccount];

int accountcount=0;
 void creat();
  void checkbalance();
  void deposite();
  void withdraw();
  void accountdetail();
  int findaccount(int accountnumber);

int main(){
        int choice;
     while(1){
        printf("\n--Bank management--\n");
        printf("1. create new account\n");
        printf("2. check account balance\n");
        printf("3. deposite money\n");
        printf("4. withdraw money\n");
        printf("5. search account\n");
        printf("6. Exit\n");

        printf("Enter your choice:");
        scanf("%d",&choice);

        switch(choice){
                 
                 case 1: creat();
                        break;
                  case 2: checkbalance();
                         break;
                  case 3: deposite();
                         break;
                  case 4: withdraw();
                         break;
                  case 5: accountdetail();
                         break;
                  case 6: printf("Exiting system....");
                          exit(0);
                 default: printf("Enter valid option");           
        }
     }
}
    void creat(){
        if(accountcount>=maxaccount){
                printf("Sorry !! Cannot create more accounts right now....\n");
                return;
        }

        acc newaccount;
          newaccount.accountnumber=accountcount+1;
          printf("Enter your name: ");
          getchar();
          fgets(newaccount.name,sizeof(newaccount.name),stdin);
          newaccount.name[strcspn(newaccount.name,"\n")]='\0';
          newaccount.balance=0.0f;


          accounts[accountcount]=newaccount;
          accountcount++;

          printf("Account created successfully\n");
          printf("Your account number is %d",newaccount.accountnumber);


    }
    void checkbalance(){
        int accountnumber;
        printf("Enter account number: ");
        scanf("%d",&accountnumber);

        int index=findaccount(accountnumber);
        if(index==-1){
              printf("Account not found\n");
              return;
        }

        printf("Account balance : %2f",accounts[index].balance);
    }

    void deposite(){
       int accountnumber;
       float amount;

       printf("Enter account number:");
       scanf("%d",&accountnumber);

       int index=findaccount(accountnumber);
       if(index == -1){
              printf("Account not found\n");
              return;
       }
       printf("Enter deposite amount:");
       scanf("%f",&amount);

       if(amount<=0){
              printf("amount should be greater than 0\n");
              return;
       }

       accounts[index].balance+=amount;

       printf("%2f amount deposited successfully\n",amount);
       printf("available balance : %2f",accounts[index].balance);
    }
    void withdraw(){
       int accountnumber;
       float amount;
        
       printf("Enter account number : ");
       scanf("%d",&accountnumber);

       int index=findaccount(accountnumber);

       if(index==-1){
              printf("Account not found\n");
              return;
       }
       printf("Enter withdraw amount :");
       scanf("%f",&amount);

       if(amount<=0){
              printf("Amount should be greater than 0\n");
              return;
       }

       if(accounts[index].balance<amount){
              printf("Insufficient account balance \n");
              return;
       }
       
       accounts[index].balance-=amount;
       printf("%2f debited successfully\n",amount);
       printf("Available balance : %2f",accounts[index].balance);
    }
    void accountdetail(){
       int accountnumber;
       
       printf("Enter account number :");
       scanf("%d",&accountnumber);

       int index=findaccount(accountnumber);
       if(index==-1){
              printf("Account not found ");
              return;
       }
       printf("\nAccount number : %d\n",accountnumber);
       printf("Account holder name : %s\n",accounts[index].name);
       printf("Account balance : %2f\n",accounts[index].balance);

    }
    int findaccount(int accountnumber){
       for(int i=0;i<accountcount;i++){
              if(accounts[i].accountnumber==accountnumber){
                     return i;
              }
             return -1;
       }
       
    }
