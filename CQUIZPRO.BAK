/*  C Quiz Project programmed using C with structure, user defined
    validations, button codes.This demonstrate the working as in real
    scenario in which entered data stored in the database and deleted
    according to the need of the user.  */


#include<stdio.h>
#include<conio.h>
#include<graphics.h>
#include<dos.h>


// *********** Prototyping of user-defined funtions *********


void printQuestion(FILE*, struct questions, int, int, char*);
void welcome(void);
void chooseLevel(void);
void WithoutDelay(char);
void previousQuestion(FILE*,int,int,char*);
void nextQuestion(FILE*,int,int,char*);
void fileToOpen(char*);
void scoreBoard(int,int[],char*,int);
void ansSheet(char*);

void editQues(char*);
void addQues(char*);
void delQues(char*);
int validationCheck(char[],int,char*);
void repeatEditing(char*);
void adminBlock(void);

// ******* Declaring Structure ifno with a variable  *********

struct questions{
     char ques[200];
     char options[4][200];
     char ans;
     char description[300];
}q1,q2,q3;

// ******* Global Declarations **********

char* level;

// ***********Starting of Main Function.************

void main(){
  char c;
  clrscr();
  welcome();
  chooseLevel();
}

void fileToOpen(char* c){
   static int count=1;
   int temp=0;
   struct questions q1;
   FILE* fp = fopen(c,"ab+");
   while( (fread(&q1,sizeof(q1),1,fp)>0) )
      ++temp;
   temp=(temp*sizeof(q1));
   fseek(fp,0,0);
   fread(&q1,sizeof(q1),1,fp);
   printQuestion(fp, q1,temp,count,c);
}

void previousQuestion(FILE* fp,int temp, int count, char* c){
    struct questions q1;
    if( ftell(fp)!= sizeof(q1) ){
       fseek(fp, ftell(fp)-2*(sizeof(struct questions)), 0);
    }
    else{
       fseek(fp, ftell(fp)-sizeof(struct questions), 0);
    }
    fread(&q1,sizeof(q1),1,fp);
    gotoxy(5,26);
    printf("%d", ftell(fp) );
    printQuestion(fp, q1, temp, count, c);
}

void nextQuestion(FILE* fp,int temp, int count, char* c){
      struct questions q1;
      if( ftell(fp)==temp ){
	 --count;
	 fseek(fp, ftell(fp)-sizeof(struct questions), 0);
      }
      fread(&q1,sizeof(q1),1,fp);
      printQuestion(fp, q1,temp,count,c);
}
void editQues(char* fileToOpen){
       int i;
       char k;
       char actualPass[20]="SK.Jain";
       char passEntered[20]="";
       gotoxy(5,18);
       printf("Press Esc to return back to admin block");
       gotoxy(3,7);
       printf("Right password - SK.Jain "); // Password to enter the admin block
       gotoxy(3,3);
       printf("Enter the privacy code:");
       for( i=1;i<=20;i++ ){
	  k=getch();
	  if( k==27 ){                // For escape key
	     clrscr();
	     adminBlock();
	  }
	  else if( k==13 ){           // For enter key
	     break;
	  }
	  else if( k==20 ){
	     --i;
	     continue;
	  }
	  else if( k==8 ){            // For backspace key
	  i=i-2;
	  while(i>-1){
	    printf("\b \b");
	    passEntered[i]='\0';
	    break;
	    }
	  }
	  else{
	     strncat(passEntered,&k,1);
	     printf("*");
	  }
       }
       if( strcmp(passEntered,actualPass) ){
	  gotoxy(3,5);
	  printf("You entered: ");
	  puts(passEntered);
	  gotoxy(32,14);
	  printf("--Wrong password--");
	  gotoxy(48,18);
	  printf("Press R to re-enter the password");

	  label1:

	  k=getch();
	  if( k=='r'||k=='R' ){
	     clrscr();
	     editQues(fileToOpen);
	  }
	  else if( k==27 ){
	     clrscr();
	     chooseLevel();
	  }
	  else{
	     goto label1;
	  }
       }
       else{
	  clrscr();

	  label:

	  gotoxy(28,4);
	  printf("Welcome to the admin block");
	  gotoxy(4,6);
	  printf("_____________________________________________________________________________");
	  gotoxy(24,12);
	  printf("->Press A to add questions\t\t");
	  gotoxy(24,14);
	  printf("->Press D to delete questions");
	  gotoxy(24,16);
	  printf("->Press Esc to return to the main menu");
	  gotoxy(39,20);
	  k=getch();
	  if( k=='a' || k=='A' ){
	    clrscr();
	    addQues(fileToOpen);
	  }
	  else if( k=='d' || k=='D' ){
	    clrscr();
	    delQues(fileToOpen);
	  }
	  else if( k==27 ){             // For escape key
	    clrscr();
	    chooseLevel();
	  }
	  else{
	    gotoxy(30,20);
	    printf("Invalid key pressed");
	    delay(800);
	    clrscr();
	    goto label;
	  }
      }
}
void addQues(char* fileToOpen){
       struct questions q1;
       FILE* fp;
       int i, n;
       char k;
       fp = fopen(fileToOpen, "ab+");
       if( fp==NULL ){
	  printf("File is not opened");
	  exit(1);
       }
       gotoxy(1,4);
       printf("\t\t\tImportant things to remember:");
       printf("\n\n* Size of question and description should be more then 10 characters.");
       printf("\n* Ans should be of single character.");
       printf("\n* Neither of the field should be empty.");
       gotoxy(13,18);
       printf("Press Enter to start\t\t");
       printf("Press D to delete question");
       gotoxy(25,21);
       printf("Press Esc to go back to main menu");
       k=getch();
       if( k=='d'||k=='D' ){
	  clrscr();
	  delQues(fileToOpen);
       }
       else if( k==27 ){           // For escape key
	  clrscr();
	  editQues(fileToOpen);
       }
       else if( k==13 ){           // For enter key
	  clrscr();
	  gotoxy(1,18);
	  printf("Press Esc to go back");
	  gotoxy(1,3);
	  printf("Enter the questions: ");
	  n=validationCheck(q1.ques,sizeof(q1.ques),fileToOpen);
	  if( n<=10 ){
	     printf("\n\nInvalid question");
	     delay(2000);
	     clrscr();
	     addQues(fileToOpen);
	  }
	  printf("\n\nEnter the options:");
	  for( i=0;i<4;i++ ){
	      n=validationCheck(q1.options[i],sizeof(q1.options),fileToOpen);
	      if( n<=0 ){
		 printf("\n\nInvalid option");
		 delay(2000);
		 clrscr();
		 addQues(fileToOpen);
		 }
	      printf("\n");
	  }
	  printf("\nEnter the correct ans for that question: ");
	  scanf("%c",&q1.ans);
	//
	  printf("%d", q1.ans);
	  if( q1.ans!='a' && q1.ans!='A' && q1.ans!='b' && q1.ans!='B'&& q1.ans!='c' && q1.ans!='C'&& q1.ans!='d' && q1.ans!='D' ){
	      printf("\n\n\t\t\t\tInvalid Ans");
	      delay(1000);
	      clrscr();
	      addQues(fileToOpen);
	  }

	  fflush(stdin);
	  printf("\n\nEnter the description for the question: ");
	  n=validationCheck(q1.description,sizeof(q1.description),fileToOpen);
	  if( n<=10 ){
	     printf("\n\nInvalid option");
	     delay(2000);
	     clrscr();
	     addQues(fileToOpen);
	  }
	  if ( fwrite(&q1, sizeof(q1), 1, fp) == 1 ){
	     gotoxy(25,18);
	     printf("Question added successfully :)");
	     repeatEditing(fileToOpen);
	  }
	  else{
	     gotoxy(20,18);
	     printf("ERROR : Sorry, Something went wrong. Try Again :(");
	  }
	  getch();
	  exit(0);
       }
       else{
	  gotoxy(25,14);
	  printf("Wrong key pressed");
	  delay(1000);
	  addQues(fileToOpen);
       }
}
int validationCheck(char string[], int size,char* fileToOpen){
   int j, count=0;
   char k;
   for( j=1;j<=size;j++ ){
	  k=getch();
	  if( k==27 ){                 // For escape key
	     clrscr();
	     addQues(fileToOpen);
	  }
	  else if( k==13 ){           // For enter key
	     return count;
	  }
	  else if( k==20 ){           // For capslock key
	     --j;
	     continue;
	  }
	  else if( k==8 ){            // For backspace key
	  j=j-2;
	  while(j>-1){
	    printf("\b \b");
	    string[j]='\0';
	    break;
	    }
	  }
	  else{
	     strncat(string,&k,1);
	     printf("%c",k);
	     count++;
	  }
       }
       return count;
}

void delQues(char *fileToOpen){
      int count=0,quesToDel;
      char k;
      FILE *temp, *fp;
      fp = fopen(fileToOpen, "ab+");

      gotoxy(15,12);
      printf("Press Enter to start\t\t");
      printf("Press A to add question");
      gotoxy(25,14);
      printf("Press Esc to go back to main menu");
      k=getch();
      if( k=='a' || k=='A' ){
	 clrscr();
	 addQues(fileToOpen);
      }
      else if( k==27 ){
	 clrscr();
	 editQues(fileToOpen);
      }
      else if( k==13 ){
	 clrscr();
	 gotoxy(4,9);
	 printf("__________________________________________________________________________");
	 gotoxy(25,13);
	 printf("---Press Esc to go back else continue---");
	 gotoxy(4,17);
	 printf("__________________________________________________________________________");
	 k=getch();
	 if( k==27 ){
	    clrscr();
	    delQues(fileToOpen);
	 }
	 else{
	   clrscr();
	   gotoxy(3,3);
	   printf("Enter the number of question which you to delete:");
	   scanf("%d", &quesToDel);
	   temp=fopen("dummy.txt","ab+");
	   if( temp==NULL ){
	      printf("File is not opened");
	      exit(1);
	      }

	   while( (fread(&q2,sizeof(q2),1,fp)>0) ){
	      ++count;
	     if(count==quesToDel)
		continue;
	     else
		fwrite(&q2,sizeof(q2),1,temp);
	     }
	    fclose(fp);
	    fclose(temp);
	    remove(fileToOpen);
	    rename("dummy.txt",fileToOpen);
	    gotoxy(25,12);
	    printf("Question deleted successfully");
	    repeatEditing(fileToOpen);
	 }
     }
	else{
	  gotoxy(28,15);
	  printf("Invalid key pressed");
	  delay(1000);
	  clrscr();
	  delQues(fileToOpen);
	}

}
void repeatEditing(char* fileToOpen){
	  char k;
	  delay(1500);
	  clrscr();
	  gotoxy(4,5);
	  printf("__________________________________________________________________________");
	  gotoxy(12,9);
	  printf("Press A to add question\t\t");
	  printf("Press D to delete question");
	  gotoxy(30,13);
	  printf("Press any other key to stop editing");
	  gotoxy(4,18);
	  printf("__________________________________________________________________________");

	  k=getch();
	  if( k=='a' || k=='A' ){
	     clrscr();
	     addQues(fileToOpen);
	  }
	  else if( k=='d' || k=='D' ){
	     clrscr();
	     delQues(fileToOpen);
	  }
	  else{
	     exit(0);
	  }
}
void printQuestion( FILE* fp, struct questions q1, int temp, int count, char* c){
   static int score[20]={0};
   char k, q;
   clrscr();
   gotoxy(35,3);
   printf("%s", level);
   gotoxy(5,4);
   printf("___________________________________________________________________________");
   gotoxy(4,7);
   printf("%d.)",count);
   printf("  %s\n", q1.ques);
   gotoxy(7,10);
   printf("%s\n", q1.options[0]);
   gotoxy(7,11);
   printf("%s\n", q1.options[1]);
   gotoxy(7,12);
   printf("%s\n", q1.options[2]);
   gotoxy(7,13);
   printf("%s\n", q1.options[3]);

   gotoxy(8,21);
   printf("Press 'P' for previous ques\t\t");
   printf("Press 'N' for next ques");
   gotoxy(26,23);
   printf("--Press Esc to change level--");
   gotoxy(25,25);
   printf("Press S to go to the score board");
   gotoxy(3,16);
   printf("Ans: ");

   while(1)
   {
     k=getch();
     if( k=='a' || k=='A' || k=='b' || k=='B' || k=='c' || k=='C' || k=='d' || k=='D'){
	printf(" %c", k);

	if( k==q1.ans )
	   score[count]=1;
	else
	   score[count]=0;

	printf("  ( Press C to change the option )");
	q=getch();
	if( q=='c' ){
	   clrscr();
	   printQuestion(fp, q1, temp, count, c);
	}
	else if( q=='s' || q=='S' ){
	   clrscr();
	   scoreBoard(count,score,c,temp);
	}
	else if( q=='n' || q=='N' ){
	   ++count;
	   nextQuestion(fp,temp,count,c);
	}
	else if( q=='p' || q=='P' ){
	   --count;
	   previousQuestion(fp,temp,count,c);
	}
	else if( k==27 ){
	   clrscr();
	   chooseLevel();
	}
	else{
	   printf("Invalid option");
	   delay(500);
	   clrscr();
	   printQuestion(fp, q1, temp, count, c);
	}
     }
     else if( k=='n' || k=='N' ){
	++count;
	nextQuestion(fp,temp,count,c);
     }
     else if( k=='p' || k=='P' ){
	if(count!=1)
	  --count;
	previousQuestion(fp,temp, count, c);
	break;
     }
     else if( k=='s' || k=='S' ){
	   clrscr();
	   scoreBoard(count,score,c,temp);
	}
     else if( k==27 ){
	   clrscr();
	   chooseLevel();
     }
     else{
	printf("Invalid option");
	delay(500);
	clrscr();
	printQuestion(fp, q1, temp, count, c);
     }
   }
}

void scoreBoard(int count, int score[], char* c, int temp){
   int i, marks=0;
   char k;
   temp=temp/sizeof(q1);
   for( i=1;i<=count;i++){
      if( score[i]==1 )
	 marks++;
   }
   gotoxy(32,4);
   printf("Your score is: %d/%d", marks, temp);
   gotoxy(5,6);
   printf("___________________________________________________________________________");
   gotoxy(5,14);
   printf("\tPress Esc to play again\t\t\t");
   printf("Press E to end the Quiz");
   gotoxy(27,17);
   printf("Press S to view the ans sheet");
   gotoxy(40,21);
   k=getch();
   if( k==27 ){
      clrscr();
      chooseLevel();
   }
   else if( k=='s' || k=='S' ){
      clrscr();
      ansSheet(c);
      exit(0);
   }
   else if( k=='e'||k=='E' ){
      exit(0);
   }
   else{
      gotoxy(28,21);
      printf("Invalid key pressed");
      delay(800);
      clrscr();
      scoreBoard(count,score,c,temp);
   }
}
void ansSheet(char* c){
    struct questions q1;
    int count=0;
    char k;
    FILE* fp;
    fp=fopen(c,"rb+");

    while( (fread(&q1,sizeof(q1),1,fp)>0) ){
	gotoxy(20,20);
	printf("-----Press any key to view next question-----");

	count++;
	gotoxy(3,5);
	printf("%d) %s\n", count, q1.ques);
	gotoxy(8,8);
	printf("%s\n", q1.options[0]);
	gotoxy(8,9);
	printf("%s\n", q1.options[1]);
	gotoxy(8,10);
	printf("%s\n", q1.options[2]);
	gotoxy(8,11);
	printf("%s\n", q1.options[3]);
	gotoxy(5,13);
	printf("Correct Ans: %c\n", q1.ans);
	gotoxy(3,16);
	printf("Description: %s\n", q1.description);
	getch();
	clrscr();
    }
    gotoxy(5,8);
    printf("____________________________________________________________________________");
    gotoxy(15,12);
    printf("--- Press Esc to play again else quiz will be terminated ---");
    gotoxy(5,15);
    printf("____________________________________________________________________________");
    k=getch();
    if( k==27 ){
      clrscr();
      chooseLevel();
    }
    else
      exit(0);
}
void chooseLevel(){
  char c;
  gotoxy(37,3);
  printf("C Quiz");
  gotoxy(2,4);
  printf("_____________________________________________________________________________");
  delay(200);
  gotoxy(21,8);
  printf("----- Choose the level for the Quiz -----");
  delay(150);
  gotoxy(28,12);
  printf("-> Press E for easy level");
  gotoxy(28,14);
  printf("-> Press M for medium level");
  gotoxy(28,16);
  printf("-> Press H for hard level");
  gotoxy(28,18);
  printf("-> Press Esc to end the quiz");
  gotoxy(23,21);
  printf("--Press A to go to the admin block--");
  gotoxy(40,24);
  c=getch();
    if( c=='a' || c=='A' ){
	adminBlock();
    }
    else if(c=='e'||c=='E'){
	level =  "C Quiz (Easy)";
	fileToOpen("Easyques.txt");
    }else if(c=='m'||c=='M'){
	level =  "C Quiz (Medium)";
	fileToOpen("Medques.txt");
    }else if(c=='h'||c=='H'){
	level = "C Quiz (Hard)";
	fileToOpen("Hardques.txt");
    }else if( c==27 ){                // For escape key
	exit(0);
    }else{
	gotoxy(34,19);
	printf("Invalid level");
	clrscr();
	chooseLevel();
    }
}
void adminBlock(){
    char c;
    clrscr();
    gotoxy(23,2);
    printf("Enter the level which you want to edit");
    gotoxy(2,4);
    printf("_____________________________________________________________________________");
    delay(150);
    gotoxy(26,10);
    printf("-> Press E for easy level");
    gotoxy(26,12);
    printf("-> Press M for medium level");
    gotoxy(26,14);
    printf("-> Press H for hard level");
    gotoxy(26,16);
    printf("-> Press Esc to go back to main menu");
    gotoxy(34,19);

    c=getch();
    if(c=='e'||c=='E'){
      //	level =  "C Quiz (Easy)";
	clrscr();
	editQues("Easyques.txt");
    }else if(c=='m'||c=='M'){
      //	level =  "C Quiz (Medium)";
	clrscr();
	editQues("Medques.txt");
    }else if(c=='h'||c=='H'){
      //	level = "C Quiz (Hard)";
	clrscr();
	editQues("Hardques.txt");
    }else if( c==27 ){                     // For escape key
	clrscr();
	chooseLevel();
    }else{
	gotoxy(34,19);
	printf("Invalid level");
	delay(800);
	clrscr();
	adminBlock();
    }
}
void welcome(){
 int i;
 for( i=60;i>30;i-=4 ){
   gotoxy(i-1,7);
   printf("____________________");
   gotoxy(i,10);
   printf("Welcome To C Quiz");
   gotoxy(i-1,12);
   printf("____________________");
   delay(200);
   clrscr();
 }
  gotoxy(32,7);
  printf("__________________");
  gotoxy(32,10);

  printf("Welcome To C Quiz");
  gotoxy(32,12);
  printf("__________________");
  gotoxy(30,16);
  printf("Press any key to Start");
  getch();
  clrscr();
}