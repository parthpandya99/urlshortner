import mysql.connector

mydb = mysql.connector.connect(
  host="localhost",
  user="root",
  password="toor",
  database = "urlconverter"
)
mycursor = mydb.cursor()

dictionary = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
base  = 62 #[a-zA-z] = 52, [0-9] = 10, i.e. 52 + 10 = 62

def enter_into_db(string):
    # sql = "INSERT INTO urls original_url VALUES %s"
    # val = (string,)
    mycursor.execute("INSERT INTO urls (original_url) VALUES (%s)", (string,))
    mydb.commit()


def get_from_db(num):
    sql = "SELECT original_url FROM customers WHERE id = (%s)"
    val = (num,)
    mycursor.execute(sql%(int),val)
    mydb.commit()
    og_url = mycursor.fetchall()
    return og_url




def encode(nu):
    string  = ""
    num = (int)(nu)
    while(num > 0):
        string += dictionary[num % base]
        num = num / base

    return string[::-1]

def decode(string):
    num = 0
    for i in range(len(string)):
        num *= base + dictionary.index(string[i])

    return num


def main():
    lurl = input("Enter the long URL")
    enter_into_db(lurl)
    num = 1
    surl = encode(num)
    print("Shortened URL:   "+surl)
    num += 1
    rnum = decode(surl)
    og_url = get_from_db(rnum)


main()

mydb.close()
