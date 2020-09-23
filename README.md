<div align="center">

## Daktari


</div>

### Description

I wrote this game in C to help me learn C.

It is a text-based Shoot-em-Up that will go Very fast

so you can play against the speed of the machine.

It was developed in Borland Turbo C/C++ lite (and

may only run/be compatible with that editor).

The text aliens spin and dive in random moves,

The speed of the game increases and the number of

bombs is incremented after each level.

Left and Right SHIFT keys move the ship and CTRL

sends out a stream of missiles to wipe out the attackers!

There is a Hall of Fame which saves as a file.

Plus great sound effects from the PC speaker!

Have fun with it !
 
### More Info
 
Left and Right SHIFT keys move the ship and CTRL

sends out a stream of missiles to wipe out the attackers!

Q quit, S toggle sound


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Jim Cook](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/jim-cook.md)
**Level**          |Beginner
**User Rating**    |5.0 (15 globes from 3 users)
**Compatibility**  |Borland C\+\+
**Category**       |[Games](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/games__3-13.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/jim-cook-daktari__3-722/archive/master.zip)

### API Declarations

```
#include"stdio.h"
#include"conio.h"
#include"bios.h"
#include"stdlib.h"
#include"dos.h"
#include"string.h"
```


### Source Code

```
// Manic Attack or DAKTARI : by J.J.Cook.
#include"stdio.h"
#include"conio.h"
#include"bios.h"
#include"stdlib.h"
#include"dos.h"
#include"string.h"
#define MAXNUMGALS 120
#define MAXNUMMISS 30
#define MAXNUMBOMBS 20
#define RIGHT 0x01
#define LEFT  0x02
#define CTRL  0x04
#define ALT  0x08
float LOOP=15000;
float Count;
float gspeed=4,ovespeed=1,firespeed=1;
float ispeed=2,cgspeed=8,g1speed=2;
float bspeed=2,mspeed=2,sndspeed=1000;
float sspeed=8,espeed=8;
int Numbombs=0,M2,M1,MISS1,CG1,I1,B1,E1,S1;
int Homefactor=1,swoop=50;
int gchar[10]={86,192,60,218,65,191,62,217,32,42};
int galx[MAXNUMGALS], misx[MAXNUMMISS],
  galy[MAXNUMGALS], misy[MAXNUMMISS],
  galc[MAXNUMGALS], bombx[MAXNUMBOMBS],
  galdx[MAXNUMGALS], bomby[MAXNUMBOMBS],
  galdy[MAXNUMGALS], galm[MAXNUMGALS],
  gall[MAXNUMGALS], galsp[MAXNUMGALS], gald[MAXNUMGALS];
int key,a,shipx,shipy,Numgals,xadder=1,newxadder,shipxadder,hits,Sheet;
long Hscore[30],SC,Count2,Score,Highscore;
char Highname[11]="\0";
int fa,Hwave[30];
int Colour[30]={15,1,9,3,11,15,1,9,3,11,15,1,9,3,11,15,1,9,3,11,15,1,9,3,11,15,1,9,3,11};
int Colour1[9]={4,12,6,14,10,2,3,11,15};
char Hname[30][11]={ "....","....","....","....","....",
			  "....","....","....","....","....",
			  "....","....","....","....","....",
			  "....","....","....","....","....",
			  "....","....","....","....","....",
			  "....","....","....","....","...." };
int Gameover,lives;
char Ch,Mov;
long int Delay=1000;
float freq=0,freqadder=0;
int Soundoff=0;
int Tone[9]={ 100,200,300,400,500,600,700,800,900 };
// Moves
char *Moveptr[30];
FILE *Hallfileptr;
char *Pstring[9]={"P","s","y","c","o","s","o","f","t"};
void main()
{
 void Initialise();
 void Game();
 void Scores();
 void Hall();
 void ShowHall();
 for(a=0;a<30;a++)
 {
  Hscore[a]=30000-(a*1000);
 }
 for(a=0;a<9;a++)
 {
  Moveptr[a]=((char*)malloc(41));
 }
 strcpy(Moveptr[0],"0000000000000000000000000000000000000000\0");
 strcpy(Moveptr[1],"0AAAAAAAA765432110777665544332AAAAAAAAAA\0");
 strcpy(Moveptr[2],"0089999999901234567011118221009999999999\0");
 strcpy(Moveptr[3],"AAAAAAAAAA000000000000000000000099999999\0");
 strcpy(Moveptr[4],"0AAAAAAAA765432110777665544332AAAAAAAAAA\0");
 strcpy(Moveptr[5],"0000000999999990110077001100770011107770\0");
 strcpy(Moveptr[6],"2222222222222222222222222222222222222210\0");
 strcpy(Moveptr[7],"777777777666666666667777777777AAAAAAAAAA\0");
 strcpy(Moveptr[8],"44449A444489A9A44449A4444484567012345670\0");
 strcpy(Moveptr[9],"9999999999999999999999999999899AAAAAAAAAA\0");
 strcpy(Moveptr[10],"0000000000000000000000000000009999999999\0");
 strcpy(Moveptr[11],"AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8AA\0");
 strcpy(Moveptr[12],"0123456700000000111111100000009999999999\0");
 strcpy(Moveptr[13],"012345677777777777777777777777AAAAAAAAAA\0");
 strcpy(Moveptr[14],"0765432111111111111111111111115999999999\0");
 strcpy(Moveptr[15],"012345434543454345434543454345670AAAAAAA\0");
 strcpy(Moveptr[16],"0122222222222222222222211110000099999999\0");
 strcpy(Moveptr[17],"00777777777011111111107777777700AAAAAAAA\0");
 strcpy(Moveptr[18],"01233333333345670A99AA99AA99AA99AA99AA90\0");
 strcpy(Moveptr[19],"0101010101010101010101010101010101010101\0");
 strcpy(Moveptr[20],"0909090909090909090909090909090909090909\0");
 strcpy(Moveptr[21],"0A0A0A0A0A0A0A0A0A0A0A0A0A0A0A0A0A0A0A0A\0");
 strcpy(Moveptr[22],"0990990990990990990990990990990990990990\0");
 strcpy(Moveptr[23],"4AA4AA4AA4AA4AA4AA4AA4AA4AA4AA4AA4AA4AA4\0");
 strcpy(Moveptr[24],"6543322111000777666655554444333333222210\0");
 strcpy(Moveptr[25],"1011011100110011000101101011100101010011\0");
 strcpy(Moveptr[26],"7654567076545670765456707654567076545670\0");
 strcpy(Moveptr[27],"7070707077707070070707707707070707070771\0");
 strcpy(Moveptr[28],"7707707007707010101010110101707007011011\0");
 strcpy(Moveptr[29],"1101010101101077070770707070110011010101\0");
 // Load Hall of fame
 fclose(Hallfileptr);
 if((Hallfileptr=fopen("HALL.dat","r"))==NULL)
 {
  printf("File could not be opened");
 }
 else
 {
  fa=0;
  while(fscanf(Hallfileptr,"%ld %d %s",&Hscore[fa],&Hwave[fa],&Hname[fa])!=EOF)
  {
	fa++;
  }
  fclose(Hallfileptr);
  strcpy(Highname,Hname[0]);
  Highscore=Hscore[0];
 }
 textmode(C4350);
 nosound();
 while(Ch!='q' && Ch!='Q')
 {
  gotoxy(30,24);
  textcolor(LIGHTGREEN);
  cprintf("D - A - K - T - A - R - I\r");
  delay(2000);
  Hall();
  {strncpy(Highname,Hname[0],11);}
  clrscr();
  gotoxy(14,26);
  textcolor(LIGHTGREEN);
  cprintf("Press 'Q' to quit or 'H' for Hall or other key for Game\r");
  cprintf("\n\n     Keys: Left / Right SHIFT to move, CTRL to Fire, S Sound On/Off\r");
  Ch=getch();
  Initialise();
  Score=0;
  lives=4;
  Sheet=1;
  LOOP=12000;
  swoop=70; Homefactor=1;
  if(Ch!='q' && Ch!='Q' && Ch!='H' && Ch!='h') {Game();}
  if(Ch=='h' || Ch=='H') {ShowHall();}
 }
}
void Initialise()
{
 // New sheet
 void Ship();
 nosound();
 LOOP=LOOP-500;
 if(LOOP<60) {LOOP=60;} // Max game speed
 if(Sheet==10 || Sheet==15 || Sheet==20 || Sheet==25 || Sheet>30) {lives++;}
 if(Sheet>=25) {lives++;}
 Gameover=0;
 int i,j=10,jf=0,y=3,c=0;
 shipy=45; shipx=40;
 Numgals=MAXNUMGALS;
 if(Sheet++>1) {Score=Score+1000;}
 swoop=swoop-5; if(swoop<1) {swoop=1;}
 Homefactor=Homefactor*5;
 if(Homefactor>10000) {Homefactor=10000;}
 Numbombs++; if(Numbombs>MAXNUMBOMBS) {Numbombs=MAXNUMBOMBS;}
 for(i=0;i<Numgals;i++)
 {
  j=j+4;
  if(j>70-c)
  {
	j=16+c; jf=0; y++; y++; c=c+2;
	if(jf==1) {jf=0; j=j+2;}
	else {jf=1;}
  }
  galx[i]=j;
  galy[i]=y;
  galc[i]=0; galdx[i]=0; galdy[i]=0; gall[i]=2;
 }
 for(i=0;i<MAXNUMMISS;i++)
 {
  misx[i]=98;
 }
 for(i=0;i<MAXNUMBOMBS;i++)
 {
  bombx[i]=99;
 }
 for(i=0;i<MAXNUMGALS;i++)
 {
  galsp[i]=0;
  galm[i]=0;
  gald[i]=0;
 }
 clrscr();
 Ship();
}
void Game()
{
 void Showgals(int);
 void Movegals();
 void Ship();
 void Missiles();
 void Input();
 void Changegals();
 void Bombs();
 void Movegals2();
 void Scores();
 void Explosion();
 Ship();
 while(Gameover==0)
 {
  //if(sndspeed==(Count*8/LOOP))
  {
	S1++; if(S1>=sndspeed) {S1=0;}
	if(S1==0)
	{
	 if(freq!=0 && Soundoff==0) {sound(freq);}
	 SC++; if(SC>=Delay) {SC=0; nosound();}
	 freq=freq+freqadder;
	 if(freq<0) {freq=0;}
	 if(freq>8000) { nosound(); freq=0; Delay=0; SC=0;}
	}
  }
  if(sspeed==(Count*8/LOOP))
  {
  Scores();
  }
  if(gspeed==(Count*8/LOOP))
  {
	Showgals(1);
	M1++; if(M1>=g1speed) {M1=0;}
	if(M1==0) {Movegals2();}
	M2++; if(M2>=gspeed) {M2=0;}
	if(M2==0) {Movegals();}
	Showgals(0);
  }
  if(ispeed==(Count*8/LOOP))
  {
	I1++; if(I1>=ispeed) {I1=0;}
	if(I1==0) {Input();}
  }
  if(cgspeed==(Count*8/LOOP))
  {
	CG1++; if(CG1>=cgspeed)
	{
	 CG1=0;
	 Changegals();
	 Showgals(0);
	}
  }
  if(bspeed==(Count*8/LOOP))
  {
	B1++; if(B1>=bspeed) {B1=0;}
	if(B1==0) {Bombs();}
  }
  if(mspeed==(Count*8/LOOP))
  {
	MISS1++; if(MISS1>=mspeed) {MISS1=0;}
	if(MISS1==0) {Missiles();}
  }
  if(espeed==(Count*8/LOOP))
  {
	E1++; if(E1>=espeed) {E1=0;}
	if(E1==0) {Explosion();}
  }
  if((Count++)>LOOP) {Count=0;}
 }
}
void Showgals(int m)
{
 int k;
 for(k=0;k<Numgals;k++)
 {
  if(gald[k]==0)
  {
	gotoxy(galx[k],galy[k]);
	if(m==0)
	{
	 if(galc[k]!=0) {textcolor(Colour1[galc[k]]);}
	 else {textcolor(gall[k]);}
	}
	else {textcolor(0);}
	cprintf("%c\r",gchar[galc[k]]);
  }
 }
}
void Movegals()
{
 int l;
 newxadder=xadder;
 for(l=0;l<Numgals;l++)
 {
  if(gald[l]==0 && galm[l]==0)
  {
	galx[l]=galx[l]+xadder;
	if((galx[l]<2 || galx[l]>78)&&galm[l]==0) {newxadder=-xadder;}
  }
 }
 xadder=newxadder;
}
void Ship()
{
 gotoxy(shipx,shipy);
 textcolor(LIGHTCYAN);
 cprintf(" \r");
 if(shipx+shipxadder>0 && shipx+shipxadder<80) {shipx=shipx+shipxadder;}
 gotoxy(shipx,shipy);
 cprintf("A\r");
}
void Missiles()
{
 int m;
 void Hitcheck(int);
 for(m=0;m<=MAXNUMMISS-1;m++)
 {
  if(misx[m]!=98)
  {
	gotoxy(misx[m],misy[m]);
	textcolor(WHITE);
	cprintf(" \r");
	shipxadder=0;
	Ship();
	Hitcheck(m);
	misy[m]--;
	if(misy[m]>1 && misx[m]!=98)
	{
	 gotoxy(misx[m],misy[m]);
	 cprintf(":\r");
	}
	else {misx[m]=98;}
  }
 }
}
void Hitcheck(int mm)
{
 int n;
 for(n=0;n<MAXNUMBOMBS;n++)
 {
  if(misx[mm]==bombx[n] && misy[mm]==bomby[n]) // Hit bomb
  {
	gotoxy(bombx[n],bomby[n]);
	cprintf(" \r");
	bombx[n]=99; misx[mm]=98;
  }
 }
 for(n=0;n<Numgals;n++)
 {
  if(misx[mm]==galx[n] && misy[mm]==galy[n] && gald[n]==0) // Hit galaxian
  {
	gotoxy(galx[n],galy[n]);
	textcolor(YELLOW);
	cprintf("*\r");
	gald[n]=1; misx[mm]=98;
	hits++;
	if(galy[n]>20) {Score+=20;}
	if(galm[n]!=0) {Score+=40;}
	Score+=10;
	if(hits==Numgals) {hits=0; Initialise(); break;}
	freq=200; freqadder=50; Delay=10; SC=0;
	break;
  }
 }
}
void Input()
{
 int mod,o,oi,oc;
 shipxadder=0;
 {
  mod=bioskey(2);
  if(mod & CTRL)
  {
	for(o=0;o<MAXNUMMISS;o++)
	{
	 if(misx[o]==98)
	 {
	  oc=0;
	  for(oi=0;oi<MAXNUMMISS;oi++)
	  {
		if(misy[oi]<shipy) {oc=1;}
	  }
	  if(oc==1)
	  {
		oc=0; misx[o]=shipx; misy[o]=shipy;
		freq=2350; freqadder=-50;
		Delay=50;
		SC=0;
		break;
	  }
	 }
	}
  }
 }
 {
  if(mod & RIGHT)
  {
	shipxadder=1;
  }
  if(mod & LEFT)
  {
	shipxadder=-1;
  }
 }
 {
  while(bioskey(1)!=0)
  {
	key=bioskey(0);
	//if(key==19712 || key==29696) {shipxadder=1; }
	//if(key==19200 || key==29440) {shipxadder=-1;}
	if(key==4209 || key==4177) { nosound(); Ch='q'; Gameover=1; }
	if(key==8051 || key==8019) { if(Soundoff==0) Soundoff=1; else Soundoff=0;}
  }
 }
 Ship();
}
void Changegals()
{
 int p;
 for(p=0;p<Numgals;p++)
 {
  if(galm[p]==0)
  {
	if(rand()%2==1)
	{
	 galc[p]++; if(galc[p]>7) {galc[p]=0;}
	}
	else
	{
	 if(int(rand()%2)==1)
	 {
	  galc[p]--; if(galc[p]<0) {galc[p]=7;}
	 }
	}
  }
 }
}
void Bombs()
{
 void BombHitcheck(int);
 int q,r;
 for(q=0;q<Numbombs;q++)
 {
  if(bombx[q]!=99)
  {
	gotoxy(bombx[q],bomby[q]);
	textcolor(RED);
	cprintf(" \r");
	BombHitcheck(q);
	bomby[q]++;
	if(bomby[q]<49 && bombx[q]!=99)
	{
	 gotoxy(bombx[q],bomby[q]);
	 cprintf("o\r");
	}
	else {bombx[q]=99; }
  }
  else
  {
	r=rand()%Numgals;
	while(gald[r]==1)
	{
	 r=rand()%Numgals;
	}
	bombx[q]=galx[r]; bomby[q]=galy[r]; break;;
  }
 }
}
void BombHitcheck(int qq)
{
 void HitShip();
 if(bombx[qq]==shipx && bomby[qq]==shipy)
 {
  HitShip();
 }
}
void HitShip()
{
 void Ship();
 void Endgame();
 int s;
 clrscr();
 nosound();
 for(s=0;s<lives-1;s++)
 {
  shipx=38+s*2; shipy=26;
  shipxadder=0;
  Ship();
  delay(250);
 }
  delay(1000);
  clrscr();
  //Initialise();
  shipx=40; shipy=45;
  lives--;
  if(lives==0) {Endgame();}
  delay(1000);
}
void Endgame()
{
 clrscr();
 gotoxy(33,26);
 textcolor(RED);
 cprintf("G A M E  O V E R\r");
 delay(2500);
 hits=0;
 Numbombs=0;
 Gameover=1;
}
void Movegals2()
{
 void Hitcheck2(int);
 int u,v,w;
 if(Numgals-hits>=1)
 {
  v=rand()%swoop;
  if(v==0)
  {
	w=rand()%Numgals;
	while(gald[w]==1)
	{
	 w=rand()%Numgals;
	}
	//if(galm[w]==0)
	{
	 galm[w]=(rand()%28)+1;
	 galsp[w]=0;
	 freq=1000+rand()%200*Sheet; Delay=4; freqadder=-1; SC=0;
	}
  }
 }
 for(u=0;u<Numgals;u++)
 {
  if(galm[u]!=0 && gald[u]==0)
  {
	strncpy(&Mov,(Moveptr[galm[u]])+galsp[u],1);
	switch (Mov)
	{
	 case '0': { galc[u]=0; galy[u]++; Hitcheck2(u); break;}
	 case '1': { galc[u]=1; galy[u]++; galx[u]--; Hitcheck2(u); break;}
	 case '2': { galc[u]=2; galx[u]--; Hitcheck2(u); break;}
	 case '3': { galc[u]=3; galx[u]--; galy[u]--; Hitcheck2(u); break;}
	 case '4': { galc[u]=4; galy[u]--; Hitcheck2(u); break;}
	 case '5': { galc[u]=5; galy[u]--; galx[u]++; Hitcheck2(u); break;}
	 case '6': { galc[u]=6; galx[u]++; Hitcheck2(u); break;}
	 case '7': { galc[u]=7; galx[u]++; galy[u]++; Hitcheck2(u); break;}
	 case '8': {
			 if(galy[u]<15 && galy[u]>2 && galx[u]>2 && galx[u]<78)
			 {
			  galm[u]=0; galsp[u]=0; break;
			 }
			 else
			 {
			 Hitcheck2(u);
			 freqadder=1; Delay=10;
			 break;
			 }
			}
	 case '9': { galc[u]++; if(galc[u]>7) {galc[u]=0;} break;}
	 case 'A': { galc[u]--; if(galc[u]<0) {galc[u]=7;} break;}
	}
	galsp[u]++; if(galsp[u]>39) {galsp[u]=0;}
  }
 }
}
void Hitcheck2(int uu)
{
 void HitShip();
 if(galx[uu]<1) {galx[uu]=78;}
 if(galx[uu]>79) {galx[uu]=2;}
 if(galy[uu]<1) {galy[uu]=48;}
 if(galy[uu]>48) {galy[uu]=2;}
 if(galx[uu]==shipx && galy[uu]==shipy)
 {
  gald[uu]=1; hits++;
  if(hits==Numgals) {hits=0; Initialise(); }
  HitShip();
 }
 if(rand()%Homefactor==1) {galm[uu]=8; galsp[uu]=0;}
}
void Scores()
{
 int z;
 if(Highscore<Score)
 {
  Highscore=Score;
  if(Gameover==0)
  {strcpy(Highname,"     ");}
 }
 gotoxy(1,1); textcolor(LIGHTCYAN);
 cprintf("Score:%ld\r",Score);
 gotoxy(32,1);
 cprintf("Highscore:%ld \"%s\"\r",Highscore,Highname);
 gotoxy(24,1);
 cprintf("Wave:%d",Sheet);
 for(z=0;z<lives-1;z++)
 {
  gotoxy(80-z*2,1);
  cprintf("A \r");
 }
}
void Explosion()
{
 // Clears explosion
 int az;
 for(az=0;az<Numgals;az++)
 {
  if(gald[az]==1)
  {
	//galx[az]==0; galy[az]==0;
	gotoxy(galx[az],galy[az]);
	cprintf(" \r");
  }
 }
}
void Hall()
{
 void ShowHall();
 int ha,hb,hc,sa;
 clrscr();
 for(hb=0;hb<30;hb++)
 {
  if(Score>Hscore[hb])
  {
	for(hc=29;hc>=hb;hc--)
	{
	 Hscore[hc]=Hscore[hc-1];
	 Hwave[hc]=Hwave[hc-1];
	 strncpy(Hname[hc],Hname[hc-1],11);
	}
	Hscore[hb]=Score;
	Hwave[hb]=Sheet;
	textcolor(LIGHTCYAN);
	gotoxy(28,24); cprintf("----------\r");
	gotoxy(10,23); cprintf("Enter your name : ");
	scanf("%10s",&Hname[hb]);
	clrscr();
	break;
  }
 }
 // save to file
 if((Hallfileptr=fopen("HALL.dat","w"))==NULL)
 { printf("Unable to open file for output !"); }
 else
 {
  for(ha=0;ha<30;ha++)
  {
	fprintf(Hallfileptr,"%ld %d %s\n ",Hscore[ha],Hwave[ha],Hname[ha]);
  }
  fclose(Hallfileptr);
 }
 delay(1000);
 textcolor(WHITE);
 gotoxy(67,48);
 cprintf("by ");
 for(sa=0;sa<9;sa++)
 {
  delay(60);
  textcolor(Colour1[sa]);
  cprintf("%c",*Pstring[sa]);
  if(Soundoff==0) sound(Tone[sa]);
 }
 nosound();
 delay(1000);
 gotoxy(67,48); printf(" ");
 gotoxy(79,48);
 delay(1000);
 ShowHall();
 getch();
 clrscr();
}
void ShowHall()
{
 int sha;
 textcolor(LIGHTGREEN); gotoxy(7,1);
 cprintf("Hall of FAME\r\n\n\n");
 cprintf("Rank Score Wave Name\n\n\r");
 for(sha=0;sha<30;sha++)
 {
  textcolor(Colour[sha]);
  cprintf("%2d : %6ld : %2d : %s\n\r",sha+1,Hscore[sha],Hwave[sha],&Hname[sha]);
 }
}
```

