#include <iostream>
#include <string>
#include <vector>
using namespace std;

void Exit(); 
void Return();  
void admin();
void user();
int main();
void signUP();
void signIN();
void Book();
void searchBySkill();
void cook();
void display_user();
void food_item();
void membership();

void mainmenu()
{
 
 cout<<endl;
 cout<<"*******************"<<endl;
 cout<<"*   WelCome to Fitbite :Healthy HomeCook Service    *"<<endl;
// cout<<"                       **\t\t\t\t\t"<<endl;
 
 cout<<"*******************"<<endl<<endl;
 cout<<"a::Admin"<<endl;                      
 cout<<"b::User"<<endl;
 cout<<"c::Cook"<<endl;
 cout<<"e:EXIT"<<endl;
 char choice;
 cout<<"Enter choice (Case-Sensitive) ";
 cin>>choice;
 
 switch(choice){ 
  case 'a' :
    admin();                 
    break;
  case 'b':
    user();
    break;
  case 'c':
    cook();
    Return();
    break;
  case 'e':  
    Exit();
    break;
  default:
   {
    cout<<"you enter wrong selection try again"<<endl;
    mainmenu();
   }
  }
}

void Exit()
{
 cout<<endl<<endl<<endl;
 cout<<"\t\t\t\t------------------------ "<<endl;
 cout<<"\t\t\t switching off"<<endl;
}

void Return(){
    cout<<"Do you want to go to main menu? (Y/N)"<<endl;
    char choice1;
    cin>>choice1;
    if (choice1=='y' || choice1=='Y'){
        mainmenu();
    }
    else{
        Exit();
    }
}

void admin(){
    string adminName ="Utsav_05";
    string Name;
    string adminPassword="qwerty";
    string password;
    cout<<"Please Enter Your AdminName :";
    cin>>Name;
    cout<<"Please Enter your Passsword :";
    cin>>password;
    
    if(password==adminPassword && Name==adminName){
        cout<<"A::Display user"<<endl;     
        cout<<"E:Return"<<endl;
        char choice2;
        cin>>choice2;
        if (isalpha(tolower(choice2))){
            switch(choice2){
                case 'e':
                    Return();
                    break;
                    
                case 'a':
                    display_user();
                    Return();
                default:{
                    cout<<"Wrong input try again"<<endl;
                    admin();
                }
            }
        }
    }
    else{
        cout<<"Invalid Input"<<endl;
        mainmenu();                                   
    }
}

void user(){
    cout<<"a::signup"<<endl;                       
    cout<<"b::signin"<<endl;
    cout<<"E:return"<<endl;
    char choice4;
    cin>>choice4;
    if (isalpha(tolower(choice4))){
        switch(choice4){
            case 'a':
                signUP();
                user();
                break;
      
            case 'b':
                signIN();
                break;
      
            case 'e':       
                Return();
                break;
            
            default:
                cout<<"wrong entry"<<endl;
                user();
        }
    }
    else{
        cout<<"you enter wrong input try again"<<endl;
        user();
    }
}

struct User {
    string name;
    string email;
    string password;
};

vector<User> users;

void signUP(){
    
        cout << "Sign Up Page\n";
        User newUser;

        // Prompt the user for their information
        cout << "Name: ";
        cin >> newUser.name;

        cout << "Email: ";
        cin >> newUser.email;

        cout << "Password: ";
        cin >> newUser.password;

        // Store the user's information
        users.push_back(newUser);
        cout<<"Credentials created successfully"<<endl;
} 

void display_user(){
    cout << "\nRegistered Users:\n";
    for (const User& user : users) {
        cout << "Name: " << user.name << "\n";
        cout << "Email: " << user.email << "\n";
    }
}

void signIN(){
    cout << "Welcome to the Sign In Page\n";
    string signInEmail;
    string signInPassword;

    cout << "Enter your email: ";
    cin >> signInEmail;

    cout << "Enter your password: ";
    cin >> signInPassword;

    bool found = false;
    for (const User& user : users) {
        if (user.email == signInEmail && user.password == signInPassword) {
            found = true;
            cout << "Welcome, " << user.name << "!\n";
            Book();
            break;
        }
    }

    if (!found) {
        cout << "Invalid email or password. Please try again.\n";
        user();
    }
}

string toLowercase(const string& input) {
    string result = input;
    for (char& c : result) {
        c = tolower(c);
    }
    return result;
}

struct HouseHelper {
    string name;
    string address;
    string contactNumber;
    string skills;
    string money;
    HouseHelper* next;
    HouseHelper* prev;
};

void searchBySkill(HouseHelper* head, const string& skill) {
    cout << "Search results for skill: " << skill << endl;
    bool found = false;
    HouseHelper* current = head;
    while (current != nullptr) {
        if (toLowercase(current->skills).find(skill) != string::npos) {
            cout << "Name: " << current->name << endl;
            cout << "Address: " << current->address << endl;
            cout << "Contact Number: " << current->contactNumber << endl;
            cout << "Skills: " << current->skills << endl;
            if (skill=="all-rounder"){
                int days,hrs;
                cout<<"Enter the duration for which cook is required(days): ";
                cin>>days;
                cout<<"Enter the hours required per day: ";
                cin>>hrs;
                int g=stoi(current->money);
                cout<<"Your total bill is "<<g*days*hrs<<endl;
                found = true;
                break;
            }
            else{
                cout<<"enter no. hours";
                int h;
                cin>>h;
                int g=stoi(current->money);
                cout<<"Your total bill is "<<g*h<<endl;
                found = true;
                break;
            }
        }
        current = current->next;
    }
    if (!found) {
        cout << "No helpers found with the skill: " << skill << endl;
    }
}

void addHelper(HouseHelper*& head, HouseHelper*& tail, const string& name, const string& address, const string& contactNumber, const string& skills,const string& money) {
    HouseHelper* newHelper = new HouseHelper{name, address, contactNumber, skills, money,nullptr, tail};
    if (tail != nullptr) {
        tail->next = newHelper;
    }
    tail = newHelper;
    if (head == nullptr) {
        head = newHelper;
    }
}
    HouseHelper* head = nullptr;
    HouseHelper* tail = nullptr;

void Book(){
    cout<<"a::Food Item"<<endl;                       
    cout<<"b::Membership"<<endl;
    cout<<"c::signout"<<endl;
    cout<<"E::Exit"<<endl;
    char choice6;
    cin>>choice6;
    if (isalpha(tolower(choice6))){
        switch(choice6){
            case 'a':
                food_item();
                Book();
                break;
      
            case 'b':
                membership();
                Book();
                break;

            case 'c':
                user();
                break;
      
            case 'e':
                Exit();                    
                break;
        }
    }
}

void food_item(){
    cout<<"What food you want your homecook to cook"<<endl;
    cout<<endl;

    cout <<"1.Indian"<<endl;
    cout<<"2.Italian"<<endl;
    cout<<"3.Mexican"<<endl;
    cout<<"4.punjabi"<<endl;
    cout<<"5.SouthIndian"<<endl;
    int choice5;
    cin>>choice5;
    string searchSkill;
    switch(choice5){ 
        case 1 :
            searchSkill="Indian";
            searchBySkill(head, toLowercase(searchSkill));
            break;
        case 2:
            searchSkill="Italian";
            searchBySkill(head, toLowercase(searchSkill));
            break;
        case 3:  
            searchSkill="Mexican";
            searchBySkill(head, toLowercase(searchSkill));
            break;
        case 4:  
            searchSkill="Punjabi";
            searchBySkill(head, toLowercase(searchSkill));
            break;
        case 5:  
            searchSkill="Southindian";
            searchBySkill(head, toLowercase(searchSkill));
            break;
        default:
        {
        cout<<"you enter wrong selection try again"<<endl;
        mainmenu();
        }
    }
}

void membership(){
    string searchSkill;
    searchSkill="All-rounder";
    searchBySkill(head, toLowercase(searchSkill));
}
 
void cook(){
    string name,address,contactNumber,skills,money;
    cout<<"Name: ";
    cin>>name;
    cout<<"Address: ";
    cin>>address;
    cout<<"Contact No.: ";
    cin>>contactNumber;
    cout<<"Skills: ";
    cin>>skills;
    cout<<"Money: ";
    cin>>money;
    addHelper(head,tail,name,address,contactNumber,skills,money);
    
   }

int main() {
    addHelper(head, tail, "John Doe", "123 Main St", "123-456-7890", "Indian","300");
    addHelper(head, tail, "Alice Smith", "456 Elm St", "987-654-3210", "Mexican","800");
    addHelper(head, tail, "Ramlal", "456 Elm St", "987-654-3210", "southinidian","300");
    addHelper(head, tail, "Shamlal", "456 Elm St", "987-654-3210", "punjabi","400");
    addHelper(head, tail, "Sunita", "456 Elm St", "987-654-3210", "italian","700");
    addHelper(head, tail, "Aasha", "456 Elm St", "987-654-3210", "all-rounder","500");
    mainmenu();
    return 0;
}
