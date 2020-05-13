#include<stdio.h>
#include<string.h>
#include<ctype.h>
#include<windows.h>
enum { BLACK=0, BLUE, GREEN, CYAN, RED, MAGENTA, BROWN, LIGHTGRAY,
        DARKGRAY, LIGHTBLUE, LIGHTGREEN, LIGHTCYAN, LIGHTRED, LIGHTMAGENTA, YELLOW, WHITE, };
static short __BACKGROUND = 0;
static short __FOREGROUND = 0;
void textbackground(short color) {
	__BACKGROUND = color;
	HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
	SetConsoleTextAttribute(hOut, __FOREGROUND + (color << 4));
}
void textcolor(short color) {
	__FOREGROUND = color;
	HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
	SetConsoleTextAttribute(hOut, color + (__BACKGROUND << 4));
}
void gotoxy(short c, short r) {
	if (c>0 && r>0) {
		COORD CursorPosition = { c-1, r-1 };
		HANDLE hOut = GetStdHandle(STD_OUTPUT_HANDLE);
		SetConsoleCursorPosition(hOut, CursorPosition);
	}
}
char * del_space_punct_digit(char * str)    //cancellare eventuali spazi, segni di punteggiatura o numeri da una stringa
{
	int k, l=0;
	for(k=0; str[k]!='\0'; k++){
	    if(!isblank(str[k]) && !ispunct(str[k]) && !isdigit(str[k])){
	        str[k]=toupper(str[k]);
	        str[l++]=str[k];
	    }
    }
	str[l]='\0';
	return str;
}
void assegamento_posizioni(char str[100+1], int pos[100+1])
{
	int cont[26], i, k, j;
	for(i=0; i<26; i++)        
	    cont[i]=i;           // all'array cont[i] assegno il valore della propria posizione, i, fino a 26
	i=0;                     // ad ogni posizione dell'array cont assegno il valore della propria posizione, i, fino a 26 in modo tale che posso, in seguito, controllare l'array str
	j=1;
	while(i<26){
		for(k=0; str[k]!='\0'; k++){
			if(cont[i]==str[k]-'A'){    
	       	    pos[k]=j;      // assegno all'array pos, nella posizione k, un valore che corrisponde all'ordine alfabetico del carattere nella stringa str, cioè nella parola chiave;
	       	    j++;           // k corrisponde alla posizione del carattere nella stringa str.
	        }
		}
		i++;
	}
}
void visualizza_numeri_corrispondenti(int len, int pos[100+1])      //visualizza i numeri corrispondenti ai caratteri dell'array str in base alla posizione che ha in esso
{
	textbackground(0);
	textcolor(10);
	int k;
	for(k=0; k<len-1; k++){
		if(k<len-2)
			printf("%u-", pos[k]);
		else
			printf("%u", pos[k]);
	}
}
void disposizione_parola__chiave_in_tabella(char str[100+1], int len)     //visualizza l'array str, cioè la parola chiave, all'interno della tabella
{
	textcolor(CYAN);
	textbackground(0);
	int k;
	for(k=0; k<len-1; k++)
		printf("  %c  ", str[k]);
}
void inserimento_lineette_in_tabella(unsigned len)           //visualizza una riga di lineette tabella        
{
	unsigned k;
	textcolor(YELLOW);
	for(k=0; k<len-1; k++)
		printf("  -  ");
}
void disposizione_numeri_corrispondenti_in_tabella(int len, int pos[100+1])  //visualizza nella tabella i numeri corrispondenti ai caratteri dell'array str in base alla posizione che ha in esso 
{
	textcolor(10);
	int k;
	for(k=0; k<len-1; k++){                  
		if(pos[k]<10)
	   		printf("  %u  ", pos[k]);
	   	else
	      	printf("  %u ", pos[k]);
	}
}
void disposizione_messaggio_in_tabella(char str2[100+1], char matrice[100+1][100+1], int len)    //visualizza nella tabella il messaggio da crittografare, cioè str2 
{
	textcolor(6);
	int k, r=0, c=0;
	for(k=0; str2[k]!='\0' && str2[k]!='\n'; k++){             
		matrice[r][c]=str2[k];
		printf("  %c  ", matrice[r][c]);
		c++;
		if(c==len-1){
			printf("\n");
			c=0;
			r++;
		}
	}
}
void inserimento_lettere_casuali_in_tabella(char matrice[100+1][100+1], int len, int len2)  //nel caso in cui si scelga il cifrario a trasposizione colonnare regolare, vengono inserite lettere casuali nell'ultima riga al fine di completarla 
{
	textcolor(RED);
	int r, c;
	r=(len2-1)/(len-1);
	for(c=(len2-1)%(len-1); c<len-1 && c!=0; c++){
		matrice[r][c]=(char) 65+rand()%26;
		printf("  %c  ", matrice[r][c]);
	}
}
void visualizza_messaggio_crittografato(char matrice[100+1][100+1], int pos[100+1], int len, int len2)   //visualizza messaggio crittografato 
{
	textbackground(0);	
    int c=0, r=0, j=1, k;
	k=(len2-1)/(len-1);
	while(j<len){
		if(pos[c]==j){
			for(r=0; r<=k; r++){
				if(r==(len2-1)/(len-1) && c>=(len2-1)%(len-1))
					textcolor(RED);
				else
					textcolor(6);
				printf("%c", matrice[r][c]);
			}
			j++;
			c=0;
			printf("  ");
		}
		else
			c++;
	}
}
int main()
{
	int opzione;
	printf("ESERCIZI A DISPOSIZIONE(1-2-3-4):\n");
	printf("1)cifrario a trasposizione colonnare;\n");
	printf("2)cifrario carbonaro;\n");
	printf("3)cifrario ROT13;\n");
	printf("4)uscire dal programma.\n");
	scanf("%d",&opzione);
	getchar();  //per "prepararsi" a leggere un altro carattere (alternativa: o metti fflush(stdin) per pulire il buffer , come vuoi)
	char str2[100+1];
	if(opzione<4 && opzione>0){ 
	    textcolor(WHITE);
		textbackground(1);
	    printf("INSERISCI IL MESSAGGIO DA CRITTOGRAFARE:\n");
		textcolor(BROWN);
		textbackground(0);
	    fgets(str2, sizeof(str2), stdin);
	}
	if(opzione==1){
		char str[100+1];
	    int t;
		    textcolor(WHITE);
		    textbackground(1);
	    printf("INSERISCI UNA SINGOLA PAROLA COME CHIAVE CRITTOGRAFICA:\n");
		    textcolor(CYAN);
		    textbackground(0);
	    fgets(str, sizeof(str), stdin);
		    textcolor(WHITE);
		    textbackground(1);
	    printf("SELEZIONA TIPOLOGIA DI ESERCIZIO(1-2):\n");
	        textcolor(WHITE);
	        textbackground(0);
	    printf("1)CIFRARIO A TRASPOSIZIONE REGOLARE: nella tabella, le posizioni vuote alla fine dell'ultima riga vengono riempite\n  con caratteri alfabetici casuali;\n");
	    printf("2)CIFRARIO A TRASPOSIZIONE IRREGOLARE: nella tabella, le posizioni vuote alla fine dell'ultima riga rimangono vuote.\n");
	    scanf("%d", &t);
	
	    del_space_punct_digit(str);
	    del_space_punct_digit(str2);
	    int len=strlen(str);
	    int pos[100+1]; 
	    int len2=strlen(str2);
	    char matrice[100+1][100+1];
	    assegamento_posizioni(str, pos);
	
	    textcolor(WHITE);
	    textbackground(1);
	    printf("NUMERI CORRISPONDENTI:\n");
        visualizza_numeri_corrispondenti(len, pos);
	    printf("\n");
	
	    textcolor(WHITE);
	    textbackground(1);
	    printf("TABELLA:\n\n");
	
	    disposizione_parola__chiave_in_tabella(str, len);
	    printf("\n");
	
	    inserimento_lineette_in_tabella(len);
	    printf("\n");
    
        disposizione_numeri_corrispondenti_in_tabella(len, pos);
    	printf("\n");
	
	    inserimento_lineette_in_tabella(len);
	    printf("\n");
	
	    disposizione_messaggio_in_tabella(str2, matrice, len);
	
	    if(t==1)
		    inserimento_lettere_casuali_in_tabella(matrice, len, len2);
	    printf("\n\n");
	
	    textcolor(WHITE);
	    textbackground(1);
	    printf("MESSAGGIO CRITTOGRAFATO: \n");
	    visualizza_messaggio_crittografato(matrice, pos, len, len2);
    }
    else if(opzione==2){
    	char str[26+1]={'A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z','\0'};
    	char cod[26+1]={'O','P','G','T','I','V','C','H','E','J','K','R','N','M','A','B','Q','L','Z','D','U','F','W','X','Y','S','\0'};
    	int k=0, j=0;
    	textcolor(WHITE);
	    textbackground(1);
	    printf("MESSAGGIO CRITTOGRAFATO: \n");
	    textcolor(LIGHTGREEN);
	    textbackground(0);
    	while(str2[k]!='\0'){
    		str2[k]=toupper(str2[k]);
    		do{
    			if(isalpha(str2[k]) && str2[k]==str[j])
    				printf("%c", cod[j]);
				else if(isblank(str2[k]) || ispunct(str2[k]) || isdigit(str2[k])){
					printf("%c", str2[k]);
					k++;
					j=0;
					str2[k]=toupper(str2[k]);
				}
			    j++;
			}while(str2[k]!=str[j-1]);
			j=0;
			k++;
		}
	}
	else if(opzione==3){
	    int k;
	    for(k=0; str2[k]!='\0' && str2[k]!='\n'; k++){
	    	str2[k]=toupper(str2[k]);
	    	if(str2[k]-'A'<13 && isalpha(str2[k]))
	    		str2[k]=str2[k]+13;
			else if(isalpha(str2[k]))
				str2[k]='A'+(12-('Z'-str2[k]));
		}
		textcolor(WHITE);
	    textbackground(1);
	    printf("MESSAGGIO CRITTOGRAFATO: \n");
	    textcolor(LIGHTGREEN);
	    textbackground(0);
		printf("%s", str2);
	}
	printf("\n\n");
	textcolor(WHITE);
	textbackground(0);
	printf("FATTO DA:\n");
	printf("ANDREA SARTONI\n");
	printf("FILIPPO LAZZARI\n");
	textcolor(MAGENTA);
}
