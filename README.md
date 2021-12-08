#include<iostream>
using namespace std;

//function declarations
void shop();
void monster();
void battle(int MonsterHealth);

//global variables
string inventory[10] = { "sword" };
int health = 100;
int money = 0;

int main() {
	srand(time(NULL));
	int room = 1;
	string input;
	cout << "You wake up from  " << endl;




	do {
		//set up a visible inventory here as well as a health/money counter
		switch (room) {//Add extra else ifs and rooms to give your player an option to move freely all around your map
		case 1:
			cout << "You are in a room 1. You can go south." << endl;
			cout << "press p for shop" << endl;
			cin >> input;
			if (input == "south")
				room = 2;
			else if (input == "p")
				shop();
			break;
		case 2:
			cout << "You are in room 2. You can go east." << endl;
			cin >> input;
			if (input == "east")
				room = 3;
			else if(input == "north")
				room = 1;
			else
				cout << "sorry not a option." << endl;
			break;
		case 3:
			cout << "You are in room 3. You can go east." << endl;
			cin >> input;
			if (input == "east")
				room = 4;
			else if (input == "west")
				room = 2;
			else
				cout << "sorry not a option." << endl;
			break;
		case 4:
			cout << "You are in room 4. You can go north and south." << endl;
			cin >> input;
			if (input == "west")
				room = 3;
			else if (input == "south")
				room = 6;
			else if (input == "north")
				room = 5;

			else
				cout << "sorry not a option." << endl;
			break;
		case 5:
			cout << "You are in room 5. You can go south." << endl;
			monster();
		//call monster gen in rooms here has to be before cin
			cin >> input;
			if (input == "south")
				room = 4;
			else
				cout << "sorry not a option." << endl;
			break;
		case 6:
			cout << "You are in room 6. You can go south." << endl;
			cin >> input;
			if (input == "south")
				room = 7;
			else if (input == "north")
				room = 4;
			else 
				cout << "sorry not a option." << endl;
			break;
		case 7:
			cout << "You are in room 7. You can go east west and north." << endl;
			cin >> input;
			if (input == "east")
				room = 8;
			else if (input == "west")
				room = 9;
			else if (input == "north")
				room = 6;
			else
				cout << "sorry not a option." << endl;
			break;
		case 8:
			cout << "You are in room 8. You can go west." << endl;
			cin >> input;
			if (input == "west")
				room = 7;
			else
				cout << "sorry not a option." << endl;
			break;
		case 9:
			cout << "You are in room 9. You can go west." << endl;
			cin >> input;
			if (input == "west")
				room = 10;
			else if (input == "east")
				room = 7;
			//MO: add east option
			else
				cout << "sorry not a option." << endl;
			break;
		case 10:
			cout << "you are in room 10. you can go north or east." << endl;
			cin >> input;
			if (input == "north")
				room = 11;
			else if (input == "east")
				room = 9;

			else
				cout << "sorry not a option." << endl;
			break;
		case 11:
			cout << "You won!!" << endl;
			
			break;
			

			//MO: add rooms 10 and 11 here
			return 0;
		}

	} while (input != "q");
}
	

//function definition
	void shop() {
	string input;
	do {
		cout << "Hi! welcome to my shop!" << endl;
		cout << "press p for potion($20), Enter 'k' for key, press 's' for sword." << endl;
		cout << "press 'q' to quit" << endl;
		cin >> input;
		if (input == "p") {//add a money variable so that it checks if you have a sufficient amount of money
			inventory[0] = "potion ";
			money -= 20;
		}
		else if (input == "k") {
			inventory[1] = "key";
		}
		//add else if to put lamp into inventory
		else if (input == "s") {
			inventory[2] = "sword";
		}

	} while (input != "q");
} 

	void monster() {
		int num = rand() % 100 + 1;
		if (num < 20) {
			cout << "a skeleton appears!" << endl;
			health -= 15;
			cout << "a skeleton attacks you" << endl;
			battle(30);
		}
	
        else if (num < 50) {
			cout << "a zombie appears!" << endl;
			num = rand() % 50 + 1;
			cout << "a zombie bites you for num damage" << endl;
			health -= num;
			battle(60);
		}

		else if (num < 75)
			cout << "a spider appears" << endl;
		else
			cout << "no monsters" << endl;

}

	void battle(int MonsterHealth) {
		int damage;
		while (health > 0 && MonsterHealth > 0) {
			//the monster attacks
			damage = rand() % 20;
			cout << "the monster hurts you for" << damage << " damage. " << endl;
			health -= damage;
			if (inventory[4] == "sword") {
				damage = rand() % 60 + 20;
				cout << "you use your sword against the enemy" << endl;
			}
			else {
				damage = rand() % 50 + 10;
				cout << "you beat the monster" << damage << " damage" << endl;
				MonsterHealth -= damage;
			}
			if (MonsterHealth <= 0)
				cout << " you defeated the monster" << endl << endl;
			else cout << "you died" << endl << endl;
		}
	}
