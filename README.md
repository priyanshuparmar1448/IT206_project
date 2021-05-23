#include <iostream>
#include <stack>
#include <string>
#include <bits/stdc++.h>
#include<iterator>
#include<algorithm>
using namespace std;

struct student
{
    int rank;
    string name;
};
bool compare(student s1,student s2)
{
    return s1.rank<s2.rank;
}


struct node                        //structure for queue
{
    string str;
    int data;
    struct node *next;
};
class Queue                                   // class for queue
{
private:
    struct node *front;
    struct node *rear;

public:
    Queue();
    void enqueue(int, string);
    string dequeue();
    void display();
};

Queue::Queue()                                // constructor for queue
{
    front = NULL;
    rear = NULL;
}

void Queue::enqueue(int n, string name)              // to add an element in the queue
{
    if (front == NULL && rear == NULL)
    {
        node *ptr = new node;
        front = ptr;
        rear = ptr;
        front->data = n;
        front->str = name;
    }
    else
    {
        node *temp = new node;
        temp->data = n;
        temp->str = name;
        rear->next = temp;
        rear = temp;
    }
}

string Queue::dequeue()                    // to delete the element in the queue
{
    node *ptr = front;
    front = front->next;
    string s = ptr->str;
    return s;
}

void Queue::display()                         // the function will display the queue
{
    node *ptr = front;
    while (ptr != rear)
    {
        cout << ptr->str <<" "<< ptr->data << "\n";
        ptr = ptr->next;
    }
    cout << ptr->str << " " << ptr->data << "\n";
}




class college                                    // college as structure with variables and function
{
public:
    int seats;
    int serial_no;
    string name;
    void push(stack <string> &s,string x);
    void display(stack <string> &s);
    bool isempty(stack <string> &s);
};


void college::push(stack <string> &s,string x)    // function to push the student name into the college stack
{
    if(seats==0)
    {
        cout<<"Sorry no more seats available in this college."<<endl;
    }
    else
    {
        s.push(x);
    }
}

void college::display(stack <string> &s)      // the function to display stack of each college
{
    if(s.empty())
    {
        return;
    }
    string x=s.top();
    cout<< x << endl;
    s.pop();
    display(s);
    s.push(x);
}

bool college::isempty(stack <string> &s)           // function to check the stack is empty or not
{
    if(s.empty())
    {
        return true;
    }
    else
    {
        return false;
    }
}



int main()
{
    cout << "Enter the number of students who want to take part in the Seat Allocation :- ";
    int n;
    cin >> n;
    cout << endl;
    student stud[n];
    for (int i = 0; i < n; i++)
    {
        cout << "Enter the name of the student " << i+1 << " :- ";
        cin >> stud[i].name;
        cout << "Enter the rank of the student " << i+1 << " :- ";
        cin >> stud[i].rank;
        cout <<endl;
    }

    int p=sizeof(stud)/sizeof(stud[0]);
    sort(stud,stud+p,compare);           // std function to sort an array

    Queue q;
    for (int i = 0; i < n; i++)
    {
        int x = stud[i].rank;
        string str = stud[i].name;
        q.enqueue(x, str);                   // allocation of student in the queue with respect to their respective rank
    }

    q.display();             // display the students in the queue

    system("PAUSE");
    system("CLS");

    cout << "\nRound: 1\nNow we go towards choice filling for each student: \n\n";
    cout << "press 1: for IIT Bombay \n";
    cout << "press 2: for IIT Delhi \n";
    cout << "press 3: for IIT Kanpur \n";
    cout << "press 4: for IIT Madras \n";
    cout << "press 5: for IIT Kharagpur \n";
    cout << "press 6: for IIT Jodhpur \n";
    cout << "press 7: for IIT Gandhinagar \n";
    cout << "press 8: for IIT Goa \n";
    cout << "press 9: for IIT Dhanbad \n";
    cout << "press 10: for IIT Roorke \n";

    college clg[10];
    stack <string> st[10];

    clg[0].name="IIT Bombay";
    clg[1].name="IIT Delhi";
    clg[2].name="IIT Kanpur";
    clg[3].name="IIT Madras";
    clg[4].name="IIT Kharagpur";
    clg[5].name="IIT Jodhpur";
    clg[6].name="IIT Gandhinagar";
    clg[7].name="IIT Goa";
    clg[8].name="IIT Dhanbad";
    clg[9].name="IIT Roorke";

    clg[0].seats=4;
    clg[1].seats=0;
    clg[2].seats=2;
    clg[3].seats=5;
    clg[4].seats=1;
    clg[5].seats=3;
    clg[6].seats=0;
    clg[7].seats=4;
    clg[8].seats=2;
    clg[9].seats=5;
    for(int i=0; i<10; i++)
    {
        clg[i].serial_no=i+1;
    }


    for (int j = 0; j < n; j++)
    {
        string s = q.dequeue();                  // to specify the turn of students we do dequeue the name of the student
        cout << endl<< "Turn of " << s << "\n";
        cout << "Enter the number of choices that you want to fill: ";
        int x;
        cin >> x;

        bool count = true;

        int i;
        for (i= 0; i < x; i++)
        {
            cout << "Give the id number of college in filling " << i + 1 << ": ";
            int x1;
            cin >> x1;
            if(clg[x1-1].seats!=0 && count==true)
            {
                count=false;                      // allocation of the college condition
                clg[x1-1].push(st[x1-1],s);
                clg[x1-1].seats--;
            }
        }
        if(i==x && count==true)
        {
            cout<<"Sorry you are not alloted any seat from your choice filling."<<endl;
        }
        if(count==false)
        {
            cout<<"Congratulations!! You are allocated a seat."<<endl;
        }
    }

    system("PAUSE");
    system("CLS");

    cout << "The Results of the Seat Allocation round:-"<<endl<<endl<<endl;
    for (int i = 0; i < 10; i++)                             // one loop for one college
    {
        cout << clg[i].name << " :- \n";
        clg[i].display(st[i]);                          // function displays the names in the stack of that college
        if(clg[i].isempty(st[i])==true)
        {
            cout<<"No student got admission in this college."<<endl;
        }
        cout<<endl;
    }
    return 0;
}
