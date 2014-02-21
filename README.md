/Структура компьютер (поля: тип процессора, тактовая частота,
// объем оперативной памяти, размер жесткого диска, тип видеокарты).

#define _CRT_SECURE_NO_WARNINGS
#include <iostream>
#include <fstream>
#include <time.h>

using namespace std;

char* names[] ={"Удачный   ", "Выгодный  ", "Надежный  ", "Пенсионный", "Экономный ", "Семейный  "};
char* money_type[] = {"Юани   ","Рубли  ","Доллары","Евро   "};

#define names_count 6
#define money_count 4


typedef struct{
	char name[256];
	char money[256];
	int summa;
	int profit;
} computer;


typedef struct Node{
	computer vklad;
	struct Node* next;
}list_item;


void main()
{
	setlocale(LC_ALL, "rus");
	srand(time(NULL));
	int n;
	printf("Enter number of vkladov:\n");
	scanf("%d", &n);
	list_item *spisok= new list_item;

	FILE* f;

	f=fopen("text.txt","wt");
	fwrite(&n, sizeof(int),1, f);
	for (int i = 0; i < n; ++i) 
	{
		strcpy(spisok->vklad.name,names[rand()%names_count]);

		strcpy(spisok->vklad.money,money_type[rand()%money_count]);
		spisok->vklad.summa = rand()%10000+1;
		spisok->vklad.profit = rand()%15+1;



		spisok->next= new list_item;
		spisok->next->next=NULL;

		//write
		fwrite(&(spisok->vklad),sizeof(spisok->vklad),1,f);
		


		printf("Название: %s\t Валюта: %s\t  Сумма вклада: %d\t Процентная ставка: %d%%\n\n",spisok->vklad.name,spisok->vklad.money,spisok->vklad.summa, spisok->vklad.profit); 
		spisok=spisok->next;


	}

	delete spisok -> next;
	spisok->next =NULL;
	fclose(f);
	system("PAUSE");

}

