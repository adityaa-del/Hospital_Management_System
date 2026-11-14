
import mysql.connector

# CONNECT TO DATABASE
con = mysql.connector.connect(
    host="localhost",
    user="root",
    password="1234",
    database="hospital"
)

cur = con.cursor()


# ADD PATIENT
def add_patient():
    print("\n--- ADD PATIENT ---")

    name = input("Enter patient name: ")
    age = int(input("Enter age: "))
    gender = input("Enter gender: ")
    disease = input("Enter disease: ")
    phone = input("Enter phone number: ")
    admission_date = input("Enter admission date (YYYY-MM-DD): ")

    sql = """INSERT INTO patients
    (name, age, gender, disease, phone, admission_date)
    VALUES (%s,%s,%s,%s,%s,%s)"""

    values = (name, age, gender, disease, phone, admission_date)

    cur.execute(sql, values)
    con.commit()

    print("Patient added successfully!")


# DISPLAY PATIENTS
def display_patients():
    cur.execute("SELECT * FROM patients")
    records = cur.fetchall()

    print("\n--- PATIENT RECORDS ---")

    for row in records:
        print(row)

    if not records:
        print("No patients found.")


# SEARCH PATIENT
def search_patient():
    pid = int(input("Enter Patient ID: "))

    cur.execute(
        "SELECT * FROM patients WHERE patient_id=%s",
        (pid,)
    )

    record = cur.fetchone()

    if record:
        print("Patient Details:", record)
    else:
        print("Patient not found!")


# UPDATE PATIENT
def update_patient():
    pid = int(input("Enter Patient ID: "))

    name = input("Enter new name: ")
    age = int(input("Enter new age: "))
    disease = input("Enter new disease: ")
    phone = input("Enter new phone: ")

    sql = """UPDATE patients
    SET name=%s, age=%s, disease=%s, phone=%s
    WHERE patient_id=%s"""

    cur.execute(sql, (name, age, disease, phone, pid))
    con.commit()

    if cur.rowcount > 0:
        print("Patient updated successfully!")
    else:
        print("Patient not found!")


# DELETE PATIENT
def delete_patient():
    pid = int(input("Enter Patient ID: "))

    cur.execute(
        "DELETE FROM patients WHERE patient_id=%s",
        (pid,)
    )

    con.commit()

    if cur.rowcount > 0:
        print("Patient deleted successfully!")
    else:
        print("Patient not found!")


# ADD DOCTOR
def add_doctor():
    print("\n--- ADD DOCTOR ---")

    name = input("Enter doctor name: ")
    specialization = input("Enter specialization: ")
    phone = input("Enter phone number: ")

    sql = """INSERT INTO doctors
    (name, specialization, phone)
    VALUES (%s,%s,%s)"""

    cur.execute(sql, (name, specialization, phone))
    con.commit()

    print("Doctor added successfully!")


# DISPLAY DOCTORS
def display_doctors():
    cur.execute("SELECT * FROM doctors")
    records = cur.fetchall()

    print("\n--- DOCTOR RECORDS ---")

    for row in records:
        print(row)

    if not records:
        print("No doctors found.")


# MAIN MENU
while True:

    print("\n==============================")
    print("  HOSPITAL MANAGEMENT SYSTEM")
    print("==============================")

    print("1. Add Patient")
    print("2. Display Patients")
    print("3. Search Patient")
    print("4. Update Patient")
    print("5. Delete Patient")
    print("6. Add Doctor")
    print("7. Display Doctors")
    print("8. Exit")

    choice = input("\nEnter your choice: ")

    try:
        if choice == '1':
            add_patient()

        elif choice == '2':
            display_patients()

        elif choice == '3':
            search_patient()

        elif choice == '4':
            update_patient()

        elif choice == '5':
            delete_patient()

        elif choice == '6':
            add_doctor()

        elif choice == '7':
            display_doctors()

        elif choice == '8':
            print("Thank you for using Hospital Management System!")
            break

        else:
            print("Invalid choice!")

    except ValueError:
        print("Please enter valid input.")

    except mysql.connector.Error as e:
        con.rollback()
        print("Database error:", e)


cur.close()
con.close()
