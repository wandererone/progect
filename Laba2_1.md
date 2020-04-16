#include <iostream>
#include <windows.h>
#include <fstream>
#include <string>
using namespace std;


int main() {

	SetConsoleCP(1251);
	SetConsoleOutputCP(1251);

	int len;
	int var;

	
	char key[80];
	char open_text[80];
	
	string shifr;
	string str;
	
	cout << "Введите ключ: ";
	gets_s(key);

	string path_1 = "myFile.txt";
	string path_2 = "key.txt";
	

	//чтение нач текста
	cout << "1 или 2: ";
	cin >> var;
	if (var == 1)
	{
		ifstream fin2;
		fin2.open(path_1);

		if (!fin2.is_open())
		{
			cout << "Ошибка" << endl;
		}
		else
		{
			cout << "Файл открыт" << endl;
			cout << "Считывание из файла: ";
			
			while (!fin2.eof())
			{
				str = "";
				getline(fin2, str);
				cout << str;
			}
		}
		fin2.close();
		strcpy_s(open_text, str.c_str() );
	}

	else if (var == 2)
	{
		ifstream fin;
		fin.open(path_1);

		if (!fin.is_open())
		{
			cout << "Ошибка" << endl;
		}
		else
		{
			cout << "Файл открыт" << endl;
			
			cout << "Считывание из файла: ";
			while (!fin.eof())
			{
				shifr = "";
				getline(fin, shifr);
				cout << shifr;
			}
		}
		fin.close();
		strcpy_s(open_text, shifr.c_str());
	}
	
	len = strlen(key);

	char* res = new char[len];

	for (int i = 0; i < len; i++)
		res[i] = open_text[i] ^ key[i];

	
	
	// запись шифровки / дешифровки
	ofstream fout_1;

	fout_1.open(path_1);

	if (!fout_1.is_open())
	{
		cout << "ошибка открытия файла!" << endl;
	}
	else
	{
		for (int i = 0; i < len; i++)
		fout_1 << res[i];
	}
	fout_1.close();
	
	
	// запись ключа
	ofstream fout_2;

	fout_2.open(path_2);

	if (!fout_2.is_open())
	{
		cout << "ошибка открытия файла!" << endl;
	}
	else
	{
			fout_2 << key;
	}
	fout_2.close();
	 
	

	printf("\nОткрытый текст: %s", open_text);
	cout << "\nЗашифрованный текст: ";
	for (int i = 0; i < len; i++)
	cout << res[i];
	 
	delete [] res;
	return 0;
}
