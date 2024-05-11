# TimeSculpt

NMIMS MPSTME Time table creation project

## TechStack Used

- Python

## Tasks

- create class: constraints, relations
- Backtracking algorithm that gets called recursively, for every new assignment
- Dictionary with { var : domain }, objects of class constraint are in the dictionary, segregated variable wise
- Define all vars, their domains and constraints.

### Classes

#### Constraints Class

- Dynamically Adding Constraints
- Check Consistency in TimeTable
- Assignment Check
- Get Unassigned Variables
- Get Domain
- Gen_domain fucntion to map all domains to vars
- var1 => object
- relationship => object
- Classes for:
  - Subjects:
    - sub_code: UID for each subject so its easier to process it compared to having strings for each
    - sub_name: string name for the subject, wont be processed by the algorithm, saved in a seperate CSV file, later reassigned based on the subject code
    - Sub_sem: int
    - sub_steam: UID
    - sub_course: UID
    - sub_theory: int
    - sub_lab: int
  - Faculties:
    - fac_id: UID
    - fac_sub_code: Array
    - fac_teach_opt: Empty, Array
    - fac_visfac: Bool (are they a visiting faculty or not)
    - fac_timing_constraint: Empty, Array
  - Rooms:
    - Type: int (type of room, map each type of room to an int, like- lab:0 computer-room:1... etc)
    - Max_cap: int (max students that can be fitted in the room)
    - Time: int (avialability of the rooms)
  - Timings:
    - 8:00 - 9:00
    - 9:00 - 10:00
    - 10:00 - 11:00
    - 11:00 - 12:00
    - 12:00 - 13:00
    - 13:00 - 14:00
    - 14:00 - 15:00
    - 15:00 - 16:00
    - 16:00 - 17:00
    - 17:00 - 18:00
    - 18:00 college closes rooms
    <!-- Unconfirmed constraints: -->
  - consecutivity_check() there cant be more than 3 classes in a row
  - max_days_check() each class should get at least 1 day off
  - max_hours_check() each class can only attend a max of X hours in a day
  - subject_hours_check() every subjects hours must be complete
  - skipped_classes_check() account for the number of hours of classes that will be skipped due to public holidays, etc that will need to be rescheduled, print these as outliers
  -

#### Relations Class

- Functions for each relation
- Satisfied function:
- relationship_check()
  {
  function to check all < , >, =, <=, >=, !=
  }
- example:
  def smaller(x,y):
  return x<y

  def greater(x,y):
  return x>y

  def equal(x,y):
  return x==y

  def l_eq(x,y):
  return x<=y

  def g_eq(x,y):
  return x>=y

  def n_eq(x,y):
  return x!=y

  n1 = int(input("Value 1: "))
  n2 = int(input("Value 2: "))

  print(smaller(n1,n2))
  print(greater(n1,n2))
  print(equal(n1,n2))
  print(l_eq(n1,n2))
  print(g_eq(n1,n2))
  print(n_eq(n1,n2))

- satisfied(var1_val, var2_val) =>bool return type
  {
  if relationship_check(var1_val, var2_val)
  {
  return True
  }
  return False
  }

- consistent( list : constraints):
  returns True if all constraints satisfied
  else False

<!-- idk -->

- get_unassigned vars
  get_uns_var(dict : matching_dict):
  returns no. of unmatched keys in dictionary

### Backtracking Algorithm

- Backtracking is a general algorithmic technique used to solve problems by incrementally building a solution and undoing certain choices when they are found to be incorrect or lead to a dead end.

- It is commonly used in situations where we need to explore all possible combinations or permutations of a solution space.

- In TimeSculpt project it is used for time table creation. The backtracking algorithm is called recursively for every new assignment, it is used to explore different possibilities and find a valid assignment for the time table, based on the defined constraints.

- The backtracking algorithm in this project involves making choices for each variable (e.g., assigning a time slot to a particular class) and then recursively exploring the remaining variables and their possible assignments.

- If a choice leads to a contradiction or violates a constraint, the algorithm backtracks and tries a different choice.

- By using backtracking, the project can systematically explore different combinations of assignments until a valid time table is found or determine that no valid solution exists.

### Algorithm used:

1. Check if all vars assigned,

   - if yes: return assignments
   <!-- - if no, recursively call -->

2. Get all un-assigned vars {'v'}

3. for i in v
   for j in v.domain
   local-assign; assign j to v
   check if constraints are satisfied - if yes: assign value - if no: recursively backtrack and check for appropriate assignment
