/*
This program helps customers order custom order from the choices cake, cupcakes, and cookies.
*/





#include <iostream>
#include<iomanip>
#include<vector>
#include<string>
#include<fstream>
void mainMenu();
void priceCake();
void priceCupcake();
void priceCalCookie();
void cakeMenu();
void cupcakeMenu();
void cookieMenu();

using namespace std;

int main() {
	cout << "Hello! Welcome to our intuitive dank baking program!\nWhat would you like today?\n\n";
	mainMenu(); //Calls function for main menu
	return 0;
}



void mainMenu() {    //the main menu of the whole thing//
	int choice;       //the variable for the choice of the item//
	cout << "Please input the number corresponding to the item you would like:\n\n";     //the output so the user knows what number for their order//
	cout << "1)Cake... $49.99 each\n2)Cupcake...$7.00 dozen each\n3)Cookie...$4.99 dozen each\n";
	cin >> choice;
	if (choice >= 1 && choice <= 3) {         //input validation for choices
		if (choice == 1) {                  //different choices with each leading into its own menu
			cakeMenu();                   //menu for cakes
		}
		if (choice == 2) {                  //menu for cupcakes//
			cupcakeMenu();
		}
		if (choice == 3) {
			cookieMenu();                 //menu for cookies//
		}
	}
	else {
		cout << "That is not one of the choices listed!\n"; //will lead back to the main menu if   
		mainMenu();                                       //a choice not listed is chosen
	}
}
void cakeMenu() {    //the menu they get if cake is selected
	ofstream outputFile;
	outputFile.open("dankbakery.txt", ios::app);
	string cakeFlavor, cakeIcing, cakeSpecial, customMessage;    //the different choices that they can use on cake//
	int cakeAmount, choice, response; //saving the choices they make for the cake//
	cout << "Please type in what flavor you would like:\n(We can do anything)\n";
	cin.ignore();
getline(cin,cakeFlavor);
	cout << "Please type in what kind of color icing would you like:\n";
getline(cin,cakeIcing);
	cout << "Would you like to have a custom message on this cake?\n";
	cout << "Please enter 1 for a custom message.\n If not, please input 2 for.\n";
	cin >> response;
	switch (response) {  //switch so that the customer can redo their cake of they made a mistake//
	case 1:
		cout << "Please type in what you would like the custom message to be:\n"; //lets them make a custom message//
		cin.ignore();         //gets the cin to not take the spaces
		getline(cin, customMessage);                       //variable for the message//
		cout << "Your custom message " << customMessage << " Has been saved" << endl;  //Tells them the message has been saved//
		break;
	case 2:
		cout << "There will be no custom message on this cake.\n"; //In case they dont want any message on the cake//
		break;
	default:
		cout << "That is not a listed choice.\n Now reseting your cake choices.\n";
		cakeMenu();   //Brings them back to the orignal menu in case some error has happened//
	}
	cout << "\nWould you like anything extra done to your cake?\n";  //Special request like more icing for example//
	cout << "If so please enter one of the following choices from below. If you prefer nothing extra be done simply type no\n\n"; //Letting them decide any extra things they want//
	cout << "\"Icing\" for extra icing and \"Size\" for the large size, or no: ";
	cin >> cakeSpecial;
	cout << "\n\nYou have selected " << cakeFlavor << " flavor\n";//cake flavor//
	
	cout << "with " << cakeIcing << " colored icing\n"; //icing color//
	
	cout << "and you have " << cakeSpecial << " special order\n";
	outputFile << "Cake ";
	outputFile << "Order: "<<endl<<"	Flavor: "<< cakeFlavor << endl;
	outputFile << "		Icing: " << cakeIcing << endl;
	outputFile <<"		Large/Extra "<<cakeSpecial<<endl;
	outputFile << "		Custom Message: " << customMessage << endl << endl;
	
	
	if (customMessage.empty())  //if the message is empty it will give a different output//
	{
		cout << "with no custom message\n\n";
		priceCake();
		
	}
	else
	{
		cout << "with your custom message being \"" << customMessage << "\"" << endl; //Outputting the custom message they wrote//
		cout << "If this is correct please enter 1 if not please enter 2\n\n";
	}  //Letting them read it all over and see if its correct//
	cin >> choice;
	switch (choice)
	{
	case 1:
		cout << "Thank you, your order has been placed!" << endl;
		priceCake();
		break;
	case 2:
		cout << "We apologize for any inconvenience we will now restart the ordering process" << endl;
		mainMenu(); //starting again if they found any errors//
		break;
	}
	outputFile.close();
}


void cupcakeMenu() {
	string cupcakeFlavor; //all of these variables are for the corresponding part//
	string cupcakeIcing;
	string cupcakeSpecial;
	ofstream outputFile;
	outputFile.open("dankbakery.txt", ios::app);
	int choice; //for the switch statement later on//
	cout << "Please type in what flavor would you like your cupcakes:\n(We can do anything)\n";//deciding the flavor//
	cin.ignore(); //ignoring spaces//
	getline(cin, cupcakeFlavor); //user inputs the flavor//
	cout << "Please type in what color icing would you like:\n"; //asking what icing they want//
	getline(cin, cupcakeIcing);  //inputs icing//
	cout << "Please type in any special requests for your cupcakes.\n If you have none, please enter no.\n";
	getline(cin, cupcakeSpecial);  //inputing the special part of cupcake//
	cout << "You have selected " << cupcakeFlavor << " flavor\n";
	cout << "with " << cupcakeIcing << " colored icing\n";
	cout << "With " << cupcakeSpecial << " (special request)\n";
	cout << "If this is correct please enter 1 if not please enter 2\n\n";
	cin >> choice;  //switch letting them read it all over and restarting if any faults are found//
	outputFile << "Cupcake ";
	outputFile << "Order: "<<endl<<"	Flavor: " << cupcakeFlavor << endl;
	outputFile << "		Icing: " << cupcakeIcing << endl;
	outputFile << "		Special Request: " << cupcakeSpecial << endl;
	switch (choice)
	{
	case 1:
		cout << "Thank you, your order has been placed!" << endl;
		priceCupcake();
		break;
	case 2:
		cout << "We apologize for any inconvenience we will now restart the ordering process" << endl;
		mainMenu();
		break;
	}
	outputFile.close();
}

void cookieMenu() {
	string cookieShape, cookieType, cookieDesigns;  //variables for the corresponding custom cookie parts//
	ofstream outputFile;
	outputFile.open("dankbakery.txt", ios::app);
	int choice; //for the later switch as before//
	cout << "How would you like your cookies shaped?\n";  //outputing asking for their input of cookie shape//
	cin.ignore(); //ignoring spacing on switch//
	getline(cin, cookieShape); //letting them input the cookie shape//
	cout << "Would you like any specific kind of cookie? Chocolate chip, Macademia nut,etc.\n";
	getline(cin, cookieType);
	cout << "Finally would you like any special designs on the cookes?";
	getline(cin, cookieDesigns);
	cout << "\nYou have " << cookieShape << " as cookie shapes\n";
	cout << "with " << cookieType << " as the type of cookie\n";
	cout << "With " << cookieDesigns << " designs\n";
	cout << "If this is correct please enter 1 if not please enter 2\n\n";
	cin >> choice;
	outputFile << "Cookie ";
	outputFile << "Order: "<<endl<<"	Cookie Shape: " << cookieShape << endl;
	outputFile << "		Cookie Type: " << cookieType << endl;
	outputFile << "		Design: " << cookieDesigns << endl;
	switch (choice) //switch after theyve read over their choices that restarts the program if any errors were made//
	{
	case 1:
		cout << "Thank you, your order has been placed!" << endl;
		priceCalCookie();
		break;
	case 2:
		cout << "We apologize for any inconvenience we will now restart the ordering process" << endl;
		mainMenu();
		break;
	}
}
void priceCake() {
	double priceTotal[3] = { 49.99, 7.00, 4.99 };
	cout << "You're total is " << "$" << priceTotal[0];
}
void priceCupcake() {
	double priceTotal[3] = { 49.99, 7.00, 4.99 };
	cout << "You're total is " << "$" << priceTotal[1];
}

void priceCalCookie() {
	double priceTotal[3] = { 49.99, 7.00, 4.99 };
	cout << "You're total is " << "$" << priceTotal[2];

}

