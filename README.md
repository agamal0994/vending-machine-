# vending-machine-
#include <iostream>

using namespace std;
class Stock {
public :
    string Item[10]= {"tea:3LE", "coffee:5LE", "ice cream:7.5LE","cola:4LE", "pepsi:4LE", "toy:6.5", "snickers:8.5LE", "nescafe:7LE", "chips:2.5LE", "wiver:10LE"};
    int Amount[10]= {10,10,10,10,10,10,10,10,10,10};
    double price[10] = {3,5,7.5,4,4,6.5,8.5,7,2.5,10};
public :
    bool isavailable(int chooseditem){
        if(Amount[chooseditem - 1]>0){
            return true ;
        }
        else {
            return false ;
        }
    }
    void print()
    {
        for (int i = 0 ; i < 10 ; i++)
        {

            cout << Item[i] << " :::::: " << Amount[i] << endl;
        }
    }
};
//-------------------------------------------------------------------
class Coin_Handler{
public :
    int LE_5 =0;
    int LE_20 =0;
    int LE_10 =0;
    int LE_1 =0;
    int LE_05 =0;

    void identifycoin(double money ){
        while(money>= 20){
            money -=20;
            LE_20 ++ ;
        }
        while(money>= 10){
            money -=10;
            LE_10 ++ ;
        }
        while(money >= 5){
            money -=5;
            LE_5 ++ ;
        }
        while(money >= 1){
            money -=1;
            LE_1 ++ ;
        }
        while(money >= 0.5){
            money -=0.5;
            LE_05 ++ ;
        }
    };
    void returnamount(){
        cout <<LE_20 << " of 20.LE" << endl ;
        cout <<LE_10 << " of 10.LE" << endl ;
        cout <<LE_5 << " of 5.LE" << endl ;
        cout <<LE_1 << " of 1.LE" << endl ;
        cout <<LE_05 << " of 0.5.LE" << endl ;
    };
};
//---------------------------------------------------------
//---------------------------------------------------------
class Vending_machine : public Coin_Handler , public Stock{
public :
    double money;
    int chooseditem ;
    int amount ;
    double bill;
public :
    int chooseitem(){
        cout << "please choose item :" <<endl ;
        cin >> chooseditem ;
        while (chooseditem > 10 || chooseditem < 1 ){
            cout << "not valid choice  , re enter choice " <<endl ;
            cin >> chooseditem ;
        }
        chooseditem-=1 ;
        return chooseditem ;
    }
    void chooseamount(){
        cout << "choose amount  : " << endl ;
        cin >> amount ;
        while (amount > Amount[chooseditem]){
            cout << "overloaded amount  please re enter ...."<<endl ;
            cin >> amount ;
        }
        Amount[chooseditem]= Amount[chooseditem] - amount ;
    }
    void  insertmoney(){
        cout << "enter money :" << endl ;
        cin >> money ;
        money -=price[chooseditem]*amount ;
        while (money < 0 ){
            cout << "your cash isn't enough re enter money " << endl ;
            cin >> money ;
        }
        cout << "the rest :"<< money << endl ;
    }

};
//-------------------------------------------------------------------
class Food_item : public Stock{
protected :
    string name ;
    double price ;
public :
    string getname()
    {
        return name;
    }
    double getprice()
    {
        return price ;
    }
};
int main()
{
    Stock ob;
    Vending_machine ov;
    Coin_Handler ok;
     while (true){
    ob.print();
    ov.chooseitem();
    if (ob.isavailable(ov.chooseditem ==true)){
       ov.chooseamount();
       ov.insertmoney();
       ok.identifycoin(ov.money) ;
       ok.returnamount();
    }else {
        cout << "this item finished " << endl ;
    }
    }


    return 0;
}
