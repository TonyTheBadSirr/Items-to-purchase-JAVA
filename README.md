# Items-to-purchase-JAVA
Simply add the items name, price, and quantity and allow the online cart simulator to do the rest!

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

package com.Williford;

public class ShoppingCartPrinter {

    String productName = ""; // Instance Variables to set a relationship between products
    double productPrice = 0;
    int productQuantity = 0;



    public static void main(String[] args) {
        ShoppingCartPrinter a = new ShoppingCartPrinter(); // allows access to the above instances, it was used this way
        double cartTotal;   //cartTotal Declaration                           // so the 2nd class can access them easily
        ItemToPurchase item1 = new ItemToPurchase();
        // 1st cart items instance to create different memory locations with the 2nd classes Setters and Getters
        System.out.println("Item 1"); // Displays the first item, and then calls the entered method below
        item1.nameEntry(); //item1 before each method is important as it calls different memory locations
        item1.priceEntry();
        item1.getItemQuantity();

        item1.setName(a.productName); // this sets the system input to a variable to be later accessed, aka initialization
        item1.setPrice(a.productPrice);
        item1.setQuantity(a.productQuantity);

        ItemToPurchase item2 = new ItemToPurchase(); // 2nd cart variable list, add more ass desired


        System.out.println("Item 2");
        item2.nameEntry(); // same as the above instances, and declarations: Calling and recording through the typed methods
        item2.priceEntry();
        item2.getItemQuantity();

        item2.setName(a.productName); // Initializing the 2nd items names to be accessed by the setters and getters
        item2.setPrice(a.productPrice);// from the 2nd class
        item2.setQuantity(a.productQuantity);


        double item1Total = item1.getPrice() * item1.getQuantity(); // this creates a total for item 1, below is item 2
        double item2Total = item2.getPrice() * item2.getQuantity();// add more as desired
        cartTotal = item1Total + item2Total; // self explanatory, this creates the cart total
        double salesTax = 0.07;// change this is accordance to your state, the rest will follow suit
        double totalSalesTax = (cartTotal * salesTax) + cartTotal;
        // this creates the total after sales tax
        System.out.println("BASE COST"); // displays text, and presents the above variables
        item1.printItemPurchase(item1.getPrice(),item1.getName(),item1.getQuantity());
        System.out.println();// creates a new line, as the above cannot have \n due to the parameters
        item2.printItemPurchase(item2.getPrice(),item2.getName(),item2.getQuantity());
        System.out.println();

        System.out.println("Sub-Total: $" + cartTotal + "\n"); //subtotal
        System.out.println("Total tax: " + (totalSalesTax - cartTotal)); // total tax of the cart
        System.out.println("CART TOTAL: " + totalSalesTax);// total cost with tax included


    }
}

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

package com.Williford;
import java.util.Scanner;
public class ItemToPurchase {
    private String itemName; // these are declared variables to be initialized later
    private double itemPrice;
    private int itemQuantity;

    Scanner scnr = new Scanner(System.in); // system input aka scanner
    ShoppingCartPrinter firstCart = new ShoppingCartPrinter(); // this creates a link to the first classes variables


    public void setName(String itemName) {
        this.itemName = firstCart.productName;
     // this sets the item name, and changes per use of declared transforming to initialized
        // Basically it is taking the initialized variables from the 1st class and puts the memory in this location to be used
    }

    public void setPrice(double itemPrice) {
        this.itemPrice = firstCart.productPrice;
        // mimics the names procedure except, this is a double not a string, a primitive not an object
    }

    public void setQuantity(int itemQuantity) {
        this.itemQuantity = firstCart.productQuantity;
        // this is another primitive, and relates the quantity from the first class
    }

    public String getName() {
        return itemName;
    } // returns the name when the method is called

    public double getPrice() {
        return itemPrice;
    } // returns the price when the method is called

    public int getQuantity() {
        return itemQuantity;
    } // returns the quantity when the method is called

    public void printItemPurchase(double itemPrice,String itemName,int itemQuantity) { // these parameters control the cart total
        System.out.println(itemQuantity + " " + itemName + " $" + itemPrice +
                " = $" + ( itemPrice * itemQuantity));
    }

    public void priceEntry() { // allows the price input
        try { // uses a try catch to repeat this method any time a line is not inputed correctly
            System.out.println("Enter the item price: ");
            firstCart.productPrice = scnr.nextDouble(); // system input for double
        } catch (Exception invalidInput) {
            System.out.println("That was an invalid input, please try again");
            priceEntry(); // this is part of the catch portion of the try catch, it returns the input to this method

        }
    }

    public void nameEntry() {
        try { // the same as above, if the name is inputted incorrectly, a string in this case, it will repeat the method
            System.out.println("Enter the item name: ");
            firstCart.productName = scnr.nextLine(); // system input for a String
        } catch (Exception invalidInput) {
            System.out.println("That was an invalid input, please try again");
            nameEntry(); // returns to the beginning of the method if an exception is found

        }
    }

    public void getItemQuantity() {
        try { // trys the below
            System.out.println("Enter the item quantity: ");
            firstCart.productQuantity = scnr.nextInt(); // system input for an intenger
        } catch (Exception invalidInput) { //catches the exception, invalidInput is just a declared title to be called
            System.out.println("That was an invalid input, please try again");
            getItemQuantity(); // returns to the beginning of the method if an exception is found
            // you can use the declaration of the exception invalidInput to use a chain such as invalidInput.getMessage()
            // this will display the actual exception message, play around with it to your hearts content!
        }
    }
}
