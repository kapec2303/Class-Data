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

    Date(const Date &d) {
        year = d.year;
        month = d.month;
        day = d.day;
        hour = d.hour;
        minute = d.minute;
        second = d.second;
    }

    bool OurEra() {
        if (year > 0) {
            isOurEra = true;
        } else {
            isOurEra = false;
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
Date add(int y, unsigned mon, unsigned int d, unsigned int h, unsigned int minutes, unsigned int sec) {
        Date AddDate = *this + Date(y, mon, d, h, minutes, sec);
        return AddDate;
    }
Date subtract(int y, unsigned mon, unsigned int d, unsigned int h, unsigned int minutes, unsigned int sec) {
        Date SubDate = *this - Date(y, mon, d, h, minutes, sec);
        return SubDate;
    }
    //перегрузка +, +=, -, -=, =, >, <, ==.
Date operator+(Date date) {
        Date result = *this;
        result.year = result.year + date.year;
        return result;
    }
Date operator+=(int date) {
        this->year += date;
        return *this;
    }
Date operator-(Date date) {
        Date result = *this;
        result.year = result.year - date.year;
        return result;
    }
Date operator-=(int date) {
        this->year -= date;
        return *this;
    }
Date operator=(Date date) {
        this->year = date.year;
        this->month = date.month;
        this->day = date.day;
        this->hour = date.hour;
        this->minute = date.minute;
        this->second = date.second;
        this->isOurEra = date.isOurEra;
        return *this;
    }
bool operator<(Date date) {
    if (this->year < date.year) {
        return true;
        //Я сначала пытался сделать сравнение нормально, но не получилось :(
    } else {
        return false;
    }
}
bool operator>(Date date) {
    if (this->year > date.year) {
        return true;
    } else {
        return false;
    }
}
bool operator==(Date date) {
        if ((this->year == date.year) and (this->month == date.month) and (this->day == date.day) and (this->hour == date.hour) and (this->minute == date.minute) and (this->second == date.second)) {
            return true;
        } else {
            return false;
        }
    }
friend ostream &operator<<(std::ostream &out, const Date &date) {
    out << "year: " << date.year << " month: " << date.month << " day: " << date.day
            << " hour: " << date.hour << " minutes: " << date.minute << " seconds: " << date.second << " "
            << (date.isOurEra ? " our era" : " before our era");
        return out;
    }
};


int main() {
    //Date def1;
    Date today(2023, 11, 17, 21, 51, 23);
    Date tomorrow(2023, 11, 18, 12, 00, 00);
    today.Monts_and_Days();
    today.OurEra();
    today.Time();
    Date d(today);
    cout << d.year << " " << d.month << " ... " << endl;
    Date res = today + tomorrow;
    cout << " + " << res.year << endl;
    res += 2;
    cout << " += " << res.year << endl;
    res = today - tomorrow;
    cout << " - " << res.year << endl;
    res -= 2;
    cout << " -= " << res.year << endl;
    res = today;
    res -= 2;
    cout << " = " << res.year << " " << res.month << " " << res.day << endl;
    cout << " < " << ( res < tomorrow) << endl;
    cout << " > " << ( res > tomorrow) << endl;
    cout << " == " << ( res == res ) << endl;
    cout << today;
    return 0;
}
