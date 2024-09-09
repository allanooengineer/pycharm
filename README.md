# pycharm
import unittest
class InvalidSalesItemError(Exception):
    pass



class MenuItems:
    def __init__(self, name, wholesalecost, sellingprice):
        self._name = name
        self._wholesalecost = wholesalecost
        self._sellingprice = sellingprice

    def get_name(self):
        return self._name

    def get_wholesalecost(self):
        return self._wholesalecost

    def get_sellingprice(self):
        return self._sellingprice

# Create objects from the MenuItems class
order1 = MenuItems("Smochamayai", "40.00", "50.00")
order2 = MenuItems("Smochasmokie", "55.00", "60.00")
order3 = MenuItems("Smokiepasua", "30.00", "45.00")
order4 = MenuItems("Bajia", "45.00", "75.00")

# Use the getter methods to access and print the values
print(f"name: {order1.get_name()}")
print(f"wholesalecost: {order1.get_wholesalecost()}")
print(f"sellingprice: {order1.get_sellingprice()}")


class SalesForDay:
    def __init__(self, day, sales_dict):
        self._day = day
        self._sales_dict = sales_dict

    def get_day(self):
        return self._day

    def get_sales_dict(self):
        return self._sales_dict




class SmochaStand:
    def __init__(self, name, location):
        self._name = name
        self._location = location
        self._current_day = 0
        self._menu = {}
        self._sales_record = []

    def get_name(self):
        return self._name

    def add_menu_item(self, menu_item):
        self._menu[menu_item.get_name( )] = menu_item

    def enter_sales_for_today(self, sales_dict):
        for item in sales_dict:
            if item not in self._menu:
                sales_for_day = SalesForDay( self._current_day, sales_dict )
        self._sales_record.append( sales_for_day )
        self._current_day += 1

    def sales_of_menu_item_for_day(self, day, item_name):
        for record in self._sales_record:
            if record.get_day( ) == day:
                sales_dict = record.get_sales_dict( )
                return sales_dict.get( item_name, 0 )
        return 0

    def total_sales_for_menu_item(self, item_name):# Online help was obtained at this point
        total_sales = 0
        for record in self._sales_record:
            sales_dict = record.get_sales_dict( )
            total_sales += sales_dict.get( item_name, 0 )
        return total_sales

    def total_profit_for_menu_item(self, item_name):# online assistance was obtained at this point
        total_sales = self.total_sales_for_menu_item( item_name )
        if item_name in self._menu:
            item = self._menu[item_name]
            profit_per_item = float( item.get_sellingprice( ) ) - float( item.get_wholesalecost( ) )
            return total_sales * profit_per_item
        return 0

    def total_profit_for_stand(self):
        total_profit = 0
        for item_name in self._menu:
            total_profit += self.total_profit_for_menu_item( item_name )
        return total_profit




stand = SmochaStand( "Mukuruno", "Kayole" )

item1 = MenuItems( 'Maandazi', 10.00, 15.00 )
stand.add_menu_item( item1 )

item2 = MenuItems( 'Rolex', 85.00, 90.00 )
stand.add_menu_item( item2 )

item3 = MenuItems( 'Smotcha', 56.00, 70.00 )
stand.add_menu_item( item3 )

day_0_sales = {
    'Smotcha': 17,
    'Smotchamayai': 25,
    'rolex':67,
    'maandazi':30,
    'smokiepasua':87,
    'soda':65

}

try:
    stand.enter_sales_for_today( day_0_sales )
except InvalidSalesItemError as e:
    print( e )

print( f"Smotcha profit = {stand.total_profit_for_menu_item( 'Smocha' )}" )
print( f"rolex profit = {stand.total_profit_for_menu_item( 'HotDog' )}" )


def main():
    pass


if __name__ == "__main__":
    main( )

