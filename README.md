# Billing-process-

#include<stdio.h>
#include<string.h>
#include<stdlib.h>

int television=0,refrigerator=0,printer=0,laptop=0,dish_washer=0;
float bill=0;
		
struct info {
    char name[40];
    char add[100];
    long long ph;
    char gst[20];
};

struct info i[5] = {
    {"RAJESHVERMA", "102, NEHRU NAGAR ANDHERI EAST MUMBAI MAHARASTRA", 9820123456, "27ABCDE1234F1Z5"},
    {"PRIYANAIR", "45, ROSE GARDEN APARTMENTS KAKKANAD KOCHI KERALA",9847234567 , "27ABCDE1234F1Z5"},
    {"ARJUNSINGH", "12, SECTOR 15 DAWRAKA NEW DELHI ",9876543210 , "27ABCDE1234F1Z5"},
    {"KAVYAREDDY", "56,HITECH CITY ROAD MADAPURA HYDERABAD TELENGANA",9825012345 , "27ABCDE1234F1Z5"},
    {"MANOJPATIL", "89,CG Road NAVARANG PURA AHAMADABAD,GUJURAT",9811198765 , "27ABCDE1234F1Z5"}
};
		
void purchase();
void cancel();
void display_bill();

int main() 
{
    int terminate=1;
    char choice[20];
		printf("\t\t\t\t\t\nSONY ELECTROIC PRIVATE LIMITED(IND)");
    while (terminate== 1) 
    {
        printf("\nMenu: purchase, \nremove, \nbill, \nexit\nEnter choice: ");
        scanf("%s",choice);
        strlwr(choice);

        if (strcmp(choice,"purchase")== 0) 
            purchase();
        else if (strcmp(choice,"remove") ==0) 
        {
            if (refrigerator == 0&&television==0&&printer==0&&laptop==0&&dish_washer==0)
                printf("Please select any item first\n");
            else
                cancel();
        }
        else if (strcmp(choice,"bill")==0) 
        { 
            display_bill(); 
            terminate = 0; 
        }
        else if (strcmp(choice, "exit") == 0) 
            terminate = 0;
        else 
            printf("Invalid choice.\n");
    }

    return 0;
}

void purchase() 
{
    char item[20];
    int qty, end = 1;

    printf("\nAvailable products: refrigerator, television, dishwasher, laptop, printer\nEnter 'end' to stop.\n");
    while (end == 1) 
    {
        printf("Enter item: ");
        scanf("%s", item);
        strlwr(item);
        if(strcmp(item, "end") == 0) 
        {
            end = 0;
            break;
        }
        printf("Enter quantity: ");
        scanf("%d", &qty);

        if (strcmp(item, "refrigerator")==0) 
        { 
            refrigerator += qty; 
            bill += qty * 10000;
        }
        else if (strcmp(item,"television")==0) 
        { 
            television+=qty; 
            bill+=qty*25000; 
        }
        else if(strcmp(item,"dishwasher")==0) 
        { 
            dish_washer+=qty; 
            bill+=qty*15000;
        }
        else if (strcmp(item,"laptop") ==0) 
        { 
            laptop+=qty; 
            bill+=qty*50000; 
        }
        else if(strcmp(item,"printer") == 0) 
        { 
            printer+=qty; 
            bill += qty*2000; 
        }
        else 
            printf("Invalid item.\n");
    }
}

void cancel() 
{
    char item[20];
    int qty,end=1;

    printf("\nAvailable products: refrigerator, television, dishwasher, laptop, printer\nEnter 'end' to stop.\n");
    while (end==1) 
    {
        printf("Enter item: ");
        scanf("%s", item);
        strlwr(item);
        if (strcmp(item,"end")==0) 
        {
            end = 0;
            break;
        }

        printf("Enter Quantity: ");
        scanf("%d", &qty);

        if(strcmp(item,"refrigerator")==0&&refrigerator>=refrigerator) 
        { 
            refrigerator-=qty; 
            bill-=qty*10000;
        }
        else if(strcmp(item,"television")==0&&television>=television) 
        { 
            television-=qty; 
            bill-=qty*25000; 
        }
        else if(strcmp(item,"dishwasher")==0&&dish_washer>=dish_washer) 
        { 
            dish_washer-=qty; 
            bill-=qty*15000;
        }
        else if (strcmp(item,"laptop")==0&&laptop>=laptop) 
        { 
            laptop-=qty; 
            bill-=qty*50000; 
        }
        else if(strcmp(item,"printer")==0&&printer>=printer) 
        { 
            printer-=qty; 
            bill-=qty*2000; 
        }
        else 
            printf("Invalid item or insufficient quantity.\n");
    }
}

void display_bill()
{
    char shopName[40];
    int j,found = 0;
    printf("Available shops to deliver:\n ");
    for(j=0;j<5;j++)
    {
    	printf("%s\n",i[j].name);
	}

    printf("Enter your shop name: ");
    scanf(" %s", shopName);

    for (j = 0; j < 5; j++) 
    {
        if (strcmp(shopName, i[j].name) == 0) 
        {
            printf("\nShop Details:\n");
            printf("Name: %s\n", i[j].name);
            printf("Address: %s\n", i[j].add);
            printf("Phone: %lld\n", i[j].ph);
            printf("GST No: %s\n", i[j].gst);
            found = 1;
            break;
        }
    }

    if (found==0) 
    {
        printf("Shop not found.\n");
        exit(0);
    }

    printf("\n---Purchased Items:---\n");
    printf("ITEM\tQUANTITY\tPRICE\tTOTAL AMOUNT\n");
    if (refrigerator > 0) 
        printf("Refrigerator\t%d\t10000\t%d\n", refrigerator, refrigerator * 10000);
    if (television > 0) 
        printf("Television\t%d\t25000\t%d\n", television, television * 25000);
    if (dish_washer > 0) 
        printf("Dishwasher\t%d\t15000\t%d\n", dish_washer, dish_washer * 15000);
    if (laptop > 0) 
        printf("Laptop\t%d\t50000\t%d\n", laptop, laptop * 50000);
    if (printer > 0) 
        printf("Printer\t%d\t2000\t%d\n", printer, printer * 2000);

    printf("\nTotal Amount: %.2f\n", bill);
}
