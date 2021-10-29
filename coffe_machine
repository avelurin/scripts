class CoffeeMachine:
    
    def __init__(self, water, milk, beans, cups, money):
        self.water = water
        self.milk = milk
        self.beans = beans
        self.cups = cups
        self.money = money
        self.state = "on"
    
    def inputing(self):
        self.command = input("Write action (buy, fill, take, remaining, exit):")
    
    def stoping(self):
            cof_mach.state = "off"

    def filling(self):
        self.water += int(input())
        self.milk += int(input())
        self.beans += int(input())
        self.cups += int(input())
    
    def check_and_make(self, coffe_name):
        if self.water >= coffe_name[0] and self.milk >= coffe_name[1] and self.beans >= coffe_name[2] and self.cups >= coffe_name[3]:
            self.water -= coffe_name[0]
            self.milk -= coffe_name[1]
            self.beans -= coffe_name[2]
            self.cups -= coffe_name[3]
            self.money += coffe_name[4]
            print("I have enough resources, making you a coffee!")
        else:
            print("No, I don't have enough resources")
            
    def chouse(self):
        espresso = [250, 0, 16, 1, 4]
        latte = [350, 75, 20, 1, 7]
        cappuccino = [200, 100, 12, 1, 6]
        self.coffe_code = input("What do you want to buy? 1 - espresso, 2 - latte, 3 - cappuccino:")
        if self.coffe_code == "1":
            self.check_and_make(espresso)
        elif self.coffe_code == "2":
            self.check_and_make(latte)
        elif self.coffe_code == "3":
            self.check_and_make(cappuccino)
            
    def remaining(self):
        print("The coffee machine has:")
        print(self.water, "of water")
        print(self.milk, "of milk")
        print(self.beans, "of coffee beans")
        print(self.cups, "of disposable cups")
        print(self.money, "of money")
    
    def giv(self):
        print("I gave you $", self.money)
        self.money = 0

cof_mach = CoffeeMachine(400, 540, 120, 9, 550)

while cof_mach.state == "on":
    cof_mach.inputing()
    if cof_mach.command == "buy":
        cof_mach.chouse()
    elif cof_mach.command == "fill":
        cof_mach.filling()
    elif cof_mach.command == "take":
        cof_mach.giv()
    elif cof_mach.command == "remaining":
        cof_mach.remaining()
    elif cof_mach.command == "exit":
        cof_mach.stoping()
