# MyFirst2DGame
using System;
using System.Threading; //ненужная фигня но убиратт лень

namespace Map_treasure;

public static class Program
{
    public static void Main()
    {
        Random random = new Random();
        int MapXMax = 15; //Куча переменних 1 часть
        int MapYMax = 15;
        int PlayerX = random.Next(1, (MapXMax + 1));
        int PlayerY = random.Next(0, MapYMax); // Y от 0 до MapYMax-1
        int TreasureX = random.Next(1, (MapXMax + 1));
        int TreasureY = random.Next(0, MapYMax); // Y от 0 до MapYMax-1
        int FakeTreasureX = random.Next(1, (MapXMax + 1));
        int FakeTreasureY = random.Next(0, MapYMax);
        int BuffX = random.Next(1, (MapXMax + 1));
        int BuffY = random.Next(0, MapYMax);
        int MonsterX = random.Next(1, (MapXMax + 1));
        int MonsterY = random.Next(0, MapYMax);
        int Portal1X = random.Next(1, (MapXMax + 1));
        int Portal1Y = random.Next(0, MapYMax);
        int Portal2X = random.Next(1, (MapXMax + 1));
        int Portal2Y = random.Next(0, MapYMax);
        int MStopBuffX = random.Next(1, (MapXMax + 1));
        int MStopBuffY = random.Next(0, MapYMax);
        bool MStan = false;
        int MStopTime = 0;
        int CursY = 0;
        int CursX = 1;
        int Score = 0;
        int Lives = 3;
        int Schet = 0;
        int Schett = 1;
        int MSchet = 0;
        while (true) //Вечний цикл начало 2 части
        {
            MSchet += 1;
            if (MSchet == 2 && MStopTime == 0) //тригери взаемодействий
            {
                MSchet -= 2;
                if (MonsterY > PlayerY)
                {
                    MonsterY -= 1;
                }
                else if (MonsterY < PlayerY)
                {
                    MonsterY += 1;
                }
                else if (MonsterX > PlayerX)
                {
                    MonsterX -= 1;
                }
                else if (MonsterX < PlayerX)
                {
                    MonsterX += 1;
                }
            }
            if (PlayerX == TreasureX && PlayerY == TreasureY)
            {
                Score += 1;
                Schett = 0;
                TreasureX = random.Next(1, (MapXMax + 1));
                TreasureY = random.Next(0, MapYMax);
                FakeTreasureX = random.Next(1, (MapXMax + 1));
                FakeTreasureY = random.Next(0, MapYMax);
                Portal1X = random.Next(1, (MapXMax + 1));
                Portal1Y = random.Next(0, MapYMax);
                Portal2X = random.Next(1, (MapXMax + 1));
                Portal2Y = random.Next(0, MapYMax);
            }
            else if (PlayerX == FakeTreasureX && PlayerY == FakeTreasureY)
            {
                Score -= 1;
                Schett = 0;
                PlayerX = random.Next(1, (MapXMax + 1));
                PlayerY = random.Next(0, MapYMax);
                TreasureX = random.Next(1, (MapXMax + 1));
                TreasureY = random.Next(0, MapYMax);
                FakeTreasureX = random.Next(1, (MapXMax + 1));
                FakeTreasureY = random.Next(0, MapYMax);
                Portal1X = random.Next(1, (MapXMax + 1));
                Portal1Y = random.Next(0, MapYMax);
                Portal2X = random.Next(1, (MapXMax + 1));
                Portal2Y = random.Next(0, MapYMax);
            }
            else if (PlayerX == BuffX && PlayerY == BuffY)
            {
                Lives += 1;
                BuffX = random.Next(1, (MapXMax + 1));
                BuffY = random.Next(0, MapYMax);
                Schet -= 40;
            }
            else if (PlayerX == MonsterX && PlayerY == MonsterY)
            {
                Score -= 5;
                Schett = 0;
                PlayerX = random.Next(1, (MapXMax + 1));
                PlayerY = random.Next(0, MapYMax);
                MonsterX = random.Next(1, (MapXMax + 1));
                MonsterY = random.Next(0, MapYMax);
            }
            else if (PlayerX == Portal1X && PlayerY == Portal1Y)
            {
                PlayerX = Portal2X;
                PlayerY = Portal2Y;
                Portal1X = random.Next(1, (MapXMax + 1));
                Portal1Y = random.Next(0, MapYMax);
                Portal2X = random.Next(1, (MapXMax + 1));
                Portal2Y = random.Next(0, MapYMax);
            }
            else if (PlayerX == Portal2X && PlayerY == Portal2Y)
            {
                PlayerX = Portal1X;
                PlayerY = Portal1Y;
                Portal1X = random.Next(1, (MapXMax + 1));
                Portal1Y = random.Next(0, MapYMax);
                Portal2X = random.Next(1, (MapXMax + 1));
                Portal2Y = random.Next(0, MapYMax);
            }
            else if (PlayerX == MStopBuffX && PlayerY == MStopBuffY)
            {
                MStan = true;
                MStopTime = 5;
                MStopBuffX = random.Next(1, (MapXMax + 1));
                MStopBuffY = random.Next(0, MapYMax);
            }
            CursY = 0;
            CursX = 1;
            Console.Clear();
            Console.WriteLine($"Ваші очки: {Score}, Житті: {Lives}."); // Вивод очков
            //Console.WriteLine($"Отладка: игрок: {PlayerX}, {PlayerY}. монстр: {MonsterX}, {MonsterY}, {MSchet}"); //ета тоже не обращай внимания
            //Console.WriteLine($"игрок: {PlayerX}, {PlayerY}, сокровище: {TreasureX}, {TreasureY}, фейк: {FakeTreasureX}, {FakeTreasureY}"); //Ето палка отладка в случаях неудачи коордов
            //Console.WriteLine($"{MStopTime}");
            while (CursY < MapYMax) // Типо прорисовка пока Y "курсора" рисования не будет = макс Y карти начало движка рендера
            {
                Console.Write(" ");
                while (CursX < (MapXMax + 1)) // Типо тоже что и на 32 но только уже по X
                {
                    if (CursX == PlayerX && CursY == PlayerY)
                    {
                        Console.Write("O"); //Игрок
                    }
                    else if (CursX == TreasureX && CursY == TreasureY)
                    {
                        Console.Write("X"); //Сокровище
                    }
                    else if (CursX == FakeTreasureX && CursY == FakeTreasureY)
                    {
                        Console.Write("×"); //Сокровище фейк
                    }
                    else if (CursX == BuffX && CursY == BuffY)
                    {
                        Console.Write("★"); //бафф
                    }
                    else if (CursX == MonsterX && CursY == MonsterY)
                    {
                        Console.Write("M"); //монстр
                    }
                    else if ((CursX == Portal1X && CursY == Portal1Y) || (CursX == Portal2X && CursY == Portal2Y))
                    {
                        Console.Write("Π"); //портал
                    }
                    else if (CursX == MStopBuffX && CursY == MStopBuffY)
                    {
                        Console.Write("="); //бафф стопа монстра
                    }
                    else
                    {
                        Console.Write("_"); //Пустая клетка
                    }
                    CursX++; //Нужно что б прорисовка не сломалась и двигалась дальше
                }
                if (CursY == PlayerY)
                {
                    Console.Write("<-");
                }
                CursY += 1; //Для перемещения на рядок ниже
                CursX = 1; //Снова Х курсора вначале что б все било ок
                Console.WriteLine(" "); //Самая нужная тут штука для правильной прорисовки и конец движка
            }
            Console.WriteLine("WASD для движения, Escape/E для вихода."); //Тутор игроку какая клавиша что делает и начало 3 части
            ConsoleKeyInfo Kla = Console.ReadKey(true); //Переменная для работи кода ниже
            if (Kla.Key == ConsoleKey.W) //Для W
            {
                if (PlayerY > 0)
                {
                    PlayerY -= 1;
                }
            }
            else if (Kla.Key == ConsoleKey.S) //Для S
            {
                if (PlayerY < (MapYMax - 1))
                {
                    PlayerY += 1;
                }
            }
            else if (Kla.Key == ConsoleKey.A) //Для A
            {
                if (PlayerX > 1)
                {
                    PlayerX -= 1;
                }
            }
            else if (Kla.Key == ConsoleKey.D) //Для D
            {
                if (PlayerX < MapXMax)
                {
                    PlayerX += 1;
                }
            }
            else if (Kla.Key == ConsoleKey.Escape || Kla.Key == ConsoleKey.E) //Для Escape на ПК или E на тел
            {
                Console.WriteLine("Гру завершено!");
                break; //Ага конечно ето виход из цикла
            }
            Schet += 1;
            if (Schet == 40)
            {
                Schet = 0;
                Score -= 1;
                Console.WriteLine("Ой ой занадто довго!");
                Thread.Sleep(1000);
            }
            if (Score < 0)
            {
                if ((Lives - 1) >= 1)
                {
                    if (Schett == 1)
                    {
                        Schett = 0;
                        Score = 5;
                        Thread.Sleep(100);
                        Lives -= 1;
                        Thread.Sleep(100);
                        Schett = 1;
                    }
                }
                else
                {
                    if (Schett == 1)
                    {
                        Schett = 0;
                        Lives -= 1;
                        Console.Clear();
                        Console.WriteLine("Ти програв!");
                        break;
                        Schett = 1;
                    }
                }
            }
            if (MStan == true)
            {
                MSchet -= 1;
                if (MStopTime == 0)
                {
                    MStan = false;
                }
                else
                {
                    MStopTime -= 1;
                }
            }
        }
    }
}
