using System;
using System.Collections.Generic;

namespace CarpoolApp
{
    class Program
    {
        static void Main(string[] args)
        {
            CarpoolSystem carpoolSystem = new CarpoolSystem();
            int choice;

            do
            {
                Console.WriteLine("1. Создать поездку");
                Console.WriteLine("2. Найти попутчиков");
                Console.WriteLine("0. Выход");
                Console.Write("Ваш выбор: ");
                choice = Convert.ToInt32(Console.ReadLine());

                switch (choice)
                {
                    case 1:
                        carpoolSystem.CreateTrip();
                        break;
                    case 2:
                        carpoolSystem.FindRiders();
                        break;
                    case 0:
                        Console.WriteLine("Выход из программы.");
                        break;
                    default:
                        Console.WriteLine("Неверный выбор. Попробуйте снова.");
                        break;
                }

            } while (choice != 0);
        }
    }

    public class Trip
    {
        public string Destination { get; set; }
        public string Date { get; set; }
        public string DriverName { get; set; }
        public int AvailableSeats { get; set; }

        public Trip(string destination, string date, string driverName, int availableSeats)
        {
            Destination = destination;
            Date = date;
            DriverName = driverName;
            AvailableSeats = availableSeats;
        }
    }

    public class CarpoolSystem
    {
        private List<Trip> trips;

        public CarpoolSystem()
        {
            trips = new List<Trip>();
        }

        public void CreateTrip()
        {
            Console.Write("Введите пункт назначения: ");
            string destination = Console.ReadLine();

            Console.Write("Введите дату поездки (например, 2023-10-01): ");
            string date = Console.ReadLine();

            Console.Write("Введите ваше имя: ");
            string driverName = Console.ReadLine();

            Console.Write("Введите количество доступных мест: ");
            int availableSeats = Convert.ToInt32(Console.ReadLine());

            trips.Add(new Trip(destination, date, driverName, availableSeats));
            Console.WriteLine($"Поездка в {destination} на {date} создана успешно.");
        }

        public void FindRiders()
        {
            Console.WriteLine("\n--- Доступные поездки ---");
            if (trips.Count == 0)
            {
                Console.WriteLine("Нет доступных поездок.");
                return;
            }

            foreach (var trip in trips)
            {
                Console.WriteLine($"Назначение: {trip.Destination}, Дата: {trip.Date}, Водитель: {trip.DriverName}, Доступные места: {trip.AvailableSeats}");
            }

            Console.WriteLine("-");
        }
    }
}
