import matplotlib.pyplot as plt
import pickle
def create_rec():
    print("\n")
    f=open("Student.dat", 'wb')
    L=[]
    while True:
        Adm_no=int(input("Enter Adm Number of Student: "))
        Stud_name=input("Enter name of student: ")
        Percentage = float(input("Enter the percentage: "))
        L.append([Adm_no, Stud_name, Percentage])
        ch=input("Do you want to enter more records?(Y/N) ")
        if ch in 'yY':
            continue
        else:
            break
    pickle.dump(L, f)
    f.close()

def display_all():
    print("\n")
    try:
        f=open("Student.dat","rb")
        R=pickle.load(f)
        for i in R:
            print(i)
    except:
        print("file not found")

def append_rec():
    print("\n")
    f=open("Student.dat", 'rb+')
    R=pickle.load(f)
    while True:
        Adm_no=int(input("Enter Adm Number of Student: "))
        Stud_name=input("Enter name of student: ")
        Percentage = float(input("Enter the percentage: "))
        R.append([Adm_no,Stud_name,Percentage])
        ch=input("Do you want to enter more records?(Y/N) ")
        if ch in 'yY':
            continue
        else:
            break
    f.seek(0)
    pickle.dump(R, f)
    f.close()
def search_rec():
    print("\n")
    try:
        f=open("Student.dat", 'rb')
        R=pickle.load(f)
        A=int(input("Enter admission number to search: "))
        for i in R:
            if i[0]==A:
                print("Record found")
                print(i)
                break 
        else:
            print("Record not found")
    except FileNotFoundError:
        print("File not found")
    f.close()
def sort_rec(Ch,col):
    try:
        f=open("Student.dat", 'rb+')
        R=pickle.load(f)
        N=len(R)
        for i in range(N-1):
            for j in range(N-i-1):
                if Ch in 'aA':
                    if R[j][col] > R[j+1][col]:
                        R[j],R[j+1]=R[j+1],R[j]
                else:
                    if R[j][col] < R[j+1][col]:
                        R[j],R[j+1]=R[j+1],R[j]
        f.seek(0)
        pickle.dump(R,f)
        f.close()
    except FileNotFoundError:
        print("File not found")
def delete_rec():
    try:
        f=open("Student.dat","rb+")
        R=pickle.load(f)
        L=[]
        A=int(input("Enter admission number to delete: "))
        for i in R:
            if i[0]==A:
              continue
            L.append(i)
        f.seek(0)
        pickle.dump(L,f)
    except FileNotFoundError:
        print("File not found")

def plot_data():
    try:
        f = open("Student.dat", "rb")
        R = pickle.load(f)
        f.close()
        names = [i[1] for i in R]         # student names
        percentages = [i[2] for i in R]   # student percentages
        plt.figure(figsize=(8,5))
        plt.bar(names, percentages)
        plt.xlabel("Students")
        plt.ylabel("Percentage")
        plt.title("Student Performance")
        plt.xticks(rotation=45)
        plt.tight_layout()
        plt.show()
    except FileNotFoundError:
        print("File not found")


while True:
    print("\n\n")
    print("\t\tMAIN MENU")
    print("*********************************************")
    print("1. Create Record")
    print("2. Display Record")
    print("3. Append Record")
    print("4. Search Record")
    print("5. Sort Record")
    print("6. Delete Record")
    print("7. Plot Data")
    print("8. Quit")
    print("*********************************************")
    choice=int(input("Enter your choice ---->"))
    if choice==1:
        create_rec()
    elif choice==2:
        display_all()
    elif choice==3:
        append_rec()
    elif choice==4:
        search_rec()
    elif choice==5:
        ch=input("Enter 'A' for ascending and 'D' for descending:")
        basis=int(input("Enter 0 to sort according to Admission no. , 1 to sort according to Name and 2 to sort according to Percentage:"))
        sort_rec(ch,basis)
    elif choice==6:
        delete_rec()
    elif choice ==7:
        plot_data()
    elif choice==8:
        break 
    else:
        print("\nWrong Choice!\n\nTry again")
        print("\nWrong Choice!\n\nTry again")
