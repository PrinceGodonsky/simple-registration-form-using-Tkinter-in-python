import tkinter as tk
from tkinter import ttk, messagebox

window = tk.Tk()
window_title = window.title("Data Entry Form")
geometry = window.geometry("500x400")
frame = tk.Frame(window)
frame.pack()

labelf = tk.LabelFrame(frame, text="Personal Information")
labelf.grid(row=0, column=0, padx=20, pady=10)
first_name = tk.Label(labelf, text="First Name:")
first_name.grid(row=0, column=0)
last_name = tk.Label(labelf, text="Last Name:")
last_name.grid(row=0, column=1)

def enter_data():
    if not firstname_entry.get() or not lastname_entry.get():
       messagebox.showerror("Input Error", "First Name and Last Name can't be empty")
    if terms_check_var.get() == "Disagree":
       messagebox.showwarning( title="Warning", message="You must agree to the terms and conditions to continue")
    
    
    first = firstname_entry.get()
    last = lastname_entry.get()
    title = title_combo.get()
    age = age_spinbox.get()
    nationality = nationality_combo.get()
    registration_status = reg_status_var.get()
    num_courses = num_courses_spinbox.get()
    num_semesters = num_semesters_spinbox.get()
    

    message_text = (
        f"Full Name: {title} {first} {last}\n"
      
        f"Age: {age}\n"
        f"Nationality: {nationality}\n"
        f"Number Of Semester: {num_semesters}\n"
        f"Number Of Courses: {num_courses}\n"
        f"Registration status: {registration_status}\n"
        
    )
    messagebox.showinfo("User Information" , message_text)
    print(message_text)
    filename = f"personal_data_entry.txt"

    try:
        with open(filename, "a" ) as file:
            file.write(message_text)
           
            messagebox.showinfo("Success", "Entry saved successfully!\n")
           
    except IOError as e:
        messagebox.showerror("Error", f"Failed to save entry: {e}")



firstname_entry = tk.Entry(labelf)
firstname_entry.grid(row=1, column=0)
lastname_entry = tk.Entry(labelf)
lastname_entry.grid(row=1, column=1)
title = tk.Label(labelf, text="Title:")
title_combo = ttk.Combobox(labelf, values=["Mr.", "Mrs.", "Miss", "Bro.", "Sis.", "Dr.", "Prof.", "Rev", "Ms."])
title_combo.set("Select Title")
title_combo.grid(row=1, column=2)
title.grid(row=0, column=2)


age_label = tk.Label(labelf, text="Age:")
age_spinbox = tk.Spinbox(labelf, from_=18, to=100)
age_spinbox.grid(row=3, column=0)
age_label.grid(row=2, column=0)

nationality_label = tk.Label(labelf, text="Nationality:")
nationality_combo = ttk.Combobox(labelf, value=["Kenya", "Uganda", "Tanzania", "Rwanda", "Nigeria", "South Africa", "Zambia", "Zimbabwe", "Ghana", "Malawi", "Botswana", "USA", "Cameroon"])
nationality_combo.set("Select Nationality")
nationality_combo.grid(row=3, column=1 )
nationality_label.grid(row=2, column=1)

for widget in labelf.winfo_children():
    widget.grid_configure(padx=10, pady=5)

course_frame = tk.LabelFrame(frame, text="Course Information")
course_frame.grid(row=1, column=0, sticky="news", padx=20, pady=10)

registered_label = tk.Label(course_frame, text="Registration Status")
reg_status_var = tk.StringVar(value="Not Registered")
registered_check = tk.Checkbutton(course_frame, text="Currently Registered",
                                  variable=reg_status_var, onvalue='Registered', offvalue='Not Registered')
registered_check.grid(row=1, column=0)
registered_label.grid(row=0, column=0)

num_courses_label = tk.Label(course_frame, text="Number of Courses:")
num_courses_spinbox = tk.Spinbox(course_frame, from_=0, to="15")
num_courses_spinbox.grid(row=1, column=1)
num_courses_label.grid(row=0, column=1)

num_semesters_label = tk.Label(course_frame, text="Number of Semesters:")
num_semesters_spinbox = tk.Spinbox(course_frame, from_=0, to="10")
num_semesters_spinbox.grid(row=1, column=2)
num_semesters_label.grid(row=0, column=2)

for widget in course_frame.winfo_children():
    widget.grid_configure(padx=10, pady=5)

terms_frame = tk.LabelFrame(frame, text="Terms & Conditions")
terms_frame.grid(row=2, column=0, sticky="news", padx=20, pady=10)
terms_check_var =tk.StringVar(value="Disagree")
terms_check = tk.Checkbutton(terms_frame, text="I agree to the terms and conditions",
                             variable=terms_check_var, onvalue="Agree", offvalue="Disagree")

terms_check.grid(row=0, column=0)

button = tk.Button(frame, text="Enter Data", command=enter_data)
button.grid(row=3, column=0, sticky="news", padx=20, pady=10)


window.mainloop()
