# SuperMarketBillingSystem
#include<iostream>
#include<fstream>

using namespace std;

class shopping
{
	private:
		int pcode;
		float price;
		float discount;
		string pname;
		
		public:
			void menu();
			void administrator();
			void buyer();
			void add();
			void edit();
			void rem();
			void list();
			void receipt();
};

void shopping :: menu()
{
	m:
	int choice;
	string email;
	string password;
	
	cout<<"\t\t\t\t.....................................\t\t\t\t\n";
    cout<<"\t\t\t\t                                     \t\t\t\t\n";
	cout<<"\t\t\t\t      Supermarket Main Menu          \t\t\t\t\n";
	cout<<"\t\t\t\t                                     \t\t\t\t\n";
	cout<<"\t\t\t\t.....................................\t\t\t\t\n";
	cout<<"\t\t\t\t                                     \t\t\t\t\n";
	cout<<"\t\t\t\t   1: Administrator                  \t\t\t\t\n";
	cout<<"\t\t\t\t                                     \t\t\t\t\n";
	cout<<"\t\t\t\t   2: Buyer                          \t\t\t\t\n";
	cout<<"\t\t\t\t                                     \t\t\t\t\n";
	cout<<"\t\t\t\t   3: Exit                           \t\t\t\t\n";
	cout<<"\t\t\t\t                                     \t\t\t\t\n";
	cout<<"\t\t\t\t    Please Select                    \t\t\t\t\n";
	cin >> choice;
	
	switch(choice)
	{
		case 1:
			cout<<"\t\t\t Please Login \n";
			cout<<"\t\t\t enter Email  \n";
			cin>>email;
			cout<<"\t\t\t enter Password \n";
			cin>>password;
			
			if(email  == "dvs@gmail.com"&& password == "dvs123"  )
			{
				administrator();
				
			}
			
			else
			{
				cout<<"\t\t\t Invalid Email / Password \n";
			}
		
		case 2: 
		    {
		    	buyer();
			}
			
		case 3:
			{
				exit(0);
			}
		
		default:
			{
				cout<<"Please Select from the given options \n";
			}
		   
	}
goto m;
}
void shopping :: administrator()
{
	m:
	int choice ;
	cout<<"\n\n\n\t\t\t       Administrator Menu    ";
	cout<<"\n\n\n\t\t\t ......1: Add the product    ";
	cout<<"\n\n\n\t\t\t ......2: Modify the product ";
	cout<<"\n\n\n\t\t\t ......3: Delete the product ";
	cout<<"\n\n\n\t\t\t ......4: Back to the main menu ";
	
	cout<<"\n\n\n\t\t\t Please enter your choice ";
	cin>>choice;
	
	switch(choice)
	{
		  case 1:
		  	add();
		  	break;
		  
		  case 2:
		  	edit();
		  	break;	
		  
		  case 3:
		  	rem();
		  	break;
		   
		  case 4:
		  	menu();
		  	break;
			  		
		  default :
		  	 cout<<" Invalid Choice \n";
	}
	goto m;
}

void shopping :: buyer()
{
	m:
	int choice;
	cout<<"\t\t\t    Buyer    \n";
	cout<<"                  \n";
	cout<<"\t\t\t   1: Buy the product         \n";
	cout<<"                  \n";
	cout<<"\t\t\t  2:  Go back                \n";
	cout<<"\t\t\t  Enter your Choice          \n";
	
	cin>>choice;
	
	switch(choice)
	{
		  case 1:
		  	  receipt();
		  	  break;
		  	  
		  case 2:
		  	  menu();
		  	  break;
		  	  
		 default :
		 	  cout<<" Invalid Choice ";
	}
	goto m;
}

void shopping :: add()
{
	m:
	fstream data;    // here we create the class the class name is data
	int c;
	int token =0;
	float p;
	float d;
	string n;
	
	cout<<"\n\n\n\t\t\t  Add New Product";
	cout<<"\n\n\n\t\t\t  Product code of the product";
	cin>>pcode;
	cout<<"\n\n\n\t\t\t  Name of the Product";
	cin>>pname;
	cout<<"\n\n\n\t\t\t  Price of the Product";
	cin>>price;
	cout<<"\n\n\n\t\t\t  Enter the discount";
	cin>>discount;
	
	
	data.open("database.txt" , ios :: in);
	
	if(!data)
    {
    	data.open("database.txt" , ios :: app|ios::out);  // out means to write app means to append
    	data<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<discount<<"\n";
    	data.close();
	}
	
	else
	{
		data>>c>>n>>p>>d;
		
		while(!data.eof())    // eof is the end of the file
		{
			if(c == pcode)
			{
				token++;
			}
			data>>c>>n>>p>>d;
		}
		data.close();
	}
	
	if(token == 1)
	  goto m;
	  
	else
	{
		data.open("database.txt" , ios :: app|ios::out);  // out means to write app means to append
    	data<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<discount<<"\n";
    	data.close();
	}
	
	cout<<"\n\n \t\t Record Inserted !";
}

void shopping :: edit()
{
	fstream data , data1;
	int pkey;
	int token=0;
	int c;
	float p;
	float d;
	string n;
	
	cout<<"\n\n\t\t Modify the record";
	cout<<"\n\n\t\t Product Code : ";
	cin>>pkey;
	
	data.open("database.txt",ios::app|ios::out);
	
	data>>pcode>>pname>>price>>discount;
	while(!data.eof())
	{
		if(pkey==pcode)
		{
			cout<<"\n\n\t\t Product new code";
			cin>>c;
			cout<<"\n\n\t\t Name of the product ";
			cin>>n;
			cout<<"\n\n\t\t Price";
			cin>>p;
			cout<<"\n\n\t\t Discount";
			cin>>d;
			data1<<" "<<c<<" "<<n<<" "<<p<<" "<<d<<"\n";
			cout<<"\n\n\t\t Record edited";
			token ++;
		}
		else
		{
			data1<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<discount<<"\n";
		}
		data>>pcode>>pname>>price>>discount;
	}
	data.close();
	data1.close();
	
	remove("database1.txt");
	rename("database1.txt","database.txt");
	
	if(token == 0)
	{
		cout<<"\n\n Record not found Sorry for the Inconvienece";
	}
}

void shopping :: rem()
{
	fstream data, data1;
	int pkey;
	int token =0;
	cout<<"\n\n\t Delete product";
	cout<<"\n\n\t Product code";
	cin>>pkey;
	data.open("database.txt",ios::in);
	if(!data)
	{
		cout<<"File doesn't exist";
	}
	else
	{
	    data.open("database.txt",ios::app|ios::out);
	    data>>pcode>>pname>>price>>discount;
	    while(!data.eof())	
	    {
	    	if(pcode==pkey)
	    	{
	    		cout<<"\n\n\t Product deleted succesfully";
	    		token++;
			}
			else
		    {
		    	data1<<" "<<pcode<<" "<<pname<<" "<<price<<" "<<discount<<"\n";
	     	}
		    data>>pcode>>pname>>price>>discount;	
		}
		data.close();
		data1.close();
		
		remove("database.txt");
	    rename("database1.txt","database.txt");
	    
	    if(token == 0)
	    {
		    cout<<"\n\n Record not found Sorry for the Inconvienece";
	    }
	}
}

void shopping :: list()
{
	fstream data;
	data.open("database.txt",ios::in);
	cout<<"\n\n\n|......................................................\n";
	cout<<"ProNo\t\t Name \t\t Price \n";
	cout<<"\n\n\n|......................................................\n";
	data>>pcode>>pname>>price>>discount;
	while(!data.eof())
	{
		cout<<pcode<<"\t\t"<<pname<<"\t\t"<<price<<"\n";
		data>>pcode>>pname>>price>>discount;
	}
	data.close();
}

void shopping :: receipt()
{
	fstream data;
	int arrc[100];
	int arrq[100];
	char choice;
	int c = 0;
	float amount = 0;
	float dis = 0;
	float total = 0;
	
	cout<<"\n\n\t\t\t\t\t  RECEIPT ";
	data.open("database.txt",ios::in);
	if(!data)
	{
		cout<<"\n\n Empty database";
	}
	else
	{
		data.close();
		list();
		cout<<"\n.........................................................\n";
		cout<<"\n|                                                        \n";
		cout<<"\n       Please place the order                            \n";
		cout<<"\n|                                                        \n";
		cout<<"\n.........................................................\n";
		do
		{
			m:
			cout<<"n\n Enter the Product code :";
			cin>>arrc[c];
			cout<<"\n\n Enter the Product quantity :";
			cin>>arrq[c];
			for(int i=0;i<c;i++)
			{
				if(arrc[c]==arrc[i])
				{
					cout<<"\n\n Duplicate product code . Please try again !";
					goto m;
				}
			}
			c++;
			cout<<"\n\n Do you want to buy another product ? If YES press y Else NO press n";
			cin>>choice;
		}
		while(choice == 'y');
		cout<<"\n\n\n\t\t\t.......................RECEIPT....................\n";
		cout<<"\n Product No \t Product Name \t Product Quantity \t Price \t Amount with Discount \n";
		
		for(int i=0;i<c;i++)
		{
			data.open("database.txt",ios::in);
			data>>pcode>>pname>>price>>dis;
			while(!data.eof())
			{
				if(pcode == arrc[i])
				{
					
					 amount = price*arrq[i];
					 dis = amount - (amount*dis/100);
					 total = total + dis;
					 cout<<"\n"<<pcode<<"\t\t"<<pname<<"\t\t"<<arrq[i]<<"\t\t"<<price<<"\t"<<amount<<"\t\t"<<dis;
				}
				data>>pcode>>pname>>price>>dis;
			}
		}
		data.close();
	}
	
	cout<<"\n\n........................................................";
	cout<<"\n Totak Amount :"<<total;
}

int main()
{
	shopping s;
	s.menu();
}
