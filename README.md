#include <iostream>
using namespace std;
class Date {
private:
//    int year{1960};
//    unsigned int month{1};
//    unsigned int day{1};
//    unsigned int hour{0};
//    unsigned int minute{0};
//    unsigned int second{0};
//    bool isOurEra{true};

public:
    int year{1960};
    unsigned int month{1};
    unsigned int day{1};
    unsigned int hour{0};
    unsigned int minute{0};
    unsigned int second{0};
    bool isOurEra{true};

    Date() {}

    Date(int y, unsigned mon, unsigned int d, unsigned int h, unsigned int minutes, unsigned int sec)
            : year(y), month(mon), day(d), hour(h), minute(minutes), second(sec) {}

    bool OurEra() {
        if (year > 0) {
            isOurEra = true;
        }
    }

    void Monts_and_Days() { //проверка дней в месяцах и самих месяцев
        if (month <= 12) {
            switch (month) {
                case 2:
                    if ((year % 4 == 0) and ((year % 100 != 0) or (year % 400 == 0))) {
                        if (day > 29) {
                            cout << "Error in Feb" << endl;
                        }

                    } else if (day > 28) {
                        cout << "Error in Feb" << endl;
                    }
                    break;
                case 4:
                case 6:
                case 9:
                case 11:
                    if (day > 30) {
                        cout << "Error, more than 30 days" << endl;
                    }
                    break;
                case 1:
                case 3:
                case 5:
                case 7:
                case 8:
                case 10:
                case 12:
                    if (day > 31) {
                        cout << "Error, more than 31 days" << endl;
                    }
                    break;
            }
        } else cout << "Month doesn't exist" << endl;
    }

    void Time() { //проверка часов, минут, секунд
        if ((hour > 24) or (minute > 59) or (second > 59)) {
            cout << "Error in time" << endl;
        }
    }

    //перегрузка +, +=, -, -=, >, <, ==.
Date operator+(Date date) {
        Date result = *this;
        result.year = result.year + date.year;
        return result;
    }
Date operator+=(int date) {
        Date result = *this;
        result.year = result.year + date;
        return result;
    }
};
//БОЛЬШЕ Я НЕ УСПЕЛ, ПРОСТИТЕ :(
int main() {
    //Date def1;
    Date today(2023, 11, 17, 21, 51, 23);
    Date tomorrow(2023, 11, 18, 12, 00, 00);
    today.Monts_and_Days();
    today.OurEra();
    today.Time();
    Date res = today + tomorrow;
    cout << res.year << endl;
    res.year += 2;
    cout << res.year << endl;
    return 0;
}
