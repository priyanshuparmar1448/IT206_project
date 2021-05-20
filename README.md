# IT206_project
#include <iostream>
#include <string>
using namespace std;

struct node
{
    string str;
    int data;
    struct node *next;
};

class queue
{
private:
    struct node* front;
    struct node* rear;
public:
    queue();
    void enqueue(int );
    void dequeue();
    void display();
    void add_str(int,string);
};

  queue::queue()
{
    front=NULL;
    rear=NULL;
}

void queue::enqueue(int n)         // to add an element in the queue
{
    if(front==NULL&&rear==NULL)
    {
        struct node *ptr=(struct node *)malloc(sizeof(struct node));
        front=ptr;
        rear=ptr;
        front->data=n;
    }
    else
    {
        node *temp=new node;
        node *pointer;
        pointer=front;
        temp->data=n;
        if(temp->data < pointer->data){
            temp->next=pointer;
            pointer=temp;
        }
        else{
            pointer=pointer->next;
        }
       
    }
}

void queue::dequeue()              // to delete the element in the queue
{
    if(front==NULL&&rear==NULL)
    {
        cout<<"queue is empty\n";
    }
    else if(front!=rear)
    {
        struct node *ptr=front;
        front=front->next;
        free(ptr);
    }
    else
    {
        struct node *ptr=front;
        front=front->next;
        free(ptr);
        front=NULL;
        rear=NULL;
    }
}

void queue::add_str(int n,string str)
{
    struct node *ptr=front;
    while(ptr!=rear)
    {
        if(ptr->data==n)
        {
            ptr->str=str;
        }
        ptr=ptr->next;
    }
    if(rear->data==n){
        rear->str=str;
    }
}

void queue::display()          // the function will display the queue
{
    struct node* ptr=front;
    while(ptr!=rear)
    {
        cout<<ptr->str<<" "<<ptr->data<<"\n";
        ptr=ptr->next;
    }
    cout<<ptr->str<<" "<<ptr->data<<"\n";
}

  int main()
{
    cout<<"give the number of students who takes part in the seat allocation system: ";
    int n;
    cin>>n;
    queue q;
    for(int i=0;i<n;i++){
        cout<<"enter the name of the student: ";
        string str;
        cin>>str;
        cout<<"enter the rank of the student: ";
        int x;
        cin>>x;
        cout<<"line 0\n";
        q.enqueue(x);
        q.add_str(x,str);
    }
    q.display();
    return 0;
}
