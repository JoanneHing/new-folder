# Academy Assist: MVP Feature List

## Add student contact: `add`
### Purpose
Allow user to add new student contact and details into the management system. It add students’ personal details and contact information into the system if they are successfully enrolled into the tuition centre.

### The Precise Command Format
`add n/[NAME] ic/[IC/FIN NUMBER] e/[EMAIL] p/[PHONE NUMBER] a/[ADDRESS] c/[CLASS TAKEN] y/[Academic Year]`

#### Example commands
`add n/John Doe ic/T384859A e/johndoe@gmail.com p/81003999 a/9 Smith Street c/Science1 y/Standard1`

#### Acceptable values for each parameter
- **NAME**:
    - Not Empty: As name is essential to identify the student.
    - Length: Between 1-100 characters. 
    - Case non-sensitive: As 'John Doe' and 'john doe' are the same. Name need not be case-sensitive.
    - Accepts latin alphabet and space: As we focus on the English format which is widely used in Singapore.
    - Error displayed if format is incorrect:
      `The name entered is invalid. Please make sure the name is between 1-100 characters and only contains alphabets and spaces.`


- **IC/ FIN NUMBER**:
  - Not empty: As IC/ FIN number is essential to identify the student.
  - Follow format of Singaporean IC and FIN number: As the system is designed for a Singapore based tuition center, the students are either Singaporean or Permanent Resident.
      - First letter: S/T/F/G/M
      - 7 digits: The unique identification number assigned to the individual.
      - Last letter: Checksum letter based on previous digits.
  - Error displayed if format is incorrect:
      `The IC/ FIN number entered is invalid. Please make sure the IC/ FIN number 9 characters long and follows the format of a Singaporean IC/ FIN number.` 


- **PHONE NUMBER**:
    - Not empty: As phone number is essential to contact the student or parent.
    - 8 digit number: 0-9. As phone number in Singapore is 8 digits long.
    - No space or other characters.
    - Error displayed if format is incorrect:
      `The phone number entered is invalid. Please make sure the phone number is 8 digits long and only contains numbers.`


-   **EMAIL**:
    - Allow empty: As email is not essential to contact the student or parent.
    - Not case-sensitive: As emails are not case-sensitive.
    - Format: username@domain.
      - Accepts latin alphabet and requires an “@”.
    - No space.
    - Error displayed if format is incorrect:
      `The email entered is invalid. Please make sure the email is in the format of username@domain.`


-   **Address**:
    - Allow empty: As address is not essential to contact the student or parent.
    - Not case-sensitive: As address is not case-sensitive.
    - Accepts latin alphabet, any other symbols, space.

-  **Class Taken**:
    - At least one: As student must be enrolled in at least one class.
    - Not case-sensitive: As the class taken is not case-sensitive.
    - Combination of Subject and Number: `Science1`
    - No space in between
    - Error displayed if format is incorrect:
      `The class taken entered is invalid. Please make sure the class taken is in the format of [Subject][Number].`

-  **Academic Year**:
    - Not empty: As every student must be enrolled in an academic year.
    - Not case-sensitive: As the academic year is not case-sensitive.
    - Standard[Num]: `Standard1`
    - No space in between
    - Error displayed if format is incorrect:
      `The academic year entered is invalid. Please make sure the academic year is in the format of Standard[Number].`

#### Error message if the value is not acceptable
Display the error message at the text display below text filed.
```
Error: Invalid command format. Please use the format: add n/[NAME] ic/[IC/FIN NUMBER] e/[EMAIL] p/[PHONE NUMBER] a/[ADDRESS] c/[CLASS TAKEN] y/[Academic Year]"
```
### Expected outputs when the command
#### Succeeds
A success message is shown to indicate that the new student has been successfully added into the system.
>> StudentID with 5 digits is generated automatically by the system. This is used to track the student in the system and used for other commands.
```
Student [StudentID] : [StudentName] is successfully added.
```

#### Fails
Error message is shown to tell the user that the input is in an incorrect format, and what the correct format should be
```
Failed to add new student, please try again. Ensure that the command follow the format: 
add n/[NAME] ic/[IC/FIN NUMBER] e/[EMAIL] p/[PHONE NUMBER] a/[ADDRESS] c/[CLASS TAKEN] y/[Academic Year]`
```

### Duplicate handling
- Checks IC/FIN number against existing contact. As IC/ FIN number is unique to each individual.
- If duplicate is found, an error message is shown to indicate that the student is already in the system.
```
Student [STUDENTID] : [NAME] already exists in the system. Please check the student details and try again.
```

### Relevant UI mock-ups

---

## Delete student contact: `del`
### Purpose
Remove a student contact from the management system. It deletes student’s personal details and contact information if they leave the tuition center.

### The Precise Command Format
`del [Student ID]`


#### Example commands
`del 12345`

#### Acceptable values for each parameter
- **Student ID**:
    - Not empty: As student ID is essential to identify the student.
    - Length: 5 digits.
    - Accepts only numbers from 0-9. No space or other characters.
    - Error displayed if format is incorrect:
      `Incorrect input format. Please try again using del [Student ID]. Ensure that the Student ID is 5 digits long and only contains 0-9.`

### Expected outputs when the command
#### Succeeds
Message is shown to indicate that the contact has been successfully deleted
```
Student [STUDENTID] : [NAME] is successfully deleted
```

#### Fails
Error message is shown to tell the user that the execution failed. Remind the user the correct format to use.
```
Incorrect input format. Please try again using del [Student ID]
```

### Duplicate handling
Not applicable

### Relevant UI mock-ups

---

## Edit student contact: `edit`
### Purpose
Edit a student details in the management system. It changes student’s personal details and contact information if there are updates to be made.

### The Precise Command Format
`edit [Student ID] [field: new_input]`


#### Example commands
`edit 12345 Address:new_address`

#### Acceptable values for each parameter
- **Student ID**:
    - Not empty: As student ID is essential to identify the student.
    - Length: 5 digits.
    - Accepts only numbers from 0-9. No space or other characters.
    - Error displayed if format is incorrect:
      `Incorrect input format. Please try again using edit [Student ID] [field: new_input]. Ensure that the Student ID is 5 digits long and only contains 0-9.`
- field:
    - Only Phone Number, Address, Class Taken and Academic Year will be accepted.
    - new_input:
        - If the field is a Phone Number, 8 digit number, 0-9. No space or other characters.
        - If the field is an Address, allow empty. Case-sensitive. Accepts latin alphabet, any other symbols, space.
        - If the field is a Class Taken, Combination of Subject and Number: `Science1`. No space in between.
        - If the field is an Academic Year, only allow Standard1, Standard2, Standard3, Standard4, Standard5 and Standard6
        - Error displayed if format is incorrect:
          `Student information cannot be changed due to incorrect input format. Please try again using edit [Student ID] [field: new_input]`

### Expected outputs when the command
#### Succeeds
Message is shown to indicate that the contact’s information has been successfully changed.
```
Student [Student ID] [StudentName] successfully changed. Here is their updated information [PHONE NUMBER] [ADDRESS] [CLASS TAKEN] [ACADEMIC YEAR]
```

#### Fails
Error message is shown to tell the user that the update failed. Remind the user the correct format to use.
```
Student information cannot be changed due to incorrect input format. Please try again using edit [Student ID] [field: new_input]
```

### Duplicate handling
Not applicable

### Relevant UI mock-ups

---

## View (or List) All Students’ Contact Details: `view`
### Purpose
Allow user to view all the student contact details in the management system. It shows all the students’ personal details and contact information that are enrolled in the tuition centre.

### The Precise Command Format
`view`

#### Example commands
`view`

#### Acceptable values for each parameter
Not Applicable. No parameter is expected for this command.
Trailing white spaces will be treated as the same as command without white space
Error displayed if format is incorrect:
```
Incorrect input format. Please try again using view only.
```

### Expected outputs when the command
#### Succeeds
All the students’ contacts and details will be shown on the UI in decreasing order of Student ID.
```
There is a total of [NUMBER OF STUDENTS] students in the system. Here are the details of the students:
```

#### Fails
An error message displayed to indicate to the user that an error had occurred or an invalid command has been entered
```
Unable to view the students’ contacts and details. Please try again. Type in help for the list of commands.
```

### Duplicate handling
Not applicable

### Relevant UI mock-ups

---
## Search specific Student Contact (By StudentName): `find`

### Purpose
Allow user to search for a specific student contact in the management system. It shows the student’s personal details and contact information that matches the given input.

### The Precise Command Format
`find [StudentName]`

#### Example commands
`find John Doe`

#### Acceptable values for each parameter
- **StudentName**:
    - Not empty: As student name is essential to identify the student.
    - Length: Between 1-100 characters.
    - Case non-sensitive: As 'John Doe' and 'john doe' are the same. Name need not be case-sensitive.
    - Accepts latin alphabet and space: As we focus on the English format which is widely used in Singapore.
    - Error displayed if format is incorrect:
      `The name entered is invalid. Please make sure the name is between 1-100 characters and only contains alphabets and spaces.`

### Expected outputs when the command
#### Succeeds
Details of students whose name matches the given input will be displayed on the UI
```
Number of students] student(s) found that matches the name [NAME].
```

#### Fails
Error message will be shown to indicate invalid input, e.g. missing parameter, and remind the user what the correct format should be
```
Search faild. Please specify the name of the student you are searching for in this format: find [NAME]
```

### Duplicate handling
Display all the students that match the name entered by the user

### Relevant UI mock-ups

---

## Add class taken by a student (class is associated with a subject): `addc`

### Purpose
Allow user to add a class taken by a student in the management system. It adds the class taken by the student and the subject associated with the class.

### The Precise Command Format
`addc [Student ID] [ClassName]`

#### Example commands
`addc 12345 Science1`

#### Acceptable values for each parameter
- **Student ID**:
    - Not empty: As student ID is essential to identify the student.
    - Length: 5 digits.
    - Accepts only numbers from 0-9. No space or other characters.
    - Error displayed if format is incorrect:
      `The studentID entered is invalid. Please make sure the studentID is 5 digits long and only contains 0-9.`
- **ClassName**:
    - Not empty: As class name is essential to identify the class.
    - Combination of Subject and Number: `Science1`
    - No space in between
    - Error displayed if format is incorrect:
      `The class name entered is invalid. Please make sure the class name is in the format of [Subject][Number].`
    - 
### Expected outputs when the command
#### Succeeds
Message is shown to indicate that the class taken by the student has been successfully added.
```
Added [StudentName] to [ClassName]
```

#### Fails
Error message is shown to tell the user that the execution failed. Remind the user the correct format to use.
```
Failed to add class taken by student. Please try again using addc [Student ID] [ClassName]
```

### Duplicate handling
If a student already has that subject attached to him/her, an error message is shown to indicate that the student is already taking that subject.
```
Student is already taking that subject. Please check the student details and try again.
```

### Relevant UI mock-ups

---

## Sort Contacts (By Field): `sort`

## Purpose
Sort students in order of [specified field]. To show students in alphabetical order of names OR based on class

### The Precise Command Format
`sort [Field]`

Field: name, class

#### Example commands
`sort name`
`sort class`

#### Acceptable values for each parameter
Only name and class are accepted as fields to sort the students by.
Error displayed if format is incorrect:
```
Invalid field. Please try again using sort [Field]. Ensure that the field is either name or class.
```

### Expected outputs when the command
#### Succeeds
All the students' contacts and details will be displayed in ascending order based on the field specified.

#### Fails
An error message displayed to indicate to the user that an error had occurred or an invalid command has been entered
```
Failed to sort the students. Please try again. Type in help for the list of commands.
```

### Duplicate handling
If students have the same name or class, sort in order of student id

### Relevant UI mock-ups

---
## Clear the contact book: `clear`
### Purpose
Clear all the data in the contact book. It removes all the data in the contact book.

### The Precise Command Format
`clear`

#### Example commands
`clear`

#### Acceptable values for each parameter
Not Applicable. No parameter is expected for this command.
Error displayed if format is incorrect:
```
Incorrect input format. Please try again using clear only.
```

### Expected outputs when the command
#### Succeeds
Message is shown to indicate that the contact book has been successfully cleared.
```
All the students' contact is successfully removed
```

#### Fails
An error message displayed to indicate to the user that an error had occurred or an invalid command has been entered
```
Failed to clear the contact book. Please try again. Type in help for the list of commands.
```

### Duplicate handling
Not applicable

### Relevant UI mock-ups

---
## Display User Guide: `help`
## Purpose
Show help message about the features to guide user through the features.

### The Precise Command Format
`help`

#### Example commands
`help`

#### Acceptable values for each parameter
No parameter is expected for this command.
Error displayed if format is incorrect:
```
Incorrect input format. Please try again using help only.
```

### Expected outputs when the command
#### Succeeds
A pop up window displaying the help message
```
Here are the list of commands:
1. add n/[NAME] ic/[IC/FIN NUMBER] e/[EMAIL] p/[PHONE NUMBER] a/[ADDRESS] c/[CLASS TAKEN] y/[Academic Year]
2. del [Student ID]
3. edit [Student ID] [field: new_input]
4. view
5. find [StudentName]
6. addc [Student ID] [ClassName]
7. sort [Field]
8. clear
9. help
```

#### Fails
A error message saying command not valid and inform user can use the help command to see the list of command
```
The command fails, please try again, type in help for the list of commands
```

### Duplicate handling
Not applicable

### Relevant UI mock-ups
