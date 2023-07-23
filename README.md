# Pacman-OOP
A simple Pacman game using object oriented programming paradigm with C++

## Code:

```
using namespace std;
#include <iostream>
#include <conio.h>
class Pac
{
private:
	int PosX, PosY;
	//bool lose = false;
public:
	Pac()
	{
		PosX = PosY = 0;
	}
	Pac(int x, int y) :Pac()
	{
		PosX = x;
		PosY = y;
	}
	inline void MoveUp() { PosY--; }
	inline void MoveDown() { PosY++; }
	inline void MoveRight() { PosX++; }
	inline void MoveLeft() { PosX--; }

	inline int GetX() { return PosX; }
	inline int GetY() { return PosY; }

	friend ostream& operator <<(ostream& o, Pac c)
	{
		o << "PosX:[" << c.GetX() <<"],PosY:[" << c.GetY() << "]\n";
		return o;
	}

};
class Fruit
{
private:
	int FruitX, FruitY;
public:
	Fruit(int x , int y)
	{
		FruitX = x;
		FruitY = y;
	}
	inline int GetX() { return FruitX; }
	inline int GetY() { return FruitY; }
};
class Control
{
private:
	int Height, Width;
	char up, down, right, left;
	bool Lose, Exict[5];
	int Score;
	Pac* P;
	Fruit* F[5];
public:
	Control(int w, int h)
	{
		Height = h;
		Width = w;
		up = 'w'; right = 'd';
		down = 's'; left = 'a';
		Lose = false;
		for (int k = 0; k < 5; k++)
		{

			Exict[k] = true;
		}
		P = new Pac(33, 14);
		F[0] = new Fruit(12, 8);
		F[1] = new Fruit(30, 4);
		F[2] = new Fruit(24, 12);
		F[3] = new Fruit(45, 12);
		F[4] = new Fruit(45, 8);
		Score = 0;
	}
	~Control()
	{
		delete P, F[0], F[1], F[2], F[3], F[4];
	}
	void Draw()
	{
		system("cls");
		for (int i = 0; i < Height; i++)
		{
			for (int j = 0; j < Width; j++)
			{

				int PacX = P->GetX();
				int PacY = P->GetY();
				int F1X = F[0]->GetX();
				int F1Y = F[0]->GetY();
				int F2X = F[1]->GetX();
				int F2Y = F[1]->GetY();
				int F3X = F[2]->GetX();
				int F3Y = F[2]->GetY();
				int F4X = F[3]->GetX();
				int F4Y = F[3]->GetY();
				int F5X = F[4]->GetX();
				int F5Y = F[4]->GetY();

				if (i == 0 || i == Height - 1 || j == 0 || j == Width - 1) cout << "#";
				else if (i == PacY && j == PacX) cout << "G";
				else if (i == F1Y && j == F1X)
				{
					if (Exict[0] == true) cout << "o";
					else cout << " ";
				}
				else if (i == F2Y && j == F2X)
				{
					if (Exict[1] == true) cout << "o";
					else cout << " ";
				}
				else if (i == F3Y && j == F3X)
				{
					if (Exict[2] == true) cout << "o";
					else cout << " ";
				}
				else if (i == F4Y && j == F4X)
				{
					if (Exict[3] == true) cout << "o";
					else cout << " ";
				}
				else if (i == F5Y && j == F5X)
				{
					if (Exict[4] == true) cout << "o";
					else cout << " ";
				}
				else if (i >= 4 && i <= 12 && j == 6) cout << "#";
				else if (i <= 12 && j == 15) cout << "#";
				else if (i >= 3 && j == 21) cout << "#";
				else if (i <= 15 && j == 42) cout << "#";
				else if (i >= 6 && i <= 10 && j == 54) cout << "#";
				else if (j >= 6 && j <= 15 && i == 12) cout << "#";
				else if (j >= 21 && j <= 38 && i == 10) cout << "#";
				else if (j >= 42 && j <= 54 && i == 10) cout << "#";
				else cout << " ";
			}
			cout << "\n";
		}
		cout << "Score: " << Score << "\n";
	}
	void Input()
	{
		int PacX = P->GetX();
		int PacY = P->GetY();
		if (_kbhit())
		{
			char c = _getch();
			if (c == up)   P->MoveUp();
			if (c == down) P->MoveDown();
			if (c == right)   P->MoveRight();
			if (c == left) P->MoveLeft();
			if(c == 'x') Lose = true;
		}
	}
	void Logic()
	{
		int PacX = P->GetX();
		int PacY = P->GetY();
		int F1X = F[0]->GetX();
		int F1Y = F[0]->GetY();
		int F2X = F[1]->GetX();
		int F2Y = F[1]->GetY();
		int F3X = F[2]->GetX();
		int F3Y = F[2]->GetY();
		int F4X = F[3]->GetX();
		int F4Y = F[3]->GetY();
		int F5X = F[4]->GetX();
		int F5Y = F[4]->GetY();
		if (PacX == F1X && PacY == F1Y)
		{
			if (Exict[0] == true)
			{
				Exict[0] = false;
				Score = Score + 10;
			}
		}
		if (PacX == F2X && PacY == F2Y)
		{
			if (Exict[1] == true)
			{
				Exict[1] = false;
				Score = Score + 10;
			}
		}
		if (PacX == F3X && PacY == F3Y)
		{
			if (Exict[2] == true)
			{
				Exict[2] = false;
				Score = Score + 10;
			}
		}
		if (PacX == F4X && PacY == F4Y)
		{
			if (Exict[3] == true)
			{
				Exict[3] = false;
				Score = Score + 10;
			}
		}
		if (PacX == F5X && PacY == F5Y)
		{
			if (Exict[4] == true)
			{
				Exict[4] = false;
				Score = Score + 10;
			}
		}
		if (PacY >= 4 && PacY <= 12 && PacX == 6) Lose = true;
		else if (PacY <= 12 && PacX == 15) Lose = true;
		else if (PacY >= 3 && PacX == 21) Lose = true;
		else if (PacY <= 15 && PacX == 42) Lose = true;
		else if (PacY >= 6 && PacY <= 10 && PacX == 54) Lose = true;
		else if (PacX >= 6 && PacX <= 15 && PacY == 12) Lose = true;
		else if (PacX >= 21 && PacX <= 38 && PacY == 10) Lose = true;
		else if (PacX >= 42 && PacX <= 54 && PacY == 10) Lose = true;
	}
	void Run()
	{
		while (!Lose)
		{
			Draw();
			Input();
			Logic();
		}
	}
};
int main()
{
	Control c(60, 20);
	c.Run();
	return 0;
}
```

## Screens: 
      
![6--Pacman-OOP-1](https://github.com/Elzubair-Dev/Pacman-OOP/assets/104657152/86f0ccb7-8097-40eb-a7e5-11408112cf39)
![6--Pacman-OOP-2](https://github.com/Elzubair-Dev/Pacman-OOP/assets/104657152/2a503eca-b5c3-485a-9a13-3ed6cb48a79a)
![6--Pacman-OOP-3](https://github.com/Elzubair-Dev/Pacman-OOP/assets/104657152/206f5ea1-dc3e-4254-b586-0253271bdbaa)

## Buy me a Coffee:
      
if you want to support me:
(https://www.buymeacoffee.com/zu698air)
     
#### Don't forget to give me Star
      
## Done

