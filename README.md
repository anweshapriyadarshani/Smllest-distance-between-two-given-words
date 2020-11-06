# Smllest-distance-between-two-given-words
Find an efficient algorithm to find the smallest distance (measured in number of words) between any two given words in a string.  For example, given words "hello", and "world" and a text content of "dog cat hello cat dog dog hello cat world", return 1 because there's only one word "cat" in between the two words


#include <bits/stdc++.h> 
#include <sstream> 
using namespace std; 
  
// Function to implement split function 
void split(const string &s, char delimeter,  
                     vector<string> &words) 
{ 
    string token; 
    stringstream tokenStream(s); 
  
    while (getline(tokenStream, token, delimeter)) 
        words.push_back(token); 
} 
  
// Function to calculate the minimum  
// distance between w1 and w2 in s 
int distance(string s, string w1, string w2) 
{ 
    if (w1 == w2) 
        return 0; 
  
    // get individual words in a list 
    vector<string> words; 
    split(s, ' ', words); 
  
    // assume total length of the string  
    // as minimum distance 
    int min_dist = words.size() + 1; 
  
    // traverse through the entire string 
    for (int index = 0; index < words.size(); index++) 
    { 
        if (words[index] == w1) 
        { 
            for (int search = 0;  
                     search < words.size(); search++) 
            { 
                if (words[search] == w2) 
                { 
                    // the distance between the words is  
                    // the index of the first word - the  
                    // current word index 
                    int curr = abs(index - search) - 1; 
  
                    // comparing current distance with  
                    // the previously assumed distance 
                    if (curr < min_dist) 
                        min_dist = curr; 
                } 
            } 
        } 
    } 
  
    // w1 and w2 are same and adjacent 
    return min_dist; 
} 
  
// Driver Code 
int main(int argc, char const *argv[]) 
{ 
    string s = "geeks for geeks contribute practice"; 
    string w1 = "geeks"; 
    string w2 = "practice"; 
    cout << distance(s, w1, w2) << endl; 
    return 0; 
} 
