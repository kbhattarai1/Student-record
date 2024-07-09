
#include<iostream.h>
#include<fstream.h>
#include<process.h>
#include<string.h>
#include<iomanip.h>
#include<stdio.h>
#include<conio.h>
#include<time.h>
#include<dos.h>
#include<ctype.h>
#include<graphics.h>
int k=8,n;
char usern[20];
void add_new();
void bbox1();
void edit();
void deleterec();
void search();
void bbox();
void time();
void loading();
void login();
void password();
void user();
int test();
void display();
class stu
{
public:
long int rollno;
int outof;
char name[25],Class[4],grade;
float marks,percent;
void getdata();
void putdata();
int getrno();
void displaybox();
void modify();
}
s1,stud;

void stu::getdata()
{
rollno=marks=outof=0;
textcolor(GREEN);
gotoxy(3,16);
cprintf("Rollno: ");
cin>>rollno;
gotoxy(3,18);
cprintf("Name: ");
gets(name);
gotoxy(3,20);
cprintf("Class: ");
cin>>Class;
gotoxy(3,22);
cprintf("Total Marks: ");
cin>>marks;
gotoxy(3,24);
cprintf("Out of: ");
cin>>outof;
percent=(marks/outof)*100;
if(percent>=75)	grade='A';
else if(percent>=60)
grade='C';
else if(percent>=50)
grade='D';
else if(percent>=40)
grade='E';
else grade='F';
}

void stu::putdata()
{
gotoxy(3,k);
cout<<rollno;
gotoxy(13,k);
cout<<name;
gotoxy(33,k);
cout<<Class;
gotoxy(41,k);
cout<<marks;
gotoxy(49,k);
cout<<outof;
gotoxy(59,k);
cout<<grade;
gotoxy(68,k);
cout<<setprecision(2)<<percent<<"%";
k=k+1;
}

int stu::getrno()
{
return rollno;
}
void stu::displaybox()
{
clrscr();
int i,j,k;

gotoxy(25,1);
cprintf("¯¯¯STUDENT RECORD SYSTEM®®®");
gotoxy(53,49);
cprintf("¯¯¯Made By: ");
textcolor(LIGHTBLUE);
cprintf("AKA");
gotoxy(30,3);
cprintf(" STUDENTS DETAILS ");
textcolor(WHITE);

gotoxy(4,5);
textcolor(GREEN);
cprintf("ROLL NO");
gotoxy(12,4);
textcolor(WHITE);

gotoxy(14,5);
textcolor(GREEN);
cprintf("NAME OF STUDENT");
gotoxy(30,4);
textcolor(WHITE);

gotoxy(32,5);
textcolor(GREEN);
cprintf("CLASS");
gotoxy(38,4);
textcolor(WHITE);

gotoxy(40,5);
textcolor(GREEN);
cprintf("MARKS");
gotoxy(46,4);
textcolor(WHITE);

gotoxy(48,5);
textcolor(GREEN);
cprintf("OUT OF");
gotoxy(55,4);
textcolor(WHITE);

gotoxy(57,5);
textcolor(GREEN);
cprintf("GRADE");
gotoxy(63,4);
textcolor(WHITE);
gotoxy(66,5);
textcolor(GREEN);
cprintf("PERCENTAGE");
gotoxy(78,4);
textcolor(WHITE);
 }
void stu::modify()
{
textcolor(RED);
gotoxy(3,16);
cprintf("Rollno: ");
cout<<rollno<<endl;
gotoxy(3,17);
cprintf("Name: ");
cout<<name<<"\t";
cprintf("Class: ");
cout<<Class<<"\t";
cprintf("Marks: ");
cout<<marks<<"\t";
cprintf("Percent: ");
cout<<percent<<endl;
gotoxy(3,18);
cprintf("Enter new details:");
cout<<endl;
char nm[20]=" ",Cl[4]=" ";
float npercent,noutof,mks;
gotoxy(3,19);
cprintf("New Name :(Enter '.' to retain old one) ");
cin>>nm;
gotoxy(3,20);
cprintf("New Class :(Enter '.' to retain old one) ");
cin>>Cl;
gotoxy(3,21);
cprintf("New Marks :(Enter '-1' to retain old one) ");
cin>>mks;
gotoxy(3,22);
cprintf("Out of :(Enter '-1' to retain old one) ");
cin>>noutof;
if(strcmp(nm,".")!=0)	{strcpy(name,nm);}
if(strcmp(Cl,".")!=0)	{strcpy(Class,Cl);}
if(mks!=-1)	{marks=mks;}
if(noutof!=-1)	{outof=noutof;}
percent=(marks/outof)*100;
{
	if(percent>=75)	grade='A';
	else if(percent>=60)	grade='C';
	else if(percent>=50)	grade='D';
	else if(percent>=40)	grade='E';
	else grade='F';
}
}
//*******************************************************************************************//
void main()
{  clrscr();
password();
bbox1();
loading();
clrscr();
bbox();
login();
user();
int ch;
char ch2;
menu:
{
time();
gotoxy(26,9);	textcolor(YELLOW+RED);
cprintf("STUDENT INFORMATION PROGRAM");
textcolor(YELLOW);
gotoxy(35,14);
cprintf("1.Add new");
gotoxy(35,16);
cprintf("2.Edit");
gotoxy(35,18);
cprintf("3.Search");
gotoxy(35,20);
cprintf("4.Display");
gotoxy(35,22);
cprintf("5.Delete");
gotoxy(35,24);
cprintf("6.Exit");
textcolor(MAGENTA+YELLOW);
gotoxy(37,29);
cprintf(
"Enter your choice: ");
cin>>ch;
clrscr();
time();
textcolor(6);
gotoxy(26,9);
cprintf("STUDENT INFORMATION PROGRAM");
switch(ch)
{
case 1:add_new();
break;
case 2:edit();
break;
case 3:search();
break;
case 4:display();
break;
case 5:deleterec();
break;
case 6:exit(0);
break;
default :gotoxy(30,31);
	 cout<<"Wrong option. Try right one.";
	  delay(500);
	  break;
}
clrscr();
bbox1();
user();
goto menu;
}
}

void add_new()
{
time();
bbox1();
user();
ifstream fi("stu.txt",ios::in|ios::app);
ofstream fo("temp.txt",ios::out|ios::app);
char last='y';
gotoxy(3,14);
textcolor(GREEN);
cprintf("Enter the details of student:");
s1.getdata();
k=8;
n=test();
if(n==0)
{
fo.write((char*) &s1, sizeof(s1));
}
else
{
for(int i=1;i<=n;i++)
{
fi.read((char*) &stud, sizeof(stud));
if(s1.getrno()<=stud.getrno())
{
fo.write((char*) &s1, sizeof(s1));
last='n';
break;}

else
fo.write((char*) &stud, sizeof(stud));
}
}
if(last=='y')
fo.write((char*)&s1,sizeof(s1));
else if(!fi.eof())
{
while(!fi.eof())
{
fi.read((char*)&stud,sizeof(stud));

fo.write((char*)&stud, sizeof(stud));
}
}
fi.close();
fo.close();
remove("stu.txt");
rename("temp.txt","stu.txt");
gotoxy(3,26);
cprintf("Information editted.");
delay(100);
clrscr();
s1.displaybox();
k=8;
n=test();
if(n==0)
{
cprintf("\n FILE IS EMPTY ! ");
delay(100);
return;
}
for(int i=1;i<=n;i++)
{
if(fi.eof())
break;
{
fi.read((char*) &stud,sizeof(stud));
s1.putdata();
}
}
getch();
fi.close();
}

//*****************************************************************************//
void edit()
{
time();
bbox1();
user();
textcolor(BLACK);
long rn;
int n,i;
char found='f';
     ifstream fin;
     ofstream fout;
     fin.open("stu.txt");
     if(fin.fail())
       {
	 cout<<"\n FILE NOT FOUND !";
	 fout.close();
	 exit(-1);
       }
    fout.open("temp.txt");
    n=test();
    if(n==0)
      {
	cout<<"\n FILE IS EMPTY ! ";
	getch();
	return;
      }
   while(fin.good())
      {
	fin.read((char*)&s1,sizeof(s1));
	fout.write((char*)&s1,sizeof(s1));
      }
   fin.close();
   fout.close();
   fout.open("stu.txt",ios::trunc);
   fin.open("temp.txt");
   if(fin.fail())
     {
      cout<<"\n FILE NOT FOUND !";
      exit(-1);
     }
   char ch; long pos;
   gotoxy(3,13);
   cout<<"ENTER ROLL NUMBER to be editted:";
   cin>>rn;
  for(i=0;i<n;i++)
	{
	pos=fin.tellg();
	   fin.read((char*)&s1,sizeof(s1));
	   char d;
	   if(s1.getrno()==rn)
	      {
		s1.modify();
		fin.seekg(pos);
		fout.write((char*)&s1,sizeof(s1));
		found='t';
		break;
	      }

	}
   fout.close();
   fin.close();
if(found=='f')
gotoxy(30,30);
       {
       cout<<"Record not found !!";
	delay(100);
	}
display();
}
//*******************************************************************************************//
void search()
{
time();
bbox1();
user();
int rn;
char found='n';
fstream fi("stu.txt",ios::in|ios::out);
fi.open("stu.txt",ios::in|ios::out);
gotoxy(3,14);	textcolor(GREEN);
cprintf("Enter the roll number to searched for: ");
cin>>rn;
n=test();
if(n==0)
{
clrscr();
	textcolor(GREEN);
	cprintf(" FILE IS EMPTY ! ");
	getch();
	return;
}
k=8;
s1.displaybox();
for(int i=1;i<=n;i++)
{
fi.read((char*) &s1, sizeof(s1));
	if(s1.getrno()==rn)
	{
	s1.putdata();
		found='y';
		getch();
		break;
	}
}
if(found=='n')
{
gotoxy(25,31);
cprintf("Rollno not found in file!");
cout<<endl;
getch();
}
fi.close();
}
//*******************************************************************************************//
void deleterec()
{
time();
bbox1();
user();
ifstream fio("stu.txt",ios::in);
ofstream file("temp.txt",ios::out);
int rno;
char found='f',confirm='n';
gotoxy(3,14);
textcolor(GREEN);
cprintf("Enter the rollno of student whose record is to be deleted: ");
cin>>rno;
n=test();
if(n==0)
{
clrscr();
	textcolor(GREEN);
	cprintf(" FILE IS EMPTY ! ");
	getch();
	return;
}
for(int i=1;i<=n;i++)
{
	fio.read((char*) &s1, sizeof(s1));
	if(s1.getrno()==rno)
	{
		k=8;	s1.displaybox();
		s1.putdata();
		found='t';
		gotoxy(3,25);
		cprintf("Are you sure you want to delete this record? (Y/N)");
		cin>>confirm;
		if(confirm=='n')
		file.write((char*)&s1,sizeof(s1));
	}
	else
		file.write((char*)&s1,sizeof(s1));
}
fio.close();
file.close();
remove("stu.txt");
rename("temp.txt","stu.txt");
fio.open("stu.txt",ios::in);
stud.displaybox();
if(found=='f')
{gotoxy(40,40);
cprintf("Record not found!!");}
n=test();
for(i=1;i<=n;i++)
{
	fio.read((char*) &stud,sizeof(stud));
	stud.putdata();
}
getch();
fio.close();
}

void display()
{ifstream fin;
     int n,j;
     fin.open("stu.txt");
     clrscr();
time();
stud.displaybox();
if(n==0)
{
clrscr();
textcolor(GREEN);
	cprintf(" FILE IS EMPTY ! ");
getch();
return;
}
k=8;
n=test();
for(j=0;j<n;j++)
{
fin.read((char*)&stud,sizeof(stud));
gotoxy(3,k);
cout<<stud.rollno;
gotoxy(13,k);
cout<<stud.name;
gotoxy(33,k);
cout<<stud.Class;
gotoxy(41,k);
cout<<stud.marks;
gotoxy(49,k);
cout<<stud.outof;
gotoxy(59,k);
cout<<stud.grade;
gotoxy(68,k);
cout<<setprecision(2)<<stud.percent<<"%";
k+=1;
}
      fin.close();
      getch();
}
//*******************************************************************************************//
void password()
{
char ch[4],ch1,temp;
int i;
textcolor(YELLOW+123);
time();	gotoxy(27,17);
cprintf("ENTER USER PASSWORD: ");
textcolor(6);
textcolor(YELLOW);
gotoxy(48,17);
cprintf("¨¨¨¨");
gotoxy(48,17);
for(i=0;i<4;)
{
temp=getch();
if((temp>='a' || temp>='A') && (temp<='z' || temp<='Z'))
{
ch[i]=temp;
cprintf("*");
i++;
}
}
getch();
if(ch[0]=='h' && ch[1]=='i'&&ch[2]=='t'&&ch[3]=='e')
{
gotoxy(20,18);
textcolor(GREEN);
cprintf("The entered password is correct.");
delay(50);
}
else
{
gotoxy(16,19);
textcolor(RED);
cprintf("The entered password is not coorect, TRY AGAIN !");
  gotoxy(34,21);
puts("Aborting....");
delay(2000);
exit(0);
}	clrscr();
}
void login()
{
int l,hl;
textcolor(GREEN);
gotoxy(27,8);
cprintf("Enter the user name: ");
cin.getline(usern,20);
l=strlen(usern);
hl=l/2;
for(int i=0;i<l;i++)
{
usern[i]=toupper(usern[i]);
}
gotoxy(27,3);
textcolor(6);
gotoxy(21,3);
cprintf("ÉÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍ»");
gotoxy(21,4);
cprintf("º");
textcolor(5);
cprintf("°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°");
textcolor(6);
cprintf("º");
gotoxy(19,5);
cprintf("  º");
textcolor(5);
cprintf("°°°°°°°°°°°°°°");
textcolor(3);
cprintf("LOGIN");
textcolor(5);
cprintf("°°°°°°°°°°°°°°°°");
textcolor(6);
cprintf("º");
gotoxy(21,6);
cprintf("º");
textcolor(5);
cprintf("°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°");
textcolor(6);
cprintf("º");
gotoxy(21,7);
cprintf("ÈÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍ¼");
gotoxy(40-hl-4,5);
cprintf("USER: ");
textcolor(4+123);
cprintf(usern);
gotoxy(27,8);cprintf("                                                 ");
}

void user()
{
int l,hl;
textcolor(6);
gotoxy(21,3);
cprintf("ÉÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍ»");
gotoxy(21,4);
cprintf("º");
textcolor(5);
cprintf("°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°");
textcolor(6);
cprintf("º");
gotoxy(19,5);
cprintf("  º");
textcolor(5);
cprintf("°°°°°°°°°°°°°°");
textcolor(3);
cprintf("     ");
textcolor(5);
cprintf("°°°°°°°°°°°°°°°°");
textcolor(6);
cprintf("º");
gotoxy(21,6);
cprintf("º");
textcolor(5);
cprintf("°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°°");
textcolor(6);
cprintf("º");
gotoxy(21,7);
cprintf("ÈÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍ¼");
gotoxy(40-hl-4,5);
cprintf("USER: ");
textcolor(4+123);
cprintf(usern);
gotoxy(27,8);
cprintf("                                                 ");
}
void loading()
{
textcolor(YELLOW+RED);
gotoxy(3,46);
cprintf("ÉÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍ»");
gotoxy(3,47);
cprintf("º                                                                         º");
gotoxy(3,48);
cprintf("ÈÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍÍ¼");
	for(int i=0;i<73;i++)
{
textcolor(YELLOW+RED);
	gotoxy(i+5,12);
	cprintf("  P R O J E C T   ");
	gotoxy(i+5,14);
	cprintf("           M A D E   B Y :  ");
	gotoxy(i+5,16);
	cprintf("     A     K     A ");
	gotoxy(34,47);
	textcolor(CYAN+RED);
cprintf("Loading...");
cout<<"("<<i+28<<"%)";
gotoxy(4+i,47);
textbackground(BLACK);
textcolor(YELLOW);
cprintf("±");
gotoxy(1,1);
delay(100);
}
}
void bbox()
{


gotoxy(23,1);
textcolor(YELLOW);
cprintf("¯¯¯ STUDNT RECORS SYSTEM ®®®");
gotoxy(52,49);
cprintf("¯¯¯ Made By: ");
textcolor(CYAN);
cprintf("AKA");
}

void bbox1()
{

gotoxy(23,1);
textcolor(YELLOW);
cprintf("¯®STUDENT RECORD SYSTEM®®");
gotoxy(52,49);
cprintf("¯¯¯ Made By: ");
textcolor(CYAN);
cprintf("AKA");
}
int test()    //FIND NO. OF RECORDS
{
int n;
	ifstream fin("stu.txt",ios::in|ios::out);
	fin.open("stu.txt");
	fin.seekg(0,ios::end);
	n=fin.tellg()/sizeof(s1);
	return n ;
}
void time()
{
time_t t;
   time(&t);
   textcolor(GREEN);
   gotoxy(15,11);
   cprintf("Today's Day, Date & Time: ");
   puts(ctime(&t));

}
