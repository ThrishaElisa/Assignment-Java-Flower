//Program Description : Java program to manage their flower inventory efficiently
//Programmer: Thrisha Yusri
//Date: 19 February 2024
package LAB;

//import scanner package
import java.util.Scanner;
import java.text.DecimalFormat;

//define FlowerShop as the driver class name
public class FlowerShop
{
    public static void main(String[] args){

        Scanner input = new Scanner(System.in);
        DecimalFormat df = new DecimalFormat("0.00");

        int size = 3;
        Flower[] flower = new Flower[size];

        System.out.println("GET USER INPUT FOR 10 FLOWERS");
        System.out.println("--------------------------------------");
        //loop through the size to get user input and store all 10 flower details
        for(int j=0; j < size; j++){
            //get the flower name from user
            System.out.print("Enter the flower name: ");
            String name = input.nextLine();

            //get the flower color from user
            System.out.print("Enter the flower color: ");
            String color = input.nextLine();

            //get the flower price from user
            System.out.print("Enter the flower price: ");
            double price = input.nextDouble();

            //get the flower quantity from user
            System.out.print("Enter the flower quantity: ");
            int quantity = input.nextInt();

            //to avoid it skipping the next input
            input.nextLine();

            //assign the values into the flower class one by one
            flower[j] = new Flower(name, color, price, quantity);
            System.out.print("\n");

        }

        System.out.println("\nDISPLAY ALL FLOWER DETAILS");
        System.out.print("--------------------------------------");
        //display all flower details
        for(int j=0; j < size; j++){
            System.out.print("\n------- Flower "+ (j+1)+"----------\n");
            System.out.print(flower[j].toString());
        }

        System.out.println("\n\n\nDISPLAY TOTAL VALUE OF FLOWER INVENTORY");
        System.out.print("--------------------------------------");
        //calculate and display the total values
        double total =0.0;
        for(int j=0; j < size; j++){
            double price = flower[j].getPrice();
            int quantity = flower[j].getQuantity();

            total = total + (price * quantity);
        }
        //display total values in inventory
        System.out.println("\nTotal values of flower inventory is RM "+df.format(total));
        int i;
        System.out.println("\n\n\nSEARCH FLOWER IN INVENTORY");
        System.out.print("--------------------------------------");
        //ask user which flower that they want to search to look at the details
        System.out.print("\nEnter the flower name that you wish to search (X to exit search function): ");
        String searchName = input.nextLine();
        while(!searchName.equalsIgnoreCase("X")){
            int foundInd = 0;
            boolean found = false;
            i = 0;
            //loop through the array of flowers to find the searched flowe name
            while (!found && i < size) {
                //when flower name is equal to the seach name, display the details
                if(flower[i].getName().equalsIgnoreCase(searchName)){                
                    found = true;
                    foundInd = i;
                }
                i++;
            }
            //if found, display the flower details
            if(found == true){
                System.out.println("\nBelow is the flower details:");
                System.out.print(flower[foundInd].toString());
            }
            else{
                System.out.println("\nUnable to find the flower in inventory.");
            }            
            System.out.print("\nEnter the flower name that you wish to search (X to exit search function): ");
            searchName = input.nextLine();
        }

        System.out.println("\n\n\nRESTOCKING FLOWERS");
        System.out.print("--------------------------------------");
        //ask user if they want to restock?
        System.out.print("\nDo you wish to restock a flower? (Y- yes / N- no): ");
        String restock = input.nextLine();
        while(restock.equalsIgnoreCase("Y")){
            //ask user which flower they want to restock
            System.out.print("\nEnter the flower name that you wish to restock: ");
            String restockName = input.nextLine();
            int foundIndRestock = 0;
            boolean foundRestock  = false;
            i = 0;  
            //search flower to restock
            while (!foundRestock && i < size) {
                if(flower[i].getName().equalsIgnoreCase(restockName)){ 
                    //ask user to enter the number to be restock
                    System.out.print("\nEnter the amount you want to restock: ");
                    int restockAmount = input.nextInt(); 
                    //to avoid it skipping the next input
                    input.nextLine();
                    //add restock number with remaining inventory
                    int newInventory = flower[i].getQuantity()+ restockAmount;                    
                    flower[i].setQuantity(newInventory);
                    foundIndRestock =i;
                    foundRestock = true;
                }
                i++;
            }
            //display new inventory
            System.out.println("\nYou have just restocked the flower: ");
            System.out.print(flower[foundIndRestock].toString());
            
            //ask user if they want to restock other flower
            System.out.print("\nDo you wish to restock a flower? (Y- yes / N- no): ");
            restock = input.nextLine();
            

        }
        
        System.out.print("\n\n*********************************     THANK YOU!   *************************\n");

        System.exit(0);
    }
}
