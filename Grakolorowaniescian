#include <iostream>
#include <string>
#include <iomanip>
#include <chrono>
#include <windows.h>
#include <thread>
#include <fstream>
using namespace std;
int pozycjaX = 0;
int pozycjaY = 0;
int ktorypoziom = 1;
char tab[10][10];
int maxdlmapyX = 0;
int maxdlmapyY = 0;
bool koniecgry = 0;
int punkty = 0;
HANDLE h = GetStdHandle(STD_OUTPUT_HANDLE);

void wyswietlmapke() {
	system("cls");
	//cout << "Pozycja Y: " << pozycjaY << endl << "Pozycja X: " << pozycjaX << endl;
	int i = 0, j = 0;
	while (i < maxdlmapyY)
	{
		while (j < maxdlmapyX)
		{
			if (pozycjaX == j && pozycjaY == i) {
				SetConsoleTextAttribute(h, 13);
				cout << (char)(219) << (char)(219);
			}
			else {
				if (tab[i][j] == 'X')
				{
					SetConsoleTextAttribute(h, 8);
				}
				else if (tab[i][j] == 'O')
				{
					SetConsoleTextAttribute(h, 7);
				}
				else
				{
					SetConsoleTextAttribute(h, 10);
				}
				cout << (char)(219) << (char)(219);
			}
			//cout << " ";
			j++;
		}
		cout << endl;
		i++;
		j = 0;
	}
	SetConsoleTextAttribute(h, 15);
}

bool czywygral() {
	int i = 0, j = 0;
	while (i<maxdlmapyY) {
		j = 0;
		while (j<maxdlmapyX) {
			if (tab[i][j]!='P' && tab[i][j]!='X') {
				return false;
			}
			j++;
		}
		i++;
	}
	return true;
}

void odczytajmapke() {
	fstream czytanko;
	int i = 0, j=0, dlmapy;
	bool czyodczytane = false;
	czytanko.open("mapki.txt", ios::in);
	string dane;
	while (!czytanko.eof() && czyodczytane==false)
	{
		getline(czytanko, dane);
		cout << dane << endl;
		if (dane == to_string(ktorypoziom)) {
			getline(czytanko, dane);
			czyodczytane = true;
			dlmapy = stoi(dane);
			dlmapy = dlmapy / 10000;
			maxdlmapyY = dlmapy;
			getline(czytanko, dane);
			dlmapy = stoi(dane);
			dlmapy = dlmapy / 10000;
			maxdlmapyX = dlmapy;
			cout << dlmapy << endl;
			while (i<maxdlmapyY) {
				getline(czytanko,dane);
				while (j<maxdlmapyX) {
					tab[i][j] = dane[j];
					j++;
				}
				i++;
				j = 0;
			}
		}
		else if (dane=="ENDOFGAME") {
			koniecgry = true;
		}
	}
}

int main()
{
	using namespace std::this_thread;
	using namespace std::chrono;
	bool czywygrana = false;
	bool czypomalowane = false, czymoze = true;
	char kierunek;
	fstream czytamydanegracza;
	fstream wpisaniedanychgracza;
	string dane;
	czytamydanegracza.open("danegracza.txt", ios::in);
	getline(czytamydanegracza, dane);
	ktorypoziom = stoi(dane);
	getline(czytamydanegracza, dane);
	punkty = stoi(dane);
	czytamydanegracza.close();
	while (true)
	{
		czywygrana = false;
		pozycjaX = 0;
		pozycjaY = 0;
		maxdlmapyY = 0;
		maxdlmapyX = 0;
		odczytajmapke();
		SetConsoleTextAttribute(h, 15);
		wyswietlmapke();
		while (czywygrana == false) {
			kierunek = 'z';
			while (kierunek != 'a' && kierunek != 's' && kierunek != 'd' && kierunek != 'w') {
				cout << "Podaj kierunek" << endl;
				cin >> kierunek;
			}
			czymoze = true;
			if (kierunek == 's') {
				while (czymoze == true) {
					if (tab[pozycjaY + 1][pozycjaX] != 'X' && pozycjaY + 1 < maxdlmapyY) {
						czymoze = true;
						tab[pozycjaY][pozycjaX] = 'P';
						pozycjaY++;
					}
					else {
						czymoze = false;
					}
					wyswietlmapke();
					sleep_for(nanoseconds(1000));
				}
			}
			else if (kierunek == 'd') {
				while (czymoze == true) {
					if (tab[pozycjaY][pozycjaX + 1] != 'X' && pozycjaX + 1 < maxdlmapyX) {
						tab[pozycjaY][pozycjaX] = 'P';
						pozycjaX++;
					}
					else {
						czymoze = false;
					}
					wyswietlmapke();
					sleep_for(nanoseconds(1000));
				}
			}
			else if (kierunek == 'a') {
				while (czymoze == true) {
					if (tab[pozycjaY][pozycjaX - 1] != 'X' && pozycjaX - 1 > -1) {
						tab[pozycjaY][pozycjaX] = 'P';
						pozycjaX--;
					}
					else {
						czymoze = false;
					}
					wyswietlmapke();
					sleep_for(nanoseconds(1000));
				}
			}
			else if (kierunek == 'w') {
				while (czymoze == true) {
					if (tab[pozycjaY - 1][pozycjaX] != 'X' && pozycjaY - 1 > -1) {
						tab[pozycjaY][pozycjaX] = 'P';
						pozycjaY--;
					}
					else {
						czymoze = false;
					}
					wyswietlmapke();
					sleep_for(nanoseconds(1000));
				}
			}
			tab[pozycjaY][pozycjaX] = 'P';
			wyswietlmapke();
			czywygrana = czywygral();
			if (czywygrana == true) {
				sleep_for(nanoseconds(2000));
				system("cls");
				ktorypoziom++;
				wpisaniedanychgracza.open("danegracza.txt", ios::out);
				wpisaniedanychgracza << ktorypoziom << endl << punkty;
				wpisaniedanychgracza.close();
			}
		}
	}
}
