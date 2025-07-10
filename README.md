🛒 SuperMegaMarket Billing System
A simple command-line supermarket billing system written in C. The program allows users to view the product list, place orders, and generate a final bill with GST included. Great for learning how to use structures, arrays, and basic input/output in C!


📌 Features
- View available products with pricing
- Place and manage customer orders
- Calculate total bill with GST (18%)
- Simple menu-driven interface


💻 How It Works
Upon running the program:
- The user is greeted with a welcome menu.
- They can choose to:
- View the product list
- Place an order
- Exit the program
- If ordering, the user selects items by ID and inputs quantities.
- The system calculates the total cost and GST, then prints a formatted bill.


🧮 GST Calculation
- GST is applied at 18% on the total value of items purchased.


🧠 Concepts Used
- Structs (Menu, Order)
- Arrays
- String handling
- Conditional logic and loops
- Modular functions
- Basic user input/output via console

----------------------------------------------------------------------
----------------------------------------------------------------------

#include <stdio.h>
#include <string.h>

#define max_order 50
#define max_item 10

struct Menu {
    int id;
    char name[50];
    float price;
};

struct order {
    int itemid;
    int quantity;
    float price;           
    char name[50];
};


struct Menu list[10] = 
{
    {1,"Orange",50},{2,"Apple",70},{3,"Tomato",20},{4,"Potato",30},{5,"Onion",40},{6,"Rice",120},{7,"Eggs",40},{8,"Milk",60},{9,"Paneer",65},{10,"Wheat flour",250}
};

void displaylist() {
    int m=10,i;
    printf("\n\tLIST\n\n");
    printf("Product\t\tPrice\n");
    printf("_______________________________\n");
    for (i=0;i<m;i++) 
	{
        printf("%d. %s \tRs : %.2f\n", list[i].id, list[i].name, list[i].price);
    }
    printf("-----------------\n");
}

float takeorder(struct order orders[], int *count) 
{
    int id,qty,i;
    char ch;
    float Totalammount=0,price,gst,total;

    do {
        printf("Enter item id: ");
        scanf("%d", &id);

        if (id<1||id>10) 
		{
            printf("Invalid item ID! Please enter between 1 and 10.\n");
            continue;
        }

        printf("Enter Quantity: ");
        scanf("%d", &qty);

        orders[*count].itemid = id;
        orders[*count].quantity = qty;

        
        orders[*count].price = list[id - 1].price;
        strcpy(orders[*count].name, list[id - 1].name);

        (*count)++;

        printf("Add more item? (y/n): ");
        while ((getchar()) != '\n'); 
        scanf("%c", &ch);
    } while (ch=='y'||ch=='Y');

    
    printf("\n\n\t   Your Bill\n");
    printf("_________________________________\n");
    printf("Item\t\tQty\tPrice\n");

    for (i=0;i<*count;i++) 
	{
        price = orders[i].price * orders[i].quantity;
        printf("%s\t\t%d\t%.2f\n", orders[i].name, orders[i].quantity, price);
        total += price;
		gst=total*0.18;
    	Totalammount=total+gst;
    }
	printf("\n\n\nGST @18 : Rs. %.2f\n",gst);
    printf("\nTotal Amount: Rs. %.2f\n",Totalammount);
    printf("\n\t 'Visit again' \n");
    printf("_________________________________\n");
	
    return total;
}

int main() 
{
    int ch;
    struct order orders[max_order];
    int count;

    do {
        printf("\n Welcome to SUPERMEGAMARKET\n");
        printf("1. View list\n");
        printf("2. Take Order\n");
        printf("3. Exit\n");
        printf("Enter Choice: ");
        scanf("%d", &ch);

        switch (ch) 
		{
            case 1:
                displaylist();
                break;
            case 2:
                count=0;
                displaylist();
                takeorder(orders, &count);
                break;
            case 3:
                printf("Thank you! Visit again\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while(ch!=3);

    return 0;
}

