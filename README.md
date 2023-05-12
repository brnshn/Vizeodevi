# Vizeodevi
NESNEYE DAYALI PROGRAMLAMA (python)
# Define the classes
class Film:
    def __init__(self, film_name, time):
        self.film_name = film_name
        self.time = time


class Salon:
    def __init__(self, name, capacity):
        self.name = name
        self.capacity = capacity


class Seans:
    def __init__(self, film, salon, date, time):
        self.film = film
        self.salon = salon
        self.date = date
        self.time = time


class Rezervasyon:
    def __init__(self, seans, customer_name, customer_surname, ticket_count, seat_no):
        self.seans = seans
        self.customer_name = customer_name
        self.customer_surname = customer_surname
        self.ticket_count = ticket_count
        self.seat_no = seat_no

# Define a function to print the available films and let the user choose one
def choose_film(films):
    print("Available films:")
    for i, film in enumerate(films):
        print(f"{i+1}. {film.film_name} ({film.time})")
    while True:
        try:
            film_choice = int(input("Enter the number of the film you want to watch: "))
            if film_choice not in range(1, len(films)+1):
                raise ValueError(f"Invalid input! Please enter a number between 1 and {len(films)}.")
            break
        except ValueError as error:
            print(error)
    return films[film_choice-1]

# Define a function to print the available seanses for the chosen film and let the user choose one
def choose_seans(film, seanslar):
    available_seanslar = [seans for seans in seanslar if seans.film == film]
    print("Available seanses seanslar:")
    for i, seans in enumerate(available_seanslar):
        print(f"{i+1}. {seans.salon.name}, {seans.date} {seans.time}")
    while True:
        try:
            seans_choice = int(input("Enter the number of the seans you want to watch: "))
            if seans_choice not in range(1, len(available_seanslar)+1):
                raise ValueError(f"Invalid input! Please enter a number between 1 and {len(available_seanslar)}.")
            break
        except ValueError as error:
            print(error)
    return available_seanslar[seans_choice-1]


# Define a function to let the user make a reservation for the chosen seans
def make_reservation(seans):
    print(f"Making a reservation for {seans.film.film_name} on {seans.date} at {seans.time} in {seans.salon.name}")
    customer_name = input("Enter your name: ")
    customer_surname = input("Enter your surname: ")
    ticket_count = int(input("Enter the number of tickets: "))
    seat_no = []
    for i in range(ticket_count):
        while True:
            seat = input(f"Enter the seat number for ticket {i+1}: ")
            if seat in seat_no:
                print('You already chose that seat number. Please choose another one.')
            else:
                seat_no.append(seat)
                break
    reservation = Rezervasyon(seans, customer_name, customer_surname, ticket_count, seat_no)
    print("Reservation successful!")
    print(f"Reservation details:\nFilm: {reservation.seans.film.film_name} \nSalon: {reservation.seans.salon.name} \nDate: {reservation.seans.date} \nTime: {reservation.seans.time} \nTicket Count: {reservation.ticket_count} \nSeat Numbers: {reservation.seat_no}")


if __name__ == '__main__':
    # film, salon ve seans classlarindan ornek olusturma
    films = [Film("Avengers: Endgame", "3h 2m"), Film("The Dark Knight", "2h 32m"), Film("Inception", "2h 28m")]
    salons = [Salon("Salon A", 50), Salon("Salon B", 30), Salon("Salon C", 20)]
    seanslar = [Seans(films[0], salons[0], "2023-05-09", "15:00"), Seans(films[0], salons[0], "2023-05-09", "19:00")
    , Seans(films[1], salons[1], "2023-05-09", "16:00"), Seans(films[1], salons[1], "2023-05-09", "20:00"), Seans(films[2], salons[2], "2023-05-09", "17:00"), Seans(films[2], salons[2], "2023-05-09", "21:00")]

    # kullanicinin film ve seanslari secip rezervasyon yapmasini saglama
    film = choose_film(films)    
    seans = choose_seans(film, seanslar)
    make_reservation(seans)
