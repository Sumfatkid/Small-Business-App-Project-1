#include <fstream>
#include <iostream>
#include <string>

using namespace std;

int main(){
  
  ofstream myoutfile("example.txt");
  
  myoutfile << "Writing this to file example.txt." << endl;
  myoutfile << "And also this." << endl;
  myoutfile << "And this." << endl;
  
  myoutfile.close();
  
  
  ifstream myinfile("example.txt");
  
  string line;
  
  while(getline(myinfile,line))
  {
      cout << line << endl;
  }
  
  myinfile.close();  
  
  return 0;
}
