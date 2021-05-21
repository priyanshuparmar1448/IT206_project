#include <iostream>
#include <string>
using namespace std;

struct node
{
    string str;
    int data;
    struct node *next;
};

struct coll
{
    string cname;
    int cid;
    int total_seats;
} college[10];

class queue
{
private:
    struct node *front;
    struct node *rear;

public:
    queue();
    void enqueue(int, string);
    string dequeue();
    void display();
    void add_str(int, string);
};

queue::queue()
{
    front = NULL;
    rear = NULL;
}

void queue::enqueue(int n, string name) // to add an element in the queue
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

string queue::dequeue() // to delete the element in the queue
{
    node *ptr = front;
    front = front->next;
    string s = ptr->str;
    return s;
}

void queue::display() // the function will display the queue
{
    struct node *ptr = front;
    while (ptr != rear)
    {
        cout << ptr->str << " " << ptr->data << "\n";
        ptr = ptr->next;
    }
    cout << ptr->str << " " << ptr->data << "\n";
}

int main()
{
    cout << "give the number of students who takes part in the seat allocation system: ";
    int n;
    cin >> n;
    queue q;
    int *arri = new int[n];       //int arri[n];
    string *arrs = new string[n]; //string arrs[n];
    cout << "\n";
    for (int i = 0; i < n; i++)
    {
        cout << "enter the name of the student: ";
        string str;
        cin >> str;
        *(arrs + i) = str;
        cout << "enter the rank of the student: ";
        int x;
        cin >> x;
        *(arri + i) = x;
        cout << "\n";
    }
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (*(arri + i) > *(arri + j))
            {
                int temp = *(arri + i);
                *(arri + i) = *(arri + j);
                *(arri + j) = temp;
                string t = *(arrs + i);
                *(arrs + i) = *(arrs + j);
                *(arrs + j) = t;
            }
        }
    }
    for (int i = 0; i < n; i++)
    {
        int x = *(arri + i);
        string str = *(arrs + i);
        q.enqueue(x, str);
    }
    delete[] arri;
    delete[] arrs;
    q.display();

    cout << "\nRound: 1\nNow we go towards choice filling for each student: \n\n";
    cout << "press 1: for IIT BOMBAY \n";    // 1
    cout << "press 2: for IIT DELHI \n";     // 3
    cout << "press 3: for IIT MADRAS \n";    // 2
    cout << "press 4: for IIT KHARAGPUR \n"; // 5
    cout << "press 5: for IIT GUWAHATI \n";  // 5
    cout << "press 6: for IIT ROORKEE \n";
    cout << "press 7: for IIT HYDERABAD \n";
    cout << "press 8: for IIT KANPUR \n";
    cout << "press 9: for IIT GANDHINAGAR \n";
    cout << "press 10: for IIT JODHPUR \n";

    int a = 0, b = 10;
    college[0].cname = "IIT BOMBAY";
    college[1].cname = "IIT DELHI";
    college[2].cname = "IIT MADRAS";
    college[3].cname = "IIT KHARAGPUR";
    college[4].cname = "IIT GUWAHATI";
    college[5].cname = "IIT ROORKEE";
    college[6].cname = "IIT HYDERABAD";
    college[7].cname = "IIT KANPUR";
    college[8].cname = "IIT GANDHINAGAR";
    college[9].cname = "IIT JODHPUR";

    for (int i = a; i < b; i++)
    {
        college[i].cid = i + 1;
    }
    for (int i = a; i < b; i++)
    {
        college[i].total_seats = rand() % 4;
    }
    //stack s1,s2,s3,s4,s5,s6,s7,s8,s9,s10;
    for (int j = 0; j < n; j++)
    {
        string s = q.dequeue();
        cout << "turn of " << s << "\n";
        cout << "enter the number of choices that you want to fill: ";
        bool count = 1;
        int x;
        cin >> x;
        for (int i = 0; i < x; i++)
        {
            cout << "give the id number of college in filling " << i + 1 << ": ";
            int x1;
            cin >> x1;
            if (college[x1].total_seats && count)
            {
                //s.push(s);
                count = 0;
                cout << "ok done";
                college[x1].total_seats--;
            }
            if (i == x - 1 && count == 1)
            {
                //s.push(x);
                cout << "no";
            }
        }
    }
    cout << "here is the result of Round: 1\n";
    for (int i = a; i < b; i++)
    {
        int y = 101;
        cout << college[i].cname << "\n";
        for (int j = 0; j < college[i].total_seats; j++)
        {
            //string s=s.pop();
            cout << y << ": ";
            //cout<<s<<"\n";
            y++;
        }
    }
    return 0;
}
