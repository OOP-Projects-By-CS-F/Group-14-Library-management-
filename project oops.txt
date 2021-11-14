
# Create a library class
# display book
# lend book - (who owns the book if not present)
# add book
# return book

# centralLibrary = Library(listofbooks, library_name)

#dictionary (books-nameofperson)

# create a main function and run an infinite while loop asking
# users for their input

from datetime import datetime

class Library:
    def __init__(self, list, name):
        self.booksList = list
        self.name = name
        self.lendDict = {}

    def displayBooks(self):
        print("We have following books in our library:")
        for book in self.booksList:
            print("*",book)

    def lendBook(self, user, book):
        if book not in self.booksList:
            print("Enter valid book name or book not in library")
            return

        if book not in self.lendDict.keys():
            YY = datetime.now().year
            MM = datetime.now().month
            DD = datetime.now().day
            # ****
            print("Enter Year Month and Day")
            flag = True
            while flag:
                try:
                    YY = int(input("YYYY"))
                    MM = int(input("MM"))
                    DD = int(input("DD"))

                    if YY > datetime.now().year or \
                        YY == datetime.now().year and MM > datetime.now().month or\
                        YY == datetime.now().year and MM == datetime.now().month and DD > datetime.now().day:
                        raise Exception("Invalid date")

                    flag = False
                except:
                    print("Enter a valid date")
                    
            # *****
            self.lendDict[book] = [user, datetime(YY,MM,DD)]
            print("Lender-Book database has been updated.  \nYou Can take book Now. \nPlease Keep It safe and return Within 30 Days")
        else:
            print(f"Sorry, This Book is already being used by {self.lendDict[book][0]}. \nPlease wait until the book is avaliable")

    def addBook(self, book):
        self.booksList.append(book)
        print("Book has been added to the book list")

    def returnBook(self, book):
        issueDateDiff = datetime.now() - self.lendDict[book][1]
        del self.lendDict[book]

        if issueDateDiff.days > 30:
            print(f"Your return date has passed. You need to pay fine {(issueDateDiff.days-30) *10} Rupees!")
        
        print("Book returned successfully.")


if __name__ == '__main__':
    central = Library(['Python',  'Rich Dad Poor Dad', 'An Ordinary Age','Artificial Intelligence Revolution','Introduction to Algorithms','Cracking the Coding Interview', 'Harry Potter',  'C++ Basics', 'Algorithms by CLRS'], "central" )
    # print(datetime.date.today().toordinal())

    while(True):

        print(f"====== Welcome to the {central.name} library ======")

        print("1. Display Books")
        print("2. Lend a Book")
        print("3. Add a Book")
        print("4. Return a Book")
        print("Press q to quit")
        print(f"Enter your choice to continue:")

        user_choice = input()

        if user_choice == '1':
            central.displayBooks()

        elif user_choice == '2':
            book = input("Enter the name of the book you want to lend: ")
            user = input("Enter your name: ")
            central.lendBook(user, book)

        elif user_choice == '3':
            book = input("Enter the name of the book you want to add: ")
            central.addBook(book)

        elif user_choice == '4':
            book = input("Enter the name of the book you want to return: ")
            user = input("Enter your name: ")
           
            central.returnBook(book)

        else:
            print ("Thank you for choosing Central Library! Have a great day Ahead!")
            break
            






